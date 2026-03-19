---
title: Coletar análises e aplicar personalização em aplicativos ChatGPT (coleta de dados do MCP)
description: Use um servidor MCP híbrido + padrão applyResponse do Web SDK para enviar eventos para o Adobe Experience Platform Edge Network e renderizar a personalização em uma interface do aplicativo ChatGPT.
keywords: Adobe Experience Platform, Web SDK, Edge Network, MCP, Aplicativos ChatGPT, applyResponse, endpoint de interação, personalização, análise
source-git-commit: c848f821ea911c82531c6784a17df0116572cd86
workflow-type: tm+mt
source-wordcount: '1126'
ht-degree: 0%

---

# Coletar análises e aplicar personalização em aplicativos ChatGPT (coleta de dados do MCP)

Este caso de uso mostra como conectar um aplicativo ChatGPT (servidor do protocolo de contexto do modelo + componentes opcionais da interface do usuário) ao Adobe Experience Platform Edge Network. Esse tipo de coleta de dados permite gravar análises para interações de conversação que chamam suas ferramentas e entregam decisões de personalização do Edge Network em um widget renderizado pelo ChatGPT.

>[!NOTE]
>
>Este documento é mantido com base nas atualizações mais recentes disponíveis das equipes de coleta de dados da Adobe e nas atualizações de tecnologia mais recentes do OpenAI. Dessa forma, a Adobe prevê que esse documento evoluirá com o tempo e aconselha a verificação de atualizações.

Esse caso de uso prefere uma abordagem híbrida, usando uma implementação do lado do servidor para coletar dados e uma implementação do lado do cliente para renderizar conteúdo personalizado. Essa abordagem é ideal, pois a chamada de ferramenta do MCP é o momento mais confiável para coletar análises. O widget é executado em um contexto do navegador e é o local certo para armazenar a identidade (em um cookie) e aplicar decisões de personalização.

