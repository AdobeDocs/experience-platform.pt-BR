---
keywords: Experience Platform;home;popular topics;shopify;Shopify;;home;popular topics;shopify;Shopify
solution: Experience Platform
title: Criar uma conexão de origem de compra na interface do usuário
topic: overview
type: Tutorial
description: Saiba como criar uma conexão de origem do Shopify usando a interface do usuário do Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 1%

---


# Criar uma conexão de origem [!DNL Shopify] na interface do usuário

>[!NOTE]
>
> O conector [!DNL Shopify] está em beta. Consulte a [Visão geral das fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores marcados com beta.

Os conectores de origem na Adobe Experience Platform fornecem a capacidade de assimilar dados de origem externa de forma programada. Este tutorial fornece etapas para criar um conector de origem [!DNL Shopify] usando a interface do usuário [!DNL Platform].

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Sistema](../../../../../xdm/home.md) do Experience Data Model (XDM): A estrutura padronizada pela qual  [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição](../../../../../xdm/schema/composition.md) do schema: Saiba mais sobre os elementos básicos dos schemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md) do Editor de schemas: Saiba como criar schemas personalizados usando a interface do editor de Schemas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

Se você já tiver uma conexão [!DNL Shopify], poderá ignorar o restante desse documento e prosseguir para o tutorial em [configurar um fluxo de dados para um conector de comércio eletrônico](../../dataflow/ecommerce.md).

### Reunir credenciais obrigatórias

Para acessar sua conta [!DNL Shopify] em [!DNL Platform], forneça os seguintes valores:

| Credencial | Descrição |
| ---------- | ----------- |
| `host` | O ponto final do servidor [!DNL Shopify]. |
| `accessToken` | O token de acesso da sua conta de usuário [!DNL Shopify]. |

Para obter mais informações sobre a introdução, consulte este [[!DNL Shopify] documento](https://shopify.dev/concepts/about-apis/authentication).

## Conectar sua conta [!DNL Shopify]

Depois de reunir as credenciais necessárias, siga as etapas abaixo para vincular sua conta [!DNL Shopify] a [!DNL Platform].

Faça logon em [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar a área de trabalho **[!UICONTROL Fontes]**. A tela **[!UICONTROL Catalog]** exibe várias fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria **[!UICONTROL eCommerce]**, selecione **[!UICONTROL Shopify]**. Se esta for a sua primeira vez usando este conector, selecione **[!UICONTROL Configurar]**. Caso contrário, selecione **[!UICONTROL Adicionar dados]** para criar um novo conector [!DNL Shopify].

![catálogo](../../../../images/tutorials/create/shopify/catalog.png)

A página **[!UICONTROL Conectar-se ao Shopify]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se você estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada exibido, forneça um nome, uma descrição opcional e suas credenciais [!DNL Shopify]. Quando terminar, selecione **[!UICONTROL Connect]** e aguarde algum tempo para a nova conexão ser estabelecida.

![connect](../../../../images/tutorials/create/shopify/new.png)

### Conta existente

Para conectar uma conta existente, selecione a conta [!DNL Shopify] com a qual você deseja se conectar e selecione **[!UICONTROL Próximo]** para prosseguir.

![existente](../../../../images/tutorials/create/shopify/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta [!DNL Shopify]. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer dados de comércio eletrônico para [!DNL Platform]](../../dataflow/ecommerce.md).