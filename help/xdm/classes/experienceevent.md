---
keywords: Experience Platform;página inicial;tópicos populares;esquema;Esquema;XDM;campos;esquemas;Esquemas;identityMap;mapa de identidade;Mapa de identidade;Design de esquema;mapa;Mapa;modelagem de evento;modelagem de evento;práticas recomendadas;evento;eventos;
solution: Experience Platform
title: Classe XDM ExperienceEvent
description: Saiba mais sobre a classe XDM ExperienceEvent e as práticas recomendadas para modelagem de dados de evento.
exl-id: a8e59413-b52f-4ea5-867b-8d81088a3321
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '2672'
ht-degree: 0%

---

# [!DNL XDM ExperienceEvent] classe

[!DNL XDM ExperienceEvent] é uma classe padrão do Experience Data Model (XDM). Use essa classe para criar um instantâneo com carimbo de data e hora do sistema quando um evento específico ocorrer ou quando um determinado conjunto de condições for atingido.

Um Evento de experiência é um registro fatual do que ocorreu, incluindo o momento e a identidade do indivíduo envolvido. Eventos podem ser explícitos (ações humanas diretamente observáveis) ou implícitos (gerados sem uma ação humana direta) e são registrados sem agregação ou interpretação. Para obter mais informações de alto nível sobre o uso dessa classe no ecossistema da Platform, consulte a [visão geral do XDM](../home.md#data-behaviors).

A própria classe [!DNL XDM ExperienceEvent] fornece vários campos relacionados a séries temporais para um esquema. Dois destes campos (`_id` e `timestamp`) são **obrigatórios** para todos os esquemas baseados nesta classe, enquanto o restante é opcional. Os valores de alguns campos são preenchidos automaticamente quando os dados são assimilados.

![A estrutura do XDM ExperienceEvent como ele aparece na interface do usuário da plataforma.](../images/classes/experienceevent/structure.png)

| Propriedade | Descrição |
| --- | --- |
| `_id`<br>**(Obrigatório)** | O campo Classe de Evento de Experiência `_id` identifica exclusivamente eventos individuais que são assimilados na Adobe Experience Platform. Este campo é usado para rastrear a exclusividade de um evento individual, impedir a duplicação de dados e pesquisar esse evento nos serviços downstream.<br><br>Quando eventos duplicados são detectados, os aplicativos e serviços da Platform podem lidar com a duplicação de forma diferente. Por exemplo, eventos duplicados no Serviço de perfil são descartados se o evento com o mesmo `_id` já existir no armazenamento Perfil.<br><br>Em alguns casos, `_id` pode ser um [Identificador exclusivo universal (UUID)](https://datatracker.ietf.org/doc/html/rfc4122) ou [Identificador exclusivo global (GUID)](https://learn.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0).<br><br>Se estiver transmitindo dados de uma conexão de origem ou assimilando diretamente de um arquivo do Parquet, você deve gerar esse valor concatenando uma determinada combinação de campos que tornam o evento único. Os exemplos de eventos que podem ser concatenados incluem ID primária, carimbo de data e hora, tipo de evento e assim por diante. O valor concatenado deve ser uma cadeia de caracteres formatada `uri-reference`, o que significa que todos os caracteres de dois pontos devem ser removidos. Posteriormente, o valor concatenado deve ser transformado em hash usando SHA-256 ou outro algoritmo de sua escolha.<br><br>É importante distinguir que **este campo não representa uma identidade relacionada a uma pessoa individual**, mas o próprio registro de dados. Os dados de identidade relacionados a uma pessoa devem ser relegados a [campos de identidade](../schema/composition.md#identity) fornecidos por grupos de campos compatíveis. |
| `eventMergeId` | Se estiver usando o [Adobe Experience Platform Web SDK](/help/web-sdk/home.md) para assimilar dados, isso representa a ID do lote assimilado que causou a criação do registro. Esse campo é preenchido automaticamente pelo sistema após a assimilação de dados. Não há suporte para o uso desse campo fora do contexto de uma implementação do SDK da Web. |
| `eventType` | Uma string que indica o tipo ou categoria do evento. Esse campo pode ser usado se você quiser distinguir tipos de evento diferentes no mesmo esquema e conjunto de dados, como distinguir um evento de exibição de produto de um evento de carrinho de compras para uma empresa de varejo.<br><br>Os valores padrão para esta propriedade são fornecidos na [seção do apêndice](#eventType), incluindo descrições do caso de uso pretendido. Esse campo é um enum extensível, o que significa que você também pode usar suas próprias cadeias de caracteres de tipo de evento para categorizar os eventos que você está rastreando.<br><br>`eventType` limita você a usar apenas um único evento por ocorrência em seu aplicativo e, portanto, você deve usar campos calculados para informar ao sistema qual evento é mais importante. Para obter mais informações, consulte a seção sobre [práticas recomendadas para campos calculados](#calculated). |
| `producedBy` | Um valor de string que descreve o produtor ou a origem do evento. Esse campo pode ser usado para filtrar determinados produtores de eventos, se necessário, para fins de segmentação.<br><br>Alguns valores sugeridos para esta propriedade são fornecidos na [seção do apêndice](#producedBy). Esse campo é um enum extensível, o que significa que você também pode usar suas próprias cadeias de caracteres para representar diferentes produtores de evento. |
| `identityMap` | Um campo de mapa que contém um conjunto de identidades com namespace para o indivíduo ao qual o evento se aplica. Este campo é atualizado automaticamente pelo sistema à medida que os dados de identidade são assimilados. Para utilizar adequadamente este campo para o [Perfil de cliente em tempo real](../../profile/home.md), não tente atualizar manualmente o conteúdo do campo em suas operações de dados.<br /><br />Consulte a seção sobre mapas de identidade nas [noções básicas da composição de esquema](../schema/composition.md#identityMap) para obter mais informações sobre o caso de uso. |
| `timestamp`<br>**(Obrigatório)** | Um carimbo de data/hora ISO 8601 de quando o evento ocorreu, formatado conforme a [RFC 3339 Seção 5.6](https://datatracker.ietf.org/doc/html/rfc3339). Este carimbo de data/hora **deve** ocorrer no passado, mas **deve** ocorrer a partir de 1970. Consulte a seção abaixo em [carimbos de data e hora](#timestamps) para obter as práticas recomendadas para o uso deste campo. |

{style="table-layout:auto"}

## Práticas recomendadas para modelagem de eventos

As seções a seguir abordam as práticas recomendadas para criar esquemas do Experience Data Model (XDM) com base em eventos no Adobe Experience Platform.

### Carimbos de data e hora {#timestamps}

O campo raiz `timestamp` de um esquema de evento pode **only** representar a observação do próprio evento e deve ocorrer no passado. Entretanto, o evento **must** ocorrerá a partir de 1970. Se os casos de uso de segmentação exigirem o uso de carimbos de data e hora que podem ocorrer no futuro, esses valores deverão ser restritos em outro lugar no esquema do Evento de experiência.

Por exemplo, se uma empresa no setor de viagem e hospitalidade estiver modelando um evento de reserva de voo, o campo `timestamp` no nível da classe representa o horário em que o evento de reserva foi observado. Outros carimbos de data e hora relacionados ao evento, como a data de início da reserva de viagem, devem ser capturados em campos separados fornecidos por grupos de campos padrão ou personalizados.

![Um exemplo de esquema de Evento de Experiência com Reserva de Voo e Data de Início realçados.](../images/classes/experienceevent/timestamps.png)

Ao manter o carimbo de data e hora em nível de classe separado de outros valores de data e hora relacionados nos esquemas de evento, você pode implementar casos de uso de segmentação flexível, preservando uma conta com carimbo de data e hora de jornadas do cliente no aplicativo de experiência.

### Uso de campos calculados {#calculated}

Certas interações em seus aplicativos de experiência podem resultar em vários eventos relacionados que tecnicamente compartilham o mesmo carimbo de data e hora de evento e, portanto, podem ser representados como um único registro de evento. Por exemplo, se um cliente exibir um produto em seu site, isso poderá resultar em um registro de evento com dois valores possíveis de `eventType`: um evento de &quot;exibição de produto&quot; (`commerce.productViews`) ou um evento genérico de &quot;exibição de página&quot; (`web.webpagedetails.pageViews`). Nesses casos, você pode usar campos calculados para capturar os atributos mais importantes quando vários eventos são capturados em uma única ocorrência.

Use o [Preparo de dados do Adobe Experience Platform](../../data-prep/home.md) para mapear, transformar e validar dados de e para o XDM. Usando as [funções de mapeamento](../../data-prep/functions.md) disponíveis fornecidas pelo serviço, você pode chamar operadores lógicos para priorizar, transformar e/ou consolidar dados de registros de vários eventos ao serem assimilados no Experience Platform. No exemplo acima, você poderia designar `eventType` como um campo calculado que priorizaria uma &quot;exibição de produto&quot; sobre uma &quot;exibição de página&quot; sempre que ambas ocorressem.

Se você estiver assimilando dados manualmente na Platform por meio da interface do usuário, consulte o manual em [campos calculados](../../data-prep/ui/mapping.md#calculated-fields) para obter etapas específicas sobre como criar campos calculados.

Se você estiver transmitindo dados para a Platform usando uma conexão de origem, será possível configurar a origem para utilizar campos calculados. Consulte a [documentação da sua origem específica](../../sources/home.md) para obter instruções sobre como implementar campos calculados ao configurar a conexão.

## Grupos de campos de esquema compatíveis {#field-groups}

>[!NOTE]
>
>Os nomes de vários grupos de campos foram alterados. Consulte o documento em [atualizações de nome de grupo de campos](../field-groups/name-updates.md) para obter mais informações.

O Adobe fornece vários grupos de campos padrão para uso com a classe [!DNL XDM ExperienceEvent]. Veja a seguir uma lista de alguns grupos de campos comumente usados para a classe:

* [[!UICONTROL Extensão completa do Adobe Analytics ExperienceEvent]](../field-groups/event/analytics-full-extension.md)
* [[!UICONTROL Transferências de saldo]](../field-groups/event/balance-transfers.md)
* [[!UICONTROL Detalhes de marketing da campanha]](../field-groups/event/campaign-marketing-details.md)
* [[!UICONTROL Ações do cartão]](../field-groups/event/card-actions.md)
* [[!UICONTROL Detalhes do canal]](../field-groups/event/channel-details.md)
* [[!UICONTROL Detalhes do Commerce]](../field-groups/event/commerce-details.md)
* [[!UICONTROL Detalhes do depósito]](../field-groups/event/deposit-details.md)
* [[!UICONTROL Detalhes de troca do dispositivo]](../field-groups/event/device-trade-in-details.md)
* [[!UICONTROL Reserva para o jantar]](../field-groups/event/dining-reservation.md)
* [[!UICONTROL Detalhes da ID do Usuário Final]](../field-groups/event/enduserids.md)
* [[!UICONTROL Detalhes do ambiente]](../field-groups/event/environment-details.md)
* [[!UICONTROL Reserva de voo]](../field-groups/event/flight-reservation.md)
* [[!UICONTROL Consentimento IAB TCF 2.0]](../field-groups/event/iab.md)
* [[!UICONTROL Reserva de hospedagem]](../field-groups/event/lodging-reservation.md)
* [[!UICONTROL Detalhes de interação do MediaAnalytics]](../field-groups/event/mediaanalytics-interaction.md)
* [[!UICONTROL Detalhes da solicitação de orçamento]](../field-groups/event/quote-request-details.md)
* [[!UICONTROL Detalhes da reserva]](../field-groups/event/reservation-details.md)
* [[!UICONTROL Detalhes da Web]](../field-groups/event/web-details.md)

## Apêndice

A seção a seguir contém informações adicionais sobre a classe [!UICONTROL XDM ExperienceEvent].

### Valores aceitos para `eventType` {#eventType}

A tabela a seguir descreve os valores aceitos para `eventType`, juntamente com suas definições:

| Valor | Definição |
| --- | --- |
| `advertising.clicks` | Esse evento é rastreado quando ocorre uma ação para selecionar um anúncio. |
| `advertising.completes` | Esse evento rastreia quando um ativo de mídia cronometrado é observado até o fim. Isso não significa necessariamente que o espectador assistiu ao vídeo inteiro, pois ele poderia ter pulado para frente. |
| `advertising.conversions` | Esse evento rastreia uma ação predefinida executada por um cliente que aciona um evento para avaliação de desempenho. |
| `advertising.federated` | Este evento rastreia se um Evento de experiência foi criado por meio de federação de dados (compartilhamento de dados entre clientes). |
| `advertising.firstQuartiles` | Esse evento é rastreado quando um anúncio de vídeo digital é reproduzido até 25% de sua duração na velocidade normal. |
| `advertising.impressions` | Esse evento rastreia as impressões de um anúncio para um cliente com potencial para ser visualizado. |
| `advertising.midpoints` | Esse evento é rastreado quando um anúncio de vídeo digital é reproduzido até 50% de sua duração na velocidade normal. |
| `advertising.starts` | Esse evento é rastreado quando um anúncio de vídeo digital é reproduzido. |
| `advertising.thirdQuartiles` | Esse evento é rastreado quando um anúncio de vídeo digital é reproduzido até 75% de sua duração na velocidade normal. |
| `advertising.timePlayed` | Esse evento rastreia a quantidade de tempo gasto por um usuário em um ativo de mídia temporizado específico. |
| `application.close` | Esse evento rastreia quando um aplicativo foi fechado ou enviado para o plano de fundo. |
| `application.launch` | Esse evento rastreia quando um aplicativo foi iniciado ou trazido para o primeiro plano. |
| `commerce.backofficeCreditMemoIssued` | Esse evento rastreia quando um aviso de crédito é emitido para um cliente. |
| `commerce.backofficeOrderCancelled` | Este evento rastreia quando um processo de compra iniciado anteriormente foi encerrado antes da conclusão. |
| `commerce.backofficeOrderItemsShipped` | Esse evento rastreia quando os itens comprados foram fisicamente entregues ao cliente. |
| `commerce.backofficeOrderPlaced` | Esse evento rastreia a colocação de um pedido. |
| `commerce.backofficeShipmentCompleted` | Este evento rastreia a conclusão bem-sucedida de todo o processo de remessa. |
| `commerce.checkouts` | Este evento rastreia quando um evento de check-out ocorre em uma lista de produtos. Pode haver mais de um evento de check-out se houver várias etapas em um processo de check-out. Se houver várias etapas, o carimbo de data e hora e a página/experiência referenciada para cada evento serão usados para identificar cada evento individual (etapa), representado em ordem. |
| `commerce.productListAdds` | Esse evento rastreia quando um produto é adicionado à lista de produtos ou ao carrinho de compras. |
| `commerce.productListOpens` | Esse evento rastreia quando uma nova lista de produtos (carrinho de compras) é inicializada ou criada. |
| `commerce.productListRemovals` | Esse evento rastreia quando uma entrada de produto é removida de uma lista de produtos ou carrinho de compras. |
| `commerce.productListReopens` | Esse evento rastreia quando uma lista de produtos (carrinho de compras) que não estava mais acessível (abandonada) foi reativada por um cliente, como por meio de uma atividade de remarketing. |
| `commerce.productListViews` | Esse evento é rastreado quando uma lista de produtos ou carrinho de compras recebe uma visualização. |
| `commerce.productViews` | Esse evento rastreia quando um produto recebe uma ou mais visualizações. |
| `commerce.purchases` | Esse evento rastreia quando um pedido é aceito. Essa é a única ação necessária em uma conversão de comércio. Um evento de compra deve ter uma lista de produtos referida. |
| `commerce.saveForLaters` | Esse evento rastreia quando uma lista de produtos é salva para uso futuro, como uma lista de desejos de produtos. |
| `decisioning.propositionDisplay` | Esse evento rastreia quando uma apresentação de decisão era exibida a uma pessoa. |
| `decisioning.propositionDismiss` | Esse evento é rastreado quando é tomada a decisão de não se envolver com a oferta apresentada. |
| `decisioning.propositionInteract` | Esse evento rastreia quando uma pessoa interagiu com uma apresentação de decisão. |
| `decisioning.propositionSend` | Esse evento é rastreado quando é decidido enviar a um cliente potencial uma recomendação ou oferta para consideração. |
| `decisioning.propositionTrigger` | Esse evento rastreia a ativação de um processo de apresentação. Ocorreu uma determinada condição ou ação para solicitar a apresentação de uma oferta. |
| `delivery.feedback` | Esse evento rastreia eventos de feedback para um delivery, como um delivery de email. |
| `directMarketing.emailBounced` | Esse evento rastreia quando um email para uma pessoa é rejeitado. |
| `directMarketing.emailBouncedSoft` | Esse evento rastreia quando um email para uma pessoa é rejeitado temporariamente. |
| `directMarketing.emailClicked` | Esse evento é rastreado quando uma pessoa clica em um link em um email de marketing. |
| `directMarketing.emailDelivered` | Esse evento rastreia quando um email foi entregue com êxito ao serviço de email de uma pessoa. |
| `directMarketing.emailOpened` | Esse evento rastreia quando uma pessoa abriu um email de marketing. |
| `directMarketing.emailSent` | Esse evento rastreia quando um email de marketing foi enviado a uma pessoa. |
| `directMarketing.emailUnsubscribed` | Esse evento é rastreado quando uma pessoa cancela a assinatura de um email de marketing. |
| `inappmessageTracking.dismiss` | Esse evento rastreia quando uma mensagem no aplicativo é descartada. |
| `inappmessageTracking.display` | Esse evento rastreia quando uma mensagem no aplicativo é exibida. |
| `inappmessageTracking.interact` | Esse evento rastreia quando uma mensagem no aplicativo teve interação. |
| `leadOperation.callWebhook` | Esse evento rastreia quando um webhook foi chamado em resposta a um lead. |
| `leadOperation.changeCampaignStream` | Esse evento significa uma mudança na estratégia de marketing ou engajamento para um lead comercial específico. |
| `leadOperation.changeEngagementCampaignCadence` | Esse evento é rastreado quando há uma mudança na frequência com a qual um lead é envolvido como parte de uma campanha. |
| `leadOperation.convertLead` | Esse evento rastreia quando um lead é convertido. |
| `leadOperation.interestingMoment` | Este evento rastreia quando um momento interessante foi gravado para uma pessoa. |
| `leadOperation.mergeLeads` | Esse evento rastreia quando as informações de vários leads que se referem à mesma entidade foram consolidadas. |
| `leadOperation.newLead` | Esse evento rastreia quando um lead é criado. |
| `leadOperation.scoreChanged` | Esse evento é rastreado quando o valor do atributo de pontuação do lead é alterado. |
| `leadOperation.statusInCampaignProgressionChanged` | Este evento é rastreado quando o status de um lead em uma campanha é alterado. |
| `listOperation.addToList` | Esse evento rastreia quando uma pessoa foi adicionada a uma lista de marketing. |
| `listOperation.removeFromList` | Esse evento rastreia quando uma pessoa foi removida de uma lista de marketing. |
| `media.adBreakComplete` | Este evento rastreia quando um evento `adBreakComplete` ocorreu. Esse evento é acionado no início de um ad break. |
| `media.adBreakStart` | Este evento rastreia quando um evento `adBreakStart` ocorreu. Esse evento é acionado no final de um ad break. |
| `media.adComplete` | Este evento rastreia quando um evento `adComplete` ocorreu. Esse evento é acionado quando um anúncio é concluído. |
| `media.adSkip` | Este evento rastreia quando um evento `adSkip` ocorreu. Esse evento é disparado quando um anúncio é ignorado. |
| `media.adStart` | Este evento rastreia quando um evento `adStart` ocorreu. Esse evento é acionado quando um anúncio é iniciado. |
| `media.bitrateChange` | Este evento rastreia quando um evento `bitrateChange` ocorreu. Esse evento é acionado quando há uma alteração na taxa de bits. |
| `media.bufferStart` | Este evento rastreia quando um evento `bufferStart` ocorreu. Esse evento é disparado quando a mídia começou a ser armazenada em buffer. |
| `media.chapterComplete` | Este evento rastreia quando um evento `chapterComplete` ocorreu. Esse evento é acionado na conclusão de um capítulo na mídia. |
| `media.chapterSkip` | Este evento rastreia quando um evento `chapterSkip` ocorreu. Esse evento é acionado quando um usuário pula para frente ou para trás para outra seção ou capítulo no conteúdo de mídia. |
| `media.chapterStart` | Este evento rastreia quando um evento `chapterStart` ocorreu. Esse evento é acionado no início de uma seção ou capítulo específico no conteúdo de mídia. |
| `media.downloaded` | Esse evento rastreia quando o conteúdo de download de mídia ocorreu. |
| `media.error` | Este evento rastreia quando um evento `error` ocorreu. Esse evento é disparado quando ocorre um erro ou problema durante a reprodução da mídia. |
| `media.pauseStart` | Este evento rastreia quando um evento `pauseStart` ocorreu. Esse evento é acionado quando um usuário inicia uma pausa na reprodução de mídia. |
| `media.ping` | Este evento rastreia quando um evento `ping` ocorreu. Isso verifica a disponibilidade de um recurso de mídia. |
| `media.play` | Este evento rastreia quando um evento `play` ocorreu. Esse evento é acionado quando o conteúdo de mídia está sendo reproduzido, indicando o consumo ativo pelo usuário. |
| `media.sessionComplete` | Este evento rastreia quando um evento `sessionComplete` ocorreu. Esse evento marca o fim de uma sessão de reprodução de mídia. |
| `media.sessionEnd` | Este evento rastreia quando um evento `sessionEnd` ocorreu. Esse evento indica a conclusão de uma sessão de mídia. Essa conclusão pode envolver o fechamento do reprodutor de mídia ou a interrupção da reprodução. |
| `media.sessionStart` | Este evento rastreia quando um evento `sessionStart` ocorreu. Esse evento marca o início de uma sessão de reprodução de mídia. É acionado quando um usuário começa a reproduzir um arquivo de mídia. |
| `media.statesUpdate` | Este evento rastreia quando um evento `statesUpdate` ocorreu. Os recursos de rastreamento do estado do player podem ser anexados a um fluxo de áudio ou vídeo. Os estados padrão são: tela cheia, mudo, legendas ocultas, picture in picture e em foco. |
| `opportunityEvent.addToOpportunity` | Esse evento rastreia quando uma pessoa foi adicionada a uma oportunidade. |
| `opportunityEvent.opportunityUpdated` | Esse evento rastreia quando uma oportunidade é atualizada. |
| `opportunityEvent.removeFromOpportunity` | Este evento rastreia quando uma pessoa foi removida de uma oportunidade. |
| `pushTracking.applicationOpened` | Esse evento rastreia quando uma pessoa abriu um aplicativo a partir de uma notificação por push. |
| `pushTracking.customAction` | Esse evento é rastreado quando uma pessoa seleciona uma ação personalizada em uma notificação por push. |
| `web.formFilledOut` | Esse evento rastreia quando uma pessoa preenche um formulário em uma página da Web. |
| `web.webinteraction.linkClicks` | Esse evento rastreia quando um link é selecionado uma ou mais vezes. |
| `web.webpagedetails.pageViews` | Esse evento rastreia quando uma página da Web recebe uma ou mais exibições. |
| `location.entry` | Esse evento rastreia a entrada de uma pessoa ou dispositivo em um local específico. |
| `location.exit` | Esse evento rastreia a saída de uma pessoa ou dispositivo de um local específico. |

{style="table-layout:auto"}

### Valores sugeridos para `producedBy` {#producedBy}

A tabela a seguir descreve alguns valores aceitos para `producedBy`:

| Valor | Definição |
| --- | --- |
| `self` | Auto |
| `system` | Sistema |
| `salesRef` | Representante de Vendas |
| `customerRep` | Representante do Cliente |
