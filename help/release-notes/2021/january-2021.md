---
title: Notas de versão da Adobe Experience Platform
description: Notas de versão de Experience Platform 27 de janeiro de 2021
doc-type: release notes
last-update: January 27, 2021
author: ens60013
translation-type: tm+mt
source-git-commit: 2e3a6acbfaa7f733a9843068c00f31f0b7f535b6
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 7%

---


# Notas de versão da Adobe Experience Platform

**Data de lançamento: 27 de janeiro de 2021**

Atualizações dos recursos existentes na Adobe Experience Platform:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Destinations]](#destinations)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] permite que os engenheiros de dados mapeiem, transformem e validem dados para e do Experience Data Model (XDM).

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Funções de expressão regular | [!DNL Data Prep] O mapeador agora oferece suporte à correspondência e extração de parte do campo de entrada com base em expressões regulares. |

Para obter mais informações, consulte [[!DNL Data Prep] overview](../../data-prep/home.md).

## Destinos {#destinations}

[!DNL Destinations] são integrações pré-criadas com plataformas de destino que permitem a ativação contínua de dados da Adobe Experience Platform. Você pode usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas por email, publicidade direcionada e muitos outros casos de uso.

**Novos destinos**

| Destino | Descrição |
| ----------- | ----------- |
| [!DNL Azure Blob] | [!DNL Azure Blob] é a solução de armazenamento de objetos da Microsoft para a nuvem. |

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Correspondência avançada de ID | Melhorias nos recursos de taxa de correspondência de audiência em [!DNL Facebook Custom Audiences] e [!DNL Google Customer Match], adicionando suporte para correspondência de identidade adicional, como IDs externas, números de telefone e IDs de dispositivo móvel. Consulte a documentação a seguir para obter mais detalhes: <ul><li>[Destino do Facebook](../../destinations/catalog/social/facebook.md)</li><li>[Destino de Correspondência de Cliente do Google](../../destinations/catalog/advertising/google-customer-match.md)</li><li>[Ativar perfis e segmentos em um destino](../../destinations/ui/activate-destinations.md)</li></ul> |

Para saber mais, visite a [visão geral de destinos](../../destinations/home.md).

## [!DNL Sources] {#sources}

A Adobe Experience Platform pode assimilar dados de fontes externas, permitindo que você estruture, rotule e aprimore esses dados usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos de Adobe, armazenamentos baseados em nuvem, software de terceiros e seu sistema de CRM.

O Experience Platform fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem que você se autentique e se conecte a sistemas de armazenamentos externos e serviços CRM, defina horários para execuções de ingestão e gerencie a throughput de ingestão de dados.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Aprimoramentos no conector de origem Adobe Audience Manager | Agora você pode filtrar e selecionar segmentos primários individuais do Audience Manager para assimilar à plataforma, bem como filtrar características originais. Consulte o tutorial em [criar um conector de origem de Audience Manager](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md) para obter mais informações. |
| [!DNL Google BigQuery] melhorias no conector de origem | Agora é possível assimilar arquivos maiores que 10 GB em uma execução de fluxo usando o conector de origem [!DNL BigQuery]. Consulte [[!DNL BigQuery] visão geral do conector de origem](../../sources/connectors/databases/bigquery.md) para obter mais informações. |
| Suporte para tipos de dados complexos para armazenamentos em nuvem | Agora é possível assimilar tipos de dados complexos, como matrizes em arquivos JSON, ao usar um conector de origem de armazenamento na nuvem. Consulte os tutoriais sobre como criar um fluxo de dados de armazenamento em nuvem [na interface do usuário](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) ou [usando a  [!DNL Flow Service] API](../../sources/tutorials/api/collect/cloud-storage.md) para obter mais informações. |
| Suporte para autenticação baseada em chave principal do serviço para [!DNL Microsoft Dynamics] origem | Agora você pode autenticar em sua conta [!DNL Dynamics] usando uma chave principal de serviço como uma alternativa à autenticação baseada em senha. Consulte [[!DNL Dynamics] visão geral do conector de origem](../../sources/connectors/crm/ms-dynamics.md) para obter mais informações. |
| Suporte de interface para separadores personalizados em fontes de armazenamentos na nuvem | Agora é possível definir um delimitador de coluna personalizado, como uma vírgula (`,`), uma guia (`\t`) ou um pipe (`|`), para coletar arquivos delimitados na interface do usuário. Consulte o tutorial em [criar um fluxo de dados com um conector de origem de armazenamento em nuvem](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) para obter mais informações |

Para saber mais sobre fontes, consulte a [visão geral das fontes](../../sources/home.md).
