---
title: Personalização do lado do servidor usando a API do servidor de rede de borda
description: Este artigo demonstra como você pode usar a API do Servidor de rede de borda para implantar a personalização do lado do servidor nas suas propriedades da Web.
keywords: personalização, api do servidor, rede de borda, lado do servidor,
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 2%

---


# Personalização do lado do servidor usando a API do servidor de rede de borda

## Visão geral {#overview}

A personalização do lado do servidor envolve o uso da variável [API do servidor de rede de borda](../../server-api/overview.md) para personalizar a experiência do cliente em suas propriedades da web.

No exemplo descrito neste artigo, o conteúdo de personalização é recuperado no lado do servidor, usando a API do servidor. Em seguida, o HTML é renderizado no lado do servidor, com base no conteúdo de personalização recuperado.

A tabela abaixo mostra um exemplo de conteúdo personalizado e não personalizado.

| Página de exemplo sem personalização | Exemplo de página com personalização |
|---|---|
| ![Exemplo de página da Web sem personalização](assets/plain.png) | ![Exemplo de página da Web com personalização](assets/personalized.png) |

## Considerações {#considerations}

### Cookies {#cookies}

Os cookies são usados para manter a identidade do usuário e as informações do cluster.  Ao usar uma implementação do lado do servidor, o servidor de aplicativos manipula o armazenamento e o envio desses cookies durante o ciclo de vida da solicitação.

| Cookie | Propósito | Armazenado por | Enviado por |
|---|---|---|---|
| `kndctr_AdobeOrg_identity` | Contém detalhes da identidade do usuário. | Servidor de aplicativos | Servidor de aplicativos |
| `kndctr_AdobeOrg_cluster` | Indica qual cluster da Rede de Borda deve ser usado para atender às solicitações. | Servidor de aplicativos | Servidor de aplicativos |

### Solicitar posicionamento {#request-placement}

As solicitações de personalização são necessárias para obter apresentações e enviar uma notificação de exibição. Ao usar uma implementação do lado do servidor, o servidor de aplicativos faz essas solicitações para a API do servidor da rede de borda.

| Solicitação | Feito por |
|---|---|
| Solicitação do Interact para recuperar apresentações | Servidor de aplicativos que chama a API de Servidor de Rede de Borda. |
| Solicitação do Interact para enviar notificações de exibição | Servidor de aplicativos que chama a API de Servidor de Rede de Borda. |

## Aplicativo de amostra {#sample-app}

O processo descrito abaixo usa um aplicativo de amostra que você pode usar como ponto de partida para experimentar e saber mais sobre esse tipo de personalização.

Você pode baixar essa amostra e personalizá-la de acordo com suas necessidades. Por exemplo, você pode alterar as variáveis de ambiente para que o aplicativo de amostra obtenha ofertas de sua própria configuração de Experience Platform.

Para fazer isso, abra o `.env` arquivo na raiz do repositório e modifique as variáveis de acordo com sua configuração. Reinicie o aplicativo de amostra e estará pronto para experimentar usando seu próprio conteúdo de personalização.

### Execução da amostra {#running-sample}

Siga as etapas abaixo para executar o aplicativo de amostra.

