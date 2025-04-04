---
keywords: Experience Platform;página inicial;tópicos populares;Apache Cassandra;apache cassandra;Cassandra;cassandra
solution: Experience Platform
title: Criar uma conexão do Apache Cassandra Source usando a API do serviço de fluxo
type: Tutorial
description: Saiba como conectar o Apache Cassandra ao Adobe Experience Platform usando a API do Serviço de fluxo.
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 11%

---


# Criar uma conexão de origem [!DNL Apache Cassandra] usando a API [!DNL Flow Service]

O [!DNL Flow Service] é usado para coletar e centralizar dados do cliente de várias fontes diferentes na Adobe Experience Platform. O serviço fornece uma interface de usuário e a API RESTful a partir da qual todas as fontes compatíveis são conectáveis.

Este tutorial usa a API [!DNL Flow Service] para guiá-lo pelas etapas de conexão do [!DNL Apache Cassandra] (doravante denominado &quot;Cassandra&quot;) ao [!DNL Experience Platform].

## Introdução

Este manual necessita de uma compreensão funcional dos seguintes componentes da Adobe Experience Platform:

* [Fontes](../../../../home.md): [!DNL Experience Platform] permite que os dados sejam assimilados de várias fontes e fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços do [!DNL Experience Platform].
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única instância do [!DNL Experience Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito ao Cassandra usando a API [!DNL Flow Service].

### Coletar credenciais necessárias

Para que [!DNL Flow Service] se conecte a [!DNL Cassandra], você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `host` | O endereço IP ou o nome de host do servidor [!DNL Cassandra]. |
| `port` | A porta TCP que o servidor [!DNL Cassandra] usa para escutar conexões de clientes. A porta padrão é `9042`. |
| `username` | O nome de usuário usado para conexão com o servidor [!DNL Cassandra] para autenticação. |
| `password` | A senha para conexão com o servidor [!DNL Cassandra] para autenticação. |
| `connectionSpec.id` | O identificador exclusivo necessário para criar uma conexão. A ID da especificação de conexão para [!DNL Cassandra] é `a8f4d393-1a6b-43f3-931f-91a16ed857f4`. |

Para obter mais informações sobre como começar, consulte [este documento Cassandra](https://cassandra.apache.org/doc/latest/operating/security.html#authentication).

### Leitura de chamadas de API de amostra

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e conteúdos de solicitação formatados corretamente. Também fornece exemplos de JSON retornado nas respostas da API. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas [!DNL Experience Platform].

### Coletar valores para cabeçalhos necessários

Para fazer chamadas para APIs do [!DNL Experience Platform], primeiro complete o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). Concluir o tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API da [!DNL Experience Platform], conforme mostrado abaixo:

* Autorização: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id `{ORG_ID}`

Todos os recursos em [!DNL Experience Platform], incluindo aqueles pertencentes a [!DNL Flow Service], estão isolados em sandboxes virtuais específicas. Todas as solicitações para [!DNL Experience Platform] APIs exigem um cabeçalho que especifique o nome da sandbox em que a operação ocorrerá:

* x-sandbox-name: `{SANDBOX_NAME}`

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho de tipo de mídia adicional:

* Tipo de conteúdo: `application/json`

## Criar uma conexão

Uma conexão especifica uma origem e contém suas credenciais para essa origem. Somente um conector é necessário por conta [!DNL Cassandra], pois pode ser usado para criar vários conectores de origem para trazer dados diferentes.

**Formato da API**

```http
POST /connections
```

**Solicitação**

Para criar uma conexão [!DNL Cassandra], sua identificação de especificação de conexão exclusiva deve ser fornecida como parte da solicitação POST. A ID da especificação de conexão para [!DNL Cassandra] é `a8f4d393-1a6b-43f3-931f-91a16ed857f4`.

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
| `auth.params.host` | O endereço IP ou o nome de host do servidor [!DNL Cassandra]. |
| `auth.params.port` | A porta TCP que o servidor [!DNL Cassandra] usa para escutar conexões de clientes. A porta padrão é `9042`. |
| `auth.params.username` | O nome de usuário usado para conexão com o servidor [!DNL Cassandra] para autenticação. |
| `auth.params.password` | A senha para conexão com o servidor [!DNL Cassandra] para autenticação. |
| `connectionSpec.id` | A ID de especificação de conexão [!DNL Cassandra]: `a8f4d393-1a6b-43f3-931f-91a16ed857f4`. |

**Resposta**

Uma resposta bem-sucedida retorna detalhes da conexão recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID é necessária para explorar seus dados no próximo tutorial.

```json
{
    "id": "ce69aa89-1baa-4054-a9aa-891baa605425",
    "etag": "\"5a026e19-0000-0200-0000-5eac76d00000\""
}
```

## Próximas etapas

Seguindo este tutorial, você criou uma conexão [!DNL Cassandra] usando a API [!DNL Flow Service] e obteve o valor de identificador exclusivo da conexão. Você pode usar essa ID no próximo tutorial enquanto aprende a [explorar bancos de dados usando a API do Serviço de Fluxo](../../explore/database-nosql.md).
