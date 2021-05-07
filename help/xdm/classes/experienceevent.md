---
keywords: Experience Platform, home, tópicos populares, esquema, esquema, XDM, perfil individual, campos, esquemas, esquemas, Esquemas, identityMap, mapa de identidade, mapa de identidade, design de esquema, mapa, mapa, mapa, esquema de união, união
solution: Experience Platform
title: Classe XDM ExperienceEvent
topic-legacy: overview
description: Este documento fornece uma visão geral da classe XDM ExperienceEvent.
exl-id: a8e59413-b52f-4ea5-867b-8d81088a3321
translation-type: tm+mt
source-git-commit: ab0798851e5f2b174d9f4241ad64ac8afa20a938
workflow-type: tm+mt
source-wordcount: '867'
ht-degree: 1%

---

# [!DNL XDM ExperienceEvent] classe

[!DNL XDM ExperienceEvent] é uma classe XDM padrão que permite criar um instantâneo com carimbo de data e hora do sistema quando um evento específico ocorre ou um determinado conjunto de condições foi atingido.

Um Evento de experiência é um registro de fatos do que ocorreu, incluindo o ponto no tempo e a identidade do indivíduo envolvido. Os eventos podem ser explícitos (ações humanas diretamente observáveis) ou implícitos (criados sem uma ação humana direta) e são registrados sem agregação ou interpretação. Para obter mais informações de alto nível sobre o uso dessa classe no ecossistema da plataforma, consulte a [Visão geral do XDM](../home.md#data-behaviors).

A própria classe [!DNL XDM ExperienceEvent] fornece vários campos relacionados à série de tempo para um esquema. Os valores de alguns desses campos são automaticamente preenchidos quando os dados são assimilados:

<img src="../images/classes/experienceevent.png" width="650" /><br />

| Propriedade | Descrição |
| --- | --- |
| `_id` | Um identificador de string exclusivo gerado pelo sistema para o evento. Este campo é usado para rastrear a exclusividade de um evento individual, evitar a duplicação de dados e buscar esse evento em serviços downstream. Como esse campo é gerado pelo sistema, ele não deve receber um valor explícito durante a assimilação dos dados.<br><br>É importante distinguir que este campo  **não** representa uma identidade relacionada a uma pessoa, mas sim o registro dos dados propriamente ditos. Os dados de identidade relacionados a uma pessoa devem ser relegados para [campos de identidade](../schema/composition.md#identity). |
| `eventMergeId` | A ID do lote assimilado que fez com que o registro fosse criado. Esse campo é preenchido automaticamente pelo sistema após a assimilação de dados. |
| `eventType` | Uma string que indica o tipo de evento principal para o registro. Os valores aceitos e suas definições são fornecidos na seção [apêndice](#eventType). |
| `identityMap` | Campo de mapa que contém um conjunto de identidades namespacadas para o indivíduo ao qual o evento se aplica. Este campo é atualizado automaticamente pelo sistema conforme os dados de identidade são assimilados. Para utilizar corretamente este campo para [Real-time Customer Profile](../../profile/home.md), não tente atualizar manualmente o conteúdo do campo em suas operações de dados.<br /><br />Consulte a seção sobre mapas de identidade nas  [noções básicas da ](../schema/composition.md#identityMap) composição do schema para obter mais informações sobre seu caso de uso. |
| `timestamp` | Um carimbo de data e hora ISO 8601 de quando o evento ocorreu, formatado de acordo com [RFC 3339, Seção 5.6](https://tools.ietf.org/html/rfc3339#section-5.6).<br><br>Esse carimbo de data e hora  **** só pode representar a observação do evento em si e deve ocorrer no passado. Se os casos de uso de segmentação exigirem o uso de carimbos de data e hora que podem ocorrer no futuro (como uma data de partida), esses valores devem ser restritos em outro lugar do esquema Evento de experiência. |

## Grupos de campos de esquema compatíveis {#field-groups}

>[!NOTE]
>
>Os nomes de vários grupos de campos foram alterados. Consulte o documento em [atualizações do nome do grupo de campos](../field-groups/name-updates.md) para obter mais informações.

O Adobe fornece vários grupos de campos padrão para uso com a classe [!DNL XDM ExperienceEvent] . Esta é uma lista de alguns grupos de campos comumente usados para a classe :

* [[!UICONTROL End User ID Details]](../field-groups/event/enduserids.md)
* [[!UICONTROL Environment Details]](../field-groups/event/environment-details.md)

## Apêndice

A seção a seguir contém informações adicionais sobre a classe [!UICONTROL XDM ExperienceEvent].

### Valores aceitos para xdm:eventType {#eventType}

A tabela a seguir descreve os valores aceitos para `xdm:eventType`, juntamente com suas definições:

| Valor | Definição |
| --- | --- |
| `advertising.completes` | Um ativo de mídia cronometrada foi observado até a conclusão. Isso não significa necessariamente que o visualizador assistiu a todo o vídeo, pois o visualizador poderia ter avançado. |
| `advertising.timePlayed` | Descreve a quantidade de tempo gasto por um usuário em um ativo de mídia programado específico. |
| `advertising.federated` | Indica se um evento de experiência foi criado por meio da federação de dados (compartilhamento de dados entre clientes). |
| `advertising.clicks` | Clique em ações em um anúncio. |
| `advertising.conversions` | Ações predefinidas executadas por um cliente que aciona um evento para avaliação de desempenho. |
| `advertising.firstQuartiles` | Um anúncio de vídeo digital executou 25% de sua duração em velocidade normal. |
| `advertising.impressions` | Impressão(ões) de um anúncio para um cliente com o potencial de ser visualizado. |
| `advertising.midpoints` | Um anúncio de vídeo digital tem 50% de sua duração em velocidade normal. |
| `advertising.starts` | Um anúncio de vídeo digital começou a ser reproduzido. |
| `advertising.thirdQuartiles` | Um anúncio de vídeo digital foi reproduzido por 75% de sua duração em velocidade normal. |
| `web.webpagedetails.pageViews` | Uma página da Web recebeu uma ou mais visualizações. |
| `web.webinteraction.linkClicks` | Um link foi selecionado uma ou mais vezes. |
| `commerce.checkouts` | Ocorreu um evento de finalização para uma lista de produtos. Pode haver mais de um evento de check-out se houver várias etapas em um processo de check-out. Se houver várias etapas, o carimbo de data e hora e a página/experiência referenciada para cada evento serão usados para identificar cada evento individual (etapa), representado em ordem. |
| `commerce.productListAdds` | Um produto foi adicionado à lista de produtos ou ao carrinho de compras. |
| `commerce.productListOpens` | Uma nova lista de produtos (carrinho de compras) foi inicializada ou criada. |
| `commerce.productListRemovals` | Uma ou mais entradas de produto foram removidas de uma lista de produtos ou carrinho de compras. |
| `commerce.productListReopens` | Uma lista de produtos (carrinho de compras) que não estava mais acessível (abandonada) foi reativada por um cliente, por exemplo, por meio de uma atividade de re-marketing. |
| `commerce.productListViews` | Uma lista de produtos ou carrinho de compras recebeu uma ou mais visualizações. |
| `commerce.productViews` | Um produto recebeu uma ou mais visualizações. |
| `commerce.purchases` | Um pedido foi aceito. Essa é a única ação necessária em uma conversão de comércio. Um evento de compra deve ter uma lista de produtos referenciada. |
| `commerce.saveForLaters` | Uma lista de produtos foi salva para uso futuro, como uma lista de desejos de produtos. |
| `delivery.feedback` | Eventos de feedback para um delivery, como um delivery de email. |
| `message.feedback` | Eventos de feedback como enviado/rejeição/erro para mensagens enviadas a um cliente. |
| `message.tracking` | Rastreamento de eventos como ações abertas/click/personalizadas em mensagens enviadas a um cliente. |
