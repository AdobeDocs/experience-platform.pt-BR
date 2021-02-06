---
keywords: Experience Platform;home;popular topics;dsw;DSW
solution: Experience Platform
title: Tutoriais da Data Science Workspace
topic: tutorial
type: Tutorial
description: A Adobe Experience Platform Data Science Workspace usa o aprendizado de máquina e a inteligência artificial para criar insights de seus dados. Integrado ao Adobe Experience Platform, o Data Science Workspace ajuda você a fazer previsões usando seu conteúdo e ativos de dados nas soluções de Adobe.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '1304'
ht-degree: 0%

---


# [!DNL Data Science Workspace] tutoriais

A Adobe Experience Platform [!DNL Data Science Workspace] usa o aprendizado da máquina e a inteligência artificial para criar insights de seus dados. Integrado ao Adobe Experience Platform, [!DNL Data Science Workspace] ajuda você a fazer previsões usando seus ativos de conteúdo e dados nas soluções de Adobe. Os cientistas de dados de todos os níveis de habilidades têm ferramentas sofisticadas e fáceis de usar que suportam o rápido desenvolvimento, treinamento e ajuste de fórmulas de aprendizado de máquina - todos os benefícios da tecnologia da IA, sem a complexidade.

Para saber mais, comece lendo a [visão geral da Data Science Workspace](../data-science-workspace/home.md).

## [!DNL Sensei Machine Learning] API

A API [!DNL Sensei Machine Learning] fornece um mecanismo para que os cientistas de dados organizem e gerenciem serviços de aprendizado de máquina, desde a integração de algoritmos por experimentação e implantação de serviços.

**Os seguintes guias de desenvolvedor de API estão disponíveis:**
- [Mecanismos](../data-science-workspace/api/engines.md)  - saiba como procurar seu  [!DNL Docker] registro, criar um Mecanismo, criar um Mecanismo de pipeline de recursos, recuperar as informações de um Mecanismo, atualizar um Mecanismo e excluir um Mecanismo.
- [MLInensons (receitas)](../data-science-workspace/api/mlinstances.md)  - Saiba como criar uma MLIntent, recuperar as informações de uma MLInpresence, atualizar uma MLIntent e excluir uma MLInpresence.
- [Experimentos](../data-science-workspace/api/experiments.md)  - saiba como criar um Experimento, recuperar um Experimento ou Experimento executa informações, atualizar um Experimento e excluir um Experimento.
- [Modelos](../data-science-workspace/api/models.md)  - saiba como registrar seu próprio Modelo, recuperar as informações de um Modelo, atualizar um Modelo, excluir um Modelo, criar uma nova transcodificação para um Modelo e recuperar os detalhes de um Modelo transcodificado.
- [MLServices](../data-science-workspace/api/mlservices.md)  - Saiba como criar um MLService, recuperar as informações de um MLService, atualizar um MLService e excluir um MLService.
- [Insights](../data-science-workspace/api/insights.md)  - saiba como recuperar as informações de um Insight, adicionar um novo Modelo de Insight e recuperar uma lista de métricas padrão para algoritmos.

Para saber mais e obter os valores necessários para executar operações CRUD com a API Sensei Machine Learning, visite o [guia de introdução](../data-science-workspace/api/getting-started.md).

## Como usar notebooks [!DNL JupyterLab]

[!DNL JupyterLab] é uma interface de usuário baseada na Web para  [!DNL Project Jupyter] e é totalmente integrada ao Adobe Experience Platform. Ele fornece um ambiente de desenvolvimento interativo para que os cientistas de dados trabalhem com [!DNL Jupyter Notebooks], código e dados. Este documento fornece uma visão geral do [!DNL JupyterLab] e seus recursos, bem como instruções para executar ações comuns.

**Este guia o ajudará a:**
- Acesse e entenda a interface [!DNL JupyterLab].
- Entenda as células de código e os kernels disponíveis em [!DNL JupyterLab].
- Entenda a configuração da GPU e do servidor de memória em [!DNL Python]/R.

Para saber mais, visite o [guia do usuário do JupyterLab](../data-science-workspace/jupyterlab/overview.md).

## Acesso a dados em notebooks JupyterLab

