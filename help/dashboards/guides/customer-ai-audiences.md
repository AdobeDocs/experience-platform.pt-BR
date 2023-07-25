---
title: Widgets da IA do cliente do painel de públicos
description: Saiba como a IA do cliente fornece insights importantes sobre churn ou propensão dos públicos-alvo de perfil do cliente em tempo real da sua organização.
hide: true
hidefromtoc: true
source-git-commit: e14067606e4c4868c926433129d835c7b0a7a18f
workflow-type: tm+mt
source-wordcount: '710'
ht-degree: 2%

---

# Widgets da IA do cliente do painel de públicos {#customer-ai-audiences-widgets}

o Customer AI é usado para gerar pontuações de propensão personalizadas, como churn e conversão para perfis individuais em escala. A IA do cliente faz isso analisando dados existentes do Evento de experiência do consumidor para prever pontuações de churn ou propensão de conversão. Esses modelos de propensão de alta precisão do cliente permitem segmentação e direcionamento mais exatos. A variável [distribuição de pontuações](#customer-ai-distribution-of-scores) e [resumo de pontuação](#customer-ai-scoring-summary) os insights demonstram a divisão no público-alvo. Eles destacam quais perfis são a propensão alta/baixa/média e como eles são distribuídos na contagem de perfis.

<!-- 
THe links when required
* [[!UICONTROL Customer AI scoring summary]](#customer-ai-scoring-summary)
* [[!UICONTROL Customer AI distribution of scores]](#customer-ai-distribution-of-scores) 
-->

## [!UICONTROL Distribuição de pontuações da IA do cliente] {#customer-ai-distribution-of-scores}

A variável [!UICONTROL Distribuição de pontuações da IA do cliente] O widget categoriza o número total de perfis por suas pontuações de propensão. A distribuição da contagem de perfis é determinada pelo modelo de IA e pela política de mesclagem selecionada e, em seguida, visualizada em incrementos de cinco por cento que indicam sua propensão. A propensão do perfil é codificada por cores em alto, médio e baixo, como verde, amarelo e vermelho, respectivamente. A contagem de perfis é fornecida ao longo do eixo Y e as pontuações de propensão são fornecidas ao longo do eixo X.

O modelo de IA que determina as pontuações de propensão é escolhido no seletor suspenso sob o título do widget. A lista suspensa contém uma lista de todos os modelos configurados da IA do cliente. Selecione o modelo de IA apropriado para sua análise na lista de modelos disponíveis. Se nenhum modelo de IA do cliente estiver disponível, uma mensagem no widget o direcionará para configurar pelo menos um modelo de IA do cliente e fornecerá um hiperlink para a página Configuração do modelo de IA do cliente. Consulte a documentação para obter instruções sobre [como configurar uma instância da IA do cliente](../../intelligent-services/customer-ai/user-guide/configure.md).

>[!NOTE]
>
>Selecione a lista suspensa imediatamente abaixo da guia de visão geral para alterar a política de mesclagem que determina quais perfis são incluídos na análise. Consulte a seção sobre [políticas de mesclagem](#merge-policies) para obter uma breve descrição, ou [visão geral da política de mesclagem](../../profile/merge-policies/overview.md) para obter mais detalhes.

Para navegar até a página de insights detalhados do modelo de IA do cliente selecionado, selecione **[!UICONTROL Exibir detalhes do modelo]**.

![O painel Públicos-alvo do Experience Platform com a [!UICONTROL Distribuição de pontuações da IA do cliente] widget e [!UICONTROL Exibir detalhes do modelo] destacado.](../images/segments/customer-ai-distribution-of-scores.png)

A página de insights detalhados do modelo é exibida.

![A página de insights da IA do cliente.](../images/profiles/customer-ai-insights-page.png)

Mais informações sobre a IA do cliente podem ser encontradas no [guia da interface do usuário do discover insights](../../intelligent-services/customer-ai/user-guide/discover-insights.md).

## [!UICONTROL Resumo de pontuação do Customer AI] {#customer-ai-scoring-summary}

Este widget exibe o número total de perfis pontuados e os categoriza em compartimentos que contêm alta, média e baixa propensão como verde, amarelo e vermelho, respectivamente. Um gráfico de rosca é usado para ilustrar a composição proporcional dos perfis totais entre propensões alta, média e baixa como verde, amarelo e vermelho, respectivamente. Um perfil se qualifica para alta propensão acima de 75, média propensão entre 25 e 74 e baixa propensão abaixo de 24. Uma legenda indica o código de cor e os limites de propensões. As contagens de perfil para as tendências alta, média e baixa são exibidas em uma caixa de diálogo quando o cursor passa o mouse sobre a respectiva seção do gráfico de rosca.

>[!NOTE]
>
>Se a visualização for uma pontuação de propensão de conversão, as pontuações mais altas serão exibidas em verde e as pontuações mais baixas em vermelho. Se você estiver prevendo a propensão de churn, ela será invertida, as pontuações mais altas estarão em vermelho e as pontuações mais baixas em verde. O intervalo médio permanece amarelo, independentemente do tipo de propensão escolhido.

O menu suspenso abaixo do título do widget fornece uma lista de todos os modelos configurados da IA do cliente. Selecione o modelo de IA apropriado para sua análise na lista de modelos disponíveis. Se nenhum modelo de IA do cliente estiver disponível, uma mensagem no widget o direcionará para configurar pelo menos um modelo de IA do cliente e fornecerá um hiperlink para a página Configuração do modelo de IA do cliente. Consulte a documentação em [como configurar uma instância da IA do cliente](../../intelligent-services/customer-ai/user-guide/configure.md) para obter instruções detalhadas.

>[!NOTE]
>
>O número total de perfis calculados depende da política de mesclagem escolhida. Para alterar a política de mesclagem usada, selecione a lista suspensa imediatamente abaixo da guia de visão geral. Consulte a seção sobre [políticas de mesclagem](#merge-policies) para obter uma breve descrição, ou [visão geral da política de mesclagem](../../profile/merge-policies/overview.md) para obter mais detalhes.

![O painel Públicos-alvo do Experience Platform com o widget de resumo de pontuação da IA do cliente é realçado.](../images/segments/customer-ai-scoring-summary.png)

Selecionar **[!UICONTROL Exibir detalhes do modelo]** para navegar até a página de insights detalhados do modelo de IA do cliente selecionado. Mais informações sobre a IA do cliente podem ser encontradas no [guia da interface do usuário do discover insights](../../intelligent-services/customer-ai/user-guide/discover-insights.md).
