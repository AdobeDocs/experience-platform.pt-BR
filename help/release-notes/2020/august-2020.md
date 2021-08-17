---
title: Notas de versão da Adobe Experience Platform
description: Notas de versão do Experience Platform 10 de agosto de 2020
doc-type: release notes
last-update: August 10, 2020
author: crhoades, ens28527
exl-id: 9347147f-e830-4487-aa12-f56723abb3c8
source-git-commit: a619227de30513bb06a22ce7b4f2fc13847c1ab6
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 7%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 12 de agosto de 2020**

Atualizações dos recursos existentes na Adobe Experience Platform:

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Destinations]](#destinations)
- [[!DNL Real-time Customer Data Platform]](#rtcdp)
- [[!DNL Sources]](#sources)

## [!DNL Data Science Workspace] {#dsw}

[!DNL Data Science Workspace] O usa aprendizagem de máquina e inteligência artificial para liberar insights de seus dados. Integrado ao Adobe Experience Platform, [!DNL Data Science Workspace] ajuda você a fazer previsões usando seus ativos de conteúdo e dados nas soluções do Adobe.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Melhorias na VM em [!DNL JupyterLab] | Melhora da estabilidade das máquinas virtuais [!DNL JupyterLab notebook] de longa duração. |

Para obter mais informações sobre [!DNL JupyterLab], consulte o [[!DNL JupyterLab] guia do usuário](../../data-science-workspace/jupyterlab/overview.md).

## Destinos {#destinations}

Em [Real-time Customer Data Platform](../../rtcdp/overview.md), os destinos são integrações pré-criadas com plataformas de destino que ativam os dados para esses parceiros de forma contínua.

**Novos destinos**

Novos destinos estão disponíveis, onde você pode ativar os dados do Adobe Experience Platform. Veja os detalhes abaixo:

| Destino | Descrição |
|--- | ---|
| [!DNL Google Customer Match] | A Correspondência de clientes do Google permite que você use seus dados online e offline para acessar e reengajar com seus clientes em propriedades próprias e operadas do Google, como: [!DNL Search], [!DNL Shopping], Gmail e YouTube. <br><br> Visite a  [!DNL Google Customer Match] [](../../destinations/catalog/advertising/google-customer-match.md) página no catálogo de destinos para obter mais informações sobre o destino e como configurá-lo na CDP em tempo real. |

**Novos recursos**

| Recurso | Descrição |
|------- | -----------|
| Editor de nome de arquivo personalizado | Atualize para o workflow de ativação de dados para destinos de marketing por email e destinos de armazenamento na nuvem que permitem editar o nome dos arquivos exportados. Para obter mais informações, consulte a [ etapa Configurar](../../destinations/ui/activate-batch-profile-destinations.md) no fluxo de trabalho de ativação. |
| Atributos recomendados | Atualize para o fluxo de trabalho de ativação de dados para destinos de marketing por email e destinos de armazenamento na nuvem que exibem atributos recomendados para você adicionar aos arquivos exportados. Para obter mais informações, consulte a [etapa Selecionar atributos](../../destinations/ui/activate-batch-profile-destinations.md) no fluxo de trabalho de ativação. |

## [!DNL Real-time Customer Data Platform] {#rtcdp}

Criada no Experience Platform, a Real-time Customer Data Platform ([!DNL Real-time CDP]) ajuda as empresas a unir dados conhecidos e desconhecidos para ativar perfis do cliente com decisões inteligentes em toda a jornada do cliente. [!DNL Real-time CDP] O combina várias fontes de dados corporativas para criar perfis de clientes em tempo real. Os segmentos criados a partir desses perfis podem ser enviados para destinos downstream para fornecer experiências personalizadas individuais do cliente em todos os canais e dispositivos.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Suporte ao IAB TCF 2.0 | [!DNL Real-time CDP] O agora é um fornecedor registrado para a versão 2.0 do  [!DNL Transparency & Consent Framework] (TCF), conforme descrito pelo  [!DNL Interactive Advertising Bureau] (IAB). Você pode configurar as operações de dados e os esquemas de perfil para aceitar os dados de consentimento do cliente gerados por uma CMP e aplicar as preferências de consentimento dos clientes ao ativar segmentos para destinos downstream. |

Para obter mais informações sobre [!DNL Real-time CDP], consulte a [[!DNL Real-time CDP] visão geral](../../rtcdp/overview.md).

## Fontes {#sources}

O Adobe Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, permite estruturar, rotular e aprimorar esses dados usando serviços [!DNL Platform]. Você pode assimilar dados de várias fontes, como aplicativos de Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

[!DNL Experience Platform] O fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e se conectar a sistemas de armazenamento externos e serviços CRM, definir horários para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Monitoramento da execução do fluxo | Os usuários podem monitorar todas as execuções de fluxo e ver uma exibição detalhada de cada execução, incluindo status de conclusão, duração da execução, lista de arquivos processados, erros e métricas. Consulte o documento [monitorando os fluxos de dados](../../sources/tutorials/ui/monitor.md) para obter mais informações. |
| Notificações de execução de fluxo | Os usuários podem assinar eventos e registrar webhooks para receber notificações em tempo real sobre o status, as métricas e os erros relacionados às execuções de fluxo. |
| Melhorias no catálogo da interface do usuário | Atualizações na tela de catálogo de origens para facilitar o acesso às ações primárias de objetos selecionados. |

Para saber mais sobre fontes, consulte a [visão geral das fontes](../../sources/home.md).
