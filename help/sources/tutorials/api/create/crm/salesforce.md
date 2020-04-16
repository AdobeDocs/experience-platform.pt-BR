---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Criar um conector Salesforce usando a API de Serviço de Fluxo
topic: overview
translation-type: tm+mt
source-git-commit: cc999ce1ab426f412c0cc2b69173a336a14024f3

---


# Criar um conector Salesforce usando a API de Serviço de Fluxo

O Serviço de fluxo é usado para coletar e centralizar dados do cliente de várias fontes diferentes na Adobe Experience Platform. O serviço fornece uma interface de usuário e uma RESTful API a partir da qual todas as fontes compatíveis são conectáveis.

Este tutorial usa a API de Serviço de Fluxo para guiá-lo pelas etapas para conectar a Plataforma a uma conta Salesforce para coletar dados do CRM.

Se você preferir usar a interface do usuário na Experience Platform, o tutorial [da interface do usuário do conector de origem do Salesforce ou](../../../ui/create/crm/dynamics-salesforce.md) Dinâmica fornece instruções passo a passo para executar ações semelhantes.

## Introdução

Este guia exige uma compreensão prática dos seguintes componentes da Adobe Experience Platform:

* [Fontes](../../../../home.md): A Plataforma de experiência permite que os dados sejam assimilados de várias fontes e, ao mesmo tempo, fornece a você a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.
* [Caixas de proteção](../../../../../sandboxes/home.md): A plataforma Experience fornece caixas de proteção virtuais que particionam uma única instância da Plataforma em ambientes virtuais separados para ajudar a desenvolver e desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito à Plataforma a uma conta do Salesforce usando a API de Serviço de Fluxo.

### Reunir credenciais obrigatórias

Para que o Serviço de Fluxo se conecte ao Salesforce, é necessário fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `environmentUrl` | O URL da instância de origem do Salesforce. |
| `username` | O nome de usuário da conta de usuário do Salesforce. |
| `password` | A senha da conta de usuário do Salesforce. |
| `securityToken` | O token de segurança da conta de usuário do Salesforce. |

Para obter mais informações sobre como começar, visite [este documento](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm)do Salesforce.

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

Antes de conectar a Plataforma a uma conta Salesforce, verifique se as especificações de conexão existem para o Salesforce. Se as especificações de conexão não existirem, não será possível estabelecer uma conexão.

Cada fonte disponível tem seu próprio conjunto exclusivo de especificações de conexão para descrever propriedades do conector, como requisitos de autenticação. Você pode procurar especificações de conexão para o Salesforce executando uma solicitação GET e usando parâmetros de query.

**Formato da API**

Enviar uma solicitação GET sem parâmetros de query retornará especificações de conexão para todas as fontes disponíveis. Você pode incluir o query `property=name=="salesforce"` para obter informações especificamente para o Salesforce.

```http
GET /connectionSpecs
GET /connectionSpecs?property=name=="salesforce"
```

**Solicitação**

A solicitação a seguir recupera as especificações de conexão do Salesforce.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name==%22salesforce%22' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna as especificações de conexão do Salesforce, incluindo seu identificador exclusivo (`id`). Essa ID é necessária na próxima etapa para criar uma conexão básica.

```json
{
    "items": [
        {
            "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
            "name": "salesforce",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "authSpec": [
                {
                    "name": "Basic Authentication",
                    "type": "Basic_Authentication",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines auth params",
                        "properties": {
                            "environmentUrl": {
                                "type": "string",
                                "description": "URL of the source instance"
                            },
                            "username": {
                                "type": "string",
                                "description": "User name for the user account"
                            },
                            "password": {
                                "type": "string",
                                "description": "Password for the user account",
                                "format": "password"
                            },
                            "securityToken": {
                                "type": "string",
                                "description": "Security token for the user account",
                                "format": "password"
                            }
                        },
                        "required": [
                            "username",
                            "password",
                            "securityToken"
                        ]
                    }
                }
            ]
        }
    ]
}
```

## Criar uma conexão básica

Uma conexão básica especifica uma fonte e contém suas credenciais para essa fonte. Somente uma conexão básica é necessária por conta Salesforce, pois pode ser usada para criar vários conectores de origem para trazer dados diferentes.

Execute a seguinte solicitação POST para criar uma conexão básica.

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
        "name": "Salesforce Base Connection",
        "description": "Base connection for Salesforce account",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "username": "{USERNAME}",
                "password": "{PASSWORD}",
                "securityToken": "{SECURITY_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
            "version": "1.0"
        }
    }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `auth.params.username` | O nome de usuário associado à sua conta do Salesforce. |
| `auth.params.password` | A senha associada à sua conta do Salesforce. |
| `auth.params.securityToken` | O token de segurança associado à sua conta do Salesforce. |
| `connectionSpec.id` | A especificação de conexão `id` da sua conta Salesforce recuperada na etapa anterior. |

**Resposta**

Uma resposta bem-sucedida contém o identificador exclusivo (`id`) da conexão base. Essa ID é necessária para explorar seus dados no próximo tutorial.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700df7b-0000-0200-0000-5e3b424f0000\""
}
```

## Próximas etapas

Ao seguir este tutorial, você criou uma conexão básica para sua conta do Salesforce usando APIs e uma ID exclusiva foi obtida como parte do corpo da resposta. Você pode usar essa ID de conexão básica no próximo tutorial à medida que aprende a [explorar sistemas CRM usando a API](../../explore/crm.md)de Serviço de Fluxo.