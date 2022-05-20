---
title: Notas de versão da Adobe Experience Platform de setembro de 2020
description: As notas de versão de setembro de 2020 para o Adobe Experience Platform.
doc-type: release notes
last-update: September 8, 2020
author: crhoades, ens25212
exl-id: bf401f3a-b088-4cbd-9a64-224294b797b9
source-git-commit: ce967ae176fce81aa26d92b3f0ee8be006808657
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 9 de setembro de 2020**

Atualizações dos recursos existentes na Adobe Experience Platform:

- [Governança de dados](#governance)
- [[!DNL Destinations]](#destinations)
- [[!DNL Observability Insights]](#observability)
- [[!DNL Privacy Service]](#privacy)
- [[!DNL Real-time Customer Profile]](#profile)
- [[!DNL Segmentation Service]](#segmentation)
- [[!DNL Sources]](#sources)

## Governança de dados {#governance}

A Governança de dados da Adobe Experience Platform é uma série de estratégias e tecnologias usadas para gerenciar dados de clientes e garantir a conformidade com regulamentos, restrições e políticas aplicáveis ao uso de dados. Ele desempenha um papel fundamental no [!DNL Experience Platform] em vários níveis, incluindo catalogação, linhagem de dados, rotulagem de uso de dados, políticas de acesso a dados e controle de acesso a dados para ações de marketing.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Aprimoramentos na interface do usuário de rotulagem do conjunto de dados | Vários novos controles de classificação e filtragem foram adicionados à interface do usuário de rotulagem do conjunto de dados para facilitar o trabalho com esquemas grandes: <ul><li>Classifique os campos por ordem alfabética com base no caminho completo do esquema.</li><li>Realize pesquisas parciais em nomes de caminho de campo.</li><li>Filtre campos sem rótulos, com um rótulo selecionado ou uma categoria de rótulo.</li></ul> |

Consulte a [Visão geral da governança de dados](../../data-governance/home.md) para obter mais informações sobre o serviço.

## Destinos {#destinations}

Em [Real-time Customer Data Platform](../../rtcdp/overview.md), os destinos são integrações pré-criadas com plataformas de destino que ativam os dados para esses parceiros de forma contínua.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Melhorias no UX | Os usuários podem acessar ações de tabelas em linha para facilitar o acesso às ações primárias, como adicionar dados, editar o agendamento e adicionar segmentos. Consulte a [espaço de trabalho destinos](../../destinations/ui/destinations-workspace.md) para obter mais informações. |

Para saber mais, visite o [visão geral dos destinos](../../destinations/home.md)

## [!DNL Observability Insights] {#observability}

[!DNL Observability Insights] O permite monitorar atividades no Adobe Experience Platform por meio do uso de métricas estatísticas e notificações de eventos.

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Notificações de evento Adobe I/O | [!DNL Observability Insights] usam Eventos Adobe I/O para criar notificações de eventos para vários serviços do Experience Platform. As cargas de notificação são enviadas para um webhook configurado, que pode ser usado para automatizar outros processos downstream. |

Consulte a [[!DNL Observability Insights] visão geral](../../observability/home.md) para obter mais informações sobre o serviço.

## [!DNL Privacy Service] {#privacy}

Várias regulamentações legais e organizacionais dão aos usuários o direito de acessar ou excluir seus dados pessoais dos armazenamentos de dados, mediante solicitação. Adobe Experience Platform [!DNL Privacy Service] O fornece uma RESTful API e interface do usuário para ajudar você a gerenciar essas solicitações de dados de seus clientes. Com [!DNL Privacy Service], você pode enviar solicitações para acessar e excluir dados pessoais de clientes de aplicativos Adobe Experience Cloud, facilitando a conformidade automatizada com as regulamentações legais e organizacionais de privacidade.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Suporte para LGPD (Brasil) | Trabalhos de privacidade agora podem ser criados no Brasil [!DNL Lei Geral de Proteção de Dados] (LGPD). Esses trabalhos são rastreados pelo código do regulamento `lgpd_bra`. |

Consulte a [Visão geral do Privacy Service](../../privacy-service/home.md) para obter mais informações sobre o serviço.

## Perfil do cliente em tempo real {#profile}

O Adobe Experience Platform permite que você conduza experiências coordenadas, consistentes e relevantes para seus clientes, independentemente de onde ou quando eles interagirem com sua marca. Com [!DNL Real-time Customer Profile], você pode ver uma visualização holística de cada cliente individual que combina dados de vários canais, incluindo dados online, offline, CRM e de terceiros. [!DNL Profile] O permite consolidar seus dados de clientes diferentes em uma visualização unificada que oferece uma conta acionável e com carimbos de data e hora de cada interação com o cliente.

| Recurso | Descrição |
| ------- | ----------- |
| Visualizador de perfil | O visualizador de perfil, na interface do usuário da plataforma, foi atualizado para ser um painel com personalização completa. O usuário agora tem a opção de realizar as seguintes tarefas: <ul><li>Atualize os atributos padrão e personalizados selecionados no widget de informações básicas.</li><li>Criar, editar e remover widgets personalizados</li><li>Redimensionar e reorganizar os widgets</li></ul> |

Para obter mais informações sobre [!DNL Real-time Customer Profile], incluindo tutoriais e práticas recomendadas para trabalhar com o [!DNL Profile] leia os [Visão geral do perfil do cliente em tempo real](../../profile/home.md).

## Serviço de segmentação {#segmentation}

O Serviço de segmentação da Adobe Experience Platform fornece uma interface de usuário e uma RESTful API que permite criar segmentos e gerar públicos a partir de sua [!DNL Real-time Customer Profile] dados. Esses segmentos são configurados e mantidos centralmente em [!DNL Platform], tornando-as facilmente acessíveis por qualquer aplicação de Adobe.

[!DNL Segmentation Service] O define um subconjunto específico de perfis ao descrever os critérios que distinguem um grupo comercializável de pessoas dentro da base do cliente. Os segmentos podem se basear em dados de registro (como informações demográficas) ou em eventos de séries cronológicas que representem as interações do cliente com sua marca.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Exportar trabalhos | Um sinalizador foi adicionado para permitir que os segmentos sejam avaliados como parte de um trabalho de exportação. Como resultado, os usuários podem executar a segmentação e as exportações em uma única tarefa. |
| Mesclar políticas | Várias políticas de mesclagem podem ser incluídas em um único trabalho de segmentação em lote. |

Para obter mais informações sobre [!DNL Segmentation Service]consulte o [Visão geral da segmentação](../../segmentation/home.md)

## Fontes {#sources}

O Adobe Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, permitir estruturar, rotular e aprimorar esses dados usando [!DNL Platform] serviços. Você pode assimilar dados de várias fontes, como aplicativos de Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

[!DNL Experience Platform] O fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e se conectar a sistemas de armazenamento externos e serviços CRM, definir horários para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Mapeamento automático | [!DNL Platform] O fornece recomendações inteligentes para mapeamento automático durante o fluxo de trabalho de assimilação de dados, com base em um esquema de destino ou conjunto de dados selecionado pelo usuário. Você pode ajustar manualmente as regras flexíveis de mapeamento automático para atender aos seus casos de uso. |
| Melhorias no UX | Os usuários podem acessar ações de tabelas em linha para facilitar o acesso às ações primárias, como adicionar dados, editar o agendamento e adicionar segmentos. Consulte a [monitoramento de fluxos de dados](../../sources/tutorials/ui/monitor.md) para obter mais informações. |

Para saber mais sobre fontes, consulte o [visão geral das fontes](../../sources/home.md).
