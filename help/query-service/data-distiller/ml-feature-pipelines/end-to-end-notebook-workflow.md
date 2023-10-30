---
title: Fluxo de trabalho completo de Enriquecimento do pipeline de dados de IA/ML
description: Use blocos de anotações do ambiente de aprendizado de máquina baseados em nuvem para criar um treinamento e pontuar um modelo de propensão que preveja conversões de assinatura dos dados do Adobe Experience Platform.
hide: true
hidefromtoc: true
exl-id: 2853e7c7-cab8-4e1b-b73f-622c937fbbaf
source-git-commit: 308d07cf0c3b4096ca934a9008a13bf425dc30b6
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 0%

---

<!-- 
title: Cloud Machine Learning Environment Notebooks
Cloud machine learning environment notebooks
Old title: 
# AI/ML data pipeline enrichment end-to-end workflow
-->

# Fluxo de trabalho completo de enriquecimento do pipeline de dados de IA/ML

Use o Data Distiller para enriquecer seus pipelines de aprendizado de máquina com dados de experiência do cliente de alto valor que foram coletados e preparados no Adobe Experience Platform.

Este documento fornece uma série de blocos de anotações do ambiente de aprendizado de máquina baseados em nuvem que demonstram um fluxo de trabalho completo. O fluxo de trabalho usa suas ferramentas preferidas de aprendizado de máquina para criar modelos de dados personalizados que oferecem suporte aos casos de uso de marketing com dados de Experience Platform.

Este workflow requer o uso de [!DNL Python] blocos de anotações em seus ambientes de aprendizado de máquina. Instruções para começar a usar esses [!DNL Python] os blocos de anotações são incluídos nos respectivos arquivos readme.

Antes de continuar com este guia, siga as etapas descritas no [Visão geral dos pipelines de recursos de IA/ML](./overview.md) para habilitar o uso dos notebooks Python de amostra usados neste caso de uso do pipeline de recurso de IA/ML.

## Blocos de ambiente de aprendizado de máquina na nuvem {#cmle-notebooks}

O fluxo de trabalho completo pode ser dividido em três fases amplas com base nos serviços usados para implementar o fluxo de trabalho.

- A exploração e preparação iniciais dos dados da plataforma dependem dos serviços da plataforma.
- O treinamento e a pontuação do modelo usam ferramentas no ambiente de aprendizado de máquina baseado em nuvem. As opções comuns para plataformas de ML incluem: Databricks ML, AWS Sagemaker, DataRobot e assim por diante.
- Assimilar pontuações de volta na Platform e qualquer criação e ativação de público-alvo com base em código com base nessas pontuações dependeria novamente dos serviços da Platform.

No entanto, todas essas fases podem ser executadas em um ou mais blocos de anotações do seu ambiente de ML sem que o usuário precise alternar contextos entre o Platform e suas ferramentas de ML baseadas em nuvem.

As etapas típicas desse fluxo de ponta a ponta foram divididas em um conjunto de notebooks modulares que, considerados em conjunto, demonstram as etapas envolvidas em um projeto típico de aprendizado de máquina envolvendo dados da plataforma. Isso facilita o uso dos notebooks como referência para a implementação de atividades específicas, bem como a seleção e adaptação do código dos notebooks relevantes para implementar um caso de uso real. Na prática, um cientista de dados pode preparar um único notebook que implementa o pipeline completo para seu projeto de ML. Como alternativa, um cientista de dados pode simplesmente adaptar o código de amostra para consultar dados da Platform e disponibilizá-lo em seu ambiente de ML antes de continuar o projeto usando recursos baseados em interface do usuário em sua plataforma de ML.

Os blocos de anotações de amostra incluídos no repositório vinculado são descritos resumidamente abaixo. A documentação detalhada de cada bloco de anotações é intercalada com o código nos próprios blocos de anotações.

<!-- Below is the meat - the how to (but without links or details) -->

### Gerar dados sintéticos {#generate-synthetic-data}

Este bloco de notas fornece código para gerar conjuntos de dados de perfis sintéticos e Eventos de experiência na sua plataforma que serão usados para ilustrar o fluxo de trabalho CMLE.

### EDA e caracterização com o serviço de consulta {#eda-and-featurization-with-query-service}

Este bloco de anotações inclui exemplos de análise exploratória em conjuntos de dados da Platform usando consultas interativas pelo Serviço de consulta da Platform. Eles são seguidos com exemplos de consultas de recursos para criar um conjunto de dados de treinamento para o modelo de propensão de exemplo.

### Exportar dados de treinamento {#export-training-data}

Este bloco de anotações ilustra a exportação do conjunto de dados de treinamento para o armazenamento na nuvem que pode ser lido pelas suas ferramentas de aprendizado de máquina.

### Treinar um modelo de propensão {#train-a-propensity-model}

Este notebook ilustra o treinamento de um modelo de propensão. Ele presume que o Databricks ML seja seu ambiente de ML, mas é escrito genericamente (ou seja, sem o uso intensivo de recursos/APIs específicos do Databricks) para que possa ser adaptado a outras plataformas.

### Pontuar o modelo de propensão

Este notebook ilustra a pontuação do modelo de propensão treinado para produzir um conjunto de dados de pontuações de propensão para cada perfil de cliente da plataforma.

### Assimilar pontuações na AEP

Este breve notebook ilustra a assimilação do conjunto de dados de pontuações de propensão para enriquecer os perfis do cliente na AEP.

### Criar e ativar públicos-alvo do código

Este bloco de anotações ilustra como o usuário pode criar públicos-alvo a partir das pontuações e ativá-los por meio de aplicativos da Platform de seu código de bloco de anotações.
