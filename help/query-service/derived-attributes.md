---
title: Atributos derivados
description: Atributos derivados permitem calcular atributos em uma cadência regular e, como opção, publicar esses atributos derivados no Perfil do cliente em tempo real como atributos de perfil. Este documento fornece uma visão geral de como usar o Serviço de query para criar atributos derivados para usar com os dados do perfil.
hide: true
hidefromtoc: true
source-git-commit: fc2d2e7dadb95460f5d735ba33e5f106880a0198
workflow-type: tm+mt
source-wordcount: '1650'
ht-degree: 1%

---

# Atributos derivados

Atributos derivados permitem calcular atributos em uma cadência regular e, como opção, publicar esses atributos derivados no Perfil do cliente em tempo real como atributos de perfil.

Atributos derivados, como aqueles criados com dados decilodificados, são necessários para uma variedade de casos de uso que analisam dados de perfil. Usando dados de decilque, você pode criar públicos-alvo a partir de segmentos com base em seu percentil ou classificação de um determinado atributo. Por exemplo, casos de uso em potencial podem incluir:

* Identificação dos 10% mais baixos de assinantes com base na visualização por canal. Isso permitiria que os profissionais de marketing direcionassem um público-alvo específico e vendessem um novo pacote de assinantes.
* Identificação de um público que está no top 10% dos panfletos com base em suas milhas totais viajadas e tem status de &quot;panfleto&quot;. Este público-alvo poderia ser usado para direcionar seletivamente a venda de uma nova oferta de cartão de crédito.

## Introdução

Essa visão geral requer uma compreensão funcional da [Chamadas de API da plataforma](../landing/api-guide.md) e os seguintes componentes do Adobe Experience Platform:

