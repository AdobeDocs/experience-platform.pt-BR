---
keywords: Experience Platform, dados da Web luma, Data Science Workspace, tópicos populares, receitas, dados de demonstração, dados da Web de demonstração, dados do luma
solution: Experience Platform
title: Criar os esquemas e conjuntos de dados da Web Luma
topic-legacy: tutorial
type: Tutorial
description: Este tutorial fornece os pré-requisitos e os ativos necessários para o modelo de propensão de demonstração Luma.
exl-id: a791e532-1116-4407-b745-fd6c2ac0d8f7
source-git-commit: f57ca64c34f569f4402cb998af72e1e9022510ca
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 1%

---

# Criar os esquemas e conjuntos de dados do modelo de propensão do Luma

Este tutorial fornece os pré-requisitos e os ativos necessários para todos os outros [!DNL Adobe Experience Platform] [!DNL Data Science Workspace] tutoriais. Após a conclusão, os esquemas e conjuntos de dados a seguir estarão disponíveis para você e sua organização IMS.

**Esquemas:**

- Schema de dados da Web Luma
- Schema de resultados de pontuação do modelo de propensão

**Conjuntos de dados:**

- Conjunto de dados da Web Luma
- Conjunto de dados de treinamento do modelo de propensão
- Conjunto de dados de pontuação do modelo de propensão
- Conjunto de dados de resultados de pontuação do modelo de propensão

## Baixar os ativos {#assets}

O tutorial a seguir usa um modelo personalizado de propensão de compra de Luma. Antes de continuar, [baixar os ativos necessários](https://experienceleague.adobe.com/docs/platform-learn/assets/DSW-course-sample-assets.zip?lang=en) pasta zip. Esta pasta contém:

- O notebook modelo de propensão de compra
- Um notebook usado para assimilar dados para um conjunto de dados de treinamento e pontuação (um subconjunto dos dados da Web Luma)
- Um arquivo JSON de demonstração com os dados da Web de 730.000 usuários do Luma
- Um notebook Python 3 EDA (análise de dados exploratórios) opcional que pode ser usado para ajudar a entender os dados e o modelo da Web.

>[!NOTE]
>
> Você pode usar seu próprio esquema e dados para qualquer um dos tutoriais. No entanto, o modelo de demonstração fornecido nos ativos não funciona, a menos que tenha fornecido os arquivos de configuração e o arquivo de requisitos adequados. Este modelo de propensão de demonstração foi projetado para funcionar com dados da Web Luma.

### Crie o schema de dados da Web Luma e assimile os dados

Para criar um modelo, você deve ter um conjunto de dados na Platform que é usado para treinar e pontuar seu modelo. O seguinte tutorial em vídeo do [Curso da Data Science Workspace](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-U-1-2021.1.dsw) O orienta a criar o schema Luma e assimilar os dados usados pelo modelo de propensão de compra.

>[!VIDEO](https://video.tv.adobe.com/v/333312)

### Criar conjuntos de dados de treinamento, pontuação e resultados de pontuação

Para executar o notebook do construtor de receitas ou usar a API para treinar e pontuar um modelo, é necessário especificar os conjuntos de dados e os esquemas usados para treinamento/pontuação. O tutorial em vídeo a seguir orienta você na configuração dos conjuntos de dados de treinamento, pontuação e resultados de pontuação, bem como no esquema de resultados de pontuação usado no modelo de propensão de compra do Luma.

>[!VIDEO](https://video.tv.adobe.com/v/333426)

## Próximas etapas

Ao seguir este tutorial, você criou com sucesso os esquemas e conjuntos de dados necessários para o modelo de propensão do Luma. Agora você está pronto para continuar para o próximo tutorial e criar o modelo usando o [notebook do construtor de receitas](../jupyterlab/create-a-model.md) tutorial.

Além disso, você pode explorar os dados usando o notebook EDA (Exploratory Data Analysis) fornecido. Este notebook pode ser usado para ajudar a entender os padrões nos dados do Luma, verificar a integridade dos dados e resumir os dados relevantes do modelo de propensão preditiva. Para saber mais sobre a Análise de dados exploratória, visite o [Documentação EDA](../jupyterlab/eda-notebook.md).
