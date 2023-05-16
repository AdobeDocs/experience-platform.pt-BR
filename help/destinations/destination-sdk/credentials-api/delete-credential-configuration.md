---
description: Esta página exemplifica a chamada da API usada para excluir um Adobe Experience Platform Destination SDK de configuração de credencial.
title: Excluir uma configuração de credencial
source-git-commit: 9e1ae44f83b886f0b5dd5a9fc9cd9b7db6154ff0
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 2%

---


# Excluir uma configuração de credencial

>[!IMPORTANT]
>
>**Ponto de acesso da API**: `platform.adobe.io/data/core/activation/authoring/credentials`

Esta página exemplifica a solicitação da API e a carga útil que você pode usar para excluir uma configuração de credencial usando o `/authoring/credentials` Ponto de extremidade da API.

## Quando usar a variável `/credentials` Ponto de extremidade da API {#when-to-use}

>[!IMPORTANT]
>
>Na maioria dos casos, você ***não*** precisam usar o `/credentials` Ponto de extremidade da API. Em vez disso, você pode configurar as informações de autenticação para o seu destino por meio do `customerAuthenticationConfigurations` parâmetros da `/destinations` endpoint .
> 
>Ler [Configuração de autenticação do cliente](../functionality/destination-configuration/customer-authentication.md) para obter informações detalhadas sobre os tipos de autenticação suportados.

Use esse ponto de extremidade de API para criar uma configuração de credencial somente se houver um sistema de autenticação global entre o Adobe e a plataforma de destino, e [!DNL Platform] o cliente não precisa fornecer credenciais de autenticação para se conectar ao seu destino. Nesse caso, você deve criar uma configuração de credencial usando o `/credentials` Ponto de extremidade da API.

Ao usar um sistema de autenticação global, você deve definir `"authenticationRule":"PLATFORM_AUTHENTICATION"` no [entrega de destino](../functionality/destination-configuration/destination-delivery.md) configuração, quando [criação de uma nova configuração de destino](../authoring-api/destination-configuration/create-destination-configuration.md).

>[!IMPORTANT]
>
>Todos os nomes de parâmetros e valores suportados pelo Destination SDK são **distinção entre maiúsculas e minúsculas**. Para evitar erros de diferenciação entre maiúsculas e minúsculas, use os nomes e valores dos parâmetros exatamente como mostrado na documentação.

## Introdução às operações da API de credenciais {#get-started}

Antes de continuar, reveja o [guia de introdução](../getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas para a API com sucesso, incluindo como obter a permissão de criação de destino necessária e os cabeçalhos necessários.

## Excluir uma configuração de credencial {#delete}

Você pode excluir um [existente](create-credential-configuration.md) configuração de credencial ao criar uma `DELETE` à `/authoring/credentials` endpoint com `{INSTANCE_ID}`da configuração de credencial que deseja excluir.

Para obter uma configuração de destino existente e sua correspondente `{INSTANCE_ID}`, consulte o artigo sobre [recuperar uma configuração de credencial](retrieve-credential-configuration.md).

**Formato da API**

```http
DELETE /authoring/credentials/{INSTANCE_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{INSTANCE_ID}` | O `ID` da configuração de credencial que deseja excluir. |

A solicitação a seguir exclui uma configuração de credencial definida pelo `{INSTANCE_ID}` parâmetro.

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

Uma resposta bem-sucedida retorna o status HTTP 200 junto com uma resposta HTTP vazia.

+++

## Tratamento de erros da API {#error-handling}

Os pontos de extremidade da API do Destination SDK seguem os princípios gerais da mensagem de erro da API do Experience Platform. Consulte [Códigos de status da API](../../../landing/troubleshooting.md#api-status-codes) e [erros do cabeçalho da solicitação](../../../landing/troubleshooting.md#request-header-errors) no guia de solução de problemas da plataforma.

## Próximas etapas {#next-steps}

Depois de ler este documento, agora você sabe como excluir uma configuração de credencial usando o `/authoring/credentials` Ponto de extremidade da API. Ler [como usar o Destination SDK para configurar seu destino](../guides/configure-destination-instructions.md) para entender onde essa etapa se encaixa no processo de configuração do seu destino.
