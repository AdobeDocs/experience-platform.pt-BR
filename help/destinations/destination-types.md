---
keywords: destinos;destino;destinos tipos;destinations;destination;destination types
title: Tipos e categorias de destino
description: Saiba mais sobre os diferentes tipos e categorias de destinos no Adobe Experience Platform.
exl-id: 7826d1e2-bd6b-4f65-9da9-0a3b3e8bb93b
source-git-commit: d57af88cc9507e0164b044a7203c66fe9fd9240e
workflow-type: tm+mt
source-wordcount: '831'
ht-degree: 1%

---

# Tipos e categorias de destino

Leia esta página para entender os diferentes tipos e categorias de destinos do Adobe Experience Platform.

## Tipos de destino {#destination-types}

No Adobe Experience Platform, distinguimos entre diferentes tipos de destino - conexões, exportações de conjunto de dados e extensões. Há vários tipos de destinos de conexão, permitindo exportar dados para destinos baseados em API, destinos sociais, plataformas de CRM e muito mais.

Por fim, as conexões também podem ser diferenciadas entre destinos públicos disponíveis em todas as organizações no catálogo de destinos e destinos privados que os clientes do Real-Time CDP Ultimate podem criar para atender aos seus casos de uso de exportação específicos.

>[!BEGINSHADEBOX]

![Tipos de diagrama de destinos.](./assets/destination-types/types-of-destinations-no-highlight.png "Diagrama de tipos de destinos."){zoomable="yes"}

>[!ENDSHADEBOX]

## Conexões {#connections}

Os destinos **[!UICONTROL Profile Export]**, **[!UICONTROL Streaming Audience Export]** e **[!DNL Edge Personalization]** na Adobe Experience Platform capturam dados do evento, combinam-nos com outras fontes de dados para formar o [Perfil de cliente em tempo real](../profile/home.md), aplicar a segmentação e exportar públicos-alvo e perfis qualificados para destinos.

## Destinos de exportação de perfil {#profile-export}

Os destinos de exportação de perfil recebem dados brutos, geralmente com o endereço de email como chave primária. Atualmente, o Experience Platform oferece suporte a dois tipos de destinos de exportação de perfis:

