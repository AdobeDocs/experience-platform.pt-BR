---
title: Ativação expandida do Audience Manager
description: Saiba como ativar públicos-alvo do Audience Manager para destinos sociais e de publicidade, por meio da Ativação expandida do Audience Manager.
source-git-commit: 5bc8d6c7173f221c2830a9b15c8ec6241e8bc59d
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 0%

---


# Ativação expandida do Audience Manager

Integrada no Adobe Experience Platform, a Ativação expandida de Audience Manager ajuda os [Audience Manager](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/aam-home) os usuários ativam os públicos para [social](../destinations/catalog/social/overview.md) e [publicidade](../destinations/catalog/advertising/overview.md) plataformas de destino da Real-Time CDP, como [Facebook](../destinations/catalog/social/facebook.md), [Anúncios do Google](../destinations/catalog/advertising/google-ads-destination.md)e muito mais.

>[!IMPORTANT]
>
>[!DNL Audience Manager Expanded Activation] está disponível somente para [!DNL Audience Manager] usuários.

## Terminologia {#terminology}

A Ativação expandida do Audience Manager usa conceitos e componentes do Adobe Experience Platform. Para entender melhor o fluxo de trabalho de Ativação expandida e os componentes que você usará, verifique se você tem uma compreensão básica dos seguintes conceitos:

* [Públicos-alvo](../segmentation/ui/overview.md): públicos são conjuntos de pessoas que compartilham comportamentos e/ou características semelhantes. Essa coleção de pessoas pode ser gerada pelo Adobe Experience Platform usando definições de segmento ou composição de público-alvo (público-alvo gerado pela Platform) ou de fontes externas, como uploads personalizados (público-alvo gerado externamente). Na Ativação expandida, os segmentos de Audience Manager (públicos-alvo) são importados como [uploads personalizados](../segmentation/ui/overview.md#import-audience).
* [Conectores de origem](../sources/home.md): conectores de origem (também conhecidos como fontes) ajudam os usuários do Experience Platform a assimilar dados de várias fontes, permitindo a estruturação, o rótulo e o aprimoramento de dados usando serviços de Experience Platform. Os dados podem ser assimilados de várias fontes, como armazenamento baseado em nuvem, software de terceiros e sistemas de CRM.
* [Conectores de destino](../destinations/home.md): os destinos descrevem qualquer endpoint, como um aplicativo Adobe, uma plataforma de publicidade, um serviço de armazenamento em nuvem ou um serviço de marketing, em que um público-alvo é ativado e entregue. [!DNL Expanded Activation] O oferece suporte à ativação de públicos-alvo para [publicidade](../destinations/catalog/advertising/overview.md) e [social](../destinations/catalog/social/overview.md) conectores de destino.

## Pré-requisitos {#prerequisites}

Antes de ativar públicos-alvo por meio da Ativação expandida, verifique se você atende aos pré-requisitos descritos abaixo.

### Requisitos de usuário e função {#permission-requirements}

Antes que você possa usar [!DNL Expanded Activation], você deve criar uma conta de usuário do Admin Console e atribuí-la à [!DNL Expanded Activation] função. Consulte a [administração](administration.md) para obter instruções detalhadas sobre como fazer isso.

### Requisitos de público {#audience-requirements}

Para ativar públicos-alvo por meio do [!DNL Expanded Activation], verifique se os públicos-alvo do Audience Manager são baseados em **endereços de email com hash**. Há duas maneiras de garantir isso, com base no uso do Audience Manager:

* Se você estiver usando a variável [Audience Manager Destinos com base em pessoas](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview) , você já estará assimilando endereços de email com hash no Audience Manager. Não há nenhuma etapa adicional que você precise executar neste caso. Você pode pular para [Ativação de públicos-alvo por meio da Ativação expandida](activate-audiences.md).
* Se você estiver _não_ usando o [Audience Manager Destinos com base em pessoas](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview) , você deve criar uma nova fonte de dados no Audience Manager e usá-la para armazenar endereços de email com hash. Consulte a documentação em [configuração de uma fonte de dados para workflows de email com hash](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/features/data-sources/create-data-source-hashed-emails) para saber como fazer isso. Depois de assimilar endereços de email com hash na fonte de dados do Audience Manager, leia a documentação em [Ativação de públicos-alvo por meio da Ativação expandida](activate-audiences.md).

## Próximas etapas {#next-steps}

Agora que você conhece melhor os casos de uso e os benefícios do [!DNL Expanded Activation], start [configuração da sua conta](administration.md) e depois [ativar seus públicos-alvo](activate-audiences.md).

