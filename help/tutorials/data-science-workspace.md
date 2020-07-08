---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Tutoriais da Data Science Workspace
topic: tutorial
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '1252'
ht-degree: 0%

---


# Tutoriais da Data Science Workspace

A Adobe Experience Platform Data Science Workspace usa o aprendizado de máquina e a inteligência artificial para criar insights de seus dados. Integrado ao Adobe Experience Platform, o Data Science Workspace ajuda você a fazer previsões usando seus ativos de conteúdo e dados nas soluções da Adobe. Os cientistas de dados de todos os níveis de habilidades têm ferramentas sofisticadas e fáceis de usar que suportam o rápido desenvolvimento, treinamento e ajuste de fórmulas de aprendizado de máquina - todos os benefícios da tecnologia da IA, sem a complexidade.

Para saber mais, comece lendo a visão geral [](../data-science-workspace/home.md)da Data Science Workspace.

## API de aprendizado de máquina do Sensei

A API Sensei Machine Learning fornece um mecanismo para que os cientistas de dados organizem e gerenciem serviços de aprendizado de máquina, desde a integração de algoritmos até a experimentação e a implantação de serviços.

**Os seguintes guias de desenvolvedor de API estão disponíveis:**
- [Mecanismos](../data-science-workspace/api/engines.md) - saiba como procurar seu registro do Docker, criar um Mecanismo, criar um Mecanismo de pipeline de recursos, recuperar as informações de um Mecanismo, atualizar um Mecanismo e excluir um Mecanismo.
- [MLInensons (receitas)](../data-science-workspace/api/mlinstances.md) - saiba como criar uma MLInpresence, recupere as informações de uma MLIntent, atualize uma MLIntent e exclua uma MLInpresence.
- [Experimentos](../data-science-workspace/api/experiments.md) - saiba como criar um Experimento, recuperar um Experimento ou Experimento executa informações, atualizar um Experimento e excluir um Experimento.
- [Modelos](../data-science-workspace/api/models.md) - saiba como registrar seu próprio Modelo, recuperar as informações de um Modelo, atualizar um Modelo, excluir um Modelo, criar uma nova transcodificação para um Modelo e recuperar os detalhes de um Modelo transcodificado.
- [MLServices](../data-science-workspace/api/mlservices.md) - Saiba como criar um MLService, recuperar as informações de um MLService, atualizar um MLService e excluir um MLService.
- [Insights](../data-science-workspace/api/insights.md) - saiba como recuperar as informações de um Insight, adicionar um novo Modelo de Insight e recuperar uma lista de métricas padrão para algoritmos.

Para saber mais e obter os valores necessários para executar operações CRUD com a API Sensei Machine Learning, visite o guia [de](../data-science-workspace/api/getting-started.md)introdução.

## Como usar notebooks JupyterLab

[!DNL JupyterLab] é uma interface de usuário baseada na Web para [!DNL Project Jupyter] e é totalmente integrada ao Adobe Experience Platform. Ele fornece um ambiente de desenvolvimento interativo para que os cientistas de dados trabalhem com notebooks, códigos e dados de Júpiter. Este documento fornece uma visão geral de [!DNL JupyterLab] e seus recursos, bem como instruções para executar ações comuns.

**Este guia o ajudará a:**
- Acesse e entenda a [!DNL JupyterLab] interface.
- Entenda as células de código e os kernels disponíveis dentro [!DNL JupyterLab].
- Entenda a configuração da GPU e do servidor de memória no Python/R.
- Leia e query [!DNL Platform] de dados usando notebooks.
- Entenda os limites de dados do notebook.

Para saber mais, visite o guia [do usuário do](../data-science-workspace/jupyterlab/overview.md)JupyterLab.

## Arquivos de origem do pacote para a criação de receita do Docker

Uma imagem do Docker permite que você empacote um aplicativo com todas as partes de que precisa. Isso inclui bibliotecas e outras dependências em um único pacote. A imagem do Docker criada é enviada para o Registro de Container do Azure usando as credenciais fornecidas a você durante o fluxo de trabalho de criação da receita.

**Este tutorial o ajudará a:**
- Baixe os pré-requisitos necessários para a criação da fórmula.
- Entenda a criação de modelo baseada no Docker.
- Crie uma imagem Docker para Python, R, PySpark ou Scala (Spark).
- Obtenha um URL de arquivo de origem do Docker.

Para saber mais, siga os arquivos de origem do [pacote em um tutorial](../data-science-workspace/models-recipes/package-source-files-recipe.md)de fórmula.

## Importar uma fórmula

>[!NOTE]
>
>
>Este tutorial requer que você tenha um URL de arquivo de origem do Docker. Visite os arquivos de origem do [pacote em um tutorial](../data-science-workspace/models-recipes/package-source-files-recipe.md) de fórmula se você não tiver um URL de arquivo de origem do Docker.

Os tutoriais de importação de fórmula fornecem insights sobre como configurar e importar uma receita empacotada. Até o final deste tutorial, você pode criar, treinar e avaliar um Modelo na Área de Trabalho de Ciência de Dados do Adobe Experience Platform.

**Este tutorial o ajudará a:**
- Crie um conjunto de configurações para uma fórmula.
- Importe uma receita baseada em Docker para Python, R, PySpark ou Scala (Spark).

Para saber mais, siga o tutorial [de importação de uma](../data-science-workspace/models-recipes/import-packaged-recipe-ui.md) interface de usuário de fórmula empacotada ou o tutorial [de](../data-science-workspace/models-recipes/import-packaged-recipe-api.md)API.

## Comboio e avaliação de um modelo

