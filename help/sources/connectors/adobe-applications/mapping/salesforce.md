---
title: Campos de mapeamento do Salesforce
description: As tabelas abaixo contêm os mapeamentos entre os campos de origem do Salesforce e seus campos XDM correspondentes.
exl-id: 33ee76f2-0495-4acd-a862-c942c0fa3177
source-git-commit: 16cc811a545414021b8686ae303d6112bcf6cebb
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 7%

---

# [!DNL Salesforce] mapeamentos de campos

As tabelas abaixo contêm os mapeamentos entre os campos de origem [!DNL Salesforce] e seus campos correspondentes do Experience Data Model (XDM).

## Contato {#contact}

Leia a [Visão geral do Perfil Individual XDM](../../../../xdm/classes/individual-profile.md) para obter mais informações sobre a classe XDM. Para obter mais informações sobre os grupos de campos XDM, leia o [guia do campo de esquema Detalhes da pessoa de negócios XDM](../../../../xdm/field-groups/profile/business-person-details.md) e o [guia do campo de esquema Componentes da pessoa de negócios XDM](../../../../xdm/field-groups/profile/business-person-components.md).

| Campo de origem | Caminho do campo XDM de destino | Notas |
| --- | --- | --- |
| `AccountId` | `b2b.accountKey.sourceID` |  |
| `iif(AccountId != null && AccountId != "", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_ORG_ID}", "sourceKey", concat(AccountId,"@${CRM_ORG_ID}.Salesforce")), null)` | `b2b.accountKey` |  |
| `iif(AccountId != null && AccountId != "", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", AccountId, "sourceKey", concat(AccountId,"@${CRM_ORG_ID}.Salesforce")), null)` | `personComponents.sourceAccountKey` |  |
| `"Salesforce"` | `b2b.personKey.sourceType` |  |
| `"${CRM_ORG_ID}"` | `b2b.personKey.sourceInstanceID` | O valor de `"${CRM_ORG_ID}"` será substituído automaticamente. |
| `concat(Id,"@${CRM_ORG_ID}.Salesforce")` | `b2b.personKey.sourceKey` | Identidade principal. O valor de `"${CRM_ORG_ID}"` será substituído automaticamente. |
| `AssistantName` | `extendedWorkDetails.assistantDetails.name.fullName` |  |
| `AssistantPhone` | `extendedWorkDetails.assistantDetails.phone.number` |  |
| `Birthdate` | `person.birthDate` |  |
| `CreatedDate` | `extSourceSystemAudit.createdDate` |  |
| `Department` | `extendedWorkDetails.departments` |  |
| `Email` | `workEmail.address` | Identidade secundária. |
| `Email` | `personComponents.workEmail.address` |  |
| `Fax` | `faxPhone.number` |  |
| `FirstName` | `person.name.firstName` |  |
| `HomePhone` | `homePhone.number` |  |
| `isDeleted` | `isDeleted` |  |
| `Id` | `b2b.personKey.sourceID` |  |
| `"Salesforce"` | `personComponents.sourcePersonKey.sourceType` |  |
| `"${CRM_ORG_ID}"` | `personComponents.sourcePersonKey.sourceInstanceID` |  |
| `Id` | `personComponents.sourcePersonKey.sourceID` |  |
| `concat(Id,"@${CRM_ORG_ID}.Salesforce")` | `personComponents.sourcePersonKey.sourceKey` |  |
| `LastActivityDate` | `extSourceSystemAudit.lastActivityDate` |  |
| `LastModifiedDate` | `extSourceSystemAudit.lastUpdatedDate` |  |
| `LastName` | `person.name.lastName` |  |
| `LastReferencedDate` | `extSourceSystemAudit.lastReferencedDate` |  |
| `LastViewedDate` | `extSourceSystemAudit.lastViewedDate` |  |
| `LeadSource` | `b2b.personSource` |  |
| `LeadSource` | `personComponents.personSource` |  |
| `MailingCity` | `workAddress.city` |  |
| `MailingCountry` | `workAddress.country` |  |
| `MailingLatitude` | `workAddress._schema.latitude` |  |
| `MailingLongitude` | `workAddress._schema.longitude` |  |
| `MailingPostalCode` | `workAddress.postalCode` |  |
| `MailingState` | `workAddress.state` |  |
| `MailingStreet` | `workAddress.street1` |  |
| `MobilePhone` | `mobilePhone.number` |  |
| `Name` | `person.name.fullName` |  |
| `OtherCity` | `otherAddress.city` |  |
| `OtherCountry` | `otherAddress.country` |  |
| `OtherLatitude` | `otherAddress._schema.latitude` |  |
| `OtherLongitude` | `otherAddress._schema.longitude` |  |
| `OtherPhone` | `otherPhone.number` |  |
| `OtherPostalCode` | `otherAddress.postalCode` |  |
| `OtherState` | `otherAddress.state` |  |
| `OtherStreet` | `otherAddress.street1` |  |
| `Phone` | `workPhone.number` |  |
| `ReportsToId` | `extendedWorkDetails.reportsToID` |  |
| `Salutation` | `person.name.courtesyTitle` |  |
| `Title` | `extendedWorkDetails.jobTitle` |  |
| `"Contact"` | `b2b.personType` |  |