1. Clonar [este repositório](https://github.com/adobe/alloy-samples) ao computador local.
2. Abra um terminal e navegue até o `personalization-server-side` pasta.
3. Executar `npm install`.
4. Executar `npm start`.
5. Abra o navegador da Web e navegue até `http://localhost`.

## Visão geral do processo {#process}

Esta seção descreve as etapas usadas na recuperação do conteúdo de personalização.

1. [Expresso](https://expressjs.com/) é usado para uma implementação enxuta do lado do servidor. Isso lida com roteamento e solicitações básicas do servidor.
2. O navegador solicita a página da Web. Todos os cookies armazenados anteriormente pelo navegador, com o prefixo `kndctr_`, estão incluídos.
3. Quando a página é solicitada no servidor de aplicativos, um evento é enviado para o [ponto de extremidade de coleção de dados interativa](../../../server-api/interactive-data-collection.md) para buscar conteúdo de personalização. O aplicativo de amostra usa métodos auxiliares para simplificar a criação e o envio de solicitações para a API (consulte [aepEdgeClient.js](https://github.com/adobe/alloy-samples/blob/main/common/aepEdgeClient.js)). A variável `POST` contém um `event` e uma `query`. Os cookies da etapa anterior, se disponíveis, estão incluídos na variável `meta>state>entries` matriz.

   ```js
   fetch(
   "https://edge.adobedc.net/ee/v2/interact?dataStreamId=abc&requestId=123",
   {
      headers: {
         accept: "*/*",
         "accept-language": "en-US,en;q=0.9",
         "cache-control": "no-cache",
         "content-type": "text/plain; charset=UTF-8",
         pragma: "no-cache",
         "sec-fetch-dest": "empty",
         "sec-fetch-mode": "cors",
         "sec-fetch-site": "cross-site",
         "sec-gpc": "1",
         "Referrer-Policy": "strict-origin-when-cross-origin",
         Referer: "http://localhost/",
      },
      body: JSON.stringify({
         event: {
         xdm: {
            web: {
               webPageDetails: {
               URL: "http://localhost/",
               },
               webReferrer: {
               URL: "",
               },
            },
            identityMap: {
               FPID: [
               {
                  id: "xyz",
                  authenticatedState: "ambiguous",
                  primary: true,
               },
               ],
            },
            timestamp: "2022-06-23T22:21:00.878Z",
         },
         data: {},
         },
         query: {
         identity: {
            fetch: ["ECID"],
         },
         personalization: {
            schemas: [
               "https://ns.adobe.com/personalization/default-content-item",
               "https://ns.adobe.com/personalization/html-content-item",
               "https://ns.adobe.com/personalization/json-content-item",
               "https://ns.adobe.com/personalization/redirect-item",
               "https://ns.adobe.com/personalization/dom-action",
            ],
            decisionScopes: ["__view__", "sample-json-offer"],
         },
         },
         meta: {
         state: {
            domain: "localhost",
            cookiesEnabled: true,
            entries: [
               {
               "key": "kndctr_XXX_AdobeOrg_identity",
               "value": "abc123"
               },
               {
               "key": "kndctr_XXX_AdobeOrg_cluster",
               "value": "or2"
               }
            ],
         },
         },
      }),
      method: "POST",
   }
   ).then((res) => res.json());
   ```

4. A oferta do Target da atividade baseada em formulário é lida da resposta e usada ao produzir a resposta HTML.
5. Para atividades baseadas em formulário, os eventos de exibição devem ser enviados manualmente na implementação para indicar quando a oferta foi exibida. Neste exemplo, a notificação é enviada no lado do servidor, durante o ciclo de vida da solicitação.

   ```js
   function sendDisplayEvent(aepEdgeClient, req, propositions, cookieEntries) {
   const address = getAddress(req);
   
   aepEdgeClient.interact(
      {
         event: {
         xdm: {
            web: {
               webPageDetails: { URL: address },
               webReferrer: { URL: "" },
            },
            timestamp: new Date().toISOString(),
            eventType: "decisioning.propositionDisplay",
            _experience: {
               decisioning: {
               propositions: propositions.map((proposition) => {
                  const { id, scope, scopeDetails } = proposition;
   
                  return {
                     id,
                     scope,
                     scopeDetails,
                  };
               }),
               },
            },
         },
         },
         query: { identity: { fetch: ["ECID"] } },
         meta: {
         state: {
            domain: "",
            cookiesEnabled: true,
            entries: [...cookieEntries],
         },
         },
      },
      {
         Referer: address,
      }
   );
   }
   ```

6. [!DNL Visual Experience Composer (VEC)] As ofertas são ignoradas, pois só podem ser renderizadas por meio do SDK da Web.
7. Quando a resposta do HTML é retornada, a identidade e os cookies de cluster são definidos na resposta pelo servidor de aplicativos.