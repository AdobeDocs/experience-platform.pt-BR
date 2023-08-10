---
title: Notas da versão de janeiro de 2021 da Adobe Experience Platform
description: As notas da versão de janeiro de 2021 da Adobe Experience Platform.
doc-type: release notes
last-update: January 27, 2021
author: ens60013
exl-id: 6fb92e35-922c-47ba-8cf4-44edd92acfa1
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '716'
ht-degree: 27%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 27 de janeiro de 2021**

Atualizações dos recursos já existentes na Adobe Experience Platform:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Destinations]](#destinations)
- [[!DNL Real-Time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] O permite que os engenheiros de dados mapeiem, transformem e validem dados de e para o Experience Data Model (XDM).

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Funções de expressão regular | [!DNL Data Prep] O mapeador agora oferece suporte à correspondência e extração de parte do campo de entrada com base em expressões regulares. |

Para obter mais informações, consulte [[!DNL Data Prep] visão geral](../../data-prep/home.md).

## Destinos {#destinations}

[!DNL Destinations] são integrações pré-construídas com plataformas de destino que permitem a ativação perfeita de dados da Adobe Experience Platform. É possível usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas de email, publicidade direcionada e muitos outros casos de uso.

**Novos destinos**

| Destino | Descrição |
| ----------- | ----------- |
| [!DNL Azure Blob] | [!DNL Azure Blob] O é a solução de armazenamento de objetos da Microsoft para a nuvem. |

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Correspondência de ID avançada | Melhorias nos recursos de taxa de correspondência de público no [!DNL Facebook Custom Audiences] e [!DNL Google Customer Match], adicionando suporte para correspondência de identidade adicional, como IDs externas, números de telefone e IDs de dispositivos móveis. Consulte a documentação a seguir para obter mais detalhes: <ul><li>[Destino do facebook](../../destinations/catalog/social/facebook.md)</li><li>[Destino da Correspondência de clientes do Google](../../destinations/catalog/advertising/google-customer-match.md)</li><li>[Ativar dados do público-alvo para destinos de exportação de segmento de transmissão](../../destinations/ui/activate-segment-streaming-destinations.md)</li></ul> |

Para saber mais, visite o [visão geral dos destinos](../../destinations/home.md).

## Perfil do cliente em tempo real {#profile}

A Adobe Experience Platform permite gerar experiências coordenadas, consistentes e relevantes para seus clientes, independentemente de onde ou quando eles interagem com sua marca. Com o Perfil do cliente em tempo real, é possível ter uma visão integral de cada cliente ao combinar dados de vários canais, incluindo online, offline, CRM e de terceiros. [!DNL Profile] O permite consolidar os dados do cliente em uma visualização unificada, oferecendo uma conta acionável com carimbo de data e hora de cada interação com o cliente.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Excluir conjunto de dados do Armazenamento de perfil | Ao excluir um conjunto de dados do Data Lake do Experience Platform, ele também será automaticamente excluído do Armazenamento de perfis. Não é mais necessário usar o endpoint da API de trabalhos do Sistema de perfil para fazer uma solicitação de exclusão para excluir explicitamente o conjunto de dados do armazenamento de perfil. Para obter mais informações, consulte [guia de ponto de extremidade da API de trabalhos do sistema de perfil](../../profile/api/profile-system-jobs.md). |
| Contagem estimada de namespace de ID para um determinado segmento | Para contagens de perfis estimadas, a API de visualização agora relata:<ul><li>Contagem total de perfis estimados em um segmento para um determinado namespace.</li><li>Contagem total de perfis estimados no Esquema de união de perfil para um determinado namespace.</li></ul>Para saber mais, consulte o [guia de endpoint da API de visualização de perfil](../../profile/api/preview-sample-status.md). |

Para obter mais informações sobre o Perfil do cliente em tempo real, incluindo tutoriais e práticas recomendadas para trabalhar com a [!DNL Profile] dados, comece lendo o [Visão geral do Perfil do cliente em tempo real](../../profile/home.md).

## [!DNL Sources] {#sources}

O Adobe Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, estruturar, rotular e aprimorar esses dados usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

A Experience Platform fornece uma API RESTful e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar a sistemas de armazenamento externos e serviços de CRM, definir períodos para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Aprimoramentos no conector de origem do Adobe Audience Manager | Agora você pode filtrar e selecionar segmentos primários individuais do Audience Manager para assimilar na Platform, bem como filtrar características primárias. Veja o tutorial sobre [criação de um conector de origem de Audience Manager](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md) para obter mais informações. |
| [!DNL Google BigQuery] aprimoramentos do conector de origem | Agora é possível assimilar arquivos com mais de 10 GB em uma execução de fluxo usando o [!DNL BigQuery] conector de origem. Consulte a [[!DNL BigQuery] visão geral do conector de origem](../../sources/connectors/databases/bigquery.md) para obter mais informações. |
| Suporte a tipos de dados complexos para armazenamentos em nuvem | Agora é possível assimilar tipos de dados complexos, como matrizes em arquivos JSON, ao usar um conector de origem de armazenamento na nuvem. Consulte os tutoriais sobre como criar um fluxo de dados de armazenamento na nuvem [na interface](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) ou [usando o [!DNL Flow Service] API](../../sources/tutorials/api/collect/cloud-storage.md) para obter mais informações. |
| Suporte para autenticação baseada em chave da entidade de serviço para [!DNL Microsoft Dynamics] origem | Agora você pode autenticar em seu [!DNL Dynamics] conta usando uma chave da entidade de serviço como alternativa à autenticação baseada em senha. Consulte a [[!DNL Dynamics] visão geral do conector de origem](../../sources/connectors/crm/ms-dynamics.md) para obter mais informações. |
| Suporte à interface do usuário para separadores personalizados em fontes de armazenamento em nuvem | Agora é possível definir um delimitador de coluna personalizado, como uma vírgula (`,`), guia (`\t`), ou uma barra vertical (`|`), para coletar arquivos delimitados na interface do usuário do. Veja o tutorial sobre [criação de um fluxo de dados com um conector de origem de armazenamento na nuvem](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) para obter mais informações |

Para saber mais sobre fontes, consulte a [visão geral das origens](../../sources/home.md).
