---
title: 'Notas de versão do Adobe Experience Platform '
description: Notas de versão de Experience Platform 9 de setembro de 2020
doc-type: release notes
last-update: September 8, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: 23c7a0d82cb849568d6411c1a09c7a16b86d4954
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 5%

---


# Notas de versão da Adobe Experience Platform

**Data de lançamento: 9 de setembro de 2020**

Atualizações dos recursos existentes no Adobe Experience Platform:

* [[!DNL Data Governance]](#governance)
* [[!Destinos DNL]](#destinations)
* [[!DNL Privacy Service]](#privacy)
* [[!Fontes DNL]](#sources)

## [!DNL Data Governance] {#governance}

O Adobe Experience Platform Data Governance é uma série de estratégias e tecnologias usadas para gerenciar dados de clientes e garantir a conformidade com regulamentos, restrições e políticas aplicáveis ao uso de dados. Ele desempenha um papel fundamental em vários [!DNL Experience Platform] níveis, incluindo catalogação, linhagem de dados, rotulagem de uso de dados, políticas de acesso a dados e controle de acesso de dados para ações de marketing.

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Aprimoramentos da interface de identificação do conjunto de dados | Vários novos controles de classificação e filtragem foram adicionados à interface do usuário de etiquetagem do conjunto de dados para facilitar o trabalho com schemas grandes: <ul><li>Classifique os campos por ordem alfabética com base no caminho completo do schema.</li><li>Execute pesquisas parciais em nomes de caminho de campo.</li><li>Filtre campos sem rótulos, um rótulo selecionado ou uma categoria de rótulo.</li></ul> |

Consulte a visão geral [do](../../data-governance/home.md) Data Governance para obter mais informações sobre o serviço.

## Destinos {#destinations}

Na Plataforma [de dados do cliente em tempo real do](../../rtcdp/overview.md)Adobe, os destinos são integrações pré-criadas com plataformas de destino que ativam os dados para esses parceiros de forma contínua.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Melhorias no UX | Os usuários podem acessar ações de tabelas em linha para facilitar o acesso a ações primárias, como adicionar dados, editar agendamento e adicionar segmentos. Consulte o documento de espaço de trabalho [de](../../rtcdp/destinations/destinations-workspace.md) destinos para obter mais informações. |

Para saber mais, visite a visão geral de [destinos](../../rtcdp/destinations/destinations-overview.md)

## [!DNL Privacy Service] {#privacy}

Várias regulamentações legais e organizacionais conferem aos usuários o direito de acessar ou excluir seus dados pessoais dos armazenamentos de dados mediante solicitação. A Adobe Experience Platform [!DNL Privacy Service] fornece uma API RESTful e uma interface de usuário para ajudá-lo a gerenciar essas solicitações de dados de seus clientes. Com [!DNL Privacy Service]o, você pode enviar solicitações para acessar e excluir dados pessoais ou particulares de clientes de aplicativos Adobe Experience Cloud, facilitando a conformidade automatizada com as regulamentações legais e organizacionais de privacidade.

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Suporte para LGPD (Brasil) | Trabalhos de privacidade agora podem ser criados sob a regulamentação do Brasil [!DNL Lei Geral de Proteção de Dados] (LGPD). Estes postos de trabalho são rastreados ao abrigo do código regulamentar `lgpd_bra`. |

Consulte a visão geral [do](../../privacy-service/home.md) Privacy Service para obter mais informações sobre o serviço.

## Fontes {#sources}

A Adobe Experience Platform pode assimilar dados de fontes externas, permitindo que você estruture, rotule e aprimore esses dados usando [!DNL Platform] serviços. Você pode assimilar dados de várias fontes, como aplicativos de Adobe, armazenamentos baseados em nuvem, software de terceiros e seu sistema de CRM.

[!DNL Experience Platform] fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem que você se autentique e se conecte a sistemas de armazenamentos externos e serviços CRM, defina horários para execuções de ingestão e gerencie a throughput de ingestão de dados.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Mapeamento automático | [!DNL Platform] fornece recomendações inteligentes para o mapeamento automático durante o fluxo de trabalho de ingestão de dados, com base em um schema de público alvo ou conjunto de dados selecionado pelo usuário. Você pode ajustar manualmente as regras flexíveis de mapeamento automático para atender aos casos de uso. |
| Melhorias no UX | Os usuários podem acessar ações de tabelas em linha para facilitar o acesso a ações primárias, como adicionar dados, editar agendamento e adicionar segmentos. Consulte o documento de [monitoramento de fluxos de dados](../../sources/tutorials/ui/monitor.md) para obter mais informações. |

Para saber mais sobre fontes, consulte a visão geral [das](../../sources/home.md)fontes.
