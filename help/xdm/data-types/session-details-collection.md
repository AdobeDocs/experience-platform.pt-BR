---
title: Tipo de Dados da Coleção de Detalhes da Sessão
description: Saiba mais sobre o tipo de dados Modelo de dados de experiência (XDM) da Coleção de detalhes da sessão.
exl-id: ffe6bcf7-61e1-4f7a-ba95-7fcb78683cc9
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 9%

---

# [!UICONTROL Session Details] Tipo de dados da coleção

A Coleção [!UICONTROL Session Details] é um tipo de dados padrão do Experience Data Model (XDM) que rastreia dados relacionados às sessões de reprodução de mídia. Os campos de coleção de mídia são usados para capturar dados enviados para outros serviços da Adobe para processamento adicional. Esse esquema engloba uma grande variedade de propriedades que podem ser usadas para fornecer insights sobre o comportamento do usuário e os padrões de consumo de conteúdo. Use o tipo de dados Coleção [!UICONTROL Session Details] para capturar a participação do usuário registrando eventos de reprodução, interações de anúncios, marcadores de progresso, pausas e outras métricas.

+++Selecione para exibir um diagrama do tipo de dados da Coleção de detalhes da sessão.
![Um diagrama do tipo de dados da Coleção de Detalhes da Sessão.](../images/data-types/session-details-collection.png)
+++

>[!NOTE]
>
>Cada nome de exibição contém um link para informações adicionais sobre os parâmetros de áudio e vídeo. As páginas vinculadas contêm detalhes sobre os dados de anúncios de vídeo coletados pelo Adobe, valores de implementação, parâmetros de rede, relatórios e considerações importantes.

