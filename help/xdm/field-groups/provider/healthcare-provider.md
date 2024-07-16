---
title: Grupo de campos de esquema do provedor de assistência médica
description: Saiba mais sobre o grupo de campos Esquema de provedor de assistência médica.
exl-id: e39b4082-4b66-47b3-a8e2-951d8a96f742
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 3%

---

# Grupo de campos de esquema [!UICONTROL Provedor de assistência médica]

[!UICONTROL Provedor de Assistência Médica] é um grupo de campos de esquema padrão para a classe [[!UICONTROL Provedor]](../../classes/provider.md). Ele fornece um único campo de tipo de objeto `healthcareProvider` que captura propriedades relacionadas a um profissional de saúde individual ou a uma organização de instalações de saúde licenciada para fornecer serviços de diagnóstico e tratamento de saúde.

![](../../images/field-groups/healthcare-provider.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `addressDetails` | Matriz de objetos | Lista os detalhes de endereço do provedor. Cada objeto inclui as seguintes propriedades: <ul><li>`address`: ([[!UICONTROL Endereço postal]](../../data-types/postal-address.md)): o endereço postal do provedor.</li><li>`addressType`: (Cadeia de caracteres) O tipo de endereço, indicando onde o provedor fornece serviços.</li></ul> |
| `emailAddress` | [[!UICONTROL Endereço de email]](../../data-types/email-address.md) | O endereço de email do provedor. |
| `fax` | [[!UICONTROL Número de telefone]](../../data-types/phone-number.md) | O número de fax do provedor. |
| `phoneNumber` | [[!UICONTROL Número de telefone]](../../data-types/phone-number.md) | O número de telefone do provedor. |
| `qualifications` | Matriz de objetos | Lista as certificações, licenças ou treinamentos relativos à prestação de cuidados. Cada objeto inclui as seguintes propriedades: <ul><li>`issuer`: ([[!UICONTROL Detalhes da conta]](../../data-types/account-details.md)): a organização que regulamenta e emite a qualificação.</li><li>`activePeriod`: (Número inteiro) o ano até o qual a qualificação é válida.</li><li>`code`: (Cadeia de caracteres) Uma representação codificada da qualificação.</li></ul> |
| `classification` | String | A classificação do provedor de serviços com base na classe ou categoria (como atendimento ao paciente, atendimento não paciente e assim por diante). |
| `isActive` | Booleano | Indica se o provedor está ativo. |
| `languages` | Matriz de cadeias de caracteres | Uma lista de idiomas em que o provedor realiza operações. |
| `practiceGroupName` | String | O nome do grupo de práticas do provedor de serviços. |
| `practiceGroupType` | String | O tipo de grupo de práticas do provedor de serviços. |
| `practiceType` | String | O tipo de prática para o provedor de serviços. |
| `specialties` | Matriz de cadeias de caracteres | Uma lista de especialidades oferecidas por este provedor. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o grupo de campos, consulte o [repositório XDM público](https://github.com/adobe/xdm/blob/master/components/fieldgroups/provider/healthcare-provider-details.schema.json).
