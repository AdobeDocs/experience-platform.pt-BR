---
description: Esta página exemplifica a chamada à API usada para excluir um Adobe Experience Platform Destination SDK de configuração de credencial.
title: Excluir uma configuração de credencial
exl-id: a540e349-043c-4f04-8ca8-f650b9943492
source-git-commit: 560200a6553a1aae66c608eef7901b3248c886b4
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 1%

---

# Excluir uma configuração de credencial

>[!IMPORTANT]
>
>**Ponto de extremidade de API**: `platform.adobe.io/data/core/activation/authoring/credentials`

Esta página exemplifica a solicitação de API e a carga que você pode usar para excluir uma configuração de credencial usando o ponto de extremidade de API `/authoring/credentials`.

## Quando usar o ponto de extremidade de API `/credentials` {#when-to-use}

>[!IMPORTANT]
>
>Na maioria dos casos, você ***não*** precisa usar o ponto de extremidade de API `/credentials`. Em vez disso, você pode configurar as informações de autenticação para o seu destino através dos parâmetros `customerAuthenticationConfigurations` do ponto de extremidade `/destinations`.
> 
>Leia a [Configuração de autenticação do cliente](../functionality/destination-configuration/customer-authentication.md) para obter informações detalhadas sobre os tipos de autenticação com suporte.

Use este ponto de extremidade de API para criar uma configuração de credencial somente se houver um sistema de autenticação global entre o Adobe e a plataforma de destino, e o cliente do [!DNL Experience Platform] não precisar fornecer credenciais de autenticação para se conectar ao destino. Nesse caso, você deve criar uma configuração de credencial usando o ponto de extremidade da API `/credentials`.

Ao usar um sistema de autenticação global, você deve definir `"authenticationRule":"PLATFORM_AUTHENTICATION"` na configuração de [entrega de destino](../functionality/destination-configuration/destination-delivery.md), ao [criar uma nova configuração de destino](../authoring-api/destination-configuration/create-destination-configuration.md). Em seguida, você deve criar uma [configuração de credenciais](../credentials-api/create-credential-configuration.md) e passar a ID do objeto de credencial no parâmetro `authenticationId` na configuração de [entrega de destino](/help/destinations/destination-sdk/functionality/destination-configuration/destination-delivery.md#platform-authentication).

>[!IMPORTANT]
>
>Todos os nomes e valores de parâmetros com suporte do Destination SDK diferenciam maiúsculas de minúsculas **1&rbrace;.** Para evitar erros de diferenciação entre maiúsculas e minúsculas, use os nomes e valores dos parâmetros exatamente como mostrado na documentação.

## Introdução às operações de API de credenciais {#get-started}

Antes de continuar, consulte o [guia de introdução](../getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas com êxito para a API, incluindo como obter a permissão de criação de destino e os cabeçalhos necessários.

## Excluir uma configuração de credencial {#delete}

Você pode excluir uma configuração de credencial [existente](create-credential-configuration.md) fazendo uma solicitação `DELETE` para o ponto de extremidade `/authoring/credentials` com o `{INSTANCE_ID}`da configuração de credencial que deseja excluir.

Para obter uma configuração de destino existente e sua `{INSTANCE_ID}` correspondente, consulte o artigo sobre [recuperação de uma configuração de credencial](retrieve-credential-configuration.md).

**Formato da API**

```http
DELETE /authoring/credentials/{INSTANCE_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{INSTANCE_ID}` | O `ID` da configuração de credencial que você deseja excluir. |

A solicitação a seguir exclui uma configuração de credencial definida pelo parâmetro `{INSTANCE_ID}`.

+++Solicitação

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/credentials/{INSTANCE_ID} \
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

Os endpoints da API do Destination SDK seguem os princípios gerais de mensagem de erro da API do Experience Platform. Consulte [códigos de status da API](../../../landing/troubleshooting.md#api-status-codes) e [erros no cabeçalho da solicitação](../../../landing/troubleshooting.md#request-header-errors) no guia de solução de problemas do Experience Platform.

## Próximas etapas {#next-steps}

Depois de ler este documento, agora você sabe como excluir uma configuração de credencial usando o ponto de extremidade da API `/authoring/credentials`. Leia [como usar o Destination SDK para configurar seu destino](../guides/configure-destination-instructions.md) para entender onde essa etapa se encaixa no processo de configuração do seu destino.