{style="table-layout:auto"}

## Lead {#lead}

Leia a [Visão geral do Perfil Individual XDM](../../../../xdm/classes/individual-profile.md) para obter mais informações sobre a classe XDM. Para obter mais informações sobre os grupos de campos XDM, leia o [guia do campo de esquema Detalhes da pessoa de negócios XDM](../../../../xdm/field-groups/profile/business-person-details.md) e o [guia do campo de esquema Componentes da pessoa de negócios XDM](../../../../xdm/field-groups/profile/business-person-components.md).

| Campo de origem | Caminho do campo XDM de destino | Notas |
| --- | --- | --- |
| `City` | `workAddress.city` |  |
| `ConvertedDate` | `b2b.convertedDate` |  |
| `Country` | `workAddress.country` |  |
| `Email` | `workEmail.address` | Identidade secundária. |
| `Email` | `personComponents.workEmail.address` |  |
| `Fax` | `faxPhone.number` |  |
| `FirstName` | `person.name.firstName` |  |
| `IsConverted` | `b2b.isConverted` |  |
| `isDeleted` | `isDeleted` |  |
| `"Salesforce"` | `b2b.personKey.sourceType` |  |
| `"${CRM_ORG_ID}"` | `b2b.personKey.sourceInstanceID` |  |
| `Id` | `b2b.personKey.sourceID` |  |
| `concat(Id,"@${CRM_ORG_ID}.Salesforce")` | `b2b.personKey.sourceKey` | Identidade principal. O valor de `"${CRM_ORG_ID}"` será substituído automaticamente. |
| `"Salesforce"` | `personComponents.sourcePersonKey.sourceType` |  |
| `"${CRM_ORG_ID}"` | `personComponents.sourcePersonKey.sourceInstanceID` |  |
| `Id` | `personComponents.sourcePersonKey.sourceID` |  |
| `concat(Id,"@${CRM_ORG_ID}.Salesforce")` | `personComponents.sourcePersonKey.sourceKey` |  |
| `LastActivityDate` | `extSourceSystemAudit.lastActivityDate` |  |
| `LastModifiedDate` | `extSourceSystemAudit.lastUpdatedDate` |  |
| `LastName` | `person.name.lastName` |  |
| `LastReferencedDate` | `extSourceSystemAudit.lastReferencedDate` |  |
| `LastViewedDate` | `extSourceSystemAudit.lastViewedDate` |  |
| `LeadSource` | `b2b.personSource` |  |
| `LeadSource` | `personComponents.personSource` |  |
| `Latitude` | `workAddress._schema.latitude` |  |
| `Longitude` | `workAddress._schema.longitude` |  |
| `Name` | `person.name.fullName` |  |
| `PostalCode` | `workAddress.postalCode` |  |
| `Salutation` | `person.name.courtesyTitle` |  |
| `State` | `workAddress.state` |  |
| `Status` | `b2b.personStatus` |  |
| `Status` | `personComponents.personStatus` |  |
| `Street` | `workAddress.street1` |  |
| `Title` | `extendedWorkDetails.jobTitle` |  |
| `Suffix` | `person.name.suffix` |  |
| `Company` | `b2b.companyName` |  |
| `Website` | `b2b.companyWebsite` |  |
| `ConvertedContactId` | `b2b.convertedContactKey.sourceID` |  |
| `iif(ConvertedContactId != null && ConvertedContactId != "", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_ORG_ID}", "sourceKey", concat(ConvertedContactId,"@${CRM_ORG_ID}.Salesforce")), null)` | `b2b.convertedContactKey` |  |
| `CreatedDate` | `extSourceSystemAudit.createdDate` |  |
| `"Lead"` | `b2b.personType` |  |
| `iif(ConvertedContactId != null && ConvertedContactId != "", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", ConvertedContactId, "sourceKey", concat(ConvertedContactId,"@${CRM_ORG_ID}.Salesforce")), null)` | `personComponents.sourceConvertedContactKey` |  |

