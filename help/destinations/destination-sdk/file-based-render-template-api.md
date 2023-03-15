---
description: Esta página explica como usar o endpoint /authoring/testing/template/render para visualizar como seriam os campos de dados de clientes modelados definidos na configuração de destino.
title: Validar campos de cliente modelados
exl-id: 8ed93f0c-3439-4d11-bb2f-d417a1e0b6a8
source-git-commit: 44e056407f5089c927752f00cc6bf173d7640b83
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 3%

---

# Validar campos de cliente modelados

## Visão geral {#overview}

A variável `/authoring/testing/template/render` O endpoint ajuda a visualizar como o modelo foi [campos de dados do cliente](file-based-destination-configuration.md#customer-data-fields) definido na configuração de destino seria semelhante a.

O endpoint gera valores aleatórios para os campos de dados do cliente e os retorna na resposta. Isso ajuda a validar a estrutura semântica dos campos de dados do cliente, como nomes de buckets ou caminhos de pastas.

## Introdução {#getting-started}

Antes de continuar, reveja o [guia de introdução](./getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas com êxito para a API, incluindo como obter a permissão de criação de destino e os cabeçalhos necessários.

## Pré-requisitos {#prerequisites}

Antes de poder usar o `/template/render` verifique se você atende às seguintes condições:

* Você tem um destino baseado em arquivo existente criado por meio do Destination SDK e pode visualizá-lo em seu [catálogo de destinos](../ui/destinations-workspace.md).
* Para fazer a solicitação de API com êxito, é necessário ter a ID da instância de destino correspondente à instância de destino que você testará. Obtenha a ID da instância de destino que você deve usar na chamada da API, no URL, ao navegar por uma conexão com seu destino na interface do Platform.

   ![Imagem da interface mostrando como obter a ID da instância de destino do URL.](assets/get-destination-instance-id.png)

## Renderizar campos de cliente modelados {#render-customer-fields}

**Formato da API**

```http
POST /authoring/testing/template/render/destination
```

Para ilustrar o comportamento desse endpoint de API, vamos considerar um destino baseado em arquivo com a seguinte configuração de campos de dados do cliente:

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

A solicitação abaixo chama a `/authoring/testing/template/render` endpoint, que retorna uma resposta com valores gerados aleatoriamente para os dois campos de dados do cliente mencionados acima.

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
| `templates` | Os nomes de campos com modelos definidos no [configuração do servidor de destino](server-and-file-configuration.md). |

**Resposta**

Uma resposta bem-sucedida retorna uma `HTTP 200 OK` e o corpo inclui valores gerados aleatoriamente para seus campos de modelo.

Essa resposta pode ajudar a validar a estrutura correta dos campos de dados do cliente, como nomes de buckets ou caminhos de pastas.


```json
{
    "results": {
        "bucket": "hfWpE-bucket",
        "path": "hfWpE-bucket/ceC"
    }
}
```

## Manipulação de erros de API {#api-error-handling}

Os endpoints da API Destination SDK seguem os princípios gerais de mensagem de erro da API Experience Platform. Consulte [Códigos de status da API](../../landing/troubleshooting.md#api-status-codes) e [erros no cabeçalho da solicitação](../../landing/troubleshooting.md#request-header-errors) no guia de solução de problemas da Platform.

## Próximas etapas {#next-steps}

Depois de ler este documento, agora você sabe como validar a configuração do campo de dados do cliente definida em seu [servidor de destino](server-and-file-configuration.md).
