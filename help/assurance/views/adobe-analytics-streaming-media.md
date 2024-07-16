---
title: Exibição do Adobe Analytics para mídia de streaming no Assurance
description: Este guia explica como usar o Adobe Analytics para mídia de streaming com o Adobe Experience Platform Assurance.
exl-id: 9a9c2c64-e9ed-4d58-b936-d802f1c3b7d3
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 100%

---

# Exibição do Adobe Analytics para mídia de streaming no Assurance

Devido a integração do Adobe Analytics para mídia de streaming com o Adobe Experience Platform Assurance, agora é possível validar a implementação do Media Analytics no aplicativo móvel. As exibições do Media Analytics mostram o que é rastreado na sessão de mídia, como:

- Evento de início de sessão que inclui todo o conteúdo principal, os metadados padrão e as propriedades de metadados personalizadas, bem como eventos de fim de sessão e de conclusão de sessão.
- Eventos de Início do intervalo de anúncio e de Início do anúncio com todas as propriedades de anúncio anexadas, bem como os eventos Ignorar e Concluir para ambos.
- Início do capítulo com todas as propriedades anexadas, bem como os eventos Ignorar capítulo e Concluir capítulo.
- Todos os eventos de alteração de reprodução (reproduzir, pausar, buffer, erros, alteração da taxa de bits).
- Todos os eventos de rastreamento de mudança de estado do reprodutor (início, fim).

Quando os dados são processados no Analytics, o status e os dados de pós-processamento, como o tempo gasto com a mídia e a duração total da pausa, também ficam disponíveis na exibição detalhada do evento.

## Introdução

Antes de continuar, verifique se você tem os seguintes serviços:

- A [Interface da coleção de dados da Adobe Experience Platform](https://experience.adobe.com/#/data-collection/)
- [Adobe Experience Platform Assurance](https://experience.adobe.com/assurance)

Para saber como instalar o Assurance em seu aplicativo, leia o [guia de implementação do Assurance](../tutorials/implement-assurance.md).

## Use o Assurance com o Adobe Analytics para mídia de streaming

Depois de conectar e configurar o seu aplicativo para o Adobe Analytics, você estará pronto para configurá-lo no Analytics para mídia de streaming. Na parte inferior do painel esquerdo, selecione **[!UICONTROL Configurar]** para adicionar a exibição Eventos do Media Analytics e clique em **Salvar**.

![Configurar](./images/adobe-analytics-streaming-media/configure.png)

Depois de adicionada, selecione a exibição **[!UICONTROL Eventos do Media Analytics]** na seção **[!UICONTROL Adobe Analytics]** para validar o rastreamento da sessão.

![Selecionar](./images/adobe-analytics-streaming-media/select.png)

Na exibição **[!UICONTROL Eventos do Media Analytics]**, você pode pesquisar e filtrar por ID de sessão (VSID) para visualizar uma sessão de mídia específica. Para exibir detalhes adicionais do evento, selecione um evento específico.

![Eventos de mídia](./images/adobe-analytics-streaming-media/media-events.png)

Para obter uma visão mais precisa das chamadas de API, também é possível ocultar os eventos de atualização do indicador de reprodução, selecionando o filtro **[!UICONTROL Ocultar eventos de atualização do indicador de reprodução]**.

![Ocultar indicador de reprodução](./images/adobe-analytics-streaming-media/hide-playhead.png)

>[!INFO]
>
>A exibição de dados de pós-processamento do Media Analytics requer o uso das seguintes versões de SDK: Android Media 2.1.2 e iOS AEPMedia 3.0.1 (ou superior)

Para exibir dados de pós-processamento, localize o evento de início da sessão e valide a conclusão da sessão na coluna de status. Se ela estiver concluída, clique no evento para exibir um resumo da sessão de mídia na exibição detalhada do evento. Para obter mais detalhes, role para baixo para encontrar os detalhes de pós-processamento.

![Exibição de pós-processamento](./images/adobe-analytics-streaming-media/post-processed-view.png)