{style="table-layout:auto"}

## Conta {#account}

Leia a [visão geral dos detalhes da Conta Comercial XDM](../../../../xdm/classes/b2b/business-account.md) para obter mais informações sobre a classe XDM.

| Campo de origem | Caminho do campo XDM de destino | Notas |
| --- | --- | --- |
| `"Salesforce"` | `accountKey.sourceType` |  |
| `"${CRM_ORG_ID}"` | `accountKey.sourceInstanceID` | O valor de `"${CRM_ORG_ID}"` será substituído automaticamente. |
| `AccountNumber` | `accountNumber` |  |
| `AccountSource` | `accountSourceType` |  |
| `AnnualRevenue` | `accountOrganization.annualRevenue.amount` |  |
| `BillingCity` | `accountBillingAddress.city` |  |
| `BillingCountry` | `accountBillingAddress.country` |  |
| `BillingLatitude` | `accountBillingAddress._schema.latitude` |  |
| `BillingLongitude` | `accountBillingAddress._schema.longitude` |  |
| `BillingPostalCode` | `accountBillingAddress.postalCode` |  |
| `BillingState` | `accountBillingAddress.state` |  |
| `BillingStreet` | `accountBillingAddress.street1` |  |
| `CreatedDate` | `extSourceSystemAudit.createdDate` |  |
| `Description` | `accountDescription` |  |
| `DunsNumber` | `accountOrganization.DUNSNumber` | Recurso do data.com |
| `Fax` | `accountFax.number` |  |
| `isDeleted` | `isDeleted` |  |
| `Id` | `accountKey.sourceID` |  |
| `concat(Id,"@${CRM_ORG_ID}.Salesforce")` | `accountKey.sourceKey` | Identidade principal. O valor de `"${CRM_ORG_ID}"` será substituído automaticamente. |
| `Industry` | `accountOrganization.industry` |  |
| `Jigsaw` | `accountOrganization.jigsaw` |  |
| `LastActivityDate` | `extSourceSystemAudit.lastActivityDate` |  |
| `LastModifiedDate` | `extSourceSystemAudit.lastUpdatedDate` |  |
| `LastReferencedDate` | `extSourceSystemAudit.lastReferencedDate` |  |
| `LastViewedDate` | `extSourceSystemAudit.lastViewedDate` |  |
| `NaicsCode` | `accountOrganization.NAICSCode` | Recurso do data.com |
| `NaicsDesc` | `accountOrganization.NAICSDescription` | Recurso do data.com |
| `Name` | `accountName` |  |
| `NumberOfEmployees` | `accountOrganization.numberOfEmployees` |  |
| `Ownership` | `accountOwnership` |  |
| `ParentId` | `accountParentKey.sourceID` |  |
| `iif(ParentId != null && ParentId != "", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_ORG_ID}", "sourceKey", concat(ParentId,"@${CRM_ORG_ID}.Salesforce")), null)` | `accountParentKey` |  |
| `Phone` | `accountPhone.number` |  |
| `ShippingCity` | `accountShippingAddress.city` |  |
| `ShippingCountry` | `accountShippingAddress.country` |  |
| `ShippingLatitude` | `accountShippingAddress._schema.latitude` |  |
| `ShippingLongitude` | `accountShippingAddress._schema.longitude` |  |
| `ShippingPostalCode` | `accountShippingAddress.postalCode` |  |
| `ShippingState` | `accountShippingAddress.state` |  |
| `ShippingStreet` | `accountShippingAddress.street1` |  |
| `Sic` | `accountOrganization.SICCode` |  |
| `SicDesc` | `accountOrganization.SICDescription` |  |
| `Site` | `accountSite` |  |
| `TickerSymbol` | `accountOrganization.tickerSymbol` |  |
| `Tradestyle` | `accountTradeStyle` | Recurso do data.com |
| `Type` | `accountType` |  |
| `Website` | `accountOrganization.website` |  |

