---
title: 'Notas de versão do Adobe Experience Platform '
description: Notas de versão de Experience Platform 14 de outubro de 2020
doc-type: release notes
last-update: October 13, 2020
author: crhoades, ens25212
translation-type: tm+mt
source-git-commit: 578579438ca1d6a7a8c0a023efe2abd616a6dff2
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 6%

---


# Notas de versão da Adobe Experience Platform

**Data de lançamento: 14 de outubro de 2020**

- [Preparo de dados](#data-prep)
- [Perfil do cliente em tempo real](#profile)
- [Serviço de segmentação](#segmentation)
- [Fontes](#sources)

## Preparo de dados {#data-prep}

O Data Prep permite que os engenheiros de dados mapeiem, transformem e validem dados para e do Experience Data Model (XDM).

**Principais recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Função `is_set`  | A `is_set` função permite verificar a presença de um atributo nos dados de origem. `is_set` pode ser usado em combinação com `is_empty` para verificar a presença do atributo e a presença do valor dentro do atributo. |
| Função `get_values`  | A `get_values` função permite obter os valores do mapa de entrada para qualquer tecla. |

Para obter mais informações, leia a visão geral [da Preparação de](../../data-prep/home.md)dados.

## Perfil do cliente em tempo real {#profile}

A Adobe Experience Platform permite que você direcione experiências coordenadas, consistentes e relevantes para seus clientes, independentemente de onde ou quando eles interagem com sua marca. Com [!DNL Real-time Customer Profile]o, você pode ver uma visualização holística de cada cliente individual que combina dados de vários canais, incluindo dados online, offline, CRM e de terceiros. [!DNL Profile] permite consolidar seus dados de clientes diferentes em uma visualização unificada, oferecendo uma conta acionável e com carimbos de data e hora de cada interação com o cliente.

| Recurso | Descrição |
| ------- | ----------- |
| Adições à API de pré-visualização do perfil | A API de pré-visualização do Perfil (`/previewsamplestatus`) agora inclui a capacidade de visualização de um detalhamento do total de fragmentos do perfil na organização IMS, bem como de visualização da distribuição de fragmentos do perfil nas namespaces de identidade. |
| Atualizações da visualização do schema união | Na interface do usuário do Experience Platform, os usuários podem encontrar mais facilmente informações relacionadas a todos os schemas e conjuntos de dados que contribuem para o schema da união, bem como os principais atributos da superfície, como campos de identidade e relacionamento. Essas atualizações melhoram a capacidade de solucionar problemas e validar se os perfis estão configurados corretamente, se as identidades estão corretamente agrupadas e se os dados foram assimilados com êxito. |

Para obter mais informações sobre [!DNL Real-time Customer Profile], incluindo tutoriais e práticas recomendadas para trabalhar com [!DNL Profile] dados, leia a visão geral [do Perfil do cliente em tempo](../../profile/home.md)real.

## Serviço de segmentação {#segmentation}

O Adobe Experience Platform Segmentation Service fornece uma interface de usuário e uma RESTful API que permite criar segmentos e gerar audiências a partir de seus [!DNL Real-time Customer Profile] dados. Esses segmentos são configurados e mantidos centralmente [!DNL Platform], tornando-os facilmente acessíveis por qualquer aplicativo Adobe.

[!DNL Segmentation Service] define um subconjunto específico de perfis descrevendo os critérios que distinguem um grupo comercializável de pessoas dentro da sua base de clientes. Os segmentos podem se basear em dados de registro (como informações demográficas) ou em eventos de séries cronológicas que representem as interações do cliente com sua marca.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Remoção do limite de segmentação de fluxo | O limite de sete dias para o período de pesquisa foi removido. |

Para obter mais informações sobre [!DNL Segmentation Service], consulte a visão geral da [segmentação](../../segmentation/home.md)

## Fontes {#sources}

A Adobe Experience Platform pode assimilar dados de fontes externas, permitindo que você estruture, rotule e aprimore esses dados usando [!DNL Platform] serviços. Você pode assimilar dados de várias fontes, como aplicativos de Adobe, armazenamentos baseados em nuvem, software de terceiros e seu sistema de CRM.

[!DNL Experience Platform] fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem que você se autentique e se conecte a sistemas de armazenamentos externos e serviços CRM, defina horários para execuções de ingestão e gerencie a throughput de ingestão de dados.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Mapeamento hierárquico | Você pode pré-visualização um arquivo de origem hierárquico, como JSON ou Parquet, durante o processo de ingestão de dados. |
| Suporte de autenticação SSH para SFTP | Você pode conectar sua conta SFTP com [!DNL Platform] chaves SSH abertas RSA/DSA. See the [SFTP overview](../../sources/connectors/cloud-storage/ftp-sftp.md) for more information. |
| Melhorias no UX | Você pode ativar seu conjunto de dados para [!DNL Profile] durante o processo de ingestão de dados. Consulte o tutorial de fluxo de trabalho [de fluxo de dados do armazenamento](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) em nuvem para obter mais informações. |

Para saber mais sobre fontes, consulte a visão geral [das](../../sources/home.md)fontes.