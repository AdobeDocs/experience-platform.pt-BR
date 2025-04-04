---
description: Saiba como formatar uma chamada de API para enviar uma solicitação de publicação de destino por meio do Adobe Experience Platform Destination SDK.
title: Criar uma solicitação de publicação de destino
exl-id: 913be9de-a699-4756-885d-b3761ec729cb
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 2%

---

# Criar uma solicitação de publicação de destino

>[!IMPORTANT]
>
>Você só precisará usar esse endpoint de API se estiver enviando um destino produtizado (público), para ser usado por outros clientes do Experience Platform. Se você estiver criando um destino privado para uso próprio, não será necessário enviar formalmente o destino usando a API de publicação.

>[!IMPORTANT]
>
>**Ponto de extremidade de API**: `platform.adobe.io/data/core/activation/authoring/destinations/publish`

Depois de configurar e testar seu destino, você pode enviá-lo ao Adobe para revisão e publicação. Leia [Enviar para revisão um destino criado no Destination SDK](../guides/submit-destination.md) para todas as outras etapas que você deve realizar como parte do processo de envio do destino.

Use o endpoint da API de destinos de publicação para enviar uma solicitação de publicação quando:

* Como parceiro da Destination SDK, você deseja disponibilizar seu destino produzido em todas as organizações da Experience Platform para todos os clientes da Experience Platform usarem;
* Você faz *quaisquer atualizações* para suas configurações. As atualizações de configuração são refletidas no destino somente após você enviar uma nova solicitação de publicação, que é aprovada pela equipe do Experience Platform.

>[!IMPORTANT]
>
>Todos os nomes e valores de parâmetros com suporte do Destination SDK diferenciam maiúsculas de minúsculas **1}.** Para evitar erros de diferenciação entre maiúsculas e minúsculas, use os nomes e valores dos parâmetros exatamente como mostrado na documentação.

## Introdução às operações de API de publicação de destino {#get-started}

Antes de continuar, consulte o [guia de introdução](../getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas com êxito para a API, incluindo como obter a permissão de criação de destino e os cabeçalhos necessários.

## Enviar uma configuração de destino para publicação {#create}

Você pode enviar uma configuração de destino para publicação fazendo uma solicitação POST para o ponto de extremidade `/authoring/destinations/publish`.

**Formato da API**

```http
POST /authoring/destinations/publish
```

+++Solicitação

A solicitação a seguir envia um destino para publicação, entre as organizações configuradas pelos parâmetros fornecidos na carga. A carga abaixo inclui todos os parâmetros aceitos pelo ponto de extremidade `/authoring/destinations/publish`.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations/publish \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "destinationId":"1230e5e4-4ab8-4655-ae1e-a6296b30f2ec",
   "destinationAccess":"ALL"
}
```

| Parâmetro | Tipo | Descrição |
|---------|----------|------|
| `destinationId` | String | A ID de destino da configuração de destino que você está enviando para publicação. Obtenha a ID de destino de uma configuração de destino usando a chamada de API [recuperar uma configuração de destino](../authoring-api/destination-configuration/retrieve-destination-configuration.md). |
| `destinationAccess` | String | Use o `ALL` para que seu destino apareça no catálogo para todos os clientes da Experience Platform. |

{style="table-layout:auto"}

+++

+++Resposta

Uma resposta bem-sucedida retorna o status HTTP 201 com detalhes da solicitação de publicação de destino.

+++

## Manipulação de erros de API

Os endpoints da API do Destination SDK seguem os princípios gerais de mensagem de erro da API do Experience Platform. Consulte [códigos de status da API](../../../landing/troubleshooting.md#api-status-codes) e [erros no cabeçalho da solicitação](../../../landing/troubleshooting.md#request-header-errors) no guia de solução de problemas do Experience Platform.

## Próximas etapas

Depois de ler este documento, agora você sabe como enviar uma solicitação de publicação para o seu destino. A equipe do Adobe Experience Platform revisará sua solicitação de publicação e entrará em contato com você em cinco dias úteis.