Este caso de uso tem um exemplo de código totalmente operacional que o acompanha. Consulte [ChatGPT App + Adobe Experience Platform Edge](https://github.com/adobe/alloy-samples/tree/main/chatgpt-app) no repositório `alloy-samples` no GitHub para obter o código de amostra e as instruções de implementação.

>[!IMPORTANT]
>
>Esta página descreve uma implementação de referência destinada a ilustrar um padrão de integração. Analise os requisitos de segurança, privacidade, consentimento e produção antes de adotar a abordagem em seu aplicativo.

## Arquitetura

Em um alto nível, há cinco partes móveis:

1. **Host MCP (ChatGPT)**: o ChatGPT invoca ferramentas expostas pelo servidor MCP e fornece um identificador de usuário pseudônimo estável nos metadados de solicitação.
1. **Servidor MCP (back-end)**: pertencente à sua organização. Ele implementa ferramentas como listar itens, obter detalhes ou enviar solicitações.
1. **Adobe IMS**: emite tokens de acesso usados pelo servidor MCP para chamar APIs de coleta de dados do Adobe.
1. **Adobe Experience Platform Edge Network**: recebe eventos de experiência enviados pelo servidor MCP e retorna confirmações de análise, atualizações de estado (como identidade) e decisões de personalização.
1. **Interface da Web inserida (widget de front-end renderizado pelo host MCP)**: exibe resultados estruturados e aplica metadados Adobe recebidos do back-end do servidor MCP.

## Fluxo de dados

1. **User** solicita **ChatGPT** usando seu servidor MCP.
1. **ChatGPT** interpreta a intenção do prompt e chama a **ferramenta MCP de back-end** apropriada.
1. **O servidor MCP de back-end** usa as APIs da Coleção de Dados (ponto de extremidade `interact`) para enviar um evento de experiência à **Edge Network** para coleta de análise e personalização opcional.
1. **O Edge Network** retorna identificadores de resposta, incluindo atualizações de estado e decisões de personalização, para a **ferramenta MCP de back-end**.
1. **A ferramenta MCP de back-end** retorna um resultado de ferramenta contendo dados corporativos em `structuredContent` e metadados Adobe em `_meta` para **ChatGPT**.
1. O **ChatGPT** fornece o resultado da ferramenta para o **widget front-end**, que renderiza os dados corporativos e aplica os metadados do Adobe usando o comando `applyResponse` da biblioteca JavaScript Web SDK. Esse comando hidrata o estado do lado do cliente e renderiza decisões de personalização qualificadas na interface do usuário.

As seções a seguir detalham cada etapa.

## Etapa 1: o usuário solicita o ChatGPT usando seu servidor MCP

Esta etapa é o ponto de entrada para o fluxo de trabalho. O usuário fornece a intenção de linguagem natural:

```text
"Use the Adobe Office Information Tool to show me details about which office that is the most pet-friendly."
```

Consulte [Criar o servidor MCP](https://developers.openai.com/apps-sdk/build/mcp-server/) na documentação de desenvolvedores do OpenAI para obter mais informações.

## Etapa 2: ChatGPT interpreta a intenção e chama uma ferramenta MCP

Com base nos metadados do servidor MCP, o ChatGPT interpreta a intenção e chama o manipulador de ferramentas apropriado no servidor MCP. Essa chamada de ferramenta cria um ponto de verdade do lado do servidor para a interação que é independente do sucesso de renderização da interface do usuário. Uma de suas ferramentas pode ter os seguintes metadados:

```json
{
  "name": "office_details",
  "description": "Fetch details for a single office by ID and return personalization handles for the UI.",
  "inputSchema": {
    "type": "object",
    "properties": {
      "sessionId": { "type": "string", "description": "Server-issued session identifier." },
      "officeId": { "type": "string", "description": "Office identifier." }
    },
    "required": ["sessionId", "officeId"],
    "additionalProperties": false
  },
  "_meta": {
    "ui": {
      "visibility": ["model", "app"]
    }
  }
}
```

Consulte [Definir ferramentas](https://developers.openai.com/apps-sdk/plan/tools/) na documentação de desenvolvedores do OpenAI para obter mais informações sobre como informar ao ChatGPT o que cada ferramenta de MCP faz.

## Etapa 3: o servidor MCP envia um evento de experiência para o Edge Network

Quando o servidor MCP recebe uma solicitação, ele aciona uma chamada para o Adobe Experience Platform Edge Network registrar dados de análise e, opcionalmente, solicitar decisão/personalização. Como esta solicitação é de servidor para servidor, use o ponto de extremidade [`interact`](https://developer.adobe.com/data-collection-apis/docs/endpoints/interact/) autenticado como parte das [APIs de Coleção de Dados](https://developer.adobe.com/data-collection-apis/docs/). A Adobe recomenda usar um [namespace personalizado](https://experienceleague.adobe.com/pt-br/docs/platform-learn/implement-web-sdk/initial-configuration/configure-identities) para transmitir o identificador exclusivo OpenAI. Verifique se o namespace criado na interface do usuário do Identities e o namespace de identidade definido na chamada são correspondentes (diferencia maiúsculas de minúsculas).

```sh
curl -X POST "https://server.adobedc.net/ee/v2/interact?datastreamId={DATASTREAM_ID}"
  -H "Authorization: Bearer {TOKEN}"
  -H "x-gw-ims-org-id: {ORG_ID}"
  -H "x-api-key: {API_KEY}"
  -H "Content-Type: application/json"
  -d '{
    "event": {
      "xdm": {
        "eventType": "office.details.view",
        "identityMap": {
          "{IDENTITY_NAMESPACE}": [
            { "id": "{PSEUDONYMOUS_SUBJECT_ID}", "primary": true }
          ]
        },
        "timestamp": "YYYY-02-20T19:00:00.000Z"
      }
    },
    "query": {
      "personalization": {
        "decisionScopes": ["__view__"]
      }
    },
    "meta": {
      "state": {
        "entries": [
          { "key": "kndctr_orgid_cluster", "value": "{CLUSTER_HINT_IF_KNOWN}" },
          { "key": "kndctr_orgid_identity", "value": "{ECID_BLOB_IF_KNOWN}" }
        ]
      }
    }
  }'
```

## Etapa 4: O Edge Network retorna alças

Quando a Edge Network recebe sua chamada `interact`, ela responde com uma matriz `handle`. Essa matriz pode incluir decisões de identidade e personalização, dependendo da configuração do fluxo de dados. Um exemplo de resposta pode ser semelhante ao seguinte:

```json
{
  "requestId": "60a2f...2294d",
  "handle": [
    {
      "type": "locationHint:result",
      "payload": [
        { "scope": "EdgeNetwork", "hint": "or2", "ttlSeconds": 1800 }
      ]
    },
    {
      "type": "state:store",
      "payload": [
        { "key": "kndctr_..._identity", "value": "CiYzM...snTI=", "maxAge": 34128000 },
        { "key": "kndctr_..._cluster", "value": "or2", "maxAge": 1800 }
      ]
    }
  ]
}
```

O servidor MCP pode então extrair informações da resposta do Edge Network para manter informações de identidade:

```ts
type EdgeHandle = { type: string; payload?: Array<{ key?: string; value?: string }> };

export function extractStateStore(handles: EdgeHandle[]) {
  const store = handles.find(h => h.type === "state:store");
  const entries = store?.payload ?? [];

  const identity = entries.find(e => e.key?.includes("_identity"))?.value;
  const cluster  = entries.find(e => e.key?.includes("_cluster"))?.value;

  return { identity, cluster };
}
```

## Etapa 5: o servidor MCP retorna a saída da ferramenta estruturada, além dos metadados do Adobe para ChatGPT

A resposta da ferramenta MCP inclui a saída e a personalização estruturadas da ferramenta do Edge Network.

* O objeto `structuredContent` contém dados corporativos dos quais o ChatGPT pode ler e relatar com segurança.
* O objeto `_meta` contém identificadores de resposta do Adobe e o `identityMap` calculado pelo servidor para que o widget possa lê-los sem expor esses dados ao ChatGPT. Manter essas informações no `_meta.adobe` permite que você seja consistente sobre onde esses dados estão localizados. Passar o mesmo `identityMap` para frente ajuda o widget a usar a mesma identidade personalizada em qualquer evento posterior do lado da interface do usuário.

```json
{
  "content": "Displayed details for office seattle.",
  "structuredContent": {
    "office": {
      "id": "seattle",
      "name": "Seattle",
      "amenities": ["Pet Friendly", "Cafe", "Bike Storage"]
    }
  },
  "_meta": {
    "adobe": {
      "identityMap": {
        "{IDENTITY_NAMESPACE}": [
          { "id": "{PSEUDONYMOUS_SUBJECT_ID}", "primary": true }
        ]
      },
      "handles": [
        {
          "type": "state:store",
          "payload": [
            { "key": "kndctr_..._identity", "value": "..." }
          ]
        },
        {
          "type": "personalization:decisions",
          "payload": [
            { "id": "..." }
          ]
        }
      ]
    }
  }
}
```

Consulte [Resultados da ferramenta](https://developers.openai.com/apps-sdk/reference/#tool-results) na OpenAI Developer reference para obter mais informações.

## Etapa 6: O widget renderiza o resultado e aplica `_adobe.handles` usando `applyResponse`

O widget renderiza os dados corporativos de `structuredContent` e lê os metadados de Adobe de `_meta.adobe`. No ChatGPT, os mesmos dados estão disponíveis para o widget por meio da camada de compatibilidade:

* `window.openai.toolOutput` contém `structuredContent`
* `window.openai.toolResponseMetadata` contém `_meta`

O widget usa o comando [`applyResponse`](../../js/commands/applyresponse.md) da biblioteca JavaScript do Web SDK para hidratar o estado do lado do cliente e renderizar as decisões de personalização retornadas pela chamada `interact` do lado do servidor. Chame o comando [`configure`](../../js/commands/configure/overview.md) antes de chamar `applyResponse`. Como o servidor MCP executou uma chamada `interact`, não é necessário chamar imediatamente o comando [`sendEvent`](../../js/commands/sendevent/overview.md) para a interação da invocação de ferramenta.

```js
// Configure the Web SDK before any other commands.
alloy("configure", {
  datastreamId: "YOUR_DATASTREAM_ID",
  orgId: "YOUR_EXPERIENCE_CLOUD_ORG_ID"
});

// Business data exposed to ChatGPT and the widget.
const { office } = window.openai?.toolOutput ?? {};

// Adobe metadata available only to the widget.
const adobe = window.openai?.toolResponseMetadata?.adobe ?? {};
const { identityMap, handles } = adobe;

// Hydrate client-side state and render personalization decisions from the
// server-side interact response.
alloy("applyResponse", {
  renderDecisions: true,
  responseBody: { handle: handles ?? [] }
});
```

Se o widget enviar eventos adicionais do lado da interface posteriormente, você poderá incluir o mesmo `identityMap` nessas chamadas:

```js
alloy("sendEvent", {
  xdm: {
    eventType: "office.details.widgetView",
    identityMap
  }
});
```

Esse padrão mantém o uso de identidade do lado do servidor e da interface do usuário alinhado, enquanto ainda permite que a chamada do lado do servidor `interact` permaneça a fonte da verdade para a coleção e a decisão do Analytics.

## Validação

Depois que todas as etapas acima estiverem configuradas, você poderá validar o seguinte:

* **Coleção de dados:** verifique se os eventos estão atingindo o conjunto de dados desejado e se cada evento é processado conforme esperado.
* **Personalization:** verifique se as decisões são retornadas pela Edge Network e se são renderizadas pelo seu widget.

## Considerações de segurança e privacidade

* Trate os identificadores do ChatGPT como sensíveis, mesmo que sejam pseudônimos.
* Aplique as práticas de consentimento e governança de dados da sua organização a esse fluxo de trabalho.
* A Adobe recomenda usar os fluxos de trabalho do OAuth 2.1 para autorização.
* Certifique-se de que os tokens e segredos de acesso nunca cheguem ao cliente ou à interface do usuário.
