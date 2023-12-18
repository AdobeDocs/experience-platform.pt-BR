---
title: Grupo de Campos de Esquema de Medicação de Cuidados Médicos
description: Saiba mais sobre o grupo de campos Esquema de medicação para instituições de saúde.
exl-id: 3423d067-fe8c-44e5-a6f9-ce0458d26ebc
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 6%

---

# [!UICONTROL Medicação para tratamento de saúde] grupo de campos de esquema

[!UICONTROL Medicação para tratamento de saúde] é um grupo de campos de esquema padrão para o [[!UICONTROL Medicação] classe](../../classes/medication.md). Ele fornece um único campo do tipo objeto `medication` que captura detalhes como nome da marca, número de lote e quantidade.

![](../../images/field-groups/healthcare-medication.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `ingredients` | Matriz de objetos | Lista os ingredientes presentes no medicamento. Cada objeto inclui as seguintes propriedades: <ul><li>`isActive`: (Booleano) Indica se este ingrediente ainda é usado ativamente neste medicamento.</li><li>`name`: (String) O nome do ingrediente.</li><li>`quantity`: (String) A quantidade do ingrediente presente no medicamento.</li></ul> |
| `brandName` | String | O nome da marca da droga. |
| `codes` | Matriz de cadeias de caracteres | Uma lista de códigos que identificam este medicamento. |
| `dosageUnitNumber` | Duplo | O número da unidade de dose do medicamento. |
| `dosageUnitOfMeasurement` | String | A unidade de medida do número de dose. |
| `expiryDate` | DateTime | Data de validade do medicamento. |
| `genericName` | String | O nome genérico do medicamento. |
| `lotNumber` | String | O identificador exclusivo do lote do medicamento. |
| `manufacturerName` | String | O nome do fabricante da droga. |
| `quantity` | Duplo | A quantidade de droga no pacote. |
| `status` | String | Um status geral indicando se o medicamento/medicação está ativo ou não. |
| `volume` | Duplo | O volume da droga. |

{style="table-layout:auto"}

Para obter mais informações sobre o grupo de campos, consulte o [repositório XDM público](https://github.com/adobe/xdm/blob/master/components/fieldgroups/medication/healthcare-medication.schema.json).
