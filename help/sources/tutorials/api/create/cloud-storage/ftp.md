---
keywords: Experience Platform; home; tópicos populares; Protocolo de transferência de ficheiros; protocolo de transferência de arquivos
solution: Experience Platform
title: Criar uma conexão de origem FTP usando a API do Serviço de fluxo
topic-legacy: overview
type: Tutorial
description: Saiba como conectar o Adobe Experience Platform a um servidor FTP (File Transfer Protocol) usando a API de Serviço de Fluxo.
exl-id: a7bef346-b357-49bc-ac54-ac8b42adac50
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 2%

---

# Criar uma conexão de origem FTP usando a API [!DNL Flow Service]

>[!NOTE]
>
>O conector FTP está em beta. Os recursos e a documentação estão sujeitos a alterações. Consulte a [Visão geral das Fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores com marca beta.

Este tutorial usa a API [!DNL Flow Service] para orientá-lo pelas etapas para conectar [!DNL Experience Platform] a um servidor FTP (File Transfer Protocol).

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../../../home.md):  [!DNL Experience Platform] O permite que os dados sejam assimilados de várias fontes, além de fornecer a você a capacidade de estruturar, rotular e aprimorar os dados recebidos usando  [!DNL Platform] serviços.
* [Sandboxes](../../../../../sandboxes/home.md):  [!DNL Experience Platform] O fornece sandboxes virtuais que particionam uma única  [!DNL Platform] instância em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito a um servidor FTP usando a API [!DNL Flow Service].

### Obter credenciais necessárias

Para que [!DNL Flow Service] se conecte ao FTP, você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `host` | O nome ou endereço IP associado ao servidor FTP. |
| `username` | O nome de usuário com acesso ao seu servidor FTP. |
| `password` | A senha do servidor FTP. |

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

Uma conexão especifica uma fonte e contém suas credenciais para essa fonte. Somente uma conexão é necessária por conta FTP, pois pode ser usada para criar vários conectores de origem para trazer dados diferentes.

### Criar uma conexão FTP usando autenticação básica

Para criar uma conexão FTP usando autenticação básica, faça uma solicitação POST para a API [!DNL Flow Service], fornecendo valores para as `host`, `userName` e `password` da sua conexão.

**Formato da API**

```http
POST /connections
```

**Solicitação**

Para criar uma conexão FTP, a ID de especificação de conexão exclusiva deve ser fornecida como parte da solicitação do POST. A ID da especificação de conexão para FTP é `fb2e94c9-c031-467d-8103-6bd6e0a432f2`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `auth.params.host` | O nome do host do seu servidor FTP. |
| `auth.params.username` | O nome de usuário associado ao servidor FTP. |
| `auth.params.password` | A senha associada ao servidor FTP. |
| `connectionSpec.id` | A ID de especificação da conexão do servidor FTP: `fb2e94c9-c031-467d-8103-6bd6e0a432f2` |

**Resposta**

Uma resposta bem-sucedida retorna o identificador exclusivo (`id`) da conexão recém-criada. Essa ID é necessária para explorar seu servidor FTP no próximo tutorial.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

## Próximas etapas

Ao seguir este tutorial, você criou uma conexão FTP usando a API [!DNL Flow Service] e obteve o valor de ID exclusivo da conexão. Você pode usar essa ID de conexão para [explorar armazenamentos em nuvem usando a API do Serviço de Fluxo](../../explore/cloud-storage.md) ou [assimilar dados do Parquet usando a API do Serviço de Fluxo](../../cloud-storage-parquet.md).
