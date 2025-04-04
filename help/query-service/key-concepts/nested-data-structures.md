---
keywords: Experience Platform;serviço de consulta;serviço de consulta;estruturas de dados aninhadas;dados aninhados;
title: Trabalho com estruturas de dados aninhadas no Serviço de consulta
description: Este documento fornece um exemplo prático para processar e transformar campos de dados aninhados usando instruções CTAS e INSERT INTO.
exl-id: 593379fb-88ad-4b14-8d2e-aa6d18129974
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '790'
ht-degree: 2%

---

# Trabalho com estruturas de dados aninhadas no Serviço de consulta

O Serviço de consulta da Adobe Experience Platform oferece suporte ao uso de campos de dados aninhados. A complexidade das estruturas de dados corporativos pode complicar a transformação ou o processamento desses dados. Este documento fornece exemplos de como criar, processar ou transformar conjuntos de dados com tipos de dados complexos, incluindo estruturas de dados aninhadas.

O Serviço de Consulta fornece uma interface [!DNL PostgreSQL] para executar consultas SQL em todos os conjuntos de dados gerenciados pela Experience Platform. O Experience Platform oferece suporte ao uso de tipos de dados primitivos ou complexos em colunas de tabela, como struct, matrizes, mapas e struct, matrizes e mapas aninhados. Os conjuntos de dados também podem conter estruturas aninhadas, em que o tipo de dados da coluna pode ser tão complexo quanto uma matriz de estruturas aninhadas, ou um mapa de mapas em que o valor de um par de valores-chave pode ser uma estrutura com vários níveis de aninhamento.

## Introdução

Este tutorial requer o uso de um cliente PSQL de terceiros ou da ferramenta Editor de consultas para gravar, validar e executar consultas na interface do usuário (UI) do Experience Platform. Detalhes completos sobre como executar consultas por meio da interface podem ser encontrados no [guia da interface do Editor de Consultas](../ui/user-guide.md). Para obter uma lista detalhada sobre quais clientes de desktop de terceiros podem se conectar ao Serviço de Consulta, consulte a [visão geral das conexões de cliente](../clients/overview.md).

Você também deve conhecer bem a sintaxe `INSERT INTO` e `CTAS`. Informações específicas sobre seu uso podem ser encontradas nas seções [`INSERT INTO`](../sql/syntax.md#insert-into) e [`CTAS`](../sql/syntax.md#create-table-as-select) da [documentação de referência da sintaxe SQL](../sql/syntax.md).

## Criar um conjunto de dados

O serviço de consulta fornece a funcionalidade Criar Tabela como Seleção (`CTAS`) para criar uma tabela com base na saída de uma instrução `SELECT` ou, como nesse caso, usando uma referência a um esquema XDM existente no Adobe Experience Platform. Abaixo está o esquema XDM para `Final_subscription` criado para este exemplo.

![Um diagrama do esquema final_subscription.](../images/best-practices/final-subscription-schema.png)

O exemplo a seguir demonstra o SQL usado para criar o conjunto de dados `final_subscription_test2`. `final_subscription_test2` é criado usando o esquema `Final_subscription`. Os dados são extraídos da origem usando uma cláusula `SELECT` para preencher algumas linhas.

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

No conjunto de dados inicial `final_subscription_test2`, o tipo de dados struct é usado para conter o campo `subscription` e o `userid` que é exclusivo para cada usuário. O campo `subscription` descreve as assinaturas de produto de um usuário. Pode haver várias assinaturas, mas uma tabela só pode conter as informações de uma assinatura por linha.

## Use INSERT INTO para atualizar campos de dados aninhados

Após a criação do conjunto de dados `final_subscription_test2`, a instrução `INSERT INTO` é usada para acrescentar dados adicionais à tabela. Ao copiar dados, os tipos de dados na origem e no destino devem corresponder. Como alternativa, o tipo de dados de origem deve ser `CAST` para o tipo de dados de destino. Os dados incrementais são adicionados ao conjunto de dados de destino usando o seguinte SQL.

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

Para descobrir a lista de assinaturas ativas de um usuário em relação a um conjunto de dados, você deve gravar uma consulta que separe os elementos de uma matriz em várias linhas e colunas. Para fazer isso, primeiro você deve entender a forma do modelo de dados, pois as informações de assinatura são mantidas em uma matriz aninhada no conjunto de dados.

O comando PSQL `\d` é usado para navegar nível por nível até os dados de assinatura necessários. As tabelas ilustram a estrutura do conjunto de dados `final_subscription_test2`. Tipos de dados complexos podem ser reconhecidos rapidamente porque não são valores de tipo típicos, como texto, booleano, carimbo de data e hora etc.

| Coluna | Tipo |
|--------|-------|
| `_lumaservices3` | final_subscription_test2__lumaservices3 |

Os campos da próxima coluna são exibidos usando o comando `\d final_subscription_test2__lumaservices3`.

| Coluna | Tipo |
|---------|-------|
| `userid` | texto |
| `subscription` | _lumaservices3_subscription_e[] |

`subscription` é uma matriz de elementos struct. Seus campos são exibidos usando o comando `\d _lumaservices3_subscription_e[]`.

| Coluna | Tipo |
|---------|-------|
| `last_eventtime` | carimbo de data e hora |
| `last_status` | texto |
| `offer_id` | texto |
| `subscription_id` | texto |

Para consultar os campos aninhados da assinatura, primeiro separe os elementos da matriz `subscription` em várias linhas e retorne os resultados usando a função explode. O exemplo SQL a seguir retorna a assinatura ativa para um usuário com base em `userid`.

```sql
SELECT userid, subs AS active_subscription FROM (
    SELECT _lumaservices3.userid AS userid, explode(_lumaservices3.subscription) AS subs 
    FROM final_subscription_test2
)
WHERE subs.last_status='Active';
```

Esta solução de exemplo simplificada permite apenas uma assinatura de usuário ativa. Na realidade, pode haver muitas assinaturas ativas para um único usuário. O exemplo a seguir modifica a consulta anterior para permitir várias assinaturas ativas simultâneas.

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

Apesar da complexidade crescente desse exemplo de SQL, o `collect_list` para assinaturas ativas não garante que a saída estará na mesma ordem que a origem. Para criar uma lista de assinaturas ativas para um usuário, você deve usar GROUP BY ou shuffling para agregar os resultados da lista.

## Próximas etapas

Após a leitura desse documento, você entende como processar ou transformar conjuntos de dados que usam tipos de dados complexos no Serviço de consulta da Adobe Experience Platform. Consulte a [orientação de execução de consultas](../best-practices/writing-queries.md) para obter mais informações sobre como executar consultas SQL em conjuntos de dados no Data Lake.
