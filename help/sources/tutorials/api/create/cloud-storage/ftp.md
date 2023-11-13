---
keywords: Experience Platform;página inicial;tópicos populares; Protocolo de transferência de arquivos; protocolo de transferência de arquivos
solution: Experience Platform
title: Criar uma conexão base FTP usando a API do serviço de fluxo
type: Tutorial
description: Saiba como conectar o Adobe Experience Platform a um servidor FTP (File Transfer Protocol, protocolo de transferência de arquivos) usando a API do serviço de fluxo.
exl-id: a7bef346-b357-49bc-ac54-ac8b42adac50
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 6%

---

# Crie uma conexão base FTP usando o [!DNL Flow Service] API

>[!NOTE]
>
>O conector FTP está na versão beta. Os recursos e a documentação estão sujeitos a alterações. Consulte a [Visão geral das fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores rotulados com beta.

Uma conexão base representa a conexão autenticada entre uma origem e o Adobe Experience Platform.

Este tutorial guiará você pelas etapas para criar uma conexão básica para [!DNL FTP] (Protocolo de transferência de arquivo) usando o [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introdução

Este manual necessita de uma compreensão funcional dos seguintes componentes da Adobe Experience Platform:

* [Origens](../../../../home.md): [!DNL Experience Platform] O permite que os dados sejam assimilados de várias fontes e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando o [!DNL Platform] serviços.
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] O fornece sandboxes virtuais que particionam uma única [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem as informações adicionais que você precisará saber para se conectar com êxito a um [!DNL FTP] servidor usando o [!DNL Flow Service] API.

### Coletar credenciais necessárias

A fim de [!DNL Flow Service] para se conectar a [!DNL FTP], você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `host` | O nome ou endereço IP associado à [!DNL FTP] servidor. |
| `username` | O nome de usuário com acesso ao seu [!DNL FTP] servidor. |
| `password` | A senha do [!DNL FTP] servidor. |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de uma origem, incluindo especificações de autenticação relacionadas à criação das conexões de base e de origem. A ID da especificação de conexão para [!DNL FTP] é: `fb2e94c9-c031-467d-8103-6bd6e0a432f2`. |

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da Platform com êxito, consulte o manual em [introdução às APIs da Platform](../../../../../landing/api-guide.md).

## Crie uma conexão básica

Uma conexão base retém informações entre sua origem e a Platform, incluindo as credenciais de autenticação da origem, o estado atual da conexão e sua ID de conexão base exclusiva. A ID de conexão básica permite explorar e navegar pelos arquivos de dentro da origem e identificar os itens específicos que deseja assimilar, incluindo informações sobre os tipos de dados e formatos.

Para criar um ID de conexão base, faça uma solicitação POST ao `/connections` ao fornecer sua [!DNL FTP] credenciais de autenticação como parte dos parâmetros de solicitação.

**Formato da API**

```http
POST /connections
```

**Solicitação**

A solicitação a seguir cria uma conexão básica para [!DNL FTP]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d  '{
        "name": "FTP connector with password",
        "description": "FTP connector password",
        "auth": {
            "specName": "Basic Authentication for FTP",
            "params": {
                "host": "{HOST}",
                "userName": "{USERNAME}",
                "password": "{PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "fb2e94c9-c031-467d-8103-6bd6e0a432f2",
            "version": "1.0"
        }
    }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `auth.params.host` | O nome do host do servidor FTP. |
| `auth.params.username` | O nome de usuário associado ao servidor FTP. |
| `auth.params.password` | A senha associada ao servidor FTP. |
| `connectionSpec.id` | A ID da especificação da conexão do servidor FTP: `fb2e94c9-c031-467d-8103-6bd6e0a432f2` |

**Resposta**

Uma resposta bem-sucedida retorna o identificador exclusivo (`id`) da conexão recém-criada. Essa ID é necessária para explorar o servidor FTP no próximo tutorial.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

## Próximas etapas

Ao seguir este tutorial, você criou uma conexão FTP usando o [!DNL Flow Service] e obtiveram o valor de identificador exclusivo da conexão. Você pode usar essa ID de conexão para [explorar armazenamentos em nuvem usando a API do Serviço de fluxo](../../explore/cloud-storage.md).
