---
title: Classe de Medicação
description: Este documento fornece uma visão geral da classe Medication no Experience Data Model (XDM).
exl-id: e5786241-dd6e-450f-98c8-2de46affb3e2
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 3%

---

# [!UICONTROL Medicação] classe

No Experience Data Model (XDM), a variável [!UICONTROL Medicação] A classe captura o conjunto mínimo de propriedades que definem uma substância usada para tratamento médico, especialmente um medicamento ou medicamento.

![Estrutura de classe](../images/classes/medication.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `_id` | [!UICONTROL String] | Um identificador de sequência de caracteres exclusivo gerado pelo sistema para o registro. Este campo é usado para rastrear a exclusividade de um registro individual, impedir a duplicação de dados e pesquisar esse registro nos serviços downstream.<br><br>Como esse campo é gerado pelo sistema, ele não recebe um valor explícito durante a assimilação de dados. No entanto, você ainda pode optar por fornecer seus próprios valores de ID exclusivos, se desejar. |
| `medicationId` | [!UICONTROL String] | Um identificador exclusivo para o medicamento. |
| `medicationName` | [!UICONTROL String] | O nome do medicamento. |

{style="table-layout:auto"}

A classe pode ser estendida com a variável [[!UICONTROL Medicação para tratamento de saúde] grupo de campos](../field-groups/medication/healthcare-medication.md) para descrever mais detalhes sobre o medicamento ou o medicamento.
