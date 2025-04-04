---
title: Notas de versão da Adobe Experience Platform de setembro de 2020
description: As notas de versão de setembro de 2020 da Adobe Experience Platform.
doc-type: release notes
last-update: September 8, 2020
author: crhoades, ens25212
exl-id: bf401f3a-b088-4cbd-9a64-224294b797b9
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '866'
ht-degree: 23%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 9 de setembro de 2020**

Atualizações dos recursos já existentes na Adobe Experience Platform:

- [Governança de dados](#governance)
- [[!DNL Destinations]](#destinations)
- [[!DNL Observability Insights]](#observability)
- [[!DNL Privacy Service]](#privacy)
- [[!DNL Real-Time Customer Profile]](#profile)
- [[!DNL Segmentation Service]](#segmentation)
- [[!DNL Sources]](#sources)

## Governança de dados {#governance}

A Governança de dados da Adobe Experience Platform é uma série de estratégias e tecnologias usadas para gerenciar dados de clientes e garantir a conformidade com regulamentos, restrições e políticas aplicáveis ao uso de dados. Ele desempenha uma função importante no [!DNL Experience Platform] em vários níveis, incluindo catalogação, linhagem de dados, rotulagem de uso de dados, políticas de acesso a dados e controle de acesso a dados para ações de marketing.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Aprimoramentos na interface do usuário de rotulagem do conjunto de dados | Vários novos controles de classificação e filtragem foram adicionados à interface do usuário de rotulagem do conjunto de dados para facilitar o trabalho com esquemas grandes: <ul><li>Classifique os campos por ordem alfabética com base no caminho completo do esquema.</li><li>Realizar pesquisas parciais em nomes de caminho de campo.</li><li>Filtrar campos sem rótulos, um rótulo selecionado ou uma categoria de rótulo.</li></ul> |

Consulte a [Visão geral da Governança de dados](../../data-governance/home.md) para obter mais informações sobre o serviço.

## Destinos {#destinations}

No [Real-Time Customer Data Platform](../../rtcdp/overview.md), os destinos são integrações pré-criadas com plataformas de destino que ativam dados para esses parceiros de forma contínua.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Melhorias de UX | Os usuários podem acessar ações de tabela em linha para facilitar o acesso a ações principais, como adicionar dados, editar agendamento e adicionar segmentos. Consulte o documento [espaço de trabalho de destinos](../../destinations/ui/destinations-workspace.md) para obter mais informações. |

Para saber mais, visite a [visão geral de destinos](../../destinations/home.md)

## [!DNL Observability Insights] {#observability}

O [!DNL Observability Insights] permite monitorar atividades no Adobe Experience Platform usando métricas estatísticas e notificações de eventos.

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Notificações de eventos do Adobe I/O | O [!DNL Observability Insights] usa o Adobe I/O Events para criar notificações de eventos para vários serviços da Experience Platform. As cargas de notificação são enviadas para um webhook configurado, que você pode usar para automatizar mais processos downstream. |

Consulte a [[!DNL Observability Insights] visão geral](../../observability/home.md) para obter mais informações sobre o serviço.

## [!DNL Privacy Service] {#privacy}

Várias regulamentações legais e organizacionais dão aos usuários o direito de acessar ou excluir seus dados pessoais dos armazenamentos de dados, mediante solicitação. O Adobe Experience Platform [!DNL Privacy Service] fornece uma API RESTful e uma interface para ajudar você a gerenciar essas solicitações de dados de seus clientes. Com o [!DNL Privacy Service], você pode enviar solicitações para acessar e excluir dados privados ou pessoais dos clientes por meio dos aplicativos da Adobe Experience Cloud, facilitando a conformidade automatizada com as regulamentações legais e organizacionais de privacidade.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Suporte para LGPD (Brasil) | Os processos de privacidade agora podem ser criados de acordo com a [!DNL Lei Geral de Proteção de Dados] (LGPD) do Brasil. Esses processos são monitorados sob o código de regulamento `lgpd_bra`. |

Consulte a [visão geral do Privacy Service](../../privacy-service/home.md) para obter mais informações sobre o serviço.

## Perfil do cliente em tempo real {#profile}

A Adobe Experience Platform permite gerar experiências coordenadas, consistentes e relevantes para seus clientes, independentemente de onde ou quando eles interagem com sua marca. Com o [!DNL Real-Time Customer Profile], você pode ter uma visão holística de cada cliente individual que combina dados de vários canais, incluindo dados online, offline, de CRM e de terceiros. O [!DNL Profile] permite consolidar seus dados diferentes de clientes em uma visualização unificada, oferecendo uma conta acionável com carimbo de data e hora de cada interação com o cliente.

| Recurso | Descrição |
| ------- | ----------- |
| Visualizador de perfil | O visualizador de perfil, na interface do usuário do Experience Platform, foi atualizado para ser um painel com personalização completa. O usuário agora tem a opção de fazer as seguintes tarefas: <ul><li>Atualizar os atributos padrão e personalizados selecionados no widget de informações básicas.</li><li>Criar, editar e remover widgets personalizados</li><li>Redimensionar e reorganizar widgets</li></ul> |

Para obter mais informações sobre o [!DNL Real-Time Customer Profile], incluindo tutoriais e práticas recomendadas para trabalhar com dados do [!DNL Profile], leia a [Visão geral do Perfil do cliente em tempo real](../../profile/home.md).

## Serviço de segmentação {#segmentation}

O Serviço de Segmentação da Adobe Experience Platform fornece uma interface de usuário e uma API RESTful que permite criar segmentos e gerar públicos a partir dos dados do [!DNL Real-Time Customer Profile]. Esses segmentos são configurados e mantidos centralmente no [!DNL Experience Platform], tornando-os prontamente acessíveis por qualquer aplicativo do Adobe.

O [!DNL Segmentation Service] define um subconjunto específico de perfis descrevendo os critérios que distinguem um grupo de pessoas na sua base de clientes que pode ser direcionado por campanhas de marketing. Os segmentos podem ser baseados em dados de registro (como informações demográficas) ou em eventos de séries temporais que representam interações de clientes com sua marca.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Exportar trabalhos | Um sinalizador foi adicionado para permitir que segmentos sejam avaliados como parte de um trabalho de exportação. Como resultado, os usuários podem executar a segmentação e as exportações em um único trabalho. |
| Mesclar políticas | Várias políticas de mesclagem podem ser incluídas em um único trabalho de segmentação em lote. |

Para obter mais informações sobre [!DNL Segmentation Service], consulte a [Visão geral da segmentação](../../segmentation/home.md)

## Origens {#sources}

O Adobe Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, permitir que você estruture, rotule e aprimore esses dados usando os serviços do [!DNL Experience Platform]. Você pode assimilar dados de várias fontes, como aplicativos da Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

O [!DNL Experience Platform] fornece uma API RESTful e uma interface do usuário interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar a sistemas de armazenamento externos e serviços de CRM, definir períodos para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Mapeamento automático | O [!DNL Experience Platform] fornece recomendações inteligentes para mapeamento automático durante o fluxo de trabalho de assimilação de dados, com base em um esquema ou conjunto de dados de destino selecionado pelo usuário. Você pode ajustar manualmente regras de mapeamento automático flexíveis para atender aos seus casos de uso. |
| Melhorias de UX | Os usuários podem acessar ações de tabela em linha para facilitar o acesso às ações principais, como adicionar dados, editar agendamento e adicionar segmentos. Consulte o documento [monitoramento de fluxos de dados](../../sources/tutorials/ui/monitor.md) para obter mais informações. |

Para saber mais sobre fontes, consulte a [visão geral das fontes](../../sources/home.md).
