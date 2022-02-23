---
title: Trabalhar com estruturas de dados aninhadas no Serviço de query
description: Este documento fornece um exemplo de trabalho para processar e transformar campos de dados aninhados usando instruções CTAS e INSERT INTO.
source-git-commit: 838ee939a8438c2f09ff64044c129e20c37ea01a
workflow-type: tm+mt
source-wordcount: '785'
ht-degree: 1%

---

# Trabalhar com estruturas de dados aninhadas no Serviço de query

O Serviço de query do Adobe Experience Platform oferece suporte ao uso de campos de dados aninhados. A complexidade das estruturas de dados empresariais pode complicar a transformação ou o processamento desses dados. Este documento fornece exemplos de como criar, processar ou transformar conjuntos de dados com tipos de dados complexos, incluindo estruturas de dados aninhadas.

O Serviço de Consulta fornece uma interface PostgreSQL para executar consultas SQL em todos os conjuntos de dados gerenciados pelo Experience Platform. A plataforma suporta o uso de tipos de dados primitivos ou complexos em colunas de tabela, como struct, matrizes, mapas e estrutura, matrizes e mapas profundamente aninhados. Os conjuntos de dados também podem conter estruturas aninhadas, onde o tipo de dados da coluna pode ser tão complexo quanto uma matriz de estruturas aninhadas, ou um mapa de mapas, onde o valor de um par de valores chave pode ser uma estrutura com vários níveis de aninhamento.

## Introdução

Este tutorial requer o uso de um cliente PSQL de terceiros ou da ferramenta Editor de consultas para gravar, validar e executar consultas na interface do usuário do Experience Platform (UI). Detalhes completos sobre como executar consultas por meio da interface do usuário podem ser encontrados no [Guia da interface do usuário do Editor de consultas](../ui/user-guide.md). Para obter uma lista detalhada em que os clientes de desktop de terceiros podem se conectar ao Serviço de query, consulte o [visão geral das conexões do cliente](../clients/overview.md).

