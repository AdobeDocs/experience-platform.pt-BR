---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: SDK de acesso a dados do Spark seguro
topic: tutorial
translation-type: tm+mt
source-git-commit: f7714b8bebe37b29290794a48314962e42b24058
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 1%

---


# SDK de acesso a dados do Spark seguro

O Secure Spark [!DNL Data Access] SDK é um kit de desenvolvimento de software que permite a leitura e a gravação de conjuntos de dados do Adobe Experience Platform.

## Introdução

Você deve ter concluído o tutorial de [autenticação](../../tutorials/authentication.md) para ter acesso aos valores para fazer chamadas para o [!DNL Data Access] SDK do Secure Spark:

- `{ACCESS_TOKEN}`
- `{API_KEY}`
- `{IMS_ORG}`

Todos os recursos em [!DNL Experience Platform] são isolados para caixas de proteção virtuais específicas. O uso do SDK do Spark requer o nome e a ID da caixa de proteção na qual a operação ocorrerá:

- `{SANDBOX_NAME}`
- `{SANDBOX_ID}`

Para obter mais informações sobre caixas de proteção em [!DNL Platform], consulte a documentação [de visão geral da](../../sandboxes/home.md)caixa de proteção.

## configuração do Ambiente

O [!DNL Spark] SDK espera que você forneça credenciais nas variáveis de ambiente ou nas opções da Fonte de Dados.

| Variable | Valor |
| -------- | ----- | 
| `SERVICE_TOKEN` | Seu token de autorização de serviço. |
| `SERVICE_API_KEY` | Sua chave da API de serviço. Geralmente, é a mesma ID do cliente IMS. |
| `ORG_ID` | Seu valor `{IMS_ORG}` de ID. |
| `USER_TOKEN` | Seu `{ACCESS_TOKEN}` valor. |

Outros parâmetros de configuração incluem:

| Variable | Valor |
| -------- | ----- |
| `ENVIRONMENT_NAME` | O ambiente ao qual você está tentando se conectar. Pode ser &quot;dev&quot;, &quot;stage&quot; ou &quot;prod&quot;. |
| `SANDBOX_NAME` | O nome da caixa de proteção à qual você está se conectando. |

Como alternativa, além de `ENVIRONMENT_NAME`, você pode definir qualquer uma das variáveis de ambiente acima dentro `QSOption`, conforme mostrado no exemplo abaixo:

```scala
val df = spark.read
    .format("com.adobe.platform.query")
    .option(QSOption.userToken, userToken) // same as env var USER_TOKEN
    .option(QSOption.imsOrg, "69A7534C5808063C0A494234@AdobeOrg") // same as env var ORG_ID
    .option(QSOption.apiKey, "acp_foundation_queryService") // same as env var SERVICE_API_KEY
    .option("mode", "interactive")
    .option("query", "SELECT * FROM csv10000row_xcm_001 LIMIT 10")
    .load()
```

## Instalação

O uso do [!DNL Spark] SDK requer otimizações de desempenho que precisam ser adicionadas ao `SparkSession`. É possível aplicá-los usando um dos seguintes métodos:

Aplique-o diretamente ao SparkSession atual:

```scala
import com.adobe.platform.query.QSOptimizations
QSOptimizations.apply(spark)
```

Defina a seguinte conff antes ou na criação do SparkSession:

```scala
spark.sql.extensions = com.adobe.platform.query.QSSparkSessionExtensions
```

## Lendo um conjunto de dados

O [!DNL Spark] SDK oferece suporte a dois modos de leitura: interativo e em lote.

O modo interativo cria uma conexão JDBC (Java Database Connectivity) para [!DNL Query Service] e obtém resultados por meio de um JDBC comum `ResultSet` que é automaticamente traduzido para um `DataFrame`. Esse modo funciona de forma semelhante ao método Spark incorporado `spark.read.jdbc()`. Este modo destina-se apenas a conjuntos de dados pequenos e requer apenas um token de usuário para autenticação.

O modo Lote usa o comando COPY [!DNL Query Service]do para gerar conjuntos de resultados Parquet em um local compartilhado. Esses arquivos Parquet podem ser processados posteriormente. Esse modo requer um token de usuário e um token de serviço com o `acp.foundation.catalog.credentials` escopo.

Um exemplo de leitura de um conjunto de dados no modo interativo pode ser visto abaixo:

```scala
val df = spark.read
      .format("com.adobe.platform.query")
      .option("user-token", {USER_TOKEN})
      .option("ims-org", {IMS_ORG})
      .option("api-key", {SERVICE_API_KEY})
      .option("mode", "interactive")
      .option("dataset-id", {DATASET_ID})
      .option("sandbox-name", {SANDBOX_NAME})
      .load()
df.show()
```

Da mesma forma, um exemplo de leitura de um conjunto de dados no modo de lote pode ser visto abaixo:

```scala
val df = spark.read
      .format("com.adobe.platform.query")
      .option("user-token", {USER_TOKEN})
      .option("service-token", {SERVICE_TOKEN})
      .option("ims-org", {IMS_ORG})
      .option("api-key", {SERVICE_API_KEY})
      .option("mode", "batch")
      .option("dataset-id", {DATASET_ID})
      .option("sandbox-name", {SANDBOX_NAME})
      .load()
df.show()
```

### SELECIONAR colunas do conjunto de dados

```scala
df = df.select("column-a", "column-b").show()
```

### Cláusula DISTINCT

A cláusula DISTINCT permite buscar todos os valores distintos em um nível de linha/coluna, removendo todos os valores de duplicado da resposta.

Um exemplo de uso da `distinct()` função pode ser visto abaixo:

```scala
df = df.select("column-a", "column-b").distinct().show()
```

### cláusula WHERE

O [!DNL Spark] SDK permite dois métodos de filtragem: Usando uma expressão SQL ou filtrando por meio de condições.

Um exemplo do uso dessas funções de filtragem pode ser visto abaixo:

#### expressão SQL

```scala
df.where("age > 15")
```

#### Condições de filtragem

```scala
df.where("age" > 15 || "name" = "Steve")
```

### Cláusula ORDER BY

A cláusula ORDER BY permite que os resultados recebidos sejam classificados por uma coluna especificada em uma ordem específica (crescente ou decrescente). No [!DNL Spark] SDK, isso é feito usando a `sort()` função.

Um exemplo de uso da `sort()` função pode ser visto abaixo:

```scala
df = df.sort($"column1", $"column2".desc)
```

### Cláusula LIMIT

A cláusula LIMIT permite que os usuários limitem o número de registros recebidos do conjunto de dados.

Um exemplo de uso da `limit()` função pode ser visto abaixo:

```scala
df = df.limit(100)
```

## Gravação em um conjunto de dados

O [!DNL Spark] SDK suporta a gravação de conjuntos de dados. Os usuários primeiro precisarão recuperar um conjunto de dados anterior para gravar em um novo conjunto de dados.

```scala
val df = spark.read
      .format("com.adobe.platform.query")
      .option("user-token", userToken)
      .option("ims-org", "{IMS_ORG}")
      .option("api-key", "{API_KEY}")
      .option("mode", "interactive")
      .option("dataset-id", "{DATASET_ID}")
      .load()

    df.write
      .format("com.adobe.platform.query")
      .option("user-token", {USER_TOKEN})
      .option("service-token", {SERVICE_TOKEN})
      .option("ims-org", "{IMS_ORG_ID})
      .option("api-key", "{API_KEY}")
      .option("create-dataset", "{DATASET_ID}")
      .save()
```
