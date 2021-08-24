---
keywords: destinos, destino, tipos de destino
title: Tipos e categorias de destino
seo-title: Tipos e categorias de destino
description: Saiba mais sobre os diferentes tipos e categorias de destinos no Adobe Experience Platform.
exl-id: 7826d1e2-bd6b-4f65-9da9-0a3b3e8bb93b
source-git-commit: 5a6f14ba65584a6bd61d62c4fb0b46e8f9e8e96d
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---

# Tipos e categorias de destino

Leia esta página para entender os diferentes tipos e categorias de destinos do Adobe Experience Platform.

## Tipos de destino

No Adobe Experience Platform, distinguimos entre dois tipos de destino: conexões e extensões. Há dois tipos de destinos de conexão, Destinos de exportação de perfil e Destinos de exportação de segmento.

![Tipos de destinos](./assets/destination-types/types-of-destinations.png)

## Conexões {#connections}

**[!UICONTROL Perfil]** Exportar e  **[!UICONTROL Streaming de segmentos]** Exportar destinos em dados de evento de captura do Adobe Experience Platform, combiná-los com outras fontes de dados para formar o Perfil do cliente em tempo real [ ](../profile/home.md), aplicar segmentação e exportar segmentos e perfis qualificados para destinos.

## Destinos de exportação de perfil

Os destinos de exportação de perfil recebem dados brutos, geralmente com o endereço de email como a chave primária. Atualmente, o Experience Platform suporta dois tipos de destinos de exportação de perfil:

* [Destinos de exportação de perfil de transmissão](#streaming-profile-export)
* [Destinos baseados em arquivo](#file-based)

### Destinos de exportação de perfil de transmissão {#streaming-profile-export}

Os destinos de exportação de perfil de fluxo recebem dados de segmento e perfil como fluxos de dados de Experience Platform. [O Amazon ](catalog/cloud-storage/amazon-kinesis.md) Kinesisand e o  [Azure Event ](catalog/cloud-storage/azure-event-hubs.md) Hubssão exemplos de tais destinos.

### Destinos baseados em arquivo {#file-based}

Os destinos baseados em arquivo recebem `.csv` arquivos contendo perfis e/ou atributos. [O Amazon S3](catalog/cloud-storage/amazon-s3.md) é um exemplo de destino onde é possível depositar arquivos contendo exportações de perfil.

## Destinos de exportação de segmento de fluxo

Os destinos de exportação de segmento recebem dados de Experience Platform segment. Esses destinos usam IDs de segmento ou IDs de usuário. [[!DNL Google Display & Video 360]](catalog/advertising/google-dv360.md) e  [[!DNL Google Ads]](catalog/advertising/google-ads-destination.md) são exemplos desses destinos.

## Exportar perfis e exportar segmentos - visão geral do vídeo

O vídeo abaixo mostra as particularidades dos dois tipos de destinos:

>[!VIDEO](https://video.tv.adobe.com/v/29707?quality=12)

## Extensões {#extensions}

A Platform aproveita o poder e a flexibilidade do gerenciamento de tags, permitindo configurar extensões de tags na interface do usuário da coleta de dados.

>[!TIP]
>
>Para obter informações detalhadas sobre extensões de tag, incluindo casos de uso e como encontrá-las na interface, consulte a [visão geral das extensões de tag](./catalog/launch-extensions/overview.md).

As extensões de tag encaminham os dados brutos do evento para vários tipos de destinos. Pense nas extensões como um tipo de destino **Encaminhamento de eventos** . Esse é um tipo mais simples de integração com plataformas de destino, que só encaminha dados brutos do evento. Exemplos disso são a [Extensão de personalização do Gainsight](./catalog/personalization/gainsight.md) ou a [Confirmação de voz da extensão do cliente](./catalog/voice/confirmit-digital-feedback.md).

![Extensões de tag em comparação a outros destinos](./assets/common/launch-and-other-destinations.png)

## Quando usar conexões e extensões

Como profissional de marketing, você pode usar uma combinação de conexões e extensões para tratar de seus casos de uso.

As conexões são úteis quando é necessário aproveitar um perfil de cliente centralizado completo ou um segmento de cliente para ativação. Por exemplo, use conexões se estiver unindo dados comportamentais de um sistema analítico com dados de CRM carregados para qualificar um usuário para um determinado segmento antes de fornecer uma mensagem personalizada a esse usuário.

As extensões são úteis quando os dados do evento são usados para acionar uma ação ou para realizar a segmentação em um ambiente externo. Por exemplo, se dados comportamentais precisarem ser encaminhados a um sistema externo sem serem unidos a outras fontes de dados no arquivo para um determinado usuário.

## Categorias de destino

As conexões e extensões no [catálogo de destinos](https://platform.adobe.com/destination/catalog) são agrupadas por categoria de destino (**Advertising**, **Cloud storage**, **Plataformas de pesquisa**, **Email marketing** etc.), dependendo da ação de marketing que ajudam a realizar. Para obter mais informações sobre cada categoria, bem como os destinos incluídos em cada categoria, consulte a [Documentação do catálogo de destinos](./catalog/overview.md).

![Categorias de destino](./assets/destination-types/destination-categories-menu.png)
