---
title: Criar uma conexão de base do Oracle Eloqua usando a API do serviço de fluxo
description: Saiba como conectar o Adobe Experience Platform ao Oracle Eloqua usando a API de serviço de fluxo.
exl-id: 866e408f-6e0b-4e81-9ad8-9d74c485c89a
source-git-commit: 7ff0709b62590bb80c1ed664368f28cdc4a950ea
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 1%

---

# Criar uma conexão de base [!DNL Oracle Eloqua] usando a API [!DNL Flow Service]

>[!WARNING]
>
>A origem [!DNL Oracle Eloqua] será substituída em janeiro de 2026. Uma nova fonte será lançada ainda este ano como alternativa. Depois que a nova origem for lançada, você deverá planejar migrar para a nova origem criando novas conexões de conta e fluxos de dados antes do final de janeiro de 2026.

Uma conexão base representa a conexão autenticada entre uma origem e o Adobe Experience Platform.

Este tutorial guiará você pelas etapas para criar uma conexão básica para [!DNL Oracle Eloqua] usando a [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Experience Platform:

* [Fontes](../../../../home.md): o Experience Platform permite a assimilação de dados de várias fontes, ao mesmo tempo em que fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços do [!DNL Experience Platform].
* [Sandboxes](../../../../../sandboxes/home.md): a Experience Platform fornece sandboxes virtuais que particionam uma única instância do [!DNL Experience Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem as informações adicionais que você precisa saber para se conectar com êxito ao [!DNL Oracle Eloqua] usando a API [!DNL Flow Service].

### Coletar credenciais necessárias

Para que [!DNL Flow Service] se conecte a [!DNL Oracle Eloqua], você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| --- | --- |
| `endpoint` | O ponto de extremidade de seu [!DNL Oracle Eloqua]. |
| `username` | O nome de usuário da sua conta [!DNL Oracle Eloqua]. O nome de usuário deve ser formatado como `siteName + \\ + username`, onde `siteName` é o nome da empresa que você usou para fazer logon em [!DNL Oracle Eloqua] e `username` é seu nome de usuário. Por exemplo, seu nome de usuário de logon pode ser: `adobe\\emily`. |
| `password` | A senha correspondente ao seu nome de usuário [!DNL Oracle Eloqua]. |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de uma origem, incluindo especificações de autenticação relacionadas à criação das conexões de base e de origem. O valor da ID da especificação de conexão da origem [!DNL Oracle Eloqua] foi corrigido como: `35d6c4d8-c9a9-11eb-b8bc-0242ac130003`. |

Para obter mais informações sobre credenciais de autenticação para [!DNL Oracle Eloqua], consulte o [[!DNL Oracle Eloqua] guia sobre autenticação](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html).

### Uso de APIs do Experience Platform

Para obter informações sobre como fazer chamadas para APIs do Experience Platform com êxito, consulte o manual sobre [introdução às APIs do Experience Platform](../../../../../landing/api-guide.md).

## Criar uma conexão básica

Uma conexão base retém informações entre sua origem e a Experience Platform, incluindo as credenciais de autenticação da origem, o estado atual da conexão e a ID de conexão base exclusiva. A ID de conexão básica permite explorar e navegar pelos arquivos de dentro da origem e identificar os itens específicos que deseja assimilar, incluindo informações sobre os tipos de dados e formatos.

Para criar uma ID de conexão base, faça uma solicitação POST para o ponto de extremidade `/connections` ao fornecer suas credenciais de autenticação [!DNL Oracle Eloqua] como parte dos parâmetros de solicitação.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `name` | O nome da sua conexão base [!DNL Oracle Eloqua]. É recomendável fornecer um nome descritivo, pois você pode usar esse valor para pesquisar sua conexão básica. |
| `description` | (Opcional) Uma propriedade que você pode incluir para fornecer informações suplementares sobre sua conexão básica. |
| `auth.specName` | O tipo de autenticação usado para a conexão. |
| `auth.params.endpoint` | O ponto de extremidade do servidor [!DNL Oracle Eloqua]. |
| `auth.params.username` | A credencial concatenada que inclui o nome do site e o nome de usuário que corresponde à sua conta do [!DNL Oracle Eloqua]. |
| `auth.params.password` | A senha que corresponde à sua conta do [!DNL Oracle Eloqua]. |
| `connectionSpec.id` | O valor da ID da especificação de conexão da origem [!DNL Oracle Eloqua] foi corrigido como: `35d6c4d8-c9a9-11eb-b8bc-0242ac130003`. |

**Resposta**

Uma resposta bem-sucedida retorna detalhes da conexão base recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID é necessária na próxima etapa para criar uma conexão de origem.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Próximas etapas

Seguindo este tutorial, você criou uma conexão de base [!DNL Oracle Eloqua] usando a API [!DNL Flow Service]. Você pode usar essa ID de conexão básica nos seguintes tutoriais:

* [Explore a estrutura e o conteúdo das tabelas de dados usando a API  [!DNL Flow Service] &#x200B;](../../explore/tabular.md)
* [Crie um fluxo de dados para trazer dados de automação de marketing para o Experience Platform usando a API  [!DNL Flow Service] &#x200B;](../../collect/marketing-automation.md)
