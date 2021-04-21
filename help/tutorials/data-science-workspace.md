---
keywords: Experience Platform, home, tópicos populares, dsw, DSW
solution: Experience Platform
title: Tutoriais do Data Science Workspace
topic-legacy: tutorial
type: Tutorial
description: O Adobe Experience Platform Data Science Workspace usa aprendizagem de máquina e inteligência artificial para criar insights de seus dados. Integrado ao Adobe Experience Platform, o Data Science Workspace ajuda você a fazer previsões usando seus ativos de conteúdo e dados nas soluções de Adobe.
exl-id: 7cfd71b1-584f-4588-bbcd-bc42a08a0bc0
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1302'
ht-degree: 0%

---

# [!DNL Data Science Workspace] tutoriais

O Adobe Experience Platform [!DNL Data Science Workspace] usa aprendizagem de máquina e inteligência artificial para criar insights de seus dados. Integrado ao Adobe Experience Platform, [!DNL Data Science Workspace] ajuda você a fazer previsões usando seus ativos de conteúdo e dados nas soluções do Adobe. Os cientistas de dados de todos os níveis de competência têm ferramentas sofisticadas e fáceis de usar que apoiam o desenvolvimento rápido, o treinamento e o ajuste das receitas de aprendizado de máquina - todos os benefícios da tecnologia de IA, sem a complexidade.

Para saber mais, comece lendo a [Visão geral do Data Science Workspace](../data-science-workspace/home.md).

## [!DNL Sensei Machine Learning] API

A API [!DNL Sensei Machine Learning] fornece um mecanismo para que os cientistas de dados organizem e gerenciem serviços de aprendizado de máquina, desde a integração de algoritmos à experimentação e à implantação de serviços.

**Os seguintes guias de desenvolvedor de API estão disponíveis:**
- [Mecanismos](../data-science-workspace/api/engines.md)  - saiba como pesquisar seu  [!DNL Docker] registro, criar um Mecanismo, criar um Mecanismo de pipeline de recursos, recuperar as informações de um Mecanismo, atualizar um Mecanismo e excluir um Mecanismo.
- [MLInpositions (receitas)](../data-science-workspace/api/mlinstances.md)  - saiba como criar uma MLIntent, recuperar as informações de uma MLIntent, atualizar uma MLIntent e excluir uma MLIntent.
- [Experimentos](../data-science-workspace/api/experiments.md)  - saiba como criar um Experimento, recuperar um Experimento ou Experimento executa informações, atualizar um Experimento e excluir um Experimento.
- [Modelos](../data-science-workspace/api/models.md)  - saiba como registrar seu próprio modelo, recuperar as informações de um modelo, atualizar um modelo, excluir um modelo, criar uma nova transcodificação para um modelo e recuperar os detalhes de um modelo transcodificado.
- [MLServices](../data-science-workspace/api/mlservices.md)  - Saiba como criar um MLService, recuperar as informações de um MLService, atualizar um MLService e excluir um MLService.
- [Insights](../data-science-workspace/api/insights.md)  - Saiba como recuperar as informações de um Insight, adicionar um novo Insight de modelo e recuperar uma lista de métricas padrão para algoritmos.

Para saber mais e obter os valores necessários para executar operações CRUD com a API de aprendizado de máquina do Sensei, visite o [guia de introdução](../data-science-workspace/api/getting-started.md).

## Como usar [!DNL JupyterLab] notebooks

[!DNL JupyterLab] O é uma interface do usuário baseada na Web para  [!DNL Project Jupyter] e está totalmente integrada ao Adobe Experience Platform. Ele fornece um ambiente de desenvolvimento interativo para que os cientistas de dados trabalhem com [!DNL Jupyter Notebooks], código e dados. Este documento fornece uma visão geral do [!DNL JupyterLab] e seus recursos, bem como instruções para executar ações comuns.

**Este guia ajudará você a:**
- Acesse e entenda a interface [!DNL JupyterLab].
- Entenda as células de código e os kernels disponíveis em [!DNL JupyterLab].
- Entenda a configuração da GPU e do servidor de memória em [!DNL Python]/R.

Para saber mais, visite o [Guia do usuário do JupyterLab](../data-science-workspace/jupyterlab/overview.md).

## Acesso a dados em notebooks JupyterLab

