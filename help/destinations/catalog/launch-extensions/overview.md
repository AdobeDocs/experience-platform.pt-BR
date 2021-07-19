---
keywords: extensões do launch, extensão do launch, destinos do launch; Extensões do platform launch, extensão do platform launch, destinos do platform launch
title: Extensão do Adobe Experience Platform Launch
description: O Adobe Experience Platform Launch reúne os recursos de gerenciamento de tags de última geração da Adobe. O Platform Launch oferece aos clientes uma forma simples de implantar e gerenciar todas as tags de análise, de marketing e de anúncios necessárias para potencializar experiências de cliente relevantes.
exl-id: 54fca635-0e37-460e-abb3-5da294d4e0cf
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 14%

---

# Extensões do Adobe Experience Platform Launch

O Adobe Experience Platform Launch é a próxima geração de recursos de gerenciamento de tags do Adobe. O Platform Launch oferece aos clientes uma forma simples de implantar e gerenciar todas as tags de análise, de marketing e de anúncios necessárias para potencializar experiências de cliente relevantes. O Platform launch é oferecido aos clientes da Adobe Experience Cloud como um recurso incluso com valor agregado.

Para obter uma introdução aos recursos do Experience Platform Launch, consulte os recursos abaixo:

- Adobe Experience Platform Launch [documentação](https://experienceleague.adobe.com/docs/launch/using/home.html?lang=pt-BR)
- Adobe Experience Platform Launch [vídeos de início rápido](../../../tags/quick-start/videos.md). Comece com [Introdução ao Adobe Experience Platform Launch](https://www.youtube.com/embed/rwqqkG1SERU) e [Visão geral do processo de publicação](https://helpx.adobe.com/br/analytics/how-to/adobe-launch-publishing-process.html), em seguida, passe para os próximos conceitos.

## Como encontrar as extensões do Platform launch na interface da plataforma {#how-to-find-extensions-in-interface}

Para localizar as extensões do Platform launch na interface da plataforma, navegue até **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]** e selecione **[!UICONTROL Extensões]** no filtro **[!UICONTROL Tipos]**.

![Filtro de extensões na interface](../../assets/catalog/launch-extensions/filter.png)

## Como funcionam as extensões do Platform launch {#how-extensions-work}

As extensões do Platform launch encaminham os dados brutos do evento para vários tipos de destinos. Pense nas extensões como um tipo de destino **Encaminhamento de eventos** . Esse é um tipo mais simples de integração com plataformas de destino, que só encaminha dados brutos do evento. Exemplos disso são a [Extensão de personalização do Gainsight](../personalization/gainsight.md) ou a [Confirmação de voz da extensão do cliente](../voice/confirmit-digital-feedback.md).

**Perfil/Segmento** Os destinos de exportação no Adobe Experience Platform capturam dados de evento, os combinam com outras fontes de dados, aplicam a segmentação e exportam segmentos e perfis qualificados para destinos. Exemplos disso são o [destino de armazenamento em nuvem do Amazon S3](../cloud-storage/amazon-s3.md) ou o [destino de publicidade do Google Display &amp; Video 360](../advertising/google-dv360.md).

![Extensões de Experience Platform Launch em comparação com outros destinos](../../assets/common/launch-and-other-destinations.png)

## Benefícios do uso de extensões do Platform launch {#extensions-benefits}

A Adobe Experience Platform Launch é gratuita para clientes atuais do Experience Cloud. O Platform launch simplifica a implantação de tags em seu site por meio de extensões fáceis de usar que podem ser instaladas, configuradas, atualizadas e excluídas. O Platform launch tem um pequeno espaço no seu site e permite que você mantenha suas páginas carregadas rapidamente.

>[!IMPORTANT]
>
>Embora não seja possível ativar segmentos para extensões do Platform launch, é possível configurar regras para encaminhar apenas os dados do evento em determinadas situações. Leia mais abaixo.

Você pode criar *regras* que determinam quando encaminhar dados do evento para extensões. Essa funcionalidade avançada permite encaminhar os dados do evento somente em determinadas situações, em vez de enviar os dados do evento em cada interação. Para obter mais informações, leia sobre as regras na [documentação do Adobe Experience Platform Launch](../../../tags/ui/managing-resources/rules.md).

## Exemplo de casos de uso para extensões do Platform launch {#extensions-use-cases}

As extensões do Platform launch permitem atender a vários casos de uso do cliente. Alguns exemplos de casos de uso para usar extensões do Platform launch são:

- Você pode enviar dados de site ou aplicativo nativo para o Facebook por meio da extensão de pixel do Facebook. O facebook Pixel indica para quais partes do site ou aplicativo um visitante navegou, encaminha essas informações para o Facebook e você pode redirecionar seu visitante via Facebook.
- Você pode encaminhar dados de evento de seus sites e aplicativos para o Google Analytics para analisar e tomar decisões com base nesses dados.
- Você pode ativar um aplicativo de caixa de papo no lado do cliente na hora certa com base em como seus usuários estão interagindo com suas páginas, de acordo com as regras configuradas no Platform launch.

## Categorias de extensão {#extension-categories}

As extensões do Platform launch podem se encaixar nas seguintes categorias na Platform:

- [Publicidade](../advertising/overview.md)
- [Analytics](../analytics/overview.md)
- [Plataforma de gerenciamento de dados](../data-management/overview.md)
- [Destinos de marketing por email](../email-marketing/overview.md)
- [Personalização](../personalization/overview.md)
- [Pesquisas](../survey/overview.md)
- [Voz do cliente](../voice/overview.md)
