---
title: Caso de uso de atributos derivados baseados em decilo
description: Este guia demonstra as etapas necessárias para usar o Serviço de query para criar atributos derivados com base em decil para usar com os dados do perfil.
exl-id: 0ec6b511-b9fd-4447-b63d-85aa1f235436
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1508'
ht-degree: 2%

---

# Caso de uso de atributos derivados baseados em decilo

Atributos derivados facilitam casos de uso complicados para analisar dados do lago de dados que podem ser usados com outros serviços downstream da plataforma ou publicados nos dados do Perfil do cliente em tempo real.

Este exemplo de uso demonstra como criar atributos derivados com base em decil para usar com os dados do Perfil do cliente em tempo real. Usando um cenário de fidelidade de uma companhia aérea como exemplo, este guia informa como criar um conjunto de dados que usa deciles categóricos para segmentar e criar públicos com base em atributos classificados.

Os seguintes conceitos-chave são ilustrados:

* Criação de esquema para segmentação de decodificação.
* Criação de decis categóricos.
* Criação de atributos derivados complexos.
* Cálculo de decodificações em um período de lookback.
* Um exemplo de query para demonstrar agregação, classificação e adição de identidades exclusivas para permitir que os públicos-alvo sejam gerados com base nesses buckets de decil.

## Introdução

Este guia requer um entendimento prático de [execução de query no Serviço de query](../best-practices/writing-queries.md) e os seguintes componentes do Adobe Experience Platform:

