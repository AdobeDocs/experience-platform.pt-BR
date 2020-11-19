---
keywords: Experience Platform;home;popular topics;shopify;Shopify
solution: Experience Platform
title: Criar um conector de origem do Shopify na interface do usuário
topic: overview
type: Tutorial
description: Este tutorial fornece etapas para a criação de um conector de origem do Shopify usando a interface do usuário da plataforma.
translation-type: tm+mt
source-git-commit: bdd80b15258bf4e3c0dee1e260fd3469c76d5885
workflow-type: tm+mt
source-wordcount: '460'
ht-degree: 1%

---


# Criar um conector [!DNL Shopify] de origem na interface do usuário

>[!NOTE]
>
> O [!DNL Shopify] conector está em beta. Consulte a visão geral [das](../../../../home.md#terms-and-conditions) Fontes para obter mais informações sobre o uso de conectores com rótulo beta.

Os conectores de origem na Adobe Experience Platform fornecem a capacidade de assimilar dados de origem externa de forma programada. Este tutorial fornece etapas para criar um conector de [!DNL Shopify] origem usando a interface do [!DNL Platform] usuário.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Sistema](../../../../../xdm/home.md)do Experience Data Model (XDM): A estrutura padronizada pela qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição](../../../../../xdm/schema/composition.md)do schema: Saiba mais sobre os elementos básicos dos schemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)do Editor de schemas: Saiba como criar schemas personalizados usando a interface do editor de Schemas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

Se você já tiver uma [!DNL Shopify] conexão, poderá ignorar o restante desse documento e prosseguir para o tutorial sobre como [configurar um fluxo de dados para um conector](../../dataflow/ecommerce.md)de comércio eletrônico.

### Reunir credenciais obrigatórias

Para acessar sua [!DNL Shopify] conta em [!DNL Platform], forneça os seguintes valores:

| Credencial | Descrição |
| ---------- | ----------- |
| `host` | O ponto final do seu [!DNL Shopify] servidor. |
| `accessToken` | O token de acesso da sua conta [!DNL Shopify] de usuário. |

Para obter mais informações sobre a introdução, consulte este [[!DNL Shopify] documento](https://shopify.dev/concepts/about-apis/authentication).

## Conectar sua [!DNL Shopify] conta

Depois de reunir as credenciais necessárias, siga as etapas abaixo para vincular sua [!DNL Shopify] conta a [!DNL Platform].

Faça logon no [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar a área de trabalho **[!UICONTROL Fontes]** . A tela **[!UICONTROL Catálogo]** exibe várias fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria de **[!UICONTROL comércio eletrônico]** , selecione **[!UICONTROL Shopify (Descobrir]**). Se esta for a sua primeira vez usando este conector, selecione **[!UICONTROL Configurar]**. Caso contrário, selecione **[!UICONTROL Adicionar dados]** para criar um novo [!DNL Shopify] conector.

![catálogo](../../../../images/tutorials/create/shopify/catalog.png)

A página **[!UICONTROL Conectar-se ao Shopify]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se você estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada exibido, forneça um nome, uma descrição opcional e suas [!DNL Shopify] credenciais. Quando terminar, selecione **[!UICONTROL Connect]** e aguarde algum tempo para a nova conexão ser estabelecida.

![connect](../../../../images/tutorials/create/shopify/new.png)

### Conta existente

Para conectar uma conta existente, selecione a [!DNL Shopify] conta à qual deseja se conectar e, em seguida, selecione **[!UICONTROL Avançar]** para continuar.

![existente](../../../../images/tutorials/create/shopify/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua [!DNL Shopify] conta. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para inserir [!DNL Platform]](../../dataflow/ecommerce.md)dados de comércio eletrônico.