Você também deve ter um bom entendimento da `INSERT INTO` e `CTAS` sintaxe. Informações específicas sobre sua utilização podem ser encontradas no [`INSERT INTO`](../sql/syntax.md#insert-into) e [`CTAS`](../sql/syntax.md#create-table-as-select) seções da [Documentação de referência da sintaxe SQL](../sql/syntax.md).

## Criar um conjunto de dados

O serviço Query fornece Criar tabela como seleção (`CTAS`) para criar uma tabela com base na saída de um `SELECT` ou, como nesse caso, usando uma referência a um esquema XDM existente no Adobe Experience Platform. Exibido abaixo é o esquema XDM para `Final_subscription` criado para este exemplo.

![Um diagrama do schema final_subscription.](../images/best-practices/final-subscription-schema.png)

O exemplo a seguir demonstra o SQL usado para criar o `final_subscription_test2` conjunto de dados. `final_subscription_test2` é criado usando o `Final_subscription` esquema. Os dados são extraídos da fonte usando um `SELECT` para preencher algumas linhas.

```sql
CREATE TABLE final_subscription_test2 with(schema='Final_subscription') AS (
        SELECT struct(userid, collect_set(subscription) AS subscription) AS _lumaservices3 FROM(
            SELECT user AS userid,
                   struct( last(eventtime) AS last_eventtime,
                           last(status) AS last_status,
                           offer_id, 
                           subsid AS subscription_id)
                   AS subscription
             FROM (
                   SELECT _lumaservices3.msftidentities.userid user
                        , _lumaservices3.subscription.subscription_id subsid
                        , _lumaservices3.subscription.subscription_status status
                        , _lumaservices3.subscription.offer_id offer_id
                        , TIMESTAMP eventtime
 
                   FROM
                        xbox_subscription_event
                   UNION   
                   SELECT _lumaservices3.msftidentities.userid user
                        , _lumaservices3.subscription.subscription_id subsid
                        , _lumaservices3.subscription.subscription_status status
                        , _lumaservices3.subscription.offer_id offer_id
                        , TIMESTAMP eventtime
                   FROM
                        office365_subscription_event
             ) 
             GROUP BY user,subsid,offer_id
             ORDER BY user ASC
       ) GROUP BY userid)
```

No conjunto de dados inicial `final_subscription_test2`, o tipo de dados struct é usado para conter a variável `subscription` e o `userid` que é exclusiva de cada usuário. O `subscription` descreve as subscrições de produtos de um usuário. Pode haver várias subscrições, mas uma tabela só pode conter as informações de uma assinatura por linha.

## Use INSERIR EM para atualizar campos de dados aninhados

Depois que a variável `final_subscription_test2` o conjunto de dados foi criado, o `INSERT INTO` é usada para anexar dados adicionais à tabela. Ao copiar dados, os tipos de dados na origem e no destino devem corresponder. Como alternativa, o tipo de dados de origem deve ser `CAST` ao tipo de dados de destino. Os dados incrementais são então adicionados ao conjunto de dados de destino usando o seguinte SQL.

```sql
INSERT INTO final_subscription_test
      SELECT struct(userid, collect_set(subscription) AS subscription) AS _lumaservices3 FROM(
            SELECT user AS userid,
                   struct( last(eventtime) AS last_eventtime,
                           last(status) AS last_status,
                           offer_id, 
                           subsid AS subscription_id)
                   AS subscription
             FROM  SELECT _lumaservices3.msftidentities.userid user
                        , _lumaservices3.subscription.subscription_id subsid
                        , _lumaservices3.subscription.subscription_status status
                        , _lumaservices3.subscription.offer_id offer_id
                        , TIMESTAMP eventtime
 
                   FROM
                        xbox_subscription_event
                   UNION   
                   SELECT _lumaservices3.msftidentities.userid user
                        , _lumaservices3.subscription.subscription_id subsid
                        , _lumaservices3.subscription.subscription_status status
                        , _lumaservices3.subscription.offer_id offer_id
                        , timestamp eventtime
                   FROM
                        office365_subscription_event
             ) 
             GROUP BY user,subsid,offer_id
             ORDER BY user ASC
       ) GROUP BY userid)
```

## Processar dados de um conjunto de dados aninhado

Para descobrir a lista de assinaturas ativas de um usuário de um conjunto de dados, você deve gravar uma consulta que separe os elementos de uma matriz em várias linhas e colunas. Para fazer isso, primeiro você deve entender a forma do modelo de dados, pois as informações de assinatura são mantidas dentro de uma matriz aninhada dentro do conjunto de dados.

O PSQL `\d` é usado para navegar nível a nível para os dados de assinatura necessários. Os quadros ilustram a estrutura da variável `final_subscription_test2` conjunto de dados. Tipos de dados complexos podem ser reconhecidos rapidamente, pois não são valores típicos, como texto, booleano, carimbo de data e hora, etc.

| Coluna | Tipo |
|--------|-------|
| `_lumaservices3` | final_subscription_test2_lumaservices3 |

Os campos da próxima coluna são exibidos usando o `\d final_subscription_test2__lumaservices3` comando.

| Coluna | Tipo |
|---------|-------|
| `userid` | texto |
| `subscription` | _lumaservices3_subscription_e[] |

`subscription` é uma matriz de elementos struct. Seus campos são exibidos usando o `\d _lumaservices3_subscription_e[]` comando.

| Coluna | Tipo |
|---------|-------|
| `last_eventtime` | carimbo de data e hora |
| `last_status` | texto |
| `offer_id` | texto |
| `subscription_id` | texto |

Para consultar os campos aninhados da assinatura, primeiro você deve separar os elementos do `subscription` em várias linhas e retorne os resultados usando a função explode . O exemplo SQL a seguir retorna a subscrição ativa de um usuário com base em `userid`.

```sql
SELECT userid, subs AS active_subscription FROM (
    SELECT _lumaservices3.userid AS userid, explode(_lumaservices3.subscription) AS subs 
    FROM final_subscription_test2
)
WHERE subs.last_status='Active';
```

Essa solução de exemplo simplificada permite somente uma assinatura de usuário ativa. Realisticamente, pode haver muitas subscrições ativas para um único usuário. O exemplo a seguir modifica a consulta anterior para permitir várias assinaturas ativas simultâneas.

```sql
SELECT userid, collect_list(subs) AS active_subscriptions FROM (
     SELECT
          _lumaservices3.userid AS userid,
          explode(_lumaservices3.subscription) AS subs
     FROM final_subscription_test2
     )
WHERE subs.last_status='Active' 
GROUP BY userid ;
```

Apesar da complexidade crescente deste exemplo de SQL, a variável `collect_list` para assinaturas ativas não garante que a saída estará na mesma ordem da fonte. Para criar uma lista de assinaturas ativas de um usuário, você deve usar GROUP BY ou shuffling para agregar os resultados da lista.

## Próximas etapas

Ao ler este documento, você agora entende como processar ou transformar conjuntos de dados que usam tipos de dados complexos no Serviço de query do Adobe Experience Platform. Consulte a [orientações de execução de consultas](./writing-queries.md) para obter mais informações sobre a execução de consultas SQL em conjuntos de dados no Data Lake.
