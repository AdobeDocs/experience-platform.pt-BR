---
title: Tipo de Dados da Coleção de Detalhes da Sessão
description: Saiba mais sobre o tipo de dados Modelo de dados de experiência (XDM) da Coleção de detalhes da sessão.
exl-id: ffe6bcf7-61e1-4f7a-ba95-7fcb78683cc9
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '926'
ht-degree: 15%

---

# [!UICONTROL Detalhes da sessão] Tipo de dados da coleção

A Coleção [!UICONTROL Detalhes da sessão] é um tipo de dados padrão do Experience Data Model (XDM) que rastreia dados relacionados às sessões de reprodução de mídia. Os campos de coleção de mídia são usados para capturar dados enviados para outros serviços da Adobe para processamento adicional. Esse esquema engloba uma grande variedade de propriedades que podem ser usadas para fornecer insights sobre o comportamento do usuário e os padrões de consumo de conteúdo. Use o tipo de dados Coleção [!UICONTROL Detalhes da sessão] para capturar o engajamento do usuário registrando eventos de reprodução, interações de anúncios, marcadores de progresso, pausas e outras métricas.

+++Selecione para exibir um diagrama do tipo de dados Coleção de detalhes da sessão.
![Um diagrama do tipo de dados da Coleção de Detalhes da Sessão.](../images/data-types/session-details-collection.png)
+++

>[!NOTE]
>
>Cada nome de exibição contém um link para informações adicionais sobre os parâmetros de áudio e vídeo. As páginas vinculadas contêm detalhes sobre os dados de anúncios de vídeo coletados pelo Adobe, valores de implementação, parâmetros de rede, relatórios e considerações importantes.

