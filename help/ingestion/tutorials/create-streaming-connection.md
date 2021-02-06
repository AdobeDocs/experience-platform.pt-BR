---
keywords: Experience Platform;home;popular topics;conexão de transmissão;criar conexão de transmissão;guia de API;tutorial;criar uma conexão de transmissão;ingestão de transmissão;;home;popular topics;streaming connection;create streaming connection;api guide;tutorial;create a streaming connection;streaming ingestion;ingestão;ingestão;
solution: Experience Platform
title: Criar uma conexão de fluxo usando a API
topic: tutorial
type: Tutorial
description: Este tutorial o ajudará a começar a usar APIs de ingestão de streaming, parte das APIs do Adobe Experience Platform Data Ingestion Service.
translation-type: tm+mt
source-git-commit: 089a4d517476b614521d1db4718966e3ebb13064
workflow-type: tm+mt
source-wordcount: '677'
ht-degree: 2%

---


# Criação de uma conexão de streaming usando a API

Este tutorial o ajudará a começar a usar APIs de ingestão de streaming, parte das APIs de [!DNL Ingestion Service] Dados da Adobe Experience Platform.

## Introdução

O registro de conexão de transmissão contínua é necessário para que os dados de transmissão de start para a Adobe Experience Platform sejam transmitidos. Ao registrar uma conexão de streaming, é necessário fornecer alguns detalhes principais, como a fonte de dados de streaming.

Depois de registrar uma conexão de streaming, você, como produtor de dados, terá um URL exclusivo que pode ser usado para transmitir dados para a Plataforma.

Este tutorial também requer um conhecimento prático de vários serviços da Adobe Experience Platform. Antes de iniciar este tutorial, reveja a documentação dos seguintes serviços:

- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): O quadro normalizado através do qual  [!DNL Platform] organiza os dados da experiência.
- [[!DNL Real-time Customer Profile]](../../profile/home.md): Fornece um perfil unificado e de consumidor em tempo real, com base em dados agregados de várias fontes.

As seções a seguir fornecem informações adicionais que você precisará saber para fazer chamadas com êxito para as APIs de ingestão de streaming.

### Lendo chamadas de exemplo da API

Este guia fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção em [como ler chamadas de API de exemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas [!DNL Experience Platform].

### Reunir valores para cabeçalhos necessários

Para fazer chamadas para [!DNL Platform] APIs, você deve primeiro concluir o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API [!DNL Experience Platform], como mostrado abaixo:

- Autorização: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos em [!DNL Experience Platform] são isolados para caixas de proteção virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifique o nome da caixa de proteção em que a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre caixas de proteção em [!DNL Platform], consulte a [documentação de visão geral da caixa de proteção](../../sandboxes/home.md).

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho adicional:

- Tipo de conteúdo: application/json

## Criar uma conexão

Uma conexão especifica a fonte e contém as informações necessárias para tornar o fluxo compatível com as APIs de ingestão de streaming.

**Formato da API**

```http
POST /flowservice/connections
```

**Solicitação**

>[!NOTE]
>
>Os valores para as `providerId` listadas e `connectionSpec` **devem** ser usados conforme mostrado no exemplo, pois são o que especifica para a API que você está criando uma conexão de streaming para a assimilação de streaming.

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "name": "Sample name",
     "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
     "description": "Sample description",
     "connectionSpec": {
         "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
         "version": "1.0"
     },
     "auth": {
         "specName": "Streaming Connection",
         "params": {
             "sourceId": "Sample connection",
             "dataType": "xdm",
             "name": "Sample connection"
         }
     }
 }
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 201 com detalhes da conexão recém-criada.

```json
{
    "id": "77a05521-91d6-451c-a055-2191d6851c34",
    "etag": "\"a500e689-0000-0200-0000-5e31df730000\""
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `id` | O `id` da conexão recém-criada. Isso será chamado de `{CONNECTION_ID}`. |
| `etag` | Um identificador atribuído à conexão, especificando a revisão da conexão. |

## Obter URL de coleta de dados

Com a conexão criada, agora é possível recuperar o URL da coleção de dados.

**Formato da API**

```http
GET /flowservice/connections/{CONNECTION_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{CONNECTION_ID}` | O valor `id` da conexão criada anteriormente. |

**Solicitação**

```shell
curl -X GET https://platform.adobe.io/data/foundation/flowservice/connections/{CONNECTION_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com informações detalhadas sobre a conexão solicitada. O URL da coleta de dados é criado automaticamente com a conexão e pode ser recuperado usando o valor `inletUrl`.

```json
{
    "items": [
        {
            "createdAt": 1583971856947,
            "updatedAt": 1583971856947,
            "createdBy": "{API_KEY}",
            "updatedBy": "{API_KEY}",
            "createdClient": "{USER_ID}",
            "updatedClient": "{USER_ID}",
            "id": "77a05521-91d6-451c-a055-2191d6851c34",
            "name": "Another new sample connection (Experience Event)",
            "description": "Sample description",
            "connectionSpec": {
                "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
                "version": "1.0"
            },
            "state": "enabled",
            "auth": {
                "specName": "Streaming Connection",
                "params": {
                    "sourceId": "Sample connection (ExperienceEvent)",
                    "inletUrl": "https://dcs.adobedc.net/collection/a868e1ce678a911ef1482b083329af3cafa4bafdc781285f25911eaae9e00eb2",
                    "inletId": "a868e1ce678a911ef1482b083329af3cafa4bafdc781285f25911eaae9e00eb2",
                    "dataType": "xdm",
                    "name": "Sample connection (ExperienceEvent)"
                }
            },
            "version": "\"56008aee-0000-0200-0000-5e697e150000\"",
            "etag": "\"56008aee-0000-0200-0000-5e697e150000\""
        }
    ]
}
```

## Próximas etapas

Agora que você criou uma conexão de streaming, é possível fazer streaming de séries de tempo ou dados de registro, permitindo que você ingira dados em [!DNL Platform]. Para saber como transmitir dados de séries de tempo para [!DNL Platform], acesse [tutorial de dados de séries de tempo de transmissão](./streaming-time-series-data.md). Para saber como transmitir dados de registro em [!DNL Platform], acesse o [tutorial de dados de registro de transmissão](./streaming-record-data.md).

## Apêndice

Esta seção fornece informações complementares sobre a criação de conexões de fluxo contínuo usando a API.

### Conexões de streaming autenticadas

A coleta de dados autenticada permite que os serviços da Adobe Experience Platform, como [!DNL Real-time Customer Profile] e [!DNL Identity], diferenciem entre registros provenientes de fontes confiáveis e fontes não confiáveis. Os clientes que desejam enviar informações pessoais identificáveis (PII) podem fazê-lo enviando Tokens de acesso IMS como parte da solicitação de POST - se o token IMS for válido, os registros serão marcados como coletados de fontes confiáveis.

Para obter mais informações sobre como criar uma conexão de streaming autenticada, consulte o tutorial [criar uma conexão de streaming autenticada](create-authenticated-streaming-connection.md).