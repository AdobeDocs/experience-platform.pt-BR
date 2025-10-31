---
title: Campos de mapeamento do Microsoft Dynamics
description: As tabelas abaixo contêm os mapeamentos entre os campos de origem do Microsoft Dynamics e seus campos XDM correspondentes.
exl-id: 32f51761-5de3-4192-8f23-c1412ca12c08
source-git-commit: 83a249daddbee1ec264b6e505517325c76ac9b09
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 8%

---

# [!DNL Microsoft Dynamics] mapeamentos de campos

As tabelas abaixo contêm os mapeamentos entre os campos de origem [!DNL Microsoft Dynamics] e seus campos correspondentes do Experience Data Model (XDM).

## Contatos {#contacts}

| Campo de origem | Campo XDM do Target | Notas |
| --- | --- | --- |
| `address1_addressid` | `workAddress._id` |  |
| `address1_city` | `workAddress.city` |  |
| `address1_country` | `workAddress.country` |  |
| `address1_county` | `workAddress.stateProvince` |  |
| `address1_latitude` | `workAddress._schema.latitude` |  |
| `address1_line1` | `workAddress.street1` |  |
| `address1_line2` | `workAddress.street2` |  |
| `address1_line3` | `workAddress.street3` |  |
| `address1_longitude` | `workAddress._schema.longitude` |  |
| `address1_postalcode` | `workAddress.postalCode` |  |
| `address1_postofficebox` | `workAddress.postOfficeBox` |  |
| `address1_stateorprovince` | `workAddress.state` |  |
| `assistantname` | `extendedWorkDetails.assistantDetails.name.fullName` |  |
| `assistantphone` | `extendedWorkDetails.assistantDetails.phone.number` |  |
| `birthdate` | `person.birthDate` |  |
| `"Dynamics"` | `b2b.personKey.sourceType` |  |
| `"${CRM_ORG_ID}"` | `b2b.personKey.sourceInstanceID` | O valor de `"${CRM_ORG_ID}"` será substituído automaticamente. |
| `contactid` | `b2b.personKey.sourceID` |  |
| `concat(contactid,"@${CRM_ORG_ID}.Dynamics")` | `b2b.personKey.sourceKey` | Identidade principal. O valor de `"${CRM_ORG_ID}"` será substituído automaticamente. |
| `iif(contactid != null && contactid != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", contactid, "sourceKey", concat(contactid,"@${CRM_ORG_ID}.Dynamics")), null)` | `personComponents.sourcePersonKey` |  |
| `department` | `extendedWorkDetails.departments` |  |
| `fullname` | `person.name.fullName` |  |
| `suffix` | `person.name.suffix` |  |
| `iif(parentcustomerid != null && parentcustomerid != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", parentcustomerid, "sourceKey", concat(parentcustomerid,"@${CRM_ORG_ID}.Dynamics")), null)` | `personComponents.sourceAccountKey` |  |
| `iif(parentcustomerid != null && parentcustomerid != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", parentcustomerid, "sourceKey",  concat(parentcustomerid, "@${CRM_ORG_ID}.Dynamics")), null)` | `b2b.accountKey` |  |
| `createdon` | `extSourceSystemAudit.createdDate` |  |
| `emailaddress1` | `workEmail.address` | Identificador secundário. |
| `emailaddress2` | `personalEmail.address` |  |
| `emailaddress1` | `personComponents.workEmail.address` |  |
| `firstname` | `person.name.firstName` |  |
| `fullname` | `person.name.fullName` |  |
| `lastname` | `person.name.lastName` |  |
| `jobtitle` | `extendedWorkDetails.jobTitle` |  |
| `middlename` | `person.name.middleName` |  |
| `mobilephone` | `mobilePhone.number` |  |
| `modifiedon` | `extSourceSystemAudit.lastUpdatedDate` |  |
| `salutation` | `person.name.courtesyTitle` |  |
| `telephone1` | `workPhone.number` |  |

{style="table-layout:auto"}

## Clientes potenciais {#leads}

