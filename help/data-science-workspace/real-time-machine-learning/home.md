---
keywords: Experience Platform;developer guide;Data Science Workspace;popular topics;Real time machine learning;
solution: Experience Platform
title: Visão geral de aprendizado de máquina em tempo real
topic: Overview
description: O aprendizado de máquina em tempo real pode melhorar consideravelmente a relevância do conteúdo de sua experiência digital para seus usuários finais. Isso é possível aproveitando a inferência em tempo real e o aprendizado contínuo no Experience Edge.
translation-type: tm+mt
source-git-commit: 9ba229195892245d29fb4f17b9f2e5cd6c6ea567
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 1%

---


# Visão geral de aprendizado de máquina em tempo real (Alpha)

>[!IMPORTANT]
>
>O aprendizado de máquina em tempo real ainda não está disponível para todos os usuários. Esse recurso está em alfa e ainda está sendo testado. Este documento está sujeito a mudanças.

O aprendizado de máquina em tempo real pode melhorar consideravelmente a relevância do conteúdo de sua experiência digital para seus usuários finais. Isso é possível aproveitando a inferência em tempo real e o aprendizado contínuo no [!DNL Experience Edge].

Uma combinação de computação ininterrupta no Hub e no Hub reduz [!DNL Edge] drasticamente a latência tradicionalmente envolvida na potencialização de experiências hiper-personalizadas relevantes e responsivas. Assim, o aprendizado de máquina em tempo real oferece inferências com uma latência incrivelmente baixa para a tomada de decisões síncrona. Os exemplos incluem a renderização de conteúdo personalizado de página da Web ou a criação de uma oferta ou desconto para reduzir a rotatividade e aumentar as conversões em uma loja da Web.

## Arquitetura de aprendizado de máquina em tempo real {#architecture}

Os diagramas a seguir fornecem uma visão geral da arquitetura de aprendizado de máquina em tempo real. Atualmente, o alfa tem uma versão mais simplificada.

![arco alfa](../images/rtml/alpha-arch.png)

![Visão geral simplificada](../images/rtml/end-to-end-arch.png)

## Fluxo de trabalho de aprendizado de máquina em tempo real

O fluxo de trabalho a seguir descreve as etapas e os resultados típicos envolvidos na criação e utilização de um modelo de aprendizado de máquina em tempo real.

### Inclusão de dados e preparações

Os dados são assimilados e transformados com o [!DNL Experience Data Model] (XDM) no Adobe Experience Platform. Esses dados são usados para treinamento de modelo. Para saber mais sobre o XDM, visite a visão geral [do](../../xdm/home.md)XDM.

### Criação  

Crie um modelo de aprendizado de máquina em tempo real criando-o do zero ou trazendo-o para um modelo ONNX serializado pré-treinado em notebooks Adobe Experience Platform Jupyter.

### Implantação

Implante seu modelo para [!DNL Experience Edge] criar um serviço de Aprendizagem de máquina em tempo real na Galeria [!UICONTROL de] serviços usando o endpoint da API de previsão.

### Inferência

Use o endpoint da API REST de previsão para gerar insights de aprendizado da máquina em tempo real.

### Delivery

Os profissionais de marketing podem definir segmentos e regras que mapeiam as pontuações de aprendizado de máquina em tempo real para experiências usando o Adobe Target. Isso permite que visitantes do site de sua marca sejam mostrados como uma experiência hiper-personalizada da mesma página ou da próxima em tempo real.

## Funcionalidade atual

O aprendizado de máquina em tempo real está atualmente em alfa. A funcionalidade descrita abaixo está sujeita a alterações à medida que mais recursos e nós são disponibilizados.

>[!NOTE]
>
> Limitações de alfa:
> - Atualmente, somente modelos baseados em ONNX são suportados.
> - As funções usadas em nós não podem ser serializadas. Por exemplo, uma função lambda usada em um nó Pandas.
> - Há 20 segundos de espera após a [!DNL Edge] implantação ser feita manualmente.
> - Para um aprendizado profundo, seus dados precisam ser enviados de tal forma que, quando `df.values` são chamados, retorne um array aceitável pelo modelo DL. Isso ocorre porque o nó de pontuação do modelo ONNX usa `df.values` e envia a saída para a pontuação em relação ao modelo.



### Recursos:

|  | Alpha (maio) |
| --- | --- |
| **Recursos** | - Usando o modelo de notebook RTML, crie, teste e implante um modelo de aprendizado de máquina personalizado. <br> - Apoio à importação de modelos pré-treinados de aprendizagem automática. <br> - SDK de aprendizado de máquina em tempo real. <br> - Conjunto inicial de nós de criação. <br> - Implantado no Adobe Experience Platform Hub. |
| **Disponibilidade** | América do Norte |
| **Nós de criação** | - Pandas <br> - ScikitLearn <br> - ONNXNode <br> - Dividir <br> - ModelUpload <br> - OneHotEncoder |
| **Tempo de execução da pontuação** | ONNX |

## Próximas etapas

Você pode começar seguindo o guia de [introdução](./getting-started.md) . Este guia o orienta a configurar todos os pré-requisitos necessários para criar um modelo de aprendizado de máquina em tempo real.