Na área de trabalho da Adobe Experience Platform Data Science, um Modelo de aprendizado de máquina é criado pela incorporação de uma Receita existente adequada à intenção do Modelo. O Modelo é então treinado e avaliado para otimizar sua eficiência e eficiência operacional ajustando seus hiperparâmetros associados. As receitas são reutilizáveis, o que significa que vários Modelos podem ser criados e adaptados para fins específicos com uma única Receita.

**Este tutorial o ajudará a:**
- Criar um novo modelo.
- Crie uma execução de treinamento para seu Modelo.
- Avalie suas execuções de treinamento do Modelo.

Para começar, siga o treinamento e avalie um tutorial [da](../data-science-workspace/models-recipes/train-evaluate-model-api.md) API de modelo ou o tutorial [da](../data-science-workspace/models-recipes/train-evaluate-model-ui.md)interface do usuário.

## Otimizar um modelo usando a estrutura do Model Insights

A Estrutura de insights do Modelo fornece ao cientista de dados ferramentas na Área de trabalho de Adobe Experience Platform Data Science para fazer escolhas rápidas e informadas para obter modelos ideais de aprendizado de máquina com base em experimentos. A estrutura melhorará a velocidade e a eficácia do fluxo de trabalho de aprendizado de máquina, bem como a facilidade de uso para cientistas de dados. Isso é feito fornecendo um modelo padrão para cada tipo de algoritmo de aprendizado da máquina para auxiliar no ajuste do modelo. O resultado final permite que cientistas de dados e cientistas de dados cidadãos tomem decisões de otimização de modelos melhores para seus clientes finais.

**Este tutorial o ajudará a:**
- Configure o código da fórmula.
- Defina métricas personalizadas.
- Use métricas de avaliação e gráficos de visualização pré-criados.

Para começar, siga o tutorial sobre como [otimizar um modelo](../data-science-workspace/models-recipes/optimize-model.md).

## Pontuar um modelo

A pontuação na área de trabalho de Adobe Experience Platform Data Science pode ser alcançada ao alimentar dados de entrada em um Modelo treinado existente. Os resultados da pontuação são armazenados e visualizáveis em um conjunto de dados de saída especificado como um novo lote.

**Este tutorial o ajudará a:**
- Criar uma nova execução de pontuação.
- Visualização nos resultados da pontuação.

Para começar, siga a pontuação de um tutorial [da](../data-science-workspace/models-recipes/score-model-api.md) API de modelo ou o tutorial [da](../data-science-workspace/models-recipes/score-model-ui.md)interface do usuário.

## Publicar um modelo como um serviço

O Adobe Experience Platform Data Science Workspace permite que você publique seu Modelo como um serviço, permitindo que os usuários em sua organização IMS pontuem dados sem a necessidade de criar seus próprios Modelos. Isso pode ser feito usando a interface do [!DNL Platform] usuário ou a API Sensei Machine Learning.

**Este tutorial o ajudará a:**
- Publicar um modelo como um serviço.
- Pontuar dados usando um serviço pela [!DNL Platform] Galeria de serviços.

Para começar, siga o tutorial [de publicação de um modelo como uma](../data-science-workspace/models-recipes/publish-model-service-api.md) API de serviço ou o tutorial [da](../data-science-workspace/models-recipes/publish-model-service-ui.md)interface do usuário.

## Agendar treinamento e pontuação para um Modelo

O Adobe Experience Platform Data Science Workspace permite configurar execuções programadas de pontuação e treinamento em um serviço de aprendizado de máquina. Automatizar o processo de treinamento e pontuação pode ajudar a manter e melhorar a eficiência de um serviço ao longo do tempo, acompanhando os padrões em seus dados.

**Este tutorial o ajudará a:**
- Configurar pontuação programada
- Configurar treinamento agendado

Para começar, siga o [cronograma de um tutorial](../data-science-workspace/models-recipes/schedule-models-ui.md)de interface de usuário modelo.

## Criar um pipeline de recursos

>[!NOTE]
>Atualmente, os pipelines de recursos estão disponíveis somente por meio da API.

O Adobe Experience Platform permite que você crie e crie pipelines de recursos personalizados para executar engenharia de recursos em escala por meio do Tempo de execução da Sensei Machine Learning Framework.

**Este guia o ajudará a:**
- Implementar classes de pipeline de recursos.
- Crie um mecanismo de pipeline de recursos usando a API.

Para saber mais, visite o tutorial para [criar um pipeline](../data-science-workspace/authoring/feature-pipeline.md)de recursos.

## Criar um aplicativo de aprendizado de máquina em tempo real (alfa)

Uma combinação de computação ininterrupta no Hub e no Hub reduz [!DNL Edge] drasticamente a latência tradicionalmente envolvida na potencialização de experiências hiper-personalizadas relevantes e responsivas. Assim, o aprendizado de máquina em tempo real oferece inferências com uma latência incrivelmente baixa para a tomada de decisões síncrona. Os exemplos incluem a renderização de conteúdo personalizado da página da Web, a criação de uma oferta e descontos para reduzir a taxa de processamento enquanto aumentam as conversões em uma loja da Web.

**Este guia o ajudará a:**
- Entenda a arquitetura de aprendizado de máquina em tempo real.
- Entenda o fluxo de trabalho de aprendizado de máquina em tempo real.
- Entenda a funcionalidade atual para Aprendizagem de máquina em tempo real.
- Forneça as próximas etapas para criar seu próprio modelo de aprendizado de máquina em tempo real.

Para saber mais, visite a visão geral [de aprendizado de máquina em tempo](../data-science-workspace/real-time-machine-learning/home.md)real.