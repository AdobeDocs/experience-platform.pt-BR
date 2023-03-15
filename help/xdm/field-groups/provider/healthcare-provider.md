---
title: Grupo de campos de esquema do provedor de assistência médica
description: Este documento fornece uma visão geral do grupo de campos Esquema de provedor de assistência médica.
exl-id: e39b4082-4b66-47b3-a8e2-951d8a96f742
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 4%

---

# [!UICONTROL Provedor de assistência médica] grupo de campos de esquema

[!UICONTROL Provedor de assistência médica] é um grupo de campos de esquema padrão para o [[!UICONTROL Provedor] classe](../../classes/provider.md). Ele fornece um único campo do tipo objeto `healthcareProvider` que inclui propriedades relacionadas com um profissional de saúde individual ou com uma organização de instalações de saúde licenciada para prestar serviços de diagnóstico e tratamento de cuidados de saúde.

![](../../images/field-groups/healthcare-provider.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `addressDetails` | Matriz de objetos | Lista os detalhes de endereço do provedor. Cada objeto inclui as seguintes propriedades: <ul><li>`address`: ([[!UICONTROL Endereço postal]](../../data-types/postal-address.md)): O endereço postal do provedor.</li><li>`addressType`: (String) O tipo de endereço, indicando onde o provedor fornece serviços.</li></ul> |
| `emailAddress` | [[!UICONTROL Endereço de email]](../../data-types/email-address.md) | O endereço de email do provedor. |
| `fax` | [[!UICONTROL Número de telefone]](../../data-types/phone-number.md) | O número de fax do provedor. |
| `phoneNumber` | [[!UICONTROL Número de telefone]](../../data-types/phone-number.md) | O número de telefone do provedor. |
| `qualifications` | Matriz de objetos | Lista as certificações, licenças ou treinamentos relativos à prestação de cuidados. Cada objeto inclui as seguintes propriedades: <ul><li>`issuer`: ([[!UICONTROL Detalhes da conta]](../../data-types/account-details.md)): a organização que regulamenta e emite a qualificação.</li><li>`activePeriod`: (número inteiro) o ano até o qual a qualificação é válida.</li><li>`code`: (String) Uma representação codificada da qualificação.</li></ul> |
| `classification` | String | A classificação do provedor de serviços com base na classe ou categoria (como atendimento ao paciente, atendimento não paciente e assim por diante). |
| `isActive` | Booleano | Indica se o provedor está ativo. |
| `languages` | Matriz de cadeias de caracteres | Uma lista de idiomas em que o provedor realiza operações. |
| `practiceGroupName` | String | O nome do grupo de práticas do provedor de serviços. |
| `practiceGroupType` | String | O tipo de grupo de práticas do provedor de serviços. |
| `practiceType` | String | O tipo de prática para o provedor de serviços. |
| `specialties` | Matriz de cadeias de caracteres | Uma lista de especialidades oferecidas por este provedor. |

{style="table-layout:auto"}

Para obter mais informações sobre o grupo de campos, consulte o [repositório XDM público](https://github.com/adobe/xdm/blob/master/components/fieldgroups/provider/healthcare-provider-details.schema.json).
