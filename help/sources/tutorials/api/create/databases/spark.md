---
keywords: Experience Platform, home, tópicos populares, Apache Spark, apache spark, Azure HDInsights
solution: Experience Platform
title: Criar um Apache Spark na Conexão de Origem do Azure HDInsights usando a API do Serviço de Fluxo
topic-legacy: overview
type: Tutorial
description: Saiba como conectar o Apache Spark no Azure HDInsights ao Adobe Experience Platform usando a API do Serviço de Fluxo.
exl-id: 1f7ca86e-32f4-45f7-92c2-f87c5c0c4ea4
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 2%

---

# Crie um [!DNL Apache Spark] em [!DNL Azure] conexão de origem do HDInsights usando a API [!DNL Flow Service]

>[!NOTE]
>
>O conector [!DNL Apache Spark] em [!DNL Azure HDInsights] está na beta. Consulte a [Visão geral das Fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores com marca beta.

[!DNL Flow Service] O é usado para coletar e centralizar dados do cliente de várias fontes diferentes no Adobe Experience Platform. O serviço fornece uma interface de usuário e uma RESTful API da qual todas as fontes compatíveis são conectáveis.

Este tutorial usa a API [!DNL Flow Service] para orientá-lo pelas etapas para se conectar [!DNL Apache Spark] em [!DNL Azure HDInsights] (a seguir chamada &quot;[!DNL Spark]&quot;) a [!DNL Experience Platform].

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../../../home.md):  [!DNL Experience Platform] O permite que os dados sejam assimilados de várias fontes, além de fornecer a você a capacidade de estruturar, rotular e aprimorar os dados recebidos usando  [!DNL Platform] serviços.
* [Sandboxes](../../../../../sandboxes/home.md):  [!DNL Experience Platform] O fornece sandboxes virtuais que particionam uma única  [!DNL Platform] instância em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito a [!DNL Spark] usando a API [!DNL Flow Service].

### Obter credenciais necessárias

Para que [!DNL Flow Service] se conecte a [!DNL Spark], você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `host` | O endereço IP ou o nome do host do servidor [!DNL Spark]. |
| `username` | O nome de usuário usado para acessar o Servidor [!DNL Spark]. |
| `password` | A senha correspondente ao usuário. |
| `connectionSpec.id` | O identificador exclusivo necessário para criar uma conexão. A ID de especificação de conexão para [!DNL Spark] é: `6a8d82bc-1caf-45d1-908d-cadabc9d63a6` |

Para obter mais informações sobre a introdução, consulte [este documento Spark](https://docs.microsoft.com/en-us/azure/hdinsight/spark/apache-spark-overview).

### Lendo exemplos de chamadas de API

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações do . Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de exemplo retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) no [!DNL Experience Platform] guia de solução de problemas.

### Coletar valores para cabeçalhos necessários

Para fazer chamadas para [!DNL Platform] APIs, primeiro complete o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API [!DNL Experience Platform], conforme mostrado abaixo:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Todos os recursos em [!DNL Experience Platform], incluindo aqueles pertencentes a [!DNL Flow Service], são isolados para sandboxes virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifica o nome da sandbox em que a operação ocorrerá:

* `x-sandbox-name: {SANDBOX_NAME}`

Todas as solicitações que contêm uma carga útil (POST, PUT, PATCH) exigem um cabeçalho de tipo de mídia adicional:

* `Content-Type: application/json`

## Criar uma conexão

Uma conexão especifica uma fonte e contém suas credenciais para essa fonte. Somente uma conexão é necessária por conta [!DNL Spark], pois pode ser usada para criar vários conectores de origem para trazer dados diferentes.

**Formato da API**

```http
POST /connections
```

**Solicitação**

Para criar uma conexão [!DNL Spark], a ID de especificação de conexão exclusiva deve ser fornecida como parte da solicitação POST. A ID de especificação de conexão para [!DNL Spark] é `6a8d82bc-1caf-45d1-908d-cadabc9d63a6`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Spark test connection",
        "description": "A Spark test connection",
        "auth": {
            "specName": "HDInsights Basic Authentication",
        "params": {
            "host" :  "{HOST}",
            "username" : "{USERNAME}",
            "password" :"{PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "6a8d82bc-1caf-45d1-908d-cadabc9d63a6",
            "version": "1.0"
        }
    }'
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `auth.params.host` | O host do servidor [!DNL Spark]. |
| `auth.params.username` | O nome de usuário associado à sua conexão [!DNL Spark]. |
| `auth.params.password` | A senha associada à conexão [!DNL Spark]. |
| `connectionSpec.id` | A ID da especificação de conexão [!DNL Spark]: `6a8d82bc-1caf-45d1-908d-cadabc9d63a6`. |

**Resposta**

Uma resposta bem-sucedida retorna detalhes da conexão recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID é necessária para explorar seus dados no próximo tutorial.

```json
{
    "id": "a45f2f58-e3a2-46ba-9f2f-58e3a2b6baf2",
    "etag": "\"900009d6-0000-0200-0000-5e8500010000\""
}
```

## Próximas etapas

Ao seguir este tutorial, você criou uma conexão [!DNL Spark] usando a API [!DNL Flow Service] e obteve o valor de ID exclusivo da conexão. Você pode usar essa ID no próximo tutorial à medida que aprende a [explorar bancos de dados usando a API do Serviço de Fluxo](../../explore/database-nosql.md).
