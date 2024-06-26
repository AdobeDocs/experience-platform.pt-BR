---
keywords: Experience Platform;página inicial;tópicos populares;oracle;
title: (Beta) Criar uma conexão básica do Responsys do Oracle usando a API do serviço de fluxo
description: Saiba como conectar o Adobe Experience Platform ao Oracle Responsys usando a API do serviço de fluxo.
hide: true
hidefromtoc: true
exl-id: 76659f5a-c923-488c-88f6-1919bc6a7bb5
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 4%

---

# (Beta) Criar um [!DNL Oracle Responsys] conexão básica usando o [!DNL Flow Service] API

>[!NOTE]
>
>A variável [!DNL Oracle Responsys] a fonte está na versão beta. Consulte a [Visão geral das fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores rotulados com beta.

Uma conexão base representa a conexão autenticada entre uma origem e o Adobe Experience Platform.

Este tutorial guiará você pelas etapas para criar uma conexão básica para [!DNL Oracle Responsys] usando o [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introdução

Este manual necessita de uma compreensão funcional dos seguintes componentes da Platform:

* [Origens](../../../../home.md): a Platform permite que os dados sejam assimilados de várias fontes e fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando o [!DNL Platform] serviços.
* [Sandboxes](../../../../../sandboxes/home.md): a Platform fornece sandboxes virtuais que particionam um único [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem as informações adicionais que você precisa saber para se conectar com êxito ao [!DNL Oracle Responsys] usando o [!DNL Flow Service] API.

### Coletar credenciais necessárias

A fim de [!DNL Flow Service] para se conectar com [!DNL Oracle Responsys], você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| --- | --- |
| `endpoint` | O URL do ponto de extremidade de autenticação REST de seu [!DNL Oracle Responsys] instância. |
| `clientId` | A ID do cliente do [!DNL Oracle Responsys] instância. |
| `clientSecret` | O segredo do cliente do seu [!DNL Oracle Responsys] instância. |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de uma origem, incluindo especificações de autenticação relacionadas à criação das conexões de base e de origem. O valor da ID da especificação de conexão do [!DNL Oracle Responsys] a origem é fixa como: `ff4274f2-c9a9-11eb-b8bc-0242ac130003`. |

Para obter mais informações sobre credenciais de autenticação para [!DNL Oracle Responsys], consulte o [[!DNL Oracle Responsys] guia sobre autenticação](https://docs.oracle.com/en/cloud/saas/marketing/responsys-develop/API/GetStarted/authentication.htm).

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da Platform com êxito, consulte o manual em [introdução às APIs da Platform](../../../../../landing/api-guide.md).

## Crie uma conexão básica

Uma conexão base retém informações entre sua origem e a Platform, incluindo as credenciais de autenticação da origem, o estado atual da conexão e sua ID de conexão base exclusiva. A ID de conexão básica permite explorar e navegar pelos arquivos de dentro da origem e identificar os itens específicos que deseja assimilar, incluindo informações sobre os tipos de dados e formatos.

Para criar um ID de conexão base, faça uma solicitação POST ao `/connections` ao fornecer sua [!DNL Oracle Responsys] credenciais de autenticação como parte dos parâmetros de solicitação.

**Formato da API**

```https
POST /connections
```

**Solicitação**

A solicitação a seguir cria uma conexão básica para [!DNL Oracle Responsys]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json'
  -d '{
      "name": "Oracle Responsys Base Connection",
      "description": "Base Connection for Oracle Responsys",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "endpoint": "{ENDPOINT}",
              "clientId": "{CLIENT_ID}",
              "clientSecret": "{CLIENT_SECRET}"
          }
      },
      "connectionSpec": {
          "id": "ff4274f2-c9a9-11eb-b8bc-0242ac130003",
          "version": "1.0"
      }
  }'
```

| Parâmetro | Descrição |
| --- | --- |
| `name` | O nome do seu [!DNL Oracle Responsys] conexão básica. É recomendável fornecer um nome descritivo, pois você pode usar esse valor para pesquisar sua conexão básica. |
| `description` | (Opcional) Uma propriedade que você pode incluir para fornecer informações suplementares sobre sua conexão básica. |
| `auth.specName` | O tipo de autenticação usado para a conexão. |
| `auth.params.endpoint` | O URL do ponto de extremidade de autenticação REST de seu [!DNL Oracle Responsys] servidor. |
| `auth.params.clientId` | A ID do cliente do [!DNL Oracle Responsys] instância. |
| `auth.params.clientSecret` | O segredo do cliente do seu [!DNL Oracle Responsys] instância. |
| `connectionSpec.id` | O valor da ID da especificação de conexão do [!DNL Oracle Responsys] a origem é fixa como: `ff4274f2-c9a9-11eb-b8bc-0242ac130003`. |

**Resposta**

Uma resposta bem-sucedida retorna detalhes da conexão base recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID é necessária na próxima etapa para criar uma conexão de origem.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Próximas etapas

Ao seguir este tutorial, você criou um [!DNL Oracle Responsys] conexão básica usando o [!DNL Flow Service] API. Você pode usar essa ID de conexão básica nos seguintes tutoriais:

* [Explore a estrutura e o conteúdo das tabelas de dados usando o [!DNL Flow Service] API](../../explore/tabular.md)
* [Crie um fluxo de dados para trazer dados de automação de marketing para a Platform usando o [!DNL Flow Service] API](../../collect/marketing-automation.md)
