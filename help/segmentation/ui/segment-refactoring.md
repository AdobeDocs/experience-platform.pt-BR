---
solution: Experience Platform
title: Guia da interface de usuário de restrições de tempo de segmentação refatorada
description: O Construtor de segmentos fornece um espaço de trabalho avançado que permite a você interagir com elementos de dados do Perfil. O espaço de trabalho fornece controles intuitivos para criar e editar regras, como arrastar e soltar blocos usados para representar propriedades de dados.
exl-id: 3a352d46-829f-4a58-b676-73c3147f792c
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---

# Refatoração de restrições de tempo

A versão de outubro de 2020 para o Adobe Experience Platform introduziu alterações de desempenho no Serviço de segmentação do Adobe Experience Platform que adicionam novas restrições ao uso dos operadores lógicos OR e AND. Essas alterações afetarão os segmentos recém-criados ou editados que usam a interface do usuário do Construtor de segmentos. Este guia explica como atenuar essas alterações.

Antes da versão de outubro de 2020, todas as restrições de tempo no nível da regra, do grupo e do evento se referiam redundantemente ao mesmo carimbo de data e hora. Para esclarecer o uso da restrição de tempo, as restrições de tempo em nível de regra e de grupo foram removidas. Para acomodar essa alteração, todas as restrições de tempo devem ser regravadas como restrições de tempo no nível do evento.

Anteriormente, um evento individual podia ter várias regras de restrição de tempo anexadas a ele.

![O estilo anterior de restrições de tempo é destacado no Construtor de segmentos.](../images/ui/segment-refactoring/former-time-constraint.png)

Como você pode ver, esse segmento tem duas restrições no nível da regra: uma para &quot;[!UICONTROL Hoje]&quot; e o outro para &quot;[!UICONTROL Ontem]&quot;.

O segmento anterior é equivalente ao seguinte segmento — ambas as restrições de tempo no nível do evento foram conectadas usando um operador AND. A primeira restrição de tempo no nível do evento faz referência a um evento de clique cujo nome é igual a &quot;Treinamento&quot; e está acontecendo hoje, enquanto a segunda restrição de tempo no nível do evento faz referência a um evento de clique cujo nome é igual a &quot;Animais de estimação&quot; e aconteceu ontem.

![O novo estilo de restrições de tempo é destacado no Construtor de segmentos.](../images/ui/segment-refactoring/time-constraint-1.png) ![O novo estilo de restrições de tempo é destacado no Construtor de segmentos.](../images/ui/segment-refactoring/time-constraint-2.png)

Essa refatoração de restrições de tempo também afeta restrições de tempo que são conectadas usando um operador OR.
