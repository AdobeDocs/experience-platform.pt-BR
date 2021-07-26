---
keywords: Experience Platform; home; tópicos populares; Vertica; vertica
solution: Experience Platform
title: Criar uma conexão básica HP Vertica usando a API do Serviço de fluxo
topic-legacy: overview
type: Tutorial
description: Saiba como conectar o HP Vertica à Adobe Experience Platform usando a API do Serviço de Fluxo.
exl-id: 37f831c1-7c82-462a-8338-a0bcaaf08cd1
source-git-commit: 3506e8307d5f6dbdb11a04911ddbd6dc81b8278f
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 1%

---

# Crie uma conexão base [!DNL HP Vertica] usando a API [!DNL Flow Service]

>[!NOTE]
>
>O conector [!DNL HP Vertica] está em beta. Consulte a [Visão geral das Fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores com marca beta.

Uma conexão base representa a conexão autenticada entre uma fonte e o Adobe Experience Platform.

Este tutorial o orienta pelas etapas para criar uma conexão básica para [!DNL HP Vertica] usando a [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../../../home.md): O Experience Platform permite que os dados sejam assimilados de várias fontes, fornecendo a capacidade de estruturar, rotular e aprimorar os dados recebidos usando  [!DNL Platform] serviços.
* [Sandboxes](../../../../../sandboxes/home.md): O Experience Platform fornece sandboxes virtuais que particionam uma única  [!DNL Platform] instância em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito a [!DNL HP Vertica] usando a API [!DNL Flow Service].

### Obter credenciais necessárias

Para que [!DNL Flow Service] se conecte a [!DNL HP Vertica], você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `connectionString` | A string de conexão usada para se conectar à instância [!DNL HP Vertica]. O padrão da string de conexão para [!DNL HP Vertica] é `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}` |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de origem, incluindo especificações de autenticação relacionadas à criação das conexões base e de origem. A ID de especificação de conexão para [!DNL HP Vertica] é: `a8b6a1a4-5735-42b4-952c-85dce0ac38b5` |

Para obter mais informações sobre como adquirir uma string de conexão, consulte [este documento HP Vertica](https://www.vertica.com/docs/9.2.x/HTML/Content/Authoring/ConnectingToVertica/ClientJDBC/CreatingAndConfiguringAConnection.htm).

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da plataforma com êxito, consulte o guia sobre como [começar a usar APIs da plataforma](../../../../../landing/api-guide.md).

## Criar uma conexão base

Uma conexão base retém informações entre a fonte e a Plataforma, incluindo as credenciais de autenticação da fonte, o estado atual da conexão e a ID de conexão base exclusiva. A ID de conexão básica permite explorar e navegar pelos arquivos da fonte e identificar os itens específicos que deseja assimilar, incluindo informações sobre os tipos e formatos de dados.

Para criar uma ID de conexão base, faça uma solicitação de POST ao endpoint `/connections`, fornecendo as credenciais de autenticação [!DNL HP Vertica] como parte dos parâmetros da solicitação.

**Formato da API**

```https
POST /connections
```

**Solicitação**

A solicitação a seguir cria uma conexão base para [!DNL HP Vertica]:


```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Connection for HP Vertica",
        "description": "Connection for HP Vertica",
        "auth": {
            "specName": "Connection String Based Authentication",
            "params": {
                "connectionString": "Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "a8b6a1a4-5735-42b4-952c-85dce0ac38b5",
            "version": "1.0"
        }
    }'
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `auth.params.connectionString` | A cadeia de conexão associada à sua conta [!DNL HP Vertica]. O padrão da string de conexão para [!DNL HP Vertica] é: `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`. |
| `connectionSpec.id` | A ID da especificação de conexão [!DNL HP Vertica]: `a8b6a1a4-5735-42b4-952c-85dce0ac38b5`. |

**Resposta**

Uma resposta bem-sucedida retorna detalhes da conexão recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID é necessária para explorar seus dados no próximo tutorial.

```json
{
    "id": "6bc13a3b-3546-455f-813a-3b3546a55fb1",
    "etag": "\"3500866c-0000-0200-0000-5e83afa30000\""
}
```

## Próximas etapas

Ao seguir este tutorial, você criou uma conexão [!DNL HP Vertica] usando a API [!DNL Flow Service] e obteve o valor de ID exclusivo da conexão. Você pode usar essa ID no próximo tutorial à medida que aprende a [explorar bancos de dados usando a API do Serviço de Fluxo](../../explore/database-nosql.md).
