---
title: Criar uma conexão base PathFactory usando a API do serviço de fluxo
description: Saiba como autenticar sua conta do PathFactory em relação ao Experience Platform usando a API do Serviço de fluxo.
exl-id: 2bdfe38b-d3f7-480f-87c6-0b98b9521be2
source-git-commit: 40c3745920204983f5388de6cba1402d87eda71c
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 2%

---

# Criar uma conexão de base [!DNL PathFactory] usando a API [!DNL Flow Service]

Uma conexão base representa a conexão autenticada entre uma origem e o Adobe Experience Platform.

Leia este documento para saber como criar uma conexão base para [!DNL PathFactory] usando a [[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>).

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Experience Platform:

* [Fontes](../../../../home.md): o Experience Platform permite a assimilação de dados de várias fontes, ao mesmo tempo em que fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços do Experience Platform.
* [Sandboxes](../../../../../sandboxes/home.md): a Experience Platform fornece sandboxes virtuais que particionam uma única instância do Experience Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

### Uso de APIs do Experience Platform

Para obter informações sobre como fazer chamadas para APIs do Experience Platform com êxito, consulte o manual sobre [introdução às APIs do Experience Platform](../../../../../landing/api-guide.md).

A seção a seguir fornece informações adicionais que você precisará saber para se conectar com êxito ao [!DNL PathFactory] usando a API [!DNL Flow Service].

### Colete as credenciais necessárias {#gather-credentials}

Para acessar a conta PathFactory na Experience Platform, você deve fornecer os seguintes valores:

| Credencial | Descrição |
| ---------- | ----------- |
| Nome de usuário | Seu nome de usuário da conta [!DNL PathFactory]. Isso é essencial para identificar sua conta no sistema. |
| Senha | A senha associada à sua conta [!DNL PathFactory]. Verifique se isso está protegido para impedir o acesso não autorizado. |
| Domínio | O domínio associado à sua conta [!DNL PathFactory]. Normalmente, refere-se ao identificador exclusivo na URL [!DNL PathFactory]. |
| Token de acesso | Um token exclusivo usado para autenticação de API para garantir a comunicação segura entre seus sistemas e o [!DNL PathFactory]. |
| Endpoints de API | Endpoints de API específicos para acessar dados: Visitantes, Sessões e Exibições de página. Cada endpoint corresponde a diferentes conjuntos de dados que você pode recuperar. **Observação:** são predefinidos por [!DNL PathFactory] e são específicos para os dados que você pretende acessar: <ul><li>**Ponto de Extremidade dos Visitantes**: `/api/public/v3/data_lake_apis/visitors.json`</li><li>**Ponto de Extremidade de Sessões**: `/api/public/v3/data_lake_apis/sessions.json`</li><li>**Ponto de Extremidade de Exibições de Página**: `/api/public/v3/data_lake_apis/page_views.json`</li></ul> |

Para obter mais informações sobre como proteger e usar suas credenciais e como obter e atualizar seu token de acesso, visite o [[!DNL PathFactory] Centro de Suporte](https://support.pathfactory.com/categories/adobe/). Esse recurso oferece guias abrangentes sobre como gerenciar suas credenciais e garantir uma integração de API eficaz e segura.

## Criar uma conexão básica

Uma conexão base retém informações entre sua origem e a Experience Platform, incluindo as credenciais de autenticação da origem, o estado atual da conexão e a ID de conexão base exclusiva. A ID de conexão básica permite explorar e navegar pelos arquivos de dentro da origem e identificar os itens específicos que deseja assimilar, incluindo informações sobre os tipos de dados e formatos.

Para criar uma ID de conexão base, faça uma solicitação POST para o ponto de extremidade `/connections` ao fornecer suas credenciais de autenticação do [!DNL PathFactory] como parte do corpo da solicitação.

**Formato da API**

```https
POST /connections
```

**Solicitação**

A solicitação a seguir cria uma conexão base para [!DNL PathFactory]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "PathFactory base connection",
      "description": "PathFactory base connection",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "host": "acme-ab12c3d4e5fg6hijk7lmnop8qrst"
              "clientId": "pathfactory",
              "clientSecret": "xxxx"
          }
      },
      "connectionSpec": {
          "id": "ea1c2a08-b722-11eb-8529-0242ac130003",
          "version": "1.0"
      }
  }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `auth.params.clientId` | A ID do cliente associada ao aplicativo [!DNL PathFactory]. |
| `auth.params.clientSecret` | O segredo do cliente associado ao aplicativo [!DNL PathFactory]. |
| `connectionSpec.id` | A ID da especificação de conexão [!DNL PathFactory]: `ea1c2a08-b722-11eb-8529-0242ac130003`. |

**Resposta**

Uma resposta bem-sucedida retorna a conexão recém-criada, incluindo seu identificador de conexão exclusivo (`id`). Essa ID é necessária para explorar seus dados no próximo tutorial.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

## Próximas etapas

Seguindo este tutorial, você criou uma conexão de base [!DNL PathFactory] usando a API [!DNL Flow Service]. Você pode usar essa ID de conexão básica nos seguintes tutoriais:

* [Explore a estrutura e o conteúdo das tabelas de dados usando a API  [!DNL Flow Service] ](../../explore/tabular.md)
* [Crie um fluxo de dados para trazer dados de automação de marketing para o Experience Platform usando a API  [!DNL Flow Service] ](../../collect/marketing-automation.md)
