---
title: Enviar evento de mídia
description: Envie dados de mídia para o Adobe Experience Platform Edge Network.
source-git-commit: 639d3d3d8bfb51e6c97066aee61271d0b00ec455
workflow-type: tm+mt
source-wordcount: '828'
ht-degree: 0%

---

# Enviar evento de mídia

A ação **[!UICONTROL Send media event]** envia um evento de mídia para uma sequência de dados, que pode ser usada por aplicativos e serviços como Adobe Experience Platform ou Adobe Analytics. Essa ação é útil quando você rastreia o conteúdo de streaming de mídia na propriedade.

![Imagem da interface do usuário do Experience Platform mostrando a tela de evento de envio de mídia.](../assets/send-media-event.png)

As opções disponíveis dependem do **[!UICONTROL Media event type]** que você selecionar. Todos os tipos de evento de mídia exigem um **[!UICONTROL Player ID]**, que é o Nome do reprodutor de conteúdo.

Alguns tipos de evento oferecem a capacidade de configurar outros campos. Se um tipo de evento de mídia não estiver listado aqui, o único campo disponível será [!UICONTROL Player ID]. Os seguintes tipos de evento de mídia incluem outros campos:

## [!UICONTROL Ad break start]

Permite configurar os detalhes do pod de publicidade.

* **[!UICONTROL Ad break name]**: o nome amigável do ad break.
* **[!UICONTROL Ad break offset (seconds)]**: O deslocamento do ad break no conteúdo, em segundos.
* **[!UICONTROL Ad break index]**: O índice do ad break dentro do conteúdo, começando em 1.

## [!UICONTROL Ad start]

Permite configurar detalhes de publicidade.

* **[!UICONTROL Ad name]**: o nome amigável do anúncio.
* **[!UICONTROL Ad ID]**: A ID do anúncio. Qualquer valor alfanumérico é suportado.
* **[!UICONTROL Ad length (seconds)]**: A duração do anúncio de vídeo, em segundos.
* **[!UICONTROL Advertiser]**: a empresa ou marca cujo produto está em destaque no anúncio.
* **[!UICONTROL Campaign ID]**: A ID da campanha publicitária.
* **[!UICONTROL Creative ID]**: A ID do criativo do anúncio.
* **[!UICONTROL Creative URL]**: A URL da campanha criativa.
* **[!UICONTROL Placement ID]**: a ID de posicionamento do anúncio.
* **[!UICONTROL Site ID]**: A ID do site do anúncio.
* **[!UICONTROL Pod position]**: o índice do anúncio dentro do ad break pai, começando em 0.

Esse tipo de evento também oferece suporte à capacidade de fornecer metadados personalizados como parte da carga útil do evento de mídia.

## [!UICONTROL Bitrate change]

* **[!UICONTROL Quality of experience data]**: Um objeto [Qualidade de Experiência](/help/xdm/data-types/qoe-data-details-collection.md) que especifica a taxa de bits, os quadros ignorados, os quadros por segundo e a hora de início.

## [!UICONTROL Chapter start]

Permite configurar detalhes do capítulo.

* **[!UICONTROL Chapter name]**: O nome do capítulo ou segmento.
* **[!UICONTROL Chapter length]**: O comprimento do capítulo, em segundos.
* **[!UICONTROL Chapter index]**: A posição do capítulo dentro do conteúdo.
* **[!UICONTROL Chapter offset]**: O deslocamento do capítulo desde o início do conteúdo, em segundos.

Esse tipo de evento também oferece suporte à capacidade de fornecer metadados personalizados como parte da carga útil do evento de mídia.

## [!UICONTROL Error]

Permite configurar detalhes do erro.

* **[!UICONTROL Error name]**: O nome do erro.
* **[!UICONTROL Source]**: A origem do erro.

## [!UICONTROL Session start]

Permite configurar os detalhes da sessão de mídia.

* **[!UICONTROL Handle media session automatically]**: uma caixa de seleção que permite que o Web SDK envie os pings necessários automaticamente. Você pode desmarcar essa caixa se quiser enviar pings manualmente.
* **[!UICONTROL Playhead]**: O indicador de reprodução, em segundos.
* **[!UICONTROL Content type]**: O tipo de conteúdo. Qualquer valor de string é compatível; o Adobe também oferece as seguintes predefinições:
   * [!UICONTROL Audiobook]
   * [!UICONTROL Downloaded video-on-demand]
   * [!UICONTROL Linear playback of the media asset]
   * [!UICONTROL Live streaming]
   * [!UICONTROL Podcast]
   * [!UICONTROL Radio show]
   * [!UICONTROL Song]
   * [!UICONTROL User-generated content]
   * [!UICONTROL Video-on-demand]
