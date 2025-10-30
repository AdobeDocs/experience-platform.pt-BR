---
title: Notas de versão de agosto de 2020 da Adobe Experience Platform
description: As notas de versão de agosto de 2020 da Adobe Experience Platform.
doc-type: release notes
last-update: August 10, 2020
author: crhoades, ens28527
exl-id: 9347147f-e830-4487-aa12-f56723abb3c8
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 26%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: quinta-feira, 12 de agosto de 2020**

Atualizações dos recursos já existentes na Adobe Experience Platform:

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Destinations]](#destinations)
- [[!DNL Real-Time Customer Data Platform]](#rtcdp)
- [[!DNL Sources]](#sources)

## [!DNL Data Science Workspace] {#dsw}

O [!DNL Data Science Workspace] usa aprendizado de máquina e inteligência artificial para liberar insights de seus dados. Integrado ao Adobe Experience Platform, o [!DNL Data Science Workspace] ajuda você a fazer previsões usando seus ativos de conteúdo e dados nas soluções da Adobe.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Melhorias na VM em [!DNL JupyterLab] | Melhora na estabilidade das máquinas virtuais [!DNL JupyterLab notebook] de longa duração. |

Para obter mais informações sobre [!DNL JupyterLab], consulte o [[!DNL JupyterLab] guia do usuário](../../data-science-workspace/jupyterlab/overview.md).

## Destinos {#destinations}

No [Real-Time Customer Data Platform](../../rtcdp/overview.md), os destinos são integrações pré-criadas com plataformas de destino que ativam dados para esses parceiros de forma contínua.

**Novos destinos**

Novos destinos estão disponíveis onde você pode ativar os dados do Adobe Experience Platform. Veja os detalhes abaixo:

| Destino | Descrição |
|--- | ---|
| [!DNL Google Customer Match] | O Google Customer Match permite usar seus dados online e offline para acessar e reengajar com seus clientes nas propriedades próprias e operadas da Google, como: [!DNL Search], [!DNL Shopping], Gmail e YouTube. <br><br> Visite a [!DNL Google Customer Match] [página](../../destinations/catalog/advertising/google-customer-match.md) do catálogo de destinos para obter mais informações sobre o destino e como configurá-lo no Real-Time CDP. |

**Novos recursos**

| Recurso | Descrição |
|------- | -----------|
| Editor de nome de arquivo personalizado | Atualização do fluxo de trabalho de ativação de dados para destinos de marketing por email e destinos de armazenamento na nuvem que permite editar o nome dos arquivos exportados. Para obter mais informações, consulte a [etapa Configurar](../../destinations/ui/activate-batch-profile-destinations.md) do fluxo de trabalho de ativação. |
| Atributos recomendados | Atualização do fluxo de trabalho de ativação de dados para destinos de marketing por email e destinos de armazenamento na nuvem que exibe atributos recomendados para você adicionar aos arquivos exportados. Para obter mais informações, consulte a [etapa Selecionar atributos](../../destinations/ui/activate-batch-profile-destinations.md) no fluxo de trabalho de ativação. |

## [!DNL Real-Time Customer Data Platform] {#rtcdp}

Integrado à Experience Platform, a Real-time Customer Data Platform ([!DNL Real-Time CDP]) ajuda as empresas a unirem dados conhecidos e desconhecidos para ativar perfis de clientes com decisões inteligentes em toda a jornada do cliente. A [!DNL Real-Time CDP] combina várias fontes de dados corporativos para criar perfis de clientes em tempo real. Os segmentos criados a partir desses perfis podem ser enviados para destinos downstream com o fim de oferecer experiências de cliente personalizadas em todos os canais e dispositivos.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Suporte ao IAB TCF 2.0 | [!DNL Real-Time CDP] agora é um fornecedor registrado para a versão 2.0 do [!DNL Transparency & Consent Framework] (TCF), conforme descrito pelo [!DNL Interactive Advertising Bureau] (IAB). Você pode configurar suas operações de dados e esquemas de perfil para aceitar dados de consentimento do cliente gerados por um CMP e aplicar as preferências de consentimento dos clientes ao ativar segmentos para destinos downstream. |

Para obter mais informações sobre a [!DNL Real-Time CDP], consulte a [[!DNL Real-Time CDP] visão geral](../../rtcdp/overview.md).

## Origens {#sources}

O Adobe Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, permitir que você estruture, rotule e aprimore esses dados usando os serviços do [!DNL Experience Platform]. Você pode assimilar dados de várias fontes, como aplicativos da Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

O [!DNL Experience Platform] fornece uma API RESTful e uma interface do usuário interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar a sistemas de armazenamento externos e serviços de CRM, definir períodos para execuções de ingestão e gerenciar a taxa de transferência de ingestão de dados.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Monitoramento de execução de fluxo | Os usuários podem monitorar todas as execuções de fluxo e ver uma exibição detalhada de cada execução, incluindo status de conclusão, duração da execução, lista de arquivos processados, erros e métricas. Consulte o documento [monitoramento de fluxos de dados](../../sources/tutorials/ui/monitor.md) para obter mais informações. |
| Notificações de execução de fluxo | Os usuários podem assinar eventos e registrar webhooks para receber notificações em tempo real sobre status, métricas e erros relacionados a execuções de fluxo. |
| Melhorias no catálogo da interface do usuário | Atualizações na tela de catálogo de origens para permitir acesso mais fácil às ações principais de objetos selecionados. |

Para saber mais sobre fontes, consulte a [visão geral das fontes](../../sources/home.md).