| Nome de exibição | Propriedade | Tipo de dados | Obrigatório | Descrição |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------|-----------|----------|---------------------------------------------------------------------------------------|
| [!UICONTROL Ad Load Type] | `adLoad` | String | Não | O tipo de anúncio carregado conforme definido pela representação interna de cada cliente. |
| [[!UICONTROL Album]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=pt-BR#album) | `album` | String | Não | O nome do álbum ao qual pertence a gravação de música ou vídeo. |
| [[!UICONTROL Artist]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=pt-BR#artist) | `artist` | String | Não | O nome do artista do álbum ou grupo que grava a música ou o vídeo. |
| [[!UICONTROL Asset ID]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=pt-BR#asset-id) | `assetID` | String | Não | O [!UICONTROL Asset ID] é o identificador exclusivo de conteúdo do ativo de mídia, como o identificador de episódio da série de TV, o identificador de ativo do filme ou o identificador de evento em tempo real. Normalmente, essas IDs são derivadas de autoridades de metadados, como EIDR, TMS/Gracenote ou Rovi. Esses identificadores também podem ser de outros sistemas proprietários ou internos. |
| [[!UICONTROL Author]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=pt-BR#author) | `author` | String | Não | O nome do autor da mídia. |
| [[!UICONTROL Broadcast Content Type]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=pt-BR#content-type) | `contentType` | String | Sim | O [!UICONTROL Broadcast Content Type] da entrega do fluxo. Os valores disponíveis por [!UICONTROL Stream Type] incluem:<br>Áudio: &quot;song&quot;, &quot;podcast&quot;, &quot;audiobook&quot; e &quot;radio&quot;;<br>Vídeo: &quot;VoD&quot;, &quot;Live&quot;, &quot;Linear&quot;, &quot;UGC&quot; e &quot;DVoD&quot;.<br>Os clientes podem fornecer valores personalizados para este parâmetro. |
| [[!UICONTROL Broadcast Network]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=pt-BR#network) | `network` | String | Não | O nome da rede/canal. |
| [[!UICONTROL Content Channel]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=pt-BR#content-channel) | `channel` | String | Sim | O [!UICONTROL Content Channel] é o canal de distribuição de onde o conteúdo foi reproduzido. |
| [!UICONTROL Content Delivery Network] | `cdn` | String | Não | O [!UICONTROL Content Delivery Network] do conteúdo reproduzido. |
| [[!UICONTROL Content ID]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=pt-BR#content-id) | `name` | sequência de caracteres | Sim | O [!UICONTROL Content ID] é um identificador exclusivo do conteúdo. Ela pode ser usada para vincular a outro setor ou IDs do CMS. |
| [[!UICONTROL Content Name]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=pt-BR#content-name-(variable)) | `friendlyName` | String | Não | O [!UICONTROL Content Name] é o nome &quot;amigável&quot; (legível) do conteúdo. |
| [[!UICONTROL Content Player Name]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=pt-BR#content-player-name) | `playerName` | String | Sim | O nome do reprodutor de conteúdo. |
| [[!UICONTROL Creator Name]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=pt-BR#originator) | `originator` | String | Não | O nome do criador do conteúdo. |
| [[!UICONTROL Day Part]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=pt-BR#day-part) | `dayPart` | String | Não | Uma propriedade que define a hora do dia em que o conteúdo foi transmitido ou reproduzido. Isso pode ter qualquer valor definido, conforme necessário pelos clientes |
| [[!UICONTROL Episode Number]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=pt-BR#episode) | `episode` | String | Não | O número do episódio. |
| [[!UICONTROL Feed Type]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=pt-BR#media-feed-type) | `feed` | String | Não | O tipo de feed, que pode representar dados reais relacionados ao feed, como EAST HD ou SD, ou a fonte do feed, como um URL. |
| [[!UICONTROL First Air Date]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=pt-BR#first-air-date) | `firstAirDate` | String | Não | A data em que o conteúdo foi exibido na televisão pela primeira vez. Qualquer formato de data é aceitável, mas a Adobe recomenda: DD/MM/AAAA. |
| [[!UICONTROL First Digital Date]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=pt-BR#first-digital-date) | `firstDigitalDate` | String | Não | A data quando o conteúdo foi exibido em qualquer canal ou plataforma digital pela primeira vez. Qualquer formato de data é aceitável, mas a Adobe recomenda: DD/MM/AAAA. |
| [[!UICONTROL Genre]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=pt-BR#genre) | `genre` | String | Não | O tipo ou agrupamento de conteúdo conforme definido pelo produtor do conteúdo. Os valores devem ser delimitados por vírgulas na implementação da variável. |
| [[!UICONTROL Media Authorized]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=pt-BR#authorized) | `authorized` | String | Não | Confirma se o usuário foi autorizado por meio da autenticação do Adobe. |
| [[!UICONTROL Media Content Length]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=pt-BR#content-length-(variable)) | `length` | Número inteiro | Sim | O [!UICONTROL Media Content Length] contém o comprimento/tempo de execução do clipe - Esse é o comprimento máximo (ou duração) do conteúdo que está sendo consumido (em segundos). |
| [[!UICONTROL MVPD Identifier]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=pt-BR#mvpd) | `mvpd` | String | Não | O identificador do Distribuidor de programação de vídeo (MVPD) de vários canais que foi fornecido por meio da autenticação do Adobe. |
| [[!UICONTROL Publisher]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=pt-BR#publisher) | `publisher` | String | Não | O nome do publicador do conteúdo de áudio. |
| [[!UICONTROL Radio Station]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=pt-BR#station) | `station` | String | Não | O nome da estação de rádio na qual o áudio é reproduzido. |
| [[!UICONTROL Rating Value]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=pt-BR#content-rating) | `rating` | String | Não | A classificação conforme definido pelas Diretrizes de controle parental da TV. |
| [[!UICONTROL Record Label]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=pt-BR#label) | `label` | String | Não | O nome da gravadora. |
| [[!UICONTROL Resume]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=pt-BR#content-resumes) | `hasResume` | Booleano | Não | Marca cada reprodução que foi retomada após mais de 30 minutos de buffer, pausa ou período de paralisação. |
| [[!UICONTROL Season Number]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=pt-BR#season) | `season` | String | Não | O [!UICONTROL Season Number] ao qual o programa pertence. Séries da temporada são necessárias somente se o programa for parte de uma série. |
| [[!UICONTROL Series Name]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=pt-BR#show) | `show` | String | Não | O Nome Do Programa/Série. O Nome do programa é necessário somente se o programa for parte de uma série. |
| [[!UICONTROL Show Type]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=pt-BR#show-type) | `showType` | String | Não | O tipo de conteúdo. Por exemplo, um trailer ou um episódio completo. O tipo de conteúdo é expresso como um número inteiro entre 0 e 3. Por exemplo, &quot;0&quot; = Episódio completo; &quot;1&quot; = Pré-visualização/Trailer; &quot;2&quot; = Clipe; &quot;3&quot; = Outros. |
| [[!UICONTROL Stream Format]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=pt-BR#stream-format) | `streamFormat` | String | Não | O formato do fluxo (HD, SD). |
| [[!UICONTROL Stream Type]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=pt-BR#stream-type) | `streamType` | String | Não | O tipo de fluxo de mídia. |
| [[!UICONTROL Version]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=pt-BR#sdk-version) | `appVersion` | String | Não | A versão do SDK usada pelo reprodutor. Isso pode ter qualquer valor personalizado que faça sentido para o reprodutor. |

{style="table-layout:auto"}