* [Destinos em lote (baseados em arquivo)](#file-based)
* [Destinos empresariais avançados (destinos de exportação de perfil de transmissão)](#advanced-enterprise-destinations)

### Destinos empresariais avançados (destinos de exportação de perfil de transmissão) {#advanced-enterprise-destinations}

>[!IMPORTANT]
>
>Destinos corporativos avançados, ou destinos de exportação de perfil de streaming, estão disponíveis somente para clientes do [Adobe Real-Time Customer Data Platform Ultimate](https://helpx.adobe.com/br/legal/product-descriptions/real-time-customer-data-platform.html?lang=pt-BR).

Use os conectores avançados de dados de destino corporativo para fornecer perfis do Adobe Real-Time Customer Data Platform em tempo quase real a sistemas internos ou a outros sistemas de terceiros para sincronização de dados, análise e outros casos de uso de enriquecimento de perfil.

Esses destinos recebem dados de público-alvo e perfil como fluxos de dados do Experience Platform.

Os destinos corporativos avançados incluem:

* [Destino da API HTTP](catalog/streaming/http-destination.md)
* [Amazon Kinesis](catalog/cloud-storage/amazon-kinesis.md)
* [Hubs de eventos do Azure](catalog/cloud-storage/azure-event-hubs.md)
* [Transmissão do Snowflake](catalog/warehouses/snowflake.md)
* [Lote do Snowflake](catalog/warehouses/snowflake-batch.md)

>[!NOTE]
>
>Os destinos do Snowflake estão disponíveis no momento apenas para clientes dos EUA. Se precisar de acesso fora dos EUA, entre em contato com a equipe de conta da Adobe.

### Destinos em lote (baseados em arquivo) {#file-based}

Os destinos baseados em arquivo recebem `.csv` arquivos contendo perfis e/ou atributos. O [Amazon S3](catalog/cloud-storage/amazon-s3.md) é um exemplo de destino onde você pode exportar arquivos contendo exportações de perfil.

## Destinos de exportação de público para transmissão {#streaming-destinations}

Os destinos de exportação de público recebem dados de público do Experience Platform. Esses destinos usam IDs de público-alvo ou IDs de usuário. Advertising e destinos sociais como [[!DNL Google Display & Video 360]](catalog/advertising/google-dv360.md), [[!DNL Google Ads]](catalog/advertising/google-ads-destination.md) ou [Facebook](catalog/social/facebook.md) são exemplos desses destinos.

## Destinos de personalização do Edge {#edge-personalization-destinations}

Os destinos de personalização do Edge no Experience Platform incluem [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) e o [Destino de personalização personalizado](/help/destinations/catalog/personalization/custom-personalization.md). Usando esses destinos, você pode ativar casos de uso de personalização de mesma página e próxima página para seus clientes.

Leia mais sobre como [configurar destinos de personalização para personalização de mesma página e próxima página](/help/destinations/ui/activate-edge-personalization-destinations.md).

## Destinos de exportação de perfil e de público-alvo - visão geral do vídeo {#video}

O vídeo abaixo mostra as particularidades dos dois tipos de destinos:

>[!VIDEO](https://video.tv.adobe.com/v/29707?quality=12)

## Tipos de públicos exportados {#exported-audiences-types}

Você pode exportar três tipos de públicos-alvo do Experience Platform para vários destinos:

* Públicos-alvo de pessoas
* Públicos-alvo da conta
* Públicos-alvo em potencial

Saiba mais sobre os [vários tipos de público-alvo](/help/segmentation/types/account-audiences.md#terminology).

Um símbolo no cartão de destino mostra quais tipos de públicos-alvo você pode exportar para cada destino.

![Exemplo de cartão de destino com símbolos mostrando quais tipos de público-alvo podem ser exportados.](/help/destinations/assets/destination-types/types-of-audiences.png "Exemplo de cartão de destino com símbolos mostrando quais tipos de público-alvo podem ser exportados."){zoomable="yes"}


## Destinos de exportação do conjunto de dados {#dataset-export-destinations}

Alguns destinos de armazenamento em nuvem no catálogo de destinos oferecem suporte a exportações de conjunto de dados. Use esses destinos para exportar conjuntos de dados brutos para locais de armazenamento na nuvem.

Leia mais sobre como [exportar conjuntos de dados](/help/destinations/ui/export-datasets.md).

## Extensões {#extensions}

O Experience Platform aproveita a eficiência e a flexibilidade do gerenciamento de tags, permitindo configurar extensões de tags na interface do usuário.

>[!TIP]
>
>Para obter informações detalhadas sobre extensões de tag, incluindo casos de uso e como encontrá-las na interface, consulte a [visão geral das extensões de tag](./catalog/launch-extensions/overview.md).

As extensões de tag encaminham dados de evento brutos para vários tipos de destinos. Pense nas extensões como um tipo de destino **Encaminhamento de eventos**. Esse é um tipo mais simples de integração com plataformas de destino, que apenas encaminha dados brutos do evento. Exemplos disso são a [Extensão de personalização do Gainsight](./catalog/personalization/gainsight.md) ou a [Voz de confirmação da extensão do cliente](./catalog/voice/confirmit-digital-feedback.md).

![Marcar extensões em comparação a outros destinos](./assets/common/launch-and-other-destinations.png)

## Quando usar conexões e extensões {#when-to-use}

Como profissional de marketing, você pode usar uma combinação de conexões e extensões para lidar com seus casos de uso.

As conexões são úteis quando é necessário aproveitar um perfil de cliente centralizado completo ou um público-alvo de cliente para ativação. Por exemplo, use conexões se estiver unindo dados comportamentais de um sistema de análise com dados de CRM carregados para qualificar um usuário para um determinado público-alvo antes de enviar uma mensagem personalizada para esse usuário.

As extensões são úteis quando os dados do evento são usados para acionar uma ação ou conduzir a segmentação em um ambiente externo. Por exemplo, se os dados comportamentais precisarem ser encaminhados a um sistema externo sem serem unidos a outras fontes de dados no arquivo para um determinado usuário.

## Categorias de destino {#categories}

As conexões e extensões no [catálogo de destinos](https://platform.adobe.com/destination/catalog) são agrupadas por categoria de destino (**Advertising**, **Armazenamento na nuvem**, **Plataformas de pesquisa**, **Marketing por email** etc.), dependendo da ação de marketing que elas ajudam a realizar. Para obter mais informações sobre cada categoria, bem como os destinos incluídos em cada categoria, consulte a [Documentação do catálogo de destinos](./catalog/overview.md).

![Categorias de destino destacadas na página do catálogo.](./assets/destination-types/destination-categories-menu.png "Categorias de destino destacadas na página de catálogo."){zoomable="yes"}
