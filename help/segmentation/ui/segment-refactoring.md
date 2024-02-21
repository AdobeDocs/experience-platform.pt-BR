---
solution: Experience Platform
title: Guia da interface de usuário de restrições de tempo de segmentação refatorada
description: O Construtor de segmentos fornece um espaço de trabalho avançado que permite a você interagir com elementos de dados do Perfil. O espaço de trabalho fornece controles intuitivos para criar e editar regras, como arrastar e soltar blocos usados para representar propriedades de dados.
exl-id: 3a352d46-829f-4a58-b676-73c3147f792c
source-git-commit: 665bbd1904e857336a4fb677230389d7977f6b60
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 9%

---

# Refatoração de restrições de tempo {#refactorization}

>[!CONTEXTUALHELP]
>id="platform_audiences_segmentBuilder_constraints"
>title="Refatoração de restrições de tempo"
>abstract="As restrições de tempo em nível de regra e de grupo foram removidas para esclarecer o uso das restrições de tempo. Reescreva sua restrição de tempo no nível da tela ou do cartão."

A versão de janeiro de 2024 do Adobe Experience Platform introduziu alterações no Serviço de segmentação da Adobe Experience Platform que adicionam novas restrições, nas quais as restrições de tempo podem ser definidas. Essas alterações afetam os segmentos recém-criados ou editados que usam a interface do usuário do Construtor de segmentos. Este guia explica como atenuar essas alterações.

Antes da versão de janeiro de 2024, todas as restrições de tempo no nível da regra, do grupo e da tela se referiam redundantemente ao mesmo carimbo de data e hora. Para esclarecer o uso da restrição de tempo, as restrições de tempo em nível de regra e de grupo foram removidas. Para acomodar essa alteração, todas as restrições de tempo **deve** ser regravada como **nível da tela** ou **nível de cartão** restrições de tempo.

Anteriormente, um evento individual podia ter várias regras de restrição de tempo anexadas a ele. Com esta atualização recente, a tentativa de adicionar uma restrição de tempo a uma regra agora resultará em uma **erro**.

![A restrição de tempo em nível de regra é realçada. O erro que ocorrerá posteriormente também é destacado. ](../images/ui/segment-refactoring/rule-time-constraint.png)

As restrições de tempo agora só podem ser aplicadas no nível da tela ou do cartão.

Ao aplicar uma restrição de tempo no nível da tela de desenho, ainda é possível selecionar todas as restrições de tempo disponíveis.

>[!NOTE]
>
>Se só houver **um** na tela, a aplicação da restrição de tempo ao cartão é **equivalente** para aplicar a restrição de tempo no nível da tela.
>
>Se houver **múltiplo** cartões na tela, a aplicação da restrição de tempo ao nível da tela aplicará essa restrição de tempo a **all** cartões na tela.

![A restrição de tempo em nível de tela de desenho é realçada.](../images/ui/segment-refactoring/canvas-time-constraint.png)

Para aplicar uma restrição de tempo no nível do cartão, selecione o cartão específico ao qual deseja aplicar a restrição de tempo. A variável **[!UICONTROL Regras de evento]** container (contêiner) é exibido. Agora é possível selecionar a restrição de tempo que deseja aplicar ao cartão.

![A restrição de tempo em nível de cartão é realçada.](../images/ui/segment-refactoring/card-time-constraint.png)
