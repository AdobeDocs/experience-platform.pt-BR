---
keywords: Experience Platform, guia do desenvolvedor, Data Science Workspace, tópicos populares, aprendizado de máquina em tempo real;
solution: Experience Platform
title: Introdução ao aprendizado de máquina em tempo real
topic-legacy: Getting started
description: O documento a seguir descreve as etapas necessárias para criar um modelo de aprendizado de máquina em tempo real no Adobe Experience Platform.
exl-id: 90a1c580-f6e7-4517-aa1e-da5092fbc4a2
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 0%

---

# Introdução ao Aprendizagem de máquina em tempo real (Alpha)

>[!IMPORTANT]
>
>O Aprendizado de máquina em tempo real ainda não está disponível para todos os usuários. Esse recurso está em alfa e ainda está sendo testado. Este documento está sujeito a alterações.

Para utilizar o Real-time Machine Learning, você precisa ter acesso a uma organização provisionada com Adobe Experience Platform e [!DNL Data Science Workspace]. Além disso, é necessário ter um conjunto de dados completo para usar em treinamento e pontuação.

Os guias para o Aprendizado de máquina em tempo real exigem uma compreensão funcional do Python 3, [Notebooks Jupyter](../jupyterlab/overview.md), ciência de dados e aprendizado de máquina.

**Termos principais:**

- **DSL:** idioma específico do domínio.
- **Edge:** o serviço de pontuação do Real-time Machine Learning pode ser executado em clusters da Edge mais próximos de suas ativações e aplicativos.
- **Hub:** o alfa atual está executando o serviço de pontuação do Aprendizado de máquina em tempo real no Hub da Adobe Experience Platform enquanto a Rede de borda da experiência está em desenvolvimento.
- **Nó:** Um Nó é a unidade fundamental da formação dos gráficos. Cada nó executa uma tarefa específica e pode ser encadeado usando links para formar um gráfico que representa um pipeline ML. A tarefa executada por um nó representa uma operação em dados de entrada, como uma transformação de dados ou esquema ou uma inferência de aprendizado de máquina. O nó gera o valor transformado ou inferido para o(s) próximo(s) nó(s).

## Conjuntos de dados no Adobe Experience Platform

Para começar a usar o Real-time Machine Learning, você deve ter acesso a um conjunto de dados. Você tem a opção de usar um conjunto de dados externo e carregá-lo em seu ambiente [!DNL JupyterLab] ou criar um novo conjunto de dados na Platform, se ainda não tiver feito isso.

>[!NOTE]
>
>Se você já tiver um conjunto de dados que deseja usar, pule para [Próximas etapas](#next-steps).

### Usar um conjunto de dados externo

Para saber mais sobre como usar um conjunto de dados externo, como carregar dados em seu ambiente [!DNL JupyterLab], visite o tutorial em [analisar seus dados usando blocos de anotações](../jupyterlab/analyze-your-data.md#external-data).

### Criar um novo conjunto de dados

Para criar um novo conjunto de dados para usar no Real-time Machine Learning, é necessário um esquema de dados para o conjunto de dados. Em seguida, é necessário assimilar dados usando o schema criado. Use os seguintes tutoriais para criar e preencher um conjunto de dados para [!DNL Platform]:

- [Criar e preencher um conjunto de dados na API](../../catalog/datasets/create.md)
- [Criar e preencher um conjunto de dados na interface do usuário](../../ingestion/tutorials/ingest-batch-data.md)

## Próximas etapas {#next-steps}

Depois de preparar seus dados para o Aprendizado de máquina em tempo real, comece seguindo o [Guia do usuário do notebook Aprendizagem de máquina em tempo real](./rtml-authoring-notebook.md) para saber como criar e carregar um modelo ONNX para a loja de modelos de Aprendizagem de máquina em tempo real.
