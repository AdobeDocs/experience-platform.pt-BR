---
title: Notas de versão do SDK da Web da Adobe Experience Platform
description: As notas de versão mais recentes do SDK da Web da Adobe Experience Platform.
keywords: Adobe Experience Platform Web SDK; Plataforma Web SDK; Web SDK; Notas de versão;
exl-id: efd4e866-6a27-4bd5-af83-4a97ca8adebd
source-git-commit: 29852bc8f17de6db04805f4738f383f2dc7c1406
workflow-type: tm+mt
source-wordcount: '1018'
ht-degree: 3%

---

# Notas de versão

## Versão 2.10.1 - 3 de maio de 2022

* Correção de um problema em que vários iframes persistentes eram criados para sincronizações de ID e destinos de segmentos.

## Versão 2.10.0 - 22 de abril de 2022

* Use um iframe persistente para todas as sincronizações de IDs e destinos de segmentos.
* Correção de um problema em que as apresentações de métricas mescladas eram duplicadas na variável `sendEvent` resultado.

## Versão 2.9.0 - 10 de março de 2022

* Adição de suporte para rastreamento [!DNL control (default)] Experiências Adobe Target.
* Otimização dos eventos de alteração de exibição para aplicativos de página única. A notificação de exibição agora é incluída no evento view-change quando experiências personalizadas são renderizadas.
* Remoção do aviso do console quando não há `eventType` está presente.
* Correção de um problema em que a função `propositions` A propriedade só foi retornada de um `sendEvent` quando as experiências foram solicitadas ou recuperadas do cache. O `propositions` Agora, a propriedade sempre será definida como uma matriz.
* Correção de um problema em que contêineres ocultos não eram mostrados quando havia um erro retornado do Adobe Experience Edge.
* Correção de um problema em que os eventos interativos não eram contados no Adobe Target. Isso foi corrigido adicionando o nome de exibição ao XDM em web.webPageDetails.viewName.
* Corrigir links de documentação quebrados nas mensagens do console.

## Versão 2.8.0 - 19 de janeiro de 2022

* Oferece suporte a seletores DOM de sombra para personalização.
* Tipos de evento de personalização renomeados. (`display` e `click` become `decisioning.propositionDisplay` e `decisioning.propositionInteract`)
* Correção de um problema em que as ofertas HTML com tags de script em linha adicionavam as tags de script duas vezes à página, mesmo que o script fosse executado apenas uma vez.

## Versão 2.7.0 - 26 de outubro de 2021

* Exponha informações adicionais do Experience Edge no valor de retorno de `sendEvent`, incluindo `inferences` e `destinations`. O formato dessas propriedades pode mudar, pois esses recursos estão sendo lançados como parte de um Beta. Para obter mais informações, consulte [Rastreamento de eventos.](fundamentals/tracking-events.md)

## Versão 2.6.4 - 7 de setembro de 2021

* Correção de um problema em que definir ações de HTML Adobe Target aplicadas ao `head` estavam substituindo todo o `head` conteúdo. Agora, defina as ações de HTML aplicadas ao `head` são alteradas para anexar HTML.

## Versão 2.6.3 - 16 de agosto de 2021

* Correção de um problema em que os objetos não destinados ao uso público eram expostos por meio da promessa resolvida do `configure` comando.

## Versão 2.6.2 - 4 de agosto de 2021

* Correção de um problema em que um aviso sobre a desativação de `result.decisions` (fornecido pelo `sendEvent` ) seria registrado no console mesmo quando a variável `result.decisions` não estava sendo acessada. Nenhum aviso será registrado ao acessar a variável `result.decisions` , mas a propriedade ainda está obsoleta.

## Versão 2.6.1 - 29 de julho de 2021

* Correção de um problema em que a renderização da personalização para uma visualização de aplicativo de página única que não tem conteúdo de personalização gerava um erro e causava a promessa retornada do `sendEvent` comando a ser rejeitado.

## Versão 2.6.0 - 27 de julho de 2021

* Fornece mais conteúdo de personalização no `sendEvent` promessa resolvida, incluindo tokens de resposta do Adobe Target. Quando a variável `sendEvent` for executado, uma promessa será retornada, o que eventualmente será resolvido com uma `result` objeto contendo informações recebidas do servidor. Anteriormente, esse objeto de resultado incluía uma propriedade chamada `decisions`. Essa `decisions` foi substituída. Uma nova propriedade, `propositions`, foi adicionado. Essa nova propriedade fornece aos clientes acesso a mais conteúdo de personalização, incluindo [tokens de resposta](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/accessing-response-tokens.html).