* [Visão geral do perfil do cliente em tempo real](../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.
* [Noções básicas da composição do schema](../../xdm/schema/composition.md): Uma introdução aos esquemas do Experience Data Model (XDM) e aos blocos de construção, princípios e práticas recomendadas para a composição de schemas.
* [Como habilitar um esquema para o Perfil do cliente em tempo real](../../profile/tutorials/add-profile-data.md): Este tutorial descreve as etapas necessárias para adicionar dados ao Perfil do cliente em tempo real.
* [Como definir um tipo de dados personalizado](../../xdm/api/data-types.md): Os tipos de dados são usados como campos do tipo referência em classes ou grupos de campos de esquema e permitem o uso consistente de uma estrutura de vários campos que pode ser incluída em qualquer lugar no esquema.

## Objetivos

O exemplo dado neste documento usa deciles para criar atributos derivados para classificar dados de um schema de fidelidade de uma companhia aérea. Atributos derivados permitem maximizar o utilitário dos dados identificando um público-alvo com base no &quot;n&quot; % superior para uma categoria escolhida.

## Criar atributos derivados com base em decis

Para definir a classificação de decodificações com base em uma dimensão específica e uma métrica correspondente, um schema deve ser projetado para permitir o agrupamento de decodificações.

Este guia usa um conjunto de dados de fidelidade da companhia aérea para demonstrar como usar o Serviço de query para criar decodificações com base nos quilômetros percorridos em vários períodos de lookback.

## Usar o Serviço de Consulta para criar decodificações

Usando o Serviço de query, você pode criar um conjunto de dados que contém decodificações categóricas, que podem ser segmentadas para criar públicos com base na classificação de atributos. Os conceitos exibidos nos exemplos a seguir podem ser aplicados para criar outros conjuntos de dados de bucket do decile, desde que uma categoria seja definida e uma métrica esteja disponível.

O exemplo de dados de fidelidade da companhia aérea usa um [Classe XDM ExperienceEvents](../../xdm/classes/experienceevent.md). Cada evento é um registro de uma transação comercial para quilometragem, creditada ou debitada, e o status de fidelidade de associação de &quot;Folheto&quot;, &quot;Frequente&quot;, &quot;Prata&quot; ou &quot;Ouro&quot;. O campo de identidade principal é `membershipNumber`.

### Conjuntos de dados de amostra

O conjunto de dados de fidelidade aérea inicial para este exemplo é &quot;Dados de fidelidade da linha aérea&quot; e tem o seguinte schema. Observe que a identidade primária para o esquema é `_profilefoundationreportingstg.membershipNumber`.

![Um diagrama do schema de dados de fidelidade da linha aérea.](../images/derived-attributes/deciles-use-case/airline-loyalty-data.png)

**Dados de exemplo**

A tabela a seguir exibe os dados de amostra contidos na variável `_profilefoundationreportingstg` objeto usado para este exemplo. Ele fornece o contexto para o uso de buckets de decil para criar atributos derivados complexos.

>[!NOTE]
>
>Para brevidade, a ID do locatário `_profilefoundationreportingstg` foi omitido do início do namespace nos títulos da coluna e menções subsequentes em todo o documento.

| `.membershipNumber` | `.emailAddress.address` | `.transactionDate` | `.transactionType` | `.transactionDetails` | `.mileage` | `.loyaltyStatus` |
|---|---|---|---|---|---|---|
| C435678623 | sfeldmark1vr@studiopress.com | 2022-01-01 | STATUS_MILES | Novo membro | 5000 | FLYER |
| B789279247 | pgalton32n@barnesandnoble.com | 2022-02-01 | AWARD_MILES | JFK-FRA | 7500 | PRATA |
| B789279247 | pgalton32n@barnesandnoble.com | 2022-02-01 | STATUS_MILES | JFK-FRA | 7500 | PRATA |
| B789279247 | pgalton32n@barnesandnoble.com | 2022-02-10 | AWARD_MILES | FRA-JFK | 5000 | PRATA |
| A123487284 | rritson1zn@sciencedaily.com | 2022-01-07 | STATUS_MILES | Novo cartão de crédito | 10000 | FLYER |

{style=&quot;table-layout:auto&quot;}

## Gerar conjuntos de dados do decile

Nos dados de fidelidade da companhia aérea vistos acima, a variável `.mileage` contém o número de milhas percorridas por um membro para cada voo individual realizado. Esses dados são usados para criar decodificações para o número de milhas voadas ao longo de lookbacks de vida útil e uma variedade de períodos de lookback. Para essa finalidade, um conjunto de dados é criado com decodificações em um tipo de dados de mapa para cada período de pesquisa e um decil apropriado para cada período de pesquisa atribuído em `membershipNumber`.

Crie um &quot;Esquema do decil de fidelidade da linha aérea&quot; para criar um conjunto de dados de decil usando o Serviço de query.

![Um diagrama do &quot;Esquema do decil de fidelidade da linha aérea&quot;.](../images/derived-attributes/deciles-use-case/airline-loyalty-decile-schema.png)

### Ativar o esquema para o Perfil do cliente em tempo real

Os dados assimilados no Experience Platform para uso pelo Perfil do cliente em tempo real devem estar em conformidade com o [um esquema do Experience Data Model (XDM) que está ativado para o Perfil](../../xdm/ui/resources/schemas.md). Para que um esquema seja ativado para o Perfil, ele deve implementar o Perfil individual XDM ou a classe ExperienceEvent XDM.

[Ative o esquema para uso no Perfil do cliente em tempo real usando a API do Registro de esquema](../../xdm/tutorials/create-schema-api.md) ou [Interface do usuário do Editor de esquemas](../../xdm/tutorials/create-schema-ui.md).  Instruções detalhadas sobre como ativar um esquema para Perfil estão disponíveis em sua respectiva documentação.

Em seguida, crie um tipo de dados a ser reutilizado para todos os grupos de campos relacionados ao decil. A criação do grupo de campos decile é uma etapa única por sandbox. Ele também pode ser reutilizado para todos os esquemas relacionados ao decil.

### Crie um namespace de identidade e o marque como o identificador principal {#identity-namespace}

Qualquer esquema criado para uso com deciles deve ter uma identidade primária atribuída. Você pode [definir um campo de identidade na interface do usuário de esquemas do Adobe Experience Platform](../../xdm/ui/fields/identity.md#define-an-identity-field)ou através do [API do Registro de Schema](../../xdm/api/descriptors.md#create).

O Serviço de Consulta também permite definir uma identidade ou uma identidade primária para campos de conjunto de dados de esquema ad hoc diretamente por meio do SQL. Consulte a documentação em [definição de uma identidade secundária e uma identidade primária nas identidades de esquema ad hoc](../data-governance/ad-hoc-schema-identities.md) para obter mais informações.

### Criar uma consulta para calcular decodificações em um período de pesquisa {#create-a-query}

O exemplo a seguir demonstra a consulta SQL para calcular um decil durante um período de pesquisa.

Um modelo pode ser feito usando o Editor de consultas na interface do usuário ou por meio do [API do serviço de consulta](../api/query-templates.md#create-a-query-template).

```sql
CREATE TABLE AS airline_loyality_decile 
{  WITH summed_miles_1 AS (
        SELECT _profilefoundationreportingstg.membershipNumber AS membershipNumber,
            _profilefoundationreportingstg.loyaltyStatus AS loyaltyStatus,
            SUM(_profilefoundationreportingstg.mileage) AS totalMiles
        FROM airline_loyalty_data
        WHERE _profilefoundationreportingstg.transactionDate < (MAKE_DATE(YEAR(CURRENT_DATE), MONTH(CURRENT_DATE), 1) - MAKE_YM_INTERVAL(0, 0))
    GROUP BY 1,2
    ),
    summed_miles_3 AS (
        SELECT _profilefoundationreportingstg.membershipNumber AS membershipNumber,
            _profilefoundationreportingstg.loyaltyStatus AS loyaltyStatus,
            SUM(_profilefoundationreportingstg.mileage) AS totalMiles
        FROM airline_loyalty_data
        WHERE _profilefoundationreportingstg.transactionDate < (MAKE_DATE(YEAR(CURRENT_DATE), MONTH(CURRENT_DATE), 1) - MAKE_YM_INTERVAL(0, 1))
    GROUP BY 1,2
    ),
    summed_miles_6 AS (
        SELECT _profilefoundationreportingstg.membershipNumber AS membershipNumber,
            _profilefoundationreportingstg.loyaltyStatus AS loyaltyStatus,
            SUM(_profilefoundationreportingstg.mileage) AS totalMiles
        FROM airline_loyalty_data
        WHERE _profilefoundationreportingstg.transactionDate < (MAKE_DATE(YEAR(CURRENT_DATE), MONTH(CURRENT_DATE), 1) - MAKE_YM_INTERVAL(0, 4))
    GROUP BY 1,2
    ),
    rankings_1 AS (
        SELECT membershipNumber,
            loyaltyStatus,
            totalMiles,
            NTILE(10) OVER (PARTITION BY loyaltyStatus ORDER BY totalMiles DESC) AS decileBucket
        FROM summed_miles_1
    ),
    rankings_3 AS (
        SELECT membershipNumber,
            loyaltyStatus,
            totalMiles,
            NTILE(10) OVER (PARTITION BY loyaltyStatus ORDER BY totalMiles DESC) AS decileBucket
        FROM summed_miles_3
    ),
    rankings_6 AS (
        SELECT membershipNumber,
            loyaltyStatus,
            totalMiles,
            NTILE(10) OVER (PARTITION BY loyaltyStatus ORDER BY totalMiles DESC) AS decileBucket
        FROM summed_miles_6
    ),
    map_1 AS (
        SELECT membershipNumber,
            MAP_FROM_ARRAYS(COLLECT_LIST(loyaltyStatus), COLLECT_LIST(decileBucket)) AS decileMonth1
        FROM rankings_1
        GROUP BY membershipNumber
    ),
    map_3 AS (
        SELECT membershipNumber,
            MAP_FROM_ARRAYS(COLLECT_LIST(loyaltyStatus), COLLECT_LIST(decileBucket)) AS decileMonth3
        FROM rankings_3
        GROUP BY membershipNumber
    ),
    map_6 AS (
        SELECT membershipNumber,
            MAP_FROM_ARRAYS(COLLECT_LIST(loyaltyStatus), COLLECT_LIST(decileBucket)) AS decileMonth6
        FROM rankings_6
        GROUP BY membershipNumber
    ),
    all_memberships AS (
        SELECT DISTINCT _profilefoundationreportingstg.membershipNumber AS membershipNumber FROM airline_loyalty_data
    )
    SELECT STRUCT(
            all_memberships.membershipNumber AS membershipNumber,
            STRUCT(
                    map_1.decileMonth1 AS decileMonth1,
                    map_3.decileMonth3 AS decileMonth3,
                    map_6.decileMonth6 AS decileMonth6
            ) AS decilesMileage
        ) AS _profilefoundationreportingstg
    FROM all_memberships
        LEFT JOIN map_1 ON  (all_memberships.membershipNumber = map_1.membershipNumber)
        LEFT JOIN map_3 ON  (all_memberships.membershipNumber = map_3.membershipNumber)
        LEFT JOIN map_6 ON  (all_memberships.membershipNumber = map_6.membershipNumber)
    }
```

### Análise de consulta

Seções da query de exemplo são examinadas com mais detalhes abaixo.

#### Períodos de pesquisa

O tipo de dados decile contém um bucket para lookbacks de 1, 3, 6, 9, 12 e duração. A query usa os períodos de lookback de 1, 3 e 6 meses, então cada seção conterá algumas consultas &quot;repetidas&quot; para criar tabelas temporárias para cada período de lookback.

>[!NOTE]
>
>Se os dados de origem não tiverem uma coluna que possa ser usada para determinar um período de lookback, todas as classificações de classe decile serão executadas em `decileMonthAll`.

#### Agregação

Use expressões de tabela comuns (CTE) para agregar a quilometragem antes de criar buckets de decil. Isso fornece o total de milhas para um período de pesquisa específico. Os CTEs existem temporariamente e só podem ser usados dentro do escopo do query maior.

```sql
summed_miles_1 AS (
    SELECT _profilefoundationreportingstg.membershipNumber AS membershipNumber,
           _profilefoundationreportingstg.loyaltyStatus AS loyaltyStatus,
           SUM(_profilefoundationreportingstg.mileage) AS totalMiles
    FROM airline_loyalty_data
    WHERE _profilefoundationreportingstg.transactionDate < (MAKE_DATE(YEAR(CURRENT_DATE), MONTH(CURRENT_DATE), 1) - MAKE_YM_INTERVAL(0, 0))
    GROUP BY 1,2
)
```

O bloco é repetido duas vezes no template (`summed_miles_3` e `summed_miles_6`) com uma alteração no cálculo de data para gerar os dados para os outros períodos de pesquisa.

É importante observar as colunas de identidade, dimensão e métrica da consulta (`membershipNumber`, `loyaltyStatus` e `totalMiles` respectivamente).

#### Classificação

Deciles permitem que você execute uma divisão categórica. Para criar o número da classificação, a variável `NTILE` é usada com um parâmetro de `10` em uma JANELA agrupada pela variável `loyaltyStatus` campo. Isso resulta em um ranking de 1 a 10. Defina as `ORDER BY` cláusula da `WINDOW` para `DESC` para garantir que um valor de classificação de `1` é dada à **maior** na dimensão.

```sql
rankings_1 AS (
    SELECT membershipNumber,
           loyaltyStatus,
           totalMiles,
           NTILE(10) OVER (PARTITION BY loyaltyStatus ORDER BY totalMiles DESC) AS decileBucket
    FROM summed_miles_1
)
```

#### Agregação de mapa

Com vários períodos de pesquisa, é necessário criar os mapas de bucket do decile antecipadamente usando o `MAP_FROM_ARRAYS` e `COLLECT_LIST` funções. No trecho de exemplo, `MAP_FROM_ARRAYS` cria um mapa com um par de chaves (`loyaltyStatus`) e valores (`decileBucket`). `COLLECT_LIST` retorna uma matriz com todos os valores na coluna especificada.

```sql
map_1 AS (
    SELECT membershipNumber,
           MAP_FROM_ARRAYS(COLLECT_LIST(loyaltyStatus), COLLECT_LIST(decileBucket)) AS decileMonth1
    FROM rankings_1
    GROUP BY membershipNumber
)
```

>[!NOTE]
>
>A agregação de mapa não é necessária se a classificação de decile for necessária somente para um período de vida.

#### Identidades exclusivas

A lista de identidades exclusivas (`membershipNumber`) é necessário para criar uma lista exclusiva de todas as associações.

```sql
all_memberships AS (
    SELECT DISTINCT _profilefoundationreportingstg.membershipNumber AS membershipNumber FROM airline_loyalty_data
)
```

>[!NOTE]
>
>Se a classificação de decile for necessária apenas para um período de vida, essa etapa pode ser omitida e a agregação por `membershipNumber` pode ser feito na etapa final.

#### Juntar todos os dados temporários

A etapa final é unir todos os dados temporários em um formulário idêntico à estrutura dos deciles no grupo de campos.

```sql
SELECT STRUCT(
           all_memberships.membershipNumber AS membershipNumber,
           STRUCT(
                map_1.decileMonth1 AS decileMonth1,
                map_3.decileMonth3 AS decileMonth3,
                map_6.decileMonth6 AS decileMonth6
           ) AS decilesMileage
       ) AS _profilefoundationreportingstg
FROM all_memberships
    LEFT JOIN map_1 ON  (all_memberships.membershipNumber = map_1.membershipNumber)
    LEFT JOIN map_3 ON  (all_memberships.membershipNumber = map_3.membershipNumber)
    LEFT JOIN map_6 ON  (all_memberships.membershipNumber = map_6.membershipNumber)
```

Se somente os dados de vida estiverem disponíveis, seu query será exibido da seguinte maneira:

```sql
SELECT STRUCT(
           rankings.membershipNumber AS membershipNumber,
           STRUCT(
                MAP_FROM_ARRAYS(COLLECT_LIST(loyaltyStatus), COLLECT_LIST(decileBucket)) AS decileMonthAll
           ) AS decilesMileage
       ) AS _profilefoundationreportingstg
FROM rankings
GROUP BY rankings.membershipNumber
```

Uma correlação entre o número de classificação e o percentil é garantida nos resultados da consulta por causa do uso de deciles. Cada classificação equivale a 10%, portanto, a identificação de um público com base nos 30% principais precisa somente atingir as classificações 1, 2 e 3.

### Executar o modelo de consulta

Execute a query para preencher o conjunto de dados do decile. Você também pode salvar a consulta como um modelo e agendá-la para ser executada em uma cadência. Quando salva como um modelo, a consulta também pode ser atualizada para usar o padrão de criação e inserção que faz referência à variável `table_exists` comando. Mais informações sobre como usar o `table_exists`pode ser encontrado no [Guia de sintaxe SQL](../sql/syntax.md#table-exists).

## Próximas etapas

O exemplo de uso fornecido acima destaca as etapas para disponibilizar os atributos de decile no Perfil do cliente em tempo real. Isso permite que o Serviço de segmentação, por meio de uma interface de usuário ou API RESTful, gere públicos com base nesses buckets de decil. Consulte a [Visão geral do serviço de segmentação](../../segmentation/home.md) para obter informações sobre como criar, avaliar e acessar segmentos.
