---
title: Grupo de Campos de Esquema do Provedor de Saúde
description: Este documento fornece uma visão geral do grupo de campos Provedor de saúde .
source-git-commit: cf39f943e27cd11b0eabbc344774fa12482a8f92
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 5%

---

# [!UICONTROL Provedor de saúde] grupo de campos de esquema

[!UICONTROL Provedor de saúde] é um grupo de campos de esquema padrão para a variável [[!UICONTROL Provedor] classe](../../classes/provider.md). Ele fornece um único campo do tipo objeto `healthcareProvider` Captura de propriedades relacionadas com um profissional de saúde individual ou com uma organização de cuidados de saúde licenciada para prestar serviços de diagnóstico e tratamento de saúde.

![](../../images/field-groups/healthcare-provider.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `addressDetails` | Matriz de objetos | Lista os detalhes de endereço do provedor. Cada objeto inclui as seguintes propriedades: <ul><li>`address`: ([[!UICONTROL Endereço postal]](../../data-types/postal-address.md)): O endereço postal do provedor.</li><li>`addressType`: (String) O tipo de endereço, indicando onde o provedor fornece serviços.</li></ul> |
| `emailAddress` | [[!UICONTROL Endereço de email]](../../data-types/email-address.md) | O endereço de email do provedor. |
| `fax` | [[!UICONTROL Número de telefone]](../../data-types/phone-number.md) | O número de fax do provedor. |
| `phoneNumber` | [[!UICONTROL Número de telefone]](../../data-types/phone-number.md) | O número de telefone do provedor. |
| `qualifications` | Matriz de objetos | Lista as certificações, licenças ou treinamento relacionados à prestação de cuidados. Cada objeto inclui as seguintes propriedades: <ul><li>`issuer`: ([[!UICONTROL Detalhes da conta]](../../data-types/account-details.md)): A organização que regulamenta e emite a qualificação.</li><li>`activePeriod`: (Número inteiro) O ano até ao qual a qualificação é válida.</li><li>`code`: (String) Uma representação codificada da qualificação.</li></ul> |
| `classification` | String | A classificação do provedor de serviços com base na classe ou categoria (como atendimento ao paciente, assistência não-paciente etc.). |
| `isActive` | Booleano | Indica se o provedor está ativo. |
| `languages` | Matriz de cadeias de caracteres | Uma lista de idiomas em que o provedor executa operações. |
| `practiceGroupName` | String | O nome do grupo de práticas para o provedor de serviços. |
| `practiceGroupType` | String | O tipo de grupo de práticas para o provedor de serviços. |
| `practiceType` | String | O tipo de prática do provedor de serviços. |
| `specialties` | Matriz de cadeias de caracteres | Uma lista de especialidades oferecidas por esse provedor. |

{style=&quot;table-layout:auto&quot;}

Para obter mais detalhes sobre o grupo de campos, consulte [repositório XDM público](https://github.com/adobe/xdm/blob/master/components/fieldgroups/provider/healthcare-provider-details.schema.json).
