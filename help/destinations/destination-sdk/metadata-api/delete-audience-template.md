---
description: Esta página exemplifica a chamada da API usada para excluir um modelo de público-alvo existente por meio do Adobe Experience Platform Destination SDK.
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

Esta página exemplifica a solicitação da API e a carga útil que você pode usar para excluir um modelo de público-alvo, usando a variável `/authoring/audience-templates` Ponto de extremidade da API.

Para obter uma descrição detalhada dos recursos que podem ser configurados por meio desse terminal, consulte [gerenciamento de metadados do público-alvo](../functionality/audience-metadata-management.md).

>[!IMPORTANT]
>
>Todos os nomes de parâmetros e valores suportados pelo Destination SDK são **distinção entre maiúsculas e minúsculas**. Para evitar erros de diferenciação entre maiúsculas e minúsculas, use os nomes e valores dos parâmetros exatamente como mostrado na documentação.

## Introdução às operações da API do modelo de público-alvo {#get-started}

Antes de continuar, reveja o [guia de introdução](../getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas para a API com sucesso, incluindo como obter a permissão de criação de destino necessária e os cabeçalhos necessários.

## Excluir um modelo de público-alvo {#delete}

Você pode excluir um [existente](create-audience-template.md) modelo de público-alvo criando um `DELETE` à `/authoring/audience-templates` endpoint com `{INSTANCE_ID}`do modelo de público que deseja excluir.

Para obter um modelo de público-alvo existente e o correspondente `{INSTANCE_ID}`, consulte o artigo sobre [recuperar um template de público](retrieve-audience-template.md).

**Formato da API**

```http
DELETE /authoring/audience-templates/{INSTANCE_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{INSTANCE_ID}` | O `ID` do modelo de público-alvo que deseja excluir. |

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

Uma resposta bem-sucedida retorna o status HTTP 200 junto com uma resposta HTTP vazia.

+++

## Tratamento de erros da API {#error-handling}

Os pontos de extremidade da API do Destination SDK seguem os princípios gerais da mensagem de erro da API do Experience Platform. Consulte [Códigos de status da API](../../../landing/troubleshooting.md#api-status-codes) e [erros do cabeçalho da solicitação](../../../landing/troubleshooting.md#request-header-errors) no guia de solução de problemas da plataforma.

## Próximas etapas {#next-steps}

Depois de ler este documento, você agora sabe como excluir um modelo de público-alvo usando o `/authoring/audience-templates` Ponto de extremidade da API. Ler [como usar o Destination SDK para configurar seu destino](../guides/configure-destination-instructions.md) para entender onde essa etapa se encaixa no processo de configuração do seu destino.