| Campo de origem | Campo XDM do Target | Notas |
| --- | --- | --- |
| `address1_addressid` | `workAddress._id` |  |
| `address1_city` | `workAddress.city` |  |
| `address1_country` | `workAddress.country` |  |
| `address1_county` | `workAddress.stateProvince` |  |
| `address1_latitude` | `workAddress._schema.latitude` |  |
| `address1_line1` | `workAddress.street1` |  |
| `address1_line2` | `workAddress.street2` |  |
| `address1_line3` | `workAddress.street3` |  |
| `address1_longitude` | `workAddress._schema.longitude` |  |
| `address1_postalcode` | `workAddress.postalCode` |  |
| `address1_postofficebox` | `workAddress.postOfficeBox` |  |
| `address1_stateorprovince` | `workAddress.state` |  |
| `telephone1` | `workPhone.number` |  |
| `mobilephone` | `mobilePhone.number` |  |
| `createdon` | `extSourceSystemAudit.createdDate` |  |
| `emailaddress1` | `workEmail.address` | Identificador secundário |
| `emailaddress2` | `personalEmail.address` |  |
| `emailaddress1` | `personComponents.workEmail.address` |  |
| `fax` | `faxPhone.number` |  |
| `firstname` | `person.name.firstName` |  |
| `fullname` | `person.name.fullName` |  |
| `jobtitle` | `extendedWorkDetails.jobTitle` |  |
| `lastname` | `person.name.lastName` |  |
| `"Dynamics"` | `b2b.personKey.sourceType` |  |
| `"${CRM_ORG_ID}"` | `b2b.personKey.sourceInstanceID` | O valor de `"${CRM_ORG_ID}"` será substituído automaticamente. |
| `leadid` | `b2b.personKey.sourceID` |  |
| `concat(leadid,"@${CRM_ORG_ID}.Dynamics")` | `b2b.personKey.sourceKey` | Identidade principal. O valor de `"${CRM_ORG_ID}"` será substituído automaticamente. |
| `iif(leadid != null && leadid != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", leadid, "sourceKey", concat(leadid,"@${CRM_ORG_ID}.Dynamics")), null)` | `personComponents.sourcePersonKey` |  |
| `middlename` | `person.name.middleName` |  |
| `mobilephone` | `mobilePhone.number` |  |
| `modifiedon` | `extSourceSystemAudit.lastUpdatedDate` |  |
| `salutation` | `person.name.courtesyTitle` |  |

{style="table-layout:auto"}

## Contas {#accounts}

| Campo de origem | Campo XDM do Target | Notas |
| --- | --- | --- |
| `"Dynamics"` | `accountKey.sourceType` |  |
| `"${CRM_ORG_ID}"` | `accountKey.sourceInstanceID` | O valor de `"${CRM_ORG_ID}"` será substituído automaticamente. |
| `accountid` | `accountKey.sourceID` | Identidade principal. O valor de `"${CRM_ORG_ID}"` será substituído automaticamente. |
| `accountnumber` | `accountNumber` |  |
| `accountratingcode` | `accountOrganization.rating` |  |
| `address1_addressid` | `accountPhysicalAddress._id` |  |
| `address1_city` | `accountPhysicalAddress.city` |  |
| `address1_country` | `accountPhysicalAddress.country` |  |
| `address1_county` | `accountPhysicalAddress.region` |  |
| `address1_latitude` | `accountPhysicalAddress._schema.latitude` |  |
| `address1_line1` | `accountPhysicalAddress.street1` |  |
| `address1_line2` | `accountPhysicalAddress.street2` |  |
| `address1_line3` | `accountPhysicalAddress.street3` |  |
| `address1_longitude` | `accountPhysicalAddress._schema.longitude` |  |
| `address1_name` | `accountPhysicalAddress.label` |  |
| `address1_postalcode` | `accountPhysicalAddress.postalCode` |  |
| `address1_postofficebox` | `accountPhysicalAddress.postOfficeBox` |  |
| `address1_stateorprovince` | `accountPhysicalAddress.state` |  |
| `createdon` | `extSourceSystemAudit.createdDate` |  |
| `description` | `accountDescription` |  |
| `fax` | `accountFax.number` |  |
| `modifiedon` | `extSourceSystemAudit.lastUpdatedDate` |  |
| `name` | `accountName` |  |
| `numberofemployees` | `accountOrganization.numberOfEmployees` |  |
| `revenue` | `accountOrganization.annualRevenue.amount` |  |
| `sic` | `accountOrganization.SICCode` |  |
| `telephone1` | `accountPhone.number` |  |
| `tickersymbol` | `accountOrganization.tickerSymbol` |  |
| `websiteurl` | `accountOrganization.website` |  |
| `concat(accountid,"@${CRM_ORG_ID}.Dynamics")` | `accountKey.sourceKey` |  |

{style="table-layout:auto"}

## Oportunidades {#opportunities}

