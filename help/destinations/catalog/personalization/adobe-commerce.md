---
title: (Beta) Conector de destino do Adobe Commerce
description: Saiba como os comerciantes da Adobe Commerce e da Real-Time CDP podem personalizar a experiência de compra, fornecendo conteúdo e promoções de site altamente relevantes, personalizadas para segmentos de clientes criados e gerenciados no Real-Time CDP.
source-git-commit: 51c5458f444220fb526eb9e82417ae6456857de6
workflow-type: tm+mt
source-wordcount: '687'
ht-degree: 2%

---

# Conexão Adobe Commerce (Beta) {#adobe-commerce}

## Visão geral {#overview}

>[!IMPORTANT]
> 
>O **[!UICONTROL Adobe Commerce]** O conector está na versão beta e só está disponível para um número selecionado de clientes.

O [!DNL Adobe Commerce] o conector de destino permite selecionar um ou mais segmentos de Experience Platform para ativar [!DNL Adobe Commerce] conta para fornecer uma experiência personalizada dinâmica para seus compradores. Within [!DNL Adobe Commerce], é possível selecionar esses segmentos do Adobe Experience Platform para personalizar ofertas exclusivas no carrinho, como &quot;comprar 2 obter 1 grátis&quot;. Você também pode exibir banners de heróis e modificar o preço do produto por meio de ofertas promocionais, todas personalizadas para segmentos do Adobe Experience Platform.

<!--## Use cases {#use-cases}

To help you better understand how and when you should use the *YourDestination* destination, here are sample use cases that Adobe Experience Platform customers can solve by using this destination.

### Use case #1 {#use-case-1}

*For mobile messaging platforms:*

*A home rental and sales platform wants to push mobile notifications to customers' Android and iOS devices to let them know that there are 100 updated listings in the area where they previously searched for a rental.*

### Use case #2 {#use-case-2}

*For social network platforms:*

*An athletic apparel brand wants to reach existing customers through their social media accounts. The apparel brand can ingest email addresses from their own CRM to Adobe Experience Platform, build segments from their own offline data, and send these segments to YourDestination, to display ads in their customers' social media feeds.*-->

## Pré-requisitos {#prerequisites}

Essa extensão está disponível no catálogo de destinos para clientes beta selecionados que compraram o Real-time CDP Prime ou o Ultimate e o Adobe Commerce.

Os clientes beta devem ter acesso a:

- [Adobe Experience Platform](https://experience.adobe.com/)
- [Console do desenvolvedor da Adobe](https://developer.adobe.com/developer-console/docs/guides/getting-started/)
- [Adobe Commerce Cloud versão 2.4.3 ou superior](https://business.adobe.com/products/magento/magento-commerce.html)

No Experience Platform, crie o seguinte:

- [Esquema](../../../xdm/schema/composition.md). O esquema criado representa os dados que você planeja assimilar do Adobe Commerce. [Saiba mais](https://experienceleague.adobe.com/docs/commerce-merchant-services/experience-platform-connector/fundamentals/update-xdm.html) sobre como criar um schema que contém grupos de campos específicos de Comércio.
- [Conjunto de dados](../../../catalog/datasets/user-guide.md#create). Um conjunto de dados é uma construção de armazenamento e gerenciamento para uma coleção de dados. Você precisa criar esse conjunto de dados a partir do esquema criado acima.
- [Datastream](../../../edge/datastreams/overview.md#create). ID que permite que os dados fluam do Adobe Experience Platform para outros produtos Adobe DX. Essa ID deve ser associada a um site específico na instância específica do Adobe Commerce. Ao criar esse armazenamento de dados, especifique o esquema XDM criado acima.

Após concluir os pré-requisitos, conecte-se ao [!DNL Commerce] destino.

## Conecte-se ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, é necessário **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar ao [!DNL Adobe Commerce] destino:

1. No [Interface da plataforma](https://experience.adobe.com/platform/), vá para **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]**.
1. Selecionar **[!UICONTROL Personalização]**.
1. Selecione o destino do Adobe Commerce para destacá-lo e, em seguida, selecione **[!UICONTROL Configurar]**.
1. Siga as etapas descritas em [tutorial de configuração de destino](../../ui/connect-destination.md).

### Parâmetros de conexão {#parameters}

Ao [configuração](../../ui/connect-destination.md) nesse destino, você deve fornecer as seguintes informações:

- **[!UICONTROL Nome]**: Preencha o nome preferencial para esse destino.
- **[!UICONTROL Descrição]**: Insira uma descrição para o seu destino. Por exemplo, você pode mencionar para qual campanha está usando esse destino. Este campo é opcional.
- **[!UICONTROL Alias de integração]**: Esse valor é enviado para o SDK da Web do Experience Platform como um nome de objeto JSON.
- **[!UICONTROL ID do fluxo de dados]**: Isso determina em qual conjunto de dados da Coleta de dados os segmentos serão incluídos na resposta à página. O menu suspenso mostra apenas os conjuntos de dados com a configuração de destino ativada. Consulte [Configurar um conjunto de dados](../../../edge/datastreams/overview.md) para obter mais detalhes.

### Ativar alertas {#enable-alerts}

Você pode habilitar alertas para receber notificações sobre o status do fluxo de dados para seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o guia sobre [inscrever-se em alertas de destinos usando a interface do usuário](../../ui/alerts.md).

Quando terminar de fornecer detalhes para a conexão de destino, selecione **[!UICONTROL Próximo]**.

## Ativar segmentos para a [!DNL Commerce] destino {#activate}

>[!IMPORTANT]
> 
>Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]** e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Ler [Ativar perfis e segmentos para destinos de solicitação de perfil](../../ui/activate-profile-request-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para a [!DNL Commerce] destino.

## Próximas etapas em [!DNL Adobe Commerce]

Agora que você configurou a variável [!DNL Commerce] no Experience Platform, é necessário configurar o [!DNL Commerce Admin] para importar os segmentos da CDP em tempo real que você criou. Consulte a [[!DNL Commerce] documentação](https://docs.magento.com/user-guide/marketing/customer-segment-rtcdp.html) para saber mais.

## Validar exportação de dados {#exported-data}

Depois de ativar os segmentos do Real-Time CDP na [!DNL Adobe Commerce] você verá esses segmentos disponíveis na [!DNL Admin] ao criar uma regra de preço do carrinho:

![Administrador do Adobe Commerce](../../assets/catalog/personalization/adobe-commerce/rtcdp-in-admin.png)

## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] Os destinos são compatíveis com as políticas de uso de dados ao manipular os dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] aplica o controle de dados, leia a [Visão geral da governança de dados](/help/data-governance/home.md).