## Versão 2.5.0 - junho de 2021

* Adição de suporte para ofertas de personalização de redirecionamento.
* As larguras e alturas do visor coletadas automaticamente que sejam valores negativos não serão mais enviadas para o servidor.
* Quando um evento é cancelado ao retornar `false` de um `onBeforeEventSend` retorno de chamada, uma mensagem é registrada.
* Correção de um problema em que partes específicas de dados XDM destinadas a um único evento eram incluídas em vários eventos.

## Versão 2.4.0 - março de 2021

* O SDK agora pode ser [instalado como um pacote npm](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/installing-the-sdk.html?lang=pt-BR).
* Suporte adicionado para um `out` opção ao [configuração do consentimento padrão](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#default-consent), que elimina todos os eventos até que o consentimento seja recebido (o `pending` ). Enfileira eventos e os envia após o recebimento do consentimento.
* O [Retorno de chamada onBeforeEventSend](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#onbeforeeventsend) agora pode ser usada para impedir que um evento seja enviado.
* Agora usa um grupo de campos do esquema XDM em vez de `meta.personalization` ao enviar eventos sobre o conteúdo personalizado que está sendo renderizado ou clicado.
* O [comando getIdentity](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html#retrieving-the-visitor-id) agora retorna a ID da região de borda ao lado da identidade.
* Os avisos e erros recebidos do servidor foram aprimorados e são tratados de forma mais apropriada.
* Suporte adicionado para [Adobe 2.0](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html?communicating-consent-preferences-via-the-adobe-standard).
* As preferências de consentimento, quando recebidas, são armazenadas em hash e no armazenamento local para uma integração otimizada entre CMPs, SDK da Web da plataforma e Rede de borda da plataforma. Se você estiver coletando preferências de consentimento, agora incentivamos você a chamar `setConsent` em cada carregamento de página.
* Dois [anzóis de monitoramento](https://github.com/adobe/alloy/wiki/Monitoring-Hooks), `onCommandResolved` e `onCommandRejected`, foram adicionadas.
* Correção de erros: Os eventos de notificação de interação de personalização conteriam informações duplicadas sobre a mesma atividade quando um usuário navegasse para uma nova visualização de aplicativo de página única, voltasse para a visualização original e clicasse em um elemento qualificado para conversão.
* Correção de erros: Se o primeiro evento enviado pelo SDK tivesse `documentUnloading` defina como `true`, [`sendBeacon`](https://developer.mozilla.org/pt-BR/docs/Web/API/Navigator/sendBeacon) seria utilizado para enviar o evento, resultando num erro relativamente a uma identidade que não foi estabelecida.

## Versão 2.3.0 - novembro de 2020

* Adição de suporte nonce para permitir políticas de segurança de conteúdo mais rigorosas.
* Adição do suporte de personalização para aplicativos de página única.
* Compatibilidade aprimorada com outro código JavaScript na página que pode estar substituindo `window.console` APIs.
* Correção de erros: `sendBeacon` não estava sendo usado quando `documentUnloading` foi definido como `true` ou quando os cliques em links eram acompanhados automaticamente.
* Correção de erros: Um link não seria rastreado automaticamente se o elemento âncora contivesse conteúdo de HTML.
* Correção de erros: Certos erros de navegador contendo um somente leitura `message` não eram tratadas adequadamente, resultando em um erro diferente sendo exposto ao cliente.
* Correção de erros: A execução do SDK em um iframe resultaria em um erro se a página HTML do iframe fosse de um subdomínio diferente da página HTML da janela pai.

## Versão 2.2.0 - outubro de 2020

* Correção de erros: O objeto Opt-in estava impedindo o Alloy de efetuar chamadas quando `idMigrationEnabled` é `true`.
* Correção de erros: Informe Alloy sobre as solicitações que devem retornar ofertas de personalização para evitar um problema de cintilação.

## Versão 2.1.0 - agosto de 2020

* Remova o `syncIdentity` e suporte à transmissão dessas IDs no `sendEvent` comando.
* Suporte ao Padrão de consentimento IAB 2.0.
* Suporte à transmissão de IDs adicionais no `setConsent` comando.
* Suporte que substitui o `datasetId` no `sendEvent` comando.
* Monitores de Alloy de Suporte ([Leia mais](https://github.com/adobe/alloy/wiki/Monitoring-Hooks))
* Passar `environment: browser` nos dados de contexto de detalhes da implementação.
