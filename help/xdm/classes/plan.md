---
title: Classe de Plano
description: Este documento fornece uma visão geral da classe Plano no Experience Data Model (XDM).
source-git-commit: cf39f943e27cd11b0eabbc344774fa12482a8f92
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 5%

---

# [!UICONTROL Plano] classe

No Experience Data Model (XDM), a variável [!UICONTROL Plano] captura o conjunto mínimo de propriedades que definem um plano, como um plano de saúde ou plano de seguro.

![Estrutura de classes](../images/classes/plan.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `_id` | [!UICONTROL String] | Um identificador de string exclusivo gerado pelo sistema para o registro. Este campo é usado para rastrear a exclusividade de um registro individual, evitar a duplicação de dados e buscar esse registro em serviços downstream.<br><br>Como esse campo é gerado pelo sistema, ele não recebe um valor explícito durante a assimilação de dados. No entanto, ainda é possível optar por fornecer seus próprios valores de ID exclusivos. |
| `planId` | [!UICONTROL String] | Um identificador exclusivo para o plano. |
| `planName` | [!UICONTROL String] | O nome do plano. |

{style=&quot;table-layout:auto&quot;}

A classe pode ser estendida com a variável [[!UICONTROL Detalhes do Plano de Saúde] grupo de campos](../field-groups/plan/healthcare-plan-details.md) descrever mais pormenores sobre um plano de seguro de doença.
