---
keywords: Experience Platform;dados da web da luma;Data Science Workspace;tópicos populares;receitas;dados de demonstração;dados da web de demonstração;dados da luma
solution: Experience Platform
title: Criar os esquemas e conjuntos de dados da Web do Luma
type: Tutorial
description: Este tutorial fornece os pré-requisitos e os ativos necessários para o modelo de propensão de demonstração do Luma.
exl-id: a791e532-1116-4407-b745-fd6c2ac0d8f7
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 0%

---

# Criar os esquemas e conjuntos de dados do modelo de propensão Luma

>[!NOTE]
>
>O Data Science Workspace não está mais disponível para compra.
>
>Esta documentação destina-se aos clientes existentes com direitos anteriores ao Data Science Workspace.

Este tutorial fornece os pré-requisitos e os ativos necessários para todos os outros tutoriais do [!DNL Adobe Experience Platform] [!DNL Data Science Workspace]. Uma vez concluídos, os seguintes esquemas e conjuntos de dados estarão disponíveis para você e sua organização.

**Esquemas:**

- Esquema de dados da Web do Luma
- Esquema de resultados de pontuação do modelo de propensão

**Conjuntos de dados:**

- Conjunto de dados da Web Luma
- Conjunto de dados de treinamento do modelo de propensão
- Conjunto de dados de pontuação do modelo de propensão
- Conjunto de dados de resultados da pontuação do modelo de propensão

## Baixar os ativos {#assets}

O tutorial a seguir usa um modelo personalizado de propensão de compra da Luma. Antes de continuar, [baixe os ativos necessários](https://experienceleague.adobe.com/docs/platform-learn/assets/DSW-course-sample-assets.zip) e a pasta zip. Esta pasta contém:

- O bloco de anotações do modelo de propensão de compra
- Um notebook usado para assimilar dados em um conjunto de dados de treinamento e pontuação (um subconjunto dos dados da Web do Luma)
- Um arquivo JSON de demonstração contendo os dados da Web de 730.000 usuários do Luma
- Um notebook Python 3 EDA (análise exploratória de dados) opcional que pode ser usado para ajudar a entender os dados e o modelo da Web.

>[!NOTE]
>
> Você pode usar seu próprio esquema e dados para qualquer um dos tutoriais do. No entanto, o modelo de demonstração fornecido nos ativos não funciona a menos que ele forneça os arquivos de configuração e o arquivo de requisitos adequados. Esse modelo de propensão de demonstração foi projetado para funcionar com dados da Web do Luma.

### Crie o esquema de dados da Web Luma e assimile os dados

Para criar um modelo, você deve ter um conjunto de dados no Experience Platform que é usado para treinar e pontuar seu modelo. O tutorial em vídeo a seguir do [curso do Data Science Workspace](https://experienceleague.adobe.com/?lang=pt-br&recommended=ExperiencePlatform-U-1-2021.1.dsw&lang=pt-BR) orienta você na criação do esquema Luma e na assimilação dos dados usados pelo modelo de propensão de compra.

>[!VIDEO](https://video.tv.adobe.com/v/3447159?captions=por_br)

### Criar os conjuntos de dados de resultados de treinamento, pontuação e pontuação

Para executar o bloco de anotações do construtor de fórmula ou usar a API para treinar e pontuar um modelo, é necessário especificar os conjuntos de dados e esquemas usados para treinamento/pontuação. O tutorial de vídeo a seguir orienta você na configuração dos conjuntos de dados de resultados de treinamento, pontuação e pontuação, bem como do esquema de resultados de pontuação usado no modelo de propensão de compra da Luma.

>[!VIDEO](https://video.tv.adobe.com/v/3447426?captions=por_br)

## Próximas etapas

Ao seguir este tutorial, você criou os esquemas e conjuntos de dados necessários para o modelo de propensão Luma com sucesso. Agora você está pronto para prosseguir para o próximo tutorial e criar o modelo usando o [tutorial de bloco de anotações do construtor de fórmula](../jupyterlab/create-a-model.md).

Além disso, você pode explorar os dados usando o bloco de anotações de Análise de Dados Exploratórios (EDA) fornecido. Esse bloco de notas pode ser usado para ajudar a entender os padrões nos dados do Luma, verificar a integridade dos dados e resumir os dados relevantes para o modelo de propensão preditiva. Para saber mais sobre a Análise de Dados Exploratórios, visite a [documentação da EDA](../jupyterlab/eda-notebook.md).