Atualmente, o JupyterLab na Data Science Workspace suporta notebooks para [!DNL Python], R, PySpark e Scala. Cada kernel suportado fornece funcionalidades incorporadas que permitem ler dados da plataforma a partir de um conjunto de dados dentro de um notebook. No entanto, o suporte para paginação de dados está limitado aos notebooks [!DNL Python] e R. Este guia foca em como usar notebooks JupyterLab para acessar seus dados.

**Este guia o ajudará a:**
- Leia, grave e utilize os dados da Plataforma de query usando notebooks Python, R, PySpark ou Scala.
- Entenda as limitações de leitura de cada tipo de notebook.

Para saber mais, visite o [Guia do desenvolvedor de acesso aos dados do notebook do JupyterLab](../data-science-workspace/jupyterlab/access-notebook-data.md)

## Arquivos de origem do pacote para criação de receita [!DNL Docker]

Uma imagem [!DNL Docker] permite que você empacote um aplicativo com todas as partes necessárias. Isso inclui bibliotecas e outras dependências em um único pacote. A imagem [!DNL Docker] incorporada é encaminhada para [!DNL Azure Container Registry] usando as credenciais fornecidas a você durante o fluxo de trabalho de criação da fórmula.

**Este tutorial o ajudará a:**
- Baixe os pré-requisitos necessários para a criação da fórmula.
- Entenda a criação de modelos baseados em [!DNL Docker].
- Crie uma imagem [!DNL Docker] para [!DNL Python], R, PySpark ou Scala ([!DNL Spark]).
- Obtenha um URL de arquivo de origem [!DNL Docker].

Para saber mais, siga os [arquivos de origem do pacote em um tutorial de fórmula](../data-science-workspace/models-recipes/package-source-files-recipe.md).

## Importar uma fórmula

>[!NOTE]
>
>Este tutorial requer que você tenha um URL de arquivo de origem [!DNL Docker]. Visite os arquivos de origem do pacote [em um tutorial de fórmula](../data-science-workspace/models-recipes/package-source-files-recipe.md) se você não tiver um URL de arquivo de origem [!DNL Docker].

Os tutoriais de importação de fórmula fornecem insights sobre como configurar e importar uma receita empacotada. Ao final deste tutorial, você pode criar, treinar e avaliar um Modelo no Adobe Experience Platform [!DNL Data Science Workspace].

**Este tutorial o ajudará a:**
- Crie um conjunto de configurações para uma fórmula.
- Importe uma fórmula baseada em [!DNL Docker] para [!DNL Python], R, PySpark ou Scala ([!DNL Spark]).

Para saber mais, siga o tutorial de importação [IU](../data-science-workspace/models-recipes/import-packaged-recipe-ui.md) ou [do tutorial de API](../data-science-workspace/models-recipes/import-packaged-recipe-api.md).

## Comboio e avaliação de um modelo

No Adobe Experience Platform [!DNL Data Science Workspace], um Modelo de aprendizado de máquina é criado pela incorporação de uma Receita existente apropriada para a intenção do Modelo. O Modelo é então treinado e avaliado para otimizar sua eficiência e eficiência operacional ajustando seus hiperparâmetros associados. As receitas são reutilizáveis, o que significa que vários Modelos podem ser criados e adaptados para fins específicos com uma única Receita.

**Este tutorial o ajudará a:**
- Criar um novo modelo.
- Crie uma execução de treinamento para seu Modelo.
- Avalie suas execuções de treinamento do Modelo.

Para começar, siga o treinamento e avalie um modelo [tutorial da API](../data-science-workspace/models-recipes/train-evaluate-model-api.md) ou o [tutorial da interface](../data-science-workspace/models-recipes/train-evaluate-model-ui.md).

## Otimizar um modelo usando a estrutura do Model Insights

O Model Insights Framework fornece ao cientista de dados ferramentas no Adobe Experience Platform [!DNL Data Science Workspace] para fazer escolhas rápidas e informadas para modelos ideais de aprendizado em máquina com base em experimentos. A estrutura melhorará a velocidade e a eficácia do fluxo de trabalho de aprendizado de máquina, bem como a facilidade de uso para cientistas de dados. Isso é feito fornecendo um modelo padrão para cada tipo de algoritmo de aprendizado da máquina para auxiliar no ajuste do modelo. O resultado final permite que cientistas de dados e cientistas de dados cidadãos tomem decisões de otimização de modelos melhores para seus clientes finais.

