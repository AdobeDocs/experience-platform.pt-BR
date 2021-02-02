---
keywords: segmentação; segmentação rtcdp;segmentação da plataforma de dados do cliente em tempo real
title: Visão geral do serviço de segmentação
seo-title: Serviço de segmentação na plataforma de dados do cliente em tempo real
description: A CDP em tempo real foi desenvolvida sobre a Adobe Experience Platform e utiliza muitos dos serviços e funcionalidades do Experience Platform. Usando o Serviço de segmentação, você pode fornecer marketing feito sob medida dividindo seus clientes em grupos menores com características semelhantes.
translation-type: tm+mt
source-git-commit: 9f20f8bfeefb5bc427a72a11ac1f01816cdbc4b2
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 0%

---


# [!DNL Segmentation Service] in [!DNL Real-time Customer Data Platform]

[!DNL Real-time Customer Data Platform] (CDP em tempo real) permite trazer dados de várias fontes para gerar uma experiência coordenada e consistente para seus clientes. É possível obter campanhas de marketing personalizadas relevantes usando [!DNL Segmentation Service], parte da Adobe Experience Platform.

A CDP em tempo real foi desenvolvida sobre a Adobe Experience Platform e utiliza muitos dos [!DNL Experience Platform] serviços e funcionalidades. Usando o [!DNL Segmentation Service], você pode fornecer marketing feito sob medida dividindo seus clientes em grupos menores com características semelhantes.

## Segmentação

A segmentação é o processo de definição de atributos ou comportamentos específicos compartilhados por um subconjunto de perfis da sua loja de perfis para diferenciar um grupo comercializável de pessoas da sua base de clientes. Por exemplo, em uma campanha de email chamada &quot;Você esqueceu de comprar seus tênis?&quot;, você pode querer uma audiência de todos os usuários que procuraram tênis de corrida nos últimos 30 dias, mas que não concluíram uma compra. Usando diferentes segmentos, você pode se concentrar em suas várias audiências, oferecendo uma experiência de marketing mais personalizada.

## [!DNL Segment Builder]

[!DNL Platform] permite que você crie e acesse segmentos com facilidade, bem como use blocos de construção diferentes para caracterizar ainda mais seus segmentos. Para obter mais informações sobre como usar o Construtor de segmentos, leia o [guia do Construtor de segmentos](./segment-builder-guide.md).

## AI do cliente

A IA do cliente, incluída na Plataforma de dados do cliente em tempo real, fornece a você o poder de gerar previsões do cliente em nível individual com explicações.

Com a ajuda de fatores influentes, a IA do cliente pode informar o que um cliente deve fazer e por que. Além disso, você pode se beneficiar das previsões e insights de IA do cliente para personalizar as experiências do cliente, atendendo às ofertas e mensagens mais apropriadas. A IA do cliente pode ajudar com:

* Fornecer modelos de propensão do cliente de alta precisão para segmentação e direcionamento mais fortes.
* Entendendo os fatores influentes e a probabilidade por trás de determinados comportamentos de clientes.
* Fornecer opções personalizáveis para os casos e dados de uso exclusivos da sua empresa.
* Aprimorando o Perfil do cliente em tempo real com as pontuações de propensão do cliente, como taxa de processamento e conversão.
* Aprimoramento dos perfis do cliente com fatores influentes para as pontuações de propensão.
* Criação de segmentos de clientes com base em fatores influentes e pontuações de propensão.

A API do cliente está localizada na guia **[!UICONTROL Serviços]** em **[!UICONTROL serviços do Adobe]**.

![Local da IA do cliente](../assets/overview/rtcdp-customer-ai.png)

### Introdução à IA do cliente

Para começar a usar a API do cliente, é necessário seguir o [tutorial de preparação de dados](../../intelligent-services/data-preparation.md) e configurar o schema de entrada com base no caso de uso. Em seguida, será necessário [configurar uma instância do AI do cliente](../../intelligent-services/customer-ai/user-guide/configure.md). Depois de configurar uma instância, um modelo é gerado onde você pode [visualização seus insights e pontuações](../../intelligent-services/customer-ai/user-guide/discover-insights.md). Usando os dados gerados a partir do seu modelo, é possível criar segmentos para a ativação orientada por dados.

Para saber mais sobre a IA do cliente, visite a [visão geral do AI do cliente](../../intelligent-services/customer-ai/overview.md). Além disso, o vídeo a seguir mostra como a Inteligência Artificial do Cliente enriquece os perfis do cliente com propensões baseadas em IA e capacita a segmentação e os esforços de definição de metas do cliente.

>[!VIDEO](https://video.tv.adobe.com/v/40374/?quality=12&learn=on)


## Próximas etapas

Depois de ler essa visão geral, agora você deve entender como a CDP em tempo real utiliza [!DNL Segmentation Service] para aprimorar a personalização e a personalização das campanhas de marketing. Para obter mais informações sobre [!DNL Segmentation Service], leia a [documentação de Segmentação](../../segmentation/home.md).
