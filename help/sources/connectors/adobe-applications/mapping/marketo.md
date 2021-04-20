---
keywords: Experience Platform, home, tópicos populares, Marketo Engage, marketing, engajamento, Marketo, mapeamento
solution: Experience Platform
title: Mapeamento de campos para a fonte de Marketo Engage
topic: visão geral
description: As tabelas abaixo contêm os mapeamentos entre os campos nos conjuntos de dados do Marketo e seus campos XDM correspondentes.
translation-type: tm+mt
source-git-commit: 2563b413ec35cb4c5f05a54bce6f7271917e51f3
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 3%

---


# (Beta) [!DNL Marketo Engage] mapeamentos de campos

>[!IMPORTANT]
>
>A fonte [!DNL Marketo Engage] está atualmente em beta. Seus recursos e a documentação estão sujeitos a alterações.

As tabelas abaixo contêm os mapeamentos entre os campos nos nove conjuntos de dados [!DNL Marketo] e seus campos correspondentes do Experience Data Model (XDM).

## Atividades {#activities}

| Conjunto de dados de origem | Campo de destino XDM | Notas |
| -------------- | ---------------- | ----- |
| `_id` | `_id` |
| `personID` | `personID` | Identidade primária |
| `eventType` | `eventType` |
| `timeStamp` | `timestamp` |
| `web.webPageDetails._marketo.URL` | `web.webPageDetails._marketo.URL` |
| `environment.browserDetails.userAgent` | `environment.browserDetails.userAgent` |
| `environment.ipV4` | `environment.ipV4` |
| `search.keywords` | `search.keywords` |
| `search.searchEngine` | `search.searchEngine` |
| `web.webPageDetails.webPageID` | `web.webPageDetails.webPageID` |
| `web.webPageDetails.name` | `web.webPageDetails.name` |
| `web.webPageDetails.isPersonalizedURL` | `web.webPageDetails.isPersonalizedURL` |
| `web.webPageDetails.queryParameters` | `web.webPageDetails.queryParameters` |
| `web.webReferrer.URL` | `web.webReferrer.URL` |
| `listOperations.listID` | `listOperations.listID` |
| `opportunityEvent.isPrimary` | `opportunityEvent.isPrimary` |
| `opportunityEvent.opportunityID` | `opportunityEvent.opportunityID` |
| `opportunityEvent.role` | `opportunityEvent.role` |
| `leadOperation.newLead.createdDate` | `leadOperation.newLead.createdDate` |
| `leadOperation.newLead.formName` | `leadOperation.newLead.formName` |
| `leadOperation.newLead.leadSource` | `leadOperation.newLead.leadSource` |
| `leadOperation.newLead.listName` | `leadOperation.newLead.listName` |
| `leadOperation.newLead.sfdcType` | `leadOperation.newLead.sfdcType` |
| `leadOperation.newLead.sourceType` | `leadOperation.newLead.sourceType` |
| `leadOperation.convertLead.assignTo` | `leadOperation.convertLead.assignTo` |
| `leadOperation.convertLead.convertedStatus` | `leadOperation.convertLead.convertedStatus` |
| `leadOperation.convertLead.isSentNotificationEmail` | `leadOperation.convertLead.isSentNotificationEmail` |
| `directMarketing.mailingID` | `directMarketing.mailingID` |
| `directMarketing.mailingName` | `directMarketing.mailingName` |
| `directMarketing.testVariantID` | `directMarketing.testVariantID` |
| `directMarketing.testVariantName` | `directMarketing.testVariantName` |
| `directMarketing.emailBouncedCode` | `directMarketing.emailBouncedCode` |
| `directMarketing.emailBouncedDetails` | `directMarketing.emailBouncedDetails` |
| `directMarketing.email` | `directMarketing.email` |
| `device.isMobileDevice` | `device.isMobileDevice` |
| `device.model` | `device.model` |
| `environment.operatingSystem` | `environment.operatingSystem` |
| `directMarketing.linkURL` | `directMarketing.linkURL` |
| `web.webInteraction.linkID` | `web.webInteraction.linkID` |
| `web.fillOutForm.webFormID` | `web.fillOutForm.webFormID` |
| `web.fillOutForm.webFormName` | `web.fillOutForm.webFormName` |
| `web.webInteraction.linkURL` | `web.webInteraction.linkURL` |
| `leadOperation.changeScore.changeValue` | `leadOperation.changeScore.changeValue` |
| `leadOperation.changeScore.newValue` | `leadOperation.changeScore.newValue` |
| `leadOperation.changeScore.oldValue` | `leadOperation.changeScore.oldValue` |
| `leadOperation.changeScore.priority` | `leadOperation.changeScore.priority` |
| `leadOperation.changeScore.reason` | `leadOperation.changeScore.reason` |
| `leadOperation.changeScore.relativeScore` | `leadOperation.changeScore.relativeScore` |
| `leadOperation.changeScore.relativeUrgency` | `leadOperation.changeScore.relativeUrgency` |
| `leadOperation.changeScore.scoreAttributeID` | `leadOperation.changeScore.scoreAttributeID` |
| `leadOperation.changeScore.scoreAttributeName` | `leadOperation.changeScore.scoreAttributeName` |
| `leadOperation.changeScore.urgency` | `leadOperation.changeScore.urgency` |
| `opportunityEvent.dataValueChanges.attributeName` | `opportunityEvent.dataValueChanges.attributeName` |
| `opportunityEvent.dataValueChanges.newValue` | `opportunityEvent.dataValueChanges.newValue` |
| `opportunityEvent.dataValueChanges.oldValue` | `opportunityEvent.dataValueChanges.oldValue` |
| `opportunityEvent.opportunityID` | `opportunityEvent.opportunityID` |
| `leadOperation.campaignProgression.campaignID` | `leadOperation.campaignProgression.campaignID` |
| `leadOperation.campaignProgression.isAcquiredBy` | `leadOperation.campaignProgression.isAcquiredBy` |
| `leadOperation.campaignProgression.isSuccessful` | `leadOperation.campaignProgression.isSuccessful` |
| `leadOperation.campaignProgression.newStatusID` | `leadOperation.campaignProgression.newStatusID` |
| `leadOperation.campaignProgression.newStatusName` | `leadOperation.campaignProgression.newStatusName` |
| `leadOperation.campaignProgression.oldStatusID` | `leadOperation.campaignProgression.oldStatusID` |
| `leadOperation.campaignProgression.oldStatusName` | `leadOperation.campaignProgression.oldStatusName` |
| `leadOperation.campaignProgression.reason` | `leadOperation.campaignProgression.reason` |

