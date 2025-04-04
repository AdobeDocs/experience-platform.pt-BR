---
title: Ativação expandida do Audience Manager
description: Saiba como ativar públicos-alvo da Audience Manager para destinos sociais e de publicidade, por meio da Ativação estendida do Audience Manager.
exl-id: 1f209578-a688-40b8-8f13-dab0d4380b3b
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 2%

---

# Ativação expandida do Audience Manager

Criada na Adobe Experience Platform, a Ativação Estendida do Audience Manager ajuda os usuários existentes do [Audience Manager](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/aam-home) a ativar os públicos para as plataformas de destino do [social](../destinations/catalog/social/overview.md) e do [advertising](../destinations/catalog/advertising/overview.md) da Real-Time CDP, como o [Facebook](../destinations/catalog/social/facebook.md), o [Google Ads](../destinations/catalog/advertising/google-ads-destination.md) e muito mais.

>[!IMPORTANT]
>
>[!DNL Audience Manager Expanded Activation] está disponível somente para usuários [!DNL Audience Manager] existentes.

## Terminologia {#terminology}

A Ativação expandida do Audience Manager usa conceitos e componentes do Adobe Experience Platform. Para entender melhor o fluxo de trabalho de Ativação expandida e os componentes que você usará, verifique se você tem uma compreensão básica dos seguintes conceitos:

* [Públicos-alvo](../segmentation/ui/overview.md): são conjuntos de pessoas que compartilham comportamentos e/ou características semelhantes. Essa coleção de pessoas pode ser gerada pelo Adobe Experience Platform usando definições de segmento ou composição de público-alvo (público-alvo gerado pela Experience Platform) ou de fontes externas, como uploads personalizados (público-alvo gerado externamente). Na Ativação Estendida, os segmentos (públicos) do Audience Manager são importados como [uploads personalizados](../segmentation/ui/audience-portal.md#import-audience).
* [Conectores do Source](../sources/home.md): os conectores do Source (também conhecidos como fontes) ajudam os usuários da Experience Platform a assimilar dados facilmente de várias fontes, permitindo a estruturação, a rotulagem e o aprimoramento de dados usando os serviços da Experience Platform. Os dados podem ser assimilados de várias fontes, como armazenamento baseado em nuvem, software de terceiros e sistemas de CRM.
* [Conectores de destino](../destinations/home.md): os destinos descrevem qualquer ponto de extremidade, como um aplicativo do Adobe, uma plataforma de publicidade, um serviço de armazenamento na nuvem ou um serviço de marketing, em que um público-alvo é ativado e entregue. [!DNL Expanded Activation] dá suporte à ativação de públicos para os conectores de destino [advertising](../destinations/catalog/advertising/overview.md) e [social](../destinations/catalog/social/overview.md).

## Pré-requisitos {#prerequisites}

Antes de ativar públicos-alvo por meio da Ativação expandida, verifique se você atende aos pré-requisitos descritos abaixo.

### Requisitos de usuário e função {#permission-requirements}

Antes de usar [!DNL Expanded Activation], você deve criar uma conta de usuário do Admin Console e atribuí-la à função [!DNL Expanded Activation]. Consulte a página [administração](administration.md) para obter instruções detalhadas sobre como fazer isso.

### Requisitos de público {#audience-requirements}

Para ativar públicos-alvo por meio do [!DNL Expanded Activation], verifique se seus públicos-alvo da Audience Manager estão baseados em **endereços de email com hash**. Há duas maneiras de garantir isso, com base no uso do Audience Manager:

* Se você estiver usando a funcionalidade [Destinos com base em pessoas do Audience Manager](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview), você já está assimilando endereços de email com hash no Audience Manager. Não há nenhuma etapa adicional que você precise executar neste caso. Você pode pular para [ativação de públicos por meio da Ativação Estendida](activate-audiences.md).
* Se você estiver _não_ usando a funcionalidade [Destinos com base em pessoas do Audience Manager](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview), deverá criar uma nova fonte de dados no Audience Manager e usá-la para armazenar endereços de email com hash. Consulte a documentação sobre [configuração de uma fonte de dados para fluxos de trabalho de email com hash](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/features/data-sources/create-data-source-hashed-emails) para saber como fazer isso. Depois de assimilar endereços de email com hash na fonte de dados do Audience Manager, leia a documentação sobre [ativação de públicos-alvo por meio da Ativação expandida](activate-audiences.md).

## Próximas etapas {#next-steps}

Agora que você conhece melhor os casos de uso e benefícios do [!DNL Expanded Activation], comece [configurando sua conta](administration.md) e [ativando seus públicos](activate-audiences.md).
