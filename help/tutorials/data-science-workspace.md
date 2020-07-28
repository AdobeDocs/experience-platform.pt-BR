---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Tutoriais da Data Science Workspace
topic: tutorial
translation-type: tm+mt
source-git-commit: 5c5f6c4868e195aef76bacc0a1e5df3857647bde
workflow-type: tm+mt
source-wordcount: '1171'
ht-degree: 0%

---


# [!DNL Data Science Workspace] tutoriais

O Adobe Experience Platform [!DNL Data Science Workspace] usa o aprendizado de máquina e a inteligência artificial para criar insights de seus dados. Integrado ao Adobe Experience Platform, [!DNL Data Science Workspace] ajuda você a fazer previsões usando seu conteúdo e seus ativos de dados nas soluções de Adobe. Os cientistas de dados de todos os níveis de habilidades têm ferramentas sofisticadas e fáceis de usar que suportam o rápido desenvolvimento, treinamento e ajuste de fórmulas de aprendizado de máquina - todos os benefícios da tecnologia da IA, sem a complexidade.

Para saber mais, comece lendo a visão geral [](../data-science-workspace/home.md)da Data Science Workspace.

## [!DNL Sensei Machine Learning] API

A [!DNL Sensei Machine Learning] API fornece um mecanismo para os cientistas de dados organizarem e gerenciarem serviços de aprendizado de máquina, desde a integração de algoritmos até a experimentação e a implantação de serviços.

**Os seguintes guias de desenvolvedor de API estão disponíveis:**
- [Mecanismos](../data-science-workspace/api/engines.md) - saiba como procurar seu [!DNL Docker] registro, criar um Mecanismo, criar um Mecanismo de pipeline de recursos, recuperar as informações de um Mecanismo, atualizar um Mecanismo e excluir um Mecanismo.
- [MLInensons (receitas)](../data-science-workspace/api/mlinstances.md) - saiba como criar uma MLInpresence, recupere as informações de uma MLIntent, atualize uma MLIntent e exclua uma MLInpresence.
- [Experimentos](../data-science-workspace/api/experiments.md) - saiba como criar um Experimento, recuperar um Experimento ou Experimento executa informações, atualizar um Experimento e excluir um Experimento.
- [Modelos](../data-science-workspace/api/models.md) - saiba como registrar seu próprio Modelo, recuperar as informações de um Modelo, atualizar um Modelo, excluir um Modelo, criar uma nova transcodificação para um Modelo e recuperar os detalhes de um Modelo transcodificado.
- [MLServices](../data-science-workspace/api/mlservices.md) - Saiba como criar um MLService, recuperar as informações de um MLService, atualizar um MLService e excluir um MLService.
- [Insights](../data-science-workspace/api/insights.md) - saiba como recuperar as informações de um Insight, adicionar um novo Modelo de Insight e recuperar uma lista de métricas padrão para algoritmos.

Para saber mais e obter os valores necessários para executar operações CRUD com a API de aprendizado de máquina do Sensei, visite o guia [de](../data-science-workspace/api/getting-started.md)introdução.

## How to use [!DNL JupyterLab] Notebooks

[!DNL JupyterLab] é uma interface de usuário baseada na Web para [!DNL Project Jupyter] e é totalmente integrada ao Adobe Experience Platform. Ele fornece um ambiente de desenvolvimento interativo para que os cientistas de dados trabalhem com [!DNL Jupyter notebooks], código e dados. Este documento fornece uma visão geral de [!DNL JupyterLab] e seus recursos, bem como instruções para executar ações comuns.

**Este guia o ajudará a:**
- Acesse e entenda a [!DNL JupyterLab] interface.
- Entenda as células de código e os kernels disponíveis dentro [!DNL JupyterLab].
- Entenda a configuração da GPU e do servidor de memória em [!DNL Python]/R.
- Leia e query [!DNL Platform] de dados usando notebooks.
- Entenda os limites de dados do notebook.

