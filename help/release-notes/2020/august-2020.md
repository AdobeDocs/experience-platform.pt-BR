---
title: 'Notas de versão do Adobe Experience Platform '
description: Notas de versão de Experience Platform 10 de agosto de 2020
doc-type: release notes
last-update: August 10, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: b4ce4c2e5ff5083f663c2daf23c32a1cec32124c
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 5%

---


# Notas de versão da Adobe Experience Platform

**Data de lançamento: 12 de agosto de 2020**

Atualizações dos recursos existentes no Adobe Experience Platform:

- [[!DNL Data Science Workspace]](#dsw)
- [[!Destinos DNL]](#destinations)
- [[!DNL Real-time Customer Data Platform]](#rtcdp)
- [[!Fontes DNL]](#sources)

## [!DNL Data Science Workspace] {#dsw}

[!DNL Data Science Workspace] usa o aprendizado de máquina e a inteligência artificial para liberar insights de seus dados. Integrado ao Adobe Experience Platform, [!DNL Data Science Workspace] ajuda você a fazer previsões usando seu conteúdo e seus ativos de dados nas soluções de Adobe.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Melhorias na VM em [!DNL JupyterLab] | Aprimorada a estabilidade de máquinas virtuais de longa duração. [!DNL JupyterLab notebook] |

Para obter mais informações sobre [!DNL JupyterLab], consulte o guia [[!DNL JupyterLab] do usuário](../../data-science-workspace/jupyterlab/overview.md).

## Destinos {#destinations}

Na Plataforma [de dados do cliente em tempo real do](../../rtcdp/overview.md)Adobe, os destinos são integrações pré-criadas com plataformas de destino que ativam os dados para esses parceiros de forma contínua.

**Novos destinos**

Novos destinos estão disponíveis onde você pode ativar seus dados do Adobe Experience Platform. Consulte abaixo para obter detalhes:

| Destino | Descrição |
|--- | ---|
| [!DNL Google Customer Match] | A Correspondência de clientes do Google permite que você use seus dados online e offline para alcançar e reinteragir com seus clientes em todas as propriedades operadas e pertencentes ao Google, como: [!DNL Search], [!DNL Shopping], Gmail e YouTube. <br><br> Visite a [!DNL Google Customer Match] página [](/help/rtcdp/destinations/google-customer-match-destination.md) no catálogo de destinos para obter mais informações sobre o destino e como configurá-lo no Adobe Real-time CDP. |

**Novos recursos**

| Recurso | Descrição |
|------- | -----------|
| Editor personalizado de nomes de arquivos | Atualize para o fluxo de trabalho da ativação de dados para destinos de marketing por email e destinos de armazenamento na nuvem que permitem editar o nome dos arquivos exportados. Para obter mais informações, consulte a etapa [](/help/rtcdp/destinations/activate-destinations.md#configure) Configurar no fluxo de trabalho da ativação. |
| Atributos recomendados | Atualize para o fluxo de trabalho da ativação de dados para destinos de marketing por email e destinos de armazenamento na nuvem que exibem os atributos recomendados para que você adicione aos arquivos exportados. Para obter mais informações, consulte a etapa [](/help/rtcdp/destinations/activate-destinations.md#select-attributes) Selecionar atributos no fluxo de trabalho da ativação. |

## [!DNL Real-time Customer Data Platform] {#rtcdp}

Construída no Experience Platform, a Adobe Real-time Customer Data Platform ([!DNL Real-time CDP]) ajuda as empresas a unir dados conhecidos e desconhecidos para ativar perfis de clientes com decisões inteligentes durante toda a jornada do cliente. [!DNL Real-time CDP] combina várias fontes de dados corporativas para criar perfis de clientes em tempo real. Segmentos criados a partir desses perfis podem ser enviados para destinos downstream para fornecer experiências personalizadas individuais do cliente em todos os canais e dispositivos.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Suporte a IAB TCF 2.0 | [!DNL Real-time CDP] agora é um fornecedor registrado para a versão 2.0 do [!DNL Transparency & Consent Framework] (TCF), conforme descrito pelo [!DNL Interactive Advertising Bureau] (IAB). Você pode configurar suas operações de dados e schemas de perfis para aceitar dados de consentimento do cliente gerados por um CMP e impor as preferências de consentimento do cliente ao ativar segmentos para destinos de downstream. Consulte a visão geral sobre o suporte ao [IAB TCF 2.0 na CDP](../../rtcdp/privacy/iab/overview.md) em tempo real para obter mais informações. |

Para obter mais informações sobre [!DNL Real-time CDP], consulte a [[!DNL Real-time CDP] visão geral](../../rtcdp/overview.md).

## Fontes {#sources}

A Adobe Experience Platform pode assimilar dados de fontes externas, permitindo que você estruture, rotule e aprimore esses dados usando [!DNL Platform] serviços. Você pode assimilar dados de várias fontes, como aplicativos de Adobe, armazenamentos baseados em nuvem, software de terceiros e seu sistema de CRM.

[!DNL Experience Platform] fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem que você se autentique e se conecte a sistemas de armazenamentos externos e serviços CRM, defina horários para execuções de ingestão e gerencie a throughput de ingestão de dados.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Monitoramento de execução de fluxo | Os usuários podem monitorar todas as execuções de fluxo e ver uma visualização detalhada de cada execução, incluindo status de conclusão, duração da execução, lista de arquivos processados, erros e métricas. Consulte o documento de [monitoramento de fluxos de dados](../../sources/tutorials/ui/monitor.md) para obter mais informações. |
| Notificações de execução de fluxo | Os usuários podem se inscrever em eventos e registrar webhooks para receber notificações em tempo real sobre o status, as métricas e os erros relacionados às execuções de fluxo. |
| Melhorias no catálogo da interface | Atualizações na tela de catálogo de fontes para facilitar o acesso às ações primárias de objetos selecionados. |

Para saber mais sobre fontes, consulte a visão geral [das](../../sources/home.md)fontes.