| Campo de origem | Campo XDM do Target | Notas |
| --- | --- | --- |
| `name` | `opportunityName` |  |
| `"Dynamics"` | `opportunityKey.sourceType` |  |
| `"${CRM_ORG_ID}"` | `opportunityKey.sourceInstanceID` | O valor de `"${CRM_ORG_ID}"` será substituído automaticamente. |
| `iif(parentaccountid != null && parentaccountid != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", parentaccountid, "sourceKey", concat(parentaccountid, "@${CRM_ORG_ID}.Dynamics")), null)` | `accountKey` |  |
| `actualclosedate` | `actualCloseDate` |  |
| `actualvalue` | `opportunityAmount.amount` |  |
| `iif(campaignid != null && campaignid != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", campaignid, "sourceKey", concat(campaignid,"@${CRM_ORG_ID}.Dynamics")), null)` | `campaignKey` |  |
| `closeprobability` | `probabilityPercentage` |  |
| `createdon` | `extSourceSystemAudit.createdDate` |  |
| `description` | `opportunityDescription` |  |
| `estimatedclosedate` | `expectedCloseDate` |  |
| `estimatedvalue` | `expectedRevenue.amount` |  |
| `modifiedon` | `extSourceSystemAudit.lastUpdatedDate` |  |
| `opportunityid` | `opportunityKey.sourceID` |  |
| `concat(opportunityid,"@${CRM_ORG_ID}.Dynamics")` | `opportunityKey.sourceKey` | Identidade principal. O valor de `"${CRM_ORG_ID}"` será substituído automaticamente. |
| `salesstage` | `opportunityStage` |  |
| `stepname` | `nextStep` |  |

{style="table-layout:auto"}

## Funções do contato da oportunidade {#opportunity-contact-roles}

