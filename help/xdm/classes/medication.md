---
title: Classe de Medicamento
description: Este documento fornece uma visão geral da classe Medication no Experience Data Model (XDM).
source-git-commit: cf39f943e27cd11b0eabbc344774fa12482a8f92
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 5%

---

# [!UICONTROL Medicação] classe

No Experience Data Model (XDM), a variável [!UICONTROL Medicação] A classe captura o conjunto mínimo de propriedades que definem uma substância usada para tratamento médico, especialmente um medicamento ou um fármaco.

![Estrutura de classes](../images/classes/medication.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `_id` | [!UICONTROL String] | Um identificador de string exclusivo gerado pelo sistema para o registro. Este campo é usado para rastrear a exclusividade de um registro individual, evitar a duplicação de dados e buscar esse registro em serviços downstream.<br><br>Como esse campo é gerado pelo sistema, ele não recebe um valor explícito durante a assimilação de dados. No entanto, ainda é possível optar por fornecer seus próprios valores de ID exclusivos. |
| `medicationId` | [!UICONTROL String] | Um identificador único para a medicação. |
| `medicationName` | [!UICONTROL String] | O nome do medicamento. |

{style=&quot;table-layout:auto&quot;}

A classe pode ser estendida com a variável [[!UICONTROL Medicamentos para a saúde] grupo de campos](../field-groups/medication/healthcare-medication.md) descrever mais pormenores sobre o medicamento ou o medicamento.
