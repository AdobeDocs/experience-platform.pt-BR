---
description: Esta página exemplifica a chamada à API usada para excluir um modelo de público-alvo existente por meio do Adobe Experience Platform Destination SDK.
title: Excluir um modelo de público-alvo
exl-id: 6eb07e3c-3269-4368-9b11-04bd993cc4ab
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 2%

---

# Excluir um modelo de público-alvo

>[!IMPORTANT]
>
>**Ponto de extremidade de API**: `platform.adobe.io/data/core/activation/authoring/audience-templates`

Esta página exemplifica a solicitação de API e a carga que você pode usar para excluir um modelo de público-alvo, usando o ponto de extremidade de API `/authoring/audience-templates`.

Para obter uma descrição detalhada dos recursos que você pode configurar por meio deste ponto de extremidade, consulte [gerenciamento de metadados de público-alvo](../functionality/audience-metadata-management.md).

>[!IMPORTANT]
>
>Todos os nomes e valores de parâmetros suportados pelo Destination SDK fazem **distinção entre maiúsculas e minúsculas**. Para evitar erros de diferenciação entre maiúsculas e minúsculas, use os nomes e valores dos parâmetros exatamente como mostrado na documentação.

## Introdução às operações de API do modelo de público-alvo {#get-started}

Antes de continuar, consulte o [guia de introdução](../getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas com êxito para a API, incluindo como obter a permissão de criação de destino e os cabeçalhos necessários.

## Excluir um modelo de público-alvo {#delete}

Você pode excluir um modelo de público-alvo [existente](create-audience-template.md) fazendo uma solicitação `DELETE` para o ponto de extremidade `/authoring/audience-templates` com o `{INSTANCE_ID}`do modelo de público-alvo que deseja excluir.

Para obter um modelo de público-alvo existente e seu `{INSTANCE_ID}` correspondente, consulte o artigo sobre [recuperação de um modelo de público-alvo](retrieve-audience-template.md).

**Formato da API**

```http
DELETE /authoring/audience-templates/{INSTANCE_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{INSTANCE_ID}` | O `ID` do modelo de público-alvo que você deseja excluir. |

+++Solicitação

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/audience-templates/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++Resposta

Uma resposta bem-sucedida retorna o status HTTP 200 juntamente com uma resposta HTTP vazia.

+++

## Manipulação de erros de API {#error-handling}

Os endpoints da API Destination SDK seguem os princípios gerais de mensagem de erro da API Experience Platform. Consulte [códigos de status da API](../../../landing/troubleshooting.md#api-status-codes) e [erros no cabeçalho da solicitação](../../../landing/troubleshooting.md#request-header-errors) no guia de solução de problemas da Platform.

## Próximas etapas {#next-steps}

Depois de ler este documento, agora você sabe como excluir um modelo de público-alvo usando o ponto de extremidade da API `/authoring/audience-templates`. Leia [como usar o Destination SDK para configurar seu destino](../guides/configure-destination-instructions.md) para entender onde esta etapa se encaixa no processo de configuração do seu destino.
