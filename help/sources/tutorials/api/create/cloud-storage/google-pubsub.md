---
keywords: Experience Platform;home;popular topics;Google PubSub;google pubsub
solution: Experience Platform
title: Criar uma conexão do Google PubSub-Source usando a API de Serviço de Fluxo
topic: visão geral
type: Tutorial
description: Saiba como conectar o Adobe Experience Platform a uma conta do Google PubSub usando a API de Serviço de Fluxo.
translation-type: tm+mt
source-git-commit: 0af90253f04377149986aedf2e9d3012ca06d4f8
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 2%

---


# Criar uma conexão de origem [!DNL Google PubSub] usando a API de serviço de fluxo

>[!NOTE]
>
>O conector [!DNL Google PubSub] está em beta. Consulte a [Visão geral das fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores marcados com beta.

Este tutorial usa a [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) para guiá-lo pelas etapas para conectar [!DNL Google PubSub] (a seguir, &quot;[!DNL PubSub]&quot;) à Adobe Experience Platform.

## Introdução

Este guia exige uma compreensão prática dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../../../home.md): O Experience Platform permite que os dados sejam assimilados de várias fontes, ao mesmo tempo em que lhe fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.
* [Caixas de proteção](../../../../../sandboxes/home.md): O Experience Platform fornece caixas de proteção virtuais que particionam uma única instância da Plataforma em ambientes virtuais separados para ajudar a desenvolver e desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para criar com êxito uma [!DNL PubSub] conexão de origem usando a API [!DNL Flow Service].

### Reunir credenciais obrigatórias

Para que [!DNL Flow Service] se conecte a [!DNL PubSub], é necessário fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `projectId` | A ID do projeto necessária para autenticar [!DNL PubSub]. |
| `credentials` | A credencial ou chave necessária para autenticar [!DNL PubSub]. |

Para obter mais informações sobre esses valores, consulte o seguinte documento [PubSub authentication](https://cloud.google.com/pubsub/docs/authentication).

### Lendo chamadas de exemplo da API

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção em [como ler chamadas de API de exemplo](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas do Experience Platform.

### Reunir valores para cabeçalhos necessários

Para fazer chamadas para APIs de plataforma, você deve primeiro concluir o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API de Experience Platform, como mostrado abaixo:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Todos os recursos no Experience Platform, incluindo os pertencentes a [!DNL Flow Service], são isolados para caixas de proteção virtuais específicas. Todas as solicitações para APIs de plataforma exigem um cabeçalho que especifique o nome da caixa de proteção em que a operação ocorrerá:

* `x-sandbox-name: {SANDBOX_NAME}`

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho de tipo de mídia adicional:

* `Content-Type: application/json`

## Criar uma conexão

Uma conexão especifica uma fonte e contém suas credenciais para essa fonte. Somente uma conexão é necessária por conta [!DNL PubSub], pois pode ser usada para criar vários fluxos de dados para trazer dados diferentes.

**Formato da API**

```http
POST /connections
```

**Solicitação**

Para criar uma conexão [!DNL PubSub], a ID do provedor e a ID da especificação da conexão devem ser fornecidas como parte da solicitação de POST. A ID do provedor é `521eee4d-8cbe-4906-bb48-fb6bd4450033` e a ID da especificação da conexão é `70116022-a743-464a-bbfe-e226a7f8210c`.

**Formato da API**

```http
POST /connections
```

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Google PubSub connection",
        "description": "Google PubSub connection",
        "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
        "auth": {
            "specName": "Google PubSub authentication credentials",
            "params": {
                "projectId": "{PROJECT_ID}",
                "credentials": "{CREDENTIALS}"
            }
        },
        "connectionSpec": {
            "id": "70116022-a743-464a-bbfe-e226a7f8210c",
            "version": "1.0"
        }
    }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `auth.params.projectId` | A ID do projeto necessária para autenticar [!DNL PubSub]. |
| `auth.params.credentials` | A credencial ou chave necessária para autenticar [!DNL PubSub]. |
| `connectionSpec.id` | A ID de especificação de conexão [!DNL PubSub]: `70116022-a743-464a-bbfe-e226a7f8210c`. |

**Resposta**

Uma resposta bem-sucedida retorna a ID de conexão da conexão [!DNL PubSub] recém-criada. Essa ID é necessária para explorar os dados do armazenamento na nuvem no próximo tutorial.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Próximas etapas

Ao seguir este tutorial, você criou uma conexão [!DNL PubSub] usando a API [!DNL Flow Service] e adquiriu sua ID de conexão exclusiva. Você pode usar essa ID de conexão para [coletar dados de transmissão usando a API do Serviço de Fluxo](../../collect/streaming.md).
