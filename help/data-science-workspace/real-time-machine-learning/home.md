---
keywords: Experience Platform;guia do desenvolvedor;Data Science Workspace;tópicos populares;Aprendizado de máquina em tempo real;
solution: Experience Platform
title: Visão geral do Aprendizado de máquina em tempo real
description: O Aprendizado de máquina em tempo real pode melhorar consideravelmente a relevância do seu conteúdo de experiência digital para os seus usuários finais. Isso é possível aproveitando a inferência em tempo real e o aprendizado contínuo no Experience Platform Edge Network.
exl-id: 23eb1877-1bdf-4982-b58c-cfb58467035a
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 1%

---

# Visão geral do Aprendizado de máquina em tempo real (Alpha)

>[!NOTE]
>
>O Data Science Workspace não está mais disponível para compra.
>
>Esta documentação destina-se aos clientes existentes com direitos anteriores ao Data Science Workspace.

>[!IMPORTANT]
>
>O Aprendizado de máquina em tempo real ainda não está disponível para todos os usuários. Esse recurso está em alfa e ainda está sendo testado. Este documento está sujeito a alterações.

O Aprendizado de máquina em tempo real pode melhorar consideravelmente a relevância do seu conteúdo de experiência digital para os seus usuários finais. Isso é possível aproveitando a inferência em tempo real e o aprendizado contínuo no [!DNL Experience Platform Edge Network].

Uma combinação de computação contínua no Hub e no [!DNL Edge] reduz drasticamente a latência tradicionalmente envolvida na geração de experiências hiperpersonalizadas que são relevantes e responsivas. Portanto, o Aprendizado de máquina em tempo real fornece inferências com uma latência incrivelmente baixa para a tomada de decisões síncronas. Os exemplos incluem a renderização de conteúdo personalizado da página da Web ou a exibição de uma oferta ou desconto para reduzir o churn e aumentar as conversões em uma loja da Web.

## Arquitetura do Real-time Machine Learning {#architecture}

Os diagramas a seguir fornecem uma visão geral da arquitetura de aprendizado de máquina em tempo real. Atualmente, o alfa tem uma versão mais simplificada.

![alfa-arco](../images/rtml/alpha-arch.png)

![Visão geral simplificada](../images/rtml/end-to-end-arch.png)

## Fluxo de trabalho do Aprendizado de máquina em tempo real

O fluxo de trabalho a seguir descreve as etapas e os resultados típicos envolvidos na criação e utilização de um modelo de Aprendizado de máquina em tempo real.

### Assimilação e preparações de dados

Os dados são assimilados e transformados com o [!DNL Experience Data Model] (XDM) no Adobe Experience Platform. Esses dados são usados para treinamento de modelo. Para saber mais sobre o XDM, visite a [visão geral do XDM](../../xdm/home.md).

### Criação

Crie um modelo de Aprendizado de máquina em tempo real criando do zero ou trazendo-o como um modelo ONX serializado pré-treinado no Adobe Experience Platform Jupyter Notebooks.

### Implantação

Implante seu modelo no [!DNL Edge Network] para criar um serviço de Aprendizado de Máquina em Tempo Real no [!UICONTROL Service Gallery] usando o ponto de extremidade da API de Previsão.

### Inferência

Use o endpoint da API REST de previsão para gerar insights de aprendizado de máquina em tempo real.

### Entrega

Os profissionais de marketing podem definir segmentos e regras que mapeiam pontuações do Aprendizado de máquina em tempo real para experiências usando o Adobe Target. Isso permite que os visitantes do site da sua marca tenham uma experiência hiperpersonalizada de mesma página ou de próxima página em tempo real.

## Funcionalidade atual

O Aprendizado de Máquina em Tempo Real está atualmente em alfa. A funcionalidade descrita abaixo está sujeita a alterações à medida que mais recursos e nós são disponibilizados.

>[!NOTE]
>
> Limitações do Alpha:
>
> - Atualmente, somente os modelos baseados em ONNX são compatíveis.
> - As funções usadas em nós não podem ser serializadas. Por exemplo, uma função lambda usada em um nó Pandas.
> - Há uma suspensão de 20 segundos após a implantação de [!DNL Edge] ser feita manualmente.
> - Para o deep learning, seus dados precisam ser enviados de forma que, quando `df.values` for chamado, retornem uma matriz que seja aceitável pelo seu modelo DL. Isso ocorre porque o nó de pontuação do modelo ONNX usa `df.values` e envia a saída para pontuação em relação ao modelo.


### Recursos:

| | Alpha (maio) |
| --- | --- |
| **Recursos** | - Uso do modelo de bloco de anotações RTML, crie, teste e implante um modelo de aprendizado de máquina personalizado. <br> - Suporte para importação de modelos de aprendizado de máquina pré-treinados. <br> - SDK do Real-time Machine Learning. <br> - Conjunto inicial de nós de criação. <br> - Implantado no Hub do Adobe Experience Platform. |
| **Disponibilidade** | América do Norte |
| **Nós de Criação** | - Pandas <br> - ScikitLearn <br> - ONNXNode <br> - Divisão <br> - ModelUpload <br> - OneHotEncoder |
| **Tempos de execução de pontuação** | ONNX |

## Próximas etapas

Você pode começar seguindo o guia de [introdução](./getting-started.md). Este guia aborda a configuração de todos os pré-requisitos necessários para criar um modelo de Aprendizado de máquina em tempo real.
