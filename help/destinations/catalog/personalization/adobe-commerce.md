---
title: Conector de destino do Adobe Commerce
description: Saiba como os comerciantes do Adobe Commerce e do Real-Time CDP podem personalizar a experiência de compra fornecendo promoções e conteúdo de site altamente relevantes, personalizados para públicos-alvo de clientes criados e gerenciados no Real-Time CDP.
exl-id: f7aa3c6c-ba7a-440c-a4d7-5d7b50dbbc0d
source-git-commit: ba5a539603da656117c95d19c9e989ef0e252f82
workflow-type: tm+mt
source-wordcount: '720'
ht-degree: 3%

---

# Conexão Adobe Commerce {#adobe-commerce}

## Visão geral {#overview}

A variável [!DNL Adobe Commerce] o conector de destino permite selecionar um ou mais públicos-alvo da Real-Time CDP para ativar no [!DNL Adobe Commerce] para fornecer uma experiência personalizada dinâmica aos seus compradores. Dentro de [!DNL Adobe Commerce], você pode selecionar esses públicos da Real-Time CDP para personalizar ofertas exclusivas no carrinho, como &quot;comprar 2 e receber 1 gratuito&quot;. Você também pode exibir banners ilustrativos e modificar os preços do produto por meio de ofertas promocionais, todas personalizadas para os públicos da Adobe Real-Time CDP.

## Pré-requisitos {#prerequisites}

Esse conector está disponível no catálogo de destinos para clientes que compraram o Real-Time CDP Prime ou Ultimate e o Adobe Commerce.

Para usar essa conexão de destino, verifique se você tem acesso a:

- [Adobe Experience Platform](https://experience.adobe.com/)
- [Console do desenvolvedor da Adobe](https://developer.adobe.com/developer-console/docs/guides/getting-started/). Com acesso ao console do desenvolvedor, você pode visualizar as informações da conta de serviço e as credenciais necessárias para [concluir a configuração](https://experienceleague.adobe.com/docs/commerce-admin/customers/customers-menu/audience-activation.html#configure-the-extension) da extensão no Adobe Commerce.
- [Adobe Commerce Cloud versão 2.4.4 ou superior](https://business.adobe.com/products/magento/magento-commerce.html)

No Experience Platform, crie o seguinte:

- [Esquema](../../../xdm/schema/composition.md). O esquema criado representa os dados que você planeja assimilar da Adobe Commerce. [Saiba mais](https://experienceleague.adobe.com/docs/commerce-merchant-services/experience-platform-connector/fundamentals/update-xdm.html) sobre como criar um esquema que contém grupos de campos específicos do Commerce.
- [Conjunto de dados](../../../catalog/datasets/user-guide.md#create). Um conjunto de dados é uma construção de armazenamento e gerenciamento para uma coleção de dados. Crie esse conjunto de dados a partir do esquema criado acima.
- [Sequência de dados](../../../datastreams/overview.md#create). ID que permite que os dados fluam do Adobe Experience Platform para outros produtos Adobe DX. Essa ID deve ser associada a um site específico em sua instância específica do Adobe Commerce. Ao criar esse fluxo de dados, especifique o esquema XDM criado acima.

Após concluir os pré-requisitos, conecte-se à [!DNL Commerce] destino.

## Conectar ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa da variável **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar à [!DNL Adobe Commerce] destino:

1. No [Interface da plataforma](https://experience.adobe.com/platform/), vá para **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]**.
1. Selecionar **[!UICONTROL Personalização]**.
1. Selecione o destino do Adobe Commerce para realçá-lo e selecione **[!UICONTROL Configurar]**.
1. Siga as etapas descritas na seção [tutorial de configuração de destino](../../ui/connect-destination.md).

### Parâmetros de conexão {#parameters}

Enquanto [configuração](../../ui/connect-destination.md) Para esse destino, você deve fornecer as seguintes informações:

- **[!UICONTROL Nome]**: Preencha o nome preferencial para este destino.
- **[!UICONTROL Descrição]**: digite uma descrição para o destino. Por exemplo, você pode mencionar para qual campanha está usando esse destino. Este campo é opcional.
- **[!UICONTROL Alias de integração]**: esse valor é enviado para o SDK da Web do Experience Platform como um nome de objeto JSON.
- **[!UICONTROL ID da sequência de dados]**: determina qual sequência de dados da Coleção de dados contém os públicos-alvo incluídos na resposta à página. O menu suspenso mostra apenas as sequências de dados com a configuração de destino habilitada. Consulte [Configurar um fluxo de dados](../../../datastreams/overview.md) para obter mais detalhes.

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface do](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Próxima]**.

## Ativar públicos-alvo para o [!DNL Commerce] destino {#activate}

>[!IMPORTANT]
> 
>Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]**, e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Ler [Ativar perfis e públicos para destinos de solicitação de perfil](../../ui/activate-edge-personalization-destinations.md) para obter instruções sobre como ativar públicos-alvo para a [!DNL Commerce] destino.

## Próximas etapas em [!DNL Adobe Commerce]

Agora que você configurou o [!DNL Commerce] destino dentro do Experience Platform, é necessário instalar o [!DNL Audience Activation] extensão no [!DNL Commerce] e configure o [!DNL Commerce Admin] para importar os públicos da Real-Time CDP que você criou. Consulte a [[!DNL Commerce] documentação](https://experienceleague.adobe.com/docs/commerce-admin/customers/customers-menu/audience-activation.html) para saber mais.

## Validar ativação de público no Commerce {#exported-data}

Depois de ativar os públicos-alvo da Real-Time CDP para o seu [!DNL Adobe Commerce] conta, você verá esses públicos-alvo disponíveis ao acessar a _Admin_ barra lateral e vá para **[!UICONTROL Clientes]** > **[!UICONTROL Público-alvo da Real-Time CDP]**.

![Painel de públicos-alvo da Real-Time CDP](../../assets/catalog/personalization/adobe-commerce/audience-library.png)

## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] os destinos estão em conformidade com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] fiscaliza a governança de dados, leia o [Visão geral da governança de dados](/help/data-governance/home.md).
