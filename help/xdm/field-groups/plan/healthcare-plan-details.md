---
title: Detalhes do Plano de Saúde Grupo de Campos do Esquema
description: Este documento fornece uma visão geral do grupo de campos Detalhes do Plano de Saúde.
source-git-commit: 3937963ceee8502b0669a3f007fd38ecf2824e9b
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 5%

---

# [!UICONTROL Detalhes do Plano de Saúde] grupo de campos de esquema

[!UICONTROL Detalhes do Plano de Saúde] é um grupo de campos de esquema padrão para a variável [[!UICONTROL Plano] classe](../../classes/plan.md). Ele fornece um único campo do tipo objeto `healthcarePlanDetails` que capta propriedades relacionadas com um plano médico.

![](../../images/field-groups/plan/healthcare-plan-details.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `networkDetails` | Matriz de objetos | Lista os detalhes da(s) rede(s) de fornecedores definida(s) pela seguradora a que o beneficiário pode solicitar tratamento e será coberta à taxa &quot;na rede&quot;. Cada objeto inclui as seguintes propriedades: <ul><li>`networkID`: (String) A ID específica da seguradora para a rede.</li><li>`networkName`: (String) O nome específico da seguradora para a rede.</li></ul> |
| `affiliations` | Matriz de cadeias de caracteres | Uma lista de entidades de negócios afiliadas ao plano. |
| `coverageType` | String | O tipo de cobertura do plano. Os valores aceitos são:<ul><li>`medical`</li><li>`dental`</li><li>`vision`</li><li>`accident`</li></ul> |
| `isActive` | Booleano | Indica se o plano está ativo. |
| `lastVerificationDate` | DateTime | A data em que o plano foi verificado pela última vez. |
| `payerID` | String | O identificador único do ordenante (por outras palavras, o prestador de seguros do plano). |
| `planLevel` | String | Indica o nível do plano. Os valores aceitos são:<ul><li>`primary`</li><li>`secondary`</li><li>`tertiary`</li><li>`quaternary`</li></ul> |
| `planType` | String | Indica o tipo de plano. Os valores aceitos são:<ul><li>`hmo`</li><li>`epo`</li><li>`pos`</li><li>`hdhp`</li></ul> |
| `targetOwnerType` | String | O tipo de proprietário para o qual um plano é. Os exemplos incluem indivíduo, grupo, organização e assim por diante. |

{style=&quot;table-layout:auto&quot;}

Para obter mais detalhes sobre o grupo de campos, consulte [repositório XDM público](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/plan/healthcare-plan-details.schema.json).
