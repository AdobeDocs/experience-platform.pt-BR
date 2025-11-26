---
description: Esta página exemplifica a chamada à API usada para excluir uma configuração de destino existente por meio do Adobe Experience Platform Destination SDK.
title: Excluir uma configuração de destino
exl-id: c7309ab7-1b8d-46d4-8017-fd4aa5918cdd
source-git-commit: fda542e62c448788099d63951277278a146fdfc8
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 2%

---

# Excluir uma configuração de destino

Esta página exemplifica a solicitação de API e a carga que você pode usar para excluir uma configuração de destino existente, usando o ponto de extremidade de API `/authoring/destinations`.

>[!IMPORTANT]
>
>Todos os nomes e valores de parâmetros com suporte do Destination SDK diferenciam maiúsculas de minúsculas **1}.** Para evitar erros de diferenciação entre maiúsculas e minúsculas, use os nomes e valores dos parâmetros exatamente como mostrado na documentação.

## Introdução às operações de API de configuração de destino {#get-started}

Antes de continuar, consulte o [guia de introdução](../../getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas com êxito para a API, incluindo como obter a permissão de criação de destino e os cabeçalhos necessários.

## Excluir uma configuração de destino {#delete}

Você pode excluir uma configuração de destino [existente](create-destination-configuration.md) fazendo uma solicitação `DELETE` para o ponto de extremidade `/authoring/destinations` com o `{INSTANCE_ID}`da configuração de destino que deseja excluir.

>[!TIP]
>
>**Ponto de extremidade de API**: `platform.adobe.io/data/core/activation/authoring/destinations`

Para obter uma configuração de destino existente e sua `{INSTANCE_ID}` correspondente, consulte o artigo sobre [recuperação de uma configuração de destino](retrieve-destination-configuration.md).

**Formato da API**

```http
DELETE /authoring/destinations/{INSTANCE_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{INSTANCE_ID}` | O `ID` da configuração de destino que você deseja excluir. |

+++Solicitação

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/destinations/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++Resposta

Uma resposta bem-sucedida retorna o status HTTP 200 juntamente com uma resposta HTTP vazia.


## Manipulação de erros de API {#error-handling}

Os endpoints da API do Destination SDK seguem os princípios gerais de mensagem de erro da API do Experience Platform. Consulte [códigos de status da API](../../../../landing/troubleshooting.md#api-status-codes) e [erros no cabeçalho da solicitação](../../../../landing/troubleshooting.md#request-header-errors) no guia de solução de problemas do Experience Platform.

## Próximas etapas

Depois de ler este documento, agora você sabe como excluir uma configuração de destino existente por meio do ponto de extremidade da API `/authoring/destinations` do Destination SDK.

Para saber mais sobre o que você pode fazer com esse endpoint, consulte os seguintes artigos:

* [Criar uma configuração de destino](create-destination-configuration.md)
* [Recuperar uma configuração de destino](retrieve-destination-configuration.md)
* [Atualizar uma configuração de destino](update-destination-configuration.md)
