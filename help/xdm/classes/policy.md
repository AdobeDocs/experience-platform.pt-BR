---
title: Classe de política
description: Este documento fornece uma visão geral da classe de Política no Experience Data Model (XDM).
source-git-commit: c0437b8f9d93c46dbec991a33a893a5b9e0cdf2c
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 7%

---

# [!UICONTROL Política] classe

No Experience Data Model (XDM), a variável [!UICONTROL Política] captura o conjunto mínimo de propriedades que definem uma apólice de seguro.

![](../images/classes/policy.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `assignedBeneficiary` | Matriz de [[!UICONTROL Pessoa]](../data-types/person.md) tipos de dados | Captura o beneficiário (ou beneficiários) atribuído à política. |
| `benefitAmount` | [[!UICONTROL Moeda]](../data-types/currency.md) | O montante a pagar de acordo com as condições de política. |
| `location` | [[!UICONTROL Endereço postal]](../data-types/postal-address.md) | O local de emissão da apólice de seguro. |
| `owner` | [!UICONTROL Objeto] | Captura as informações de perfil do detentor da política. |
| `owner.faxPhone` | [[!UICONTROL Número de telefone]](../data-types/phone-number.md) | O número de telefone do fax do proprietário. |
| `owner.homeAddress` | [[!UICONTROL Endereço postal]](../data-types/postal-address.md) | O endereço residencial do proprietário. |
| `owner.homePhone` | [[!UICONTROL Número de telefone]](../data-types/phone-number.md) | O número do telefone da casa do proprietário. |
| `owner.mobilePhone` | [[!UICONTROL Número de telefone]](../data-types/phone-number.md) | O número do telefone celular do proprietário. |
| `owner.personalEmail` | [[!UICONTROL Endereço de email]](../data-types/email-address.md) | O endereço de email pessoal do proprietário. |
| `ID` | [!UICONTROL String] | Um identificador para a apólice de seguro. |
| `_id` | [!UICONTROL String] | Um identificador de string exclusivo gerado pelo sistema para o registro. Este campo é usado para rastrear a exclusividade de um registro individual, evitar a duplicação de dados e buscar esse registro em serviços downstream.<br><br>Como esse campo é gerado pelo sistema, ele não recebe um valor explícito durante a assimilação de dados. No entanto, ainda é possível optar por fornecer seus próprios valores de ID exclusivos. |
| `endDate` | [!UICONTROL DateTime] | A data em que a cobertura da apólice de seguro termina (ou termina). |
| `hasAssignedBeneficiary` | [!UICONTROL Booleano] | Indica se a política tem um beneficiário atribuído. |
| `name` | [!UICONTROL String] | O nome da apólice de seguro. |
| `startDate` | [!UICONTROL DateTime] | A data em que a cobertura da apólice de seguro começa (ou começou). |
| `type` | [!UICONTROL String] | O tipo de apólice de seguro, como residência, automóvel, entrada ou barco. |

{style=&quot;table-layout:auto&quot;}
