---
title: Grupo de campos Esquema de detalhes de pessoa de negócios XDM
description: Este documento fornece uma visão geral do grupo de campos de esquema Detalhes de pessoas de negócios XDM.
exl-id: e9da5c1c-5a30-4cbc-beb2-cc5efe57cab0
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 6%

---

# [!UICONTROL Detalhes de pessoa de negócios XDM] grupo de campos de esquema

[!UICONTROL Detalhes de pessoa de negócios XDM] é um grupo de campos de esquema padrão para o [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md) que captura informações sobre uma pessoa individual no contexto de uma empresa B2B (business-to-business).

![](../../images/field-groups/business-person-details.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `b2b` | Objeto | Um objeto que captura os detalhes específicos do B2B sobre a pessoa. |
| `b2b.accountKey` | [[!UICONTROL Origem B2B]](../../data-types/b2b-source.md) | Um identificador composto para a conta comercial relacionada à pessoa. |
| `b2b.convertedContactKey` | [[!UICONTROL Origem B2B]](../../data-types/b2b-source.md) | Um identificador composto para o contato associado se o lead foi convertido. |
| `b2b.personKey` | [[!UICONTROL Origem B2B]](../../data-types/b2b-source.md) | Um identificador composto para a pessoa ou fragmento de perfil. |
| `b2b.accountID` | String | Um identificador exclusivo para a conta comercial à qual essa pessoa está associada. |
| `b2b.blockedCause` | String | Se a pessoa estiver bloqueada, essa propriedade fornecerá o motivo. |
| `b2b.convertedContactID` | String | A ID do contato se o lead foi convertido com sucesso. |
| `b2b.convertedDate` | DateTime | A data de conversão se o lead foi convertido com sucesso. |
| `b2b.isBlocked` | Booleano | Indica se a pessoa está bloqueada. |
| `b2b.isConverted` | Booleano | Indica se o cliente em potencial foi convertido. |
| `b2b.isMarketingSuspended` | Booleano | Indica se o marketing é suspenso para a pessoa. |
| `b2b.marketingSuspendedCause` | String | Se o marketing for suspenso para a pessoa, essa propriedade fornecerá o motivo. |
| `b2b.personGroupID` | String | Um identificador de grupo da pessoa. |
| `b2b.personScore` | Duplo | Uma pontuação gerada para a pessoa por um sistema CRM. |
| `b2b.personSource` | String | A fonte da qual as informações da pessoa foram recebidas. |
| `b2b.personStatus` | String | O status atual de marketing ou vendas da pessoa. |
| `b2b.personType` | String | O tipo de pessoa B2B. |
| `extSourceSystemAudit` | [Atributos de auditoria do sistema de origem externa](../../data-types/external-source-system-audit-attributes.md) | Se a relação comercial vem de um sistema de origem externa, esse objeto captura atributos de auditoria para esse sistema. |
| `extendedWorkDetails` | Objeto | Captura detalhes adicionais relacionados ao trabalho sobre a pessoa. |
| `extendedWorkDetails.assistantDetails` | Objeto | Registra os seguintes atributos relacionados ao assistente da pessoa: <ul><li>`name`: ([Nome da pessoa](../../data-types/person-name.md)O nome completo do assistente.</li><li>`phone`: ([Número de telefone](../../data-types/phone-number.md)) O número de telefone do assistente.</li></ul> |
| `extendedWorkDetails.departments` | Matriz de cadeias de caracteres | Uma lista de nomes de departamento onde a pessoa trabalha. |
| `extendedWorkDetails.jobTitle` | String | O cargo da pessoa. |
| `extendedWorkDetails.photoUrl` | String | Um URL para uma foto da pessoa. |
| `extendedWorkDetails.reportsToID` | String | Um identificador para o gerente de relatórios da pessoa. |
| `faxPhone` | [Número de telefone](../../data-types/phone-number.md) | O número de fax da pessoa. |
| `homeAddress` | [Endereço postal](../../data-types/postal-address.md) | O endereço residencial da pessoa. |
| `homePhone` | [Número de telefone](../../data-types/phone-number.md) | O número de telefone residencial da pessoa. |
| `mobilePhone` | [Número de telefone](../../data-types/phone-number.md) | O número do celular da pessoa. |
| `otherAddress` | [Endereço postal](../../data-types/postal-address.md) | Um endereço alternativo para a pessoa. |
| `otherPhone` | [Número de telefone](../../data-types/phone-number.md) | Um número de telefone alternativo da pessoa. |
| `person` | [Pessoa](../../data-types/person.md) | Um ator, contato ou proprietário individual. |
| `personalEmail` | [Endereço de email](../../data-types/email-address.md) | O endereço de email pessoal da pessoa. |
| `workAddress` | [Endereço postal](../../data-types/postal-address.md) | O endereço comercial da pessoa. |
| `workEmail` | [Endereço de email](../../data-types/email-address.md) | O email comercial da pessoa. |
| `workPhone` | [Número de telefone](../../data-types/phone-number.md) | O número de telefone comercial da pessoa. |
| `identityMap` | Mapa | Um campo de mapa que contém um conjunto de identidades com namespace para a pessoa. Este campo é atualizado automaticamente pelo sistema à medida que os dados de identidade são assimilados. Para utilizar adequadamente esse campo para [Perfil do cliente em tempo real](../../../profile/home.md), não tente atualizar manualmente o conteúdo do campo em suas operações de dados.<br /><br />Consulte a seção sobre mapas de identidade na [noções básicas da composição do esquema](../../schema/composition.md#identityMap) para obter mais informações sobre o caso de uso. |
| `isDeleted` | Booleano | Indica se essa pessoa foi excluída no Marketo Engage.<br><br>Ao usar o [Conector de origem do Marketo](../../../sources/connectors/adobe-applications/marketo/marketo.md), todos os registros excluídos no Marketo são refletidos automaticamente no Perfil do cliente em tempo real. No entanto, os registros relacionados a esses perfis ainda podem persistir no Data Lake. Ao configurar `isDeleted` para `true`, você pode usar o campo para filtrar quais registros foram excluídos de suas fontes ao consultar o Data Lake. |
| `organizations` | Matriz de cadeias de caracteres | Uma lista de nomes de organização em que a pessoa trabalha. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o grupo de campos, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-details.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-details.schema.json)
