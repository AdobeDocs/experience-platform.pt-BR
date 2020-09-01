---
keywords: Experience Platform;home;popular topics;Phoenix;phoenix
solution: Experience Platform
title: Crie um conector Phoenix usando a API de Serviço de Fluxo
topic: overview
description: Este tutorial usa a API de Serviço de Fluxo para guiá-lo pelas etapas para conectar um banco de dados Phoenix ao Experience Platform.
translation-type: tm+mt
source-git-commit: 5959d4344ec1c16542de045899ce74beb39a7bc4
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 1%

---


# Criar um [!DNL Phoenix] conector usando a [!DNL Flow Service] API

>[!NOTE]
>
>O [!DNL Phoenix] conector está em beta. Consulte a visão geral [das](../../../../home.md#terms-and-conditions) Fontes para obter mais informações sobre o uso de conectores com rótulo beta.

[!DNL Flow Service] é usada para coletar e centralizar dados do cliente de várias fontes diferentes no Adobe Experience Platform. O serviço fornece uma interface de usuário e uma RESTful API a partir da qual todas as fontes compatíveis são conectáveis.

Este tutorial usa a [!DNL Flow Service] API para guiá-lo pelas etapas para conectar um [!DNL Phoenix] banco de dados ao [!DNL Experience Platform].

## Introdução

Este guia exige uma compreensão prática dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../../../home.md): [!DNL Experience Platform] permite que os dados sejam ingeridos de várias fontes e, ao mesmo tempo, fornece a você a capacidade de estruturar, rotular e aprimorar os dados recebidos usando [!DNL Platform] serviços.
* [Caixas de proteção](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornece caixas de proteção virtuais que particionam uma única [!DNL Platform] instância em ambientes virtuais separados para ajudar a desenvolver e desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito [!DNL Phoenix] usando a [!DNL Flow Service] API.

### Reunir credenciais obrigatórias

Para [!DNL Flow Service] se conectar com [!DNL Phoenix], é necessário fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `host` | O endereço IP ou o nome do host do [!DNL Phoenix] servidor. |
| `username` | O nome de usuário que você usa para acessar o [!DNL Phoenix] Servidor. |
| `password` | A senha correspondente ao usuário. |
| `port` | A porta TCP que o [!DNL Phoenix] servidor usa para escutar as conexões do cliente. Se você se conectar ao [!DNL Azure] HDInsights, especifique a porta como 443. |
| `httpPath` | O URL parcial correspondente ao [!DNL Phoenix] servidor. Especifique /hbasephonix0 se estiver usando o cluster [!DNL Azure] HDInsights. |
| `enableSsl` | Um valor booliano. Especifica se as conexões com o servidor são criptografadas usando SSL. |
| `connectionSpec.id` | O identificador exclusivo necessário para criar uma conexão. A ID de especificação de conexão para [!DNL Phoenix] é: `102706fb-a5cd-42ee-afe0-bc42f017ff43` |

Para obter mais informações sobre como começar, consulte [este documento](https://python-phoenixdb.readthedocs.io/en/latest/api.html)Phoenix.

### Lendo chamadas de exemplo da API

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção sobre [como ler chamadas](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de exemplo no guia de [!DNL Experience Platform] solução de problemas.

### Reunir valores para cabeçalhos necessários

Para fazer chamadas para [!DNL Platform] APIs, você deve primeiro concluir o tutorial [de](../../../../../tutorials/authentication.md)autenticação. A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de [!DNL Experience Platform] API, como mostrado abaixo:

* Autorização: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos no [!DNL Experience Platform], incluindo os pertencentes ao [!DNL Flow Service], são isolados para caixas de proteção virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifique o nome da caixa de proteção em que a operação ocorrerá:

* x-sandbox-name: `{SANDBOX_NAME}`

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho de tipo de mídia adicional:

* Tipo de conteúdo: `application/json`

## Criar uma conexão

Uma conexão especifica uma fonte e contém suas credenciais para essa fonte. Somente uma conexão é necessária por [!DNL Phoenix] conta, pois pode ser usada para criar vários conectores de origem para trazer dados diferentes.

**Formato da API**

```http
POST /connections
```

**Solicitação**

Para criar uma [!DNL Phoenix] conexão, sua ID exclusiva de especificação de conexão deve ser fornecida como parte da solicitação de POST. A ID de especificação de conexão para [!DNL Phoenix] é `102706fb-a5cd-42ee-afe0-bc42f017ff43`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Phoenix test connection",
        "description": "Phoenix test connection",
        "auth": {
            "specName": "Basic Authentication",
        "params": {
            "host" :  "{HOST}",
            "username" : "{USERNAME}",
            "password" :"{PASSWORD}",
            "port" : {PORT},
            "httpPath" : "{PATH}",
            "enableSsl" : {SSL}
            }
        },
        "connectionSpec": {
            "id": "102706fb-a5cd-42ee-afe0-bc42f017ff43",
            "version": "1.0"
        }
    }'
```

| Propriedade | Descrição |
| --------- | ----------- |
| `auth.params.host` | The host of the [!DNL Phoenix] server. |
| `auth.params.username` | O nome de usuário associado à sua [!DNL Phoenix] conexão. |
| `auth.params.password` | A senha associada à sua [!DNL Phoenix] conexão. |
| `auth.params.port` | A porta TCP para a sua [!DNL Phoenix] conexão. |
| `auth.params.httpPath` | O caminho http parcial para sua [!DNL Phoenix] conexão. |
| `auth.params.enableSsl` | O valor booliano que especifica se as conexões com o servidor são criptografadas usando SSL. |
| `connectionSpec.id` | A ID da especificação da [!DNL Phoenix] conexão: `102706fb-a5cd-42ee-afe0-bc42f017ff43`. |

**Resposta**

Uma resposta bem-sucedida retorna detalhes da conexão recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID é necessária para explorar seus dados no próximo tutorial.

```json
{
    "id": "0d982fff-c443-403e-982f-ffc443f03e37",
    "etag": "\"830082dc-0000-0200-0000-5e84ee560000\""
}
```

## Próximas etapas

Ao seguir este tutorial, você criou uma [!DNL Phoenix] conexão usando a [!DNL Flow Service] API e obteve o valor de ID exclusivo da conexão. Você pode usar essa ID no próximo tutorial à medida que aprende a [explorar bancos de dados usando a API](../../explore/database-nosql.md)do Serviço de Fluxo.