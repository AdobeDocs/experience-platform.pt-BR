---
title: Adobe Analytics para mídia de streaming View in Assurance
description: Este guia explica como usar o Adobe Analytics para mídia de streaming com o Adobe Experience Platform Assurance.
exl-id: 9a9c2c64-e9ed-4d58-b936-d802f1c3b7d3
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 2%

---

# Visualização do Adobe Analytics para mídia de streaming no Assurance

Com a integração entre o Adobe Analytics para mídia de streaming e o Adobe Experience Platform Assurance, agora é possível validar a implementação do Media Analytics no aplicativo móvel. As exibições do Media Analytics exibem o que é rastreado na sessão de mídia, como:

- Evento de início de sessão que contém todo o conteúdo principal, metadados padrão e propriedades de metadados personalizadas, bem como eventos de fim de sessão e de conclusão de sessão.
- Eventos de início de ad break e de início de anúncio com todas as propriedades de anúncio anexadas, bem como eventos Ignorar e Concluir para ambos.
- Início do capítulo com todas as propriedades anexadas, bem como eventos de Ignorar capítulo e Concluir capítulo.
- Todos os eventos de alteração de reprodução (reprodução, pausa, buffer, erros, alteração da taxa de bits).
- Todos os eventos de monitoramento de alterações no estado do player (início, fim).

Quando os dados são processados no Analytics, o status e os dados pós-processados, como tempo de mídia gasto e duração total da pausa, também ficam disponíveis na exibição de detalhes do evento.

## Introdução

Antes de continuar, verifique se você tem os seguintes serviços:

- A variável [Interface da coleção de dados do Adobe Experience Platform](https://experience.adobe.com/#/data-collection/)
- [Adobe Experience Platform Assurance](https://experience.adobe.com/assurance)

Para saber como instalar o Assurance em seu aplicativo, leia o [guia de implementação do Assurance](../tutorials/implement-assurance.md).

## Use o Assurance com o Adobe Analytics para mídia de streaming

Depois de se conectar e configurar seu aplicativo para Adobe Analytics, você estará pronto para configurá-lo para Análise de mídia de transmissão. Na parte inferior do painel esquerdo, selecione **[!UICONTROL Configurar]** para adicionar a exibição Eventos do Media Analytics e **Salvar** o mesmo.

![Configurar](./images/adobe-analytics-streaming-media/configure.png)

Depois de adicionado, selecione o **[!UICONTROL Eventos do Media Analytics]** exibir no **[!UICONTROL Adobe Analytics]** para validar o rastreamento da sessão.

![Selecionar](./images/adobe-analytics-streaming-media/select.png)

No **[!UICONTROL Eventos do Media Analytics]** Para visualizar uma sessão de mídia específica, pesquise e filtre por ID de sessão (VSID). Para exibir detalhes adicionais do evento, selecione um evento específico.

![Eventos de mídia](./images/adobe-analytics-streaming-media/media-events.png)

Para obter uma visão mais sucinta das chamadas de API, também é possível ocultar os eventos de atualização do indicador de reprodução selecionando o **[!UICONTROL Ocultar eventos de atualização do indicador de reprodução]** filtro.

![Ocultar indicador de reprodução](./images/adobe-analytics-streaming-media/hide-playhead.png)

>[!INFO]
>
>A exibição de dados de análise de mídia pós-processados requer o uso de versões do SDK: Android Media 2.1.2 e iOS AEPMedia 3.0.1 (ou superior)

Para exibir dados pós-processados, localize o evento de início da sessão e valide na coluna de status se a sessão foi concluída. Se concluído, clique no evento para exibir um resumo da sessão de mídia na exibição detalhada do evento. Para obter mais detalhes, role para baixo para encontrar os detalhes pós-processados.

![Exibição pós-processada](./images/adobe-analytics-streaming-media/post-processed-view.png)