| Nome de exibição | Propriedade | Tipo de dados | Obrigatório | Descrição |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------|-----------|----------|---------------------------------------------------------------------------------------|
| [!UICONTROL Tipo de carregamento do anúncio] | `adLoad` | String | Não | O tipo de anúncio carregado conforme definido pela representação interna de cada cliente. |
| [[!UICONTROL Álbum]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#album) | `album` | String | Não | O nome do álbum ao qual pertence a gravação de música ou vídeo. |
| [[!UICONTROL Artista]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#artist) | `artist` | String | Não | O nome do artista do álbum ou grupo que grava a música ou o vídeo. |
| [[!UICONTROL ID do ativo]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#asset-id) | `assetID` | String | Não | A [!UICONTROL ID do Ativo] é o identificador exclusivo de conteúdo do ativo de mídia, como o identificador de episódio da série de TV, o identificador de ativo do filme ou o identificador de evento em tempo real. Normalmente, essas IDs são derivadas de autoridades de metadados, como EIDR, TMS/Gracenote ou Rovi. Esses identificadores também podem ser de outros sistemas proprietários ou internos. |
| [[!UICONTROL Autor]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#author) | `author` | String | Não | O nome do autor da mídia. |
| [[!UICONTROL Tipo de Conteúdo de Difusão]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-type) | `contentType` | String | Sim | O [!UICONTROL Tipo de Conteúdo de Difusão] da entrega de fluxo. Os valores disponíveis por [!UICONTROL Tipo de Fluxo] incluem:<br>Áudio: &quot;song&quot;, &quot;podcast&quot;, &quot;audiobook&quot; e &quot;radio&quot;;<br>Vídeo: &quot;VoD&quot;, &quot;Live&quot;, &quot;Linear&quot;, &quot;UGC&quot; e &quot;DVoD&quot;.<br>Os clientes podem fornecer valores personalizados para este parâmetro. |
| [[!UICONTROL Rede de Difusão]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#network) | `network` | String | Não | O nome da rede/canal. |
| [[!UICONTROL Canal de conteúdo]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-channel) | `channel` | String | Sim | O [!UICONTROL Canal de Conteúdo] é o canal de distribuição de onde o conteúdo foi reproduzido. |
| [[!UICONTROL Conclusões de conteúdo]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-complete) | `isCompleted` | Booleano | Não | [!UICONTROL Conclusões de conteúdo] indica se um ativo de mídia cronometrado foi observado até a conclusão. Esse evento não significa necessariamente que o espectador assistiu ao vídeo inteiro; o espectador poderia ter pulado para frente. |
| [!UICONTROL Rede de Entrega de Conteúdo] | `cdn` | String | Não | A [!UICONTROL Rede de Entrega de Conteúdo] do conteúdo reproduzido. |
| [[!UICONTROL ID de conteúdo]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-id) | `name` | sequência de caracteres | Sim | A [!UICONTROL ID de Conteúdo] é um identificador exclusivo do conteúdo. Ela pode ser usada para vincular a outro setor ou IDs de CMS. |
| [[!UICONTROL Nome do conteúdo]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-name-(variable)) | `friendlyName` | String | Não | O [!UICONTROL Nome do Conteúdo] é o nome &quot;amigável&quot; (legível) do conteúdo. |
| [[!UICONTROL Nome do reprodutor de conteúdo]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-player-name) | `playerName` | String | Sim | O nome do reprodutor de conteúdo. |
| [[!UICONTROL Nome do criador]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#originator) | `originator` | String | Não | O nome do criador do conteúdo. |
| [[!UICONTROL Parte do dia]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#day-part) | `dayPart` | String | Não | Uma propriedade que define a hora do dia em que o conteúdo foi transmitido ou reproduzido. Isso pode ter qualquer valor definido, conforme necessário pelos clientes |
| [[!UICONTROL Número do episódio]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#episode) | `episode` | String | Não | O número do episódio. |
| [[!UICONTROL Tipo de Feed]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#media-feed-type) | `feed` | String | Não | O tipo de feed, que pode representar dados reais relacionados ao feed, como EAST HD ou SD, ou a fonte do feed, como um URL. |
| [[!UICONTROL Primeira Transmissão]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#first-air-date) | `firstAirDate` | String | Não | A data em que o conteúdo foi exibido na televisão pela primeira vez. Qualquer formato de data é aceitável, mas o Adobe recomenda: DD/MM/AAAA. |
| [[!UICONTROL Primeira data digital]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#first-digital-date) | `firstDigitalDate` | String | Não | A data quando o conteúdo foi exibido em qualquer canal ou plataforma digital pela primeira vez. Qualquer formato de data é aceitável, mas o Adobe recomenda: DD/MM/AAAA. |
| [[!UICONTROL Gênero]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#genre) | `genre` | String | Não | O tipo ou agrupamento de conteúdo conforme definido pelo produtor do conteúdo. Os valores devem ser delimitados por vírgulas na implementação da variável. |
| [[!UICONTROL Mídia Autorizada]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#authorized) | `authorized` | String | Não | Confirma se o usuário foi autorizado por meio da autenticação Adobe. |
| [[!UICONTROL Duração do Conteúdo de Mídia]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-length-(variable)) | `length` | Número inteiro | Sim | O [!UICONTROL Comprimento do Conteúdo de Mídia] contém o comprimento/tempo de execução do clipe. Esse é o comprimento máximo (ou duração) do conteúdo que está sendo consumido (em segundos). |
| [[!UICONTROL Inícios da mídia]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#media-starts) | `isViewed` | Booleano | Não | O evento de carregamento da mídia. Isso ocorre quando o visualizador seleciona o botão Reproduzir. Isso conta mesmo se houver anúncios antes da exibição, buffering, erros, etc. |
| [[!UICONTROL Identificador MVPD]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#mvpd) | `mvpd` | String | Não | O identificador do Distribuidor de programação de vídeo multicanal (MVPD) fornecido pela autenticação de Adobe. |
| [[!UICONTROL Publicador]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#publisher) | `publisher` | String | Não | O nome do publicador do conteúdo de áudio. |
| [[!UICONTROL Estação de rádio]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#station) | `station` | String | Não | O nome da estação de rádio na qual o áudio é reproduzido. |
| [[!UICONTROL Valor de Classificação]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-rating) | `rating` | String | Não | A classificação conforme definido pelas Diretrizes de controle parental da TV. |
| [[!UICONTROL Rótulo do Registro]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#label) | `label` | String | Não | O nome da gravadora. |
| [[!UICONTROL Retomar]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-resumes) | `hasResume` | Booleano | Não | Marca cada reprodução que foi retomada após mais de 30 minutos de buffer, pausa ou período de paralisação. |
| [[!UICONTROL Número da temporada]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#season) | `season` | String | Não | O [!UICONTROL Número da Temporada] ao qual o programa pertence. Séries da temporada são necessárias somente se o programa for parte de uma série. |
| [[!UICONTROL Nome da Série]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#show) | `show` | String | Não | O Nome Do Programa/Série. O Nome do programa é necessário somente se o programa for parte de uma série. |
| [[!UICONTROL Mostrar tipo]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#show-type) | `showType` | String | Não | O tipo de conteúdo. Por exemplo, um trailer ou um episódio completo. O tipo de conteúdo é expresso como um número inteiro entre 0 e 3. Por exemplo, &quot;0&quot; = Episódio completo; &quot;1&quot; = Pré-visualização/Trailer; &quot;2&quot; = Clipe; &quot;3&quot; = Outros. |
| [[!UICONTROL Formato de fluxo]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#stream-format) | `streamFormat` | String | Não | O formato do fluxo (HD, SD). |
| [[!UICONTROL Tipo de fluxo]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#stream-type) | `streamType` | String | Não | O tipo de fluxo de mídia. |
| [[!UICONTROL Versão]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#sdk-version) | `appVersion` | String | Não | A versão do SDK usada pelo reprodutor. Isso pode ter qualquer valor personalizado que faça sentido para o reprodutor. |

{style="table-layout:auto"}

<!-- This is required for sessionStart. 
Q) How do I indicate that?
Q) Do you know where to link for:
Ad Load Type
Content Delivery Network
 -->
