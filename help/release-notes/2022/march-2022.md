---
title: Notas de versão da Adobe Experience Platform
description: As notas de versão mais recentes do Adobe Experience Platform.
exl-id: 0d499aa6-e25d-4d34-ad32-5e4ab361cba1
source-git-commit: 3f1750d75bd69c5cf47eb593144f564564f90405
workflow-type: tm+mt
source-wordcount: '1193'
ht-degree: 6%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 30 de março de 2022**

New features in Adobe Experience Platform:

- [Audit logs](#audit-logs)
- [Related accounts in Real-Time CDP B2B Edition](#related-accounts)

Atualizações dos recursos existentes na Adobe Experience Platform:

- [Alertas](#alerts)
- [[!DNL Dashboards]](#dashboards)
- [Data collection](#data-collection)
- [[!DNL Query Service]](#query-service)
- [Fontes](#sources)

<!-- - [Experience Data Model (XDM)](#xdm) -->

## Audit Logs {#audit-logs}

Experience Platform allows you to audit user activity for various services and capabilities. The audit logs provide information about who did what and when.

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Audit logs for Dataset, Schema, Class, Field group, Data type, Sandbox, Destination, Segment, Merge policy, Computed attribute, Product profile and Account (Adobe) | These are the resources which are recorded by audit logs. If the feature is enabled, the audit logs will be automatically collected as activity occurs. You do not need to manually enable log collection. |
| Export audit logs | `CSV``JSON` The generated files are saved directly to your machine. |

{style=&quot;table-layout:auto&quot;}

[](../../landing/governance-privacy-security/audit-logs/overview.md)

## Related accounts in Real-Time CDP B2B Edition {#related-accounts}

>[!NOTE]
>
>The Related accounts feature is available for customers of the Real-Time CDP B2B Edition only.

B2B enterprises often have their customer information stored in multiple systems, each including only partial or even conflicting data for the same real-world business entity. This creates a massive challenge of arriving at an accurate view of their customers, therefore reducing the efficiency and effectiveness of their B2B marketing and sales efforts. [!DNL Real-time CDP B2B] You can include the related accounts in your segment definitions to broaden your reach or apply wider criteria in your segments.

Read more about the feature in the following documentation pages:

- [Related accounts in Real-Time CDP B2B Edition overview](../../rtcdp/b2b-ai-ml-services/related-accounts.md)
- [Related accounts tab in the Account profile UI guide](../../rtcdp/accounts/account-profile-ui-guide.md#related-accounts-tab)
- [How to use related accounts in segment definitions](../../rtcdp/segmentation/b2b.md#related-accounts)

[](../../rtcdp/overview.md)

## Alertas {#alerts}

Experience Platform allows you to subscribe to event-based alerts for various Platform activities. 

****

| Recurso | Descrição |
| --- | --- |
| New alert rules | Two new alert rules are now available for sources related to data ingestion. [](../../observability/alerts/rules.md) |

{style=&quot;table-layout:auto&quot;}

[](../../observability/alerts/overview.md)

## Painéis {#dashboards}

[!DNL dashboards]

### Profile Dashboards

The Profiles dashboard displays a snapshot of the attribute (record) data that your organization has within the Profile Store in Experience Platform.

****

| Recurso | Descrição |
| --- | --- |
| Unsegmented Profiles widget | The widget provides the total number of all profiles not attached to any segment. The number generated is accurate as of the last snapshot and represents the opportunity for profile activation across your organization. [](../../dashboards/guides/profiles.md#standard-widgets) |
| Unsegmented Profiles Trend widget | This widget provides a line graph illustration for the number of profiles that are not attached to any segment over a given period of time. The trend can be visualized over 30 days, 90 days, and 12 month periods. [](../../dashboards/guides/profiles.md#standard-widgets) |
| Unsegmented Profiles by Identity widget | This widget categorizes the total number of unsegmented profiles by their unique identifier. The data is visualized in a bar chart. [](../../dashboards/guides/profiles.md#standard-widgets) |
| Single identity profiles widget | This widget provides a count of your organization&#39;s profiles that only have one type of ID type that creates their identity, either an email or ECID. [](../../dashboards/guides/profiles.md#standard-widgets) |

{style=&quot;table-layout:auto&quot;}

[](../../dashboards/guides/profiles.md)

### Destinations Dashboards

The Destinations dashboard displays a snapshot of the destinations that your organization has enabled within Experience Platform.

****

| Recurso | Descrição |
| --- | --- |
| Destinations count widget | The widget provides the total number of available endpoints where an audience can be activated and delivered within the system. This number includes both active and inactive destinations. [](../../dashboards/guides/destinations.md#standard-widgets) |

{style=&quot;table-layout:auto&quot;}

[](../../dashboards/guides/destinations.md)

## Data collection {#data-collection}

Platform provides a suite of technologies that allow you to collect client-side customer experience data and send it to the Adobe Experience Platform Edge Network where it can be enriched, transformed, and distributed to Adobe or non-Adobe destinations.

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Global datastream settings | You can now configure several new global settings when configuring a datastream: geo location, first-party ID cookie, and third-party ID sync. [](../../edge/fundamentals/datastreams.md#configure) |
| [](../../server-api/overview.md) | The Server API allows customers to interact with the Experience Platform Edge Network using a new, authenticated endpoint, to power a variety of data collection, personalization, advertising and marketing use cases. |

[](../../collection/home.md)

<!-- ## Experience Data Model (XDM) {#xdm}

Experience Data Model (XDM) is an open-source specification that provides common structures and definitions (schemas) for data that is brought into Adobe Experience Platform. By adhering to XDM standards, all customer experience data can be incorporated into a common representation to deliver insights in a faster, more integrated way. You can gain valuable insights from customer actions, define customer audiences through segments, and use customer attributes for personalization purposes.

| Feature | Description |
| --- | --- |
| Add or remove individual standard fields for a schema | The Schema Editor UI now allows you to add portions of standard field groups to your schemas, providing more flexibility for the fields you choose to include without needing to build custom resources from scratch.<br><br>You can now also define ad-hoc custom fields directly within the schema structure and assign them to a new or existing custom field group without needing to create or edit the field group beforehand.<br><br>See the guide on [creating and editing schemas in the UI](../../xdm/ui/resources/schemas.md) for more information on these new workflows. |

{style="table-layout:auto"}

For more information on XDM in Platform, see the [XDM System overview](../../xdm/home.md). -->

## Serviço de query {#query-service}

[!DNL Query Service][!DNL Data Lake] [!DNL Data Lake]

****

| Recurso | Descrição |
| --- | --- |
| `table_exists` | The new feature command is used to confirm whether or not a table currently exists in the system. `true`****`false`**** [](../../query-service/sql/syntax.md) |

{style=&quot;table-layout:auto&quot;}

[](../../query-service/home.md)

## Fontes {#sources}

Adobe Experience Platform can ingest data from external sources while allowing you to structure, label, and enhance that data using Platform services. You can ingest data from a variety of sources such as Adobe applications, cloud-based storage, third-party software, and your CRM system.

Experience Platform provides a RESTful API and an interactive UI that lets you set up source connections for various data providers with ease. These source connections allow you to authenticate and connect to external storage systems and CRM services, set times for ingestion runs, and manage data ingestion throughout.

****

| Recurso | Descrição |
| --- | --- |
| New sources now available for B2B usage | You can now use all the available sources on Platform for B2B use cases. [](../../sources/home.md) |
| [!DNL Oracle Eloqua] | [!DNL Oracle Eloqua][!DNL Oracle Eloqua] [ [!DNL Oracle Eloqua] ](../../sources/connectors/marketing-automation/oracle-eloqua.md) |
| [!DNL Data Landing Zone] | [!DNL Data Landing Zone][!DNL Flow Service] [ [!DNL Data Landing Zone] ](../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md) |

{style=&quot;table-layout:auto&quot;}

[](../../sources/home.md)
