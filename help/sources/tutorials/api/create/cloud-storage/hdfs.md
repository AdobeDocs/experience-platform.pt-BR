---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Criar um conector Apache HDFS usando a API de Serviço de Fluxo
topic: overview
translation-type: tm+mt
source-git-commit: e5789a10c49b2933a0727692dedf2601a214dbc2
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 2%

---


# Criar um conector Apache HDFS usando a API de Serviço de Fluxo

>[!NOTE]
>O conector HDFS Apache está em beta. Os recursos e a documentação estão sujeitos a alterações.

O Serviço de fluxo é usado para coletar e centralizar os dados do cliente de várias fontes diferentes para inserir a Adobe Experience Platform. O serviço fornece uma interface de usuário e uma RESTful API a partir da qual todas as fontes compatíveis são conectáveis.

Este tutorial usa a API de Serviço de Fluxo para guiá-lo pelas etapas para conectar um Apache Hadoop Distributed File System (a seguir denominado &quot;HDFS&quot;) à Experience Platform.

## Introdução

Este guia exige uma compreensão prática dos seguintes componentes da Adobe Experience Platform:

* [Fontes](../../../../home.md): A Plataforma de experiência permite que os dados sejam assimilados de várias fontes e, ao mesmo tempo, fornece a você a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.
* [Caixas de proteção](../../../../../sandboxes/home.md): A plataforma Experience fornece caixas de proteção virtuais que particionam uma única instância da Plataforma em ambientes virtuais separados para ajudar a desenvolver e desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito ao HDFS usando a API de Serviço de Fluxo.

### Reunir credenciais obrigatórias

| Credencial | Descrição |
| ---------- | ----------- |
| `url` | O URL define os parâmetros de autenticação necessários para a conexão anônima com o HDFS. Para obter mais informações sobre como obter este valor, consulte [este documento](https://hadoop.apache.org/docs/r1.2.1/HttpAuthentication.html)HDFS. |
| `connectionSpec.id` | O identificador necessário para criar uma conexão. A ID de especificação de conexão fixa para HDFS é `54e221aa-d342-4707-bcff-7a4bceef0001`. |

### Lendo chamadas de exemplo da API

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção sobre [como ler chamadas](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de exemplo no guia de solução de problemas da plataforma Experience.

### Reunir valores para cabeçalhos necessários

Para fazer chamadas para APIs de plataforma, você deve primeiro concluir o tutorial [de](../../../../../tutorials/authentication.md)autenticação. A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas da API da plataforma da experiência, como mostrado abaixo:

* Autorização: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos na plataforma Experience, incluindo os pertencentes ao Serviço de fluxo, estão isolados para caixas de proteção virtuais específicas. Todas as solicitações para APIs de plataforma exigem um cabeçalho que especifique o nome da caixa de proteção em que a operação ocorrerá:

* x-sandbox-name: `{SANDBOX_NAME}`

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho de tipo de mídia adicional:

* Tipo de conteúdo: `application/json`

## Criar uma conexão

Uma conexão especifica uma fonte e contém suas credenciais para essa fonte. Apenas uma conexão é necessária por conta HDFS, pois pode ser usada para criar vários conectores de origem para trazer dados diferentes.

**Formato da API**

```http
POST /connections
```

**Solicitação**

A solicitação a seguir cria uma nova conexão HDFS, configurada pelas propriedades fornecidas na carga:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "HDFS test connection",
        "description": "A test connection for an HDFS source",
        "auth": {
            "specName": "Anonymous Authentication",
            "params": {
                "url": "{URL}"
                }
        },
        "connectionSpec": {
            "id": "54e221aa-d342-4707-bcff-7a4bceef0001",
            "version": "1.0"
        }
    }'
```

| Propriedade | Descrição |
| --------- | ----------- |
| `auth.params.url` | O URL que define os parâmetros de autenticação necessários para conectar-se ao HDFS anonimamente |
| `connectionSpec.id` | A ID de especificação de conexão HDFS: `54e221aa-d342-4707-bcff-7a4bceef0001`. |

**Resposta**

Uma resposta bem-sucedida retorna detalhes da conexão recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID é necessária para explorar seus dados no próximo tutorial.

```json
{
    "id": "6a6a880a-2b15-4051-aa88-0a2b1570516d",
    "etag": "\"1801bb7d-0000-0200-0000-5ed6ad580000\""
}
```

## Próximas etapas

Ao seguir este tutorial, você criou uma conexão HDFS usando a API Serviço de Fluxo e obteve o valor de ID exclusivo da conexão. Você pode usar essa ID no próximo tutorial à medida que aprende a [explorar um armazenamento em nuvem de terceiros usando a API](../../explore/cloud-storage.md)de Serviço de Fluxo.