* [Visão geral do perfil do cliente em tempo real](../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.
* [Noções básicas da composição do schema](../xdm/schema/composition.md): Uma introdução aos esquemas do Experience Data Model (XDM) e aos blocos de construção, princípios e práticas recomendadas para a composição de schemas.
* [Como habilitar um esquema para o Perfil do cliente em tempo real](../profile/tutorials/add-profile-data.md): Este tutorial descreve as etapas necessárias para adicionar dados ao Perfil do cliente em tempo real.

## Suporte SQL para atributos derivados

Para definir a classificação de decodificações com base em uma dimensão específica (categoria) e uma métrica correspondente (receita, pontos, duração da visualização etc.), um schema deve ser projetado para permitir a segmentação de decodificação. Esse schema pode ser usado como parte do schema de perfil maior.

### Criar um namespace de identidade para o esquema do perfil {#identity-namespace}

Os namespaces de identidade são um componente do [ Identity Service](../identity-service/home.md) que serve como indicadores do contexto ao qual uma identidade está relacionada. Uma identidade totalmente qualificada inclui um valor de ID e um namespace. Ao corresponder e mesclar dados de registro em fragmentos de perfil, o valor de identidade e o namespace devem corresponder.

Os conjuntos de dados criados relacionados à identidade podem ser agrupados como um grupo de dados e ajudar a manter o ciclo de vida dos dados. É possível criar namespaces personalizados usando o [API do serviço de identidade](../identity-service/api/create-custom-namespace.md) ou pela interface do usuário. Consulte a [gerenciar documentação de namespaces personalizados](../identity-service/namespaces.md#manage-namespaces) para obter orientação sobre como fazer isso por meio da interface do usuário do .

O descritor de identidade principal pode ser atribuído a um campo na interface do usuário de esquemas ou pode ser criado usando a API do Registro de esquemas. Consulte a documentação para obter instruções sobre como [definir um campo de identidade na interface do usuário do Adobe Experience Platform](../xdm/ui/fields/identity.md#define-an-identity-field)ou através do [API do Registro de Schema](../xdm/api/descriptors.md#create).

O Serviço de Consulta também permite definir uma identidade ou uma identidade primária para campos de conjunto de dados de esquema ad hoc diretamente por meio do SQL. Consulte a documentação em [definição de uma identidade secundária e uma identidade primária nas identidades de esquema ad hoc](./data-governance/ad-hoc-schema-identities.md) para obter mais informações.

## Criar atributos derivados

O exemplo de query fornecido neste documento foca em decodificações para categorizar conjuntos de dados grandes e classificar os dados dos valores mais alto para o mais baixo (ou vice-versa), e filtrar com base no período.

### Deciles {#deciles}

Um decile é um método de dividir um conjunto de dados classificados em 10 partes iguais. Quando os dados são divididos em decodificações, uma classificação de decil é atribuída a cada linha no conjunto de dados. Isso permite que os dados sejam classificados em ordem decrescente ou crescente.

Uma classificação decile organiza os dados em ordem do mais baixo para o mais alto e é feita em uma escala de 1 a 10, onde cada número sucessivo corresponde a um aumento de 10 pontos percentuais.

Os buckets do decile representam o número de grupos classificados e são usados para atribuir uma classificação a uma dimensão (categoria) no conjunto de dados. O bucket pode ser um número ou uma expressão que resulta em um valor inteiro positivo para cada partição. Os buckets não devem ter um valor nulo.

Os quartis são usados para dividir a distribuição por quatro e percentis por 100.

### Criar o esquema para buckets de decil {#create-schema}

O schema criado para buckets do decile tem três partes integrais: um tipo de dados, um grupo de campos para o tipo de dados (por conjunto de dados de origem) e um campo de identidade principal.

>[!NOTE]
>
>Um namespace de identidade deve ser criado antes que o schema possa ser criado. Consulte a [namespace de identidade](#identity-namespace) para obter mais detalhes.

O Adobe fornece várias classes XDM padrão (&quot;core&quot;), incluindo Perfil individual XDM e ExperienceEvent XDM. Além dessas classes principais, você também pode criar suas próprias classes personalizadas para descrever casos de uso mais específicos da sua organização. Consulte os guias sobre como [criar e editar esquemas na interface do usuário](../xdm/ui/resources/schemas.md#create) ou usando a [endpoint de schemas na API do Registro de Schema](../xdm/api/schemas.md#create) para obter mais detalhes.

Os dados assimilados no Experience Platform para uso pelo Perfil do cliente em tempo real devem estar em conformidade com um esquema do Experience Data Model (XDM) habilitado para o Perfil. Para que um esquema seja ativado para o Perfil, ele deve implementar o Perfil individual XDM ou a classe ExperienceEvent XDM.

Você pode [habilite um esquema para usar no Perfil do cliente em tempo real usando a API do Registro de esquema](../xdm/tutorials/create-schema-api.md) ou [Interface do usuário do Editor de esquemas](../xdm/tutorials/create-schema-ui.md).  Instruções detalhadas sobre como ativar um esquema para Perfil estão disponíveis em sua respectiva documentação.

### Criar um tipo de dados {#create-data-type}

Os tipos de dados são usados como campos do tipo referência em classes ou grupos de campos de esquema e permitem o uso consistente de uma estrutura de vários campos que pode ser incluída em qualquer lugar no esquema. A criação do tipo de dados é uma etapa única por sandbox, pois pode ser reutilizada para todos os grupos de campos relacionados ao decil.

Consulte a documentação para obter instruções sobre como [definir um tipo de dados personalizado](../xdm/api/data-types.md) usando o [API do Registro de Schema](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

### Criar o grupo de campos decile {#create-field-group}

A criação do grupo de campos é uma etapa única por sandbox. Ele também pode ser reutilizado para todos os esquemas relacionados ao decil.

Consulte a documentação para obter instruções sobre como [criar grupos de campos por meio da interface do usuário](../xdm/ui/resources/field-groups.md#create)

## Usar o Serviço de Consulta para criar decodificações

O Serviço de query fornece uma maneira ideal de criar um conjunto de dados que contém decodificações categóricas. Isso pode ser usado em conjunto com o Serviço de segmentação para criar públicos com base na classificação de atributos.

Os conceitos exibidos nos exemplos a seguir podem ser aplicados para criar outros conjuntos de dados de bucket do decile, desde que uma categoria (dimensão) seja definida e uma métrica esteja disponível. Os exemplos são baseados em dados de um esquema de fidelidade da companhia aérea. Os dados de fidelidade da companhia aérea usam a classe Eventos de experiência, onde cada evento é um registro de uma transação comercial para **milhagem**, creditadas ou debitadas, e a associação **status de fidelidade** &quot;Folheto&quot;, &quot;Frequente&quot;, &quot;Prata&quot; ou &quot;Ouro&quot;. O campo de identidade principal é `membershipNumber`.

### Criar um modelo de consulta {#create-a-query-template}

O modelo pode ser feito usando o Editor de consultas na interface do usuário ou por meio do [API do serviço de consulta](./api/query-templates.md#create-a-query-template).

As seções do modelo de query exibidas abaixo serão examinadas com mais detalhes.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/query/query-templates \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
         "name": "Airline Loyalty Deciles Insert into profile",
         "sql":
            "WITH summed_miles_1 AS (
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
                LEFT JOIN map_6 ON  (all_memberships.membershipNumber = map_6.membershipNumber)"
        }'
```

#### Períodos de pesquisa

O tipo de dados decile contém um compartimento para 1, 3, 6, 9, 12 e retornos de tempo de vida. O query usa os períodos de análise de 1, 3 e 6 meses, de modo que cada seção conterá algumas consultas &quot;repetidas&quot; para criar tabelas temporárias para cada período de análise.

>[!NOTE]
>
>Se os dados de origem não tiverem uma coluna que possa ser usada para determinar um período de análise, todas as classificações de classe de decil serão executadas em `decileMonthAll`.

#### Agregação

Use expressões de tabela comuns (CTE) para agregar a quilometragem antes de criar buckets de decil. Isso fornece o total de milhas para um período de análise específico. Os CTEs existem temporariamente e só podem ser usados dentro do escopo do query maior.

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

Observe a identidade, a dimensão e as colunas de métrica da consulta (`membershipNumber`, `loyaltyStatus` e `totalMiles` respectivamente).

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

Com vários períodos de retrospectiva, você precisa criar os mapas de bucket do decile antecipadamente usando o `MAP_FROM_ARRAYS` e `COLLECT_LIST` funções. No trecho de exemplo, `MAP_FROM_ARRAYS` cria um mapa com um par de chaves (`loyaltyStatus`) e valores (`decileBucket`). `COLLECT_LIST` retorna uma matriz com todos os valores na coluna especificada.

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

### Executar o modelo de consulta

As consultas podem ser [executado por meio da interface do usuário](./ui/user-guide.md#executing-queries) ou [API do serviço de consulta](./api/queries.md#create-a-query).

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/query/queries \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "dbName": "prod:all",
    "templateId": "{{airline_decile_query_template_id}}",
    "insertIntoParameters": {
        "datasetName": "airline_loyalty_decile"
    }
}'
```

Uma correlação entre o número de classificação e o percentil é garantida nos resultados da consulta por causa do uso de deciles. Cada classificação equivale a 10%, portanto, a identificação de um público com base nos 30% principais precisa somente atingir as classificações 1, 2 e 3.

## Próximas etapas

O Serviço de segmentação fornece uma interface de usuário e uma RESTful API que permite gerar públicos com base nesses buckets de decil. Consulte a [Visão geral do serviço de segmentação](../segmentation/home.md) para obter informações sobre como criar, avaliar e acessar segmentos.

Para obter informações detalhadas sobre como criar e usar segmentos no Construtor de segmentos (a implementação da interface do usuário do Serviço de segmentação), consulte o [Guia do Construtor de segmentos](../segmentation/ui/overview.md).

Para obter informações sobre como criar definições de segmento usando a API, consulte o tutorial em [criação de segmentos de público-alvo usando a API](../segmentation/tutorials/create-a-segment.md).