{style=&quot;table-layout:auto&quot;}

## Programas {#programs}

| Conjunto de dados de origem | Campo de destino XDM | Notas |
| -------------- | ---------------- | ----- |
| `id` | `campaignID` | Identidade principal |
| `sfdcId` | `extSourceSystemAudit.externalID` | Identidade secundária |
| `name` | `campaignName` |
| `description` | `campaignDescription` |
| `type` | `campaignType` |
| `status` | `campaignStatus` |
| `channel` | `channelName` |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |
| `cost` | `actualCost.amount` |
| `parentProgramId` | `parentCampaignID` |
| `integrationPartner` | `integrationPartnerName` |
| `startDate` | `campaignStartDate` |
| `endDate` | `campaignEndDate` |

{style=&quot;table-layout:auto&quot;}

## Associações do Programa {#program-memberships}

| Conjunto de dados de origem | Campo de destino XDM | Notas |
| -------------- | ---------------- | ----- |
| `id` | `campaignMemberID` | Identidade principal |
| `programId` | `campaignID` | Relação |
| `leadId` | `personID` | Relação |
| `acquiredByCampaignID` | `acquiredByCampaignID` |
| `reachedSuccess` | `hasReachedSuccess` |
| `isExhausted` | `isExhausted` |
| `statusName` | `memberStatus` |
| `statusReason` | `memberStatusReason` |
| `membershipDate` | `membershipDate` |
| `nurtureCadence` | `nurtureCadence` |
| `trackName` | `nurtureTrackName` |
| `webinarUrl` | `webinarConfirmationUrl` |
| `registrationCode` | `webinarRegistrationID` |
| `reachedSuccessDate` | `reachedSuccessDate` |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |

{style=&quot;table-layout:auto&quot;}

## Empresas {#companies}

