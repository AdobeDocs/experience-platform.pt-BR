---
title: Criar uma conexão básica do Amazon Redshift usando a API do serviço de fluxo
description: Saiba como conectar o Adobe Experience Platform ao Amazon Redshift usando a API do Serviço de fluxo.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 2728ce08-05c9-4dca-af1d-d2d1b266c5d9
source-git-commit: a7c2c5e4add5c80e0622d5aeb766cec950d79dbb
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 5%

---

# Criar um [!DNL Amazon Redshift] conexão básica usando o [!DNL Flow Service] API

>[!IMPORTANT]
>
>A variável [!DNL Amazon Redshift] origem está disponível no catálogo de origens para usuários que compraram o Real-time Customer Data Platform Ultimate.

Uma conexão base representa a conexão autenticada entre uma origem e o Adobe Experience Platform.

Este tutorial guiará você pelas etapas para criar uma conexão básica para [!DNL Amazon Redshift] usando o [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introdução

Este manual necessita de uma compreensão funcional dos seguintes componentes da Adobe Experience Platform:

* [Origens](../../../../home.md): [!DNL Experience Platform] O permite que os dados sejam assimilados de várias fontes e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando o [!DNL Platform] serviços.
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] O fornece sandboxes virtuais que particionam uma única [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito ao [!DNL Amazon Redshift] usando o [!DNL Flow Service] API.

### Coletar credenciais necessárias

A fim de [!DNL Flow Service] para se conectar com [!DNL Amazon Redshift], você deve fornecer as seguintes propriedades de conexão:

| **Credencial** | **Descrição** |
| -------------- | --------------- |
| `server` | O servidor associado ao seu [!DNL Amazon Redshift] conta. |
| `port` | A porta TCP que um [!DNL Amazon Redshift] O servidor usa o para detectar conexões de clientes. |
| `username` | O nome de usuário associado à [!DNL Amazon Redshift] conta. |
| `password` | A senha associada ao seu [!DNL Amazon Redshift] conta. |
| `database` | A variável [!DNL Amazon Redshift] banco de dados que você está acessando. |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de uma origem, incluindo especificações de autenticação relacionadas à criação das conexões de base e de origem. A ID da especificação de conexão para [!DNL Amazon Redshift] é `3416976c-a9ca-4bba-901a-1f08f66978ff`. |

Para obter mais informações sobre a introdução, consulte esta [[!DNL Amazon Redshift] documento](https://docs.aws.amazon.com/redshift/latest/gsg/getting-started.html).

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da Platform com êxito, consulte o manual em [introdução às APIs da Platform](../../../../../landing/api-guide.md).

## Crie uma conexão básica

>[!NOTE]
>
>O padrão de codificação para [!DNL Redshift] é Unicode. Isso não pode ser alterado.

Uma conexão base retém informações entre sua origem e a Platform, incluindo as credenciais de autenticação da origem, o estado atual da conexão e sua ID de conexão base exclusiva. A ID de conexão básica permite explorar e navegar pelos arquivos de dentro da origem e identificar os itens específicos que deseja assimilar, incluindo informações sobre os tipos de dados e formatos.

Para criar um ID de conexão base, faça uma solicitação POST ao `/connections` ao fornecer sua [!DNL Amazon Redshift] credenciais de autenticação como parte dos parâmetros de solicitação.

**Formato da API**

```https
POST /connections
```

**Solicitação**

A solicitação a seguir cria uma conexão básica para [!DNL Amazon Redshift]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "amazon-redshift base connection",
      "description": "base connection for amazon-redshift,
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "{SERVER}",
              "port": "{PORT},
              "username": "{USERNAME}",
              "password": "{PASSWORD}",
              "database": "{DATABASE}"
          }
      },
      "connectionSpec": {
          "id": "3416976c-a9ca-4bba-901a-1f08f66978ff",
          "version": "1.0"
      }
  }'
```

| Propriedade | Descrição |
| ------------- | --------------- |
| `auth.params.server` | Seu [!DNL Amazon Redshift] servidor. |
| `auth.params.port` | A porta TCP que o [!DNL Amazon Redshift] O servidor usa o para detectar conexões de clientes. |
| `auth.params.database` | O banco de dados associado à [!DNL Amazon Redshift] conta. |
| `auth.params.password` | A senha associada ao seu [!DNL Amazon Redshift] conta. |
| `auth.params.username` | O nome de usuário associado à [!DNL Amazon Redshift] conta. |
| `connectionSpec.id` | A variável [!DNL Amazon Redshift] ID da especificação de conexão: `3416976c-a9ca-4bba-901a-1f08f66978ff` |

**Resposta**

Uma resposta bem-sucedida retorna a conexão recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID é necessária para explorar seus dados no próximo tutorial.

```json
{
    "id": "373e88fc-43da-4e3c-be88-fc43da3e3c0f",
    "etag": "\"1700ce7b-0000-0200-0000-5e3b405e0000\""
}
```

## Próximas etapas

Ao seguir este tutorial, você criou um [!DNL Amazon Redshift] conexão básica usando o [!DNL Flow Service] API. Você pode usar essa ID de conexão básica nos seguintes tutoriais:

* [Explore a estrutura e o conteúdo das tabelas de dados usando o [!DNL Flow Service] API](../../explore/tabular.md)
* [Crie um fluxo de dados para trazer dados do banco de dados para a Platform usando o [!DNL Flow Service] API](../../collect/database-nosql.md)