Atualmente, o JupyterLab no Data Science Workspace oferece suporte a notebooks para [!DNL Python], R, PySpark e Scala. Cada kernel suportado fornece funcionalidades integradas que permitem ler os dados da plataforma a partir de um conjunto de dados dentro de um notebook. No entanto, o suporte para paginação de dados é limitado aos blocos de anotações [!DNL Python] e R. Este guia tem como foco o uso de notebooks JupyterLab para acessar seus dados.

**Este guia ajudará você a:**
- Leia, grave e consulte os dados da plataforma usando os notebooks Python, R, PySpark ou Scala.
- Entenda as limitações de leitura de cada tipo de notebook.

Para saber mais, visite o [Guia do desenvolvedor de acesso a dados do notebook JupyterLab](../data-science-workspace/jupyterlab/access-notebook-data.md)

## Arquivos de origem de pacote para criação de receita [!DNL Docker]

Uma imagem [!DNL Docker] permite agrupar um aplicativo com todas as partes necessárias. Isso inclui bibliotecas e outras dependências em um único pacote. A imagem [!DNL Docker] criada é enviada para o [!DNL Azure Container Registry] usando as credenciais fornecidas para você durante o fluxo de trabalho de criação da receita.

**Este tutorial ajudará você a:**
- Baixe os pré-requisitos necessários para a criação da receita.
- Entenda a criação de modelo baseada em [!DNL Docker].
- Crie uma imagem [!DNL Docker] para [!DNL Python], R, PySpark ou Scala ([!DNL Spark]).
- Obtenha um URL de arquivo de origem [!DNL Docker].

Para saber mais, siga os [arquivos-fonte do pacote em um tutorial de receita](../data-science-workspace/models-recipes/package-source-files-recipe.md).

## Importar uma fórmula

>[!NOTE]
>
>Este tutorial requer que você tenha um URL de arquivo de origem [!DNL Docker]. Visite os [arquivos de origem do pacote em um tutorial de receita](../data-science-workspace/models-recipes/package-source-files-recipe.md) se não tiver um URL de arquivo de origem [!DNL Docker].

Os tutoriais de importação de receita fornecem insights sobre como configurar e importar uma receita empacotada. Ao final deste tutorial, você pode criar, treinar e avaliar um Modelo no Adobe Experience Platform [!DNL Data Science Workspace].

**Este tutorial ajudará você a:**
- Crie um conjunto de configurações para uma fórmula.
- Importe uma receita baseada em [!DNL Docker] para [!DNL Python], R, PySpark ou Scala ([!DNL Spark]).

Para saber mais, siga o tutorial importar uma receita empacotada [UI](../data-science-workspace/models-recipes/import-packaged-recipe-ui.md) ou o [tutorial de API](../data-science-workspace/models-recipes/import-packaged-recipe-api.md).

## Comboio e avaliação de um modelo

No Adobe Experience Platform [!DNL Data Science Workspace], um Modelo de aprendizado de máquina é criado incorporando uma Receita existente apropriada para a intenção do Modelo. O Modelo é então treinado e avaliado para otimizar sua eficiência e eficácia operacional ajustando seus hiperparâmetros associados. Receitas são reutilizáveis, o que significa que vários Modelos podem ser criados e adaptados a fins específicos com uma única Receita.

**Este tutorial ajudará você a:**
- Crie um novo Modelo.
- Crie uma execução de treinamento para seu modelo.
- Avalie as execuções de treinamento do Modelo.

Para começar, siga o treinamento e avalie um [tutorial de API](../data-science-workspace/models-recipes/train-evaluate-model-api.md) ou o [tutorial de interface do usuário](../data-science-workspace/models-recipes/train-evaluate-model-ui.md) de modelo.

## Otimizar um modelo usando a estrutura de insights do modelo

A Estrutura de insights do modelo fornece ao cientista de dados ferramentas no Adobe Experience Platform [!DNL Data Science Workspace] para fazer escolhas rápidas e informadas para modelos ideais de aprendizado de máquina com base em experimentos. A estrutura melhorará a velocidade e a eficácia do fluxo de trabalho de aprendizado de máquina, bem como a facilidade de uso para cientistas de dados. Isso é feito fornecendo um modelo padrão para cada tipo de algoritmo de aprendizado de máquina para auxiliar no ajuste do modelo. O resultado final permite que cientistas de dados e cientistas de dados cidadãos tomem melhores decisões de otimização de modelos para seus clientes finais.

