---
title: Criar uma conexão de base Phoenix usando a API do serviço de fluxo
description: Saiba como conectar um banco de dados Phoenix ao Adobe Experience Platform usando a API do serviço de fluxo.
exl-id: b69d9593-06fe-4fff-88a9-7860e4e45eb7
source-git-commit: efffd6ce1ed541ce20ee6500e42165465f2fa6a0
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 2%

---

# Criar um [!DNL Phoenix] conexão básica usando o [!DNL Flow Service] API

Uma conexão base representa a conexão autenticada entre uma origem e o Adobe Experience Platform.

Este tutorial fornece etapas sobre como criar uma conexão base e conectar seu [!DNL Phoenix] para a Adobe Experience Platform usando a variável [!DNL Flow Service] API.

## Introdução

Este guia requer entendimento prático dos seguintes componentes do Experience Platform:

* [Origens](../../../../home.md): o Experience Platform permite que os dados sejam assimilados de várias fontes e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços Experience Platform.
* [Sandboxes](../../../../../sandboxes/home.md): o Experience Platform fornece sandboxes virtuais que particionam uma única instância de Experience Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito ao [!DNL Phoenix] usando o [!DNL Flow Service] API.

### Coletar credenciais necessárias

Você deve fornecer as credenciais de autenticação a seguir para se conectar ao [!DNL Phoenix] conta para Experience Platform.

| Credencial | Descrição |
| ---------- | ----------- |
| `host` | O endereço IP ou o nome de host do [!DNL Phoenix] servidor. |
| `username` | O nome de usuário que você usa para acessar [!DNL Phoenix] Servidor. |
| `password` | A senha correspondente ao usuário. |
| `port` | A porta TCP que o [!DNL Phoenix] O servidor usa o para detectar conexões de clientes. Se você estiver se conectando ao [!DNL Azure HDInsights]e especifique a porta como 443. Se esse parâmetro não for fornecido, o valor padrão será 8765. |
| `httpPath` | O URL parcial correspondente à variável [!DNL Phoenix] servidor. Especifique /hbasephoenix0 se estiver usando [!DNL Azure] Cluster HDInsights. |
| `enableSsl` | Um valor booleano. Especifica se as conexões com o servidor são criptografadas usando SSL. |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de uma origem, incluindo especificações de autenticação relacionadas à criação das conexões de base e de origem. A ID da especificação de conexão para [!DNL Phoenix] é: `102706fb-a5cd-42ee-afe0-bc42f017ff43` |

Para obter mais informações sobre a introdução, consulte [este documento Phoenix](https://python-phoenixdb.readthedocs.io/en/latest/api.html).

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da Platform com êxito, consulte o manual em [introdução às APIs da Platform](../../../../../landing/api-guide.md).

## Criar uma conexão básica

Uma conexão base retém informações entre sua origem e a Platform, incluindo as credenciais de autenticação da origem, o estado atual da conexão e sua ID de conexão base exclusiva. A ID de conexão básica permite explorar e navegar pelos arquivos de dentro da origem e identificar os itens específicos que deseja assimilar, incluindo informações sobre os tipos de dados e formatos.

Para criar uma conexão base, faça uma solicitação POST ao `/connections` ao fornecer sua [!DNL Phoenix] credenciais de autenticação no corpo da solicitação.

**Formato da API**

```https
POST /connections
```

**Solicitação**

A solicitação a seguir cria uma conexão básica para [!DNL Phoenix]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Phoenix test connection",
      "description": "Phoenix test connection",
      "auth": {
          "specName": "Basic Authentication",
      "params": {
          "host":  "{HOST}",
          "username": "{USERNAME}",
          "password":"{PASSWORD}",
          "port": {PORT},
          "httpPath": "{PATH}",
          "enableSsl": {SSL}
          }
      },
      "connectionSpec": {
          "id": "102706fb-a5cd-42ee-afe0-bc42f017ff43",
          "version": "1.0"
      }
  }'
```

| Propriedade | Descrição |
| --------- | ----------- |
| `auth.params.host` | O host do [!DNL Phoenix] servidor. |
| `auth.params.username` | O nome de usuário associado à [!DNL Phoenix] conexão. |
| `auth.params.password` | A senha associada ao seu [!DNL Phoenix] conexão. |
| `auth.params.port` | A porta TCP para o seu [!DNL Phoenix] conexão. |
| `auth.params.httpPath` | O caminho http parcial para o [!DNL Phoenix] conexão. |
| `auth.params.enableSsl` | O valor booleano que especifica se as conexões com o servidor são criptografadas usando SSL. |
| `connectionSpec.id` | A variável [!DNL Phoenix] ID da especificação de conexão: `102706fb-a5cd-42ee-afe0-bc42f017ff43`. |

**Resposta**

Uma resposta bem-sucedida retorna detalhes da conexão recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID é necessária para explorar seus dados no próximo tutorial.

```json
{
    "id": "0d982fff-c443-403e-982f-ffc443f03e37",
    "etag": "\"830082dc-0000-0200-0000-5e84ee560000\""
}
```

## Próximas etapas

Ao seguir este tutorial, você criou um [!DNL Phoenix] conexão básica usando o [!DNL Flow Service] API. Você pode usar essa ID de conexão básica nos seguintes tutoriais:

* [Explore a estrutura e o conteúdo das tabelas de dados usando o [!DNL Flow Service] API](../../explore/tabular.md)
* [Crie um fluxo de dados para trazer dados do banco de dados para a Platform usando o [!DNL Flow Service] API](../../collect/database-nosql.md)
