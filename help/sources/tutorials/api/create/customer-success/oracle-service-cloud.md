---
keywords: Experience Platform;página inicial;tópicos populares;Nuvem do serviço de Oracle;nuvem do serviço de oracle
title: Criar uma conexão de origem do Oracle Service Cloud usando a API do Flow Service
description: Saiba como conectar o Adobe Experience Platform à Oracle Service Cloud usando a API do Serviço de fluxo.
exl-id: 00c0bc9c-a740-4bab-a882-2cfed8abe758
source-git-commit: 1695b7d638feb648d5cd7af07879f3ed13f938eb
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 2%

---

# Crie uma conexão de origem do Oracle Service Cloud usando o [!DNL Flow Service] API

Uma conexão base representa a conexão autenticada entre uma origem e o Adobe Experience Platform.

Este tutorial percorre as etapas para criar uma conexão básica para a Oracle Service Cloud usando o [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introdução

Este guia requer entendimento prático dos seguintes componentes do Experience Platform:

* [Origens](../../../../home.md): o Experience Platform permite que os dados sejam assimilados de várias fontes e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.
* [Sandboxes](../../../../../sandboxes/home.md): o Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem as informações adicionais que você precisará saber para se conectar com êxito ao Oracle Service Cloud usando o [!DNL Flow Service] API.

### Coletar credenciais necessárias

A fim de [!DNL Flow Service] para se conectar com a Oracle Service Cloud, você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `host` | O URL do host da instância da Nuvem do Oracle Service. |
| `username` | O nome de usuário da sua conta de usuário da Oracle Service Cloud. |
| `password` | A senha da sua conta da Oracle Service Cloud. |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de uma origem, incluindo especificações de autenticação relacionadas à criação das conexões de base e de origem. A ID de especificação de conexão da Oracle Service Cloud é: `ba5126ec-c9ac-11eb-b8bc-0242ac130003`. |

Para obter mais informações sobre como autenticar sua conta da Oracle Service Cloud, consulte o [[!DNL Oracle] guia sobre autenticação](https://docs.oracle.com/en/cloud/saas/b2c-service/20c/cxska/OKCS_Authenticate_and_Authorize.html).

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da Platform com êxito, consulte o manual em [introdução às APIs da Platform](../../../../../landing/api-guide.md).

## Criar uma conexão básica

Uma conexão base retém informações entre sua origem e a Platform, incluindo as credenciais de autenticação da origem, o estado atual da conexão e sua ID de conexão base exclusiva. A ID de conexão básica permite explorar e navegar pelos arquivos de dentro da origem e identificar os itens específicos que deseja assimilar, incluindo informações sobre os tipos de dados e formatos.

Para criar um ID de conexão base, faça uma solicitação POST ao `/connections` ao fornecer suas credenciais de autenticação da Oracle Service Cloud como parte dos parâmetros de solicitação.

**Formato da API**

```http
POST /connections
```

**Solicitação**

A solicitação a seguir cria uma conexão básica para o Oracle Service Cloud:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Base connection for Oracle Service Cloud",
      "description": "Base connection for Oracle Service Cloud",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "host": "{HOST}",
              "username": "{USERNAME}",
              "password": "{PASSWORD}"
          }
      },
      "connectionSpec": {
          "id": "ba5126ec-c9ac-11eb-b8bc-0242ac130003",
          "version": "1.0"
      }
  }'
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `auth.params.host` | O URL do host da instância da Nuvem do Oracle Service. |
| `auth.params.username` | O nome de usuário associado à sua conta da Oracle Service Cloud. |
| `auth.params.password` | A senha associada à sua conta da Oracle Service Cloud. |
| `connectionSpec.id` | A ID de especificação da conexão do Oracle Service Cloud: `ba5126ec-c9ac-11eb-b8bc-0242ac130003` |

**Resposta**

Uma resposta bem-sucedida retorna a conexão recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID é necessária para explorar seu sistema CRM na próxima etapa.

```json
{
    "id": "4267c2ab-2104-474f-a7c2-ab2104d74f86",
    "etag": "\"0200f1c5-0000-0200-0000-5e4352bf0000\""
}
```

## Próximas etapas

Seguindo este tutorial, você criou uma conexão básica do Oracle Service Cloud usando o [!DNL Flow Service] API. Você pode usar essa ID de conexão básica nos seguintes tutoriais:

* [Explore a estrutura e o conteúdo das tabelas de dados usando o [!DNL Flow Service] API](../../explore/tabular.md)
* [Crie um fluxo de dados para trazer os dados de sucesso do cliente para a Platform usando o [!DNL Flow Service] API](../../collect/customer-success.md)