* **[!UICONTROL Clip length/runtime (seconds)]**: a duração máxima do conteúdo que está sendo consumido, em segundos. Para mídia ao vivo com duração desconhecida, o valor de `86400` é o padrão.
* **[!UICONTROL Content ID]**: A ID do conteúdo.
* **[!UICONTROL Ad load type]**: o tipo de anúncio carregado. Os dois valores a seguir são suportados:
   * [!UICONTROL Ads same as TV]
   * [!UICONTROL Other (custom/dynamic ads)]
* **[!UICONTROL Album]**: O álbum ao qual a música pertence.
* **[!UICONTROL Artist]**: O artista da música.
* **[!UICONTROL Asset ID]**: o identificador exclusivo do conteúdo do ativo de mídia. Normalmente, essas IDs são derivadas de autoridades de metadados, como EIDR, TMS/Gracenote ou Rovi. Esses identificadores também podem ser de outros sistemas proprietários ou internos.
* **[!UICONTROL Author]**: O nome do autor do audiobook.
* **[!UICONTROL Authorized]**: Um sinalizador que determina se o usuário está conectado por meio da autenticação Adobe.
* **[!UICONTROL Day part]**: A hora do dia em que o conteúdo foi transmitido ou reproduzido. Qualquer valor de string é suportado.
* **[!UICONTROL Episode]**: O número do episódio.
* **[!UICONTROL Feed type]**: O tipo de feed.
* **[!UICONTROL First air date]**: a data quando o conteúdo foi exibido na televisão pela primeira vez. Qualquer valor de cadeia de caracteres é suportado; no entanto, a Adobe recomenda o uso do formato `YYYY-MM-DD`.
* **[!UICONTROL First digital date]**: a data quando o conteúdo foi exibido em qualquer canal ou plataforma digital pela primeira vez. Qualquer valor de cadeia de caracteres é suportado; no entanto, a Adobe recomenda o uso do formato `YYYY-MM-DD`.
* **[!UICONTROL Content name]**: O nome amigável do conteúdo.
* **[!UICONTROL Genre]**: o tipo ou agrupamento de conteúdo definido pelo produtor do conteúdo. Este campo aceita vários valores, delimitados por vírgula.
* **[!UICONTROL Label]**: O nome do rótulo do registro.
* **[!UICONTROL Rating]**: A classificação conforme definida pelas Diretrizes de controle parental da TV.
* **[!UICONTROL MVPD]**: O MVPD conforme fornecido pela autenticação Adobe.
* **[!UICONTROL Network]**: O nome da rede ou do canal.
* **[!UICONTROL Originator]**: O criador do conteúdo.
* **[!UICONTROL Publisher]**: O publicador do conteúdo de áudio.
* **[!UICONTROL Season]**: Se o programa for parte de uma série, o número da temporada do programa.
* **[!UICONTROL Show]**: se o programa for parte de uma série, o nome da série.
* **[!UICONTROL Show type]**: O tipo de programa. Qualquer valor de string é compatível; o Adobe também oferece as seguintes predefinições:
   * [!UICONTROL Clip]
   * [!UICONTROL Full episode]
   * [!UICONTROL Other]
   * [!UICONTROL Preview/trailer]
* **[!UICONTROL Stream type]**: O tipo de fluxo.
* **[!UICONTROL Stream format]**: o formato do fluxo, como HD ou SD.
* **[!UICONTROL Station]**: O nome ou ID da estação de rádio.

Esse tipo de evento também oferece suporte à capacidade de fornecer metadados personalizados como parte da carga útil do evento de mídia. Ela também permite substituições na configuração da sequência de dados, fornecendo controle sobre quais aplicativos e serviços recebem esses dados. Ao definir uma substituição da configuração do fluxo de dados em um comando individual e nas configurações da extensão de tag, o comando individual tem prioridade. Consulte [Substituições da configuração da sequência de dados](../configure/configuration-overrides.md) para obter mais informações.

## [!UICONTROL States update]

Permite configurar detalhes de atualização de estado. Você pode iniciar ou encerrar os seguintes estados:

* [!UICONTROL Closed captioning]
* [!UICONTROL Full screen]
* [!UICONTROL In focus]
* [!UICONTROL Mute]
* [!UICONTROL Picture in picture]

Os seguintes campos estão disponíveis:

* **[!UICONTROL States started]**: Um menu suspenso que permite indicar que um estado foi iniciado. Selecionar o botão **[!UICONTROL Add another state that started]** permite iniciar vários estados na mesma ação.
* **[!UICONTROL States ended]**: Um menu suspenso que permite indicar que um estado terminou. Selecionar o botão **[!UICONTROL Add another state that ended]** permite finalizar vários estados na mesma ação.
