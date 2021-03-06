---
title: Grupo de Campos de Esquema Detalhes da Pessoa Comercial XDM
description: Este documento fornece uma visão geral do grupo de campos Detalhes da pessoa de negócios XDM.
exl-id: e9da5c1c-5a30-4cbc-beb2-cc5efe57cab0
source-git-commit: 0084492ed467c5996a94c5c55a79c9faf8f5046e
workflow-type: tm+mt
source-wordcount: '601'
ht-degree: 6%

---

# [!UICONTROL Detalhes da Pessoa Comercial XDM] grupo de campos de esquema

[!UICONTROL Detalhes da Pessoa Comercial XDM] é um grupo de campos de esquema padrão para a variável [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md) que capta informações sobre uma pessoa no contexto de uma empresa B2B.

![](../../images/field-groups/business-person-details.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `b2b` | Objeto | Um objeto que captura os detalhes específicos de B2B sobre a pessoa. |
| `b2b.accountKey` | [[!UICONTROL Origem B2B]](../../data-types/b2b-source.md) | Um identificador composto para a conta comercial relacionada à pessoa. |
| `b2b.convertedContactKey` | [[!UICONTROL Origem B2B]](../../data-types/b2b-source.md) | Um identificador composto para o contato associado se o lead foi convertido. |
| `b2b.personKey` | [[!UICONTROL Origem B2B]](../../data-types/b2b-source.md) | Um identificador composto para a pessoa ou fragmento de perfil. |
| `b2b.accountID` | String | Uma ID exclusiva para a conta comercial à qual essa pessoa está associada. |
| `b2b.blockedCause` | String | Se a pessoa estiver bloqueada, essa propriedade fornecerá o motivo do bloqueio. |
| `b2b.convertedContactID` | String | A ID de contato se o lead foi convertido com êxito. |
| `b2b.convertedDate` | DateTime | A data da conversão se o lead foi convertido com êxito. |
| `b2b.isBlocked` | Booleano | Indica se a pessoa está bloqueada. |
| `b2b.isConverted` | Booleano | Indica se o lead é convertido. |
| `b2b.isMarketingSuspended` | Booleano | Indica se a comercialização está suspensa para a pessoa. |
| `b2b.marketingSuspendedCause` | String | Se o marketing for suspenso para a pessoa, essa propriedade fornecerá o motivo para isso. |
| `b2b.personGroupID` | String | Um identificador de grupo para a pessoa. |
| `b2b.personScore` | Duplo | Uma pontuação gerada para a pessoa por um sistema de CRM. |
| `b2b.personSource` | String | A fonte da qual a informação da pessoa foi recebida. |
| `b2b.personStatus` | String | O status atual de marketing ou vendas da pessoa. |
| `b2b.personType` | String | O tipo de pessoa B2B. |
| `extSourceSystemAudit` | [Atributos de Auditoria do Sistema de Origem Externa](../../data-types/external-source-system-audit-attributes.md) | Se a relação do empresário for proveniente de um sistema de origem externo, esse objeto capturará atributos de auditoria para esse sistema. |
| `extendedWorkDetails` | Objeto | Captura detalhes adicionais relacionados ao trabalho sobre a pessoa. |
| `extendedWorkDetails.assistantDetails` | Objeto | Captura os seguintes atributos relacionados ao assistente da pessoa: <ul><li>`name`: ([Nome da pessoa](../../data-types/person-name.md)) Nome completo do assistente.</li><li>`phone`: ([Número de telefone](../../data-types/phone-number.md)) O número de telefone do assistente.</li></ul> |
| `extendedWorkDetails.departments` | Matriz de cadeias de caracteres | Uma lista de nomes de departamento onde a pessoa trabalha. |
| `extendedWorkDetails.jobTitle` | String | O cargo da pessoa. |
| `extendedWorkDetails.photoUrl` | String | Um URL para uma foto da pessoa. |
| `extendedWorkDetails.reportsToID` | String | Um identificador para o gerente de relatórios da pessoa. |
| `faxPhone` | [Número de telefone](../../data-types/phone-number.md) | O número do fax da pessoa. |
| `homeAddress` | [Endereço postal](../../data-types/postal-address.md) | O endereço residencial da pessoa. |
| `homePhone` | [Número de telefone](../../data-types/phone-number.md) | O número do telefone da pessoa. |
| `mobilePhone` | [Número de telefone](../../data-types/phone-number.md) | O número do celular da pessoa. |
| `otherAddress` | [Endereço postal](../../data-types/postal-address.md) | Um endereço alternativo para a pessoa. |
| `otherPhone` | [Número de telefone](../../data-types/phone-number.md) | Um número de telefone alternativo para a pessoa. |
| `person` | [Pessoa](../../data-types/person.md) | Um ator individual, contato ou proprietário. |
| `personalEmail` | [Endereço de email](../../data-types/email-address.md) | O endereço de email pessoal da pessoa. |
| `workAddress` | [Endereço postal](../../data-types/postal-address.md) | O endereço de trabalho da pessoa. |
| `workEmail` | [Endereço de email](../../data-types/email-address.md) | O endereço de email da pessoa. |
| `workPhone` | [Número de telefone](../../data-types/phone-number.md) | O número de telefone do trabalho da pessoa. |
| `identityMap` | Mapa | Campo de mapa que contém um conjunto de identidades namespacadas para a pessoa. Este campo é atualizado automaticamente pelo sistema conforme os dados de identidade são assimilados. Para utilizar adequadamente esse campo para [Perfil do cliente em tempo real](../../../profile/home.md), não tente atualizar manualmente o conteúdo do campo em suas operações de dados.<br /><br />Consulte a seção sobre mapas de identidade na [noções básicas da composição do schema](../../schema/composition.md#identityMap) para obter mais informações sobre o caso de uso. |
| `isDeleted` | Booleano | Indica se esta pessoa foi excluída no Marketo Engage.<br><br>Ao usar a variável [Conector de origem Marketo](../../../sources/connectors/adobe-applications/marketo/marketo.md), todos os registros excluídos no Marketo são refletidos automaticamente no Perfil do cliente em tempo real. No entanto, os registros relacionados a esses perfis ainda podem persistir no Data Lake. Ao configurar `isDeleted` para `true`, você pode usar o campo para filtrar quais registros foram excluídos de suas fontes ao consultar o Data Lake. |
| `organizations` | Matriz de cadeias de caracteres | Uma lista de nomes de organizações onde a pessoa trabalha. |

{style=&quot;table-layout:auto&quot;}

Para obter mais detalhes sobre o grupo de campos, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-details.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-details.schema.json)
