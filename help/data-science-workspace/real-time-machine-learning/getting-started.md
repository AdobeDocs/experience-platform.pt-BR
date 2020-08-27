---
keywords: Experience Platform;developer guide;Data Science Workspace;popular topics;Real time machine learning;
solution: Experience Platform
title: Introdução ao aprendizado de máquina em tempo real
topic: Getting started
description: O documento a seguir descreve as etapas necessárias para criar um modelo de aprendizado de máquina em tempo real no Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 9ba229195892245d29fb4f17b9f2e5cd6c6ea567
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 0%

---


# Introdução ao aprendizado de máquina em tempo real (Alpha)

>[!IMPORTANT]
>
>O aprendizado de máquina em tempo real ainda não está disponível para todos os usuários. Esse recurso está em alfa e ainda está sendo testado. Este documento está sujeito a mudanças.

Para utilizar o aprendizado de máquina em tempo real, é necessário ter acesso a uma organização provisionada com a Adobe Experience Platform e [!DNL Data Science Workspace]. Além disso, é necessário ter um conjunto de dados completo para uso em treinamento e pontuação.

Os guias para aprendizado de máquina em tempo real exigem uma compreensão funcional do Python 3, notebooks [de](../jupyterlab/overview.md)Júpiter, ciência de dados e aprendizado de máquina.

**Principais termos:**

- **DSL:** Idioma Específico do Domínio.
- **Borda:** O serviço de pontuação do Machine Learning em tempo real pode ser executado em clusters do Edge mais próximos de suas ativações e aplicativos.
- **Hub:** O alfa atual está executando o serviço de pontuação Aprendizado de máquina em tempo real no Adobe Experience Platform Hub enquanto a Experience Edge Network está em desenvolvimento.
- **Nó:** Um nó é a unidade fundamental da qual os gráficos são formados. Cada nó executa uma tarefa específica e eles podem ser encadeados juntos usando links para formar um gráfico que representa um pipeline ML. A tarefa executada por um nó representa uma operação em dados de entrada, como uma transformação de dados ou schema, ou uma inferência de aprendizado de máquina. O nó gera o valor transformado ou inferido para os próximos nós.

## Conjuntos de dados no Adobe Experience Platform

Para start usando o aprendizado de máquina em tempo real, é necessário ter acesso a um conjunto de dados. Você tem a opção de usar um conjunto de dados externo e carregá-lo no seu [!DNL JupyterLab] ambiente ou criar um novo conjunto de dados na Plataforma, se ainda não tiver feito isso.

>[!NOTE]
>
>Se você já tiver um conjunto de dados que deseja usar, pule para as [Próximas etapas](#next-steps).

### Usar um conjunto de dados externo

Para saber mais sobre como usar um conjunto de dados externo, como carregar dados para seu [!DNL JupyterLab] ambiente, visite o tutorial sobre como [analisar seus dados usando notebooks](../jupyterlab/analyze-your-data.md#external-data).

### Criar um novo conjunto de dados

Para criar um novo conjunto de dados para uso em Aprendizagem de máquina em tempo real, é necessário um schema de dados para o conjunto de dados. Em seguida, é necessário assimilar dados usando o schema criado. Use os seguintes tutoriais para criar e preencher um conjunto de dados para [!DNL Platform]:

- [Criar e preencher um conjunto de dados na API](../../catalog/datasets/create.md)
- [Criar e preencher um conjunto de dados na interface do usuário](../../ingestion/tutorials/ingest-batch-data.md)

## Próximas etapas {#next-steps}

Depois de preparar seus dados para Aprendizagem de máquina em tempo real, siga o guia [do usuário do notebook Aprendizagem de máquina em tempo](./rtml-authoring-notebook.md) real para aprender a criar e carregar um modelo ONNX na loja de modelos Aprendizagem de máquina em tempo real.

