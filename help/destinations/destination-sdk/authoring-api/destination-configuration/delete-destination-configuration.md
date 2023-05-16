---
description: Esta página exemplifica a chamada da API usada para excluir uma configuração de destino existente por meio do Adobe Experience Platform Destination SDK.
title: Excluir uma configuração de destino
source-git-commit: acb7075f49b4194c31371d2de63709eea7821329
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 3%

---


# Excluir uma configuração de destino

Esta página exemplifica a solicitação da API e a carga útil que você pode usar para excluir uma configuração de destino existente, usando o `/authoring/destinations` Ponto de extremidade da API.

>[!IMPORTANT]
>
>Todos os nomes de parâmetros e valores suportados pelo Destination SDK são **distinção entre maiúsculas e minúsculas**. Para evitar erros de diferenciação entre maiúsculas e minúsculas, use os nomes e valores dos parâmetros exatamente como mostrado na documentação.

## Introdução às operações da API de configuração de destino {#get-started}

Antes de continuar, reveja o [guia de introdução](../../getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas para a API com sucesso, incluindo como obter a permissão de criação de destino necessária e os cabeçalhos necessários.

## Excluir uma configuração de destino {#delete}

Você pode excluir um [existente](create-destination-configuration.md) configuração do servidor de destino fazendo uma `DELETE` à `/authoring/destinations` endpoint com `{INSTANCE_ID}`da configuração de destino que deseja excluir.

>[!TIP]
>
>**Ponto de acesso da API**: `platform.adobe.io/data/core/activation/authoring/destinations`

Para obter uma configuração de destino existente e sua correspondente `{INSTANCE_ID}`, consulte o artigo sobre [recuperar uma configuração de destino](retrieve-destination-configuration.md).

**Formato da API**

```http
DELETE /authoring/destinations/{INSTANCE_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{INSTANCE_ID}` | O `ID` da configuração de destino que deseja excluir. |

+++Solicitação

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/destinations/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++Resposta

Uma resposta bem-sucedida retorna o status HTTP 200 junto com uma resposta HTTP vazia.


## Tratamento de erros da API {#error-handling}

Os pontos de extremidade da API do Destination SDK seguem os princípios gerais da mensagem de erro da API do Experience Platform. Consulte [Códigos de status da API](../../../../landing/troubleshooting.md#api-status-codes) e [erros do cabeçalho da solicitação](../../../../landing/troubleshooting.md#request-header-errors) no guia de solução de problemas da plataforma.

## Próximas etapas

Depois de ler este documento, agora você sabe como excluir uma configuração de destino existente por meio do Destination SDK `/authoring/destinations` Ponto de extremidade da API.

Para saber mais sobre o que você pode fazer com esse terminal, consulte os seguintes artigos:

* [Criar uma configuração de destino](create-destination-configuration.md)
* [Recuperar uma configuração de destino](retrieve-destination-configuration.md)
* [Atualizar uma configuração de destino](update-destination-configuration.md)