{style="table-layout:auto"}

## Oportunidade {#opportunity}

Leia a [Visão geral da oportunidade de negócios XDM](../../../../xdm/classes/b2b/business-opportunity.md) para obter mais informações sobre a classe XDM.

| Campo de origem | Caminho do campo XDM de destino | Notas |
| --- | --- | --- |
| `"Salesforce"` | `opportunityKey.sourceType` |  |
| `"${CRM_ORG_ID}"` | `opportunityKey.sourceInstanceID` | O valor de `"${CRM_ORG_ID}"` será substituído automaticamente. |
| `concat(Id,"@${CRM_ORG_ID}.Salesforce")` | `opportunityKey.sourceKey` | Identidade principal. O valor de `"${CRM_ORG_ID}"` será substituído automaticamente. |
| `AccountId` | `accountKey.sourceID` |  |
| `iif(AccountId != null && AccountId != "", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_ORG_ID}", "sourceKey", concat(AccountId,"@${CRM_ORG_ID}.Salesforce")), null)` | `accountKey` | Relação. |
| `Amount` | `opportunityAmount.amount` |  |
| `CampaignId` | `campaignKey.sourceID` |  |
| `iif(CampaignId != null && CampaignId != "", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_ORG_ID}", "sourceKey", concat(CampaignId,"@${CRM_ORG_ID}.Salesforce")), null)` | `campaignKey` |  |
| `CloseDate` | `expectedCloseDate` |  |
| `CreatedDate` | `extSourceSystemAudit.createdDate` |  |
| `Description` | `opportunityDescription` |  |
| `ExpectedRevenue` | `expectedRevenue.amount` |  |
| `FiscalQuarter` | `fiscalQuarter` |  |
| `FiscalYear` | `fiscalYear` |  |
| `ForecastCategory` | `forecastCategory` |  |
| `ForecastCategoryName` | `forecastCategoryName` |  |
| `Id` | `opportunityKey.sourceID` |  |
| `IsClosed` | `isClosed` |  |
| `isDeleted` | `isDeleted` |  |
| `IsWon` | `isWon` |  |
| `LastActivityDate` | `extSourceSystemAudit.lastActivityDate` |  |
| `LastModifiedDate` | `extSourceSystemAudit.lastUpdatedDate` |  |
| `LastReferencedDate` | `extSourceSystemAudit.lastReferencedDate` |  |
| `LastViewedDate` | `extSourceSystemAudit.lastViewedDate` |  |
| `LeadSource` | `leadSource` |  |
| `Name` | `opportunityName` |  |
| `NextStep` | `nextStep` |  |
| `Probability` | `probabilityPercentage` |  |
| `StageName` | `opportunityStage` |  |
| `TotalOpportunityQuantity` | `opportunityQuantity` |  |
| `Type` | `opportunityType` |  |
| `CurrencyIsoCode` | `opportunityAmount.currencyCode` |  |

{style="table-layout:auto"}

## Função do contato da oportunidade {#opportunity-contact-role}

Leia a [Visão geral da classe de relação pessoal de oportunidade de negócios XDM](../../../../xdm/classes/b2b/business-opportunity-person-relation.md) para obter mais informações sobre a classe XDM.

