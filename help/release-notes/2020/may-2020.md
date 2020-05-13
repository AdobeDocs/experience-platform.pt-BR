---
title: 'Notas de versão do Adobe Experience Platform '
description: Notas de versão da plataforma Experience 13 de maio de 2020
doc-type: release notes
last-update: May 13, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: 9d4c645e830790a7d5430fe3d514464ca8bef025
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 4%

---


# Notas de versão da Adobe Experience Platform

**Data de lançamento: 13 de maio de 2020**

Atualizações dos recursos existentes na Adobe Experience Platform:

- [Área de trabalho da ciência de dados](#dsw)
- [Experience Platform Web SDK e Experience Platform Edge Network](#edge)
- [Fontes](#sources)

## Área de trabalho da ciência de dados {#dsw}

A Data Science Workspace usa o aprendizado de máquina e a inteligência artificial para liberar insights de seus dados. Integrado à Adobe Experience Platform, a Data Science Workspace ajuda você a fazer previsões usando seus ativos de conteúdo e dados nas soluções da Adobe. Uma das maneiras de fazer isso é usando o JupyterLab. O JupyterLab é uma interface de usuário baseada na Web para o <a href="https://jupyter.org/" target="_blank">Project Júpitter</a> e é totalmente integrado à Adobe Experience Platform. Ele fornece um ambiente de desenvolvimento interativo para que os cientistas de dados trabalhem com notebooks, códigos e dados de Júpiter.

**Novos recursos**

| Recurso | Descrição |
|--- | ---|
| JupyterLab Launcher | O JupyterLab Launcher agora inclui iniciadores para notebooks Spark 2.4. Os iniciadores de notebook do Spark 2.3 agora estão marcados como obsoletos e definidos para serem removidos em uma versão subsequente. |
| Spark 2.4 | As novas receitas Scala (Spark) e PySpark agora usam o Spark 2.4. |
| Kernels | Os notebooks Scala (Spark) agora são criados pelo kernel Scala. Os notebooks PySpark agora são criados pelo kernel Python. O kernel do Spark e do PySpark está obsoleto e definido para ser removido em uma versão subsequente. |
| Receitas | As novas receitas do PySpark e do Spark agora seguem o fluxo de trabalho do Docker, semelhante às receitas do Python e R. |

Para obter mais informações sobre como migrar seus notebooks e fórmulas para usar o Spark 2.4, consulte o guia [de migração do](../../data-science-workspace/recipe-notebook-migration.md)notebook. Para obter informações mais gerais sobre a Data Science Workspace, consulte a documentação [de](../../data-science-workspace/home.md)visão geral.

## Experience Platform Web SDK e Experience Platform Edge Network {#edge}

O Experience Platform Web SDK e a Experience Platform Edge Network permitem que os usuários enviem dados para a Adobe Experience Platform e outras soluções da Adobe em tempo real para dispositivos de usuário final e navegadores. A lista mais recente de casos de uso pode ser encontrada no nosso roteiro [](https://github.com/adobe/alloy/projects/5) público, que é atualizado com frequência.

**Novos recursos**

| Recurso | Descrição |
|--- | ---|
| Suporte para ECID | O SDK oferece suporte ao ECID pronto para uso sem quaisquer bibliotecas ou informações adicionais para instalação |
| Interface de usuário de configuração | Gerencie suas configurações de ID com a nova interface de usuário de configuração de borda no Launch, deve estar na lista de permissões para acessar |
| Mistura SDK da Web da plataforma Adobe Experience | Um mixin para uso com o SDK da Web da Experience Platform que abrange todos os campos suportados. |
| Controles de consentimento do curso | Dá ao empresa controles sobre aceitação e não participação do SDK da Web da Experience Platform |
| Suporte à depuração do cliente na nova extensão do Experience Cloud Debugger | Consulte solicitações do SDK da Web da Experience Platform, bem como os rastreamentos de borda para ver como os dados fluem pelo sistema. |
| Adobe Analytics | Envie dados para os conjuntos de relatórios do Analytics por meio da configuração da borda. O XDM é nivelado em dados de contexto, suporta marcação de vários conjuntos |
| Adobe Target | Suporte para o Público alvo da Adobe. Incluindo VEC, Compositor baseado em formulário, A/B, XT, Personalização automatizada, MVT |
| Suporte ao Adobe Audiência Manager | Suporte para sincronizações de ID do Audiência Manager, destinos de URL e destinos de cookies |
| `synceIdnetity` | Renomeado `setCustomersIds` para `syncIdentity` tornar mais claro |
| Construtor de objetos XDM | Na extensão de inicialização, agora é possível criar objetos XDM como Elementos de dados |

Para obter mais informações sobre o SDK da Web da plataforma e o Edge Network, consulte a [documentação](../../edge/home.md).

## Fontes {#sources}

A plataforma Adobe Experience pode assimilar dados de fontes externas, permitindo que você estruture, rotule e aprimore esses dados usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos da Adobe, armazenamentos baseados em nuvem, software de terceiros e seu sistema de CRM.

A plataforma Experience fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem que você se autentique e se conecte a sistemas de armazenamentos externos e serviços CRM, defina horários para execuções de ingestão e gerencie a throughput de ingestão de dados.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Suporte adicional à API e à interface do usuário para sistemas de armazenamento em nuvem | Novos conectores de origem para o Armazenamento de Arquivo do Azure. |
| Suporte adicional à API e à interface do usuário para bancos de dados | Novos conectores de origem para o Azure Data Explorer, IBM DB2 e Oracle DB. |

**Problemas conhecidos**

- Nenhum

Para saber mais sobre fontes, consulte a visão geral [das](../../sources/home.md)fontes.