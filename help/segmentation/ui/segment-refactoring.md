---
keywords: Experience Platform;home;popular topics;segmentação;Segmentação;construtor de segmentos;Construtor de segmentos
solution: Experience Platform
title: Guia da interface do usuário de restrições de tempo de segmentação refatorizadas
topic: ui guide
description: 'O Construtor de segmentos fornece uma área de trabalho avançada que permite interagir com elementos de dados do Perfil. A área de trabalho fornece controles intuitivos para criar e editar regras, como os blocos de arrastar e soltar usados para representar propriedades de dados. '
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 0%

---


# Refatoração de restrições de tempo

A versão de outubro de 2020 para Adobe Experience Platform introduziu mudanças de desempenho no Adobe Experience Platform Segmentation Service que adicionam novas restrições ao uso dos operadores lógicos OR e AND. Essas alterações afetarão os segmentos recém-criados ou editados feitos usando a interface do usuário do Construtor de segmentos. Este guia explica como atenuar essas mudanças.

Antes da versão de outubro de 2020, todas as restrições de tempo em nível de regra, em nível de grupo e em nível de evento faziam referência redundante ao mesmo carimbo de data e hora. A fim de esclarecer a utilização de restrições de tempo, as restrições de tempo a nível de regras e de grupo foram removidas. Para acomodar essa alteração, todas as restrições de tempo devem ser regravadas como restrições de tempo no nível do evento.

Anteriormente, um evento individual podia ter várias regras de restrição de tempo anexadas a ele.

![](../images/ui/segment-refactoring/former-time-constraint.png)

Como você pode ver, este segmento tem duas restrições no nível da regra: Um para &quot;[!UICONTROL Today]&quot; e outro para &quot;[!UICONTROL Ontem]&quot;.

O segmento anterior é equivalente ao seguinte segmento. ambas as restrições de tempo no nível do evento foram conectadas usando um operador E. A primeira restrição de tempo no nível do evento faz referência a um evento de clique cujo nome é &quot;Treinamento&quot; e está ocorrendo hoje, enquanto a segunda restrição de tempo no nível do evento faz referência a um evento de clique cujo nome é &quot;Pets&quot; e aconteceu ontem.

![](../images/ui/segment-refactoring/time-constraint-1.png) ![](../images/ui/segment-refactoring/time-constraint-2.png)

Essa refatoração das restrições de tempo também afeta as restrições de tempo que são conectadas usando um operador OU.