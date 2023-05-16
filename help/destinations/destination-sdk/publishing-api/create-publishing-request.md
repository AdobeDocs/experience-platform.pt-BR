---
description: Saiba como formatar uma chamada de API para enviar uma solicitação de publicação de destino por meio do Adobe Experience Platform Destination SDK.
title: Criar uma solicitação de publicação de destino
source-git-commit: acb7075f49b4194c31371d2de63709eea7821329
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 2%

---


# Criar uma solicitação de publicação de destino

>[!IMPORTANT]
>
>Você só precisará usar esse endpoint da API se estiver enviando um destino (público) produzido para ser usado por outros clientes do Experience Platform. Se estiver criando um destino privado para uso próprio, não será necessário enviar formalmente o destino usando a API de publicação.

>[!IMPORTANT]
>
>**Ponto de acesso da API**: `platform.adobe.io/data/core/activation/authoring/destinations/publish`

Após configurar e testar seu destino, você pode enviá-lo ao Adobe para análise e publicação. Ler [Enviar para revisão de um destino criado no Destination SDK](../guides/submit-destination.md) para todas as outras etapas, é necessário fazer parte do processo de envio do destino.

Use o endpoint da API de destinos de publicação para enviar uma solicitação de publicação quando:

* Como parceiro de Destination SDK, você deseja disponibilizar o destino produzido em todas as organizações de Experience Platform para que todos os clientes de Experience Platform possam usá-lo;
* Você faz *qualquer atualização* nas suas configurações. As atualizações de configuração são refletidas no destino somente após enviar uma nova solicitação de publicação, que é aprovada pela equipe do Experience Platform.

>[!IMPORTANT]
>
>Todos os nomes de parâmetros e valores suportados pelo Destination SDK são **distinção entre maiúsculas e minúsculas**. Para evitar erros de diferenciação entre maiúsculas e minúsculas, use os nomes e valores dos parâmetros exatamente como mostrado na documentação.

## Introdução às operações da API de publicação de destino {#get-started}

Antes de continuar, reveja o [guia de introdução](../getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas para a API com sucesso, incluindo como obter a permissão de criação de destino necessária e os cabeçalhos necessários.

## Enviar uma configuração de destino para publicação {#create}

Você pode enviar uma configuração de destino para publicação fazendo uma solicitação de POST para a `/authoring/destinations/publish` endpoint .

**Formato da API**

```http
POST /authoring/destinations/publish
```

+++Solicitação

A solicitação a seguir envia um destino para publicação, em todas as organizações configuradas pelos parâmetros fornecidos no payload. A carga abaixo inclui todos os parâmetros aceitos pela `/authoring/destinations/publish` endpoint .

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
| `destinationId` | String | A ID de destino da configuração de destino que você está enviando para publicação. Obtenha a ID de destino de uma configuração de destino usando o [recuperar uma configuração de destino](../authoring-api/destination-configuration/retrieve-destination-configuration.md) Chamada de API. |
| `destinationAccess` | String | Use `ALL` para que seu destino apareça no catálogo para todos os clientes do Experience Platform. |

{style="table-layout:auto"}

+++Resposta

Uma resposta bem-sucedida retorna o status HTTP 201 com detalhes da solicitação de publicação de destino.

## Tratamento de erros da API

Os pontos de extremidade da API do Destination SDK seguem os princípios gerais da mensagem de erro da API do Experience Platform. Consulte [Códigos de status da API](../../../landing/troubleshooting.md#api-status-codes) e [erros do cabeçalho da solicitação](../../../landing/troubleshooting.md#request-header-errors) no guia de solução de problemas da plataforma.

## Próximas etapas

Após a leitura deste documento, você agora sabe como enviar uma solicitação de publicação para o seu destino. A equipe da Adobe Experience Platform verificará sua solicitação de publicação e retornará a você com cinco dias úteis.