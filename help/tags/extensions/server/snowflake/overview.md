---
title: Visão geral do Snowflake
description: Saiba mais sobre o Snowflake para encaminhamento de eventos no Adobe Experience Platform.
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: abddf0c4-3d4c-4f66-a6e0-c10b54ea3430
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---

# Visão geral do [!DNL Snowflake]

[[!DNL Snowflake]](https://www.snowflake.com/en/) é um data warehouse de nuvem que pode armazenar e analisar todos os seus registros de dados em um único local. Ele pode ser usado para data warehouse, data lake, engenharia de dados, ciência de dados, desenvolvimento de aplicativos de dados e compartilhamento e consumo seguros de dados em tempo real ou compartilhados.

O [!DNL Snowflake] foi criado sobre o Amazon Web Services (AWS), o Microsoft Azure (Azure) e a Google Cloud Platform (GCP).

![Um diagrama mostrando a arquitetura de dados [!DNL Snowflake].](../../../images/extensions/server/snowflake/snowflake.png)

## Nossa integração com o Snowflake

Uma conta Snowflake pode ser hospedada em qualquer uma das seguintes plataformas de nuvem:

- [O Amazon Web Services ([!DNL AWS])](https://aws.amazon.com/) - [!DNL AWS] é uma plataforma de computação em nuvem que oferece uma grande variedade de serviços, como computação distribuída, armazenamento em banco de dados, entrega de conteúdo e serviços de integração de software como um serviço (SaaS) para CRM (gerenciamento de relacionamento com o cliente) e ERP (planejamento de recursos corporativos).

Consulte a [[!DNL AWS] visão geral](../aws/overview.md) para obter mais informações sobre como instalar a extensão e configurar as regras de encaminhamento de eventos.

- [Microsoft Azure ([!DNL Azure])](https://azure.microsoft.com/en-us/products/event-hubs/#overview) - [!DNL Azure] é uma plataforma de computação em nuvem e um portal online que permite acessar e gerenciar os serviços e recursos em nuvem fornecidos pela Microsoft.

Consulte a [[!DNL Azure] visão geral](../azure/overview.md) para obter mais informações sobre como instalar a extensão e configurar as regras de encaminhamento de eventos.

- [[!DNL Google Cloud Platform]](https://cloud.google.com/) - [!DNL Google Cloud Platform] é uma plataforma de computação em nuvem que oferece uma grande variedade de serviços, como computação distribuída, armazenamento de banco de dados, entrega de conteúdo e serviços de integração de software como um serviço (SaaS) para CRM (gerenciamento de relacionamento com o cliente) e ERP (planejamento de recursos corporativos).

Consulte a [[!DNL Google Cloud Platform] visão geral](../google-cloud-platform/overview.md) para obter mais informações sobre como instalar a extensão e configurar as regras de encaminhamento de eventos.

Nossas extensões nativas de encaminhamento de eventos do [[!DNL AWS]](../aws/overview.md), [[!DNL Azure]](../azure/overview.md) e [[!DNL Google Cloud Platform]](../google-cloud-platform/overview.md) permitem que os clientes coletem, enriqueçam e encaminhem seus dados de eventos do lado do servidor em tempo real para seus serviços em nuvem, para serem consumidos pelo [!DNL Snowflake]. Consulte abaixo:

![O diagrama de relatórios [!DNL Snowflake] que mostra o vínculo entre [!DNL AWS] e [!DNL Azure].](../../../images/extensions/server/snowflake/snowflake-workflow.png)

## Próximas etapas

Este guia forneceu uma visão geral do [!DNL Snowflake] e do uso de [!DNL AWS] e [!DNL Azure] extensões de encaminhamento de eventos.

Para obter mais informações sobre os recursos de encaminhamento de eventos [!DNL AWS] e [!DNL Azure] no Experience Platform, consulte a [[!DNL AWS] visão geral da extensão](../aws/overview.md) e a [[!DNL Azure] visão geral da extensão](../azure/overview.md).
