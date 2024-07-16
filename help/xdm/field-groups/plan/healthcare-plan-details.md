---
title: Grupo de Campos de Esquema de Detalhes do Plano de Saúde
description: Saiba mais sobre o grupo de campos de esquema Detalhes do plano de saúde.
exl-id: 5a480c5b-74f8-48dd-858a-5cf2628dc7f0
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 5%

---

# [!UICONTROL Detalhes do plano de saúde] grupo de campos de esquema

[!UICONTROL Detalhes do Plano de Saúde] é um grupo de campos de esquema padrão para a classe [[!UICONTROL Plano]](../../classes/plan.md). Ele fornece um único campo de tipo de objeto `healthcarePlanDetails` que captura propriedades relacionadas a um plano médico.

![](../../images/field-groups/plan/healthcare-plan-details.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `networkDetails` | Matriz de objetos | Lista os detalhes da(s) rede(s) definida(s) pela seguradora dos provedores para os quais o beneficiário pode buscar tratamento e será coberta pela taxa &quot;na rede&quot;. Cada objeto inclui as seguintes propriedades: <ul><li>`networkID`: (Cadeia de caracteres) A ID específica da seguradora da rede.</li><li>`networkName`: (Cadeia de caracteres) O nome específico da seguradora para a rede.</li></ul> |
| `affiliations` | Matriz de cadeias de caracteres | Uma lista de entidades comerciais afiliadas ao plano. |
| `coverageType` | String | O tipo de cobertura do plano. Os valores aceitos são:<ul><li>`medical`</li><li>`dental`</li><li>`vision`</li><li>`accident`</li></ul> |
| `isActive` | Booleano | Indica se o plano está ativo. |
| `lastVerificationDate` | DateTime | A data em que o plano foi verificado pela última vez. |
| `payerID` | String | O identificador exclusivo do pagador (em outras palavras, o provedor de seguro do plano). |
| `planLevel` | String | Indica o nível do plano. Os valores aceitos são:<ul><li>`primary`</li><li>`secondary`</li><li>`tertiary`</li><li>`quaternary`</li></ul> |
| `planType` | String | Indica o tipo de plano. Os valores aceitos são:<ul><li>`hmo`</li><li>`epo`</li><li>`pos`</li><li>`hdhp`</li></ul> |
| `targetOwnerType` | String | O tipo de proprietário para o qual um plano se destina. Os exemplos incluem indivíduo, grupo, organização e assim por diante. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o grupo de campos, consulte o [repositório XDM público](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/plan/healthcare-plan-details.schema.json).
