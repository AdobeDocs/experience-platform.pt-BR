---
title: Notas de versão da Adobe Experience Platform
description: Notas de versão de Experience Platform 9 de setembro de 2020
doc-type: release notes
last-update: September 8, 2020
author: crhoades, ens25212
translation-type: tm+mt
source-git-commit: adf8e8457c8ffef263223a38d3f9c345cf7c6ab2
workflow-type: tm+mt
source-wordcount: '862'
ht-degree: 6%

---


# Notas de versão da Adobe Experience Platform

**Data de lançamento: 9 de setembro de 2020**

Atualizações dos recursos existentes na Adobe Experience Platform:

- [[!DNL Data Governance]](#governance)
- [[!DNL Destinations]](#destinations)
- [[!DNL Observability Insights]](#observability)
- [[!DNL Privacy Service]](#privacy)
- [[!DNL Real-time Customer Profile]](#profile)
- [[!DNL Segmentation Service]](#segmentation)
- [[!DNL Sources]](#sources)

## [!DNL Data Governance] {#governance}

O Adobe Experience Platform Data Governance é uma série de estratégias e tecnologias usadas para gerenciar dados de clientes e garantir a conformidade com regulamentos, restrições e políticas aplicáveis ao uso de dados. Ele desempenha um papel fundamental em vários [!DNL Experience Platform] níveis, incluindo catalogação, linhagem de dados, rotulagem de uso de dados, políticas de acesso a dados e controle de acesso de dados para ações de marketing.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Aprimoramentos da interface de identificação do conjunto de dados | Vários novos controles de classificação e filtragem foram adicionados à interface do usuário de etiquetagem do conjunto de dados para facilitar o trabalho com schemas grandes: <ul><li>Classifique os campos por ordem alfabética com base no caminho completo do schema.</li><li>Execute pesquisas parciais em nomes de caminho de campo.</li><li>Filtre campos sem rótulos, um rótulo selecionado ou uma categoria de rótulo.</li></ul> |

Consulte a visão geral [do](../../data-governance/home.md) Data Governance para obter mais informações sobre o serviço.

## Destinos {#destinations}

Na Plataforma [de dados do cliente em tempo](../../rtcdp/overview.md)real, os destinos são integrações pré-criadas com plataformas de destino que ativam os dados para esses parceiros de forma contínua.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Melhorias no UX | Os usuários podem acessar ações de tabelas em linha para facilitar o acesso a ações primárias, como adicionar dados, editar agendamento e adicionar segmentos. Consulte o documento de espaço de trabalho [de](../../destinations/ui/destinations-workspace.md) destinos para obter mais informações. |

Para saber mais, visite a visão geral de [destinos](../../destinations/home.md)

## [!DNL Observability Insights] {#observability}

[!DNL Observability Insights] permite que você monitore atividades no Adobe Experience Platform através do uso de métricas estatísticas e notificações de eventos.

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Notificações do Evento Adobe I/O | [!DNL Observability Insights] aproveita Eventos Adobe I/O para criar notificações de eventos para vários serviços de Experience Platform. As cargas de notificação são enviadas para um webhook configurado, que você pode usar para automatizar outros processos de downstream. See the [notifications overview](../../observability/notifications/overview.md) for more information. |

Consulte a [[!DNL Observability Insights] visão geral](../../observability/home.md) para obter mais informações sobre o serviço.

## [!DNL Privacy Service] {#privacy}

Várias regulamentações legais e organizacionais conferem aos usuários o direito de acessar ou excluir seus dados pessoais dos armazenamentos de dados mediante solicitação. A Adobe Experience Platform [!DNL Privacy Service] fornece uma API RESTful e uma interface de usuário para ajudá-lo a gerenciar essas solicitações de dados de seus clientes. Com [!DNL Privacy Service]o, você pode enviar solicitações para acessar e excluir dados pessoais ou particulares de clientes de aplicativos Adobe Experience Cloud, facilitando a conformidade automatizada com as regulamentações legais e organizacionais de privacidade.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Suporte para LGPD (Brasil) | Trabalhos de privacidade agora podem ser criados sob a regulamentação do Brasil [!DNL Lei Geral de Proteção de Dados] (LGPD). Estes postos de trabalho são rastreados ao abrigo do código regulamentar `lgpd_bra`. |

Consulte a visão geral [do](../../privacy-service/home.md) Privacy Service para obter mais informações sobre o serviço.

## Perfil do cliente em tempo real {#profile}

A Adobe Experience Platform permite que você direcione experiências coordenadas, consistentes e relevantes para seus clientes, independentemente de onde ou quando eles interagem com sua marca. Com [!DNL Real-time Customer Profile]o, você pode ver uma visualização holística de cada cliente individual que combina dados de vários canais, incluindo dados online, offline, CRM e de terceiros. [!DNL Profile] permite consolidar seus dados de clientes diferentes em uma visualização unificada, oferecendo uma conta acionável e com carimbos de data e hora de cada interação com o cliente.

| Recurso | Descrição |
| ------- | ----------- |
| Visualizador de perfis | O visualizador de perfis, na interface do usuário da plataforma, foi atualizado para ser um painel com personalização total. O usuário agora tem a opção de fazer as seguintes tarefas: <ul><li>Atualize os atributos padrão e personalizados selecionados no widget de informações básicas.</li><li>Criar, editar e remover widgets personalizados</li><li>Redimensionar e reorganizar widgets</li></ul> |

Para obter mais informações sobre [!DNL Real-time Customer Profile], incluindo tutoriais e práticas recomendadas para trabalhar com [!DNL Profile] dados, leia a visão geral [do Perfil do cliente em tempo](../../profile/home.md)real.

## Serviço de segmentação {#segmentation}

O Adobe Experience Platform Segmentation Service fornece uma interface de usuário e uma RESTful API que permite criar segmentos e gerar audiências a partir de seus [!DNL Real-time Customer Profile] dados. Esses segmentos são configurados e mantidos centralmente [!DNL Platform], tornando-os facilmente acessíveis por qualquer aplicativo Adobe.

[!DNL Segmentation Service] define um subconjunto específico de perfis descrevendo os critérios que distinguem um grupo comercializável de pessoas dentro da sua base de clientes. Os segmentos podem se basear em dados de registro (como informações demográficas) ou em eventos de séries cronológicas que representem as interações do cliente com sua marca.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Exportar trabalhos | Um sinalizador foi adicionado para permitir que os segmentos sejam avaliados como parte de um trabalho de exportação. Como resultado, os usuários podem executar a segmentação e as exportações em uma única tarefa. |
| Mesclar políticas | Várias políticas de mesclagem podem ser incluídas em um único trabalho de segmentação em lote. |

Para obter mais informações sobre [!DNL Segmentation Service], consulte a visão geral da [Segmentação](../../segmentation/home.md)

## Fontes {#sources}

A Adobe Experience Platform pode assimilar dados de fontes externas, permitindo que você estruture, rotule e aprimore esses dados usando [!DNL Platform] serviços. Você pode assimilar dados de várias fontes, como aplicativos de Adobe, armazenamentos baseados em nuvem, software de terceiros e seu sistema de CRM.

[!DNL Experience Platform] fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem que você se autentique e se conecte a sistemas de armazenamentos externos e serviços CRM, defina horários para execuções de ingestão e gerencie a throughput de ingestão de dados.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Mapeamento automático | [!DNL Platform] fornece recomendações inteligentes para o mapeamento automático durante o fluxo de trabalho de ingestão de dados, com base em um schema de público alvo ou conjunto de dados selecionado pelo usuário. Você pode ajustar manualmente as regras flexíveis de mapeamento automático para atender aos casos de uso. |
| Melhorias no UX | Os usuários podem acessar ações de tabelas em linha para facilitar o acesso a ações primárias, como adicionar dados, editar agendamento e adicionar segmentos. Consulte o documento de [monitoramento de fluxos de dados](../../sources/tutorials/ui/monitor.md) para obter mais informações. |

Para saber mais sobre fontes, consulte a visão geral [das](../../sources/home.md)fontes.
