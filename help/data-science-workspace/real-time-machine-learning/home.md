---
keywords: Experience Platform; guia do desenvolvedor; Área de trabalho de ciência de dados; tópicos populares; Aprendizado de máquina em tempo real;
solution: Experience Platform
title: Visão geral de aprendizado de máquina em tempo real
description: A aprendizagem de máquina em tempo real pode aumentar drasticamente a relevância dos seus experiência conteúdo digitais para seus usuários finais. Isso é possibilitado utilizando a inferência e o aprendizado contínuo em tempo real na Experience Platform Edge Network.
exl-id: 23eb1877-1bdf-4982-b58c-cfb58467035a
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 1%

---

# Visão geral de aprendizado de máquina em tempo real (Alpha)

>[!NOTE]
>
>O Área de trabalho de ciência de dados não está mais disponível para compra.
>
>Esta documentação destina-se a clientes existentes com direitos anteriores à Data Science Área de trabalho.

>[!IMPORTANT]
>
>O Machine Learning em tempo real ainda não está disponível para todos os usuários. Esse recurso está na alfa e ainda está sendo testado. Esta documento está sujeita a mudanças.

A aprendizagem de máquina em tempo real pode aumentar drasticamente a relevância dos seus experiência conteúdo digitais para seus usuários finais. Isso é possibilitado ao aproveitar a inferência em tempo real e o aprendizado contínuo sobre o [!DNL Experience Platform Edge Network].

Uma combinação de computação perfeita no Hub e [!DNL Edge] reduz drasticamente a latência que está tradicionalmente envolvida na alimentação de experiências hiper-personalizadas que são relevantes e responsivo. Portanto, o Machine Learning em tempo real fornece inferências com latência incrivelmente baixa para a tomada de decisões síncrona. Os exemplos incluem a renderização de página conteúdo web personalizadas ou o acesso a uma oferta ou desconto para reduzir churn e aumentar as conversões em uma loja na web.

## Arquitetura de aprendizado de máquina em tempo real {#architecture}

Os diagramas a seguir fornecem uma visão geral da arquitetura de aprendizado de máquina em tempo real. Atualmente, o alpha tem uma versão mais simplificada.

![alfa-arco](../images/rtml/alpha-arch.png)

![Visão geral simplificada](../images/rtml/end-to-end-arch.png)

## fluxo de Trabalho de aprendizado de máquina em tempo real

A fluxo de Trabalho a seguir descreve as etapas típicas e os resultados envolvidos na criação e utilização de um modelo de Aprendizagem de máquina em tempo real.

### Ingestão e preparações de dados

Os dados são assimilados e transformados com o [!DNL Experience Data Model] (XDM) na Adobe Experience Platform. Esses dados são usados para modelos de treinamento. Para saber mais sobre o XDM, visita a visão geral](../../xdm/home.md) do [XDM.

### Criação

Criar um modelo de Aprendizagem de Máquina em Tempo Real, criando-o do zero ou trazendo-o como um modelo ONNX serializado pré-treinado em Adobe Experience Platform Notebooks Jupyter.

### Implantação

Implante seu modelo para [!DNL Edge Network] criar um serviço de aprendizagem de máquina em tempo real na [!UICONTROL Galeria] de serviços usando o endpoint da API de previsão.

### Inferência

Use o endpoint da API Forecast REST para gerar insights de aprendizado de máquina em tempo real.

### Entrega

Os profissionais de marketing podem definir segmentos e regras que mapeiam as pontuações de Aprendizagem de máquina em tempo real para experiências usando Adobe Target. Isso permite que os visitantes do site da sua marca sejam mostrados da mesma página hiper-personalizadas experiência em tempo real.

## Funcionalidade atuais

O Machine Learning em tempo real está atualmente na alfa. A funcionalidade descrita abaixo está sujeita à mudança à medida que mais recursos e nós são disponibilizados.

>[!NOTE]
>
> Limitações alfa:
> - Atualmente, somente modelos baseados em ONNX são suportados.
> - As funções usadas em nós não podem ser serializadas. Por exemplo, uma função lambda usada em um nó Pandas.
> - Há uma suspensão de 20 segundos após a implantação de [!DNL Edge] ser feita manualmente.
> - Para o deep learning, seus dados precisam ser enviados de forma que, quando `df.values` for chamado, retornem uma matriz que seja aceitável pelo seu modelo DL. Isso ocorre porque o modelo ONNX de pontuação nó usa `df.values` e envia a saída para pontuação em relação ao modelo.


### Características:

| | Alfa (maio) |
| --- | --- |
| **Recursos** | - Uso do notebook modelo, autor, teste e implantar de um modelo personalizado de aprendizado de máquina. <br> - Suporte para importação de modelos de aprendizado de máquina pré-treinados. <br> - SDK de aprendizado de máquina em tempo real. <br> - Conjunto inicial de nós de criação. <br> - Implantado no Adobe Experience Platform Hub. |
| **Disponibilidade** | América do Norte |
| **Criação de nós** | - Pandas <br> - ScikitLearn <br> - ONNXNode <br> - Split <br> - ModelUpload <br> - OneHotEncoder |
| **Pontuação de tempos de execução** | ONNX |

## Próximas etapas

Você pode começar seguindo o guia de [introdução](./getting-started.md). Este guia o conduz pela configuração de todos os pré-requisitos necessários para a criação de um modelo de Aprendizagem de máquina em tempo real.
