---
title: Classe de Medicação
description: Saiba mais sobre a classe Medication no Experience Data Model (XDM).
exl-id: e5786241-dd6e-450f-98c8-2de46affb3e2
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 4%

---

# Classe [!UICONTROL Medicação]

No Experience Data Model (XDM), a classe [!UICONTROL Medication] captura o conjunto mínimo de propriedades que definem uma substância usada para tratamento médico, especialmente um medicamento ou medicamento.

![Estrutura de classe](../images/classes/medication.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `_id` | [!UICONTROL String] | Um identificador de sequência de caracteres exclusivo gerado pelo sistema para o registro. Este campo é usado para rastrear a exclusividade de um registro individual, impedir a duplicação de dados e pesquisar esse registro nos serviços downstream.<br><br>Como este campo é gerado pelo sistema, ele não receberá um valor explícito durante a assimilação de dados. No entanto, você ainda pode optar por fornecer seus próprios valores de ID exclusivos, se desejar. |
| `medicationId` | [!UICONTROL String] | Um identificador exclusivo para o medicamento. |
| `medicationName` | [!UICONTROL String] | O nome do medicamento. |

{style="table-layout:auto"}

A classe pode ser estendida com o [[!UICONTROL grupo de campo ](../field-groups/medication/healthcare-medication.md) de medicação para assistência médica] para descrever mais detalhes sobre o medicamento ou o medicamento.
