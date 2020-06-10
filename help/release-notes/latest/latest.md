---
title: 'Notas de versão do Adobe Experience Platform '
description: As notas de versão mais recentes da Experience Platform
doc-type: release notes
last-update: June 10, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: 1dad479708291e911719c3f3dd5edd2e9b497973
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 5%

---


# Notas de versão da Adobe Experience Platform

**Data de lançamento: 10 de junho de 2020**

Atualizações dos recursos existentes na Adobe Experience Platform:

- [Área de trabalho da ciência de dados](#dsw)
- [Segmentação](#segmentation)
- [Fontes](#sources)

## Área de trabalho da ciência de dados {#dsw}

A Data Science Workspace usa o aprendizado de máquina e a inteligência artificial para liberar insights de seus dados. Integrado à Adobe Experience Platform, a Data Science Workspace ajuda você a fazer previsões usando seus ativos de conteúdo e dados nas soluções da Adobe.

A Data Science Workspace tem trabalhado em novas maneiras para permitir melhores experiências e previsões através do uso de aprendizado de máquina em tempo real. O Aprendizado de máquina em tempo real oferece a capacidade de criar, testar e implantar modelos personalizados ou importados de aprendizado de máquina pré-treinados em formatos de modelo interoperáveis padrão do setor para pontuação/ativação em tempo real por meio de um terminal de API.

Observe que o aprendizado de máquina em tempo real está em alfa e ainda está sendo desenvolvido.

| Recurso | Descrição |
|--- | ---|
| Iniciador de ML em tempo real do JupyterLab | O JupyterLab Launcher agora inclui um notebook Python para aprendizado de máquina em tempo real (Alpha). |

Para obter mais informações sobre o aprendizado de máquina em tempo real alfa, consulte a visão geral [de aprendizado de máquina em tempo](../../data-science-workspace/real-time-machine-learning/home.md)real.

## Segmentação {#segmentation}

O Adobe Experience Platform Segmentation Service fornece uma interface de usuário e uma RESTful API que permite criar segmentos e gerar audiências a partir dos dados do Perfil do cliente em tempo real. Esses segmentos são configurados e mantidos centralmente na Plataforma, tornando-os facilmente acessíveis por qualquer aplicativo da Adobe.

O Serviço de segmentação define um subconjunto específico de perfis ao descrever os critérios que distinguem um grupo comercializável de pessoas dentro da sua base de clientes. Os segmentos podem se basear em dados de registro (como informações demográficas) ou em eventos de séries cronológicas que representem as interações do cliente com sua marca.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Campos de data | Um recurso de &quot;aniversário&quot; para funções de data foi adicionado, permitindo que os usuários avaliem datas sem o ano. |

Para obter mais informações sobre a segmentação, consulte a visão geral da [segmentação](../../segmentation/home.md)

## Fontes {#sources}

A plataforma Adobe Experience pode assimilar dados de fontes externas, permitindo que você estruture, rotule e aprimore esses dados usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos da Adobe, armazenamentos baseados em nuvem, software de terceiros e seu sistema de CRM.

A plataforma Experience fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem que você se autentique e se conecte a sistemas de armazenamentos externos e serviços CRM, defina horários para execuções de ingestão e gerencie a throughput de ingestão de dados.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Suporte adicional à API e à interface do usuário para sistemas de armazenamento em nuvem | Novo conector de origem para o Apache HDFS |
| Suporte adicional à API e à interface do usuário para bancos de dados | Novo conector de origem para Couchbase. |

Para saber mais sobre fontes, consulte a visão geral [das](../../sources/home.md)fontes.
