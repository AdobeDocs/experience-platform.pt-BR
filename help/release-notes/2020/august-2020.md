---
title: 'Notas de versão do Adobe Experience Platform '
description: Notas de versão de Experience Platform 10 de agosto de 2020
doc-type: release notes
last-update: August 10, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: 89531ad458bd41720090ef2c429376af4460d7c0
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 7%

---


# Notas de versão da Adobe Experience Platform

**Data de lançamento: 12 de agosto de 2020**

Atualizações dos recursos existentes no Adobe Experience Platform:

- [[!DNL Data Science Workspace]](#dsw)
- [[!Fontes DNL]](#sources)

## [!DNL Data Science Workspace] {#dsw}

[!DNL Data Science Workspace] usa o aprendizado de máquina e a inteligência artificial para liberar insights de seus dados. Integrado ao Adobe Experience Platform, [!DNL Data Science Workspace] ajuda você a fazer previsões usando seu conteúdo e seus ativos de dados nas soluções de Adobe.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Melhorias na VM em [!DNL JupyterLab] | Aprimorada a estabilidade de máquinas virtuais de longa duração. [!DNL JupyterLab notebook] |

Para obter mais informações sobre [!DNL JupyterLab], consulte o guia [[!DNL JupyterLab] do usuário](../../data-science-workspace/jupyterlab/overview.md).

## Fontes {#sources}

A Adobe Experience Platform pode assimilar dados de fontes externas, permitindo que você estruture, rotule e aprimore esses dados usando [!DNL Platform] serviços. Você pode assimilar dados de várias fontes, como aplicativos de Adobe, armazenamentos baseados em nuvem, software de terceiros e seu sistema de CRM.

[!DNL Experience Platform] fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem que você se autentique e se conecte a sistemas de armazenamentos externos e serviços CRM, defina horários para execuções de ingestão e gerencie a throughput de ingestão de dados.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Monitoramento de execução de fluxo | Os usuários podem monitorar todas as execuções de fluxo e ver uma visualização detalhada de cada execução, incluindo status de conclusão, duração da execução, lista de arquivos processados, erros e métricas. Consulte o documento de [monitoramento de fluxos de dados](../../sources/tutorials/ui/monitor.md) para obter mais informações. |
| Atualização da conta | Os usuários podem atualizar as credenciais, o nome e a descrição de qualquer conta existente para fornecer informações mais significativas e corrigir quaisquer erros que possam ter sido criados. |
| Notificações de execução de fluxo | Os usuários podem se inscrever em eventos e registrar webhooks para receber notificações em tempo real sobre o status, as métricas e os erros relacionados às execuções de fluxo. |
| Melhorias no catálogo da interface | Atualizações na tela de catálogo de fontes para facilitar o acesso às ações primárias de objetos selecionados. |

Para saber mais sobre fontes, consulte a visão geral [das](../../sources/home.md)fontes.
