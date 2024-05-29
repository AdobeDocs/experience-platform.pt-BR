---
title: Notas de versão do SDK da Web da Adobe Experience Platform
description: As notas de versão mais recentes do Adobe Experience Platform Web SDK.
keywords: Adobe Experience Platform Web SDK;Platform Web SDK;Web SDK;notas de versão;
exl-id: efd4e866-6a27-4bd5-af83-4a97ca8adebd
source-git-commit: 060f6bb0ff6f57a84698a27bd9f640c0178e5b51
workflow-type: tm+mt
source-wordcount: '1811'
ht-degree: 1%

---


# Notas de versão

Este documento aborda as notas de versão do Adobe Experience Platform Web SDK.
Para obter as notas de versão mais recentes da extensão de tag do SDK da Web, consulte o [Notas de versão da extensão de tag do SDK da Web](../tags/extensions/client/web-sdk/web-sdk-ext-release-notes.md).

>[!IMPORTANT]
>
>Google [anunciou](https://developers.google.com/privacy-sandbox/3pcd/prepare/prepare-for-phaseout) planeja descontinuar o suporte do Chrome para cookies de terceiros no segundo semestre de 2024. Consequentemente, os cookies de terceiros não serão mais compatíveis com a maioria dos navegadores.
>
>Quando essa alteração for implementada, o Adobe descontinuará o suporte para o `demdex` cookie atualmente compatível com o SDK da Web.

## Versão 2.20.0 - 21 de maio de 2024

**Novos recursos**

* Suporte adicionado para [Coleção de mídia de streaming](../web-sdk/commands/configure/streamingmedia.md).

**Correções e aprimoramentos**

* Correção de um bug que fazia com que o conteúdo padrão ficasse oculto pelo trecho pré-ocultação quando o consentimento era recusado.

## Versão 2.19.2 - 10 de janeiro de 2024

**Correções e aprimoramentos**

* Correção de um problema em que os erros de identidade mascaravam outros erros e alteravam os erros de identidade para avisos.
* Correção de um problema em que a parte inferior das chamadas de página nunca era enviada quando havia uma chamada de parte superior da página com `renderDecisions` definir como `false`.
* Correção de um problema em que o SDK da Web não lia identidades entre domínios quando havia várias `adobe_mc` parâmetros da sequência de consulta.

## Versão 2.19.1 - 10 de novembro de 2023

**Correções e aprimoramentos**

* Correção de um problema em que a matriz de apresentações retornava de `sendEvent` As chamadas sempre estavam vazias.

## Versão 2.19.0 - 1 de novembro de 2023

**Novos recursos**

* Adição de suporte para renderização de mensagens no aplicativo do Adobe Journey Optimizer.
* Suporte adicionado para [eventos na parte superior e inferior da página](use-cases/top-bottom-page-events.md).
* Adicionado [`defaultPersonalizationEnabled`](commands/sendevent/personalization.md) opção para o `sendEvent` comando para controlar a solicitação do escopo de toda a página e da superfície padrão.

**Correções e aprimoramentos**

* A personalização combinada exibe eventos juntos ao renderizar vários tipos de personalização.
* Correção de um problema em que os nomes de exibição do aplicativo de página única diferenciavam maiúsculas de minúsculas.
* Correção de um problema com seletores de oferta personalizados DOM sombra.

## Versão 2.18.0 - 31 de julho de 2023

**Novos recursos**

* Suporte adicionado para [substituições por comando da ID do fluxo de dados](../datastreams/overrides.md).

**Correções e aprimoramentos**

* Correção de um problema em que os links de saída falhavam ao serem qualificados devido ao domínio fazer parte da consulta.
* Obsoleto `edgeConfigId` a favor de `datastreamId` na configuração do SDK da Web.

## Versão 2.17.0 - 17 de maio de 2023

**Correções e aprimoramentos**

* O SDK da Web agora codifica os valores de destino do cookie Audience Manager, semelhantes ao [Data Integration Library (DIL)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html?lang=pt-BR).

## Versão 2.16.0 - 25 de abril de 2023

**Novos recursos**

* Suporte adicionado para [substituições de configuração da sequência de dados](../datastreams/overrides.md).

## Versão 2.15.0 - 30 de março de 2023

**Novos recursos**

* Suporte adicionado para [`onBeforeLinkClickSend`](/help/web-sdk/commands/configure/onbeforelinkclicksend.md) link, clique em callback.
* Adição de suporte para o rastreamento de cliques do Adobe Journey Optimizer.

**Correções e aprimoramentos**

* A coleção de links agora inclui o nome do link e a região do visitante.
* Remoção do erro de console para destinos de URL com falha.

## Versão 2.14.0 - 25 de janeiro de 2023

* (Beta) Adição de suporte para superfícies e apresentações do Adobe Journey Optimizer.

**Correções e aprimoramentos**

* Correção de um problema com ações de código personalizado do Adobe Target VEC em que o código era inserido em um local alternativo em vez de com [!DNL at.js].
* Correção de um problema em que, em alguns casos, o cabeçalho &quot;referenciador&quot; não era definido corretamente nas solicitações para o Edge Network.
* Correção de um problema em que [dica do cliente do agente do usuário](/help/web-sdk/use-cases/client-hints.md) as propriedades podem ser definidas como um tipo incorreto.
* Correção de um problema em que `placeContext.localTime` não corresponde ao esquema.

## Versão 2.13.1 - 13 de outubro de 2022

* Correção de um problema em que a migração de visitantes não funcionava se window.Visitor fosse definido após a configuração. Esse problema ocorre principalmente ao executar com tags Adobe.
* Correção de um problema em que `device.screenWidth` e `device.screenHeight` foram preenchidos como strings em alguns ambientes.

## Versão 2.13.0 - 28 de setembro de 2022

**Novos recursos**

* Suporte adicionado para [Migração completa de página por página](home.md#migrating-to-web-sdk). O perfil do Adobe Target agora será preservado à medida que um visitante se move entre páginas da at.js e do SDK da Web.
* Adição de suporte configurável para [Client Hints de usuário-agente de alta entropia](/help/web-sdk/use-cases/client-hints.md).
* Adição de suporte para o [`applyResponse`](/help/web-sdk/commands/applyresponse.md) comando. Isso permite a personalização híbrida por meio do [API do servidor Edge Network](../server-api/overview.md).
* Os links do modo de controle de qualidade agora funcionam em várias páginas.

**Correções e aprimoramentos**

* Correção de um problema em que as métricas de rastreamento de cliques de personalização não eram atualizadas quando o rastreamento de link era desativado.
* Comandos atualizados para gerar um erro de validação quando opções desconhecidas forem especificadas.
* A variável `_experience.decisioning.propositionEventType` A propriedade agora é preenchida ao enviar automaticamente eventos de personalização de exibição e interação.
* Adição da validação de namespace duplicado para o `getIdentity` comando.
* Adição da validação do escopo de decisão duplicado para o `sendEvent` comando.

## Versão 2.12.0 - 29 de junho de 2022

* Altere as solicitações para o Edge Network para usar o `cluster` dica de localização do cookie como parte do URL. Isso garante que os usuários que mudam de localização (por exemplo, por meio de uma VPN ou ao dirigir com dispositivos móveis etc.) no meio da sessão atinjam a mesma borda e tenham o mesmo perfil de personalização.
* Restrinja as funções configuradas na resposta do comando getLibraryInfo.

## Versão 2.11.0 - 13 de junho de 2022

**Novos recursos**

* Agora é possível fornecer experiências personalizadas com mais precisão, compartilhando IDs de visitante entre aplicativos móveis e conteúdo da Web móvel, e entre domínios. Consulte a [documentação dedicada](identity/id-sharing.md) para saber mais.
* Agora é possível renderizar ou executar uma matriz de propostas de [!DNL Adobe Target] em aplicativos de página única, sem incrementar as métricas do analytics. Isso reduz os erros de relatório e aumenta a precisão da análise. Consulte a [documentação dedicada](personalization/rendering-personalization-content.md#applypropositions) para saber mais.
* Foram adicionadas informações adicionais à `getLibraryInfo` incluindo os comandos disponíveis e a configuração final da instância.

**Correções e aprimoramentos**

* Configurações de cookie atualizadas para usar `sameSite="none"` e `secure` sinalizador ativado [!DNL HTTPS] páginas.
* Correção de um problema em que o conteúdo personalizado não era aplicado corretamente ao usar o `eq` pseudoseletor.
* Correção de um problema em que `localTimezoneOffset` falha na validação do Experience Platform.

## Versão 2.10.1 - 3 de maio de 2022

* Correção de um problema em que vários iframes persistentes eram criados para sincronizações de ID e destinos de segmento.

## Versão 2.10.0 - 22 de abril de 2022

* Use um iframe persistente para todas as sincronizações de ID e destinos de segmentos.
* Correção de um problema em que as apresentações de métricas mescladas eram duplicadas no `sendEvent` resultado.

## Versão 2.9.0 - 10 de março de 2022

* Suporte adicionado para rastreamento [!DNL control (default)] Experiências do Adobe Target.
* Otimização dos eventos de alteração de visualização para aplicativos de página única. A notificação de exibição agora é incluída no evento de alteração de visualização quando as experiências personalizadas são renderizadas.
* Remoção do aviso do console quando não `eventType` está presente.
* Correção de um problema em que a variável `propositions` a propriedade foi retornada somente de um `sendEvent` comando quando as experiências foram solicitadas ou recuperadas do cache. A variável `propositions` agora, a propriedade sempre será definida como uma matriz.
* Correção de um problema em que os contêineres ocultos não eram exibidos quando um erro era retornado do Edge Network.
* Correção de um problema em que os eventos interativos não eram contados no Adobe Target. Isso foi corrigido adicionando o nome da exibição ao XDM em web.webPageDetails.viewName.
* Corrigir links de documentação corrompidos nas mensagens do console.

## Versão 2.8.0 - 19 de janeiro de 2022

* Seletores DOM de sombra compatíveis com personalização.
* Tipos de evento de personalização renomeados. (`display` e `click` tornar `decisioning.propositionDisplay` e `decisioning.propositionInteract`)
* Correção de um problema em que as ofertas do HTML com tags de script integradas adicionavam as tags de script duas vezes à página, mesmo que o script fosse executado apenas uma vez.

## Versão 2.7.0 - 26 de outubro de 2021

* Expor informações adicionais do Edge Network no valor de retorno do `sendEvent`, incluindo `inferences` e `destinations`. O formato dessas propriedades pode mudar, pois esses recursos estão sendo lançados como parte de uma versão beta.

## Versão 2.6.4 - 7 de setembro de 2021

* Correção de um problema em que as ações set HTML Adobe Target eram aplicadas ao `head` elementos estavam substituindo todo o `head` conteúdo. Agora defina as ações de HTML aplicadas ao `head` elemento são alterados para anexar HTML.

## Versão 2.6.3 - 16 de agosto de 2021

* Correção de um problema em que objetos não destinados ao uso público eram expostos por meio da promessa resolvida do `configure` comando.

## Versão 2.6.2 - 4 de agosto de 2021

* Correção de um problema em que um aviso sobre a desativação do `result.decisions` (fornecido pela `sendEvent` ) seria registrado no console mesmo quando a variável `result.decisions` a propriedade não estava sendo acessada. Nenhum aviso será registrado ao acessar o `result.decisions` propriedade, mas a propriedade ainda está obsoleta.

## Versão 2.6.1 - 29 de julho de 2021

* Correção de um problema em que a personalização da renderização para uma exibição de aplicativo de página única sem conteúdo de personalização gerava um erro e causava o retorno da promessa do `sendEvent` comando a ser rejeitado.

## Versão 2.6.0 - 27 de julho de 2021

* Fornece mais conteúdo de personalização no `sendEvent` promessa resolvida, incluindo tokens de resposta do Adobe Target. Quando a variável `sendEvent` é executado, uma promessa é retornada, que eventualmente é resolvida com um `result` objeto que contém informações recebidas do servidor. Anteriormente, esse objeto de resultado incluía uma propriedade chamada `decisions`. Este `decisions` propriedade foi descontinuada. Uma nova propriedade, `propositions`, foi adicionado. Essa nova propriedade fornece aos clientes acesso a mais conteúdo de personalização, incluindo [tokens de resposta](/help/web-sdk/personalization/adobe-target/accessing-response-tokens.md).

## Versão 2.5.0 - junho de 2021

* Adição de suporte para ofertas de personalização de redirecionamento.
* As larguras e alturas do visor coletadas automaticamente que são valores negativos não serão mais enviadas para o servidor.
* Quando um evento é cancelado ao retornar `false` de um `onBeforeEventSend` retorno de chamada, uma mensagem agora é registrada.
* Correção de um problema em que dados XDM específicos destinados a um único evento eram incluídos em vários eventos.

## Versão 2.4.0 - março de 2021

* O SDK agora pode ser instalado como um [Pacote NPM](/help/web-sdk/install/npm.md).
* Adição de suporte para um `out` opção quando [configuração do consentimento padrão](/help/web-sdk/commands/configure/defaultconsent.md), que elimina todos os eventos até que o consentimento seja recebido (o existente `pending` opção enfileira eventos e os envia quando o consentimento é recebido).
* A variável [`onBeforeEventSend`](/help/web-sdk/commands/configure/onbeforeeventsend.md) O retorno de chamada agora pode ser usado para impedir que um evento seja enviado.
* Agora usa um grupo de campos de esquema XDM em vez de `meta.personalization` ao enviar eventos sobre conteúdo personalizado que está sendo renderizado ou clicado.
* A variável [`getIdentity`](/help/web-sdk/commands/getidentity.md) O comando agora retorna a ID da região da borda ao lado da identidade.
* Os avisos e erros recebidos do servidor foram aprimorados e são tratados de maneira mais apropriada.
* Adição de suporte para o padrão Adobe Consent 2.0 para o [`setConsent`](/help/web-sdk/commands/setconsent.md) comando.
* As preferências de consentimento, quando recebidas, são colocadas em hash e armazenadas no armazenamento local para uma integração otimizada entre CMPs, SDK da Web da plataforma e Edge Network da plataforma. Se estiver coletando preferências de consentimento, agora recomendamos que você ligue para `setConsent` em cada carregamento de página.
* Dois [monitoração de ganchos](https://github.com/adobe/alloy/wiki/Monitoring-Hooks), `onCommandResolved` e `onCommandRejected`, foram adicionadas.
* Correção de erros: os eventos de notificação da interação de personalização conteriam informações duplicadas sobre a mesma atividade quando um usuário navegasse para uma nova exibição de aplicativo de página única, retornasse à exibição original e clicasse em um elemento qualificado para conversão.
* Correção de erros: se o primeiro evento enviado pelo SDK tivesse `documentUnloading` definir como `true`, [`sendBeacon`](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/sendBeacon) seria usado para enviar o evento, resultando em um erro relacionado a uma identidade que não está sendo estabelecida.

## Versão 2.3.0 - novembro de 2020

* Adição de suporte ao nonce para permitir políticas mais rigorosas de segurança de conteúdo.
* Adição de suporte de personalização para aplicativos de página única.
* Compatibilidade aprimorada com outro código JavaScript na página que pode estar sendo substituído `window.console` APIs.
* Correção de erros: `sendBeacon` não estava sendo usada quando `documentUnloading` foi definido como `true` ou quando os cliques em links eram rastreados automaticamente.
* Correção de erros: um link não seria rastreado automaticamente se o elemento de ancoragem contivesse conteúdo de HTML.
* Correção de erros: Determinados erros do navegador que contêm um plug-in somente leitura `message` propriedade não foram tratados adequadamente, resultando em um erro diferente sendo exposto ao cliente.
* Correção de erros: executar o SDK em um iframe resultaria em um erro se a página HTML do iframe fosse de um subdomínio diferente da página HTML da janela principal.

## Versão 2.2.0 - outubro de 2020

* Correção de erros: o objeto de aceitação impedia o SDK da Web de fazer chamadas quando `idMigrationEnabled` é `true`.
* Correção de erros: torne o SDK da Web ciente das solicitações que devem retornar ofertas de personalização para evitar um problema de oscilação.

## Versão 2.1.0 - agosto de 2020

* Remova o `syncIdentity` comando e suporte que transmitem essas IDs no `sendEvent` comando.
* Suporte ao Padrão de consentimento IAB 2.0.
* Suporte à transmissão de IDs adicionais no `setConsent` comando.
* Suporte para substituição de `datasetId` no `sendEvent` comando.
* Ganchos de monitoramento de suporte ([Leia mais](https://github.com/adobe/alloy/wiki/Monitoring-Hooks))
* Aprovado `environment: browser` nos dados de contexto de detalhes da implementação.
