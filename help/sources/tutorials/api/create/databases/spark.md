---
keywords: Experience Platform;home;popular topics;Apache Spark;apache spark;Azure HDInsights
solution: Experience Platform
title: Criar um Apache Spark na Conexão de Origem do Azure HDInsights usando a API de Serviço de Fluxo
topic: overview
type: Tutorial
description: Saiba como conectar o Apache Spark no Azure HDInsights à Adobe Experience Platform usando a API de Serviço de Fluxo.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 2%

---


# Crie uma [!DNL Apache Spark] em [!DNL Azure] conexão de origem HDInsights usando a API [!DNL Flow Service]

>[!NOTE]
>
>O conector [!DNL Apache Spark] no conector [!DNL Azure HDInsights] está em beta. Consulte a [Visão geral das fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores marcados com beta.

[!DNL Flow Service] é usada para coletar e centralizar dados do cliente de várias fontes diferentes no Adobe Experience Platform. O serviço fornece uma interface de usuário e uma RESTful API a partir da qual todas as fontes compatíveis são conectáveis.

Este tutorial usa a API [!DNL Flow Service] para guiá-lo pelas etapas para conectar [!DNL Apache Spark] em [!DNL Azure HDInsights] (a seguir, &quot;[!DNL Spark]&quot;) a [!DNL Experience Platform].

## Introdução

Este guia exige uma compreensão prática dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../../../home.md):  [!DNL Experience Platform] permite que os dados sejam ingeridos de várias fontes e, ao mesmo tempo, fornece a você a capacidade de estruturar, rotular e aprimorar os dados recebidos usando  [!DNL Platform] serviços.
* [Caixas de proteção](../../../../../sandboxes/home.md):  [!DNL Experience Platform] fornece caixas de proteção virtuais que particionam uma única  [!DNL Platform] instância em ambientes virtuais separados para ajudar a desenvolver e desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito a [!DNL Spark] usando a API [!DNL Flow Service].

### Reunir credenciais obrigatórias

Para que [!DNL Flow Service] se conecte com [!DNL Spark], é necessário fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `host` | O endereço IP ou o nome do host do servidor [!DNL Spark]. |
| `username` | O nome de usuário que você usa para acessar o [!DNL Spark] Server. |
| `password` | A senha correspondente ao usuário. |
| `connectionSpec.id` | O identificador exclusivo necessário para criar uma conexão. A ID de especificação de conexão para [!DNL Spark] é: `6a8d82bc-1caf-45d1-908d-cadabc9d63a6` |

Para obter mais informações sobre a introdução, consulte [este documento Spark](https://docs.microsoft.com/en-us/azure/hdinsight/spark/apache-spark-overview).

### Lendo chamadas de exemplo da API

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção em [como ler chamadas de API de exemplo](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas [!DNL Experience Platform].

### Reunir valores para cabeçalhos necessários

Para fazer chamadas para [!DNL Platform] APIs, você deve primeiro concluir o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API [!DNL Experience Platform], como mostrado abaixo:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Todos os recursos em [!DNL Experience Platform], incluindo os pertencentes a [!DNL Flow Service], são isolados para caixas de proteção virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifique o nome da caixa de proteção em que a operação ocorrerá:

* `x-sandbox-name: {SANDBOX_NAME}`

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho de tipo de mídia adicional:

* `Content-Type: application/json`

## Criar uma conexão

Uma conexão especifica uma fonte e contém suas credenciais para essa fonte. Somente uma conexão é necessária por conta [!DNL Spark], pois pode ser usada para criar vários conectores de origem para trazer dados diferentes.

**Formato da API**

```http
POST /connections
```

**Solicitação**

Para criar uma conexão [!DNL Spark], sua ID exclusiva de especificação de conexão deve ser fornecida como parte da solicitação de POST. A ID de especificação de conexão para [!DNL Spark] é `6a8d82bc-1caf-45d1-908d-cadabc9d63a6`.

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
| `auth.params.password` | A senha associada à sua conexão [!DNL Spark]. |
| `connectionSpec.id` | A ID de especificação de conexão [!DNL Spark]: `6a8d82bc-1caf-45d1-908d-cadabc9d63a6`. |

**Resposta**

Uma resposta bem-sucedida retorna detalhes da conexão recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID é necessária para explorar seus dados no próximo tutorial.

```json
{
    "id": "a45f2f58-e3a2-46ba-9f2f-58e3a2b6baf2",
    "etag": "\"900009d6-0000-0200-0000-5e8500010000\""
}
```

## Próximas etapas

Ao seguir este tutorial, você criou uma conexão [!DNL Spark] usando a API [!DNL Flow Service] e obteve o valor de ID exclusivo da conexão. Você pode usar essa ID no próximo tutorial à medida que aprende a [explorar bancos de dados usando a API de Serviço de Fluxo](../../explore/database-nosql.md).