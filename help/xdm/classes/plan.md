---
title: Classe do plano
description: Saiba mais sobre a classe Plano no Experience Data Model (XDM).
exl-id: ccff962d-3104-482c-8d65-d2bd2602a9be
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 4%

---

# Classe [!UICONTROL Plano]

No Experience Data Model (XDM), a classe [!UICONTROL Plan] captura o conjunto mínimo de propriedades que definem um plano, como um plano de saúde ou um plano de seguro.

![Estrutura de classe](../images/classes/plan.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `_id` | [!UICONTROL String] | Um identificador de sequência de caracteres exclusivo gerado pelo sistema para o registro. Este campo é usado para rastrear a exclusividade de um registro individual, impedir a duplicação de dados e pesquisar esse registro nos serviços downstream.<br><br>Como este campo é gerado pelo sistema, ele não receberá um valor explícito durante a assimilação de dados. No entanto, você ainda pode optar por fornecer seus próprios valores de ID exclusivos, se desejar. |
| `planId` | [!UICONTROL String] | Um identificador exclusivo do plano. |
| `planName` | [!UICONTROL String] | O nome do plano. |

{style="table-layout:auto"}

A classe pode ser estendida com o grupo de campos [[!UICONTROL Detalhes do plano de saúde]](../field-groups/plan/healthcare-plan-details.md) para descrever mais detalhes sobre um plano de seguro de saúde.
