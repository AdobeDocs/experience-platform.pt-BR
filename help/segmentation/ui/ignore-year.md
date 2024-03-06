---
solution: Experience Platform
title: Ignorar Atualização de Restrição de Tempo do Ano
description: Saiba como resolver um problema com a restrição de tempo ignorar ano.
source-git-commit: d0bd7990f0d77cd5f8d30da735b89c188e13c780
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 9%

---


# Ignorar atualização de restrição de tempo anual {#ignore-year}

>[!CONTEXTUALHELP]
>id="platform_audiences_segmentBuilder_ignoreYear"
>title="Ignorar atualização anual"
>abstract="A restrição ignorar tempo anual foi atualizada. Salve novamente o público-alvo."

A versão de fevereiro de 2024 do Adobe Experience Platform introduziu alterações no Serviço de segmentação do Adobe Experience Platform que soluciona um problema com a opção &quot;ignorar ano&quot; na criação e avaliação de públicos-alvo.

A opção &quot;ignorar ano&quot; foi projetada para ignorar o componente de ano de uma data ao executar avaliações de público-alvo. Você pode usar essa opção em situações em que a relação temporal entre eventos diferentes é importante, mas o ano específico não é importante, como um campo de data de nascimento.

No entanto, durante os anos bissextos, como 2024, o sistema subjacente não conseguiu lidar adequadamente com essa opção, resultando em avaliações imprecisas do público-alvo. Como resultado, se &quot;ignorar ano&quot; fosse ativado em um ano bissexto, a avaliação do público-alvo perderia um dia.

Se você criou um público-alvo antes de lançar esta correção, basta salvar novamente o público-alvo no Construtor de segmentos para aplicar a correção. Se você não tiver certeza se o público-alvo é afetado por essa resolução, o Construtor de segmentos perguntará ao usuário se o público-alvo existente é afetado por esse problema.
