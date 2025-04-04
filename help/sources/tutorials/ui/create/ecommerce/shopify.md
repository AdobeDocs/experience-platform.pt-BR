---
keywords: Experience Platform;página inicial;tópicos populares;shopify;Shopify
solution: Experience Platform
title: Criar uma conexão do Shopify Source na interface
type: Tutorial
description: Saiba como criar uma conexão de origem do Shopify usando a interface do Adobe Experience Platform.
exl-id: 527cac95-3d9a-4089-98e4-66d746641b85
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 2%

---

# Criar uma conexão de origem [!DNL Shopify] na interface

Os conectores do Source no Adobe Experience Platform fornecem a capacidade de assimilar dados obtidos externamente de forma programada. Este tutorial fornece etapas para a criação de um conector de origem [!DNL Shopify] usando a interface do usuário [!DNL Experience Platform].

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Sistema do Experience Data Model (XDM)](../../../../../xdm/home.md): a estrutura padronizada pela qual o [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas sobre a composição de esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os blocos de construção básicos de esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição de esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

Se você já tiver uma conexão [!DNL Shopify], ignore o restante deste documento e prossiga para o tutorial em [configurando um fluxo de dados para um conector de comércio eletrônico](../../dataflow/ecommerce.md).

### Coletar credenciais necessárias

Para acessar sua conta do [!DNL Shopify] em [!DNL Experience Platform], você deve fornecer os seguintes valores:

| Credencial | Descrição |
| ---------- | ----------- |
| `host` | O ponto final do servidor [!DNL Shopify]. |
| `accessToken` | O token de acesso para sua conta de usuário do [!DNL Shopify]. |

Para obter mais informações sobre a introdução, consulte este [[!DNL Shopify] documento](https://shopify.dev/concepts/about-apis/authentication).

## Conectar sua conta do [!DNL Shopify]

Depois de obter as credenciais necessárias, siga as etapas abaixo para vincular sua conta do [!DNL Shopify] ao [!DNL Experience Platform].

Faça logon em [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar o espaço de trabalho **[!UICONTROL Fontes]**. A tela **[!UICONTROL Catálogo]** exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria **[!UICONTROL comércio eletrônico]**, selecione **[!UICONTROL Shopify]**. Se esta for a primeira vez que você usa este conector, selecione **[!UICONTROL Configurar]**. Caso contrário, selecione **[!UICONTROL Adicionar dados]** para criar um novo conector [!DNL Shopify].

![catálogo](../../../../images/tutorials/create/shopify/catalog.png)

A página **[!UICONTROL Conectar ao Shopify]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se você estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada que aparece, forneça um nome, uma descrição opcional e suas credenciais do [!DNL Shopify]. Quando terminar, selecione **[!UICONTROL Conectar]** e aguarde algum tempo para que a nova conexão seja estabelecida.

![conectar](../../../../images/tutorials/create/shopify/new.png)

### Conta existente

Para conectar uma conta existente, selecione a conta [!DNL Shopify] com a qual deseja se conectar e clique em **[!UICONTROL Avançar]** para continuar.

![existente](../../../../images/tutorials/create/shopify/existing.png)

## Próximas etapas

Seguindo este tutorial, você estabeleceu uma conexão com sua conta do [!DNL Shopify]. Agora você pode seguir para o próximo tutorial e [configurar um fluxo de dados para trazer os dados de comércio eletrônico para o  [!DNL Experience Platform]](../../dataflow/ecommerce.md).