**Este tutorial ajudará você a:**
- Configure o código da receita.
- Defina métricas personalizadas.
- Use métricas de avaliação e gráficos de visualização pré-criados.

Para começar, siga o tutorial em [otimizando um modelo](../data-science-workspace/models-recipes/optimize-model.md).

## Pontuar um modelo

A pontuação no Adobe Experience Platform [!DNL Data Science Workspace] pode ser alcançada ao alimentar os dados de entrada em um Modelo treinado existente. Os resultados da pontuação são armazenados e visualizados em um conjunto de dados de saída especificado como um novo lote.

**Este tutorial ajudará você a:**
- Crie uma nova execução de pontuação.
- Visualize seus resultados de pontuação.

Para começar, siga a pontuação de um modelo [tutorial da API](../data-science-workspace/models-recipes/score-model-api.md) ou o [tutorial da interface do usuário](../data-science-workspace/models-recipes/score-model-ui.md).

## Publicar um modelo como um serviço

O Adobe Experience Platform [!DNL Data Science Workspace] permite que você publique seu Modelo como um serviço, permitindo que os usuários em sua Organização IMS marquem dados sem a necessidade de criar seus próprios Modelos. Isso pode ser feito usando a interface do usuário [!DNL Platform] ou a API [!DNL Sensei Machine Learning].

**Este tutorial ajudará você a:**
- Publicar um modelo como um serviço.
- Pontuação de dados usando um serviço por meio do [!DNL Platform] [!UICONTROL Service Gallery].

Para começar, siga o tutorial publicar um modelo como um serviço [API ](../data-science-workspace/models-recipes/publish-model-service-api.md) ou o [tutorial da interface do usuário](../data-science-workspace/models-recipes/publish-model-service-ui.md).

## Agendar treinamento e pontuação para um Modelo

O Adobe Experience Platform [!DNL Data Science Workspace] permite que você configure a pontuação agendada e a execução do treinamento em um serviço de aprendizado de máquina. A automatização do processo de treinamento e pontuação pode ajudar a manter e melhorar a eficiência de um serviço ao longo do tempo, mantendo os padrões em seus dados.

**Este tutorial ajudará você a:**
- Configurar pontuação agendada
- Configurar treinamento programado

Para começar, siga o [agendar um tutorial de interface de modelo](../data-science-workspace/models-recipes/schedule-models-ui.md).

## Criar um pipeline de recursos

>[!NOTE]
>
>Atualmente, os pipelines de recursos só estão disponíveis por meio da API.

O Adobe Experience Platform permite criar e criar pipelines de recursos personalizados para executar a engenharia de recursos em escala pelo [!DNL Sensei Machine Learning Framework Runtime].

**Este guia ajudará você a:**
- Implemente classes de pipeline de recursos.
- Crie um mecanismo de pipeline de recurso usando a API .

Para saber mais, visite o tutorial para [criar um pipeline de recursos](../data-science-workspace/authoring/feature-pipeline.md).

## Criar um aplicativo [!DNL Real-Time Machine Learning] (alfa)

Uma combinação de computação contínua no Hub e no [!DNL Edge] reduz drasticamente a latência tradicionalmente envolvida no fornecimento de experiências hiper-personalizadas que são relevantes e responsivas. Portanto, [!DNL Real-time Machine Learning] fornece inferências com uma latência incrivelmente baixa para a tomada de decisão síncrona. Os exemplos incluem renderização de conteúdo personalizado da página da Web, criação de uma oferta e descontos para reduzir o churn enquanto aumenta as conversões em uma loja da Web.

**Este guia ajudará você a:**
- Entenda a arquitetura [!DNL Real-time Machine Learning].
- Entenda o workflow [!DNL Real-time Machine Learning].
- Entenda a funcionalidade atual para [!DNL Real-time Machine Learning].
- Forneça as próximas etapas para criar seu próprio [!DNL Real-time Machine Learning model].

Para saber mais, visite a [Visão geral do aprendizado de máquina em tempo real](../data-science-workspace/real-time-machine-learning/home.md).
