---
keywords: Experience Platform;página inicial;tópicos populares;esquema;Esquema;XDM;campos;esquemas;Esquemas;identityMap;mapa de identidade;Mapa de identidade;Design de esquema;mapa;Mapa;modelagem de evento;modelagem de evento;práticas recomendadas;evento;eventos;
solution: Experience Platform
title: Classe XDM ExperienceEvent
description: Este documento fornece uma visão geral da classe XDM ExperienceEvent e as práticas recomendadas para a modelagem de dados de eventos.
exl-id: a8e59413-b52f-4ea5-867b-8d81088a3321
source-git-commit: a3140d5216857ef41c885bbad8c69d91493b619d
workflow-type: tm+mt
source-wordcount: '1836'
ht-degree: 1%

---

# [!DNL XDM ExperienceEvent] classe

[!DNL XDM ExperienceEvent] é uma classe padrão do Experience Data Model (XDM) que permite criar um instantâneo com carimbo de data e hora do sistema quando um evento específico ocorre ou um determinado conjunto de condições é atingido.

Um Evento de experiência é um registro fatual do que ocorreu, incluindo o momento e a identidade do indivíduo envolvido. Eventos podem ser explícitos (ações humanas diretamente observáveis) ou implícitos (gerados sem uma ação humana direta) e são registrados sem agregação ou interpretação. Para obter mais informações de alto nível sobre o uso dessa classe no ecossistema da Platform, consulte o [Visão geral do XDM](../home.md#data-behaviors).

A variável [!DNL XDM ExperienceEvent] A própria classe fornece vários campos relacionados a séries temporais para um esquema. Dois desses campos (`_id` e `timestamp`) são **obrigatório** para todos os esquemas baseados na classe, enquanto o restante é opcional. Os valores de alguns campos são preenchidos automaticamente quando os dados são assimilados.

![A estrutura do ExperienceEvent XDM como aparece na interface do usuário da plataforma](../images/classes/experienceevent/structure.png)

| Propriedade | Descrição |
| --- | --- |
| `_id`<br>**(Obrigatório)** | Um identificador de string exclusivo para o evento. Este campo é usado para rastrear a exclusividade de um evento individual, impedir a duplicação de dados e pesquisar esse evento nos serviços downstream. Em alguns casos, `_id` pode ser um [Identificador exclusivo universal (UUID)](https://tools.ietf.org/html/rfc4122) ou [Identificador exclusivo global (GUID)](https://docs.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0).<br><br>Se você estiver transmitindo dados de uma conexão de origem ou assimilando diretamente de um arquivo do Parquet, é necessário gerar esse valor concatenando uma determinada combinação de campos que tornam o evento único, como ID principal, carimbo de data e hora, tipo de evento e assim por diante. O valor concatenado deve ser um `uri-reference` string formatada, o que significa que os caracteres de dois pontos devem ser removidos. Posteriormente, o valor concatenado deve ser transformado em hash usando SHA-256 ou outro algoritmo de sua escolha.<br><br>É importante distinguir esse **este campo não representa uma identidade relacionada a uma pessoa individual**, mas sim o próprio registro dos dados. Os dados de identidade relativos a uma pessoa devem ser [campos de identidade](../schema/composition.md#identity) fornecido por grupos de campos compatíveis. |
| `eventMergeId` | Se estiver usando o [Adobe Experience Platform Web SDK](../../edge/home.md) para assimilar dados, representa a ID do lote assimilado que causou a criação do registro. Esse campo é preenchido automaticamente pelo sistema após a assimilação de dados. Não há suporte para o uso desse campo fora do contexto de uma implementação do SDK da Web. |
| `eventType` | Uma string que indica o tipo ou categoria do evento. Esse campo pode ser usado se você quiser distinguir tipos de evento diferentes no mesmo esquema e conjunto de dados, como distinguir um evento de exibição de produto de um evento de carrinho de compras para uma empresa de varejo.<br><br>Os valores padrão para essa propriedade são fornecidos na variável [seção apêndice](#eventType), incluindo descrições do caso de uso pretendido. Esse campo é um enum extensível, o que significa que você também pode usar suas próprias cadeias de caracteres de tipo de evento para categorizar os eventos que você está rastreando.<br><br>`eventType` O limita o uso de apenas um evento por ocorrência no aplicativo e, portanto, você deve usar campos calculados para informar ao sistema qual evento é mais importante. Para obter mais informações, consulte a seção sobre [práticas recomendadas para campos calculados](#calculated). |
| `producedBy` | Um valor de string que descreve o produtor ou a origem do evento. Esse campo pode ser usado para filtrar determinados produtores de eventos, se necessário, para fins de segmentação.<br><br>Alguns valores sugeridos para essa propriedade são fornecidos na [seção apêndice](#producedBy). Esse campo é um enum extensível, o que significa que você também pode usar suas próprias cadeias de caracteres para representar diferentes produtores de evento. |
| `identityMap` | Um campo de mapa que contém um conjunto de identidades com namespace para o indivíduo ao qual o evento se aplica. Este campo é atualizado automaticamente pelo sistema à medida que os dados de identidade são assimilados. Para utilizar adequadamente esse campo para [Perfil do cliente em tempo real](../../profile/home.md), não tente atualizar manualmente o conteúdo do campo em suas operações de dados.<br /><br />Consulte a seção sobre mapas de identidade na [noções básicas da composição do esquema](../schema/composition.md#identityMap) para obter mais informações sobre o caso de uso. |
| `timestamp`<br>**(Obrigatório)** | Um carimbo de data e hora ISO 8601 de quando o evento ocorreu, formatado conforme [RFC 3339 Seção 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). Esse carimbo de data e hora deve ocorrer no passado. Consulte a seção abaixo em [carimbos de data e hora](#timestamps) para obter as práticas recomendadas de uso deste campo. |

{style="table-layout:auto"}

## Práticas recomendadas para modelagem de eventos

As seções a seguir abordam as práticas recomendadas para criar esquemas do Experience Data Model (XDM) com base em eventos no Adobe Experience Platform.

### Carimbos de data e hora {#timestamps}

A raiz `timestamp` de um esquema de evento pode **somente** representam a observação do próprio evento e devem ocorrer no passado. Se os casos de uso de segmentação exigirem o uso de carimbos de data e hora que podem ocorrer no futuro, esses valores deverão ser restritos em outro lugar no esquema do Evento de experiência.

Por exemplo, se uma empresa no setor de viagens e hospitalidade estiver modelando um evento de reserva de voo, o nível de classe `timestamp` field representa a hora em que o evento de reserva foi observado. Outros carimbos de data e hora relacionados ao evento, como a data de início da reserva de viagem, devem ser capturados em campos separados fornecidos por grupos de campos padrão ou personalizados.

![Um exemplo de esquema de Evento de experiência com Reserva de voo e Data de início destacado.](../images/classes/experienceevent/timestamps.png)

Ao manter o carimbo de data e hora em nível de classe separado de outros valores de data e hora relacionados nos esquemas de evento, você pode implementar casos de uso de segmentação flexível, preservando uma conta com carimbo de data e hora de jornadas do cliente no aplicativo de experiência.

### Uso de campos calculados {#calculated}

Certas interações em seus aplicativos de experiência podem resultar em vários eventos relacionados que tecnicamente compartilham o mesmo carimbo de data e hora de evento e, portanto, podem ser representados como um único registro de evento. Por exemplo, se um cliente visualizar um produto no seu site, isso poderá resultar em um registro de evento com dois eventos potenciais `eventType` valores: um evento &quot;exibição de produto&quot; (`commerce.productViews`) ou um evento genérico de &quot;exibição de página&quot; (`web.webpagedetails.pageViews`). Nesses casos, você pode usar campos calculados para capturar os atributos mais importantes quando vários eventos são capturados em uma única ocorrência.

[Preparação de dados do Adobe Experience Platform](../../data-prep/home.md) permite mapear, transformar e validar dados de e para XDM. Usar o disponível [mapeamento de funções](../../data-prep/functions.md) fornecido pelo serviço, você pode chamar operadores lógicos para priorizar, transformar e/ou consolidar dados de registros de vários eventos ao serem assimilados no Experience Platform. No exemplo acima, você poderia designar `eventType` como um campo calculado que priorizaria uma &quot;exibição de produto&quot; em vez de uma &quot;exibição de página&quot; sempre que ambas ocorressem.

Se você estiver assimilando dados manualmente na Platform por meio da interface do usuário, consulte o manual em [campos calculados](../../data-prep/ui/mapping.md#calculated-fields) para obter etapas específicas sobre como criar campos calculados.

Se você estiver transmitindo dados para a Platform usando uma conexão de origem, será possível configurar a origem para utilizar campos calculados. Consulte a [documentação para sua origem específica](../../sources/home.md) para obter instruções sobre como implementar campos calculados ao configurar a conexão.

## Grupos de campos de esquema compatíveis {#field-groups}

>[!NOTE]
>
>Os nomes de vários grupos de campos foram alterados. Consulte o documento sobre [atualizações do nome do grupo de campos](../field-groups/name-updates.md) para obter mais informações.

O Adobe fornece vários grupos de campos padrão para uso com o [!DNL XDM ExperienceEvent] classe. Veja a seguir uma lista de alguns grupos de campos comumente usados para a classe:

* [[!UICONTROL Extensão completa do Adobe Analytics ExperienceEvent]](../field-groups/event/analytics-full-extension.md)
* [[!UICONTROL Transferências de saldo]](../field-groups/event/balance-transfers.md)
* [[!UICONTROL Detalhes de marketing da campanha]](../field-groups/event/campaign-marketing-details.md)
* [[!UICONTROL Ações do cartão]](../field-groups/event/card-actions.md)
* [[!UICONTROL Detalhes do canal]](../field-groups/event/channel-details.md)
* [[!UICONTROL Detalhes do comércio]](../field-groups/event/commerce-details.md)
* [[!UICONTROL Detalhes do depósito]](../field-groups/event/deposit-details.md)
* [[!UICONTROL Detalhes de troca do dispositivo]](../field-groups/event/device-trade-in-details.md)
* [[!UICONTROL Reserva para o jantar]](../field-groups/event/dining-reservation.md)
* [[!UICONTROL Detalhes da ID do usuário final]](../field-groups/event/enduserids.md)
* [[!UICONTROL Detalhes do ambiente]](../field-groups/event/environment-details.md)
* [[!UICONTROL Reserva de voo]](../field-groups/event/flight-reservation.md)
* [[!UICONTROL Consentimento IAB TCF 2.0]](../field-groups/event/iab.md)
* [[!UICONTROL Reserva de acomodação]](../field-groups/event/lodging-reservation.md)
* [[!UICONTROL Detalhes da solicitação de orçamento]](../field-groups/event/quote-request-details.md)
* [[!UICONTROL Detalhes da reserva]](../field-groups/event/reservation-details.md)
* [[!UICONTROL Detalhes da Web]](../field-groups/event/web-details.md)

## Apêndice

A seção a seguir contém informações adicionais sobre o [!UICONTROL XDM ExperienceEvent] classe.

### Valores aceitos para `eventType` {#eventType}

A tabela a seguir descreve os valores aceitos para `eventType`, juntamente com suas definições:

| Valor | Definição |
| --- | --- |
| `advertising.clicks` | Clique em ações em um anúncio. |
| `advertising.completes` | Um ativo de mídia cronometrado foi observado até o fim. Isso não significa necessariamente que o espectador assistiu ao vídeo inteiro, pois ele poderia ter pulado para frente. |
| `advertising.conversions` | Ações predefinidas executadas por um cliente que acionam um evento para avaliação de desempenho. |
| `advertising.federated` | Indica se um Evento de experiência foi criado por meio de federação de dados (compartilhamento de dados entre clientes). |
| `advertising.firstQuartiles` | Um anúncio de vídeo digital foi reproduzido até 25% de sua duração na velocidade normal. |
| `advertising.impressions` | Impressões de um anúncio para um cliente com potencial para ser visualizado. |
| `advertising.midpoints` | Um anúncio de vídeo digital foi reproduzido até 50% de sua duração na velocidade normal. |
| `advertising.starts` | Um anúncio de vídeo digital foi reproduzido. |
| `advertising.thirdQuartiles` | Um anúncio de vídeo digital foi reproduzido até 75% de sua duração na velocidade normal. |
| `advertising.timePlayed` | Descreve a quantidade de tempo gasto por um usuário em um ativo de mídia temporizado específico. |
| `application.close` | Um aplicativo foi fechado ou enviado em segundo plano. |
| `application.launch` | Um aplicativo foi iniciado ou colocado em primeiro plano. |
| `commerce.checkouts` | Ocorreu um evento de check-out para uma lista de produtos. Pode haver mais de um evento de check-out se houver várias etapas em um processo de check-out. Se houver várias etapas, o carimbo de data e hora e a página/experiência referenciada para cada evento serão usados para identificar cada evento individual (etapa), representado em ordem. |
| `commerce.productListAdds` | Um produto foi adicionado à lista de produtos ou ao carrinho de compras. |
| `commerce.productListOpens` | Uma nova lista de produtos (carrinho de compras) foi inicializada ou criada. |
| `commerce.productListRemovals` | Uma ou mais entradas de produto foram removidas de uma lista de produtos ou carrinho de compras. |
| `commerce.productListReopens` | Uma lista de produtos (carrinho de compras) que não estava mais acessível (abandonada) foi reativada por um cliente, como por meio de uma atividade de remarketing. |
| `commerce.productListViews` | Uma lista de produtos ou um carrinho de compras recebeu uma ou mais visualizações. |
| `commerce.productViews` | Um produto recebeu uma ou mais visualizações. |
| `commerce.purchases` | Um pedido foi aceito. Essa é a única ação necessária em uma conversão de comércio. Um evento de compra deve ter uma lista de produtos referida. |
| `commerce.saveForLaters` | Uma lista de produtos foi salva para uso futuro, como uma lista de desejos de produtos. |
| `decisioning.propositionDisplay` | Uma proposta de decisão foi exibida para uma pessoa. |
| `decisioning.propositionInteract` | Uma pessoa interagiu com uma proposta de decisão. |
| `delivery.feedback` | Eventos de feedback para um delivery, como um delivery de email. |
| `directMarketing.emailBounced` | Um email para uma pessoa rejeitado. |
| `directMarketing.emailBouncedSoft` | Um email para uma pessoa rejeitado temporariamente. |
| `directMarketing.emailClicked` | Uma pessoa clicou em um link em um email de marketing. |
| `directMarketing.emailDelivered` | Um email foi entregue com êxito ao serviço de email da pessoa |
| `directMarketing.emailOpened` | Uma pessoa abriu um email de marketing. |
| `directMarketing.emailUnsubscribed` | Uma pessoa cancelou a assinatura de um email de marketing. |
| `inappmessageTracking.dismiss` | Uma mensagem no aplicativo foi descartada. |
| `inappmessageTracking.display` | Uma mensagem no aplicativo foi exibida. |
| `inappmessageTracking.interact` | Uma mensagem no aplicativo recebeu interação. |
| `leadOperation.callWebhook` | Um webhook foi chamado em resposta a um lead. |
| `leadOperation.convertLead` | Um cliente em potencial foi convertido. |
| `leadOperation.interestingMoment` | Registrou-se um momento interessante para uma pessoa. |
| `leadOperation.newLead` | Um cliente em potencial foi criado. |
| `leadOperation.scoreChanged` | O valor do atributo de pontuação do lead foi alterado. |
| `leadOperation.statusInCampaignProgressionChanged` | O status de um lead em uma campanha foi alterado. |
| `listOperation.addToList` | Uma pessoa foi adicionada a uma lista de marketing. |
| `listOperation.removeFromList` | Uma pessoa foi removida de uma lista de marketing. |
| `message.feedback` | Eventos de feedback como enviado/rejeição/erro para mensagens enviadas a um cliente. |
| `message.tracking` | Rastrear eventos como ações abertas/clicadas/personalizadas em mensagens enviadas a um cliente. |
| `opportunityEvent.addToOpportunity` | Uma pessoa foi adicionada a uma oportunidade. |
| `opportunityEvent.opportunityUpdated` | Uma oportunidade foi atualizada. |
| `opportunityEvent.removeFromOpportunity` | Uma pessoa foi removida de uma oportunidade. |
| `pushTracking.applicationOpened` | Uma pessoa abriu um aplicativo a partir de uma notificação por push. |
| `pushTracking.customAction` | Uma pessoa clicou em uma ação personalizada em uma notificação por push. |
| `web.formFilledOut` | Uma pessoa preencheu um formulário em uma página wep. |
| `web.webinteraction.linkClicks` | Um link foi selecionado uma ou mais vezes. |
| `web.webpagedetails.pageViews` | Uma página da Web recebeu uma ou mais exibições. |

{style="table-layout:auto"}

### Valores sugeridos para `producedBy` {#producedBy}

A tabela a seguir descreve alguns valores aceitos para `producedBy`:

| Valor | Definição |
| --- | --- |
| `self` | Auto |
| `system` | Sistema |
| `salesRef` | Representante de Vendas |
| `customerRep` | Representante do Cliente |
