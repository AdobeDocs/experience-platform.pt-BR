---
description: Esta página exemplifica a chamada à API usada para excluir um modelo de público-alvo existente por meio do Adobe Experience Platform Destination SDK.
title: Excluir um modelo de público-alvo
source-git-commit: 9e1ae44f83b886f0b5dd5a9fc9cd9b7db6154ff0
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 3%

---


# Excluir um modelo de público-alvo

>[!IMPORTANT]
>
>**Ponto de acesso da API**: `platform.adobe.io/data/core/activation/authoring/audience-templates`

Esta página exemplifica a solicitação de API e a carga que você pode usar para excluir um modelo de público-alvo usando o `/authoring/audience-templates` Endpoint da API.

Para obter uma descrição detalhada dos recursos que você pode configurar por meio desse endpoint, consulte [gerenciamento de metadados de público](../functionality/audience-metadata-management.md).

>[!IMPORTANT]
>
>Todos os nomes e valores de parâmetros compatíveis com o Destination SDK são **diferencia maiúsculas de minúsculas**. Para evitar erros de diferenciação entre maiúsculas e minúsculas, use os nomes e valores dos parâmetros exatamente como mostrado na documentação.

## Introdução às operações de API do modelo de público-alvo {#get-started}

Antes de continuar, reveja o [guia de introdução](../getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas com êxito para a API, incluindo como obter a permissão de criação de destino e os cabeçalhos necessários.

## Excluir um modelo de público-alvo {#delete}

É possível excluir um [existente](create-audience-template.md) modelo de público fazendo um `DELETE` solicitação à `/authoring/audience-templates` terminal com o `{INSTANCE_ID}`do modelo de público-alvo que você deseja excluir.

Para obter um template de público-alvo existente e seu correspondente `{INSTANCE_ID}`, consulte o artigo sobre [recuperação de um template de público](retrieve-audience-template.md).

**Formato da API**

```http
DELETE /authoring/audience-templates/{INSTANCE_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{INSTANCE_ID}` | A variável `ID` do modelo de público-alvo que você deseja excluir. |

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

Os endpoints da API Destination SDK seguem os princípios gerais de mensagem de erro da API Experience Platform. Consulte [Códigos de status da API](../../../landing/troubleshooting.md#api-status-codes) e [erros no cabeçalho da solicitação](../../../landing/troubleshooting.md#request-header-errors) no guia de solução de problemas da Platform.

## Próximas etapas {#next-steps}

Depois de ler este documento, agora você sabe como excluir um modelo de público-alvo usando o `/authoring/audience-templates` Endpoint da API. Ler [como usar o Destination SDK para configurar seu destino](../guides/configure-destination-instructions.md) para entender onde essa etapa se encaixa no processo de configuração do destino.
