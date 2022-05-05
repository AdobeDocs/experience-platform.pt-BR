---
keywords: Experience Platform, home, tópicos populares, fontes, API, explorar, serviço de fluxo
title: Explorar uma fonte tabular usando a API do Serviço de fluxo
description: Este tutorial usa a API do Serviço de fluxo para explorar o conteúdo e a estrutura de uma fonte baseada em tabela.
source-git-commit: 1333eac5e022ef32f051120496154a88e2f9324e
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 3%

---

# Explore tabelas de dados usando o [!DNL Flow Service] API

Este tutorial fornece etapas sobre como explorar e visualizar a estrutura e o conteúdo de suas tabelas de dados usando o [[!DNL Flow Service]](https://www.adobe.io/experience-platform-apis/references/flow-service/) API.

>[!NOTE]
>
> Para explorar as tabelas de dados, você já deve ter uma ID de conexão base válida para uma fonte tabular. Caso não tenha essa ID, consulte os seguintes tutoriais para obter as etapas sobre como criar uma ID de conexão básica para uma fonte tabular: <ul><li>[Advertising](../../../home.md#advertising)</li><li>[CRM](../../../home.md#customer-relationship-management)</li><li>[Sucesso do cliente](../../../home.md#customer-success)</li><li>[Banco de dados](../../../home.md#database)</li><li>[Comércio eletrônico](../../../home.md#ecommerce)</li><li>[Automação de marketing](../../../home.md#marketing-automation)</li><li>[Pagamentos](../../../home.md#payments)</li><li>[Protocolos](../../../home.md#protocols)</li></ul>

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../../home.md): [!DNL Experience Platform] permite que os dados sejam assimilados de várias fontes, fornecendo a capacidade de estruturar, rotular e aprimorar os dados recebidos usando [!DNL Platform] serviços.
* [Sandboxes](../../../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da plataforma com êxito, consulte o guia em [introdução às APIs do Platform](../../../../landing/api-guide.md).

## Explorar suas tabelas de dados

Você pode recuperar informações sobre a estrutura das tabelas de dados fazendo uma solicitação do GET para a [!DNL Flow Service] API enquanto fornece a ID de conexão básica da sua fonte.

**Formato da API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| Parâmetro | Descrição |
| --- | --- |
| `{BASE_CONNECTION_ID}` | A ID de conexão básica da sua origem. |

**Solicitação**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/5e73e5a2-dc36-45a8-9f16-93c7a43af318/explore?objectType=root' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma matriz de tabelas da origem. Encontre a tabela que deseja trazer para a Platform e anote sua `path` , conforme você precisará fornecê-la na próxima etapa para inspecionar sua estrutura.

```json
[
    {
        "type": "table",
        "name": "ACME Spring Campaign",
        "path": "acmeSpringCampaign",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "ACME Summer Campaign",
        "path": "acmeSummerCampaign",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

## Inspect a estrutura de uma tabela

Para inspecionar o conteúdo das tabelas de dados, execute uma solicitação GET para [!DNL Flow Service] API ao especificar o caminho de uma tabela como parâmetro de consulta.

**Formato da API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| Parâmetro | Descrição |
| --- | --- |
| `{BASE_CONNECTION_ID}` | A ID de conexão básica da sua origem. |
| `{TABLE_PATH}` | A propriedade path da tabela que você deseja inspecionar. |

**Solicitação**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/5e73e5a2-dc36-45a8-9f16-93c7a43af318/explore?objectType=table&object=acmeSpringCampaign' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna informações sobre o conteúdo e a estrutura da tabela especificada. Os detalhes relativos a cada coluna da tabela estão localizados em elementos do `columns` matriz.

```json
{
  "format": "flat",
  "schema": {
    "columns": [
      {
        "name": "TestID",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "Name",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "Datefield",
        "type": "string",
        "meta:xdmType": "date-time",
        "xdm": {
          "type": "string",
          "format": "date-time"
        }
      },
      {
        "name": "complaint_type",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "complaint_description",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "status",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "status_change_date",
        "type": "string",
        "meta:xdmType": "date-time",
        "xdm": {
          "type": "string",
          "format": "date-time"
        }
      },
      {
        "name": "city",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "Datefield2",
        "type": "string",
        "meta:xdmType": "date-time",
        "xdm": {
          "type": "string",
          "format": "date-time"
        }
      }
    ]
  }
}
```

## Próximas etapas

Ao seguir este tutorial, você coletou informações sobre a estrutura e o conteúdo das tabelas de dados. Além disso, você recuperou o caminho para a tabela que deseja assimilar no Platform. Você pode usar essas informações para criar uma conexão de origem e um fluxo de dados para trazer seus dados para a Platform. Consulte os seguintes tutoriais para obter etapas específicas sobre como criar uma conexão de origem e um fluxo de dados usando o [!DNL Flow Service] API:

* [Fontes de publicidade](../collect/advertising.md)
* [Fontes de CRM](../collect/crm.md)
* [Fontes de sucesso do cliente](../collect/customer-success.md)
* [Fontes de banco de dados](../collect/database-nosql.md)
* [Fontes de comércio eletrônico](../collect/ecommerce.md)
* [Fontes de automação de marketing](../collect/marketing-automation.md)
* [Fontes de pagamentos](../collect/payments.md)
* [Fontes de protocolos](../collect/protocols.md)