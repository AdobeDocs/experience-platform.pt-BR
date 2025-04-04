---
keywords: Experience Platform;home;popular tópicos;oracle;
title: (Beta) Criar uma conexão básica do Oracle Responsys usando a API do serviço de fluxo
description: Saiba como conectar o Adobe Experience Platform ao Oracle Responsys usando a API do serviço de fluxo.
hide: true
hidefromtoc: true
exl-id: 76659f5a-c923-488c-88f6-1919bc6a7bb5
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 2%

---

# (Beta) Crie uma conexão de base [!DNL Oracle Responsys] usando a API [!DNL Flow Service]

>[!NOTE]
>
>A origem [!DNL Oracle Responsys] está na versão beta. Consulte a [Visão geral das fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores rotulados com beta.

Uma conexão base representa a conexão autenticada entre uma origem e o Adobe Experience Platform.

Este tutorial guiará você pelas etapas para criar uma conexão básica para [!DNL Oracle Responsys] usando a [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Experience Platform:

* [Fontes](../../../../home.md): o Experience Platform permite a assimilação de dados de várias fontes, ao mesmo tempo em que fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços do [!DNL Experience Platform].
* [Sandboxes](../../../../../sandboxes/home.md): a Experience Platform fornece sandboxes virtuais que particionam uma única instância do [!DNL Experience Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem as informações adicionais que você precisa saber para se conectar com êxito ao [!DNL Oracle Responsys] usando a API [!DNL Flow Service].

### Coletar credenciais necessárias

Para que [!DNL Flow Service] se conecte a [!DNL Oracle Responsys], você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| --- | --- |
| `endpoint` | A URL do ponto de extremidade de autenticação REST da instância [!DNL Oracle Responsys]. |
| `clientId` | A ID do cliente da sua instância [!DNL Oracle Responsys]. |
| `clientSecret` | O segredo do cliente da sua instância [!DNL Oracle Responsys]. |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de uma origem, incluindo especificações de autenticação relacionadas à criação das conexões de base e de origem. O valor da ID da especificação de conexão da origem [!DNL Oracle Responsys] foi corrigido como: `ff4274f2-c9a9-11eb-b8bc-0242ac130003`. |

Para obter mais informações sobre credenciais de autenticação para [!DNL Oracle Responsys], consulte o [[!DNL Oracle Responsys] guia sobre autenticação](https://docs.oracle.com/en/cloud/saas/marketing/responsys-develop/API/GetStarted/authentication.htm).

### Uso de APIs do Experience Platform

Para obter informações sobre como fazer chamadas para APIs do Experience Platform com êxito, consulte o manual sobre [introdução às APIs do Experience Platform](../../../../../landing/api-guide.md).

## Criar uma conexão básica

Uma conexão base retém informações entre sua origem e a Experience Platform, incluindo as credenciais de autenticação da origem, o estado atual da conexão e a ID de conexão base exclusiva. A ID de conexão básica permite explorar e navegar pelos arquivos de dentro da origem e identificar os itens específicos que deseja assimilar, incluindo informações sobre os tipos de dados e formatos.

Para criar uma ID de conexão base, faça uma solicitação POST para o ponto de extremidade `/connections` ao fornecer suas credenciais de autenticação [!DNL Oracle Responsys] como parte dos parâmetros de solicitação.

**Formato da API**

```https
POST /connections
```

**Solicitação**

A solicitação a seguir cria uma conexão base para [!DNL Oracle Responsys]:

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
| `name` | O nome da sua conexão base [!DNL Oracle Responsys]. É recomendável fornecer um nome descritivo, pois você pode usar esse valor para pesquisar sua conexão básica. |
| `description` | (Opcional) Uma propriedade que você pode incluir para fornecer informações suplementares sobre sua conexão básica. |
| `auth.specName` | O tipo de autenticação usado para a conexão. |
| `auth.params.endpoint` | A URL do ponto de extremidade de autenticação REST do servidor [!DNL Oracle Responsys]. |
| `auth.params.clientId` | A ID do cliente da sua instância [!DNL Oracle Responsys]. |
| `auth.params.clientSecret` | O segredo do cliente da sua instância [!DNL Oracle Responsys]. |
| `connectionSpec.id` | O valor da ID da especificação de conexão da origem [!DNL Oracle Responsys] foi corrigido como: `ff4274f2-c9a9-11eb-b8bc-0242ac130003`. |

**Resposta**

Uma resposta bem-sucedida retorna detalhes da conexão base recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID é necessária na próxima etapa para criar uma conexão de origem.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Próximas etapas

Seguindo este tutorial, você criou uma conexão de base [!DNL Oracle Responsys] usando a API [!DNL Flow Service]. Você pode usar essa ID de conexão básica nos seguintes tutoriais:

* [Explore a estrutura e o conteúdo das tabelas de dados usando a API  [!DNL Flow Service] ](../../explore/tabular.md)
* [Crie um fluxo de dados para trazer dados de automação de marketing para o Experience Platform usando a API  [!DNL Flow Service] ](../../collect/marketing-automation.md)
