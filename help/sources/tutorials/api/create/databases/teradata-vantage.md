---
keywords: Experience Platform;página inicial;tópicos populares;Teradata Vantage
title: Criar uma conexão do Teradata Vantage Base usando a API do Serviço de fluxo
description: Saiba como conectar o Adobe Experience Platform ao Teradata Vantage usando a API do Serviço de fluxo.
exl-id: 88707dca-3c7a-43c7-9d71-473ad9715fc6
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 5%

---

# Criar uma conexão de base [!DNL Teradata Vantage] usando a API [!DNL Flow Service]

Uma conexão base representa a conexão autenticada entre uma origem e o Adobe Experience Platform.

Este tutorial guiará você pelas etapas para criar uma conexão básica para [!DNL Teradata Vantage] usando a [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introdução

Este manual necessita de uma compreensão funcional dos seguintes componentes da Adobe Experience Platform:

* [Fontes](../../../../home.md): [!DNL Experience Platform] permite que os dados sejam assimilados de várias fontes e fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços do [!DNL Experience Platform].
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única instância do [!DNL Experience Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

### Uso de APIs do Experience Platform

Para obter informações sobre como fazer chamadas para APIs do Experience Platform com êxito, consulte o manual sobre [introdução às APIs do Experience Platform](../../../../../landing/api-guide.md).

A seção a seguir fornece informações adicionais que você precisará saber para se conectar com êxito ao [!DNL Teradata Vantage] usando a API [!DNL Flow Service].

### Coletar credenciais necessárias

Para que [!DNL Flow Service] se conecte a [!DNL Teradata Vantage], você deve fornecer as seguintes propriedades de conexão:

| Credencial | Descrição |
| --- | --- |
| `connectionString` | Uma cadeia de conexão é uma cadeia que fornece informações sobre uma fonte de dados e como você pode se conectar a ela. O padrão da cadeia de conexão para [!DNL Teradata Vantage] é `DBCName={SERVER};Uid={USERNAME};Pwd={PASSWORD}`. |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de uma origem, incluindo especificações de autenticação relacionadas à criação das conexões de base e de origem. A ID da especificação de conexão para [!DNL Teradata Vantage] é: `2fa8af9c-2d1a-43ea-a253-f00a00c74412` |

Para obter mais informações sobre a introdução, consulte este [[!DNL Teradata Vantage] documento](https://docs.teradata.com/r/Teradata-VantageTM-Advanced-SQL-Engine-Security-Administration/July-2021/Setting-Up-the-Administrative-Infrastructure/Controlling-Access-to-the-Operating-System/Working-with-OS-Level-Security-Options).

## Criar uma conexão básica

Uma conexão base retém informações entre sua origem e a Experience Platform, incluindo as credenciais de autenticação da origem, o estado atual da conexão e a ID de conexão base exclusiva. A ID de conexão básica permite explorar e navegar pelos arquivos de dentro da origem e identificar os itens específicos que deseja assimilar, incluindo informações sobre os tipos de dados e formatos.

Para criar uma ID de conexão base, faça uma solicitação POST para o ponto de extremidade `/connections` ao fornecer suas credenciais de autenticação do [!DNL Teradata Vantage] como parte do corpo da solicitação.

**Formato da API**

```https
POST /connections
```

**Solicitação**

A solicitação a seguir cria uma conexão base para [!DNL Teradata Vantage]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Teradata Vantage base connection",
      "description": "Teradata Vantage base connection",
      "auth": {
          "specName": "ConnectionString,
          "params": {
              "connectionString": "DBCName={SERVER};Uid={USERNAME};Pwd={PASSWORD}"
          }
      },
      "connectionSpec": {
          "id": "2fa8af9c-2d1a-43ea-a253-f00a00c74412",
          "version": "1.0"
      }
  }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `auth.params.connectionString` | A cadeia de conexão usada para se conectar à sua instância do [!DNL Teradata Vantage]. O padrão da cadeia de conexão para [!DNL Teradata Vantage] é `DBCName={SERVER};Uid={USERNAME};Pwd={PASSWORD}`. |
| `connectionSpec.id` | A ID da especificação de conexão [!DNL Teradata Vantage]: `2fa8af9c-2d1a-43ea-a253-f00a00c74412`. |

**Resposta**

Uma resposta bem-sucedida retorna a conexão recém-criada, incluindo seu identificador de conexão exclusivo (`id`). Essa ID é necessária para explorar seus dados no próximo tutorial.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

Seguindo este tutorial, você criou uma conexão de base [!DNL Teradata Vantage] usando a API [!DNL Flow Service]. Você pode usar essa ID de conexão básica nos seguintes tutoriais:

* [Explore a estrutura e o conteúdo das tabelas de dados usando a API  [!DNL Flow Service] &#x200B;](../../explore/tabular.md)
* [Crie um fluxo de dados para trazer dados do banco de dados para a Experience Platform usando a API  [!DNL Flow Service] &#x200B;](../../collect/database-nosql.md)
