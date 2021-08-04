---
title: Notas de versão do SDK da Web da Adobe Experience Platform
description: As notas de versão mais recentes do SDK da Web da Adobe Experience Platform.
keywords: Adobe Experience Platform Web SDK; Plataforma Web SDK; Web SDK; Notas de versão;
exl-id: efd4e866-6a27-4bd5-af83-4a97ca8adebd
source-git-commit: f3821176b0cbc4ad07fbd2e0e20caa1205324a44
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 4%

---

# Notas de versão

## Versão 2.6.2 - 4 de agosto de 2021

* Correção de um problema em que um aviso sobre a desativação de `result.decisions` (fornecido pelo comando `sendEvent`) era registrado no console mesmo quando a propriedade `result.decisions` não estava sendo acessada. Nenhum aviso será registrado ao acessar a propriedade `result.decisions`, mas a propriedade ainda está obsoleta.

## Versão 2.6.1 - 29 de julho de 2021

* Correção de um problema em que a renderização da personalização para uma visualização de aplicativo de página única que não tem conteúdo de personalização gerava um erro e fazia com que a promessa retornada do comando `sendEvent` fosse rejeitada.

## Versão 2.6.0 - 27 de julho de 2021

* Fornece mais conteúdo de personalização na promessa `sendEvent` resolvida, incluindo tokens de resposta do Adobe Target. Quando o comando `sendEvent` é executado, uma promessa é retornada, que é eventualmente resolvida com um objeto `result` contendo as informações recebidas do servidor. Anteriormente, esse objeto de resultado incluía uma propriedade chamada `decisions`. Esta propriedade `decisions` foi preterida. Uma nova propriedade, `propositions`, foi adicionada. Essa nova propriedade fornece aos clientes acesso a mais conteúdo de personalização, incluindo [tokens de resposta](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/accessing-response-tokens.html).

## Versão 2.5.0 - junho de 2021

* Adição de suporte para ofertas de personalização de redirecionamento.
* As larguras e alturas do visor coletadas automaticamente que sejam valores negativos não serão mais enviadas para o servidor.
* Quando um evento é cancelado retornando `false` de um retorno de chamada `onBeforeEventSend`, uma mensagem agora é registrada.
* Correção de um problema em que partes específicas de dados XDM destinadas a um único evento eram incluídas em vários eventos.

## Versão 2.4.0 - março de 2021

* O SDK agora pode ser [instalado como um pacote npm](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/installing-the-sdk.html?lang=pt-BR).
* Adição de suporte para uma opção `out` ao [configurar o consentimento padrão](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#default-consent), que elimina todos os eventos até o recebimento do consentimento (a opção `pending` existente enfileira os eventos e os envia depois que o consentimento é recebido).
* O retorno de chamada [onBeforeEventSend](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#onbeforeeventsend) agora pode ser usado para impedir o envio de um evento.
* Agora usa um grupo de campos do esquema XDM em vez de `meta.personalization` ao enviar eventos sobre o conteúdo personalizado que está sendo renderizado ou clicado.
* O [comando getIdentity](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html#retrieving-the-visitor-id) agora retorna a ID da região de borda ao lado da identidade.
* Os avisos e erros recebidos do servidor foram aprimorados e são tratados de forma mais apropriada.
* Adição de suporte para [Adobe Consent 2.0 standard](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html?communicating-consent-preferences-via-the-adobe-standard).
* As preferências de consentimento, quando recebidas, são armazenadas em hash e no armazenamento local para uma integração otimizada entre CMPs, SDK da Web da plataforma e Rede de borda da plataforma. Se você estiver coletando preferências de consentimento, agora incentivamos você a chamar `setConsent` em cada carregamento de página.
* Dois [ganchos de monitoramento](https://github.com/adobe/alloy/wiki/Monitoring-Hooks), `onCommandResolved` e `onCommandRejected` foram adicionados.
* Correção de erros: Os eventos de notificação de interação de personalização conteriam informações duplicadas sobre a mesma atividade quando um usuário navegasse para uma nova visualização de aplicativo de página única, voltasse para a visualização original e clicasse em um elemento qualificado para conversão.
* Correção de erros: Se o primeiro evento enviado pelo SDK tivesse `documentUnloading` definido como `true`, [`sendBeacon`](https://developer.mozilla.org/pt-BR/docs/Web/API/Navigator/sendBeacon) seria usado para enviar o evento, resultando em um erro em relação a uma identidade que não estava sendo estabelecida.

## Versão 2.3.0 - novembro de 2020

* Adição de suporte nonce para permitir políticas de segurança de conteúdo mais rigorosas.
* Adição do suporte de personalização para aplicativos de página única.
* Aprimorada a compatibilidade com outro código JavaScript na página que pode estar substituindo `window.console` APIs.
* Correção de erros: `sendBeacon` não estava sendo usado quando `documentUnloading` estava definido como `true` ou quando os cliques em links eram rastreados automaticamente.
* Correção de erros: Um link não seria rastreado automaticamente se o elemento da âncora contivesse conteúdo HTML.
* Correção de erros: Determinados erros do navegador que continham uma propriedade somente leitura `message` não eram tratados adequadamente, resultando em um erro diferente sendo exposto ao cliente.
* Correção de erros: A execução do SDK em um iframe resultaria em um erro se a página HTML do iframe fosse de um subdomínio diferente da página HTML da janela pai.

## Versão 2.2.0 - outubro de 2020

* Correção de erros: O objeto Opt-in estava bloqueando o Alloy de fazer chamadas quando `idMigrationEnabled` é `true`.
* Correção de erros: Informe Alloy sobre as solicitações que devem retornar ofertas de personalização para evitar um problema de cintilação.

## Versão 2.1.0 - agosto de 2020

* Remova o comando `syncIdentity` e suporte a transmissão dessas IDs no comando `sendEvent`.
* Suporte ao Padrão de consentimento IAB 2.0.
* Suporte à transmissão de IDs adicionais no comando `setConsent`.
* Suporte à substituição de `datasetId` no comando `sendEvent`.
* Suporte a Monitores de Alloy ([Leia mais](https://github.com/adobe/alloy/wiki/Monitoring-Hooks))
* Passe `environment: browser` nos dados de contexto dos detalhes da implementação.