| Conjunto de dados de origem | Campo de destino XDM | Notas |
| -------------- | ---------------- | ----- |
| `id` | `accountID` | Identidade principal |
| `mktoCdpExternalId` | `extSourceSystemAudit.externalID` | Identidade secundária |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |
| `billingCity` | `accountBillingAddress.city` |
| `billingCountry` | `accountBillingAddress.country` |
| `billingPostalCode` | `accountBillingAddress.postalCode` |
| `billingState` | `accountBillingAddress.state` |
| `billingStreet` | `accountBillingAddress.street1` |
| `annualRevenue` | `accountOrganization.annualRevenue.amount` |
| `sicCode` | `accountOrganization.SICCode` |
| `industry` | `accountOrganization.industry` |
| `numberOfEmployees` | `accountOrganization.numberOfEmployees` |
| `website` | `accountOrganization.website` |
| `mainPhone` | `accountPhone.number` |
| `company` | `accountName` |
| `companyNotes` | `accountDescription` |
| `site` | `accountSite` |

{style=&quot;table-layout:auto&quot;}

## Listas estáticas {#static-lists}

| Conjunto de dados de origem | Campo de destino XDM | Notas |
| -------------- | ---------------- | ----- |
| `id` | `marketingListID` | Identidade principal |
| `name` | `marketingListName` |
| `description` | `marketingListDescription` |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |

{style=&quot;table-layout:auto&quot;}

## Associações da lista estática {#static-list-memnberships}

| Conjunto de dados de origem | Campo de destino XDM | Notas |
| -------------- | ---------------- | ----- |
| `marketingListMemberID` | `staticListMemberID` | Identidade principal |
| `marketingListID` | `staticListID` | Relação |
| `personID` | `personID` | Relação |
| `createdAt` | `extSourceSystemAudit.createdDate` |

{style=&quot;table-layout:auto&quot;}

## Contas nomeadas {#named-accounts}

>[!IMPORTANT]
>
>O conjunto de dados de contas nomeadas é necessário somente com o recurso de ABM (Account-Based Marketing, marketing baseado em conta) da Marketo. Se você não estiver usando o ABM, não precisará configurar mapeamentos para contas nomeadas.

| Conjunto de dados de origem | Campo de destino XDM | Notas |
| -------------- | ---------------- | ----- |
| `id` | `accountID` | Identidade principal |
| `crmGuid` | `extSourceSystemAudit.externalID` | Identidade secundária |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |
| `city` | `accountBillingAddress.city` |
| `country` | `accountBillingAddress.country` |
| `state` | `accountBillingAddress.state` |
| `annualRevenue` | `accountOrganization.annualRevenue.amount` |
| `sicCode` | `accountOrganization.SICCode` |
| `industry` | `accountOrganization.industry` |
| `logoUrl` | `accountOrganization.logoUrl` |
| `numberOfEmployees` | `accountOrganization.numberOfEmployees` |
| `name` | `accountName` |
| `parentAccountId` | `accountParentID` |
| `sourceType` | `accountSourceType` |

{style=&quot;table-layout:auto&quot;}

## Oportunidades {#opportunities}

| Conjunto de dados de origem | Campo de destino XDM | Notas |
| -------------- | ---------------- | ----- |
| `id` | `opportunityID` | Identidade principal |
| `externalOpportunityId` | `extSourceSystemAudit.externalID` | Identidade secundária |
| `mktoCdpAccountOrgId` | `accountID` | Relação |
| `description` | `opportunityDescription` |
| `name` | `opportunityName` |
| `stage` | `opportunityStage` |
| `type` | `opportunityType` |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |
| `expectedRevenue` | `expectedRevenue.amount` |
| `amount` | `opportunityAmount.amount` |
| `closeDate` | `expectedCloseDate` |
| `fiscalQuarter` | `fiscalQuarter` |
| `fiscalYear` | `fiscalYear` |
| `forecastCategory` | `forecastCategory` |
| `forecastCategoryName` | `forecastCategoryName` |
| `isClosed` | `isClosed` |
| `isWon` | `isWon` |
| `quantity` | `opportunityQuantity` |
| `probability` | `probabilityPercentage` |
| `Campaign-ID` | `campaignID` | Recomendado somente se você usar a integração do Salesforce. |
| `lastActivityDate` | `lastActivityDate` |
| `leadSource` | `leadSource` |
| `nextStep` | `nextStep` |

{style=&quot;table-layout:auto&quot;}

## Funções de contato da oportunidade {#opportunity-contact-roles}

