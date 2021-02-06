---
keywords: Experience Platform;home;popular topics;conexão de fluxo;criar conexão de fluxo;uguide;tutorial;criar uma conexão de fluxo;ingestão de fluxo;;home;popular topics;streaming connection;create streaming connection;ui guide;tutorial;create a streaming connection;streaming ingestion;ingestion;ingestão;
solution: Experience Platform
title: Criar uma conexão de transmissão usando a interface do usuário
topic: tutorial
type: Tutorial
description: Este guia de interface de usuário o ajudará a criar uma conexão de streaming usando o Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 089a4d517476b614521d1db4718966e3ebb13064
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 0%

---


# Criar uma conexão de streaming usando a interface do usuário

Este guia de interface de usuário o ajudará a criar uma conexão de streaming usando o Adobe Experience Platform.

## Introdução

Para que os dados de streaming sejam start para [!DNL Experience Platform], primeiro crie uma conexão HTTP de streaming. Ao criar uma conexão de streaming, você precisa fornecer detalhes importantes, como a fonte de dados de streaming, e se pretende enviar dados de uma fonte confiável (autenticada) ou não confiável (não autenticada).

Depois de registrar uma conexão de streaming, você terá um URL exclusivo que pode ser usado para transmitir dados para [!DNL Platform].

Observe que para concluir este guia, você precisará acessar a Adobe Experience Platform. Se você não tiver acesso a [!DNL Platform], entre em contato com o administrador do sistema antes de continuar.

## Criar uma conexão de streaming

Depois de fazer logon na interface do usuário [!DNL Experience Platform], clique em **[!UICONTROL Fontes]** para abrir a guia **[!UICONTROL Catálogo]**. Esta página exibe os tipos de origem disponíveis como cartões individuais, com cada cartão contendo uma bolha que exibe o número de fluxos de dados que foram criados de conexões de fluxo contínuo para conjuntos de dados.

![](../images/streaming-ingestion/ui/click-sources.png)

Na página **[!UICONTROL Origens]**, clique em **[!UICONTROL API HTTP]** e, em seguida, em **[!UICONTROL Origem do Connect]**.

![](../images/streaming-ingestion/ui/click-connect-source.png)

A tela **[!UICONTROL Conectar-se a HTTP]** é exibida. Em **[!UICONTROL Detalhes do serviço]**, forneça o nome e uma descrição para a nova conexão de streaming.

Em **[!UICONTROL Autenticação de conta]**, selecione as seguintes propriedades de configuração para a sua conexão de streaming:

- **[!UICONTROL Autenticação]:** se a conexão de streaming requer autenticação. A autenticação garante que os dados sejam coletados de fontes confiáveis. É recomendável que isso seja ativado ao lidar com informações pessoais identificáveis (PII).
- **[!UICONTROL Compatibilidade] do Schema XDM:** se essa conexão de streaming enviará ou não eventos compatíveis com schemas XDM. Por padrão, essa propriedade é ativada **em**.

Depois de terminar de selecionar suas propriedades de configuração, clique em **[!UICONTROL Connect]**. Sua conexão HTTP de streaming agora é criada e agora pode ser visualizada na guia **[!UICONTROL Procurar]** na área de trabalho **[!UICONTROL Origens]**.

![](../images/streaming-ingestion/ui/http-sources-details.png)

Na guia **[!UICONTROL Procurar]**, você pode clicar em sua conexão HTTP de fluxo recém-criada e visualização os detalhes dessa conexão.

![](../images/streaming-ingestion/ui/browse-sources.png)

Ao clicar no hiperlink do nome da conexão, você pode selecionar os dados a serem exibidos configurando qual conjunto de dados está conectado, clicando em **[!UICONTROL Selecionar dados]**.

![](../images/streaming-ingestion/ui/select-data.png)

Você pode [criar um novo conjunto de dados](#create-a-new-dataset) ou [usar um conjunto de dados existente](#use-an-existing-dataset).

### Criar um novo conjunto de dados

Para criar um novo conjunto de dados, forneça o nome, a descrição e o schema do público alvo para o conjunto de dados.

![](../images/streaming-ingestion/ui/create-new-dataset.png)

Ao inserir todos os detalhes e clicar em **[!UICONTROL Próximo]**, você pode revisar os detalhes fornecidos antes de clicar em **[!UICONTROL Concluir]** para conectar o conjunto de dados à sua conexão HTTP de streaming.

![](../images/streaming-ingestion/ui/review-create-new-dataset.png)

### Usar um conjunto de dados existente

Para usar um conjunto de dados existente, selecione **[!UICONTROL Nome do conjunto de dados de saída]**.

![](../images/streaming-ingestion/ui/use-existing-dataset.png)

Depois de clicar em **[!UICONTROL Próximo]**, você pode revisar os detalhes antes de clicar em **[!UICONTROL Concluir]** para conectar o conjunto de dados selecionado à sua conexão HTTP de streaming.

![](../images/streaming-ingestion/ui/review-existing-dataset.png)

## Próximas etapas

Ao seguir este tutorial, você criou uma conexão HTTP de streaming, permitindo que você use o terminal de streaming para acessar várias APIs [!DNL Data Ingestion]. Para obter instruções para criar uma conexão de streaming na API, leia o tutorial [criação de uma conexão de streaming](../tutorials/create-streaming-connection.md).
