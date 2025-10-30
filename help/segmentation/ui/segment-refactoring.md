---
solution: Experience Platform
title: Guia da interface de usuário de restrições de tempo de segmentação refatorada
description: O Construtor de segmentos fornece um espaço de trabalho avançado que permite a você interagir com elementos de dados do Perfil. O espaço de trabalho fornece controles intuitivos para criar e editar regras, como arrastar e soltar blocos usados para representar propriedades de dados.
hidefromtoc: true
exl-id: 3a352d46-829f-4a58-b676-73c3147f792c
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 9%

---

# Refatoração de restrições de tempo {#refactorization}

>[!CONTEXTUALHELP]
>id="platform_audiences_segmentBuilder_constraints"
>title="Refatoração de restrições de tempo"
>abstract="As restrições de tempo em nível de regra e de grupo foram removidas para esclarecer o uso das restrições de tempo. Reescreva sua restrição de tempo no nível da tela ou do cartão."

A versão de janeiro de 2024 do Adobe Experience Platform introduziu alterações no Serviço de segmentação da Adobe Experience Platform que adicionam novas restrições, nas quais as restrições de tempo podem ser definidas. Essas alterações afetam os segmentos recém-criados ou editados que usam a interface do usuário do Construtor de segmentos. Este guia explica como atenuar essas alterações.

Antes da versão de janeiro de 2024, todas as restrições de tempo no nível da regra, do grupo e da tela se referiam redundantemente ao mesmo carimbo de data e hora. Para esclarecer o uso da restrição de tempo, as restrições de tempo em nível de regra e de grupo foram removidas. Para acomodar essa alteração, todas as restrições de tempo **devem** ser regravadas como **nível da tela** ou **nível do cartão** restrições de tempo.

Anteriormente, um evento individual podia ter várias regras de restrição de tempo anexadas a ele. Com esta atualização recente, tentar adicionar uma restrição de tempo a uma regra resultará em um **erro**.

![A restrição de tempo em nível de regra está realçada. O erro que ocorrerá posteriormente também é destacado.](../images/ui/segment-refactoring/rule-time-constraint.png)

As restrições de tempo agora só podem ser aplicadas no nível da tela ou do cartão.

Ao aplicar uma restrição de tempo no nível da tela de desenho, ainda é possível selecionar todas as restrições de tempo disponíveis.

>[!NOTE]
>
>Se houver apenas **um** cartão na tela, aplicar a restrição de tempo ao cartão será **equivalente** para aplicar a restrição de tempo no nível da tela.
>
>Se houver **vários** cartões na tela, aplicar a restrição de tempo ao nível da tela aplicará essa restrição de tempo a **todos** cartões na tela.

![A restrição de tempo em nível de tela está realçada.](../images/ui/segment-refactoring/canvas-time-constraint.png)

Para aplicar uma restrição de tempo no nível do cartão, selecione o cartão específico ao qual deseja aplicar a restrição de tempo. O contêiner **[!UICONTROL Event Rules]** aparece. Agora é possível selecionar a restrição de tempo que deseja aplicar ao cartão.

![A restrição de tempo em nível de cartão está realçada.](../images/ui/segment-refactoring/card-time-constraint.png)
