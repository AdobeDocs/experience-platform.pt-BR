---
title: Conector de destino do Adobe Commerce
description: Saiba como os comerciantes do Adobe Commerce e do Real-Time CDP podem personalizar a experiência de compra fornecendo promoções e conteúdo de site altamente relevantes, personalizados para públicos-alvo de clientes criados e gerenciados no Real-Time CDP.
exl-id: f7aa3c6c-ba7a-440c-a4d7-5d7b50dbbc0d
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '818'
ht-degree: 5%

---

# Conexão Adobe Commerce {#adobe-commerce}

## Visão geral {#overview}

Use o conector de destino [!DNL Adobe Commerce] para selecionar um ou mais públicos do [!DNL Real-Time CDP] a serem ativados na sua conta do [!DNL Adobe Commerce] para fornecer uma experiência personalizada dinâmica aos seus compradores. Dentro de [!DNL Adobe Commerce], você pode selecionar esses [!DNL Real-Time CDP] públicos para personalizar ofertas exclusivas no carrinho, como &quot;comprar 2 e receber 1 grátis&quot;. Você também pode exibir banners ilustrativos e modificar os preços dos produtos por meio de ofertas promocionais, tudo personalizado para os públicos-alvo da Adobe [!DNL Real-Time CDP].

## Pré-requisitos {#prerequisites}

Esse conector está disponível no catálogo de destinos para clientes que compraram o [!DNL Real-Time CDP] Prime ou o Ultimate e o Adobe Commerce.

Para usar essa conexão de destino, verifique se você tem acesso a:

