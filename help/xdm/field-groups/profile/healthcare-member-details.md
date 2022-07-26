---
title: Grupo de Campos do Esquema Detalhes do Membro da Saúde
description: Este documento fornece uma visão geral do grupo de campos Detalhes do Membro da Saúde.
source-git-commit: a51079ff1686ecae3e5fe9f0170b28bc16bcef86
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 3%

---

# [!UICONTROL Detalhes do Membro da Saúde] grupo de campos de esquema

[!UICONTROL Detalhes do Membro da Saúde] é um grupo de campos de esquema padrão para a variável [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md) que capta detalhes de uma pessoa que tem ou irá receber assistência médica ou cuidados, como informação de contato, médico de assistência primária e informação sobre planos.

![Estrutura do grupo de campos](../../images/field-groups/healthcare-member-details/structure.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `billingAddress` | [[!UICONTROL Endereço postal]](../../data-types/postal-address.md) | O endereço de cobrança da pessoa. |
| `faxPhone` | [[!UICONTROL Número de telefone]](../../data-types/phone-number.md) | O número do fax da pessoa. |
| `homeAddress` | [[!UICONTROL Endereço postal]](../../data-types/postal-address.md) | O endereço residencial da pessoa. |
| `homePhone` | [[!UICONTROL Número de telefone]](../../data-types/phone-number.md) | O número do telefone da pessoa. |
| `mailingAddress` | [[!UICONTROL Endereço postal]](../../data-types/postal-address.md) | O endereço de correspondência da pessoa. |
| `memberDetails` | Objeto | Um objeto que contém informações detalhadas sobre os atributos e relações de saúde da pessoa. Consulte a [subseção abaixo](#memberDetails) para obter mais informações sobre a estrutura do objeto. |
| `mobilePhone` | [[!UICONTROL Número de telefone]](../../data-types/phone-number.md) | O número do celular da pessoa. |
| `person` | [[!UICONTROL Pessoa]](../../data-types/person.md) | Um ator individual, contato ou proprietário relacionado à associação à saúde da pessoa. |
| `personalEmail` | [[!UICONTROL Endereço de email]](../../data-types/email-address.md) | O endereço de email pessoal da pessoa. |
| `shippingAddress` | [[!UICONTROL Endereço postal]](../../data-types/postal-address.md) | O endereço de envio da pessoa. |

{style=&quot;table-layout:auto&quot;}

## `memberDetails` {#memberDetails}

`memberDetails` é um objeto que contém informações detalhadas sobre os atributos e as relações da pessoa com relação ao sistema de saúde. A estrutura de `memberDetails` está descrita abaixo.

![estrutura memberDetails](../../images/field-groups/healthcare-member-details/memberDetails.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `emergencyContact` | Objeto | Captura os seguintes detalhes de contato de emergência para a pessoa: <ul><li>`fullName`: (String) O nome completo do contato de emergência.</li><li>`phone`: (String) O número de telefone do contato de emergência.</li><li>`relationshipToMember`: (String) A relação do contato de emergência com a pessoa.</li></ul> |
| `medications` | Matriz de objetos | Lista os detalhes de medicamentos atuais e passados associados à pessoa. Cada item de matriz é um objeto que captura os seguintes detalhes: <ul><li>`refillLocation`: ([[!UICONTROL Endereço postal]](../../data-types/postal-address.md)) O local de recarga do medicamento.</li><li>`ID`: (String) ID da medicação.</li><li>`isCurrent`: (Booleano) Indica se a medicação é atual ou passada.</li><li>`numberOfRefills`: (Número inteiro) O número de recargas prescrito pelo fornecedor deste medicamento.</li><li>`startDate`: (DateTime) A data em que a pessoa começou a tomar o medicamento.</li></ul> |
| `multipleBirth` | Objeto | Captura detalhes relacionados a vários nascimentos: <ul><li>`isMultipleBirth`: (Booleano) Indica se a pessoa deu vários nascimentos.</li><li>`multipleBirthNumber`: (Número inteiro) O número de bebês nascidos se `isMultipleBirth` é verdadeiro.</li></ul> |
| `plans` | Matriz de objetos | Lista os detalhes dos planos médicos atuais e passados associados à pessoa. Cada item de matriz é um objeto que captura os seguintes detalhes: <ul><li>`coverageEndDate`: (DateTime) A data em que a cobertura do plano termina.</li><li>`coverageStartDate`: (DateTime) A data em que a cobertura do plano começa.</li><li>`isActive`: (Booleano) Indica se o plano está ativo.</li><li>`planId`: (String) A ID do plano.</li></ul> |
| `primaryCarePhysicians` | Matriz de objetos | Lista os detalhes dos médicos de assistência primária associados à pessoa. Cada item de matriz é um objeto que captura os seguintes detalhes: <ul><li>`endDate`: (DateTime) A data em que o médico de cuidados primários terminou o tratamento da pessoa.</li><li>`fullname`: (String) O nome completo do médico.</li><li>`providerId`: (String) Um identificador exclusivo para o médico.</li><li>`startDate`: (DateTime) A data em que o médico de cuidados primários iniciou o tratamento da pessoa.</li></ul> |
| `specialists` | Matriz de objetos | Lista os detalhes de especialistas em saúde associados à pessoa. Cada item de matriz é um objeto que captura os seguintes detalhes: <ul><li>`fullname`: (String) O nome completo do especialista.</li><li>`providerId`: (String) Um identificador exclusivo do especialista.</li><li>`specialty`: (String) A especialidade do provedor (como anestesiologia, urologia, radiologia, dermatologia, etc.).</li></ul> |
| `beneficiaryRelationship` | String | A relação de beneficiário com o membro do sistema de saúde se a pessoa for dependente (por exemplo, o próprio, o cônjuge, o filho, etc.). |
| `billingAccountID` | String | Um identificador exclusivo para a conta de faturamento da pessoa. |
| `dateAgeCollected` | DateTime | A data em que a idade da pessoa foi coletada. |
| `deceasedDate` | DateTime | A data em que a pessoa morreu se ela estivesse falecida. |
| `isDeceased` | Booleano | Indica se a pessoa está falecida. |
| `isDependent` | Booleano | Indica se a pessoa é um dependente. |
| `nationality` | String | A relação jurídica entre a pessoa e seu estado, representada por meio do código ISO 3166-1 Alpha-2. |
| `preferredAvailability` | String | A disponibilidade de dia e hora preferencial da pessoa para um compromisso. |
| `primaryMemberID` | String | Um identificador exclusivo do assinante principal se a pessoa for dependente. |

{style=&quot;table-layout:auto&quot;}

Para obter mais detalhes sobre o grupo de campos, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-healthcare-member.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-healthcare-member.schema.json)

Consulte a documentação do schema do setor para obter mais informações sobre como esse grupo de campos pode ser usado para servir [casos de uso da indústria de saúde](../../schema/industries/healthcare.md).
