---
keywords: Experience Platform;página inicial;tópicos populares;Salesforce;salesforce
solution: Experience Platform
title: Criar uma conexão básica do Salesforce usando a API do serviço de fluxo
type: Tutorial
description: Saiba como conectar o Adobe Experience Platform a uma conta do Salesforce usando a API do Serviço de fluxo.
exl-id: 43dd9ee5-4b87-4c8a-ac76-01b83c1226f6
source-git-commit: 27ad8812137502d0a636345852f0cae5d01c7b23
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 4%

---

# Criar um [!DNL Salesforce] conexão básica usando o [!DNL Flow Service] API

Uma conexão base representa a conexão autenticada entre uma origem e o Adobe Experience Platform.

Este tutorial guiará você pelas etapas para criar uma conexão básica para [!DNL Salesforce] usando o [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introdução

Este manual necessita de uma compreensão funcional dos seguintes componentes da Adobe Experience Platform:

* [Origens](../../../../home.md): [!DNL Experience Platform] O permite que os dados sejam assimilados de várias fontes e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando o [!DNL Platform] serviços.
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] O fornece sandboxes virtuais que particionam uma única [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito [!DNL Platform] para um [!DNL Salesforce] conta usando o [!DNL Flow Service] API.

### Coletar credenciais necessárias

A fim de [!DNL Flow Service] para se conectar a [!DNL Salesforce], você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `environmentUrl` | O URL do [!DNL Salesforce] instância de origem. |
| `username` | O nome de usuário para o [!DNL Salesforce] conta de usuário. |
| `password` | A senha para o [!DNL Salesforce] conta de usuário. |
| `securityToken` | O token de segurança para o [!DNL Salesforce] conta de usuário. |
| `apiVersion` | Opcional) A versão da API REST do [!DNL Salesforce] instância que você está usando. O valor da versão da API deve ser formatado com um decimal. Por exemplo, se você estiver usando a versão da API `52`, você deverá inserir o valor como `52.0` Se esse campo ficar em branco, o Experience Platform usará automaticamente a versão mais recente disponível. |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de uma origem, incluindo especificações de autenticação relacionadas à criação das conexões de base e de origem. A ID da especificação de conexão para [!DNL Salesforce] é: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

Para obter mais informações sobre a introdução, visite [este documento do Salesforce](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm).

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da Platform com êxito, consulte o manual em [introdução às APIs da Platform](../../../../../landing/api-guide.md).

## Criar uma conexão básica

Uma conexão base retém informações entre sua origem e a Platform, incluindo as credenciais de autenticação da origem, o estado atual da conexão e sua ID de conexão base exclusiva. A ID de conexão básica permite explorar e navegar pelos arquivos de dentro da origem e identificar os itens específicos que deseja assimilar, incluindo informações sobre os tipos de dados e formatos.

Para criar um ID de conexão base, faça uma solicitação POST ao `/connections` e forneça seu [!DNL Salesforce] credenciais de autenticação no corpo da solicitação.

**Formato da API**

```http
POST /connections
```

**Solicitação**

A solicitação a seguir cria uma conexão básica para [!DNL Salesforce]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Salesforce Connection",
      "description": "Connection for Salesforce account",
      "auth": {
          "specName": "Basic Authentication",
          "params": {****
              "username": "{USERNAME}",
              "password": "{PASSWORD}",
              "securityToken": "{SECURITY_TOKEN}"
          }
      },
      "connectionSpec": {
          "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
          "version": "1.0"
      }
  }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `auth.params.username` | O nome de usuário associado à [!DNL Salesforce] conta. |
| `auth.params.password` | A senha associada ao seu [!DNL Salesforce] conta. |
| `auth.params.securityToken` | O token de segurança associado à [!DNL Salesforce] conta. |
| `connectionSpec.id` | A variável [!DNL Salesforce] ID da especificação de conexão: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

**Resposta**

Uma resposta bem-sucedida retorna a conexão recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID é necessária para explorar seu sistema CRM na próxima etapa.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700df7b-0000-0200-0000-5e3b424f0000\""
}
```

## Próximas etapas

Ao seguir este tutorial, você criou um [!DNL Salesforce] conexão básica usando o [!DNL Flow Service] API. Você pode usar essa ID de conexão básica nos seguintes tutoriais:

* [Explore a estrutura e o conteúdo das tabelas de dados usando o [!DNL Flow Service] API](../../explore/tabular.md)
* [Crie um fluxo de dados para trazer dados do CRM para a Platform usando o [!DNL Flow Service] API](../../collect/crm.md)
