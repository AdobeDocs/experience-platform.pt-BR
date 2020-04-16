---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Criar um conector Gen2 do Armazenamento Azure Data Lake usando a API de Serviço de Fluxo
topic: overview
translation-type: tm+mt
source-git-commit: 065076aee83990bcad0110f0d7704a60fac400c6

---


# Criar um conector Gen2 do Armazenamento Azure Data Lake usando a API de Serviço de Fluxo

O Serviço de fluxo é usado para coletar e centralizar dados do cliente de várias fontes diferentes na Adobe Experience Platform. O serviço fornece uma interface de usuário e uma RESTful API a partir da qual todas as fontes compatíveis são conectáveis.

Este tutorial usa a API de Serviço de Fluxo para guiá-lo pelas etapas para conectar a Plataforma de Experiência ao Armazenamento Azure Data Lake Gen2 (a seguir denominado &quot;ADLS Gen2&quot;).

## Introdução

Este guia exige uma compreensão prática dos seguintes componentes da Adobe Experience Platform:

* [Fontes](../../../../home.md): A Plataforma de experiência permite que os dados sejam assimilados de várias fontes e, ao mesmo tempo, fornece a você a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.
* [Caixas de proteção](../../../../../sandboxes/home.md): A plataforma Experience fornece caixas de proteção virtuais que particionam uma única instância da Plataforma em ambientes virtuais separados para ajudar a desenvolver e desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para criar com êxito um conector de origem ADLS Gen2 usando a API de Serviço de Fluxo.

### Reunir credenciais obrigatórias

Para que o Serviço de Fluxo se conecte ao ADLS Gen2, é necessário fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `url` | O URL do endereço. |
| `servicePrincipalId` | A ID do cliente do aplicativo. |
| `servicePrincipalKey` | A chave do aplicativo. |
| `tenant` | As informações do locatário que contêm seu aplicativo. |

Para obter mais informações sobre esses valores, consulte [este documento](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-data-lake-storage)ADLS Gen2.

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

## Pesquisar especificações de conexão

Antes de conectar Plataforma ao ADLS Gen2, verifique se há especificações de conexão para ADLS Gen2. Se as especificações de conexão não existirem, não será possível estabelecer uma conexão.

Cada fonte disponível tem seu próprio conjunto exclusivo de especificações de conexão para descrever propriedades do conector, como requisitos de autenticação. Você pode procurar especificações de conexão para ADLS Gen2 executando uma solicitação GET e usando parâmetros de query.

**Formato da API**

Enviar uma solicitação GET sem parâmetros de query retornará especificações de conexão para todas as fontes disponíveis. Você pode incluir o query `property=name=="adls-gen2"` para obter informações especificamente para o ADLS Gen2.

```http
GET /connectionSpecs
GET /connectionSpecs?property=name=="adls-gen2"
```

**Solicitação**

A solicitação a seguir recupera as especificações de conexão para ADLS Gen2.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="adls-gen2"' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna as especificações de conexão para ADLS Gen2, incluindo seu identificador exclusivo (`id`). Essa ID é necessária na próxima etapa para criar uma conexão básica.

```json
{
    "items": [
        {
            "id": "b3ba5556-48be-44b7-8b85-ff2b69b46dc4",
            "name": "adls-gen2",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "authSpec": [
                {
                    "name": "Basic Authentication for adls-gen2",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines auth params required for connecting to adlsgen2 using service principal",
                        "properties": {
                            "url": {
                                "type": "string",
                                "description": "Endpoint for Azure Data Lake Storage Gen2."
                            },
                            "servicePrincipalId": {
                                "type": "string",
                                "description": "Service Principal Id to connect to ADLSGen2."
                            },
                            "servicePrincipalKey": {
                                "type": "string",
                                "description": "Service Principal Key to connect to ADLSGen2.",
                                "format": "password"
                            },
                            "tenant": {
                                "type": "string",
                                "description": "Tenant information(domain name or tenant ID)."
                            }
                        },
                        "required": [
                            "url",
                            "servicePrincipalId",
                            "servicePrincipalKey",
                            "tenant"
                        ]
                    }
                }
            ]
        }
    ]
}
```

## Criar uma conexão básica

Uma conexão básica especifica uma fonte e contém suas credenciais para essa fonte. Somente uma conexão básica é necessária por conta ADLS Gen2, pois pode ser usada para criar vários conectores de origem para trazer dados diferentes.

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
    -d '{
        "name": "adls-gen2",
        "description": "base connection for adls-gen2",
        "auth": {
            "specName": "Basic Authentication for adls-gen2",
            "params": {
                "url": "{URL}",
                "servicePrincipalId": "{SERVICE_PRINCIPAL_ID}",
                "servicePrincipalKey": "{SERVICE_PRINCIPAL_KEY}",
                "tenant": "{TENANT}"
            }
        },
        "connectionSpec": {
            "id": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0"
        }
    }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `auth.params.url` | O endpoint de URL para sua conta ADLS Gen2. |
| `auth.params.servicePrincipalId` | A ID principal de serviço da sua conta ADLS Gen2. |
| `auth.params.servicePrincipalKey` | A chave principal de serviço da sua conta ADLS Gen2. |
| `auth.params.tenant` | As informações de locatário de sua conta ADLS Gen2. |
| `connectionSpec.id` | A especificação de conexão `id` da sua conta ADLS Gen2 recuperada na etapa anterior. |

**Resposta**

Uma resposta bem-sucedida retorna detalhes da conexão básica recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID é necessária para explorar seu armazenamento em nuvem na próxima etapa.

```json
{
    "id": "7497ad71-6d32-4973-97ad-716d32797304",
    "etag": "\"23005f80-0000-0200-0000-5e1d00a20000\""
}
```

## Próximas etapas

Ao seguir este tutorial, você criou uma conexão ADLS Gen2 usando APIs e uma ID exclusiva foi obtida como parte do corpo da resposta. Você pode usar essa ID de conexão para [explorar armazenamentos em nuvem usando a API](../../explore/cloud-storage.md) do Serviço de Fluxo ou [assimilando dados de parquet usando a API](../../cloud-storage-parquet.md)do Serviço de Fluxo.
