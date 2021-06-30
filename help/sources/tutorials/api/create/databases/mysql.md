---
keywords: Experience Platform, home, tópicos populares, MySQL, mysql
solution: Experience Platform
title: Criar uma conexão base [!DNL MySQL] usando a API do Serviço de fluxo
topic-legacy: overview
type: Tutorial
description: Saiba como conectar o Adobe Experience Platform ao MySQL usando a API do Serviço de Fluxo.
exl-id: 273da568-84ed-4a3d-bfea-0f5b33f1551a
source-git-commit: 5fb5f0ce8bd03ba037c6901305ba17f8939eb9ce
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 1%

---

# Crie uma conexão base [!DNL MySQL] usando a API [!DNL Flow Service]

Uma conexão base representa a conexão autenticada entre uma fonte e o Adobe Experience Platform.

Este tutorial o orienta pelas etapas para criar uma conexão básica para [!DNL MySQL] usando a [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../../../home.md):  [!DNL Experience Platform] O permite que os dados sejam assimilados de várias fontes, além de fornecer a você a capacidade de estruturar, rotular e aprimorar os dados recebidos usando  [!DNL Platform] serviços.
* [Sandboxes](../../../../../sandboxes/home.md):  [!DNL Experience Platform] O fornece sandboxes virtuais que particionam uma única  [!DNL Platform] instância em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito a [!DNL MySQL] usando a API [!DNL Flow Service].

### Obter credenciais necessárias

Para que [!DNL Flow Service] se conecte ao armazenamento [!DNL MySQL], você deve fornecer o valor da seguinte propriedade de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `connectionString` | A cadeia de conexão [!DNL MySQL] associada à sua conta. O padrão da string de conexão [!DNL MySQL] é: `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`. |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de origem, incluindo especificações de autenticação relacionadas à criação das conexões base e de origem. A ID de especificação de conexão para [!DNL MySQL] é `26d738e0-8963-47ea-aadf-c60de735468a`. |

Para obter mais informações sobre como obter uma string de conexão, consulte este [[!DNL MySQL] documento](https://dev.mysql.com/doc/connector-net/en/connector-net-connections-string.html).

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da plataforma com êxito, consulte o guia sobre como [começar a usar APIs da plataforma](../../../../../landing/api-guide.md).

## Criar uma conexão base

Uma conexão base retém informações entre a fonte e a Plataforma, incluindo as credenciais de autenticação da fonte, o estado atual da conexão e a ID de conexão base exclusiva. A ID de conexão básica permite explorar e navegar pelos arquivos da fonte e identificar os itens específicos que deseja assimilar, incluindo informações sobre os tipos e formatos de dados.

Para criar uma ID de conexão base, faça uma solicitação de POST ao endpoint `/connections`, fornecendo as credenciais de autenticação [!DNL MySQL] como parte dos parâmetros da solicitação.

**Formato da API**

```https
POST /connections
```

**Solicitação**

A solicitação a seguir cria uma conexão base para [!DNL MySQL]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "[!DNL MySQL] Test Connection",
        "description": "[!DNL MySQL] Test Connection",
        "auth": {
            "specName": "Connection String Based Authentication",
            "params": {
                "connectionString": "Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "26d738e0-8963-47ea-aadf-c60de735468a",
            "version": "1.0"
        }
    }'
```

| Propriedade | Descrição |
| --------- | ----------- |
| `auth.params.connectionString` | A cadeia de conexão [!DNL MySQL] associada à sua conta. O padrão da string de conexão [!DNL MySQL] é: `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`. |
| `connectionSpec.id` | A ID da especificação de conexão [!DNL MySQL]: `26d738e0-8963-47ea-aadf-c60de735468a`. |

**Resposta**

Uma resposta bem-sucedida retorna detalhes da conexão base recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID é necessária para explorar seu banco de dados no próximo tutorial.

```json
{
    "id": "1a444165-3439-4c16-8441-653439dc166a",
    "etag": "\"5b04c219-0000-0200-0000-5e179c8f0000\""
}
```

## Próximas etapas

Ao seguir este tutorial, você criou uma conexão [!DNL MySQL] usando a API [!DNL Flow Service] e obteve o valor de ID exclusivo da conexão. Você pode usar essa ID de conexão no próximo tutorial à medida que aprende a [explorar bancos de dados ou sistemas NoSQL usando a API do Serviço de Fluxo](../../explore/database-nosql.md).
