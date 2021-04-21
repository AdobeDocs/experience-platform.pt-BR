---
keywords: Experience Platform, home, tópicos populares, Azure, Armazenamento de arquivos do Azure, Armazenamento de arquivos do Azure
solution: Experience Platform
title: Criar uma Conexão da Fonte de Armazenamento de Arquivo do Azure usando a API do Serviço de Fluxo
topic-legacy: overview
type: Tutorial
description: Saiba como conectar o Armazenamento de Arquivos do Azure à Adobe Experience Platform usando a API do Serviço de Fluxo.
exl-id: 0c585ae2-be2d-4167-b04b-836f7e2c04a9
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '587'
ht-degree: 2%

---

# Crie uma conexão de origem [!DNL Azure File Storage] usando a API [!DNL Flow Service]

>[!NOTE]
>
>O conector [!DNL Azure File Storage] está em beta. Consulte a [Visão geral das Fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores com marca beta.

[!DNL Flow Service] O é usado para coletar e centralizar dados do cliente de várias fontes diferentes no Adobe Experience Platform. O serviço fornece uma interface de usuário e uma RESTful API da qual todas as fontes compatíveis são conectáveis.

Este tutorial usa a API [!DNL Flow Service] para orientá-lo pelas etapas para se conectar [!DNL Azure File Storage] a [!DNL Experience Platform].

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../../../home.md):  [!DNL Experience Platform] O permite que os dados sejam assimilados de várias fontes, além de fornecer a você a capacidade de estruturar, rotular e aprimorar os dados recebidos usando  [!DNL Platform] serviços.
* [Sandboxes](../../../../../sandboxes/home.md):  [!DNL Experience Platform] O fornece sandboxes virtuais que particionam uma única  [!DNL Platform] instância em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito a [!DNL Azure File Storage] usando a API [!DNL Flow Service].

### Obter credenciais necessárias

Para que [!DNL Flow Service] se conecte a [!DNL Azure File Storage], você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `host` | O endpoint da instância [!DNL Azure File Storag]e que você está acessando. |
| `userId` | O usuário com acesso suficiente ao endpoint [!DNL Azure File Storage]. |
| `password` | A senha da sua instância [!DNL Azure File Storage] |
| ID da especificação da conexão | O identificador exclusivo necessário para criar uma conexão. A ID de especificação de conexão para [!DNL Azure File Storage] é: `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8` |

Para obter mais informações sobre a introdução, consulte [este documento do Armazenamento de Arquivos do Azure](https://docs.microsoft.com/en-us/azure/storage/files/storage-how-to-use-files-windows).

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

Uma conexão especifica uma fonte e contém suas credenciais para essa fonte. Somente uma conexão é necessária por conta [!DNL Azure File Storage], pois pode ser usada para criar vários conectores de origem para trazer dados diferentes.

**Formato da API**

```http
POST /connections
```

**Solicitação**

Para criar uma conexão [!DNL Azure File Storage], a ID de especificação de conexão exclusiva deve ser fornecida como parte da solicitação POST. A ID de especificação de conexão para [!DNL Azure File Storage] é `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8`.

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
| `auth.params.host` | O endpoint da instância [!DNL Azure File Storage] que você está acessando. |
| `auth.params.userId` | O usuário com acesso suficiente ao endpoint [!DNL Azure File Storage]. |
| `auth.params.password` | A chave de acesso [!DNL Azure File Storage]. |
| `connectionSpec.id` | A ID da especificação de conexão [!DNL Azure File Storage]: `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8`. |

**Resposta**

Uma resposta bem-sucedida retorna detalhes da conexão recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID é necessária para explorar seus dados no próximo tutorial.

```json
{
    "id": "f9377f50-607a-4818-b77f-50607a181860",
    "etag": "\"2f0276fa-0000-0200-0000-5eab3abb0000\""
}
```

## Próximas etapas

Ao seguir este tutorial, você criou uma conexão [!DNL Azure File Storage] usando a API [!DNL Flow Service] e obteve o valor de ID exclusivo da conexão. Você pode usar essa ID no próximo tutorial à medida que aprende a [explorar um armazenamento em nuvem de terceiros usando a API do Serviço de Fluxo](../../explore/cloud-storage.md).