| Campo de origem | Caminho do campo XDM de destino | Notas |
| --- | --- | --- |
| `"Salesforce"` | `opportunityPersonKey.sourceType` |  |
| `"${CRM_ORG_ID}"` | `opportunityPersonKey.sourceInstanceID` | O valor de `"${CRM_ORG_ID}"` será substituído automaticamente. |
| `"Salesforce"` | `personKey.sourceType` |  |
| `"${CRM_ORG_ID}"` | `personKey.sourceInstanceID` |  |
| `ContactId` | `personKey.sourceID` |  |
| `concat(ContactId,"@${CRM_ORG_ID}.Salesforce")` | `personKey.sourceKey` |  |
| `CreatedDate` | `extSourceSystemAudit.createdDate` |  |
| `Id` | `opportunityPersonKey.sourceID` |  |
| `concat(Id,"@${CRM_ORG_ID}.Salesforce")` | `opportunityPersonKey.sourceKey` | Identidade principal. O valor de `"${CRM_ORG_ID}"` será substituído automaticamente. |
| `isDeleted` | `isDeleted` |  |
| `IsPrimary` | `isPrimary` |  |
| `LastModifiedDate` | `extSourceSystemAudit.lastUpdatedDate` |  |
| `"Salesforce"` | `opportunityKey.sourceType` |  |
| `"${CRM_ORG_ID}"` | `opportunityKey.sourceInstanceID` |  |
| `OpportunityId` | `opportunityKey.sourceID` |  |
| `concat(OpportunityId,"@${CRM_ORG_ID}.Salesforce")` | `opportunityKey.sourceKey` |  |
| `Role` | `personRole` |  |

{style="table-layout:auto"}

## Campaign {#campaign}

Leia a [visão geral da classe de Campanha Comercial XDM](../../../../xdm/classes/b2b/business-campaign.md) para obter mais informações sobre a classe XDM. Para obter mais informações sobre os grupos de campos XDM, leia o [guia do campo de esquema de detalhes da Campanha de negócios XDM](../../../../xdm/field-groups/b2b-campaign/details.md).

| Campo de origem | Caminho do campo XDM de destino | Notas |
| --- | --- | --- |
| `"Salesforce"` | `campaignKey.sourceType` |  |
| `"${CRM_ORG_ID}"` | `campaignKey.sourceInstanceID` | O valor de `"${CRM_ORG_ID}"` será substituído automaticamente. |
| `isDeleted` | `isDeleted` |  |
| `Id` | `campaignKey.sourceID` |  |
| `concat(Id,"@${CRM_ORG_ID}.Salesforce")` | `campaignKey.sourceKey` | Identidade principal. O valor de `"${CRM_ORG_ID}"` será substituído automaticamente. |
| `Name` | `campaignName` |  |
| `ParentId` | `parentCampaignKey.sourceID` |  |
| `iif(ParentId != null && ParentId != "", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_ORG_ID}", "sourceKey", concat(ParentId,"@${CRM_ORG_ID}.Salesforce")), null)` | `parentCampaignKey` |  |
| `Type` | `campaignType` |  |
| `Status` | `campaignStatus` |  |
| `StartDate` | `campaignStartDate` |  |
| `EndDate` | `campaignEndDate` |  |
| `ExpectedRevenue` | `expectedRevenue.amount` |  |
| `BudgetedCost` | `budgetedCost.amount` |  |
| `ActualCost` | `actualCost.amount` |  |
| `ExpectedResponse` | `expectedResponse` |  |
| `IsActive` | `isActive` |  |
| `Description` | `campaignDescription` |  |
| `CreatedDate` | `extSourceSystemAudit.createdDate` |  |
| `LastModifiedDate` | `extSourceSystemAudit.lastUpdatedDate` |  |
| `LastActivityDate` | `extSourceSystemAudit.lastActivityDate` |  |
| `LastViewedDate` | `extSourceSystemAudit.lastViewedDate` |  |
| `LastReferencedDate` | `extSourceSystemAudit.lastReferencedDate` |  |
| `CurrencyIsoCode` | `actualCost.currencyCode` |  |

## Membro da campanha {#campaign-member}

Leia a [Visão geral dos membros da campanha de negócios XDM](../../../../xdm/classes/b2b/business-campaign-members.md) para obter mais informações sobre a classe XDM. Para obter mais informações sobre os grupos de campos XDM, leia o documento [Grupo de campos de esquema de detalhes do membro da campanha de negócios XDM](../../../../xdm/field-groups/b2b-campaign/details.md).

