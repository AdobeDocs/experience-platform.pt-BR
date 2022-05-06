---
keywords: Experience Platform, home, tópicos populares, Phoenix, phonix
solution: Experience Platform
title: Criar uma conexão base Phoenix usando a API do Serviço de fluxo
topic-legacy: overview
type: Tutorial
description: Saiba como conectar um banco de dados Phoenix à Adobe Experience Platform usando a API do Serviço de Fluxo.
exl-id: b69d9593-06fe-4fff-88a9-7860e4e45eb7
source-git-commit: 93061c84639ca1fdd3f7abb1bbd050eb6eebbdd6
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 1%

---

# Crie um [!DNL Phoenix] conexão básica usando o [!DNL Flow Service] API

>[!NOTE]
>
>O [!DNL Phoenix] O conector está em beta. Consulte a [Visão geral das fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores com rótulo beta.

[!DNL Flow Service] O é usado para coletar e centralizar dados do cliente de várias fontes diferentes no Adobe Experience Platform. O serviço fornece uma interface de usuário e uma RESTful API da qual todas as fontes compatíveis são conectáveis.

Este tutorial usa o [!DNL Flow Service] API para orientá-lo pelas etapas para conectar um [!DNL Phoenix] banco de dados para [!DNL Experience Platform].

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../../../home.md): [!DNL Experience Platform] permite que os dados sejam assimilados de várias fontes, fornecendo a capacidade de estruturar, rotular e aprimorar os dados recebidos usando [!DNL Platform] serviços.
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito ao [!DNL Phoenix] usando o [!DNL Flow Service] API.

### Obter credenciais necessárias

Para [!DNL Flow Service] para conectar-se com [!DNL Phoenix], você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `host` | O endereço IP ou o nome do host do [!DNL Phoenix] servidor. |
| `username` | O nome de usuário que você usa para acessar [!DNL Phoenix] Servidor. |
| `password` | A senha correspondente ao usuário. |
| `port` | A porta TCP que [!DNL Phoenix] O servidor usa o para detectar as conexões do cliente. Se você se conectar a [!DNL Azure] HDInsights, especifique a porta como 443. |
| `httpPath` | O URL parcial correspondente ao [!DNL Phoenix] servidor. Especifique /hbasephonix0 se estiver usando [!DNL Azure] Cluster HDInsights. |
| `enableSsl` | Um valor booleano. Especifica se as conexões com o servidor são criptografadas usando SSL. |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de origem, incluindo especificações de autenticação relacionadas à criação das conexões base e de origem. A ID de especificação de conexão para [!DNL Phoenix] é: `102706fb-a5cd-42ee-afe0-bc42f017ff43` |

Para obter mais informações sobre a introdução, consulte [este documento Phoenix](https://python-phoenixdb.readthedocs.io/en/latest/api.html).

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da plataforma com êxito, consulte o guia em [introdução às APIs do Platform](../../../../../landing/api-guide.md).

## Criar uma conexão base

Uma conexão base retém informações entre a fonte e a Plataforma, incluindo as credenciais de autenticação da fonte, o estado atual da conexão e a ID de conexão base exclusiva. A ID de conexão básica permite explorar e navegar pelos arquivos da fonte e identificar os itens específicos que deseja assimilar, incluindo informações sobre os tipos e formatos de dados.

Para criar uma ID de conexão base, faça uma solicitação de POST para a variável `/connections` endpoint enquanto fornece seu [!DNL Phoenix] credenciais de autenticação como parte dos parâmetros da solicitação.

**Formato da API**

```https
POST /connections
```

**Solicitação**

A solicitação a seguir cria uma conexão base para [!DNL Phoenix]:

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
| `auth.params.password` | A senha associada à sua [!DNL Phoenix] conexão. |
| `auth.params.port` | A porta TCP para o seu [!DNL Phoenix] conexão. |
| `auth.params.httpPath` | O caminho http parcial para seu [!DNL Phoenix] conexão. |
| `auth.params.enableSsl` | O valor booleano que especifica se as conexões com o servidor são criptografadas usando SSL. |
| `connectionSpec.id` | O [!DNL Phoenix] ID de especificação de conexão: `102706fb-a5cd-42ee-afe0-bc42f017ff43`. |

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
