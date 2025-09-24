---
keywords: Experience Platform;página inicial;tópicos populares;esquema;Esquema;XDM;campos;esquemas;Esquemas;identityMap;mapa de identidade;Mapa de identidade;Design de esquema;mapa;Mapa;modelagem de evento;modelagem de evento;práticas recomendadas;evento;eventos;
solution: Experience Platform
title: Classe XDM ExperienceEvent
description: Saiba mais sobre a classe XDM ExperienceEvent e as práticas recomendadas para modelagem de dados de evento.
exl-id: a8e59413-b52f-4ea5-867b-8d81088a3321
source-git-commit: 8aa8a1c42e9656716be746ba447a5f77a8155b4c
workflow-type: tm+mt
source-wordcount: '2783'
ht-degree: 0%

---

# [!DNL XDM ExperienceEvent] classe

[!DNL XDM ExperienceEvent] é uma classe padrão do Experience Data Model (XDM). Use essa classe para criar um instantâneo com carimbo de data e hora do sistema quando um evento específico ocorrer ou quando um determinado conjunto de condições for atingido.

Um Evento de experiência é um registro fatual do que ocorreu, incluindo o momento e a identidade do indivíduo envolvido. Eventos podem ser explícitos (ações humanas diretamente observáveis) ou implícitos (gerados sem uma ação humana direta) e são registrados sem agregação ou interpretação. Para obter mais informações de alto nível sobre o uso dessa classe no ecossistema do Experience Platform, consulte a [visão geral do XDM](../home.md#data-behaviors).

A própria classe [!DNL XDM ExperienceEvent] fornece vários campos relacionados a séries temporais para um esquema. Dois destes campos (`_id` e `timestamp`) são **obrigatórios** para todos os esquemas baseados nesta classe, enquanto o restante é opcional. Os valores de alguns campos são preenchidos automaticamente quando os dados são assimilados.

![A estrutura do XDM ExperienceEvent como ele aparece na interface do usuário do Experience Platform.](../images/classes/experienceevent/structure.png)

| Propriedade | Descrição |
| --- | --- |
| `_id`<br>**(Obrigatório)** | O campo Classe de Evento de Experiência `_id` identifica exclusivamente eventos individuais que são assimilados na Adobe Experience Platform. Este campo é usado para rastrear a exclusividade de um evento individual, impedir a duplicação de dados e pesquisar esse evento nos serviços downstream.<br><br>Quando eventos duplicados são detectados, os aplicativos e serviços da Experience Platform podem lidar com a duplicação de forma diferente. Por exemplo, eventos duplicados no Serviço de perfil são descartados se o evento com o mesmo `_id` já existir no armazenamento Perfil. No entanto, esses eventos ainda serão registrados no data lake.<br><br>Em alguns casos, `_id` pode ser um [Identificador exclusivo universal (UUID)](https://datatracker.ietf.org/doc/html/rfc4122) ou [Identificador exclusivo global (GUID)](https://learn.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0).<br><br>Se estiver transmitindo dados de uma conexão de origem ou assimilando diretamente de um arquivo do Parquet, você deve gerar esse valor concatenando uma determinada combinação de campos que tornam o evento único. Os exemplos de eventos que podem ser concatenados incluem ID primária, carimbo de data e hora, tipo de evento e assim por diante. O valor concatenado deve ser uma cadeia de caracteres formatada `uri-reference`, o que significa que todos os caracteres de dois pontos devem ser removidos. Posteriormente, o valor concatenado deve ser transformado em hash usando SHA-256 ou outro algoritmo de sua escolha.<br><br>É importante distinguir que **este campo não representa uma identidade relacionada a uma pessoa individual**, mas o próprio registro de dados. Os dados de identidade relacionados a uma pessoa devem ser relegados a [campos de identidade](../schema/composition.md#identity) fornecidos por grupos de campos compatíveis. |
| `eventMergeId` | Se estiver usando o [Adobe Experience Platform Web SDK](/help/web-sdk/home.md) para assimilar dados, isso representa a ID do lote assimilado que causou a criação do registro. Esse campo é preenchido automaticamente pelo sistema após a assimilação de dados. Não há suporte para o uso desse campo fora do contexto de uma implementação do Web SDK. |
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

Use o [Preparo de dados do Adobe Experience Platform](../../data-prep/home.md) para mapear, transformar e validar dados de e para o XDM. Usando as [funções de mapeamento](../../data-prep/functions.md) disponíveis fornecidas pelo serviço, você pode chamar operadores lógicos para priorizar, transformar e/ou consolidar dados de registros de vários eventos ao serem assimilados na Experience Platform. No exemplo acima, você poderia designar `eventType` como um campo calculado que priorizaria uma &quot;exibição de produto&quot; sobre uma &quot;exibição de página&quot; sempre que ambas ocorressem.

Se você estiver assimilando dados manualmente na Experience Platform por meio da interface do usuário, consulte o manual em [campos calculados](../../data-prep/ui/mapping.md#calculated-fields) para obter etapas específicas sobre como criar campos calculados.

Se você estiver transmitindo dados para o Experience Platform usando uma conexão de origem, será possível configurar a origem para utilizar campos calculados. Consulte a [documentação da sua origem específica](../../sources/home.md) para obter instruções sobre como implementar campos calculados ao configurar a conexão.

## Grupos de campos de esquema compatíveis {#field-groups}

>[!NOTE]
>
>Os nomes de vários grupos de campos foram alterados. Consulte o documento em [atualizações de nome de grupo de campos](../field-groups/name-updates.md) para obter mais informações.

A Adobe fornece vários grupos de campos padrão para uso com a classe [!DNL XDM ExperienceEvent]. Veja a seguir uma lista de alguns grupos de campos comumente usados para a classe:

* [[!UICONTROL Extensão completa do Adobe Analytics ExperienceEvent]](../field-groups/event/analytics-full-extension.md)
* [[!UICONTROL Extensão completa do Adobe Advertising Cloud ExperienceEvent]](../field-groups/event/advertising-full-extension.md)
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
| `click` | **Obsoleto** Em vez disso, use `decisioning.propositionInteract`. |
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
| `decisioning.propositionDisplay` | Esse evento é usado quando o Web SDK envia automaticamente informações sobre o que está sendo exibido em uma página. No entanto, você não precisará desse tipo de evento se já estiver incluindo informações de exibição de outras maneiras, como com ocorrências na parte superior e inferior da página. Na parte inferior das ocorrências da página, você pode escolher qualquer tipo de evento que desejar. |
| `decisioning.propositionDismiss` | Esse tipo de evento é usado quando uma mensagem no aplicativo do Adobe Journey Optimizer ou um cartão de conteúdo é descartado. |
| `decisioning.propositionFetch` | Usado para indicar que um evento é principalmente para buscar decisões. O Adobe Analytics descartará esse evento automaticamente. |
| `decisioning.propositionInteract` | Esse tipo de evento é usado para rastrear interações, como cliques, em conteúdo personalizado. |
| `decisioning.propositionSend` | Esse evento é rastreado quando é decidido enviar a um cliente potencial uma recomendação ou oferta para consideração. |
| `decisioning.propositionTrigger` | Eventos deste tipo são armazenados no armazenamento local pelo [Web SDK](../../web-sdk/home.md), mas não são enviados para a Experience Edge. Sempre que um conjunto de regras é satisfeito, um evento é gerado e armazenado no armazenamento local (se essa configuração estiver ativada). |
| `delivery.feedback` | Esse evento rastreia eventos de feedback para um delivery, como um delivery de email. |
| `directMarketing.emailBounced` | Esse evento rastreia quando um email para uma pessoa é rejeitado. |
| `directMarketing.emailBouncedSoft` | Esse evento rastreia quando um email para uma pessoa é rejeitado temporariamente. |
| `directMarketing.emailClicked` | Esse evento é rastreado quando uma pessoa clica em um link em um email de marketing. |
| `directMarketing.emailDelivered` | Esse evento rastreia quando um email foi entregue com êxito ao serviço de email de uma pessoa. |
| `directMarketing.emailOpened` | Esse evento rastreia quando uma pessoa abriu um email de marketing. |
| `directMarketing.emailSent` | Esse evento rastreia quando um email de marketing foi enviado a uma pessoa. |
| `directMarketing.emailUnsubscribed` | Esse evento é rastreado quando uma pessoa cancela a assinatura de um email de marketing. |
| `display` | **Obsoleto** Em vez disso, use `decisioning.propositionDisplay`. |
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
| `media.adBreakComplete` | Esse evento sinaliza a conclusão de um ad break. |
| `media.adBreakStart` | Esse evento sinaliza o início de um ad break. |
| `media.adComplete` | Esse evento sinaliza a conclusão de um anúncio. |
| `media.adSkip` | Esse evento sinaliza quando um anúncio é ignorado. |
| `media.adStart` | Esse evento sinaliza o início de um anúncio. |
| `media.bitrateChange` | Esse evento sinaliza quando há uma alteração na taxa de bits. |
| `media.bufferStart` | O tipo de evento `media.bufferStart` é enviado quando o buffering começa. Não há um tipo de evento `bufferResume` específico; considera-se que o buffering foi retomado quando um evento `play` é enviado após um evento `bufferStart`. |
| `media.chapterComplete` | Este evento sinaliza a conclusão de um capítulo. |
| `media.chapterSkip` | Esse evento é acionado quando um usuário passa para frente ou para trás em outra seção ou capítulo. |
| `media.chapterStart` | Esse evento sinaliza o início de um capítulo. |
| `media.downloaded` | Esse evento rastreia quando o conteúdo de download de mídia ocorreu. |
| `media.error` | Esse evento sinaliza quando um erro ocorreu durante a reprodução da mídia. |
| `media.pauseStart` | Este evento rastreia quando um evento `pauseStart` ocorreu. Esse evento é acionado quando um usuário inicia uma pausa na reprodução de mídia. Não há um tipo de evento de retomada. Um currículo é inferido quando você envia um evento de reprodução após um `pauseStart`. |
| `media.ping` | O tipo de evento `media.ping` é usado para indicar o status de reprodução em andamento. Para o conteúdo principal, esse evento deve ser enviado a cada 10 segundos durante a reprodução, começando 10 segundos após o início da reprodução. Para conteúdo de anúncio, ele deve ser enviado a cada segundo durante o rastreamento do anúncio. Os eventos de ping não devem incluir o mapa de parâmetros no corpo da solicitação. |
| `media.play` | O tipo de evento `media.play` é enviado quando o player faz a transição para o estado `playing` a partir de outro estado, como `buffering,` `paused` (quando retomado pelo usuário) ou `error` (quando recuperado), incluindo cenários como reprodução automática. Este evento é disparado pelo retorno de chamada `on('Playing')` do player. |
| `media.sessionComplete` | Esse evento é enviado quando o fim do conteúdo principal é atingido. |
| `media.sessionEnd` | O tipo de evento `media.sessionEnd` notifica o back-end do Media Analytics para fechar imediatamente uma sessão quando um usuário abandona a visualização e é improvável que retorne. Se esse evento não for enviado, a sessão expirará após 10 minutos de inatividade ou 30 minutos sem movimento do indicador de reprodução. Quaisquer chamadas de mídia subsequentes com essa ID de sessão serão ignoradas. |
| `media.sessionStart` | O tipo de evento `media.sessionStart` é enviado com a chamada de iniciação de sessão. Ao receber uma resposta, a ID da sessão é extraída do cabeçalho Localização e usada para todas as chamadas de evento subsequentes para o servidor de coleta. |
| `media.statesUpdate` | Este evento rastreia quando um evento `statesUpdate` ocorreu. Os recursos de rastreamento do estado do player podem ser anexados a um fluxo de áudio ou vídeo. Os estados padrão são: `fullscreen`, `mute`, `closedCaptioning`, `pictureInPicture` e `inFocus`. |
| `opportunityEvent.addToOpportunity` | Esse evento rastreia quando uma pessoa foi adicionada a uma oportunidade. |
| `opportunityEvent.opportunityUpdated` | Esse evento rastreia quando uma oportunidade é atualizada. |
| `opportunityEvent.removeFromOpportunity` | Este evento rastreia quando uma pessoa foi removida de uma oportunidade. |
| `personalization.request` | **Obsoleto** Em vez disso, use `decisioning.propositionFetch`. |
| `pushTracking.applicationOpened` | Esse evento rastreia quando uma pessoa abriu um aplicativo a partir de uma notificação por push. |
| `pushTracking.customAction` | Esse evento é rastreado quando uma pessoa seleciona uma ação personalizada em uma notificação por push. |
| `web.formFilledOut` | Esse evento rastreia quando uma pessoa preenche um formulário em uma página da Web. |
| `web.webinteraction.linkClicks` | O evento sinaliza que um clique em um link foi registrado automaticamente pelo Web SDK. |
| `web.webpagedetails.pageViews` | Esse tipo de evento é o método padrão para marcar a ocorrência como uma exibição de página. |
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
