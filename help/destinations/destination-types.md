---
keywords: destinos;destino;tipos de destino
title: Tipos de destino e categorias
seo-title: Tipos de destino e categorias
description: Saiba mais sobre os diferentes tipos e categorias de destinos no Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: e13a19640208697665b0a7e0106def33fd1e456d
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 0%

---


# Tipos de destino e categorias

Leia esta página para entender os diferentes tipos e categorias de destinos do Adobe Experience Platform.

## Tipos de destino

No Adobe Experience Platform, fazemos a distinção entre dois tipos de destino - conexões e extensões. Existem dois tipos de destinos de conexão, destinos de exportação de Perfil e destinos de exportação de segmento.

![Tipos de destinos](./assets/destination-types/types-of-destinations.png)

### Conexões {#connections}

**[!UICONTROL Os destinos]** Exportações e  **[!UICONTROL Segmentos de]** Exportações de perfis no Adobe Experience Platform capturam os dados do evento, combinam-nos com outras fontes de dados para formar o Perfil [ Cliente em tempo ](../profile/home.md)real, aplicar a segmentação e exportar segmentos e perfis qualificados para destinos.

#### Destinos de exportação do perfil

Os destinos de exportação de perfil geram um arquivo que contém perfis e/ou atributos. Esses destinos usam dados brutos, geralmente com endereço de email como a chave primária. O [destino do armazenamento em nuvem do Amazon S3](./catalog/cloud-storage/amazon-s3.md) é um exemplo de destino onde você pode depositar arquivos que contêm exportações de perfis.

#### Destinos de exportação do segmento

Os destinos de exportação do segmento enviam os perfis e os segmentos para os quais eles se qualificaram para plataformas de destino. Esses destinos usam IDs de segmento ou IDs de usuário. Os destinos de publicidade como [[!DNL Google Display & Video 360]](./catalog/advertising/google-dv360.md) ou [[!DNL Google Ads]](./catalog/advertising/google-ads-destination.md) são exemplos desses tipos de destinos.

#### Destinos de exportação de perfis e segmentos - visão geral do vídeo

O vídeo abaixo mostra as particularidades dos dois tipos de destinos:

>[!VIDEO](https://video.tv.adobe.com/v/29707?quality=12)

### Extensões {#extensions}

A plataforma aproveita o poder e a flexibilidade da Adobe Experience Platform Launch para incluir extensões de lançamento de plataforma na interface da plataforma.

>[!TIP]
>
>Para obter informações detalhadas sobre extensões do Adobe Experience Platform Launch, incluindo casos de uso e como encontrá-las na interface, consulte a [visão geral das extensões do Adobe Experience Platform Launch](./catalog/launch-extensions/overview.md).

As extensões de lançamento de plataforma encaminham os dados brutos do evento para vários tipos de destinos. Pense nas extensões como um tipo de destino **Encaminhamento de Eventos**. Esse é um tipo mais simples de integração com as plataformas de destino, que apenas encaminha dados brutos do evento. Exemplos disso são a [extensão de personalização Gainsight](./catalog/personalization/gainsight.md) ou a [Confirmação de voz da extensão do cliente](./catalog/voice/confirmit-digital-feedback.md).

![extensões de Experience Platform Launch em relação a outros destinos](./assets/common/launch-and-other-destinations.png)

### Quando usar conexões e extensões

Como profissional de marketing, você pode usar uma combinação de conexões e extensões para resolver seus casos de uso.

As conexões são úteis quando é necessário aproveitar um perfil completo centralizado do cliente ou um segmento do cliente para ativação. Por exemplo, use conexões se estiver unindo dados comportamentais de um sistema analítico com dados de CRM carregados para qualificar um usuário para um determinado segmento antes de fornecer uma mensagem personalizada a esse usuário.

As extensões são úteis quando os dados do evento são usados para acionar uma ação ou para conduzir a segmentação em um ambiente externo. Por exemplo, se dados comportamentais precisarem ser encaminhados para um sistema externo sem que sejam unidos a outras fontes de dados no arquivo para um determinado usuário.

## Categorias de destino

As conexões e extensões no catálogo de [destinos](https://platform.adobe.com/destination/catalog) são agrupadas por categoria de destino (**Publicidade**, **armazenamento da nuvem**, **plataformas de Pesquisa**, **Marketing por email**, etc.), dependendo do caso de uso de marketing que eles ajudam a realizar. Para obter mais informações sobre cada uma das categorias, bem como sobre os destinos incluídos em cada categoria, consulte a [Documentação do catálogo de destinos](./catalog/overview.md).

![Categorias de destino](./assets/destination-types/destination-categories-menu.png)

