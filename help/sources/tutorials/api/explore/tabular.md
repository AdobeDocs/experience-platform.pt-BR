---
keywords: Experience Platform;página inicial;tópicos populares;fontes;API;explorar;serviço de fluxo
title: Explorar um Source tabular usando a API de serviço de fluxo
description: Este tutorial usa a API de serviço de fluxo para explorar o conteúdo e a estrutura de uma fonte baseada em tabela.
exl-id: 0c7a5b8a-2071-4ac2-b2d1-c5534e7c7d9c
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 6%

---

# Explorar tabelas de dados usando a API [!DNL Flow Service]

Este tutorial fornece etapas sobre como explorar e visualizar a estrutura e o conteúdo de suas tabelas de dados usando a API [[!DNL Flow Service]](https://www.adobe.io/experience-platform-apis/references/flow-service/).

>[!NOTE]
>
> Para explorar suas tabelas de dados, você já deve ter uma ID de conexão de base válida para uma fonte tabular. Se você não tiver essa ID, consulte os seguintes tutoriais para obter etapas sobre como criar uma ID de conexão base para uma origem em tabela: <ul><li>[Advertising](../../../home.md#advertising)</li><li>[CRM](../../../home.md#customer-relationship-management)</li><li>[Sucesso do cliente](../../../home.md#customer-success)</li><li>[Banco de dados](../../../home.md#database)</li><li>[Comércio eletrônico](../../../home.md#ecommerce)</li><li>[Automação de marketing](../../../home.md#marketing-automation)</li><li>[Pagamentos](../../../home.md#payments)</li><li>[Protocolos](../../../home.md#protocols)</li></ul>

## Introdução

Este manual necessita de uma compreensão funcional dos seguintes componentes da Adobe Experience Platform:

* [Fontes](../../../home.md): [!DNL Experience Platform] permite que os dados sejam assimilados de várias fontes e fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços do [!DNL Experience Platform].
* [Sandboxes](../../../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única instância do [!DNL Experience Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

### Uso de APIs do Experience Platform

Para obter informações sobre como fazer chamadas para APIs do Experience Platform com êxito, consulte o manual sobre [introdução às APIs do Experience Platform](../../../../landing/api-guide.md).

## Explore suas tabelas de dados

Você pode recuperar informações sobre a estrutura das tabelas de dados fazendo uma solicitação GET para a API [!DNL Flow Service] enquanto fornece a ID de conexão básica da sua origem.

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

Uma resposta bem-sucedida retorna uma matriz de tabelas da origem. Encontre a tabela que deseja trazer para o Experience Platform e anote sua propriedade `path`, pois é necessário fornecê-la na próxima etapa para inspecionar sua estrutura.

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

## Inspecionar a estrutura de uma tabela

Para inspecionar o conteúdo das tabelas de dados, execute uma solicitação GET para a API [!DNL Flow Service] ao especificar o caminho de uma tabela como um parâmetro de consulta.

**Formato da API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| Parâmetro | Descrição |
| --- | --- |
| `{BASE_CONNECTION_ID}` | A ID de conexão básica da sua origem. |
| `{TABLE_PATH}` | A propriedade de caminho da tabela que você deseja inspecionar. |

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

Uma resposta bem-sucedida retorna informações sobre o conteúdo e a estrutura da tabela especificada. Detalhes sobre cada coluna da tabela estão localizados em elementos da matriz `columns`.

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

Seguindo este tutorial, você coletou informações sobre a estrutura e o conteúdo das tabelas de dados. Além disso, você recuperou o caminho para a tabela que deseja assimilar na Experience Platform. Você pode usar essas informações para criar uma conexão de origem e um fluxo de dados para trazer seus dados para a Experience Platform. Consulte os seguintes tutoriais para obter etapas específicas sobre como criar uma conexão de origem e um fluxo de dados usando a API [!DNL Flow Service]:

* [Fontes do Advertising](../collect/advertising.md)
* [Origens de CRM](../collect/crm.md)
* [Fontes de sucesso do cliente](../collect/customer-success.md)
* [Origens de Banco de Dados](../collect/database-nosql.md)
* [Fontes de comércio eletrônico](../collect/ecommerce.md)
* [Fontes de automação de marketing](../collect/marketing-automation.md)
* [Origens de pagamentos](../collect/payments.md)
* [Origens de protocolos](../collect/protocols.md)
