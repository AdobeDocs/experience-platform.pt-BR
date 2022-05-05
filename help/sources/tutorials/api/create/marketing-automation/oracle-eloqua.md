---
keywords: Experience Platform, home, tópicos populares, oracle, eloqua, oracle eloqua
solution: Experience Platform
title: Criar uma conexão básica do Oracle Eloqua usando a API do Serviço de fluxo
topic-legacy: overview
type: Tutorial
description: Saiba como conectar o Adobe Experience Platform ao Oracle Eloqua usando a API de Serviço de Fluxo.
exl-id: 866e408f-6e0b-4e81-9ad8-9d74c485c89a
source-git-commit: 1f2ae53e5503618b7ac12628923b30c457fd17e2
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 1%

---

# Crie um [!DNL Oracle Eloqua] conexão básica usando o [!DNL Flow Service] API

Uma conexão base representa a conexão autenticada entre uma fonte e o Adobe Experience Platform.

Este tutorial o orienta pelas etapas para criar uma conexão básica para [!DNL Oracle Eloqua] usando o [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes da Platform:

* [Fontes](../../../../home.md): A Platform permite que os dados sejam assimilados de várias fontes, além de fornecer a você a capacidade de estruturar, rotular e aprimorar os dados recebidos usando [!DNL Platform] serviços.
* [Sandboxes](../../../../../sandboxes/home.md): A plataforma fornece sandboxes virtuais que particionam uma única [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisa saber para se conectar com êxito ao [!DNL Oracle Eloqua] usando o [!DNL Flow Service] API.

### Obter credenciais necessárias

Para [!DNL Flow Service] para conectar-se com [!DNL Oracle Eloqua], você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| --- | --- |
| `endpoint` | O terminal de sua [!DNL Oracle Eloqua]. |
| `username` | O nome de usuário de seu [!DNL Oracle Eloqua] conta. O nome de usuário deve ser formatado como `siteName + \\ + username`, onde `siteName` é o nome da empresa na qual você usou para fazer logon [!DNL Oracle Eloqua] e `username` é seu nome de usuário. Por exemplo, seu nome de usuário de logon pode ser: `adobe\\emily`. |
| `password` | A senha correspondente ao seu [!DNL Oracle Eloqua] nome de usuário. |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de origem, incluindo especificações de autenticação relacionadas à criação das conexões base e de origem. O valor da ID da especificação de conexão do [!DNL Oracle Eloqua] A origem é fixa como: `35d6c4d8-c9a9-11eb-b8bc-0242ac130003`. |

Para obter mais informações sobre credenciais de autenticação para [!DNL Oracle Eloqua], consulte o [[!DNL Oracle Eloqua] guia de autenticação](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html).

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da plataforma com êxito, consulte o guia em [introdução às APIs do Platform](../../../../../landing/api-guide.md).

## Criar uma conexão base

Uma conexão base retém informações entre a fonte e a Plataforma, incluindo as credenciais de autenticação da fonte, o estado atual da conexão e a ID de conexão base exclusiva. A ID de conexão básica permite explorar e navegar pelos arquivos da fonte e identificar os itens específicos que deseja assimilar, incluindo informações sobre os tipos e formatos de dados.

Para criar uma ID de conexão base, faça uma solicitação de POST para a variável `/connections` endpoint enquanto fornece seu [!DNL Oracle Eloqua] credenciais de autenticação como parte dos parâmetros da solicitação.

**Formato da API**

```https
POST /connections
```

**Solicitação**

A solicitação a seguir cria uma conexão base para [!DNL Oracle Eloqua]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json'
  -d '{
      "name": "Oracle Eloqua Base Connection",
      "description": "Base Connection for Oracle Eloqua",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "endpoint": "{ENDPOINT}",
              "username": "{USERNAME}",
              "password": "{PASSWORD}"
          }
      },
      "connectionSpec": {
          "id": "35d6c4d8-c9a9-11eb-b8bc-0242ac130003",
          "version": "1.0"
      }
  }'
```

| Parâmetro | Descrição |
| --- | --- |
| `name` | O nome da sua [!DNL Oracle Eloqua] conexão básica. É recomendável fornecer um nome descritivo, pois você pode usar esse valor para buscar sua conexão básica. |
| `description` | (Opcional) Uma propriedade que pode ser incluída para fornecer informações suplementares sobre a conexão básica. |
| `auth.specName` | O tipo de autenticação usado para a conexão. |
| `auth.params.endpoint` | O terminal de sua [!DNL Oracle Eloqua] servidor. |
| `auth.params.username` | A credencial concatenada que inclui o nome do site e o nome de usuário que corresponde a seu [!DNL Oracle Eloqua] conta. |
| `auth.params.password` | A senha que corresponde ao seu [!DNL Oracle Eloqua] conta. |
| `connectionSpec.id` | O valor da ID da especificação de conexão do [!DNL Oracle Eloqua] A origem é fixa como: `35d6c4d8-c9a9-11eb-b8bc-0242ac130003`. |

**Resposta**

Uma resposta bem-sucedida retorna detalhes da conexão base recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID é necessária na próxima etapa para criar uma conexão de origem.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Próximas etapas

Ao seguir este tutorial, você criou um [!DNL Oracle Eloqua] conexão básica usando o [!DNL Flow Service] API. Você pode usar essa ID de conexão básica nos seguintes tutoriais:

* [Explore a estrutura e o conteúdo das tabelas de dados usando o [!DNL Flow Service] API](../../explore/tabular.md)
* [Crie um fluxo de dados para trazer dados de automação de marketing para a Platform usando o [!DNL Flow Service] API](../../collect/marketing-automation.md)
