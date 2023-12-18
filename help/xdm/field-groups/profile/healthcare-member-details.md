---
title: Grupo de Campos de Esquema de Detalhes de Membro de Assistência Médica
description: Saiba mais sobre o grupo de campos de esquema Detalhes do membro do plano de saúde.
exl-id: 43ba025e-2acf-4cb7-8487-e6c7c7240867
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 2%

---

# [!UICONTROL Detalhes do membro da área de saúde] grupo de campos de esquema

[!UICONTROL Detalhes do membro da área de saúde] é um grupo de campos de esquema padrão para o [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md) que captura detalhes de uma pessoa que tem ou receberá serviço ou cuidados médicos, como informações de contato, médico de assistência médica e informações do plano.

![Estrutura do grupo de campos](../../images/field-groups/healthcare-member-details/structure.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `billingAddress` | [[!UICONTROL Endereço postal]](../../data-types/postal-address.md) | O endereço de cobrança da pessoa. |
| `faxPhone` | [[!UICONTROL Número de telefone]](../../data-types/phone-number.md) | O número de fax da pessoa. |
| `homeAddress` | [[!UICONTROL Endereço postal]](../../data-types/postal-address.md) | O endereço residencial da pessoa. |
| `homePhone` | [[!UICONTROL Número de telefone]](../../data-types/phone-number.md) | O número de telefone residencial da pessoa. |
| `mailingAddress` | [[!UICONTROL Endereço postal]](../../data-types/postal-address.md) | O endereço para correspondência da pessoa. |
| `memberDetails` | Objeto | Um objeto que contém informações detalhadas sobre os atributos e relacionamentos da pessoa relacionados ao tratamento de saúde. Consulte a [subseção abaixo](#memberDetails) para obter mais informações sobre a estrutura do objeto. |
| `mobilePhone` | [[!UICONTROL Número de telefone]](../../data-types/phone-number.md) | O número do celular da pessoa. |
| `person` | [[!UICONTROL Pessoa]](../../data-types/person.md) | Um ator individual, contato ou proprietário relacionado à associação da pessoa ao plano de saúde. |
| `personalEmail` | [[!UICONTROL Endereço de email]](../../data-types/email-address.md) | O endereço de email pessoal da pessoa. |
| `shippingAddress` | [[!UICONTROL Endereço postal]](../../data-types/postal-address.md) | O endereço de entrega da pessoa. |

{style="table-layout:auto"}

## `memberDetails` {#memberDetails}

`memberDetails` é um objeto que contém informações detalhadas sobre os atributos e relacionamentos da pessoa relacionados ao tratamento de saúde. A estrutura do `memberDetails` é descrita abaixo.

![estrutura memberDetails](../../images/field-groups/healthcare-member-details/memberDetails.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `emergencyContact` | Objeto | Registra os seguintes detalhes de contato de emergência da pessoa: <ul><li>`fullName`: (String) O nome completo do contato de emergência.</li><li>`phone`: (String) O número de telefone do contato de emergência.</li><li>`relationshipToMember`: (String) A relação do contato de emergência com a pessoa.</li></ul> |
| `medications` | Matriz de objetos | Lista os detalhes dos medicamentos atuais e anteriores associados à pessoa. Cada item da matriz é um objeto que captura os seguintes detalhes: <ul><li>`refillLocation`: ([[!UICONTROL Endereço postal]](../../data-types/postal-address.md)) O local de recarga para o medicamento.</li><li>`ID`: (String) ID da medicação.</li><li>`isCurrent`: (Booleano) Indica se o medicamento é atual ou passado.</li><li>`numberOfRefills`: (número inteiro) o número de recargas receitadas pelo fornecedor deste medicamento.</li><li>`startDate`: (DateTime) A data em que a pessoa começou a tomar o medicamento.</li></ul> |
| `multipleBirth` | Objeto | Captura detalhes relacionados a múltiplos nascimentos: <ul><li>`isMultipleBirth`: (booleano) indica se a pessoa deu vários nascimentos.</li><li>`multipleBirthNumber`: (número inteiro) o número de bebês nascidos se `isMultipleBirth` é verdadeiro.</li></ul> |
| `plans` | Matriz de objetos | Lista os detalhes dos planos médicos atuais e anteriores associados à pessoa. Cada item da matriz é um objeto que captura os seguintes detalhes: <ul><li>`coverageEndDate`: (DateTime) A data em que a cobertura do plano termina.</li><li>`coverageStartDate`: (DateTime) A data em que a cobertura do plano começa.</li><li>`isActive`: (Booleano) Indica se o plano está ativo.</li><li>`planId`: (String) a ID do plano.</li></ul> |
| `primaryCarePhysicians` | Matriz de objetos | Lista os detalhes dos médicos de cuidados primários associados à pessoa. Cada item da matriz é um objeto que captura os seguintes detalhes: <ul><li>`endDate`: (DateTime) A data em que o médico de cuidados primários terminou o tratamento da pessoa.</li><li>`fullname`: (String) O nome completo do médico.</li><li>`providerId`: (String) Um identificador exclusivo do médico.</li><li>`startDate`: (DateTime) A data em que o médico de cuidados primários iniciou o cuidado da pessoa.</li></ul> |
| `specialists` | Matriz de objetos | Lista os detalhes dos especialistas em saúde associados à pessoa. Cada item da matriz é um objeto que captura os seguintes detalhes: <ul><li>`fullname`: (String) O nome completo do especialista.</li><li>`providerId`: (String) Um identificador exclusivo do especialista.</li><li>`specialty`: (String) A especialidade do provedor (como anestesiologia, urologia, radiologia, dermatologia e assim por diante).</li></ul> |
| `beneficiaryRelationship` | String | O relacionamento do beneficiário com o membro do plano de saúde se a pessoa for um dependente (exemplos incluem ele mesmo, cônjuge, filho etc.). |
| `billingAccountID` | String | Um identificador exclusivo da conta de cobrança da pessoa. |
| `dateAgeCollected` | DateTime | A data em que a idade da pessoa foi coletada. |
| `deceasedDate` | DateTime | A data em que a pessoa morreu se estiver falecida. |
| `isDeceased` | Booleano | Indica se a pessoa faleceu. |
| `isDependent` | Booleano | Indica se a pessoa é dependente. |
| `nationality` | String | A relação jurídica entre a pessoa e seu estado, representada usando o código ISO 3166-1 Alpha-2. |
| `preferredAvailability` | String | A disponibilidade de dia e hora preferencial da pessoa para um compromisso. |
| `primaryMemberID` | String | Um identificador exclusivo do assinante principal se a pessoa for dependente. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o grupo de campos, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-healthcare-member.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-healthcare-member.schema.json)

Consulte a documentação do esquema do setor para obter mais informações sobre como esse grupo de campos pode ser usado para servir [casos de uso do setor de saúde](../../schema/industries/healthcare.md).
