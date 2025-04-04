---
keywords: Experience Platform;guia do desenvolvedor;Data Science Workspace;tópicos populares;Aprendizado de máquina em tempo real;
solution: Experience Platform
title: Introdução ao Aprendizado de máquina em tempo real
description: O documento a seguir descreve as etapas necessárias para criar um modelo de Aprendizado de máquina em tempo real no Adobe Experience Platform.
exl-id: 90a1c580-f6e7-4517-aa1e-da5092fbc4a2
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 0%

---

# Introdução ao Real-time Machine Learning (Alpha)

>[!NOTE]
>
>O Data Science Workspace não está mais disponível para compra.
>
>Esta documentação destina-se aos clientes existentes com direitos anteriores ao Data Science Workspace.

>[!IMPORTANT]
>
>O Aprendizado de máquina em tempo real ainda não está disponível para todos os usuários. Esse recurso está em alfa e ainda está sendo testado. Este documento está sujeito a alterações.

Para utilizar o Aprendizado de Máquina em Tempo Real, você precisa ter acesso a uma organização provisionada com o Adobe Experience Platform e o [!DNL Data Science Workspace]. Além disso, é necessário ter um conjunto de dados completo para usar em treinamento e pontuação.

Os guias para o Aprendizado de Máquina em Tempo Real exigem uma compreensão funcional do Python 3, [Jupyter Notebooks](../jupyterlab/overview.md), ciência de dados e aprendizado de máquina.

**Termos principais:**

- **DSL:** Idioma Específico do Domínio.
- **Edge:** o serviço de pontuação do Real-time Machine Learning pode ser executado em clusters Edge mais próximos das suas ativações e aplicativos.
- **Hub:** o alfa atual está executando o serviço de pontuação do Aprendizado de Máquina em Tempo Real no Hub do Adobe Experience Platform enquanto a Edge Network está em desenvolvimento.
- **Nó:** Um Nó é a unidade fundamental da qual os gráficos são formados. Cada nó executa uma tarefa específica e eles podem ser encadeados usando links para formar um gráfico que representa um pipeline de ML. A tarefa executada por um nó representa uma operação nos dados de entrada, como uma transformação de dados ou esquema, ou uma inferência de aprendizado de máquina. O nó gera o valor transformado ou inferido para o(s) próximo(s) nó(s).

## Conjuntos de dados na Adobe Experience Platform

Para começar a usar o Aprendizado de máquina em tempo real, você deve ter acesso a um conjunto de dados. Você tem a opção de usar um conjunto de dados externo e carregá-lo no ambiente [!DNL JupyterLab] ou criar um novo conjunto de dados no Experience Platform, se ainda não tiver feito isso.

>[!NOTE]
>
>Se você já tiver um conjunto de dados que deseja usar, pule para [Próximas etapas](#next-steps).

### Usar um conjunto de dados externo

Para saber mais sobre como usar um conjunto de dados externo, como carregar dados para o ambiente [!DNL JupyterLab], visite o tutorial em [análise de dados usando blocos de anotações](../jupyterlab/analyze-your-data.md#external-data).

### Criar um novo conjunto de dados

Para criar um novo conjunto de dados para usar no Aprendizado de máquina em tempo real, você precisa de um esquema de dados para seu conjunto de dados. Em seguida, é necessário assimilar dados usando o esquema criado. Use os seguintes tutoriais para criar e preencher um conjunto de dados para [!DNL Experience Platform]:

- [Criar e preencher um conjunto de dados na API](../../catalog/datasets/create.md)
- [Criar e preencher um conjunto de dados na interface do](../../ingestion/tutorials/ingest-batch-data.md)

## Próximas etapas {#next-steps}

Depois de preparar seus dados para o Aprendizado de Máquina em Tempo Real, comece seguindo o [guia do usuário do bloco de anotações do Aprendizado de Máquina em Tempo Real](./rtml-authoring-notebook.md) para saber como criar e carregar um modelo ONX para a loja de modelos do Aprendizado de Máquina em Tempo Real.
