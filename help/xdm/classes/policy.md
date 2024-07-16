---
title: Classe de Política
description: Saiba mais sobre a classe Política no Experience Data Model (XDM).
exl-id: 56cc8c69-84a0-493e-85c5-e0cd994e4bee
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 3%

---

# Classe [!UICONTROL Política]

No Experience Data Model (XDM), a classe [!UICONTROL Policy] captura o conjunto mínimo de propriedades que definem uma apólice de seguro.

![](../images/classes/policy.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `assignedBeneficiary` | Matriz de tipos de dados [[!UICONTROL Pessoa]](../data-types/person.md) | Registra o beneficiário (ou beneficiários) atribuído à apólice. |
| `benefitAmount` | [[!UICONTROL Moeda]](../data-types/currency.md) | O valor a ser pago de acordo com os termos da apólice. |
| `location` | [[!UICONTROL Endereço postal]](../data-types/postal-address.md) | O local em que a apólice de seguro é emitida. |
| `owner` | [!UICONTROL Objeto] | Registra as informações do perfil do detentor da apólice. |
| `owner.faxPhone` | [[!UICONTROL Número de telefone]](../data-types/phone-number.md) | O número de fax do proprietário. |
| `owner.homeAddress` | [[!UICONTROL Endereço postal]](../data-types/postal-address.md) | O endereço residencial do proprietário. |
| `owner.homePhone` | [[!UICONTROL Número de telefone]](../data-types/phone-number.md) | O telefone residencial do proprietário. |
| `owner.mobilePhone` | [[!UICONTROL Número de telefone]](../data-types/phone-number.md) | O número de telefone celular do proprietário. |
| `owner.personalEmail` | [[!UICONTROL Endereço de email]](../data-types/email-address.md) | O endereço de email pessoal do proprietário. |
| `ID` | [!UICONTROL String] | Um identificador da apólice de seguro. |
| `_id` | [!UICONTROL String] | Um identificador de sequência de caracteres exclusivo gerado pelo sistema para o registro. Este campo é usado para rastrear a exclusividade de um registro individual, impedir a duplicação de dados e pesquisar esse registro nos serviços downstream.<br><br>Como este campo é gerado pelo sistema, ele não receberá um valor explícito durante a assimilação de dados. No entanto, você ainda pode optar por fornecer seus próprios valores de ID exclusivos, se desejar. |
| `endDate` | [!UICONTROL DateTime] | A data em que a cobertura da apólice de seguro termina (ou terminou). |
| `hasAssignedBeneficiary` | [!UICONTROL Booleano] | Indica se a apólice tem um beneficiário atribuído. |
| `name` | [!UICONTROL String] | O nome da apólice de seguro. |
| `startDate` | [!UICONTROL DateTime] | A data em que a cobertura da apólice de seguro começa (ou começou). |
| `type` | [!UICONTROL String] | O tipo de apólice de seguro, como casa, automóvel, locatário ou barco. |

{style="table-layout:auto"}
