---
keywords: Experience Platform;guia do desenvolvedor;Data Science Workspace;tópicos populares;Aprendizado de máquina em tempo real;
solution: Experience Platform
title: Introdução ao Aprendizado de máquina em tempo real
description: O documento a seguir descreve as etapas necessárias para criar um modelo de Aprendizado de máquina em tempo real no Adobe Experience Platform.
exl-id: 90a1c580-f6e7-4517-aa1e-da5092fbc4a2
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 0%

---

# Introdução ao Real-time Machine Learning (Alpha)

>[!IMPORTANT]
>
>O Aprendizado de máquina em tempo real ainda não está disponível para todos os usuários. Esse recurso está em alfa e ainda está sendo testado. Este documento está sujeito a alterações.

Para utilizar o Aprendizado de máquina em tempo real, é necessário ter acesso a uma organização provisionada com o Adobe Experience Platform e [!DNL Data Science Workspace]. Além disso, é necessário ter um conjunto de dados completo para usar em treinamento e pontuação.

Os guias para o Aprendizado de Máquina em Tempo Real exigem uma compreensão funcional do Python 3, [Jupyter Notebooks](../jupyterlab/overview.md), ciência de dados e aprendizado de máquina.

**Termos principais:**

- **DSL:** Idioma específico do domínio.
- **Borda:** O serviço de pontuação do Real-time Machine Learning pode ser executado em clusters de borda mais próximos às suas ativações e aplicativos.
- **Hub:** O alfa atual é executar o serviço de pontuação do Real-time Machine Learning no Hub da Adobe Experience Platform enquanto a Experience Edge Network está em desenvolvimento.
- **Nó:** Um Nó é a unidade fundamental da qual os gráficos são formados. Cada nó executa uma tarefa específica e eles podem ser encadeados usando links para formar um gráfico que representa um pipeline de ML. A tarefa executada por um nó representa uma operação nos dados de entrada, como uma transformação de dados ou esquema, ou uma inferência de aprendizado de máquina. O nó gera o valor transformado ou inferido para o(s) próximo(s) nó(s).

## Conjuntos de dados na Adobe Experience Platform

Para começar a usar o Aprendizado de máquina em tempo real, você deve ter acesso a um conjunto de dados. Você tem a opção de usar um conjunto de dados externo e carregá-lo no seu [!DNL JupyterLab] ou criar um novo conjunto de dados na Platform, se ainda não tiver feito.

>[!NOTE]
>
>Se você já tiver um conjunto de dados que deseja usar, pule para [Próximas etapas](#next-steps).

### Usar um conjunto de dados externo

Para saber mais sobre como usar um conjunto de dados externo, como carregar dados para o seu [!DNL JupyterLab] , visite o tutorial em [analisar seus dados usando blocos de anotações](../jupyterlab/analyze-your-data.md#external-data).

### Criar um novo conjunto de dados

Para criar um novo conjunto de dados para usar no Aprendizado de máquina em tempo real, você precisa de um esquema de dados para seu conjunto de dados. Em seguida, é necessário assimilar dados usando o esquema criado. Use os seguintes tutoriais para criar e preencher um conjunto de dados do [!DNL Platform]:

- [Criar e preencher um conjunto de dados na API](../../catalog/datasets/create.md)
- [Criar e preencher um conjunto de dados na interface do](../../ingestion/tutorials/ingest-batch-data.md)

## Próximas etapas {#next-steps}

Depois de preparar seus dados para o Aprendizado de máquina em tempo real, comece seguindo o [Guia do usuário do notebook Real-time Machine Learning](./rtml-authoring-notebook.md) para saber como criar e fazer upload de um modelo ONX para a loja de modelos de Aprendizado de máquina em tempo real.
