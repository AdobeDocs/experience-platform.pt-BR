---
title: Notas de versão do SDK da Web da Adobe Experience Platform
description: As notas de versão mais recentes do SDK da Web da Adobe Experience Platform.
keywords: Adobe Experience Platform Web SDK;Experience Platform Web SDK;Web SDK;notas de versão;
exl-id: efd4e866-6a27-4bd5-af83-4a97ca8adebd
source-git-commit: 05b9893e17db0caeab1175f35f939cb6a1dd0291
workflow-type: tm+mt
source-wordcount: '2573'
ht-degree: 5%

---


# Notas de versão do Web SDK

Este documento aborda as notas de versão do Adobe Experience Platform Web SDK.
Para obter as notas de versão mais recentes da extensão de tag do Web SDK, consulte as [notas de versão da extensão de tag do Web SDK](../tags/extensions/client/web-sdk/web-sdk-ext-release-notes.md).

## Versão 2.29.0 - 4 de setembro de 2025

**Novos recursos**

- Adição de suporte para coleta de dados de anúncio do Adobe para o Adobe Jornada Analytics
- Adição de suporte para gravar detalhes da assinatura push nos perfis do usuário.

**Correções e melhorias**

- Correção de um problema em que as seções de substituição de configuração eram mescladas em vez de substituídas.
- Correção de um problema em que a coleção de links enviava todo o conteúdo do documento como o nome do link.
- Correção de um problema em que determinadas apresentações não podiam ser renderizadas novamente.

## Versão 2.28.1 - sexta-feira, 31 de julho de 2025

**Correções e melhorias**

- Correção de um problema que impedia a execução de compilações personalizadas.

## Versão 2.28.0 - sexta-feira, 24 de julho de 2025

**Novos recursos**

- Adição de suporte para regras de desqualificação do Adobe Journey Optimizer.

**Correções e melhorias**

- Correção de um erro no [rastreador do Media Analytics](commands/getmediaanalyticstracker.md) em que a propriedade `length` do objeto de mídia aceitava incorretamente tipos de dados inválidos.
- Melhoria na manipulação de erros de [gerenciamento de identidade](identity/overview.md) para processar corretamente rejeições de promessas quando a pesquisa de identidade falha.
- Solução de um problema em que o [conteúdo de personalização](personalization/rendering-personalization-content.md) com itens de conteúdo do HTML não era renderizado com um erro relacionado a um `renderStatusHandler` ausente.
- Corrigido o Activity Map [coleção de URLs](commands/configure/clickcollectionenabled.md) para manipular corretamente URLs não HTTP.

**Problemas conhecidos**

- O processo de [compilação personalizada](/help/web-sdk/install/create-custom-build.md) usando `npx @adobe/alloy` não está funcionando no momento como esperado na versão 2.28.0. Todos os componentes são incluídos na criação gerada, independentemente dos módulos selecionados. Esse problema não afeta o arquivo padrão do JavaScript disponível na CDN. Uma correção está em andamento.

## Versão 2.27.0 - quarta-feira, 20 de maio de 2025

**Correções e melhorias**

- Correção de um problema com mensagens no aplicativo em que o estilo personalizado não era aplicado corretamente.
- Alteração do formato do histórico de eventos. Isso fará com que mensagens no aplicativo e cartões de conteúdo sejam exibidos novamente conforme os dados antigos do histórico são excluídos.
- Correção de um problema em que as apresentações eram reaplicadas em casos de uso de SPA.
- Correção de um problema com o rastreamento de cliques em elementos DOM sombra.

## Versão 2.26.0 - 5 de março de 2025

**Novos recursos**

- Agora você pode usar o pacote NPM do Web SDK para criar builds personalizados do Web SDK e selecionar apenas os componentes de biblioteca necessários. Isso reduz o tamanho da biblioteca e os tempos de carregamento otimizados. Consulte a documentação sobre como [criar uma compilação personalizada do Web SDK usando o pacote NPM](install/create-custom-build.md).
- O comando [`getIdentity`](commands/getidentity.md) agora lê automaticamente a ECID diretamente do cookie de identidade `kndctr`. Se você chamar `getIdentity` com o namespace `ECID` e já houver um cookie de identidade, o Web SDK não fará mais uma solicitação à Edge Network para obter a identidade. Agora, ele lê a identidade do cookie.

