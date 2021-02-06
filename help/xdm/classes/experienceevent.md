---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;perfil individual;campos;schemas;Schemas;identityMap;identity map;Identity map;Schema design;map;Map;união schema;união
solution: Experience Platform
title: Classe XDM ExperienceEvent
topic: overview
description: Este documento fornece uma visão geral da classe ExperienceEvent do XDM.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 1%

---


# [!DNL XDM ExperienceEvent] classe

[!DNL XDM ExperienceEvent] é uma classe XDM padrão que permite criar um instantâneo com carimbo de data e hora do sistema quando ocorre um evento específico ou quando um determinado conjunto de condições é atingido.

Um Evento de experiência é um registro de fatos do que ocorreu, incluindo o momento e a identidade do indivíduo envolvido. Os eventos podem ser explícitos (ações humanas diretamente observáveis) ou implícitos (criados sem uma ação humana direta) e são registrados sem agregação ou interpretação. Para obter mais informações de alto nível sobre o uso dessa classe no ecossistema da plataforma, consulte a [visão geral do XDM](../home.md#data-behaviors).

A classe [!DNL XDM ExperienceEvent] em si fornece vários campos relacionados a séries de tempo para um schema. Os valores de alguns desses campos são automaticamente preenchidos quando os dados são assimilados:

<img src="../images/classes/experienceevent.png" width="650" /><br />

| Propriedade | Descrição |
| --- | --- |
| `_id` | Um identificador exclusivo de sequência gerado pelo sistema para o evento. Este campo é usado para rastrear a singularidade de um evento individual, evitar a duplicação de dados e buscar esse evento em serviços de downstream. Como esse campo é gerado pelo sistema, ele não deve receber um valor explícito durante a ingestão dos dados.<br><br>É importante distinguir que este campo  **não** representa uma identidade relacionada com uma pessoa individual, mas sim o registro dos próprios dados. Os dados de identidade relacionados a uma pessoa devem ser relegados para [campos de identidade](../schema/composition.md#identity). |
| `eventMergeId` | A ID do lote ingerido que fez com que o registro fosse criado. Esse campo é automaticamente preenchido pelo sistema após a ingestão dos dados. |
| `eventType` | Uma string que indica o tipo de evento primário do registro. Os valores aceitos e suas definições são fornecidos na seção [apêndice](#eventType). |
| `identityMap` | Um campo de mapa que contém um conjunto de identidades namespacadas para o indivíduo ao qual o evento se aplica. Este campo é atualizado automaticamente pelo sistema à medida que os dados de identidade são assimilados. Para utilizar adequadamente este campo para [Perfil do cliente em tempo real](../../profile/home.md), não tente atualizar manualmente o conteúdo do campo em suas operações de dados.<br /><br />Consulte a seção sobre mapas de identidade nas  [noções básicas de ](../schema/composition.md#identityMap) composição de schemas para obter mais informações sobre o caso de uso. |
| `timestamp` | A hora em que ocorreu o evento ou observação, formatada de acordo com [RFC 3339, seção 5.6](https://tools.ietf.org/html/rfc3339#section-5.6)). |

## Misturas compatíveis {#mixins}

>[!NOTE]
>
>Os nomes de várias misturas mudaram. Consulte o documento em [mixin name updates](../mixins/name-updates.md) para obter mais informações.

O Adobe fornece várias combinações padrão para uso com a classe [!DNL XDM ExperienceEvent]. A seguir está uma lista de algumas combinações comumente usadas para a classe:

* [[!UICONTROL Detalhes da ID do usuário final]](../mixins/event/enduserids.md)
* [[!UICONTROL Detalhes do ambiente]](../mixins/event/environment-details.md)

## Apêndice

A seção a seguir contém informações adicionais sobre a classe [!UICONTROL XDM ExperienceEvent].

### Valores aceitos para xdm:eventType {#eventType}

A tabela a seguir descreve os valores aceitos para `xdm:eventType`, juntamente com suas definições:

| Valor | Definição |
| --- | --- |
| `advertising.completes` | Um ativo de mídia cronometrado foi observado até a conclusão. Isso não significa necessariamente que o visualizador assistiu o vídeo inteiro, pois o visualizador poderia ter pulado para frente. |
| `advertising.timePlayed` | Descreve a quantidade de tempo gasta por um usuário em um ativo de mídia cronometrado específico. |
| `advertising.federated` | Indica se um Evento da Experiência foi criado por meio da federação de dados (compartilhamento de dados entre clientes). |
| `advertising.clicks` | Clique em ações em um anúncio. |
| `advertising.conversions` | Ação(ões) predefinida(s) executada(s) por um cliente que aciona um evento para avaliação do desempenho. |
| `advertising.firstQuartiles` | Um anúncio de vídeo digital tem uma duração de 25% em velocidade normal. |
| `advertising.impressions` | Impressão(ões) de um anúncio para um cliente com o potencial de ser visualizado. |
| `advertising.midpoints` | Um anúncio de vídeo digital tem uma duração de 50% em velocidade normal. |
| `advertising.starts` | Um anúncio de vídeo digital começou a ser reproduzido. |
| `advertising.thirdQuartiles` | Um anúncio de vídeo digital tem uma duração de 75% em velocidade normal. |
| `web.webpagedetails.pageViews` | Uma página da Web recebeu uma ou mais visualizações. |
| `web.webinteraction.linkClicks` | Um link foi selecionado uma ou mais vezes. |
| `commerce.checkouts` | Ocorreu um evento de finalização para uma lista de produto. Pode haver mais de um evento de finalização se houver várias etapas em um processo de finalização. Se houver várias etapas, o carimbo de data e hora e a página/experiência referenciada para cada evento serão usados para identificar cada evento individual (etapa), representado em ordem. |
| `commerce.productListAdds` | Um produto foi adicionado à lista do produto ou ao carrinho de compras. |
| `commerce.productListOpens` | Uma nova lista de produto (carrinho de compras) foi inicializada ou criada. |
| `commerce.productListRemovals` | Uma ou mais entradas de produto foram removidas de uma lista de produto ou carrinho de compras. |
| `commerce.productListReopens` | Uma lista de produto (carrinho de compras) que não estava mais acessível (abandonada) foi reativada por um cliente, como por meio de uma atividade de recomercialização. |
| `commerce.productListViews` | Uma lista de produto ou carrinho de compras recebeu uma ou mais visualizações. |
| `commerce.productViews` | Um produto recebeu uma ou mais visualizações. |
| `commerce.purchases` | Um pedido foi aceito. Esta é a única ação necessária em uma conversão de comércio. Um evento purchase deve ter uma lista de produto referenciada. |
| `commerce.saveForLaters` | Uma lista de produto foi salva para uso futuro, como uma lista de desejos de produto. |
| `delivery.feedback` | Eventos de feedback para um delivery, como um delivery de email. |
| `message.feedback` | Eventos de feedback como send/bounce/error para mensagens enviadas a um cliente. |
| `message.tracking` | Rastrear eventos como ações abertas/clicadas/personalizadas em mensagens enviadas a um cliente. |