Para saber mais, visite o guia [do usuário do](../data-science-workspace/jupyterlab/overview.md)JupyterLab.

## Arquivos de origem do pacote para criação de [!DNL Docker] fórmula

Uma [!DNL Docker] imagem permite empacotar um aplicativo com todas as partes de que ele precisa. Isso inclui bibliotecas e outras dependências em um único pacote. A [!DNL Docker] imagem criada é encaminhada para o [!DNL Azure Container Registry] usando as credenciais fornecidas a você durante o fluxo de trabalho de criação da receita.

**Este tutorial o ajudará a:**
- Baixe os pré-requisitos necessários para a criação da fórmula.
- Entenda a criação de modelos [!DNL Docker] baseados.
- Crie uma [!DNL Docker] imagem para [!DNL Python], R, PySpark ou Scala ([!DNL Spark]).
- Obtenha um URL de arquivo [!DNL Docker] de origem.

Para saber mais, siga os arquivos de origem do [pacote em um tutorial](../data-science-workspace/models-recipes/package-source-files-recipe.md)de fórmula.

## Importar uma fórmula

>[!NOTE]
>
>
>Este tutorial requer que você tenha um URL de arquivo [!DNL Docker] de origem. Visite os arquivos de origem do [pacote em um tutorial](../data-science-workspace/models-recipes/package-source-files-recipe.md) de fórmula se você não tiver um URL de arquivo de [!DNL Docker] origem.

Os tutoriais de importação de fórmula fornecem insights sobre como configurar e importar uma receita empacotada. Ao final deste tutorial, você pode criar, treinar e avaliar um Modelo no Adobe Experience Platform [!DNL Data Science Workspace].

**Este tutorial o ajudará a:**
- Crie um conjunto de configurações para uma fórmula.
- Importe uma fórmula [!DNL Docker] baseada para [!DNL Python], R, PySpark ou Scala ([!DNL Spark]).

Para saber mais, siga o tutorial [de importação de uma](../data-science-workspace/models-recipes/import-packaged-recipe-ui.md) interface de usuário de fórmula empacotada ou o tutorial [de](../data-science-workspace/models-recipes/import-packaged-recipe-api.md)API.

## Comboio e avaliação de um modelo

Na Adobe Experience Platform [!DNL Data Science Workspace], um Modelo de aprendizado de máquina é criado pela incorporação de uma Receita existente adequada à intenção do Modelo. O Modelo é então treinado e avaliado para otimizar sua eficiência e eficiência operacional ajustando seus hiperparâmetros associados. As receitas são reutilizáveis, o que significa que vários Modelos podem ser criados e adaptados para fins específicos com uma única Receita.

**Este tutorial o ajudará a:**
- Criar um novo modelo.
- Crie uma execução de treinamento para seu Modelo.
- Avalie suas execuções de treinamento do Modelo.

Para começar, siga o treinamento e avalie um tutorial [da](../data-science-workspace/models-recipes/train-evaluate-model-api.md) API de modelo ou o tutorial [da](../data-science-workspace/models-recipes/train-evaluate-model-ui.md)interface do usuário.

## Otimizar um modelo usando a estrutura do Model Insights

A Framework Model Insights fornece ao cientista de dados ferramentas no Adobe Experience Platform [!DNL Data Science Workspace] para fazer escolhas rápidas e informadas para modelos ideais de aprendizado de máquina com base em experimentos. A estrutura melhorará a velocidade e a eficácia do fluxo de trabalho de aprendizado de máquina, bem como a facilidade de uso para cientistas de dados. Isso é feito fornecendo um modelo padrão para cada tipo de algoritmo de aprendizado da máquina para auxiliar no ajuste do modelo. O resultado final permite que cientistas de dados e cientistas de dados cidadãos tomem decisões de otimização de modelos melhores para seus clientes finais.

**Este tutorial o ajudará a:**
- Configure o código da fórmula.
- Defina métricas personalizadas.
- Use métricas de avaliação e gráficos de visualização pré-criados.

