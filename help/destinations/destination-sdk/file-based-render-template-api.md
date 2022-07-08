---
description: Esta página explica como usar o endpoint /authoring/testing/template/render para visualizar como seriam os campos de dados do cliente modelos definidos na configuração de destino.
title: Validar campos de clientes modelos
source-git-commit: fa092e4d1828d9ecd5bc98e3f225fa377f38065f
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 3%

---


# Validar campos de clientes modelos

## Visão geral {#overview}

O `/authoring/testing/template/render` endpoint ajuda a visualizar como o modelo [campos de dados do cliente](file-based-destination-configuration.md#customer-data-fields) definido na configuração de destino, seria parecido.

O endpoint gera valores aleatórios para os campos de dados do cliente e os retorna na resposta. Isso ajuda a validar a estrutura semântica dos campos de dados do cliente, como nomes de bucket ou caminhos de pasta.

## Introdução {#getting-started}

Antes de continuar, reveja o [guia de introdução](./getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas para a API com sucesso, incluindo como obter a permissão de criação de destino necessária e os cabeçalhos necessários.

## Pré-requisitos {#prerequisites}

Antes de usar a variável `/template/render` , certifique-se de atender às seguintes condições:

* Você tem um destino com base em arquivo existente criado por meio do Destination SDK e pode vê-lo em seu [catálogo de destinos](../ui/destinations-workspace.md).
* Para fazer a solicitação da API com êxito, é necessário a ID da instância de destino correspondente à instância de destino que você testará. Obtenha a ID da instância de destino que você deve usar na chamada da API, do URL, ao navegar em uma conexão com seu destino na interface do usuário da plataforma.

   ![Imagem da interface do usuário que mostra como obter a ID da instância de destino do URL.](assets/get-destination-instance-id.png)

## Renderizar campos de clientes modelos {#render-customer-fields}

**Formato da API**

```http
POST /authoring/testing/template/render/destination
```

Para ilustrar o comportamento desse ponto de extremidade de API, considere um destino baseado em arquivo com a seguinte configuração de campos de dados do cliente:

```json
"fileBasedS3Destination":{
   "bucket":{
      "templatingStrategy":"PEBBLE_V1",
      "value":"{{customerData.bucket}}"
   },
   "path":{
      "templatingStrategy":"PEBBLE_V1",
      "value":"{{customerData.path}}"
   }
}
```

**Solicitação**

A solicitação abaixo chama a função `/authoring/testing/template/render` endpoint, que retorna uma resposta com valores gerados aleatoriamente para os dois campos de dados do cliente mencionados acima.

```shell
curl -X POST 'https://platform.adobe.io/data/core/activation/authoring/testing/template/render/destination' \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
 {
    "destinationId": "{DESTINATION_CONFIGURATION_ID}",
    "templates": {
        "bucket": "{{customerData.bucket}}",
        "path": "{{customerData.bucket}}/{{customerData.path}}"
    }
}'
```

| Parâmetros | Descrição |
| -------- | ----------- |
| `destinationId` | A ID do [configuração de destino](file-based-destination-configuration.md) que você está testando. |
| `templates` | Os nomes de campo modelos definidos em [configuração do servidor de destino](server-and-file-configuration.md). |

**Resposta**

Uma resposta bem-sucedida retorna um `HTTP 200 OK` e o corpo inclui valores gerados aleatoriamente para seus campos modelos.

Essa resposta tem como objetivo ajudar você a validar a estrutura correta dos campos de dados do cliente, como nomes de bucket ou caminhos de pasta.


```json
{
    "results": {
        "bucket": "hfWpE-bucket",
        "path": "hfWpE-bucket/ceC"
    }
}
```

## Tratamento de erros da API {#api-error-handling}

Os pontos de extremidade da API do Destination SDK seguem os princípios gerais da mensagem de erro da API do Experience Platform. Consulte [Códigos de status da API](../../landing/troubleshooting.md#api-status-codes) e [erros do cabeçalho da solicitação](../../landing/troubleshooting.md#request-header-errors) no guia de solução de problemas da plataforma.

## Próximas etapas {#next-steps}

Depois de ler este documento, você agora sabe como validar a configuração do campo de dados do cliente definida em [servidor de destino](server-and-file-configuration.md).
