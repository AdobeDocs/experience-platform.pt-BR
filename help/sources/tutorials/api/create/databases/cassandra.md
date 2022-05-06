---
keywords: Experience Platform, home, tópicos populares, Apache Cassandra, apache Cassandra, Cassandra, cassandra
solution: Experience Platform
title: Criar uma conexão de fonte do Apache Cassandra usando a API do Serviço de fluxo
topic-legacy: overview
type: Tutorial
description: Saiba como conectar o Apache Cassandra à Adobe Experience Platform usando a API do Serviço de Fluxo.
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 4%

---


# Crie um [!DNL Apache Cassandra] conexão de origem usando o [!DNL Flow Service] API

[!DNL Flow Service] O é usado para coletar e centralizar dados do cliente de várias fontes diferentes no Adobe Experience Platform. O serviço fornece uma interface de usuário e uma RESTful API da qual todas as fontes compatíveis são conectáveis.

Este tutorial usa o [!DNL Flow Service] API para orientá-lo pelas etapas para se conectar [!DNL Apache Cassandra] (a seguir designada &quot;Cassandra&quot;) [!DNL Experience Platform].

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../../../home.md): [!DNL Experience Platform] permite que os dados sejam assimilados de várias fontes, fornecendo a capacidade de estruturar, rotular e aprimorar os dados recebidos usando [!DNL Platform] serviços.
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com sucesso ao Cassandra usando o [!DNL Flow Service] API.

### Obter credenciais necessárias

Para [!DNL Flow Service] para conectar-se com [!DNL Cassandra], você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `host` | O endereço IP ou o nome do host do [!DNL Cassandra] servidor. |
| `port` | A porta TCP que [!DNL Cassandra] O servidor usa o para detectar as conexões do cliente. A porta padrão é `9042`. |
| `username` | O nome de usuário usado para se conectar ao [!DNL Cassandra] para autenticação. |
| `password` | A senha para se conectar ao [!DNL Cassandra] para autenticação. |
| `connectionSpec.id` | O identificador exclusivo necessário para criar uma conexão. A ID de especificação de conexão para [!DNL Cassandra] é `a8f4d393-1a6b-43f3-931f-91a16ed857f4`. |

Para obter mais informações sobre a introdução, consulte [este documento Cassandra](https://cassandra.apache.org/doc/latest/operating/security.html#authentication).

### Lendo exemplos de chamadas de API

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações do . Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de exemplo retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler exemplos de chamadas de API](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) no [!DNL Experience Platform] guia de solução de problemas.

### Coletar valores para cabeçalhos necessários

Para fazer chamadas para [!DNL Platform] As APIs devem ser concluídas primeiro [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todos [!DNL Experience Platform] Chamadas de API, conforme mostrado abaixo:

* Autorização: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Todos os recursos em [!DNL Experience Platform], incluindo os pertencentes ao [!DNL Flow Service], são isoladas em sandboxes virtuais específicas. Todas as solicitações para [!DNL Platform] As APIs exigem um cabeçalho que especifica o nome da sandbox em que a operação ocorrerá:

* x-sandbox-name: `{SANDBOX_NAME}`

Todas as solicitações que contêm uma carga útil (POST, PUT, PATCH) exigem um cabeçalho de tipo de mídia adicional:

* Tipo de conteúdo: `application/json`

## Criar uma conexão

Uma conexão especifica uma fonte e contém suas credenciais para essa fonte. Somente um conector é necessário por [!DNL Cassandra] , pois pode ser usada para criar vários conectores de origem para trazer dados diferentes.

**Formato da API**

```http
POST /connections
```

**Solicitação**

Para criar um [!DNL Cassandra] para conexão, a ID de especificação de conexão exclusiva deve ser fornecida como parte da solicitação POST. A ID de especificação de conexão para [!DNL Cassandra] é `a8f4d393-1a6b-43f3-931f-91a16ed857f4`.

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
| `auth.params.host` | O endereço IP ou o nome do host do [!DNL Cassandra] servidor. |
| `auth.params.port` | A porta TCP que [!DNL Cassandra] O servidor usa o para detectar as conexões do cliente. A porta padrão é `9042`. |
| `auth.params.username` | O nome de usuário usado para se conectar ao [!DNL Cassandra] para autenticação. |
| `auth.params.password` | A senha para se conectar ao [!DNL Cassandra] para autenticação. |
| `connectionSpec.id` | O [!DNL Cassandra] ID de especificação de conexão: `a8f4d393-1a6b-43f3-931f-91a16ed857f4`. |

**Resposta**

Uma resposta bem-sucedida retorna detalhes da conexão recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID é necessária para explorar seus dados no próximo tutorial.

```json
{
    "id": "ce69aa89-1baa-4054-a9aa-891baa605425",
    "etag": "\"5a026e19-0000-0200-0000-5eac76d00000\""
}
```

## Próximas etapas

Ao seguir este tutorial, você criou um [!DNL Cassandra] conexão usando o [!DNL Flow Service] API e obtiveram o valor de ID exclusivo da conexão. Você pode usar essa ID no próximo tutorial enquanto aprende a usar [explorar bancos de dados usando a API do Serviço de Fluxo](../../explore/database-nosql.md).
