---
keywords: Experience Platform, home, tópicos populares, shopify, Shopify
solution: Experience Platform
title: Criar uma conexão de origem de compra na interface do usuário
topic: visão geral
type: Tutorial
description: Saiba como criar uma conexão de origem do Shopify usando a interface do usuário do Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: cc23228cb410dc4c70a56c5142be00c2ca1c40d3
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 1%

---


# Criar uma conexão de origem [!DNL Shopify] na interface do usuário

Os conectores de origem no Adobe Experience Platform oferecem a capacidade de assimilar dados de origem externa de acordo com a programação. Este tutorial fornece etapas para criar um conector de origem [!DNL Shopify] usando a interface do usuário [!DNL Platform].

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Sistema](../../../../../xdm/home.md) do Experience Data Model (XDM): A estrutura padronizada pela qual  [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição](../../../../../xdm/schema/composition.md) do schema: Saiba mais sobre os elementos básicos dos esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md) do Editor de esquema: Saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.

Se você já tiver uma conexão [!DNL Shopify], poderá ignorar o restante deste documento e prosseguir para o tutorial em [configurar um fluxo de dados para um conector de eCommerce](../../dataflow/ecommerce.md).

### Obter credenciais necessárias

Para acessar sua conta [!DNL Shopify] em [!DNL Platform], você deve fornecer os seguintes valores:

| Credencial | Descrição |
| ---------- | ----------- |
| `host` | O ponto final do seu servidor [!DNL Shopify]. |
| `accessToken` | O token de acesso para sua conta de usuário [!DNL Shopify]. |

Para obter mais informações sobre a introdução, consulte este [[!DNL Shopify] documento](https://shopify.dev/concepts/about-apis/authentication).

## Conecte sua conta [!DNL Shopify]

Depois de coletar suas credenciais necessárias, siga as etapas abaixo para vincular sua conta [!DNL Shopify] a [!DNL Platform].

Faça logon em [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Sources]** na barra de navegação esquerda para acessar o espaço de trabalho **[!UICONTROL Sources]**. A tela **[!UICONTROL Catalog]** exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria **[!UICONTROL eCommerce]**, selecione **[!UICONTROL Shopify]**. Se esta for a primeira vez que você usa esse conector, selecione **[!UICONTROL Configure]**. Caso contrário, selecione **[!UICONTROL Add data]** para criar um novo conector [!DNL Shopify].

![catálogo](../../../../images/tutorials/create/shopify/catalog.png)

A página **[!UICONTROL Connect to Shopify]** é exibida. Nesta página, você pode usar novas credenciais ou credenciais existentes.

### Nova conta

Se estiver usando novas credenciais, selecione **[!UICONTROL New account]**. No formulário de entrada exibido, forneça um nome, uma descrição opcional e suas credenciais [!DNL Shopify]. Quando terminar, selecione **[!UICONTROL Connect]** e aguarde algum tempo para que a nova conexão seja estabelecida.

![connect](../../../../images/tutorials/create/shopify/new.png)

### Conta existente

Para conectar uma conta existente, selecione a conta [!DNL Shopify] com a qual deseja se conectar e selecione **[!UICONTROL Next]** para prosseguir.

![existente](../../../../images/tutorials/create/shopify/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta [!DNL Shopify]. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer dados do eCommerce para  [!DNL Platform]](../../dataflow/ecommerce.md).