| Conjunto de dados de origem | Campo de destino XDM | Notas |
| -------------- | ---------------- | ----- |
| `id` | `opportunityPersonID` | Identidade principal |
| `mktoCdpSfdcId` | `extSourceSystemAudit.externalID` | Identidade secundária |
| `mktoCdpOpptyId` | `opportunityID` | Relação |
| `leadId` | `personID` | Relação |
| `role` | `personRole` |
| `isPrimary` | `isPrimary` |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |

{style=&quot;table-layout:auto&quot;}

## Pessoas {#persons}

No painel [!DNL Profiles] da interface do usuário da plataforma, se o valor da compilação de ID na política de mesclagem usada para navegar estiver definido como `None`, a janela de identidades vinculadas exibirá somente o atributo de identidade principal.

Como solução alternativa, você pode atualizar o campo de identificação de identificação de `None` para `Private graph` para ver todas as identidades vinculadas a um [!DNL Profile]. Como alternativa, você pode criar uma nova política de mesclagem ou usar uma política de mesclagem diferente que contenha um valor de identificação definido como `Private graph`. Se você optar por criar uma nova política de mesclagem ou usar uma política de mesclagem diferente, deverá garantir que a política contenha o mesmo tipo de schema usado para o conjunto de mapeamento [!DNL Marketo] Pessoas. Para obter mais informações, consulte o [guia da interface do usuário de políticas de mesclagem](../../../../profile/ui/merge-policies.md).

| Conjunto de dados de origem | Campo de destino XDM | Notas |
| -------------- | ---------------- | ----- |
| `id` | `personID` | Identidade primária |
| `emailSuspended` | `b2b.personOptInOut._channels.email` |
| `emailSuspendedAt` | `b2b.personOptInOut.optOutDetails.email.optOutDate` |
| `emailSuspendedCause` | `b2b.personOptInOut.optOutDetails.email.optOutReason` |
| `contactCompany` | `b2b.accountID` |
| `marketingSuspended` | `b2b.isMarketingSuspended` |
| `marketingSuspendedCause` | `b2b.marketingSuspendedCause` |
| `leadScore` | `b2b.personScore` |
| `leadSource` | `b2b.personSource` |
| `leadStatus` | `b2b.personStatus` |
| `personType` | `b2b.personType` |
| `leadPartitionId` | `b2b.personGroupID` |
| `mktoCdpCnvContactPersonId` | `b2b.convertedContactID` |
| `mktoCdpIsConverted` | `b2b.isConverted` |
| `mktoCdpConvertedDate` | `b2b.convertedDate` |
| `sfdcId` | `extSourceSystemAudit.externalID` | Identidade secundária |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |
| `title` | `extendedWorkDetails.jobTitle` |
| `fax` | `faxPhone.number` |
| `mobilePhone` | `mobilePhone.number` |
| `firstName` | `person.name.firstName` |
| `lastName` | `person.name.lastName` |
| `middleName` | `person.name.middleName` |
| `salutation` | `person.name.courtesyTitle` |
| `dateOfBirth` | `person.birthDate` |
| `city` | `workAddress.city` |
| `country` | `workAddress.country` |
| `postalCode` | `workAddress.postalCode` |
| `state` | `workAddress.state` |
| `address` | `workAddress.street1` |
| `phone` | `workPhone.number` |
| `company` | `organizations` |
| `leadScore` | `personComponents.personScore` |
| `leadSource` | `personComponents.personSource` |
| `leadStatus` | `personComponents.personStatus` |
| `personType` | `personComponents.personType` |
| `leadPartitionId` | `personComponents.personGroupID` |
| `mktoCdpCnvContactPersonId` | `personComponents.sourceConvertedContactID` |
| `contactCompany` | `personComponents.sourceAccountID` |
| `sfdcContactId` | `personComponents.sourceExternalID` | Recomendado somente se você usar a integração do Salesforce. |
| `id` | `personComponents.sourcePersonID` |
| `email` | `personComponents.workEmail.address` |
| `email` | `workEmail.address` |

{style=&quot;table-layout:auto&quot;}

## Próximas etapas

Ao ler este documento, você ganhou informações sobre a relação de mapeamento entre seus conjuntos de dados [!DNL Marketo] e seus campos XDM correspondentes. Consulte o tutorial em [criar uma [!DNL Marketo] conexão de origem](../../../tutorials/ui/create/adobe-applications/marketo.md) para concluir o fluxo de dados [!DNL Marketo].
