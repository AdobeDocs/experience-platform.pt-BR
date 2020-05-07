---
keywords: Experience Platform;developer guide;Data Science Workspace;popular topics;Real time machine learning;
solution: Experience Platform
title: Visão geral de aprendizado de máquina em tempo real
topic: Overview
translation-type: tm+mt
source-git-commit: ab8b000bec0ae30c695582f57c40105b7ca1f22f
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 2%

---


# Visão geral de aprendizado de máquina em tempo real

>[!IMPORTANT]
>O aprendizado de máquina em tempo real ainda não está disponível para todos os usuários. Esse recurso está em alfa e ainda está sendo testado. Este documento está sujeito a mudanças.

A estrutura de aprendizado de máquina em tempo real da plataforma Adobe Experience permite que você use o aprendizado de máquina para fornecer as experiências certas aos usuários finais certos no momento certo, nos canais certos, com um intervalo de tempo de subsegundo.

## Benefícios

O aprendizado de máquina em tempo real pode melhorar consideravelmente a relevância do conteúdo de sua experiência digital para seus usuários finais. Isso é possível aproveitando a inferência em tempo real e o aprendizado contínuo no Experience Edge.

Uma combinação de computação contínua no Hub e no Edge reduz drasticamente a latência tradicionalmente envolvida na potencialização de experiências hiper-personalizadas relevantes e responsivas. Assim, o aprendizado de máquina em tempo real oferece inferências com uma latência incrivelmente baixa para a tomada de decisões síncrona. Os exemplos incluem a renderização de conteúdo personalizado de página da Web ou a criação de uma oferta ou desconto para reduzir a rotatividade e aumentar as conversões em uma loja da Web.

## Arquitetura de aprendizado de máquina em tempo real

O diagrama a seguir fornece uma visão geral da arquitetura de aprendizado de máquina em tempo real.

![Visão geral simplificada](../images/rtml/simple-overview.png)

## Fluxo de trabalho de aprendizado de máquina em tempo real (Alpha)

O fluxo de trabalho a seguir descreve as etapas e os resultados típicos envolvidos na criação e utilização de um modelo de aprendizado de máquina em tempo real.

### Inclusão de dados e preparações

Os dados são assimilados e transformados com o Modelo de dados de experiência (XDM) na Adobe Experience Platform. Esses dados são usados para treinamento de modelo. Para saber mais sobre o XDM, visite a visão geral [do](../../xdm/home.md)XDM.

### Criação  

Crie um modelo de aprendizado de máquina em tempo real criando-o do zero ou trazendo-o para um modelo ONNX serializado pré-treinado em notebooks Jupyter da Adobe Experience Platform.

### Implantação

Implante seu modelo no Experience Edge para criar um serviço de aprendizado de máquina em tempo real na Service Gallery usando o endpoint da Predição API.

### Inferência

Use o endpoint da API REST de previsão para gerar insights de aprendizado da máquina em tempo real.

### Delivery

Os profissionais de marketing podem definir segmentos e regras que mapeiam as pontuações de aprendizado de máquina em tempo real para experiências usando o Público alvo da Adobe. Isso permite que os visitantes do site de sua marca sejam exibidos em tempo real, em uma experiência hiper-personalizada de página ou próxima (menos de 100 ms).

## Plano de desenvolvimento

O aprendizado de máquina em tempo real está atualmente na fase alfa. A tabela abaixo descreve alguns dos recursos e atualizações que devem ser lançados na futura iteração beta.

<table>
    <th></th>
    <th>Alpha (maio)</th>
    <th>Beta</th>
    <tr>
        <td>
            <strong>Recursos</strong>
        </td>
        <td>
            <li>A Data Science Workspace traz seu próprio Modelo e autor por meio da integração do iniciador de notebooks.</li>
            <li>Conjunto inicial de operadores de criação.</li>
            <li>Implantar no Hub</li>
            <li>Modelos baseados em aprendizado da Scikit.</li>
        </td>
        <td>
            <li>Integração da interface do usuário da Galeria de serviços da Data Science Workspace.</li>
            <li>Enriquecer automaticamente o Perfil do cliente em tempo real com resultados de inferência.</li>
            <li>Modelos de aprendizado profundo.</li>
            <li>Conjunto ampliado de operadores de criação, incluindo operadores personalizados.</li>
        </td>
    </tr>
    <tr>
        <td>
            <strong>Disponibilidade</strong>
        </td>
        <td>
            América do Norte
        </td>
        <td>
            <li>América do Norte</li>
            <li>Europa e Oriente Médio (EMEA)</li>
            <li>Pacífico Asiático (APAC)</li>
        </td>
    </tr>
    <tr>
        <td>
            <strong>Criação  </strong>
        </td>
        <td>
            <li>Suporte a Python</li>
            <li>SDK de aprendizado de máquina em tempo real</li>
            <li>Nó de criação Python: Pandas, ScikitLearn, ONNXNode, Split, ModelUpload, OneHotEncoder.</li>
        </td>
        <td>
            <li>Suporte a fluxo de tela.</li>
            <li>Outros nós de criação Python: Leitor de Perfil do cliente em tempo real, Gravador de Perfil do cliente em tempo real, Storages numéricos, XDM2Frame, Frame2XDM. </li>
        </td>
    </tr>
    <tr>
        <td>
            <strong>Tempo de execução da pontuação</strong>
        </td>
        <td>
            ONNX
        </td>
        <td>
            ONNX
        </td>
    </tr>
</table>

## Próximas etapas

Você pode começar seguindo o guia de [introdução](./getting-started.md) . Este guia o orienta a configurar todos os pré-requisitos necessários para criar um modelo de aprendizado de máquina em tempo real.