| Campo de origem | Campo XDM do Target | Notas |
| --- | --- | --- |
| `"Dynamics"` | `opportunityPersonKey.sourceType` |  |
| `"${CRM_ORG_ID}"` | `opportunityPersonKey.sourceInstanceID` | O valor de `"${CRM_ORG_ID}"` será substituído automaticamente. |
| `connectionid` | `opportunityPersonKey.sourceID` |  |
| `concat(connectionid,"@${CRM_ORG_ID}.Dynamics")` | `opportunityPersonKey.sourceKey` | Identidade principal. O valor de `"${CRM_ORG_ID}"` será substituído automaticamente. |
| `createdon` | `extSourceSystemAudit.createdDate` |  |
| `modifiedon` | `extSourceSystemAudit.lastUpdatedDate` |  |
| `iif(record1id != null && record1id != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", record1id, "sourceKey", concat(record1id,"@${CRM_ORG_ID}.Dynamics")), null)` | `opportunityKey` |  |
| `iif(record2id != null && record2id != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", record2id, "sourceKey", concat(record2id,"@${CRM_ORG_ID}.Dynamics")), null)` | `personKey` |  |
| `connectionrole1.name` | `personRole` |  |
| `record1objecttypecode` | *Um grupo de campos personalizados deve ser definido como um esquema de destino.* Consulte a seção do apêndice para obter as etapas sobre [como mapear um campo de origem do tipo lista de opções para um esquema XDM de destino](#picklist-type-fields) para obter mais informações. | Para obter uma lista de valores e rótulos possíveis para o campo de origem `record1objecttypecode`, consulte este [[!DNL Microsoft Dynamics] documento de referência da entidade de conexão](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/entities/connection?view=op-9-1#record1objecttypecode-options). |
| `record2objecttypecode` | *Um grupo de campos personalizados deve ser definido como um esquema de destino.* Consulte a seção do apêndice para obter as etapas sobre [como mapear um campo de origem do tipo lista de opções para um esquema XDM de destino](#picklist-type-fields) para obter mais informações. | Para obter uma lista de valores e rótulos possíveis para o campo de origem `record2objecttypecode`, consulte este [[!DNL Microsoft Dynamics] documento de referência da entidade de conexão](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/entities/connection?view=op-9-1#record2objecttypecode-options). |

{style="table-layout:auto"}

## Campanhas {#campaigns}

| Campo de origem | Campo XDM do Target | Notas |
| --- | --- | --- |
| `campaignid` | `campaignKey.sourceID` |  |
| `"${CRM_ORG_ID}"` | `campaignKey.sourceInstanceID` | O valor de `"${CRM_ORG_ID}"` será substituído automaticamente. |
| `concat(campaignid,"@${CRM_ORG_ID}.Dynamics")` | `campaignKey.sourceKey` | Identidade principal. O valor de `"${CRM_ORG_ID}"` será substituído automaticamente. |
| `"Dynamics"` | `campaignKey.sourceType` |  |
| `iif(campaignid != null && campaignid != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", campaignid, "sourceKey", concat(campaignid,"@${CRM_ORG_ID}.Dynamics")), null)` | `extSourceSystemAudit.externalKey` | O `extSourceSystemAudit.externalKey` é a identidade secundária. O valor de `"${CRM_ORG_ID}"` será substituído automaticamente. |
| `createdon` | `extSourceSystemAudit.createdDate` |  |
| `modifiedby` | `extSourceSystemAudit.lastUpdatedBy` |  |
| `modifiedon` | `extSourceSystemAudit.lastUpdatedDate` |  |
| `description` | `campaignDescription` |  |
| `name` | `campaignName` |  |
| `totalactualcost` | `actualCost.amount` |  |
| `budgetedcost` | `budgetedCost.amount` |  |
| `expectedrevenue` | `expectedRevenue.amount` |  |
| `actualend` | `campaignEndDate` |  |
| `actualstart` | `campaignStartDate` |  |
| `expectedresponse` | `expectedResponse` |  |
| `utcconversiontimezonecode` | `timeZone` |  |
| `utcconversiontimezonecode` | `timezoneName` |  |

{style="table-layout:auto"}

## Lista de marketing {#marketing-list}

| Campo de origem | Campo XDM do Target | Notas |
| --- | --- | --- |
| `"Dynamics"` | `marketingListKey.sourceType` |  |
| `"${CRM_ORG_ID}"` | `marketingListKey.sourceInstanceID` | O valor de `"${CRM_ORG_ID}"` será substituído automaticamente. |
| `description` | `marketingListDescription` |  |
| `listname` | `marketingListName` |  |
| `listid` | `marketingListKey.sourceID` |  |
| `concat(listid,"@${CRM_ORG_ID}.Dynamics")` | `marketingListKey.sourceKey` | Identidade principal. O valor de `"${CRM_ORG_ID}"` será substituído automaticamente. |
| `modifiedon` | `extSourceSystemAudit.lastUpdatedDate` |  |
| `createdon` | `extSourceSystemAudit.createdDate` |  |

{style="table-layout:auto"}

## Membros da lista de marketing {#marketing-list-members}

| Campo de origem | Campo XDM do Target | Notas |
| --- | --- | --- |
| `"Dynamics"` | `marketingListMemberKey.sourceType` |  |
| `"${CRM_ORG_ID}"` | `marketingListMemberKey.sourceInstanceID` | O valor de `"${CRM_ORG_ID}"` será substituído automaticamente. |
| `iif(entityid != null && entityid != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", entityid, "sourceKey", concat(entityid,"@${CRM_ORG_ID}.Dynamics")), null)` | `personKey` |
| `listmemberid` | `marketingListMemberKey.sourceID` |  |
| `concat(listmemberid,"@${CRM_ORG_ID}.Dynamics")` | `marketingListMemberKey.sourceKey` | Identidade principal. O valor de `"${CRM_ORG_ID}"` será substituído automaticamente. |
| `iif(listid != null && listid != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", listid, "sourceKey", concat(listid,"@${CRM_ORG_ID}.Dynamics")), null)` | `marketingListKey` |  |
| `createdon` | `extSourceSystemAudit.createdDate` |  |

{style="table-layout:auto"}

## Apêndice

As seções abaixo fornecem informações adicionais que você pode usar ao configurar mapeamentos B2B para sua origem do Dynamics [!DNL Microsoft].

### Campos do tipo lista de opções {#picklist-type-fields}

Você pode usar [campos calculados](../../../../data-prep/ui/mapping.md#calculated-fields) para mapear um campo de origem do tipo lista de opções de [!DNL Microsoft Dynamics] para um campo XDM de destino.

Por exemplo, o campo `genderCode` inclui duas opções:

| Valor | Rótulo |
| --- | --- |
| 1 | `male` |
| 2 | `female` |

Você pode usar as seguintes opções para mapear o campo de origem `genderCode` para o campo de destino `person.gender`:

#### Usar um operador lógico

| Campo de origem | Campo XDM do Target |
| --- | --- |
| `decode(genderCode, "1", "male", "2", "female", "default")` | `person.gender` |

Neste cenário, o valor corresponde à chave, se a chave for encontrada em opções, ou `default`, se `default` estiver presente e a chave não for encontrada. O valor corresponde a `null` se as opções forem `null` ou se não houver `default` e a chave não for encontrada.

#### Usar um campo calculado

| Campo de origem | Campo XDM do Target |
| --- | --- |
| `iif(gendercode.equals("1"),"male",iif(gendercode.equals("2"),"female",null))` | `person.gender` |

>[!TIP]
>
>Uma iteração aninhada da operação acima seria semelhante a: `iif(condition, iif(cond1, tv1, fv1), iif(cond2, tv2, fv2))`.

Para obter mais informações, consulte o [documento sobre operadores lógicos em [!DNL Data Prep]](../../../../data-prep/functions.md##logical-operators)