**Correções e melhorias**

- Correção de um problema em que os comandos `getIdentity` não retornavam a identidade após o envio de uma chamada `collect`.
- Correção de um problema em que os redirecionamentos de personalização causavam oscilação de conteúdo antes de o redirecionamento ocorrer.

## Versão 2.25.0 - sexta-feira, 23 de janeiro de 2025

**Correções e melhorias**

- Adicionada validação de opção ao comando `setDebug`.
- Adicionado um aviso ao configurar uma função `onBeforeLinkClickSend` ou um qualificador de link de download quando a coleção de cliques está desabilitada.
- Correção de um problema em que as apresentações renderizadas não eram incluídas nas notificações de exibição.

**Novos recursos**

- Implementação de um fallback para o domínio configurado do Edge quando cookies de terceiros são ativados e as solicitações para adobedc.demdex.net são bloqueadas.

## Versão 2.24.1 - sábado, 6 de dezembro de 2024

**Correções e melhorias**

- Solução de um problema de dependência relacionado ao [Mecanismo de regras do Adobe Experience Platform](https://github.com/adobe/aepsdk-rulesengine-typescript/), que estava causando erros em algumas integrações de clientes. O Web SDK agora exige o [Mecanismo de Regras do Adobe Experience Platform](https://github.com/adobe/aepsdk-rulesengine-typescript/) versão 2.0.3 ou posterior.

## Versão 2.24.0 - sexta-feira, 31 de outubro de 2024

**Novos recursos**

- Agora há suporte para [substituições de sequência de dados](../datastreams/overrides.md) ao iniciar sessões de mídia.

- Adição de suporte para tokens de resposta do Adobe Target no [`onContentRendering`](monitoring-hooks.md#onContentRendering)gancho de monitoramento.

**Correções e melhorias**

- Quando várias mensagens no aplicativo são retornadas, somente a mensagem com a maior prioridade é exibida. Os outros são registrados como suprimidos.
- Substituições vazias de sequências de dados não são mais enviadas para o Edge Network, reduzindo possíveis conflitos com as configurações de roteamento do lado do servidor.
- Os seguintes nomes de componentes da mensagem de registro foram renomeados para, para alinhar com outros SDKs da Adobe:
   - `DecisioningEngine` foi renomeado para `RulesEngine`
   - `LegacyMediaAnalytics` foi renomeado para `MediaAnalyticsBridge`
   - `Privacy` foi renomeado para `Consent`
- Correção de um erro que ocorria quando itens de conteúdo padrão eram renderizados via [`applyPropositions`](../web-sdk/commands/applypropositions.md).
- Correção de um erro CSS nas ações de movimentação e redimensionamento do Adobe Target.
- A chave `machineLearning` foi removida das respostas [`sendEvent`](../web-sdk/commands/sendevent/overview.md).

## Versão 2.23.0 - 19 de setembro de 2024

**Novos recursos**

- Adicionado suporte para a solicitação da [ID PRINCIPAL](identity/overview.md#tracking-coreid-web-sdk) no comando [getIdentity](commands/getidentity.md#get-identity-using-the-web-sdk-javascript-library).

**Correções e melhorias**

- Correção de um problema em que os cookies não eram gravados corretamente ao executar o Web SDK localmente.

## Versão 2.22.0 - 22 de agosto de 2024

**Novos recursos**

- Adição de suporte para ganchos de monitoramento de personalização.

**Correções e melhorias**

- Remoção do suporte ao Internet Explorer, reduzindo o tamanho do gzip da biblioteca em 9%.
- Correção de um problema em que os detalhes do link do Activity Map não eram inicializados quando o gancho do monitor `onInstanceConfigured` era chamado.
- Correção de um problema em que os destinos de cookies não eram definidos com o caminho correto.
- Correção de um problema do cliente com a chamada para o tem.
- Correção de um problema em que uma codificação de URL inválida no parâmetro `adobe_mc` causava a falha das chamadas [sendEvent](commands/sendevent/overview.md).

## Versão 2.21.1 - sexta-feira, 18 de julho de 2024

**Correções e melhorias**

- Correção de um erro de build ao usar a biblioteca NPM.

## Versão 2.21.0 - quarta-feira, 16 de julho de 2024

**Novos recursos**

- Adição de suporte para rastreamento automático de interação de apresentação.
- Adição de um script de construção personalizado que fornece um arquivo alloy.js.
- Melhoria na coleção de cliques com o suporte ao ActivityMap e ao agrupamento de eventos.

## Versão 2.20.0 - quarta-feira, 21 de maio de 2024

**Novos recursos**

- Adicionado suporte para [Coleção de mídia de streaming](../web-sdk/commands/configure/streamingmedia.md).

**Correções e melhorias**

- Correção de um bug que fazia com que o conteúdo padrão ficasse oculto pelo trecho pré-ocultação quando o consentimento era recusado.

## Versão 2.19.2 - quinta-feira, 10 de janeiro de 2024

**Correções e melhorias**

- Correção de um problema em que os erros de identidade mascaravam outros erros e alteravam os erros de identidade para avisos.
- Correção de um problema em que a parte inferior das chamadas de página nunca era enviada quando havia uma chamada de parte superior da página com `renderDecisions` definido como `false`.
- Correção de um problema em que o Web SDK não lia identidades entre domínios quando havia vários parâmetros da cadeia de caracteres de consulta `adobe_mc`.

## Versão 2.19.1 - sábado, 10 de novembro de 2023

**Correções e melhorias**

- Correção de um problema em que a matriz de apresentações retornada das chamadas `sendEvent` estava sempre vazia.

## Versão 2.19.0 - quinta-feira, 1 de novembro de 2023

**Novos recursos**

- Adição de suporte para renderização de mensagens no aplicativo do Adobe Journey Optimizer.
- Adicionado suporte para [eventos de início e fim de página](use-cases/top-bottom-page-events.md).
- Adicionada a opção [`defaultPersonalizationEnabled`](commands/sendevent/personalization.md) ao comando `sendEvent` para controlar a solicitação do escopo da página e da superfície padrão.

**Correções e melhorias**

- A personalização combinada exibe eventos juntos ao renderizar vários tipos de personalização.
- Correção de um problema em que os nomes de exibição do aplicativo de página única diferenciavam maiúsculas de minúsculas.
- Correção de um problema com seletores de oferta personalizados DOM sombra.

## Versão 2.18.0 - terça-feira, 31 de julho de 2023

**Novos recursos**

- Adicionado suporte para [substituições por comando da ID de sequência de dados](../datastreams/overrides.md).

**Correções e melhorias**

- Correção de um problema em que os links de saída falhavam ao serem qualificados devido ao domínio fazer parte da consulta.
- `edgeConfigId` substituído em favor de `datastreamId` na configuração do Web SDK.

## Versão 2.17.0 - quinta-feira, 17 de maio de 2023

**Correções e melhorias**

- O Web SDK agora codifica os valores de destino do cookie do Audience Manager, semelhante ao [Data Integration Library (DIL)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html?lang=pt-BR).

## Versão 2.16.0 - 25 de abril de 2023

**Novos recursos**

- Adicionado suporte para [substituições de configuração de sequência de dados](../datastreams/overrides.md).

## Versão 2.15.0 - 30 de março de 2023

**Novos recursos**

- Adicionado suporte para retorno de chamada de clique de link [`onBeforeLinkClickSend`](/help/web-sdk/commands/configure/onbeforelinkclicksend.md).
- Adição de suporte para o rastreamento de cliques do Adobe Journey Optimizer.

**Correções e melhorias**

- A coleção de links agora inclui o nome do link e a região do visitante.
- Remoção do erro de console para destinos de URL com falha.

## Versão 2.14.0 - quinta-feira, 25 de janeiro de 2023

- (Beta) Adição de suporte para superfícies e apresentações do Adobe Journey Optimizer.

**Correções e melhorias**

- Correção de um problema com ações de código personalizado do Adobe Target VEC em que o código era inserido em um local alternativo em vez de [!DNL at.js].
- Correção de um problema em que, em alguns casos, o cabeçalho &quot;referenciador&quot; não era definido corretamente em solicitações para o Edge Network.
- Correção de um problema em que as propriedades da [dica do cliente de agente do usuário](/help/web-sdk/use-cases/client-hints.md) podiam ser definidas como um tipo incorreto.
- Correção de um problema em que `placeContext.localTime` não correspondia ao esquema.

## Versão 2.13.1 - sexta-feira, 13 de outubro de 2022

- Correção de um problema em que a migração de visitantes não funcionava se window.Visitor fosse definido após a configuração. Esse problema ocorre principalmente ao executar com tags do Adobe.
- Correção de um problema em que `device.screenWidth` e `device.screenHeight` eram preenchidos como cadeias de caracteres em alguns ambientes.

## Versão 2.13.0 - 28 de setembro de 2022

**Novos recursos**

- Adicionado suporte para [Página por Migração Completa de Página](home.md#migrating-to-web-sdk). O perfil do Adobe Target agora será preservado à medida que um visitante se move entre as páginas da at.js e do Web SDK.
- Adição de suporte configurável para [User-Agent Client Hints de alta entropia](/help/web-sdk/use-cases/client-hints.md).
- Suporte adicionado para o comando [`applyResponse`](/help/web-sdk/commands/applyresponse.md). Isso habilita a personalização híbrida através da [API do Edge Network](https://developer.adobe.com/data-collection-apis/docs/api/).
- Os links do modo de controle de qualidade agora funcionam em várias páginas.

**Correções e melhorias**

- Correção de um problema em que as métricas de rastreamento de cliques de personalização não eram atualizadas quando o rastreamento de link era desativado.
- Comandos atualizados para gerar um erro de validação quando opções desconhecidas forem especificadas.
- A propriedade `_experience.decisioning.propositionEventType` agora é preenchida ao enviar automaticamente eventos de personalização de exibição e interação.
- Adicionada validação de namespace duplicada para o comando `getIdentity`.
- Adição da validação do escopo de decisão duplicado para o comando `sendEvent`.

## Versão 2.12.0 - quinta-feira, 29 de junho de 2022

- Altere as solicitações para o Edge Network para usar a dica de localização do cookie `cluster` como parte da URL. Isso garante que os usuários que mudam de localização (por exemplo, por meio de uma VPN ou ao dirigir com dispositivos móveis etc.) no meio da sessão atinjam a mesma borda e tenham o mesmo perfil de personalização.
- Restrinja as funções configuradas na resposta do comando getLibraryInfo.

## Versão 2.11.0 - terça-feira, 13 de junho de 2022

**Novos recursos**

- Agora é possível fornecer experiências personalizadas com mais precisão, compartilhando IDs de visitante entre aplicativos móveis e conteúdo da Web móvel, e entre domínios. Consulte a [documentação dedicada](identity/id-sharing.md) para saber mais.
- Agora é possível renderizar ou executar uma matriz de propostas de [!DNL Adobe Target] em aplicativos de página única, sem incrementar as métricas de análise. Isso reduz os erros de relatório e aumenta a precisão da análise. Consulte a [documentação dedicada](personalization/rendering-personalization-content.md#applypropositions) para saber mais.
- Adição de mais informações ao comando `getLibraryInfo`, incluindo os comandos disponíveis e a configuração final da instância.

**Correções e melhorias**

- Atualização das configurações de cookie para usar o sinalizador `sameSite="none"` e `secure` em [!DNL HTTPS] páginas.
- Correção de um problema em que o conteúdo personalizado não era aplicado corretamente ao usar o pseudoseletor `eq`.
- Correção de um problema em que `localTimezoneOffset` poderia falhar na validação do Experience Platform.

## Versão 2.10.1 - quarta-feira, 3 de maio de 2022

- Correção de um problema em que vários iframes persistentes eram criados para sincronizações de ID e destinos de segmento.

## Versão 2.10.0 - 22 de abril de 2022

- Use um iframe persistente para todas as sincronizações de ID e destinos de segmentos.
- Correção de um problema em que as propostas de métricas mescladas eram duplicadas no resultado `sendEvent`.

## Versão 2.9.0 - 10 de março de 2022

- Adicionado suporte para rastrear [!DNL control (default)] experiências do Adobe Target.
- Otimização dos eventos de alteração de visualização para aplicativos de página única. A notificação de exibição agora é incluída no evento de alteração de visualização quando as experiências personalizadas são renderizadas.
- Removido o aviso do console quando nenhum `eventType` estiver presente.
- Correção de um problema em que a propriedade `propositions` era retornada somente de um comando `sendEvent` quando as experiências eram solicitadas ou recuperadas do cache. A propriedade `propositions` agora sempre será definida como uma matriz.
- Correção de um problema em que os contêineres ocultos não eram exibidos quando um erro era retornado da Edge Network.
- Correção de um problema em que os eventos interativos não eram contados no Adobe Target. Isso foi corrigido adicionando o nome da exibição ao XDM em web.webPageDetails.viewName.
- Corrigir links de documentação corrompidos nas mensagens do console.

## Versão 2.8.0 - quinta-feira, 19 de janeiro de 2022

- Seletores DOM de sombra compatíveis com personalização.
- Tipos de evento de personalização renomeados. (`display` e `click` tornam-se `decisioning.propositionDisplay` e `decisioning.propositionInteract`)
- Correção de um problema em que as ofertas do HTML com tags de script integradas adicionavam as tags de script duas vezes à página, mesmo que o script fosse executado apenas uma vez.

## Versão 2.7.0 - quarta-feira, 26 de outubro de 2021

- Exponha informações adicionais da Edge Network no valor de retorno de `sendEvent`, incluindo `inferences` e `destinations`. O formato dessas propriedades pode mudar, pois esses recursos estão sendo lançados como parte de uma Beta.

## Versão 2.6.4 - 7 de setembro de 2021

- Correção de um problema em que as ações definidas do HTML Adobe Target aplicadas ao elemento `head` substituíam todo o conteúdo `head`. Agora, as ações de definição do HTML aplicadas ao elemento `head` são alteradas para anexar o HTML.

## Versão 2.6.3 - 16 de agosto de 2021

- Correção de um problema em que objetos não destinados a uso público eram expostos por meio da promessa resolvida do comando `configure`.

## Versão 2.6.2 - 4 de agosto de 2021

- Correção de um problema em que um aviso sobre a descontinuação de `result.decisions` (fornecido pelo comando `sendEvent`) seria registrado no console mesmo quando a propriedade `result.decisions` não estava sendo acessada. Nenhum aviso será registrado ao acessar a propriedade `result.decisions`, mas a propriedade ainda está obsoleta.

## Versão 2.6.1 - sexta-feira, 29 de julho de 2021

- Correção de um problema em que a personalização de renderização para uma exibição de aplicativo de página única sem conteúdo de personalização gerava um erro e fazia com que a promessa retornada do comando `sendEvent` fosse rejeitada.

## Versão 2.6.0 - quarta-feira, 27 de julho de 2021

- Fornece mais conteúdo de personalização na promessa resolvida `sendEvent`, incluindo tokens de resposta do Adobe Target. Quando o comando `sendEvent` é executado, uma promessa é retornada, que é eventualmente resolvida com um objeto `result` contendo informações recebidas do servidor. Anteriormente, este objeto de resultado incluía uma propriedade chamada `decisions`. Esta propriedade `decisions` foi preterida. Uma nova propriedade `propositions` foi adicionada. Esta nova propriedade fornece aos clientes acesso a mais conteúdo de personalização, incluindo [tokens de resposta](/help/web-sdk/personalization/adobe-target/accessing-response-tokens.md).

## Versão 2.5.0 - junho de 2021

- Adição de suporte para ofertas de personalização de redirecionamento.
- As larguras e alturas do visor coletadas automaticamente que são valores negativos não serão mais enviadas para o servidor.
- Quando um evento é cancelado ao retornar `false` de um retorno de chamada `onBeforeEventSend`, uma mensagem é registrada.
- Correção de um problema em que dados XDM específicos destinados a um único evento eram incluídos em vários eventos.

## Versão 2.4.0 - março de 2021

- O SDK agora pode ser instalado como um [pacote NPM](/help/web-sdk/install/npm.md).
- Adicionado suporte para uma opção `out` ao [configurar o consentimento padrão](/help/web-sdk/commands/configure/defaultconsent.md), que descarta todos os eventos até que o consentimento seja recebido (a opção `pending` existente enfileira eventos e os envia quando o consentimento é recebido).
- O retorno de chamada [`onBeforeEventSend`](/help/web-sdk/commands/configure/onbeforeeventsend.md) agora pode ser usado para impedir que um evento seja enviado.
- Agora usa um grupo de campos de esquema XDM em vez de `meta.personalization` ao enviar eventos sobre conteúdo personalizado que está sendo renderizado ou clicado.
- O comando [`getIdentity`](/help/web-sdk/commands/getidentity.md) agora retorna a ID da região da borda ao lado da identidade.
- Os avisos e erros recebidos do servidor foram aprimorados e são tratados de maneira mais apropriada.
- Adição de suporte ao padrão Consentimento 2.0 da Adobe para o comando [`setConsent`](/help/web-sdk/commands/setconsent.md).
- As preferências de consentimento, quando recebidas, são colocadas em hash e armazenadas no armazenamento local para uma integração otimizada entre CMPs, Experience Platform Web SDK e Experience Platform Edge Network. Se você estiver coletando preferências de consentimento, agora recomendamos que ligue para `setConsent` em cada carregamento de página.
- Dois [ganchos de monitoramento](https://github.com/adobe/alloy/wiki/Monitoring-Hooks), `onCommandResolved` e `onCommandRejected` foram adicionados.
- Correção de erros: os eventos de notificação de interação do Personalization conteriam informações duplicadas sobre a mesma atividade quando um usuário navegasse para uma nova exibição de aplicativo de página única, voltasse para a exibição original e clicasse em um elemento qualificado para conversão.
- Correção de erros: se o primeiro evento enviado pelo SDK tivesse `documentUnloading` definido como `true`, [`sendBeacon`](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/sendBeacon) seria usado para enviar o evento, resultando em um erro em relação a uma identidade que não está sendo estabelecida.

## Versão 2.3.0 - novembro de 2020

- Adição de suporte ao nonce para permitir políticas mais rigorosas de segurança de conteúdo.
- Adição de suporte de personalização para aplicativos de página única.
- Aprimoramento de compatibilidade com outro código JavaScript na página que pode estar substituindo as APIs `window.console`.
- Correção de erros: `sendBeacon` não estava sendo usado quando `documentUnloading` estava definido como `true` ou quando os cliques em links eram rastreados automaticamente.
- Correção de erros: um link não seria rastreado automaticamente se o elemento de ancoragem tivesse conteúdo do HTML.
- Correção de erros: determinados erros do navegador contendo uma propriedade `message` somente leitura não foram tratados adequadamente, resultando em um erro diferente sendo exposto ao cliente.
- Correção de erros: executar o SDK em um iframe resultaria em um erro se a página do HTML do iframe fosse de um subdomínio diferente da página do HTML da janela principal.

## Versão 2.2.0 - outubro de 2020

- Correção de erros: o objeto de aceitação estava impedindo que o Web SDK fizesse chamadas quando `idMigrationEnabled` fosse `true`.
- Correção de erros: torne o Web SDK ciente das solicitações que devem retornar ofertas de personalização para evitar um problema de oscilação.

## Versão 2.1.0 - agosto de 2020

- Remova o comando `syncIdentity` e ofereça suporte à transmissão dessas IDs no comando `sendEvent`.
- Suporte ao Padrão de consentimento IAB 2.0.
- Suporte à transmissão de IDs adicionais no comando `setConsent`.
- Suporte à substituição de `datasetId` no comando `sendEvent`.
- Ganchos de Monitoramento de Suporte ([Leia mais](https://github.com/adobe/alloy/wiki/Monitoring-Hooks))
- Passar `environment: browser` nos dados de contexto de detalhes da implementação.
