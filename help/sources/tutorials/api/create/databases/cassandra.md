---
keywords: Experience Platform;página inicial;tópicos populares;Apache Cassandra;apache cassandra;Cassandra;cassandra
solution: Experience Platform
title: Criar uma conexão de origem do Apache Cassandra usando a API do serviço de fluxo
type: Tutorial
description: Saiba como conectar o Apache Cassandra ao Adobe Experience Platform usando a API do Serviço de fluxo.
source-git-commit: 997423f7bf92469e29c567bd77ffde357413bf9e
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 4%

---


# Criar um [!DNL Apache Cassandra] conexão de origem usando o [!DNL Flow Service] API

[!DNL Flow Service] O é usado para coletar e centralizar dados do cliente de várias fontes diferentes no Adobe Experience Platform. O serviço fornece uma interface de usuário e a API RESTful a partir da qual todas as fontes compatíveis são conectáveis.

Este tutorial usa o [!DNL Flow Service] API para orientá-lo pelas etapas de conexão [!DNL Apache Cassandra] (a seguir designada &quot;Cassandra&quot;) a [!DNL Experience Platform].

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Origens](../../../../home.md): [!DNL Experience Platform] O permite que os dados sejam assimilados de várias fontes e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando o [!DNL Platform] serviços.
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] O fornece sandboxes virtuais que particionam uma única [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem as informações adicionais que você precisará saber para se conectar com êxito ao Cassandra usando o [!DNL Flow Service] API.

### Coletar credenciais necessárias

A fim de [!DNL Flow Service] para se conectar com [!DNL Cassandra], você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `host` | O endereço IP ou o nome de host do [!DNL Cassandra] servidor. |
| `port` | A porta TCP que o [!DNL Cassandra] O servidor usa o para detectar conexões de clientes. A porta padrão é `9042`. |
| `username` | O nome de usuário usado para se conectar ao [!DNL Cassandra] servidor para autenticação. |
| `password` | A senha para se conectar ao [!DNL Cassandra] servidor para autenticação. |
| `connectionSpec.id` | O identificador exclusivo necessário para criar uma conexão. A ID da especificação de conexão para [!DNL Cassandra] é `a8f4d393-1a6b-43f3-931f-91a16ed857f4`. |

Para obter mais informações sobre a introdução, consulte [este documento Cassandra](https://cassandra.apache.org/doc/latest/operating/security.html#authentication).

### Leitura de chamadas de API de amostra

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O exemplo de JSON retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) no [!DNL Experience Platform] guia de solução de problemas.

### Coletar valores para cabeçalhos obrigatórios

Para fazer chamadas para [!DNL Platform] APIs, primeiro conclua o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). Concluir o tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todos os [!DNL Experience Platform] Chamadas de API, conforme mostrado abaixo:

* Autorização: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Todos os recursos em [!DNL Experience Platform], incluindo as que pertencem à [!DNL Flow Service], são isolados em sandboxes virtuais específicas. Todas as solicitações para [!DNL Platform] As APIs exigem um cabeçalho que especifique o nome da sandbox em que a operação ocorrerá:

* x-sandbox-name: `{SANDBOX_NAME}`

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho de tipo de mídia adicional:

* Tipo de conteúdo: `application/json`

## Criar uma conexão

Uma conexão especifica uma origem e contém suas credenciais para essa origem. Somente um conector é necessário por [!DNL Cassandra] conta, pois pode ser usada para criar vários conectores de origem para trazer dados diferentes.

**Formato da API**

```http
POST /connections
```

**Solicitação**

Para criar um [!DNL Cassandra] conexão, sua ID de especificação de conexão exclusiva deve ser fornecida como parte da solicitação POST. A ID da especificação de conexão para [!DNL Cassandra] é `a8f4d393-1a6b-43f3-931f-91a16ed857f4`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Cassandra test connection",
        "description": "A test connection for Cassandra",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                    "host": "{HOST},
                    "port": "{PORT}",
                    "username": "{USERNAME}",
                    "password": "{PASSWORD}"
                }
        },
        "connectionSpec": {
            "id": "a8f4d393-1a6b-43f3-931f-91a16ed857f4",
            "version": "1.0"
        }
    }'
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `auth.params.host` | O endereço IP ou o nome de host do [!DNL Cassandra] servidor. |
| `auth.params.port` | A porta TCP que o [!DNL Cassandra] O servidor usa o para detectar conexões de clientes. A porta padrão é `9042`. |
| `auth.params.username` | O nome de usuário usado para se conectar ao [!DNL Cassandra] servidor para autenticação. |
| `auth.params.password` | A senha para se conectar ao [!DNL Cassandra] servidor para autenticação. |
| `connectionSpec.id` | A variável [!DNL Cassandra] ID de especificação da conexão: `a8f4d393-1a6b-43f3-931f-91a16ed857f4`. |

**Resposta**

Uma resposta bem-sucedida retorna detalhes da conexão recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID é necessária para explorar seus dados no próximo tutorial.

```json
{
    "id": "ce69aa89-1baa-4054-a9aa-891baa605425",
    "etag": "\"5a026e19-0000-0200-0000-5eac76d00000\""
}
```

## Próximas etapas

Ao seguir este tutorial, você criou um [!DNL Cassandra] conexão usando o [!DNL Flow Service] e obtiveram o valor de ID exclusivo da conexão. Você pode usar essa ID no próximo tutorial enquanto aprende a [explorar bancos de dados usando a API do Serviço de Fluxo](../../explore/database-nosql.md).
