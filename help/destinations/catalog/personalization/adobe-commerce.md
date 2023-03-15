---
title: Conector de destino do Adobe Commerce
description: Saiba como os comerciantes da Adobe Commerce e da Real-Time CDP podem personalizar a experiência de compra, fornecendo conteúdo e promoções de site altamente relevantes, personalizadas para públicos-alvo de clientes criados e gerenciados no Real-Time CDP.
exl-id: f7aa3c6c-ba7a-440c-a4d7-5d7b50dbbc0d
source-git-commit: 813a564eb02a5366945468ee689b2744e31baaa8
workflow-type: tm+mt
source-wordcount: '720'
ht-degree: 2%

---

# Conexão Adobe Commerce {#adobe-commerce}

## Visão geral {#overview}

O [!DNL Adobe Commerce] o conector de destino permite selecionar um ou mais públicos-alvo do Real-Time CDP para ativar no seu [!DNL Adobe Commerce] conta para fornecer uma experiência personalizada dinâmica para seus compradores. Within [!DNL Adobe Commerce], você pode selecionar esses públicos-alvo da Real-Time CDP para personalizar ofertas exclusivas no carrinho, como &quot;comprar 2 obter 1 grátis&quot;. Você também pode exibir banners de heróis e modificar o preço do produto por meio de ofertas promocionais, tudo personalizado para públicos-alvo da Adobe Real-Time CDP.

## Pré-requisitos {#prerequisites}

Esse conector está disponível no catálogo de destinos para clientes que compraram o Real-Time CDP Prime ou Ultimate e o Adobe Commerce.

Para usar essa conexão de destino, verifique se você tem acesso a:

- [Adobe Experience Platform](https://experience.adobe.com/)
- [Console do desenvolvedor da Adobe](https://developer.adobe.com/developer-console/docs/guides/getting-started/). Com o acesso ao console do desenvolvedor, você pode visualizar as informações da conta de serviço e da credencial necessárias para [concluir a configuração](https://experienceleague.adobe.com/docs/commerce-admin/customers/customers-menu/audience-activation.html#configure-the-extension) da extensão no Adobe Commerce.
- [Adobe Commerce Cloud versão 2.4.4 ou superior](https://business.adobe.com/products/magento/magento-commerce.html)

No Experience Platform, crie o seguinte:

- [Esquema](../../../xdm/schema/composition.md). O esquema criado representa os dados que você planeja assimilar do Adobe Commerce. [Saiba mais](https://experienceleague.adobe.com/docs/commerce-merchant-services/experience-platform-connector/fundamentals/update-xdm.html) sobre como criar um schema que contém grupos de campos específicos de Comércio.
- [Conjunto de dados](../../../catalog/datasets/user-guide.md#create). Um conjunto de dados é uma construção de armazenamento e gerenciamento para uma coleção de dados. Você cria esse conjunto de dados a partir do esquema criado acima.
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
- **[!UICONTROL ID do fluxo de dados]**: Isso determina qual conjunto de dados de Coleta de dados contém os públicos incluídos na resposta à página. O menu suspenso mostra apenas os conjuntos de dados com a configuração de destino ativada. Consulte [Configurar um conjunto de dados](../../../edge/datastreams/overview.md) para obter mais detalhes.

### Ativar alertas {#enable-alerts}

Você pode habilitar alertas para receber notificações sobre o status do fluxo de dados para seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o guia sobre [inscrever-se em alertas de destinos usando a interface do usuário](../../ui/alerts.md).

Quando terminar de fornecer detalhes para a conexão de destino, selecione **[!UICONTROL Próximo]**.

## Ativar públicos-alvo para a [!DNL Commerce] destino {#activate}

>[!IMPORTANT]
> 
>Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]** e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Ler [Ativar perfis e segmentos para destinos de solicitação de perfil](../../ui/activate-profile-request-destinations.md) para obter instruções sobre como ativar públicos-alvo para o [!DNL Commerce] destino.

## Próximas etapas em [!DNL Adobe Commerce]

Agora que você configurou a variável [!DNL Commerce] no Experience Platform, é necessário instalar o [!DNL Audience Activation] extensão em [!DNL Commerce] e configure o [!DNL Commerce Admin] para importar os públicos-alvo do Real-Time CDP criados. Consulte a [[!DNL Commerce] documentação](https://experienceleague.adobe.com/docs/commerce-admin/customers/customers-menu/audience-activation.html) para saber mais.

## Validar a ativação do público-alvo no Commerce {#exported-data}

Depois de ativar os públicos-alvo do Real-Time CDP no [!DNL Adobe Commerce] você verá esses públicos-alvo disponíveis ao acessar a _Administrador_ barra lateral, em seguida, vá para **[!UICONTROL Clientes]** > **[!UICONTROL Público-alvo da CDP em tempo real]**.

![Painel de públicos-alvo da Real-Time CDP](../../assets/catalog/personalization/adobe-commerce/audience-library.png)

## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] Os destinos são compatíveis com as políticas de uso de dados ao manipular os dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] aplica o controle de dados, leia a [Visão geral da governança de dados](/help/data-governance/home.md).
