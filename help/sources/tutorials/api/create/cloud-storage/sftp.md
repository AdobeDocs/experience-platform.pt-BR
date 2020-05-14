---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Criar um conector SFTP usando a API de Serviço de Fluxo
topic: overview
translation-type: tm+mt
source-git-commit: 37a5f035023cee1fc2408846fb37d64b9a3fc4b6
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 2%

---


# Criar um conector SFTP usando a API de Serviço de Fluxo

>[!NOTE]
>O conector SFTP está em beta. Os recursos e a documentação estão sujeitos a alterações.

O Serviço de fluxo é usado para coletar e centralizar dados do cliente de várias fontes diferentes na Adobe Experience Platform. O serviço fornece uma interface de usuário e uma RESTful API a partir da qual todas as fontes compatíveis são conectáveis.

Este tutorial usa a API de Serviço de Fluxo para guiá-lo pelas etapas para conectar a Experience Platform a um servidor SFTP (Secure File Transfer Protocol).

Se você preferir usar a interface do usuário na plataforma da experiência, o tutorial [da](../../../ui/create/cloud-storage/ftp-sftp.md) interface fornece instruções passo a passo para executar ações semelhantes.

## Introdução

Este guia exige uma compreensão prática dos seguintes componentes da Adobe Experience Platform:

* [Fontes](../../../../home.md): A Plataforma de experiência permite que os dados sejam assimilados de várias fontes e, ao mesmo tempo, fornece a você a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.
* [Caixas de proteção](../../../../../sandboxes/home.md): A plataforma Experience fornece caixas de proteção virtuais que particionam uma única instância da Plataforma em ambientes virtuais separados para ajudar a desenvolver e desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito a um servidor SFTP usando a API de Serviço de Fluxo.

### Reunir credenciais obrigatórias

Para que o Serviço de fluxo se conecte ao SFTP, é necessário fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `host` | O nome ou endereço IP associado ao servidor SFTP. |
| `username` | O nome de usuário com acesso ao seu servidor SFTP. |
| `password` | A senha do servidor SFTP. |

### Lendo chamadas de exemplo da API

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção sobre [como ler chamadas](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de exemplo no guia de solução de problemas da plataforma Experience.

### Reunir valores para cabeçalhos necessários

Para fazer chamadas para APIs de plataforma, você deve primeiro concluir o tutorial [de](../../../../../tutorials/authentication.md)autenticação. A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas da API da plataforma da experiência, como mostrado abaixo:

* Autorização: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos na plataforma Experience, incluindo os pertencentes ao Serviço de Fluxo, são isolados para caixas de proteção virtuais específicas. Todas as solicitações para APIs de plataforma exigem um cabeçalho que especifique o nome da caixa de proteção em que a operação ocorrerá:

* x-sandbox-name: `{SANDBOX_NAME}`

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho de tipo de mídia adicional:

* Tipo de conteúdo: `application/json`

## Criar uma conexão

Uma conexão especifica uma fonte e contém suas credenciais para essa fonte. Somente uma conexão é necessária por conta SFTP, pois pode ser usada para criar vários conectores de origem para trazer dados diferentes.

**Formato da API**

```http
POST /connections
```

**Solicitação**

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d  "auth": {
        "specName": "Basic Authentication for sftp",
        "params": {
            "host": "{HOST_NAME}",
            "userName": "{USER_NAME}",
            "password": "{PASSWORD}"
        }
    },
    "connectionSpec": {
        "id": "b7bf2577-4520-42c9-bae9-cad01560f7bc",
        "version": "1.0"
    }
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `auth.params.host` | O nome do host do servidor SFTP. |
| `auth.params.username` | O nome de usuário associado ao servidor SFTP. |
| `auth.params.password` | A senha associada ao servidor SFTP. |
| `connectionSpec.id` | A ID da especificação da conexão do servidor STFP: `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

**Resposta**

Uma resposta bem-sucedida retorna o identificador exclusivo (`id`) da conexão recém-criada. Essa ID é necessária para explorar o servidor SFTP no próximo tutorial.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

## Próximas etapas

Ao seguir este tutorial, você criou uma conexão SFTP usando a API de Serviço de Fluxo e obteve o valor de ID exclusivo da conexão. Você pode usar essa ID de conexão para [explorar armazenamentos em nuvem usando a API](../../explore/cloud-storage.md) do Serviço de Fluxo ou [assimilando dados de parquet usando a API](../../cloud-storage-parquet.md)do Serviço de Fluxo.
