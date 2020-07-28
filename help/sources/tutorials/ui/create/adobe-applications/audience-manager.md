---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Criar um conector de fonte de Adobe Audience Manager na interface do usuário
topic: overview
translation-type: tm+mt
source-git-commit: f09ff4d1b159a6989868c5cfc35b361cfb640a99
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 2%

---


# Criar um conector de fonte de Adobe Audience Manager na interface do usuário

Este tutorial o orienta pelas etapas para criar conectores de origem para o Adobe Audience Manager trazer os dados do Evento da experiência do consumidor para o Platform usando a interface do usuário.

## Criar uma conexão de origem com o Adobe Audience Manager

Faça logon no <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> e selecione **Fontes** na barra de navegação esquerda para acessar a área de trabalho de fontes. A tela *Catálogo* exibe várias fontes com as quais você pode criar conexões de origem e cada fonte mostra o número de conexões existentes associadas a elas.

Na categoria de aplicativos *de* Adobe, selecione **Adobe Audience Manager** para exibir uma barra de informações no lado direito da tela. A barra de informações fornece uma breve descrição para a fonte selecionada, bem como opções para visualização de sua documentação ou para conexão com a fonte.

Para criar um novo conector de origem para Adobe Audience Manager, clique em **Conectar fonte**.

![](../../../../images/tutorials/create/aam/aam_catalog.png)

Uma caixa de diálogo é exibida. Clique em **Conectar** para criar a conexão.

![](../../../../images/tutorials/create/aam/aam_connect_full.png)

Se uma conexão de origem com o Adobe Audience Manager for estabelecida, a página de atividade *de* origem do conector Audience Manager será exibida.

![](../../../../images/tutorials/create/aam/aam_flow.png)

Se desejar pausar os dados de Audience Manager recebidos, você poderá fazer isso clicando na lista de fluxo de dados e alterne seu *Status* da coluna *Propriedades* direita.

![](../../../../images/tutorials/create/aam/aam_flow_disable.png)

## Próximas etapas

Enquanto um fluxo de dados Audience Manager está ativo, os dados recebidos são automaticamente assimilados aos Perfis do cliente em tempo real. Agora você pode utilizar esses dados de entrada e criar segmentos de audiência usando o Platform Segmentation Service. Consulte os seguintes documentos para obter mais detalhes:

- [Visão geral do Perfil do cliente em tempo real](../../../../../profile/home.md)
- [Visão geral do Serviço de segmentação](../../../../../segmentation/home.md)