- [Adobe Experience Platform](https://experience.adobe.com/)
- [Adobe Developer Console](https://developer.adobe.com/developer-console/docs/guides/getting-started/). Com acesso ao console do desenvolvedor, você pode exibir as informações de conta de serviço e de credencial necessárias para [concluir a configuração](https://experienceleague.adobe.com/docs/commerce-admin/customers/customers-menu/audience-activation.html?lang=pt-BR#configure-the-extension) da extensão no Adobe Commerce.
- [Adobe Commerce versão 2.4.4 ou superior](https://business.adobe.com/br/products/commerce.html)

No Experience Platform, crie o seguinte:

- [Esquema](../../../xdm/schema/composition.md). O esquema criado representa os dados que você planeja assimilar da Adobe Commerce. [Saiba mais](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/fundamentals/update-xdm.html?lang=pt-BR) sobre como criar um esquema que contenha grupos de campos específicos do Commerce.
- [Conjunto de dados](../../../catalog/datasets/user-guide.md#create). Um conjunto de dados é uma construção de armazenamento e gerenciamento para uma coleção de dados. Crie esse conjunto de dados a partir do esquema criado acima.
- [Sequência de dados](../../../datastreams/configure.md#create). ID que permite que os dados fluam do [!DNL Adobe Experience Platform] para outros produtos Adobe DX. Essa ID deve ser associada a um site específico em sua instância específica do Adobe Commerce. Ao criar esse fluxo de dados, especifique o esquema XDM criado acima.

Após concluir os pré-requisitos, conecte-se ao destino [!DNL Commerce].

## Públicos-alvo compatíveis {#supported-audiences}

Esta seção descreve quais tipos de públicos-alvo você pode exportar para esse destino.

| Origem do público | Suportado | Descrição |
|---------|----------|----------|
| [!DNL Segmentation Service] | Sim | Públicos-alvo gerados pelo [Serviço de Segmentação](../../../segmentation/home.md) da Experience Platform. |
| Todas as outras origens de público-alvo | Sim | Esta categoria inclui todas as origens de público-alvo fora dos públicos-alvo gerados pelo [!DNL Segmentation Service]. Leia sobre as [várias origens do público-alvo](/help/segmentation/ui/audience-portal.md#customize). Alguns exemplos incluem: <ul><li> carregar audiências personalizadas [importadas](../../../segmentation/ui/audience-portal.md#import-audience) para o Experience Platform de arquivos CSV,</li><li> públicos-alvo semelhantes, </li><li> públicos federados, </li><li> públicos-alvo gerados em outros aplicativos Experience Platform, como [!DNL Adobe Journey Optimizer], </li><li> e muito mais. </li></ul> |

{style="table-layout:auto"}



Públicos-alvo compatíveis por tipo de dados de público-alvo:

| Tipo de dados de público | Suportado | Descrição | Casos de uso |
|--------------------|-----------|-------------|-----------|
| [Públicos-alvo](/help/segmentation/types/people-audiences.md) | Sim | Com base nos perfis de clientes, permitindo direcionar grupos específicos de pessoas para campanhas de marketing. | Compradores frequentes, abandonadores de carrinho |
| [Públicos-alvo da conta](/help/segmentation/types/account-audiences.md) | Não | Direcione indivíduos em organizações específicas para estratégias de marketing baseadas em conta. | Marketing B2B |
| [Públicos-alvo potenciais](/help/segmentation/types/prospect-audiences.md) | Não | Direcione indivíduos que ainda não são clientes, mas compartilham características com seu público-alvo. | Prospecção com dados de terceiros |
| [Exportações do conjunto de dados](/help/catalog/datasets/overview.md) | Não | Coleções de dados estruturados armazenados no Data Lake [!DNL Adobe Experience Platform]. | Relatórios, fluxos de trabalho de ciência de dados |

{style="table-layout:auto"}


## Conectar ao destino {#connect}

>[!IMPORTANT]
>
>Para se conectar ao destino, você precisa das **[!UICONTROL View Destinations]** e **[!UICONTROL Manage Destinations]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.

Para se conectar ao destino [!DNL Adobe Commerce]:

1. Na [interface do Experience Platform](https://experience.adobe.com/platform/), vá para **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**.
1. Selecione **[!UICONTROL Personalization]**.
1. Selecione o destino do Adobe Commerce para realçá-lo e, em seguida, selecione **[!UICONTROL Set up]**.
1. Siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md).

### Parâmetros de conexão {#parameters}

Ao [configurar](../../ui/connect-destination.md) este destino, você deve fornecer as seguintes informações:

- **[!UICONTROL Name]**: Preencha o nome preferencial para este destino.
- **[!UICONTROL Description]**: insira uma descrição para o seu destino. Por exemplo, você pode mencionar para qual campanha está usando esse destino. Este campo é opcional.
- **[!UICONTROL Integration alias]**: esse valor é enviado para o Experience Platform Web SDK como um nome de objeto JSON.
- **[!UICONTROL Datastream ID]**: isso determina qual sequência de dados da Coleção de dados contém os públicos-alvo incluídos na resposta à página. O menu suspenso mostra apenas as sequências de dados com a configuração de destino habilitada. Consulte [Configurando uma sequência de dados](../../../datastreams/overview.md) para obter mais detalhes.

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Next]**.

## Ativar públicos para o destino [!DNL Commerce] {#activate}

>[!IMPORTANT]
>
>Para ativar dados, você precisa das **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** e **[!UICONTROL View Segments]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.

Leia [Ativar perfis e públicos-alvo para destinos de solicitação de perfil](../../ui/activate-edge-personalization-destinations.md) para obter instruções sobre como ativar públicos-alvo para o destino [!DNL Commerce].

## Próximas etapas em [!DNL Adobe Commerce] {#next-steps-adobe-commerce}

Agora que você configurou o destino [!DNL Commerce] no Experience Platform, é necessário instalar a extensão [!DNL Audience Activation] no [!DNL Commerce] e configurar o [!DNL Commerce Admin] para importar os públicos [!DNL Real-Time CDP] que você criou. Consulte a [[!DNL Commerce] documentação](https://experienceleague.adobe.com/docs/commerce-admin/customers/customers-menu/audience-activation.html?lang=pt-BR) para saber mais.

## Validar a ativação do público-alvo no Commerce {#exported-data}

Após ativar os públicos-alvo do [!DNL Real-Time CDP] na sua conta do [!DNL Adobe Commerce], você verá esses públicos-alvo disponíveis ao acessar a barra lateral do _Admin_ e, em seguida, ao **[!UICONTROL Customers]** > **[!UICONTROL Real-Time CDP Audience]**.

![Painel de Públicos-Alvo do Real-Time CDP](../../assets/catalog/personalization/adobe-commerce/audience-library.png)

## Uso e governança de dados {#data-usage-governance}

Todos os destinos do [!DNL Adobe Experience Platform] são compatíveis com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como o [!DNL Adobe Experience Platform] fiscaliza a governança de dados, leia a [Visão geral da Governança de Dados](/help/data-governance/home.md).
