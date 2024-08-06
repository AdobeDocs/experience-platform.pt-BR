---
keywords: Experience Platform;dados da web da luma;Data Science Workspace;tópicos populares;receitas;dados de demonstração;dados da web de demonstração;dados da luma
solution: Experience Platform
title: Criar os esquemas e conjuntos de dados da Web do Luma
type: Tutorial
description: Este tutorial fornece os pré-requisitos e os ativos necessários para o modelo de propensão de demonstração do Luma.
exl-id: a791e532-1116-4407-b745-fd6c2ac0d8f7
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 0%

---

# Criar os esquemas e conjuntos de dados do modelo de propensão Luma

>[!NOTE]
>
>O Área de trabalho de ciência de dados não está mais disponível para compra.
>
>Esta documentação destina-se a clientes existentes com direitos anteriores à Data Science Área de trabalho.

Esta tutorial fornece os pré-requisitos e ativos necessários para todos os outros [!DNL Adobe Experience Platform] [!DNL Data Science Workspace] tutoriais. Após a conclusão, os seguintes esquemas e conjuntos de dados estarão disponíveis para você e para sua organização.

**Esquemas:**

- schema de dados luma da Web
- Resultados da pontuação do modelo de propensão schema

**Conjuntos de dados:**

- Conjunto de dados da Web Luma
- Conjunto de dados de treinamento do modelo de propensão
- Pontuação do modelo de propensão conjunto de dados
- Resultados da pontuação do modelo de propensão conjunto de dados

## Baixe o ativos {#assets}

A tutorial a seguir usa um modelo personalizado de propensão de compra Luma. Antes de continuar, [baixar a pasta ativos](https://experienceleague.adobe.com/docs/platform-learn/assets/DSW-course-sample-assets.zip) zip necessária. Esta pasta contém:

- O notebook de modelo de propensão de compra
- Um notebook usado para assimilar dados a uma treinamento e pontuação conjunto de dados (um subconjunto dos dados da Web Luma)
- Um arquivo JSON de demonstração contendo os dados da Web de 730.000 usuários Luma
- Um notebook Python 3 EDA (análise exploratória de dados) opcional que pode ser usado para ajudar a entender os dados e o modelo da Web.

>[!NOTE]
>
> Você pode usar seu próprio esquema e dados para qualquer um dos tutoriais do. No entanto, o modelo de demonstração fornecido nos ativos não funciona a menos que ele forneça os arquivos de configuração e o arquivo de requisitos adequados. Esse modelo de propensão de demonstração foi projetado para funcionar com dados da Web do Luma.

### Criar os dados da Web Luma schema e assimilar os dados

Em solicitar para criar um modelo, você deve ter uma conjunto de dados em Platform que é usada para treinar e marcar seu modelo. O vídeo a seguir tutorial do [curso](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-U-1-2021.1.dsw&amp;lang=pt-BR) de Ciência de Dados Área de trabalho o conduz pela criação do schema Luma e pela ingestão dos dados usados pelo modelo de propensão de compra.

>[!VIDEO](https://video.tv.adobe.com/v/333312)

### Criar os conjuntos de dados treinamento, pontuação e pontuação de resultados

Em solicitar para executar o notebook fórmula construtor ou usar a API para treinar e marcar um modelo, você precisa especificar as conjunto de dados(s) e schema(s) usadas para treinamento/pontuação. O vídeo a seguir tutorial o orienta pela configuração de conjuntos de dados de treinamento, pontuação e pontuação de resultados, bem como os resultados de pontuação schema usados no modelo de propensão de compra do Luma.

>[!VIDEO](https://video.tv.adobe.com/v/333426)

## Próximas etapas

Ao seguir esse tutorial, você criou com sucesso os schemas e conjuntos de dados necessários para o modelo de propensão luma. Agora você está pronto para continuar para o próximo tutorial e criar o modelo usando o [notebook](../jupyterlab/create-a-model.md) fórmula construtor tutorial.

Além disso, você pode explorar os dados usando o bloco de anotações de Análise de Dados Exploratórios (EDA) fornecido. Esse bloco de notas pode ser usado para ajudar a entender os padrões nos dados do Luma, verificar a integridade dos dados e resumir os dados relevantes para o modelo de propensão preditiva. Para saber mais sobre a Análise de Dados Exploratórios, visite a [documentação da EDA](../jupyterlab/eda-notebook.md).
