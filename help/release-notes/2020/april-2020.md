---
title: 'Notas de versão do Adobe Experience Platform '
description: Notas de versão da Experience Platform 8 de abril de 2020
doc-type: release notes
last-update: March 4, 2020
author: ens71067
translation-type: tm+mt
source-git-commit: 3f3704cc1e11a4d11278a34800c8bfdc24a80753

---


# Notas de versão da Adobe Experience Platform

## Data de lançamento: 8 de abril de 2020

## Serviços inteligentes

Os Serviços inteligentes capacitam analistas e profissionais de marketing a aproveitar o poder da inteligência artificial e do aprendizado de máquina em casos de uso de experiência do cliente. Isso permite que os analistas de marketing configurem previsões específicas para as necessidades de uma empresa usando configurações de nível empresarial sem a necessidade de especialização em ciência de dados. Além disso, os profissionais de marketing podem ativar previsões na Adobe Experience Cloud, na Adobe Experience Platform e em aplicativos de terceiros.

**Principais recursos**

| Recurso | Descrição |
|---|---|
| AI do cliente | A IA do cliente fornece aos comerciantes o poder de gerar previsões de clientes a nível individual com explicações. Com a ajuda de fatores influentes, a IA do cliente pode informar o que um cliente deve fazer e por que. Além disso, os profissionais de marketing podem se beneficiar das previsões e insights de IA do cliente para personalizar as experiências do cliente, atendendo às ofertas e mensagens mais apropriadas. |
| Atribuição AI | O AI de atribuição é um serviço de atribuição algorítmico e com vários canais que calcula a influência e o impacto incremental das interações do cliente em relação aos resultados especificados. Com a Atribuição AI, os profissionais de marketing podem medir e otimizar o gasto de marketing e publicidade ao compreender o impacto de cada interação individual do cliente em cada fase das viagens do cliente. |

**Problemas conhecidos**

* Nenhum problema conhecido no momento.

Para obter mais informações sobre os Serviços inteligentes e o que eles têm a oferta, consulte a visão geral [dos Serviços](../../intelligent-services/home.md)inteligentes.

## Privacy Service

As novas regulamentações legais e organizacionais estão dando aos usuários o direito de acessar ou excluir seus dados pessoais dos armazenamentos de dados mediante solicitação. O Adobe Experience Platform Privacy Service fornece uma API RESTful e uma interface de usuário para ajudá-lo a gerenciar essas solicitações de dados de seus clientes. Com o Privacy Service, você pode enviar solicitações para acessar e excluir dados pessoais ou privados de clientes dos aplicativos da Adobe Experience Cloud, facilitando a conformidade automatizada com as regulamentações legais e organizacionais de privacidade.

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Suporte a PDPA | As solicitações de privacidade agora podem ser criadas e rastreadas sob o Personal Data Protection Act (PDPA) na Tailândia. Ao fazer solicitações de privacidade na API, a `regulation` matriz aceita o valor &quot;pdpa_tha&quot;. |
| Tipos de Namespace na interface do usuário | Agora você pode especificar diferentes tipos de namespace no Construtor de solicitações na interface do usuário do Privacy Service. Consulte o guia [do](../../privacy-service/ui/user-guide.md) usuário para obter mais informações. |
| Substituição de ponto final antigo | O ponto de extremidade da API antiga (`data/privacy/gdpr`) foi substituído. |

Problemas conhecidos

* Nenhum

Para obter mais informações sobre o Privacy Service, leia a visão geral [](../../privacy-service/home.md)do Privacy Service para obter start.

## Fontes

A plataforma Adobe Experience pode assimilar dados de fontes externas, permitindo que você estruture, rotule e aprimore esses dados usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos da Adobe, armazenamentos baseados em nuvem, software de terceiros e seu sistema de CRM.

A plataforma Experience fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem que você se autentique e se conecte a sistemas de armazenamentos externos e serviços CRM, defina horários para execuções de ingestão e gerencie a throughput de ingestão de dados.

### Novos recursos

| Recurso | Descrição |
| ------- | ----------- |
| Suporte a API e interface do usuário para bancos de dados | Novos conectores de origem para Apache Spark (em HDInsights), Azure Synapse Analytics, Azure Table Armazenamento, Hive (em HDInsights) e Phoenix. |
| Suporte a API e interface para aplicativos baseados em pagamentos | Novos conectores de origem para o PayPal. |
| Suporte a API e interface para aplicativos baseados em protocolos | Novos conectores de origem para OData genérico. |

### Problemas conhecidos

* Nenhum

Para obter mais informações sobre fontes, consulte a visão geral [das](../../source-connectors/home.md)fontes.

<!-- ## Access control

Experience Platform leverages [Adobe Admin Console](https://adminconsole.adobe.com) product profiles to link users with permissions and sandboxes. Permissions control access to a variety of Platform capabilities, including data modeling, profile management, and sandbox administration.

### Key features

|Feature | Description|
|--- | ---|
|Permissions | In the Admin Console, the _Permissions_ tab within a Platform product profile allows you customize which Platform capabilities are available for the users attached to that profile. Available permission categories include: Data Modeling, Data Management, Profile Management, Identities, Data Monitoring, Sandbox Administration, Destinations, Sources.|
|Access to sandboxes | The _Permissions_ tab within a Platform product profile can grant users access to specific sandboxes. See the section on [sandboxes](#sandboxes) below for more information.|

For more information, please see the [access control overview](../../access-control/home.md).

## Sandboxes

Experience Platform is built to enrich digital experience applications on a global scale. Companies often run multiple digital experience applications in parallel and need to cater for the development, testing, and deployment of these applications while ensuring operational compliance. In order to address this need, Experience Platform provides sandboxes which partition a single Platform instance into separate virtual environments to help develop and evolve digital experience applications.

### Key features

|Feature | Description|
|--- | ---|
|Production sandbox | Experience Platform provides a single production sandbox, which cannot be deleted or reset.|
|Non-production sandboxes | Multiple non-production sandboxes can be created for a single Platform instance, allowing you to test features, run experiments, and make custom configurations without impacting your production sandbox.|
|Sandbox switcher | In the Experience Platform user interface, the sandbox switcher in the top-left corner of the screen allows you to switch between available sandboxes through a dropdown menu.|
|`x-sandbox-name` header | All calls to Experience Platform APIs must now include the new `x-sandbox-name` header, whose value references the `name` attribute of the sandbox the operation will take place in.|

For more information, please see the [sandboxes overview](../../sandboxes/home.md). -->