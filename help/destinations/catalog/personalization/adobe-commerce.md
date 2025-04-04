---
title: Conector de destino do Adobe Commerce
description: Saiba como os comerciantes do Adobe Commerce e do Real-Time CDP podem personalizar a experiência de compra fornecendo promoções e conteúdo de site altamente relevantes, personalizados para públicos-alvo de clientes criados e gerenciados no Real-Time CDP.
exl-id: f7aa3c6c-ba7a-440c-a4d7-5d7b50dbbc0d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 4%

---

# Conexão Adobe Commerce {#adobe-commerce}

## Visão geral {#overview}

O conector de destino [!DNL Adobe Commerce] permite que você selecione um ou mais públicos-alvo da Real-Time CDP para ativar em sua conta [!DNL Adobe Commerce] a fim de fornecer uma experiência personalizada dinâmica para seus compradores. Dentro de [!DNL Adobe Commerce], você pode selecionar esses públicos da Real-Time CDP para personalizar ofertas exclusivas no carrinho, como &quot;comprar 2 e receber 1 grátis&quot;. Você também pode exibir banners ilustrativos e modificar os preços do produto por meio de ofertas promocionais, todas personalizadas para os públicos da Adobe Real-Time CDP.

## Pré-requisitos {#prerequisites}

Esse conector está disponível no catálogo de destinos para clientes que compraram o Real-Time CDP Prime ou o Ultimate e o Adobe Commerce.

Para usar essa conexão de destino, verifique se você tem acesso a:

- [Adobe Experience Platform](https://experience.adobe.com/)
- [Adobe Developer Console](https://developer.adobe.com/developer-console/docs/guides/getting-started/). Com acesso ao console do desenvolvedor, você pode exibir as informações de conta de serviço e de credencial necessárias para [concluir a configuração](https://experienceleague.adobe.com/docs/commerce-admin/customers/customers-menu/audience-activation.html#configure-the-extension) da extensão no Adobe Commerce.
- [Adobe Commerce Cloud versão 2.4.4 ou superior](https://business.adobe.com/products/magento/magento-commerce.html)

No Experience Platform, crie o seguinte:

- [Esquema](../../../xdm/schema/composition.md). O esquema criado representa os dados que você planeja assimilar da Adobe Commerce. [Saiba mais](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/fundamentals/update-xdm.html) sobre como criar um esquema que contenha grupos de campos específicos do Commerce.
- [Conjunto de dados](../../../catalog/datasets/user-guide.md#create). Um conjunto de dados é uma construção de armazenamento e gerenciamento para uma coleção de dados. Crie esse conjunto de dados a partir do esquema criado acima.
- [Sequência de dados](../../../datastreams/overview.md#create). ID que permite que os dados fluam do Adobe Experience Platform para outros produtos Adobe DX. Essa ID deve ser associada a um site específico em sua instância específica do Adobe Commerce. Ao criar esse fluxo de dados, especifique o esquema XDM criado acima.

Após concluir os pré-requisitos, conecte-se ao destino [!DNL Commerce].

## Conectar ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa de **[!UICONTROL Exibir Destinos]** e **[!UICONTROL Gerenciar Destinos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.

Para se conectar ao destino [!DNL Adobe Commerce]:

1. Na [interface do Experience Platform](https://experience.adobe.com/platform/), vá para **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]**.
1. Selecione **[!UICONTROL Personalization]**.
1. Selecione o destino do Adobe Commerce para realçá-lo e selecione **[!UICONTROL Configurar]**.
1. Siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md).

### Parâmetros de conexão {#parameters}

Ao [configurar](../../ui/connect-destination.md) este destino, você deve fornecer as seguintes informações:

- **[!UICONTROL Nome]**: preencha o nome preferencial para este destino.
- **[!UICONTROL Descrição]**: insira uma descrição para o seu destino. Por exemplo, você pode mencionar para qual campanha está usando esse destino. Este campo é opcional.
- **[!UICONTROL Alias de integração]**: esse valor é enviado para o Experience Platform Web SDK como um nome de objeto JSON.
- **[!UICONTROL ID da Sequência de Dados]**: determina qual sequência de dados da Coleção de Dados contém os públicos-alvo incluídos na resposta à página. O menu suspenso mostra apenas as sequências de dados com a configuração de destino habilitada. Consulte [Configurando uma sequência de dados](../../../datastreams/overview.md) para obter mais detalhes.

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Avançar]**.

## Ativar públicos para o destino [!DNL Commerce] {#activate}

>[!IMPORTANT]
> 
>Para ativar dados, você precisa de **[!UICONTROL Exibir Destinos]**, **[!UICONTROL Ativar Destinos]**, **[!UICONTROL Exibir Perfis]** e **[!UICONTROL Exibir Segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.

Leia [Ativar perfis e públicos-alvo para destinos de solicitação de perfil](../../ui/activate-edge-personalization-destinations.md) para obter instruções sobre como ativar públicos-alvo para o destino [!DNL Commerce].

## Próximas etapas em [!DNL Adobe Commerce]

Agora que você configurou o destino [!DNL Commerce] no Experience Platform, é necessário instalar a extensão [!DNL Audience Activation] no [!DNL Commerce] e configurar o [!DNL Commerce Admin] para importar os públicos-alvo do Real-Time CDP que você criou. Consulte a [[!DNL Commerce] documentação](https://experienceleague.adobe.com/docs/commerce-admin/customers/customers-menu/audience-activation.html) para saber mais.

## Validar a ativação do público-alvo no Commerce {#exported-data}

Após ativar os públicos da Real-Time CDP na sua conta do [!DNL Adobe Commerce], você verá esses públicos disponíveis ao acessar a barra lateral _Admin_ e, em seguida, acessar **[!UICONTROL Clientes]** > **[!UICONTROL Público-alvo da Real-Time CDP]**.

![Painel de Públicos-Alvo do Real-Time CDP](../../assets/catalog/personalization/adobe-commerce/audience-library.png)

## Uso e governança de dados {#data-usage-governance}

Todos os destinos do [!DNL Adobe Experience Platform] são compatíveis com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como o [!DNL Adobe Experience Platform] fiscaliza a governança de dados, leia a [Visão geral da Governança de Dados](/help/data-governance/home.md).
