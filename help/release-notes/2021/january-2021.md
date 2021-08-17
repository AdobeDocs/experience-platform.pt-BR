---
title: Notas de versão da Adobe Experience Platform
description: Notas de versão do Experience Platform 27 de janeiro de 2021
doc-type: release notes
last-update: January 27, 2021
author: ens60013
exl-id: 6fb92e35-922c-47ba-8cf4-44edd92acfa1
source-git-commit: 02c22453470d55236d4235c479742997e8407ef3
workflow-type: tm+mt
source-wordcount: '713'
ht-degree: 6%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 27 de janeiro de 2021**

Atualizações dos recursos existentes na Adobe Experience Platform:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Destinations]](#destinations)
- [[!DNL Real-time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] O permite que os engenheiros de dados mapeiem, transformem e validem dados de e para o Experience Data Model (XDM).

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Funções de expressão regular | [!DNL Data Prep] O Mapper agora oferece suporte à correspondência e extração de parte do campo de entrada com base em expressões regulares. |

Para obter mais informações, consulte a [[!DNL Data Prep] visão geral](../../data-prep/home.md).

## Destinos {#destinations}

[!DNL Destinations] são integrações pré-criadas com plataformas de destino que permitem a ativação contínua de dados do Adobe Experience Platform. Você pode usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas por email, anúncios direcionados e muitos outros casos de uso.

**Novos destinos**

| Destino | Descrição |
| ----------- | ----------- |
| [!DNL Azure Blob] | [!DNL Azure Blob] é a solução de armazenamento de objetos da Microsoft para a nuvem. |

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Correspondência de ID avançada | Aprimoramentos nos recursos de taxa de correspondência do público-alvo em [!DNL Facebook Custom Audiences] e [!DNL Google Customer Match], adicionando suporte para correspondência de identidade adicional, como IDs externas, números de telefone e IDs de dispositivo móvel. Consulte a seguinte documentação para obter mais detalhes: <ul><li>[Destino do facebook](../../destinations/catalog/social/facebook.md)</li><li>[Destino de correspondência do cliente do Google](../../destinations/catalog/advertising/google-customer-match.md)</li><li>[Ativar os dados do público-alvo para os destinos de exportação do segmento de fluxo](../../destinations/ui/activate-segment-streaming-destinations.md)</li></ul> |

Para saber mais, visite a [visão geral de destinos](../../destinations/home.md).

## Perfil do cliente em tempo real {#profile}

O Adobe Experience Platform permite que você conduza experiências coordenadas, consistentes e relevantes para seus clientes, independentemente de onde ou quando eles interagirem com sua marca. Com o Perfil do cliente em tempo real, você pode ver uma visualização holística de cada cliente individual que combina dados de vários canais, incluindo dados online, offline, CRM e de terceiros. [!DNL Profile] O permite consolidar os dados do cliente em uma visualização unificada, oferecendo uma conta acionável com carimbo de data e hora de cada interação com o cliente.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Excluir conjunto de dados do armazenamento de Perfis | Ao excluir um conjunto de dados do Experience Platform Data Lake, ele também será automaticamente excluído do armazenamento de perfis. Não é mais necessário usar o ponto de extremidade da API de tarefas do Sistema de perfil para fazer uma solicitação de exclusão para excluir o conjunto de dados do armazenamento de perfil explicitamente. Para obter mais informações, consulte o [guia do ponto de extremidade da API de tarefas do sistema de perfil](../../profile/api/profile-system-jobs.md). |
| Contagem estimada de namespace de ID para um determinado segmento | Para contagens de perfil estimadas, a API de visualização agora relata:<ul><li>Contagem total de perfis estimados em um segmento para um determinado namespace.</li><li>Contagem total de perfis estimados no Esquema de união de perfis para um determinado namespace.</li></ul>Para saber mais, consulte o [guia do endpoint da API de visualização de perfil](../../profile/api/preview-sample-status.md). |

Para obter mais informações sobre o Perfil do cliente em tempo real, incluindo tutoriais e práticas recomendadas para trabalhar com dados [!DNL Profile], comece lendo a [Visão geral do perfil do cliente em tempo real](../../profile/home.md).

## [!DNL Sources] {#sources}

A Adobe Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, permitir estruturar, rotular e aprimorar esses dados usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos de Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

O Experience Platform fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e se conectar a sistemas de armazenamento externos e serviços CRM, definir horários para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Aprimoramentos no conector de origem do Adobe Audience Manager | Agora é possível filtrar e selecionar segmentos primários individuais do Audience Manager para assimilar na plataforma, bem como filtrar características originais. Consulte o tutorial em [criar um conector de fonte Audience Manager](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md) para obter mais informações. |
| [!DNL Google BigQuery] melhorias no conector de origem | Agora é possível assimilar arquivos com mais de 10 GB em uma execução de fluxo usando o conector de origem [!DNL BigQuery]. Consulte a [[!DNL BigQuery] visão geral do conector de origem](../../sources/connectors/databases/bigquery.md) para obter mais informações. |
| Suporte para tipos de dados complexos para armazenamento em nuvem | Agora é possível assimilar tipos de dados complexos, como matrizes em arquivos JSON, ao usar um conector de origem de armazenamento em nuvem. Consulte os tutoriais sobre como criar um fluxo de dados de armazenamento em nuvem [na interface do usuário](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) ou [usando a [!DNL Flow Service] API](../../sources/tutorials/api/collect/cloud-storage.md) para obter mais informações. |
| Suporte para autenticação baseada em chave principal de serviço para [!DNL Microsoft Dynamics] origem | Agora você pode autenticar para sua conta [!DNL Dynamics] usando uma chave principal de serviço como alternativa à autenticação por senha. Consulte a [[!DNL Dynamics] visão geral do conector de origem](../../sources/connectors/crm/ms-dynamics.md) para obter mais informações. |
| Suporte à interface do usuário para separadores personalizados em fontes de armazenamento na nuvem | Agora é possível definir um delimitador de coluna personalizado, como uma vírgula (`,`), guia (`\t`) ou uma barra vertical (`|`), para coletar arquivos delimitados na interface do usuário. Consulte o tutorial em [criar um fluxo de dados com um conector de origem de armazenamento em nuvem](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) para obter mais informações |

Para saber mais sobre fontes, consulte a [visão geral das fontes](../../sources/home.md).
