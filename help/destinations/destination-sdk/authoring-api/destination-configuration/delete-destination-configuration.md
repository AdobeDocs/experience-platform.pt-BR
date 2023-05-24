---
description: Esta página exemplifica a chamada à API usada para excluir uma configuração de destino existente por meio do Adobe Experience Platform Destination SDK.
title: Excluir uma configuração de destino
source-git-commit: acb7075f49b4194c31371d2de63709eea7821329
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 3%

---


# Excluir uma configuração de destino

Esta página exemplifica a solicitação de API e a carga que você pode usar para excluir uma configuração de destino existente, usando o `/authoring/destinations` Endpoint da API.

>[!IMPORTANT]
>
>Todos os nomes e valores de parâmetros compatíveis com o Destination SDK são **diferencia maiúsculas de minúsculas**. Para evitar erros de diferenciação entre maiúsculas e minúsculas, use os nomes e valores dos parâmetros exatamente como mostrado na documentação.

## Introdução às operações de API de configuração de destino {#get-started}

Antes de continuar, reveja o [guia de introdução](../../getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas com êxito para a API, incluindo como obter a permissão de criação de destino e os cabeçalhos necessários.

## Excluir uma configuração de destino {#delete}

É possível excluir um [existente](create-destination-configuration.md) configuração do servidor de destino fazendo uma `DELETE` solicitação à `/authoring/destinations` terminal com o `{INSTANCE_ID}`da configuração de destino que você deseja excluir.

>[!TIP]
>
>**Ponto de acesso da API**: `platform.adobe.io/data/core/activation/authoring/destinations`

Para obter uma configuração de destino existente e suas configurações `{INSTANCE_ID}`, consulte o artigo sobre [recuperação de uma configuração de destino](retrieve-destination-configuration.md).

**Formato da API**

```http
DELETE /authoring/destinations/{INSTANCE_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{INSTANCE_ID}` | A variável `ID` da configuração de destino que você deseja excluir. |

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

Os endpoints da API Destination SDK seguem os princípios gerais de mensagem de erro da API Experience Platform. Consulte [Códigos de status da API](../../../../landing/troubleshooting.md#api-status-codes) e [erros no cabeçalho da solicitação](../../../../landing/troubleshooting.md#request-header-errors) no guia de solução de problemas da Platform.

## Próximas etapas

Depois de ler este documento, agora você sabe como excluir uma configuração de destino existente por meio do Destination SDK `/authoring/destinations` Endpoint da API.

Para saber mais sobre o que você pode fazer com esse endpoint, consulte os seguintes artigos:

* [Criar uma configuração de destino](create-destination-configuration.md)
* [Recuperar uma configuração de destino](retrieve-destination-configuration.md)
* [Atualizar uma configuração de destino](update-destination-configuration.md)

