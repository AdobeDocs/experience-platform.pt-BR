---
keywords: segmentação; rtcdp de segmentação; segmentação da plataforma de dados do cliente em tempo real
title: Serviço de segmentação no Real-time Customer Data Platform
description: A CDP em tempo real foi criada sobre a Adobe Experience Platform e utiliza muitos dos serviços e funcionalidades do Experience Platform. Usando o Serviço de segmentação, você pode fornecer marketing personalizado dividindo seus clientes em grupos menores com características semelhantes.
exl-id: 140667c0-e288-40c4-8c45-c275e348b84a
source-git-commit: ad0d38cbd249642d582a807c5679065827f57717
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 0%

---

# [!DNL Segmentation Service] no [!DNL Real-time Customer Data Platform]

[!DNL Real-time Customer Data Platform] (CDP em tempo real) permite trazer dados de várias fontes para gerar uma experiência coordenada e consistente para seus clientes. É possível realizar campanhas de marketing personalizadas relevantes usando o [!DNL Segmentation Service], parte do Adobe Experience Platform.

A CDP em tempo real foi criada sobre a Adobe Experience Platform e utiliza muitos dos [!DNL Experience Platform] serviços e funcionalidade. Usar o [!DNL Segmentation Service], é possível fornecer marketing personalizado dividindo seus clientes em grupos menores com características semelhantes.

## Segmentação

A segmentação é o processo de definir atributos ou comportamentos específicos compartilhados por um subconjunto de perfis do seu armazenamento de perfil para distinguir um grupo comercializável de pessoas da base de clientes. Por exemplo, em uma campanha de email chamada &quot;Você se esqueceu de comprar seus tênis?&quot;, talvez você queira um público-alvo de todos os usuários que procuraram por tênis de corrida nos últimos 30 dias, mas que não concluíram uma compra. Usando segmentos diferentes, você pode se concentrar em vários públicos-alvo, proporcionando uma experiência de marketing mais personalizada.

## [!DNL Segment Builder]

[!DNL Platform] O permite criar e acessar segmentos com facilidade, bem como usar blocos de construção diferentes para caracterizar ainda mais seus segmentos. Para obter mais informações sobre como usar o Construtor de segmentos, leia o [Guia do Construtor de segmentos](./segment-builder-guide.md).

## Customer AI

A Customer AI, incluída no Real-time Customer Data Platform, fornece o poder de gerar previsões de clientes a nível individual com explicações.

Com a ajuda de fatores influentes, a AI do cliente pode informar o que um cliente deve fazer e por quê. Além disso, você pode se beneficiar das previsões e insights do Customer AI para personalizar as experiências do cliente, disponibilizando as ofertas e mensagens mais apropriadas. O Customer AI pode ajudar com:

* Fornecer modelos de propensão do cliente de alta precisão para segmentação e direcionamento mais fortes.
* Entendendo os fatores influentes e a probabilidade por trás de determinados comportamentos do cliente.
* Fornecer opções personalizáveis para os casos de uso e dados exclusivos de sua empresa.
* Aprimoramento do perfil do cliente em tempo real com pontuações de propensão do cliente, como churn e conversão.
* Aprimoramento de perfis de clientes com fatores influentes para pontuações de propensão.
* Criação de segmentos de clientes com base em fatores influentes e pontuações de propensão.

A API do cliente está localizada na seção **[!UICONTROL Serviços]** guia em **[!UICONTROL Serviços da Adobe]**.

![Local do Customer AI](../assets/overview/rtcdp-customer-ai.png)

### Introdução ao Customer AI

Para começar a usar a API do cliente, é necessário seguir o [tutorial de preparação de dados](../../intelligent-services/data-preparation.md) e configure o schema de entrada com base no seu caso de uso. Em seguida, será necessário [configurar uma instância do Customer AI](../../intelligent-services/customer-ai/user-guide/configure.md). Após configurar uma instância, um modelo é gerado, onde você pode [visualizar seus insights e pontuações](../../intelligent-services/customer-ai/user-guide/discover-insights.md). Com os dados gerados a partir do modelo, você pode criar segmentos para a ativação orientada por dados.

Para saber mais sobre a API do cliente, comece visitando o [Visão geral do Customer AI](../../intelligent-services/customer-ai/overview.md). Além disso, o vídeo a seguir mostra como o Customer AI enriquece os perfis do cliente com propensões baseadas em IA e capacita os esforços de segmentação e direcionamento do cliente.

>[!VIDEO](https://video.tv.adobe.com/v/40374/?quality=12&learn=on)


## Próximas etapas

Após ler essa visão geral, você deve entender como a CDP em tempo real utiliza [!DNL Segmentation Service] para aprimorar a personalização e a personalização de campanhas de marketing. Para obter mais informações sobre o [!DNL Segmentation Service]Por favor leia o [Documentação de segmentação](../../segmentation/home.md).
