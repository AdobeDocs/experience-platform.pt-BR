---
title: 'Notas de versão do Adobe Experience Platform '
description: As notas de versão mais recentes do Experience Platform
doc-type: release notes
last-update: July 15, 2020
author: crhoades, ens25212
translation-type: tm+mt
source-git-commit: 2bbd62fc53d304ff05250688733f1b18dfd18007
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 6%

---


# Notas de versão da Adobe Experience Platform

**Data de lançamento: 15 de julho de 2020**

Atualizações dos recursos existentes no Adobe Experience Platform:

<!-- - [Data Governance](#governance) -->
<!-- - [Real-time Customer Profile](#profile) -->
- [Serviço de segmentação](#segmentation)
- [Fontes](#sources)

<!-- ## [!DNL Data Governance] {#governance}

Adobe Experience Platform Data Governance is a series of strategies and technologies used to manage customer data and ensure compliance with regulations, restrictions, and policies applicable to data usage. It plays a key role within [!DNL Experience Platform] at various levels, including cataloging, data lineage, data usage labeling, data access policies, and access control on data for marketing actions.

**New features**

| Feature    | Description  |
| -----------| ---------- |
| Automatic policy enforcement in [!DNL Real-time Customer Data Platform] | Data usage policies are now automatically enforced in [!DNL Real-time CDP] when violating actions occur, including activating segments to destinations. When a policy violation is triggered, users get real-time visibility into usage restrictions within the activation workflow, indicating what data they cannot use and why.<br><br>See the section on [enforcing data usage compliance](../../rtcdp/privacy/data-governance-overview.md#enforce-data-usage-compliance) within the overview on [!DNL Data Governance] in [!DNL Real-time CDP] for more information. |
| Adobe Audience Manager integration | Any segments that are shared with [!DNL Audience Manager] from [!DNL Platform] inherit any applied data usage labels as [!DNL Data Export Controls], and vice versa. See the [!DNL Audience Manager] documentation for specific [mappings between usage labels and Data Export Controls](https://docs.adobe.com/content/help/en/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aam-data-export-control-in-aep). |
| Custom data usage labels | You can now create custom data usage labels using the Policy Service API or in the UI. See the [labels overview](../../data-governance/labels/overview.md) for more information. |

See the [Data Governance overview](../../data-governance/home.md) for more information on the service.

## [!DNL Real-time Customer Profile] {#profile}

Adobe Experience Platform enables you to drive coordinated, consistent, and relevant experiences for your customers no matter where or when they interact with your brand. With [!DNL Real-time Customer Profile], you can see a holistic view of each individual customer that combines data from multiple channels, including online, offline, CRM, and third party data. [!DNL Profile] allows you to consolidate your disparate customer data into a unified view offering an actionable, timestamped account of every customer interaction.

**New features**

| Feature | Description |
| ------- | ----------- |
| Data usage policy enforcement | In [!DNL Real-time Customer Data Platform], data usage policy violations are automatically surfaced when a violating action in the [!UICONTROL Profile] workspace is attempted. See the [release notes for Data Governance](#governance) for more information on automatic policy enforcement. | 

-->

## [!DNL Segmentation Service] {#segmentation}

O Serviço de segmentação de Adobe Experience Platform fornece uma interface de usuário e uma RESTful API que permite criar segmentos e gerar audiências a partir de seus [!DNL Real-time Customer Profile] dados. Esses segmentos são configurados e mantidos centralmente [!DNL Platform], tornando-os facilmente acessíveis por qualquer aplicativo da Adobe.

[!DNL Segmentation Service] define um subconjunto específico de perfis descrevendo os critérios que distinguem um grupo comercializável de pessoas dentro da sua base de clientes. Os segmentos podem se basear em dados de registro (como informações demográficas) ou em eventos de séries cronológicas que representem as interações do cliente com sua marca.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Segmentação em streaming | A segmentação de fluxo agora pode se qualificar como um usuário em um segmento à medida que os dados chegam, [!DNL Platform]reduzindo drasticamente o tempo de qualificação do segmento. A segmentação de fluxo também reduz a necessidade de executar tarefas de segmentação manualmente. |

<!-- | Data usage policy enforcement | In [!DNL Real-time Customer Data Platform], data usage policy violations are automatically surfaced when a violating action in the [!UICONTROL Segments] workspace is attempted. See the [release notes for Data Governance](#governance) for more information on automatic policy enforcement. | -->

Para obter mais informações sobre [!DNL Segmentation Service], consulte a visão geral da [Segmentação](../../segmentation/home.md)

## Fontes {#sources}

O Adobe Experience Platform pode assimilar dados de fontes externas, permitindo que você estruture, rotule e aprimore esses dados usando [!DNL Platform] serviços. Você pode assimilar dados de várias fontes, como aplicativos da Adobe, armazenamentos baseados em nuvem, software de terceiros e seu sistema de CRM.

O Experience Platform fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem que você se autentique e se conecte a sistemas de armazenamentos externos e serviços CRM, defina horários para execuções de ingestão e gerencie a throughput de ingestão de dados.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Suporte a API e interface para excluir fluxos de dados | Os fluxos de dados que foram feitos com erros ou se tornaram desnecessários agora podem ser excluídos por meio de APIs ou usando a interface do usuário. |
| Suporte a API e interface para ingestão única | A ingestão única para fluxos de dados, onde somente a data do start é fornecida e nenhuma ingestão futura está programada, agora pode ser executada por meio de APIs ou por meio da interface do usuário. |

Para saber mais sobre fontes, consulte a visão geral [das](../../sources/home.md)fontes.
