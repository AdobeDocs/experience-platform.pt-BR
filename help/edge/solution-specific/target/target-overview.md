---
title: 'O SDK da Web do Público alvo Adobe e da plataforma Adobe Experience. '
seo-title: Adobe Experience Platform Web SDK e uso do Público alvo da Adobe
description: Saiba como renderizar conteúdo personalizado com o Experience Platform Web SDK usando o Público alvo Adobe
seo-description: Saiba como renderizar conteúdo personalizado com o Experience Platform Web SDK usando o Público alvo Adobe
translation-type: tm+mt
source-git-commit: db4bfec04a1116ce2b6a0be7ca0e8cb2f9639ad6

---


# Visão geral do Público alvo

O SDK da Web da plataforma Adobe Experience é integrado ao Público alvo da Adobe por meio desse recurso [de](../../fundamentals/rendering-personalization-content.md) personalização e permite que você forneça conteúdo personalizado e decisões de forma simples.

## Ativação do Adobe Público alvo

Para ativar o Público alvo, é necessário fazer o seguinte:

- Ative o público alvo na sua configuração [de](../../fundamentals/edge-configuration.md) borda com o código de cliente apropriado.
- Adicione a `renderDecisions` opção aos seus eventos.

Em seguida, opcionalmente, você também pode:

- Adicione `scopes` aos seus eventos para recuperar atividades específicas (úteis para atividades criadas com o compositor baseado em formulário).
- Adicione o snippet de [pré-ocultação](../../fundamentals/managing-flicker.md) para ocultar apenas algumas partes da página.

## Uso do VEC

Com o SDK, você pode usar o VEC normalmente com uma exceção, você precisará da extensão [auxiliar VEC do](https://docs.adobe.com/content/help/en/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html) público alvo instalada e ativa.

## Uso do Criador baseado em forma

O compositor baseado em formulário também pode ser usado para retornar conteúdo. Os escopos aparecerão como locais (mBoxes) na interface do usuário do Público alvo. Além disso, verifique se o desenvolvedor está procurando as respostas se decidir usar escopos.

## Audiências no XDM

Dentro do Público alvo, os dados XDM serão exibidos no Construtor de Audiências como um parâmetro personalizado. O XDM é serializado usando a notação de pontos (por exemplo, `web.webPageDetails.name`)

## Terminologia

__Decisões__ - Em Público alvo, elas estão relacionadas à experiência selecionada de uma Atividade.

__Âmbito__ - Âmbito de aplicação da decisão. Em Público alvo, esta é a mBox. A mBox global é o `__view__` escopo.

__Schema__ - O schema de uma decisão é o tipo de oferta no Público alvo.

__XDM__ - o XDM é serializado em notação de pontos e colocado em Público alvo como parâmetros mBox.