**Este tutorial o ajudará a:**
- Configure o código da fórmula.
- Defina métricas personalizadas.
- Use métricas de avaliação e gráficos de visualização pré-criados.

Para começar, siga o tutorial em [otimização de um modelo](../data-science-workspace/models-recipes/optimize-model.md).

## Pontuar um modelo

A pontuação no Adobe Experience Platform [!DNL Data Science Workspace] pode ser alcançada ao alimentar dados de entrada em um Modelo treinado existente. Os resultados da pontuação são armazenados e visualizáveis em um conjunto de dados de saída especificado como um novo lote.

**Este tutorial o ajudará a:**
- Criar uma nova execução de pontuação.
- Visualização nos resultados da pontuação.

Para começar, siga a pontuação de um tutorial de API [modelo](../data-science-workspace/models-recipes/score-model-api.md) ou o tutorial de [UI](../data-science-workspace/models-recipes/score-model-ui.md).

## Publicar um modelo como um serviço

A Adobe Experience Platform [!DNL Data Science Workspace] permite que você publique seu Modelo como um serviço, permitindo que os usuários na organização IMS pontuem dados sem a necessidade de criar seus próprios Modelos. Isso pode ser feito usando a interface do usuário [!DNL Platform] ou a API [!DNL Sensei Machine Learning].

**Este tutorial o ajudará a:**
- Publicar um modelo como um serviço.
- Dados de pontuação usando um serviço por meio da [!DNL Platform] [!UICONTROL Service Gallery].

Para começar, siga o tutorial de publicação de um modelo como um serviço [API](../data-science-workspace/models-recipes/publish-model-service-api.md) ou [IU](../data-science-workspace/models-recipes/publish-model-service-ui.md).

## Agendar treinamento e pontuação para um Modelo

O Adobe Experience Platform [!DNL Data Science Workspace] permite que você configure a pontuação programada e as execuções de treinamento em um serviço de aprendizado de máquina. Automatizar o processo de treinamento e pontuação pode ajudar a manter e melhorar a eficiência de um serviço ao longo do tempo, acompanhando os padrões em seus dados.

**Este tutorial o ajudará a:**
- Configurar pontuação programada
- Configurar treinamento agendado

Para começar, siga [agende um tutorial de interface de usuário modelo](../data-science-workspace/models-recipes/schedule-models-ui.md).

## Criar um pipeline de recursos

>[!NOTE]
>
>Atualmente, os pipelines de recursos estão disponíveis somente por meio da API.

A Adobe Experience Platform permite que você crie e crie pipelines de recursos personalizados para executar engenharia de recursos em escala pelo [!DNL Sensei Machine Learning Framework Runtime].

**Este guia o ajudará a:**
- Implementar classes de pipeline de recursos.
- Crie um mecanismo de pipeline de recursos usando a API.

Para saber mais, visite o tutorial para [criar um pipeline de recursos](../data-science-workspace/authoring/feature-pipeline.md).

## Criar um aplicativo [!DNL Real-Time Machine Learning] (alfa)

Uma combinação de computação ininterrupta no Hub e [!DNL Edge] reduz drasticamente a latência tradicionalmente envolvida na potencialização de experiências hiper-personalizadas relevantes e responsivas. Assim, [!DNL Real-time Machine Learning] oferece inferências com uma latência incrivelmente baixa para a tomada de decisões síncrona. Os exemplos incluem a renderização de conteúdo personalizado da página da Web, a criação de uma oferta e descontos para reduzir a taxa de processamento enquanto aumentam as conversões em uma loja da Web.

**Este guia o ajudará a:**
- Entenda a arquitetura [!DNL Real-time Machine Learning].
- Entenda o fluxo de trabalho [!DNL Real-time Machine Learning].
- Entenda a funcionalidade atual para [!DNL Real-time Machine Learning].
- Forneça as próximas etapas para criar seu próprio [!DNL Real-time Machine Learning model].

Para saber mais, visite a [visão geral de aprendizado de máquina em tempo real](../data-science-workspace/real-time-machine-learning/home.md).