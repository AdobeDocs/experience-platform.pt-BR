---
title: Tipos de destinos e Categorias
seo-title: Tipos de destinos e Categorias
description: 'Na Platform de dados do cliente em tempo real da Adobe, os destinos de exportação de Perfil/segmento capturam dados do evento, os combinam com outras fontes de dados, aplicam a segmentação e exportam segmentos e perfis qualificados para destinos. Inicie extensões para encaminhar dados brutos do evento a vários tipos de destinos. '
seo-description: Na Platform de dados do cliente em tempo real da Adobe, os destinos de exportação de Perfil/segmento capturam dados do evento, os combinam com outras fontes de dados, aplicam a segmentação e exportam segmentos e perfis qualificados para destinos. Inicie extensões para encaminhar dados brutos do evento a vários tipos de destinos.
translation-type: tm+mt
source-git-commit: 6f680a60c88bc5fee6ce9cb5a4f314c4b9d02249
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 0%

---


# Tipos e Categorias de destino

Leia esta página para entender os diferentes tipos e categorias dos destinos da Platform de dados do cliente em tempo real da Adobe.

## Tipos de destino

Na Adobe Real-time Customer Data Platform, distinguimos entre dois tipos de destino - conexões e extensões. Existem dois tipos de destinos de conexão, destinos de exportação de Perfil e destinos de exportação de segmento.

![Tipos de destinos](/help/rtcdp/destinations/assets/types-of-destinations.png)

<br> 

### Conexões

**[!UICONTROL Exportação]** de Perfis e exportação **[!UICONTROL de]** segmentos nos dados do cliente em tempo real da Adobe A Platform captura dados do evento, combina-os com outras fontes de dados para formar o perfil [do cliente em tempo](/help/profile/home.md)real, aplicar a segmentação e exportar segmentos e perfis qualificados para destinos.

<br> 

#### Destinos de exportação do Perfil

Os destinos de exportação de Perfil geram um arquivo que contém perfis e/ou atributos. Esses destinos usam dados brutos, geralmente com endereço de email como a chave primária. O destino [do armazenamento em nuvem do](/help/rtcdp/destinations/amazon-s3-destination.md) Amazon S3 é um exemplo de destino onde você pode depositar arquivos que contêm exportações de perfis.

#### Destinos de exportação do segmento

Os destinos de exportação do segmento enviam os perfis e os segmentos para os quais eles se qualificaram para plataformas de destino. Esses destinos usam IDs de segmento ou IDs de usuário. Destinos de publicidade como [!DNL Google Display & Video 360](/help/rtcdp/destinations/google-dv360-destination.md) ou [!DNL Google Ads](/help/rtcdp/destinations/google-ads-destination.md) são exemplos desses tipos de destinos.

#### Destinos de exportação de Perfis e segmentos - visão geral do vídeo

O vídeo abaixo mostra as particularidades dos dois tipos de destinos:

>[!VIDEO](https://video.tv.adobe.com/v/29707?quality=12)

<br> 

### Extensões

A CDP em tempo real da Adobe aproveita o poder e a flexibilidade do Experience Platform Launch para incluir extensões de lançamento na interface CDP em tempo real da Adobe.

>[!TIP]
>
>Para obter informações detalhadas sobre extensões de Experience Platform Launch, incluindo casos de uso e como encontrá-las na interface, consulte a visão geral [das extensões de](/help/rtcdp/destinations/experience-platform-launch-extensions.md)lançamento.

Inicie extensões para encaminhar dados brutos do evento a vários tipos de destinos. Pense nas extensões como um tipo de destino de Encaminhamento de **Eventos** . Esse é um tipo mais simples de integração com as plataformas de destino, que apenas encaminha dados brutos do evento. Exemplos disso são a extensão [de personalização](/help/rtcdp/destinations/gainsight-extension.md) Gainsight ou a [Confirmar voz da extensão](/help/rtcdp/destinations/confirmit-digital-feedback-extension.md)Cliente.

![extensões de Experience Platform Launch em relação a outros destinos](/help/rtcdp/destinations/assets/launch-and-other-destinations.png)

<br> 

### Quando usar conexões e extensões

Como profissional de marketing, você pode usar uma combinação de conexões e extensões para resolver seus casos de uso.

As conexões são úteis quando é necessário aproveitar um perfil completo centralizado do cliente ou um segmento do cliente para ativação. Por exemplo, use conexões se estiver unindo dados comportamentais de um sistema analítico com dados de CRM carregados para qualificar um usuário para um determinado segmento antes de fornecer uma mensagem personalizada a esse usuário.

As extensões são úteis quando os dados do evento são usados para acionar uma ação ou para conduzir a segmentação em um ambiente externo. Por exemplo, se dados comportamentais precisarem ser encaminhados para um sistema externo sem que sejam unidos a outras fontes de dados no arquivo para um determinado usuário.

<br> 

## categorias de destino

As conexões e extensões no catálogo [de](https://platform.adobe.com/destination/catalog) destinos são agrupadas por categoria de destino (**Publicidade**, armazenamento **** Cloud, plataformas **de** Pesquisa, marketing **por** email etc.), dependendo do caso de uso de marketing que eles ajudam a atingir. Para obter mais informações sobre cada uma das categorias, bem como sobre os destinos incluídos em cada categoria, consulte a documentação [do catálogo de](/help/rtcdp/destinations/destinations-catalog.md)Destinos.

![categorias de destino](/help/rtcdp/destinations/assets/destination-categories-menu.png)

