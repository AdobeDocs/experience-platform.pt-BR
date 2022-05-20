---
title: Notas de versão da Adobe Experience Platform de agosto de 2020
description: As notas de versão de agosto de 2020 para o Adobe Experience Platform.
doc-type: release notes
last-update: August 10, 2020
author: crhoades, ens28527
exl-id: 9347147f-e830-4487-aa12-f56723abb3c8
source-git-commit: ce967ae176fce81aa26d92b3f0ee8be006808657
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 12 de agosto de 2020**

Atualizações dos recursos existentes na Adobe Experience Platform:

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Destinations]](#destinations)
- [[!DNL Real-time Customer Data Platform]](#rtcdp)
- [[!DNL Sources]](#sources)

## [!DNL Data Science Workspace] {#dsw}

[!DNL Data Science Workspace] O usa aprendizagem de máquina e inteligência artificial para liberar insights de seus dados. Integrado ao Adobe Experience Platform, [!DNL Data Science Workspace] O ajuda você a fazer previsões usando seu conteúdo e ativos de dados nas soluções do Adobe.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Melhorias na VM em [!DNL JupyterLab] | Melhorou a estabilidade de longo prazo [!DNL JupyterLab notebook] máquinas virtuais. |

Para obter mais informações sobre [!DNL JupyterLab]consulte o [[!DNL JupyterLab] guia do usuário](../../data-science-workspace/jupyterlab/overview.md).

## Destinos {#destinations}

Em [Real-time Customer Data Platform](../../rtcdp/overview.md), os destinos são integrações pré-criadas com plataformas de destino que ativam os dados para esses parceiros de forma contínua.

**Novos destinos**

Novos destinos estão disponíveis, onde você pode ativar os dados do Adobe Experience Platform. Veja os detalhes abaixo:

| Destino | Descrição |
|--- | ---|
| [!DNL Google Customer Match] | A Correspondência de clientes do Google permite que você use seus dados online e offline para acessar e reengajar seus clientes em propriedades próprias e operadas da Google, como: [!DNL Search], [!DNL Shopping], Gmail e YouTube. <br><br> Visite o [!DNL Google Customer Match] [página](../../destinations/catalog/advertising/google-customer-match.md) no catálogo de destinos para obter mais informações sobre o destino e como configurá-lo na CDP em tempo real. |

**Novos recursos**

| Recurso | Descrição |
|------- | -----------|
| Editor de nome de arquivo personalizado | Atualize para o workflow de ativação de dados para destinos de marketing por email e destinos de armazenamento na nuvem que permitem editar o nome dos arquivos exportados. Para obter mais informações, consulte [ Etapa de configuração](../../destinations/ui/activate-batch-profile-destinations.md) no fluxo de trabalho de ativação. |
| Atributos recomendados | Atualize para o fluxo de trabalho de ativação de dados para destinos de marketing por email e destinos de armazenamento na nuvem que exibem atributos recomendados para você adicionar aos arquivos exportados. Para obter mais informações, consulte [Etapa Selecionar atributos](../../destinations/ui/activate-batch-profile-destinations.md) no fluxo de trabalho de ativação. |

## [!DNL Real-time Customer Data Platform] {#rtcdp}

Criado no Experience Platform, Real-time Customer Data Platform ([!DNL Real-time CDP]) ajuda as empresas a unirem dados conhecidos e desconhecidos para ativar perfis do cliente com decisões inteligentes na jornada do cliente. [!DNL Real-time CDP] O combina várias fontes de dados corporativas para criar perfis de clientes em tempo real. Os segmentos criados a partir desses perfis podem ser enviados para destinos downstream para fornecer experiências personalizadas individuais do cliente em todos os canais e dispositivos.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Suporte ao IAB TCF 2.0 | [!DNL Real-time CDP] agora é um fornecedor registrado para a versão 2.0 do [!DNL Transparency & Consent Framework] (TCF), conforme descrito pela [!DNL Interactive Advertising Bureau] (IAB). Você pode configurar as operações de dados e os esquemas de perfil para aceitar os dados de consentimento do cliente gerados por uma CMP e aplicar as preferências de consentimento dos clientes ao ativar segmentos para destinos downstream. |

Para obter mais informações sobre [!DNL Real-time CDP], consulte o [[!DNL Real-time CDP] visão geral](../../rtcdp/overview.md).

## Fontes {#sources}

O Adobe Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, permitir estruturar, rotular e aprimorar esses dados usando [!DNL Platform] serviços. Você pode assimilar dados de várias fontes, como aplicativos de Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

[!DNL Experience Platform] O fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e se conectar a sistemas de armazenamento externos e serviços CRM, definir horários para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Monitoramento da execução do fluxo | Os usuários podem monitorar todas as execuções de fluxo e ver uma exibição detalhada de cada execução, incluindo status de conclusão, duração da execução, lista de arquivos processados, erros e métricas. Consulte a [monitoramento de fluxos de dados](../../sources/tutorials/ui/monitor.md) para obter mais informações. |
| Notificações de execução de fluxo | Os usuários podem assinar eventos e registrar webhooks para receber notificações em tempo real sobre o status, as métricas e os erros relacionados às execuções de fluxo. |
| Melhorias no catálogo da interface do usuário | Atualizações na tela de catálogo de origens para facilitar o acesso às ações primárias de objetos selecionados. |

Para saber mais sobre fontes, consulte o [visão geral das fontes](../../sources/home.md).
