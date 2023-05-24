---
description: Esta página exemplifica a chamada à API usada para excluir uma Adobe Experience Platform Destination SDK de configuração de credencial.
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

Esta página exemplifica a solicitação de API e a carga que você pode usar para excluir uma configuração de credencial usando o `/authoring/credentials` Endpoint da API.

## Quando usar a variável `/credentials` Endpoint da API {#when-to-use}

>[!IMPORTANT]
>
>Na maioria dos casos, você ***não*** necessidade de usar o `/credentials` Endpoint da API. Em vez disso, você poderá configurar as informações de autenticação para seu destino por meio da `customerAuthenticationConfigurations` parâmetros do `/destinations` terminal.
> 
>Ler [Configuração de autenticação do cliente](../functionality/destination-configuration/customer-authentication.md) para obter informações detalhadas sobre os tipos de autenticação compatíveis.

Use esse endpoint de API para criar uma configuração de credencial somente se houver um sistema de autenticação global entre o Adobe e sua plataforma de destino e o [!DNL Platform] O cliente não precisa fornecer credenciais de autenticação para se conectar ao seu destino. Nesse caso, você deve criar uma configuração de credencial usando o `/credentials` Endpoint da API.

Ao usar um sistema de autenticação global, você deve definir `"authenticationRule":"PLATFORM_AUTHENTICATION"` no [entrega de destino](../functionality/destination-configuration/destination-delivery.md) configuração, quando [criação de uma nova configuração de destino](../authoring-api/destination-configuration/create-destination-configuration.md).

>[!IMPORTANT]
>
>Todos os nomes e valores de parâmetros compatíveis com o Destination SDK são **diferencia maiúsculas de minúsculas**. Para evitar erros de diferenciação entre maiúsculas e minúsculas, use os nomes e valores dos parâmetros exatamente como mostrado na documentação.

## Introdução às operações de API de credenciais {#get-started}

Antes de continuar, reveja o [guia de introdução](../getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas com êxito para a API, incluindo como obter a permissão de criação de destino e os cabeçalhos necessários.

## Excluir uma configuração de credencial {#delete}

É possível excluir um [existente](create-credential-configuration.md) configuração de credencial fazendo um `DELETE` solicitação à `/authoring/credentials` terminal com o `{INSTANCE_ID}`da configuração de credencial que você deseja excluir.

Para obter uma configuração de destino existente e suas configurações `{INSTANCE_ID}`, consulte o artigo sobre [recuperação de uma configuração de credencial](retrieve-credential-configuration.md).

**Formato da API**

```http
DELETE /authoring/credentials/{INSTANCE_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{INSTANCE_ID}` | A variável `ID` da configuração de credencial que você deseja excluir. |

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

Uma resposta bem-sucedida retorna o status HTTP 200 juntamente com uma resposta HTTP vazia.

+++

## Manipulação de erros de API {#error-handling}

Os endpoints da API Destination SDK seguem os princípios gerais de mensagem de erro da API Experience Platform. Consulte [Códigos de status da API](../../../landing/troubleshooting.md#api-status-codes) e [erros no cabeçalho da solicitação](../../../landing/troubleshooting.md#request-header-errors) no guia de solução de problemas da Platform.

## Próximas etapas {#next-steps}

Depois de ler este documento, agora você sabe como excluir uma configuração de credencial usando o `/authoring/credentials` Endpoint da API. Ler [como usar o Destination SDK para configurar seu destino](../guides/configure-destination-instructions.md) para entender onde essa etapa se encaixa no processo de configuração do destino.
