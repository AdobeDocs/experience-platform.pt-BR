---
description: Esta página exemplifica a chamada à API usada para excluir uma configuração existente do servidor de destino por meio do Adobe Experience Platform Destination SDK.
title: Excluir uma configuração do servidor de destino
exl-id: 2322a2ce-220e-4590-a553-b15152412752
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 1%

---

# Excluir uma configuração do servidor de destino

Esta página exemplifica a solicitação de API e a carga que você pode usar para excluir uma configuração existente do servidor de destino, usando o ponto de extremidade da API `/authoring/destination-servers`.

Para obter uma descrição detalhada dos recursos que você pode excluir por meio desse endpoint, leia os seguintes artigos:

* [Especificações do servidor para destinos criados com o Destination SDK](../../../destination-sdk/functionality/destination-server/server-specs.md)
* [Especificações de modelos para destinos criados com o Destination SDK](../../../destination-sdk/functionality/destination-server/templating-specs.md)
* [Formato da mensagem](../../../destination-sdk/functionality/destination-server/message-format.md)
* [Configuração da formatação de arquivo](../../../destination-sdk/functionality/destination-server/file-formatting.md)

>[!IMPORTANT]
>
>Todos os nomes e valores de parâmetros suportados pelo Destination SDK fazem **distinção entre maiúsculas e minúsculas**. Para evitar erros de diferenciação entre maiúsculas e minúsculas, use os nomes e valores dos parâmetros exatamente como mostrado na documentação.

## Introdução às operações de API do servidor de destino {#get-started}

Antes de continuar, consulte o [guia de introdução](../../getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas com êxito para a API, incluindo como obter a permissão de criação de destino e os cabeçalhos necessários.

## Excluir uma configuração do servidor de destino {#delete}

Você pode excluir uma configuração de servidor de destino [existente](create-destination-server.md) fazendo uma solicitação `DELETE` para o ponto de extremidade `/authoring/destination-servers` com o `{INSTANCE_ID}`da configuração de servidor de destino que deseja excluir.

>[!TIP]
>
>**Ponto de extremidade de API**: `platform.adobe.io/data/core/activation/authoring/destination-servers`

Para obter uma configuração existente do servidor de destino e seu `{INSTANCE_ID}` correspondente, consulte o artigo sobre [recuperação de uma configuração do servidor de destino](retrieve-destination-server.md).

**Formato da API**

```http
DELETE /authoring/destination-servers/{INSTANCE_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{INSTANCE_ID}` | O `ID` da configuração do servidor de destino que você deseja excluir. |

+++Solicitação

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/destination-servers/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++Resposta

Uma resposta bem-sucedida retorna o status HTTP 200 juntamente com uma resposta HTTP vazia.

## Manipulação de erros de API {#error-handling}

Os endpoints da API Destination SDK seguem os princípios gerais de mensagem de erro da API Experience Platform. Consulte [códigos de status da API](../../../../landing/troubleshooting.md#api-status-codes) e [erros no cabeçalho da solicitação](../../../../landing/troubleshooting.md#request-header-errors) no guia de solução de problemas da Platform.

## Próximas etapas {#next-steps}

Depois de ler este documento, agora você sabe como excluir um servidor de destino existente por meio do ponto de extremidade da API do Destination SDK `/authoring/destination-servers`.

Para saber mais sobre o que você pode fazer com esse endpoint, consulte os seguintes artigos:

* [Criar uma configuração do servidor de destino](create-destination-server.md)
* [Recuperar uma configuração do servidor de destino](retrieve-destination-server.md)
* [Atualizar uma configuração do servidor de destino](update-destination-server.md)
