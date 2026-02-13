---
title: Visão geral dos casos de uso do Personalization
description: Saiba como implementar casos de uso de personalização usando o Adobe Experience Platform Web SDK, incluindo padrões para renderização de conteúdo e rastreamento de exibição.
keywords: personalização;enviarEvento;renderizarDecisões;aplicarPropositions;decisionScopes;exibir eventos;cintilação;
exl-id: 6beccbfd-fddb-4e19-8a56-caba276e1643
source-git-commit: caaf5cad7276d6429fbbf35585fd4845de6ff60c
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 0%

---

# Visão geral dos casos de uso do Personalization

O Adobe Experience Platform Web SDK permite uma grande variedade de casos de uso de personalização para propriedades da Web. Ele oferece suporte a arquiteturas flexíveis (lado do cliente, lado do servidor e híbrido) para que você possa solicitar decisões e renderizar conteúdo de maneiras que correspondam às necessidades do seu site.

## Renderizar conteúdo personalizado

O Web SDK pode recuperar decisões de personalização (também conhecidas como _propostas_) e ajudar você a renderizá-las na página. A renderização é assíncrona, portanto, evite assumir um tempo específico para quando o conteúdo é aplicado.

Escolha o padrão que corresponde aos itens de proposta recebidos:

1. **Renderizar automaticamente propostas de ação DOM**: use quando as propostas incluírem `dom-action` itens com seletores e tipos de ação que o Web SDK pode aplicar automaticamente. Consulte [Renderizar automaticamente propostas de ação DOM](render-auto-pers-content.md).
1. **Renderizar ofertas do HTML sem seletores usando applyPropositions**: use quando receber conteúdo do HTML, mas deverá fornecer onde e como aplicá-lo (seletor + tipo de ação) por meio de metadados. Consulte [Renderizar ofertas do HTML sem seletores](render-html-offers.md).
1. **Renderizar apresentações manualmente**: use quando precisar de controle total sobre a lógica de renderização (por exemplo, composição de interface do usuário do JSON ou aplicação de regras de negócios personalizadas). Consulte [Renderizar apresentações manualmente](render-manual-propositions.md).

>[!TIP]
>
>Esses padrões podem ser combinados. Por exemplo, você pode ativar a renderização automática de ação DOM e também renderizar manualmente o conteúdo de escopos de decisão específicos.

## Tópicos complementares comuns

A maioria das implementações de personalização envolve estes tópicos comuns:

* **Impedir cintilação** (opcional): ocultar e revelar contêineres durante a personalização. Consulte [Gerenciar cintilação](manage-flicker.md).
* **Rastrear o que foi exibido**: registre eventos de exibição para o conteúdo renderizado. Consulte [Gerenciar eventos de exibição](display-events.md).
* **Busca do topo da página/métricas do fim da página**: solicite decisões antecipadamente e inclua medições posteriormente. Consulte [Configurar os eventos de início e fim da página](top-bottom-page-events.md).

## Amostras do Web SDK

Além das páginas de documento nessa pasta, o Adobe mantém um repositório de aplicativos de amostra que podem ser referenciados. Consulte [amostras do Web SDK](https://github.com/adobe/alloy-samples/) no GitHub para ver cenários de personalização adicionais, incluindo:

* Personalização do lado do cliente
* Personalização do lado do servidor
* Personalização híbrida
* Personalization em aplicativos de página única
