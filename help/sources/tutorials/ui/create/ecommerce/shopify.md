---
keywords: Experience Platform;página inicial;tópicos populares;shopify;Shopify
solution: Experience Platform
title: Criar uma conexão de origem do Shopify na interface
type: Tutorial
description: Saiba como criar uma conexão de origem do Shopify usando a interface do Adobe Experience Platform.
exl-id: 527cac95-3d9a-4089-98e4-66d746641b85
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 1%

---

# Criar um [!DNL Shopify] conexão de origem na interface

Os conectores de origem no Adobe Experience Platform fornecem a capacidade de assimilar dados originados externamente de forma programada. Este tutorial fornece etapas para a criação de um [!DNL Shopify] conector de origem usando o [!DNL Platform] interface do usuário.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Sistema do Experience Data Model (XDM)](../../../../../xdm/home.md): o quadro normalizado pelo qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição do esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os componentes básicos dos esquemas XDM, incluindo princípios fundamentais e práticas recomendadas na composição do esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

Se você já tiver uma [!DNL Shopify] conexão, você pode ignorar o restante deste documento e prosseguir para o tutorial em [configuração de um fluxo de dados para um conector de comércio eletrônico](../../dataflow/ecommerce.md).

### Coletar credenciais necessárias

Para acessar seu [!DNL Shopify] conta em [!DNL Platform], você deve fornecer os seguintes valores:

| Credencial | Descrição |
| ---------- | ----------- |
| `host` | O ponto final do [!DNL Shopify] servidor. |
| `accessToken` | O token de acesso do seu [!DNL Shopify] conta de usuário. |

Para obter mais informações sobre a introdução, consulte esta [[!DNL Shopify] documento](https://shopify.dev/concepts/about-apis/authentication).

## Conecte seu [!DNL Shopify] account

Depois de obter as credenciais necessárias, siga as etapas abaixo para vincular [!DNL Shopify] conta para [!DNL Platform].

Efetue logon no [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Origens]** na barra de navegação esquerda, para acessar a **[!UICONTROL Origens]** espaço de trabalho. A variável **[!UICONTROL Catálogo]** A tela exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

No **[!UICONTROL comércio eletrônico]** categoria, selecione **[!UICONTROL Shopify]**. Se esta for a primeira vez que você usa este conector, selecione **[!UICONTROL Configurar]**. Caso contrário, selecione **[!UICONTROL Adicionar dados]** para criar um novo [!DNL Shopify] conector.

![catálogo](../../../../images/tutorials/create/shopify/catalog.png)

A variável **[!UICONTROL Conectar ao Shopify]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada que aparece, forneça um nome, uma descrição opcional e [!DNL Shopify] credenciais. Quando terminar, selecione **[!UICONTROL Conectar]** e aguarde algum tempo para estabelecer a nova conexão.

![conectar](../../../../images/tutorials/create/shopify/new.png)

### Conta existente

Para conectar uma conta existente, selecione a [!DNL Shopify] conta à qual deseja se conectar e selecione **[!UICONTROL Próxima]** para continuar.

![existente](../../../../images/tutorials/create/shopify/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com o seu [!DNL Shopify] conta. Agora você pode seguir para o próximo tutorial e [configurar um fluxo de dados para trazer os dados de comércio eletrônico para o [!DNL Platform]](../../dataflow/ecommerce.md).
