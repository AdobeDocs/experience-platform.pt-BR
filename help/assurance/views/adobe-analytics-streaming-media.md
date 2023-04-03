---
title: Exibição do Adobe Analytics para mídia de streaming no Assurance
description: Este guia explica como usar o Adobe Analytics para mídia de streaming com o Adobe Experience Platform Assurance.
source-git-commit: 07dc01c11c79ac2dad05d89309cabb5715c0b63c
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 1%

---


# Exibição do Adobe Analytics para mídia de streaming no Assurance

Com a integração entre o Adobe Analytics para mídia de streaming e o Adobe Experience Platform Assurance, agora é possível validar a implementação do Media Analytics no aplicativo móvel. As exibições do Media Analytics exibem o que é rastreado na sessão de mídia, como:

- Evento de início de sessão que contém todas as propriedades de conteúdo principal, metadados padrão e metadados personalizados, bem como eventos de término de sessão e de conclusão de sessão.
- Eventos Ad Break Start e Ad Start com todas as propriedades do anúncio anexadas, bem como Eventos Skip e Complete para ambos.
- Início do capítulo com todas as propriedades anexadas, bem como os eventos Capítulo ignorado e Capítulo concluído .
- Todos os eventos de alteração de reprodução (reproduzir, pausar, buffer, erros, alteração da taxa de bits).
- Todos os eventos de rastreamento de alterações do estado do player (início, fim).

Quando os dados são processados no Analytics, o status pós-processados e os dados, como o tempo gasto da mídia e a duração total da pausa, também estão disponíveis na visualização detalhada do evento.

## Introdução

Antes de continuar, verifique se você tem os seguintes serviços:

- O [Interface do usuário da coleta de dados do Adobe Experience Platform](https://experience.adobe.com/#/data-collection/)
- [Adobe Experience Platform Assurance](https://experience.adobe.com/assurance)

Para saber como instalar o Assurance no seu aplicativo, leia o [guia de controle de execução](../tutorials/implement-assurance.md).

## Usar o Assurance com a Adobe Analytics para mídia de streaming

Depois de se conectar e configurar seu aplicativo para Adobe Analytics, você estará pronto para configurá-lo para o Streaming Media Analytics. Na parte inferior do painel esquerdo, selecione **[!UICONTROL Configurar]** para adicionar a exibição Eventos do Media Analytics e **Salvar** sim.

![Configurar](./images/adobe-analytics-streaming-media/configure.png)

Depois de adicionado, selecione o **[!UICONTROL Eventos do Media Analytics]** no **[!UICONTROL Adobe Analytics]** para validar o rastreamento de sessão.

![Selecionar](./images/adobe-analytics-streaming-media/select.png)

No **[!UICONTROL Eventos do Media Analytics]** , você pode pesquisar e filtrar por ID de sessão (VSID) para visualizar uma sessão de mídia específica. Para exibir detalhes adicionais do evento, selecione um evento específico.

![Eventos de mídia](./images/adobe-analytics-streaming-media/media-events.png)

Para obter uma exibição mais sucinta das chamadas de API, também é possível ocultar os eventos de atualização do indicador de reprodução selecionando o **[!UICONTROL Ocultar eventos de atualização do indicador de reprodução]** filtro.

![Ocultar indicador de reprodução](./images/adobe-analytics-streaming-media/hide-playhead.png)

>[!INFO]
>
>A visualização de dados de análise de mídia pós-processada requer o uso das versões do SDK: Android Media 2.1.2 e iOS AEPMedia 3.0.1 (ou superior)

Para exibir dados pós-processados, localize o evento de início da sessão e valide na coluna de status em que a sessão foi concluída. Se concluído, clique no evento para exibir um resumo da sessão de mídia na exibição de detalhes do evento. Para obter mais detalhes, role para baixo até encontrar os detalhes pós-processados.

![Exibição pós-processada](./images/adobe-analytics-streaming-media/post-processed-view.png)