Para começar, siga o tutorial sobre como [otimizar um modelo](../data-science-workspace/models-recipes/optimize-model.md).

## Pontuar um modelo

A pontuação no Adobe Experience Platform [!DNL Data Science Workspace] pode ser alcançada ao alimentar dados de entrada em um Modelo treinado existente. Os resultados da pontuação são armazenados e visualizáveis em um conjunto de dados de saída especificado como um novo lote.

**Este tutorial o ajudará a:**
- Criar uma nova execução de pontuação.
- Visualização nos resultados da pontuação.

Para começar, siga a pontuação de um tutorial [da](../data-science-workspace/models-recipes/score-model-api.md) API de modelo ou o tutorial [da](../data-science-workspace/models-recipes/score-model-ui.md)interface do usuário.

## Publicar um modelo como um serviço

O Adobe Experience Platform [!DNL Data Science Workspace] permite que você publique seu Modelo como um serviço, permitindo que os usuários na organização IMS pontuem dados sem a necessidade de criar seus próprios Modelos. Isso pode ser feito usando a interface do [!DNL Platform] usuário ou a [!DNL Sensei Machine Learning] API.

**Este tutorial o ajudará a:**
- Publicar um modelo como um serviço.
- Pontuação de dados usando um serviço por meio da Galeria [!DNL Platform] de serviços.

Para começar, siga o tutorial [de publicação de um modelo como uma](../data-science-workspace/models-recipes/publish-model-service-api.md) API de serviço ou o tutorial [da](../data-science-workspace/models-recipes/publish-model-service-ui.md)interface do usuário.

## Agendar treinamento e pontuação para um Modelo

O Adobe Experience Platform [!DNL Data Science Workspace] permite que você configure a pontuação programada e as execuções de treinamento em um serviço de aprendizado de máquina. Automatizar o processo de treinamento e pontuação pode ajudar a manter e melhorar a eficiência de um serviço ao longo do tempo, acompanhando os padrões em seus dados.

**Este tutorial o ajudará a:**
- Configurar pontuação programada
- Configurar treinamento agendado

Para começar, siga o [cronograma de um tutorial](../data-science-workspace/models-recipes/schedule-models-ui.md)de interface de usuário modelo.

## Criar um pipeline de recursos

>[!NOTE]
>Atualmente, os pipelines de recursos estão disponíveis somente por meio da API.

O Adobe Experience Platform permite que você crie e crie pipelines de recursos personalizados para executar engenharia de recursos em escala pelo [!DNL Sensei Machine Learning Framework Runtime].

**Este guia o ajudará a:**
- Implementar classes de pipeline de recursos.
- Crie um mecanismo de pipeline de recursos usando a API.

Para saber mais, visite o tutorial para [criar um pipeline](../data-science-workspace/authoring/feature-pipeline.md)de recursos.

## Criar um [!DNL Real-Time Machine Learning] aplicativo (alfa)

Uma combinação de computação ininterrupta no Hub e no Hub reduz [!DNL Edge] drasticamente a latência tradicionalmente envolvida na potencialização de experiências hiper-personalizadas relevantes e responsivas. Assim, [!DNL Real-time Machine Learning] fornece inferências com uma latência incrivelmente baixa para a tomada de decisões síncrona. Os exemplos incluem a renderização de conteúdo personalizado da página da Web, a criação de uma oferta e descontos para reduzir a taxa de processamento enquanto aumentam as conversões em uma loja da Web.

**Este guia o ajudará a:**
- Entenda a [!DNL Real-time Machine Learning] arquitetura.
- Entenda o [!DNL Real-time Machine Learning] fluxo de trabalho.
- Entenda a funcionalidade atual para [!DNL Real-time Machine Learning].
- Forneça as próximas etapas para criar suas próprias etapas [!DNL Real-time Machine Learning model].

Para saber mais, visite a visão geral [de aprendizado de máquina em tempo](../data-science-workspace/real-time-machine-learning/home.md)real.