| Campo de origem | Caminho do campo XDM de destino | Notas |
| --- | --- | --- |
| `"Salesforce"` | `campaignMemberKey.sourceType` |  |
| `"${CRM_ORG_ID}"` | `campaignMemberKey.sourceInstanceID` | O valor de `"${CRM_ORG_ID}"` será substituído automaticamente. |
| `isDeleted` | `isDeleted` |  |
| `Id` | `campaignMemberKey.sourceID` |  |
| `concat(Id,"@${CRM_ORG_ID}.Salesforce")` | `campaignMemberKey.sourceKey` | Identidade principal. O valor de `"${CRM_ORG_ID}"` será substituído automaticamente. |
| `"Salesforce"` | `campaignKey.sourceType` |  |
| `${CRM_ORG_ID}` | `campaignKey.sourceInstanceID` |  |
| `CampaignId` | `campaignKey.sourceID` |  |
| `concat(CampaignId,"@${CRM_ORG_ID}.Salesforce")` | `campaignKey.sourceKey` |  |
| `"Salesforce"` | `personKey.sourceType` |  |
| `${CRM_ORG_ID}` | `personKey.sourceInstanceID` |  |
| `LeadOrContactId` | `personKey.sourceID` |  |
| `concat(LeadOrContactId,"@${CRM_ORG_ID}.Salesforce")` | `personKey.sourceKey` |  |
| `Status` | `memberStatus` |  |
| `HasResponded` | `hasResponded` |  |
| `CreatedDate` | `extSourceSystemAudit.createdDate` |  |
| `LastModifiedDate` | `extSourceSystemAudit.lastUpdatedDate` |  |
| `FirstRespondedDate` | `firstRespondedDate` |  |
| `Type` | `b2b.personType` |  |

## Relação de contato da conta {#account-contact-relation}

Leia a [classe de Relação de Pessoa da Conta Comercial XDM](../../../../xdm/classes/b2b/business-account-person-relation.md) para obter mais informações sobre a classe XDM.

| Campo de origem | Caminho do campo XDM de destino | Notas |
| --- | --- | --- |
| `AccountId` | `accountKey.sourceID` |  |
| `iif(AccountId != null && AccountId != "", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_ORG_ID}", "sourceKey", concat(AccountId,"@${CRM_ORG_ID}.Salesforce")), null)` | `accountKey` |  |
| `ContactId` | `personKey.sourceID` |  |
| `iif(ContactId != null && ContactId != "", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_ORG_ID}", "sourceKey", concat(ContactId,"@${CRM_ORG_ID}.Salesforce")), null)` | `personKey` |  |
| `CreatedById` | `extSourceSystemAudit.createdBy` |  |
| `CreatedDate` | `extSourceSystemAudit.createdDate` |  |
| `EndDate` | `relationEndDate` |  |
| `IsDeleted` | `isDeleted` |  |
| `Id` | `accountPersonKey.sourceID` |  |
| `"Salesforce"` | `accountPersonKey.sourceType` |  |
| `"${CRM_ORG_ID}"` | `accountPersonKey.sourceInstanceID` |  |
| `concat(Id, "@${CRM_ORG_ID}.Salesforce")` | `accountPersonKey.sourceKey` | Identidade principal. |
| `IsActive` | `IsActive` |  |
| `IsDirect` | `IsDirect` |  |
| `LastModifiedById` | `extSourceSystemAudit.lastUpdatedBy` |  |
| `LastModifiedDate` | `extSourceSystemAudit.lastUpdatedDate` |  |
| `explode(Roles,";")` | `personRoles[]` |  |
| `StartDate` | `relationStartDate` |  |

## Próximas etapas

Ao ler este documento, você ganhou o insight na relação de mapeamento entre os campos de origem [!DNL Salesforce] e seus campos XDM correspondentes. Consulte a documentação sobre [criação de uma [!DNL Salesforce] conexão de origem](../../../connectors/crm/salesforce.md) para obter mais informações.
