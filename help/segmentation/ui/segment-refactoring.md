---
keywords: Experience Platform, home, tópicos populares, segmentação, Segmentação, construtor de segmentos, Construtor de segmentos
solution: Experience Platform
title: Guia da interface do usuário de restrições de tempo de segmentação refatoradas
topic-legacy: ui guide
description: O Construtor de segmentos fornece um espaço de trabalho avançado que permite interagir com elementos de dados do perfil. O espaço de trabalho oferece controles intuitivos para criar e editar regras, como blocos de arrastar e soltar usados para representar propriedades de dados.
exl-id: 3a352d46-829f-4a58-b676-73c3147f792c
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 0%

---

# Reestruturação de restrições de tempo

A versão de outubro de 2020 do Adobe Experience Platform introduziu alterações de desempenho no Adobe Experience Platform Segmentation Service que adicionam novas restrições ao uso dos operadores lógicos OR e AND. Essas alterações afetarão segmentos recém-criados ou editados feitos com a interface do usuário do Construtor de segmentos. Este guia explica como atenuar essas alterações.

Antes da versão de outubro de 2020, todas as restrições de tempo a nível de regra, de grupo e a nível de evento se referiam redundantemente ao mesmo carimbo de data e hora. Para esclarecer o uso da restrição de tempo, as restrições de tempo a nível de regra e de grupo foram removidas. Para acomodar essa alteração, todas as restrições de tempo devem ser regravadas como restrições de tempo no nível do evento.

Anteriormente, um evento individual podia ter várias regras de restrição de tempo anexadas a ele.

![](../images/ui/segment-refactoring/former-time-constraint.png)

Como é possível observar, esse segmento tem duas restrições no nível da regra: Um para &quot;[!UICONTROL Today]&quot; e outro para &quot;[!UICONTROL Yesterday]&quot;.

O segmento anterior é equivalente ao seguinte segmento — ambas as restrições de tempo no nível do evento foram conectadas usando um operador AND. A primeira restrição de tempo de nível de evento faz referência a um evento de clique cujo nome é &quot;Treinamento&quot; e está acontecendo hoje, enquanto a segunda restrição de tempo de nível de evento faz referência a um evento de clique cujo nome é igual a &quot;Predefinições&quot; e aconteceu ontem.

![](../images/ui/segment-refactoring/time-constraint-1.png) ![](../images/ui/segment-refactoring/time-constraint-2.png)

Essa refatoração das restrições de tempo também afeta as restrições de tempo que são conectadas usando um operador OU.
