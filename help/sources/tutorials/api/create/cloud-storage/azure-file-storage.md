---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Criar um conector de Armazenamento de Arquivo do Azure usando a API de Serviço de Fluxo
topic: overview
translation-type: tm+mt
source-git-commit: 690ddbd92f0a2e4e06b988e761dabff399cd2367
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 2%

---


# Criar um [!DNL Azure File Storage] conector usando a [!DNL Flow Service] API

>[!NOTE]
>
>O [!DNL Azure File Storage] conector está em beta. Consulte a visão geral [das](../../../../home.md#terms-and-conditions) Fontes para obter mais informações sobre o uso de conectores com rótulo beta.

[!DNL Flow Service] é usada para coletar e centralizar dados do cliente de várias fontes diferentes no Adobe Experience Platform. O serviço fornece uma interface de usuário e uma RESTful API a partir da qual todas as fontes compatíveis são conectáveis.

Este tutorial usa a [!DNL Flow Service] API para guiá-lo pelas etapas para se conectar [!DNL Azure File Storage] a [!DNL Experience Platform].

## Introdução

Este guia exige uma compreensão prática dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../../../home.md): [!DNL Experience Platform] permite que os dados sejam ingeridos de várias fontes e, ao mesmo tempo, fornece a você a capacidade de estruturar, rotular e aprimorar os dados recebidos usando [!DNL Platform] serviços.
* [Caixas de proteção](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornece caixas de proteção virtuais que particionam uma única [!DNL Platform] instância em ambientes virtuais separados para ajudar a desenvolver e desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito [!DNL Azure File Storage] usando a [!DNL Flow Service] API.

### Reunir credenciais obrigatórias

Para [!DNL Flow Service] se conectar com [!DNL Azure File Storage], é necessário fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `host` | O terminal da instância [!DNL Azure File Storag]e que você está acessando. |
| `userId` | O usuário com acesso suficiente ao ponto de [!DNL Azure File Storage] extremidade. |
| `password` | A senha da sua [!DNL Azure File Storage] instância |
| ID da especificação da conexão | O identificador exclusivo necessário para criar uma conexão. A ID de especificação de conexão para [!DNL Azure File Storage] é: `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8` |

Para obter mais informações sobre a introdução, consulte [este documento](https://docs.microsoft.com/en-us/azure/storage/files/storage-how-to-use-files-windows)de Armazenamento de Arquivo do Azure.

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

Uma conexão especifica uma fonte e contém suas credenciais para essa fonte. Somente uma conexão é necessária por conta do Armazenamento de Arquivo do Azure, pois pode ser usada para criar vários conectores de origem para trazer dados diferentes.

**Formato da API**

```http
POST /connections
```

**Solicitação**

A solicitação a seguir cria uma nova [!DNL Azure File Storage] conexão, configurada pelas propriedades fornecidas na carga:


```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
        -d '{
        "name": "Azure File Storage connection",
        "description": "An Azure File Storage test connection",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                    "host": "{HOST}",
                    "userId": "{USER_ID}",
                    "password": "{PASSWORD}"
                }
        },
        "connectionSpec": {
            "id": "be5ec48c-5b78-49d5-b8fa-7c89ec4569b8",
            "version": "1.0"
        }
    }'
```

| Propriedade | Descrição |
| --------- | ----------- |
| `auth.params.host` | O ponto de extremidade da [!DNL Azure File Storage] instância que você está acessando. |
| `auth.params.userId` | O usuário com acesso suficiente ao ponto de [!DNL Azure File Storage] extremidade. |
| `auth.params.password` | A chave [!DNL Azure File Storage] de acesso. |
| `connectionSpec.id` | A ID da especificação da [!DNL Azure File Storage] conexão: `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8`. |

**Resposta**

Uma resposta bem-sucedida retorna detalhes da conexão recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID é necessária para explorar seus dados no próximo tutorial.

```json
{
    "id": "f9377f50-607a-4818-b77f-50607a181860",
    "etag": "\"2f0276fa-0000-0200-0000-5eab3abb0000\""
}
```

## Próximas etapas

Ao seguir este tutorial, você criou uma [!DNL Azure File Storage] conexão usando a [!DNL Flow Service] API e obteve o valor de ID exclusivo da conexão. Você pode usar essa ID no próximo tutorial à medida que aprende a [explorar um armazenamento em nuvem de terceiros usando a API](../../explore/cloud-storage.md)de Serviço de Fluxo.
