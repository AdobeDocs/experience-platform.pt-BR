---
title: Grupo de Campo Esquema de Medicação de Saúde
description: Este documento fornece uma visão geral do grupo de campos Esquema de medicação da Saúde.
source-git-commit: 3b0c85eb5184dd116b1013e617cf528080fa0656
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 6%

---

# [!UICONTROL Medicamentos para a saúde] grupo de campos de esquema

[!UICONTROL Medicamentos para a saúde] é um grupo de campos de esquema padrão para a variável [[!UICONTROL Medicação] classe](../../classes/medication.md). Ele fornece um único campo do tipo objeto `medication` que captura detalhes como nome da marca, número do lote e quantidade.

![](../../images/field-groups/healthcare-medication.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `ingredients` | Matriz de objetos | Lista os ingredientes presentes no medicamento. Cada objeto inclui as seguintes propriedades: <ul><li>`isActive`: (Booleano) Indica se este ingrediente é ainda ativamente utilizado neste medicamento.</li><li>`name`: (String) O nome do ingrediente.</li><li>`quantity`: (String) A quantidade do ingrediente presente no medicamento.</li></ul> |
| `brandName` | String | O nome da marca da droga. |
| `codes` | Matriz de cadeias de caracteres | Uma lista de códigos que identificam este medicamento. |
| `dosageUnitNumber` | Duplo | Número da unidade de dose do medicamento. |
| `dosageUnitOfMeasurement` | String | A unidade de medida para o número de dose. |
| `expiryDate` | DateTime | Prazo de validade do medicamento. |
| `genericName` | String | O nome genérico do fármaco. |
| `lotNumber` | String | O identificador exclusivo para o lote do medicamento. |
| `manufacturerName` | String | O nome do fabricante da droga. |
| `quantity` | Duplo | A quantidade de droga na embalagem. |
| `status` | String | Um estado geral que indica se o fármaco/medicação é ativo ou não. |
| `volume` | Duplo | O volume da droga. |

{style=&quot;table-layout:auto&quot;}

Para obter mais detalhes sobre o grupo de campos, consulte [repositório XDM público](https://github.com/adobe/xdm/blob/master/components/fieldgroups/medication/healthcare-medication.schema.json).
