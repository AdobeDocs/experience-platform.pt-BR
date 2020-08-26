---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Criar um conector SFTP usando a API de Serviço de Fluxo
topic: overview
translation-type: tm+mt
source-git-commit: 690ddbd92f0a2e4e06b988e761dabff399cd2367
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 2%

---


# Criar um conector SFTP usando a [!DNL Flow Service] API

>[!NOTE]
>
>O conector SFTP está em beta. Os recursos e a documentação estão sujeitos a alterações. Consulte a visão geral [das](../../../../home.md#terms-and-conditions) Fontes para obter mais informações sobre o uso de conectores com rótulo beta.

[!DNL Flow Service] é usada para coletar e centralizar dados do cliente de várias fontes diferentes no Adobe Experience Platform. O serviço fornece uma interface de usuário e uma RESTful API a partir da qual todas as fontes compatíveis são conectáveis.

Este tutorial usa a [!DNL Flow Service] API para guiá-lo pelas etapas para se conectar [!DNL Experience Platform] a um servidor SFTP (Secure File Transfer Protocol).

Se você preferir usar a interface do usuário no [!DNL Experience Platform], o tutorial [da](../../../ui/create/cloud-storage/ftp-sftp.md) interface do usuário fornece instruções passo a passo para executar ações semelhantes.

## Introdução

Este guia exige uma compreensão prática dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../../../home.md): [!DNL Experience Platform] permite que os dados sejam ingeridos de várias fontes e, ao mesmo tempo, fornece a você a capacidade de estruturar, rotular e aprimorar os dados recebidos usando [!DNL Platform] serviços.
* [Caixas de proteção](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornece caixas de proteção virtuais que particionam uma única [!DNL Platform] instância em ambientes virtuais separados para ajudar a desenvolver e desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito a um servidor SFTP usando a [!DNL Flow Service] API.

### Reunir credenciais obrigatórias

Para [!DNL Flow Service] se conectar ao SFTP, é necessário fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `host` | O nome ou endereço IP associado ao servidor SFTP. |
| `username` | O nome de usuário com acesso ao seu servidor SFTP. |
| `password` | A senha do servidor SFTP. |

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

Uma conexão especifica uma fonte e contém suas credenciais para essa fonte. Somente uma conexão é necessária por conta SFTP, pois pode ser usada para criar vários conectores de origem para trazer dados diferentes.

**Formato da API**

```http
POST /connections
```

**Solicitação**

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d  "auth": {
        "specName": "Basic Authentication for sftp",
        "params": {
            "host": "{HOST_NAME}",
            "userName": "{USER_NAME}",
            "password": "{PASSWORD}"
        }
    },
    "connectionSpec": {
        "id": "b7bf2577-4520-42c9-bae9-cad01560f7bc",
        "version": "1.0"
    }
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `auth.params.host` | O nome do host do servidor SFTP. |
| `auth.params.username` | O nome de usuário associado ao servidor SFTP. |
| `auth.params.password` | A senha associada ao servidor SFTP. |
| `connectionSpec.id` | A ID da especificação da conexão do servidor STFP: `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

**Resposta**

Uma resposta bem-sucedida retorna o identificador exclusivo (`id`) da conexão recém-criada. Essa ID é necessária para explorar o servidor SFTP no próximo tutorial.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

## Próximas etapas

Ao seguir este tutorial, você criou uma conexão SFTP usando a [!DNL Flow Service] API e obteve o valor de ID exclusivo da conexão. Você pode usar essa ID de conexão para [explorar armazenamentos em nuvem usando a API](../../explore/cloud-storage.md) do Serviço de Fluxo ou [assimilando dados de parquet usando a API](../../cloud-storage-parquet.md)do Serviço de Fluxo.
