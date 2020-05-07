---
keywords: Experience Platform;developer guide;Data Science Workspace;popular topics;Real time machine learning;
solution: Experience Platform
title: Introdução ao aprendizado de máquina em tempo real
topic: Getting started
translation-type: tm+mt
source-git-commit: c9e6eb41e51ad17ad11b9a669ca5e4cf6c899f8b
workflow-type: tm+mt
source-wordcount: '350'
ht-degree: 0%

---


# Introdução ao aprendizado de máquina em tempo real

>[!IMPORTANT]
>O aprendizado de máquina em tempo real ainda não está disponível para todos os usuários. Esse recurso está em alfa e ainda está sendo testado. Este documento está sujeito a mudanças.

Para utilizar o aprendizado de máquina em tempo real, é necessário ter acesso a uma organização provisionada com a Adobe Experience Platform e a Data Science Workspace. Além disso, é necessário ter um conjunto de dados na Plataforma.

Os guias para o aprendizado de máquina em tempo real exigem um entendimento prático sobre Python 3, notebooks [de](../jupyterlab/overview.md)Júpiter, ciência de dados e aprendizado de máquina.

## Conjuntos de dados na plataforma Adobe Experience

Para start usando o aprendizado de máquina em tempo real, é necessário ter um conjunto de dados preenchido na plataforma da experiência. Você tem a opção de usar um conjunto de dados externo e carregá-lo no ambiente JupyterLab ou criar um novo conjunto de dados na Plataforma, se ainda não tiver feito isso.

>[!NOTE]
>Se você já tiver um conjunto de dados que deseja usar, ignore as duas etapas a seguir.

### Usar um conjunto de dados externo

Para saber mais sobre o uso de um conjunto de dados externo, como o carregamento de dados para seu ambiente JupyterLab, visite o tutorial sobre como [analisar seus dados usando notebooks](../jupyterlab/analyze-your-data.md#external-data).

### Criar um novo conjunto de dados

Para criar um novo conjunto de dados para uso em Aprendizagem de máquina em tempo real, é necessário um schema de dados para o conjunto de dados. Em seguida, é necessário assimilar dados usando o schema criado. Use os seguintes tutoriais para criar e preencher um conjunto de dados para Plataforma:

- [Criar e preencher um conjunto de dados na API](../../catalog/datasets/create.md)
- [Criar e preencher um conjunto de dados na interface do usuário](../../ingestion/tutorials/ingest-batch-data.md)

## Git e Docker

Se você planeja treinar um modelo usando o fluxo de trabalho da fórmula do Data Science Workplace, Git e Docker são necessários.

>[!NOTE]
>Você não precisa baixar o Git e o Docker se planeja treinar um modelo usando um notebook Python ou se estiver usando seu próprio modelo ONNX.

- [Guia de instalação do Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
- [Guia de instalação do Docker](https://docs.docker.com/get-docker/)

## Próximas etapas

Depois de preparar seus dados para o Aprendizado de máquina em tempo real, siga o tutorial sobre como [treinar um modelo](./training-ml-model.md) para aprender como criar e carregar um modelo ONNX para a loja de modelos de aprendizado de máquina em tempo real.

