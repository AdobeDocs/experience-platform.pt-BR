---
keywords: Experience Platform, home, tópicos populares, paypal, Paypal
solution: Experience Platform
title: Criar uma conexão de origem PayPal na interface do usuário
topic-legacy: overview
type: Tutorial
description: Saiba como criar uma conexão de origem PayPal usando a interface do usuário do Adobe Experience Platform.
exl-id: bbd3f634-cb28-45d8-9b7b-ed3873101882
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 1%

---

# Criar uma conexão de origem [!DNL PayPal] na interface do usuário

>[!NOTE]
>
> O conector [!DNL PayPal] está em beta. Consulte a [Visão geral das Fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores com marca beta.

Os conectores de origem no Adobe Experience Platform oferecem a capacidade de assimilar dados de origem externa de acordo com a programação. Este tutorial fornece etapas para criar um conector de origem [!DNL PayPal] usando a interface do usuário [!DNL Platform].

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): A estrutura padronizada pela qual  [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição](../../../../../xdm/schema/composition.md) do schema: Saiba mais sobre os elementos básicos dos esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md) do Editor de esquema: Saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.

Se você já tiver uma conexão válida [!DNL PayPal], poderá ignorar o restante deste documento e prosseguir para o tutorial em [configurar um fluxo de dados](../../dataflow/payments.md)

### Obter credenciais necessárias

Para acessar sua conta [!DNL PayPal] [!DNL Platform], você deve fornecer os seguintes valores:

| Credencial | Descrição |
| ---------- | ----------- |
| `host` | O URL da instância [!DNL PayPal]. |
| `clientID` | A ID do cliente associada ao aplicativo [!DNL PayPal]. |
| `clientSecret` | O segredo do cliente associado ao seu aplicativo [!DNL PayPal]. |

Para obter mais informações sobre a introdução, consulte este [[!DNL PayPal] documento](https://developer.paypal.com/docs/api/overview/#get-credentials)

## Conecte sua conta [!DNL PayPal]

Depois de coletar suas credenciais necessárias, siga as etapas abaixo para vincular sua conta [!DNL PayPal] a [!DNL Platform].

Faça logon em [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Sources]** na barra de navegação esquerda para acessar o espaço de trabalho **[!UICONTROL Sources]**. A tela **[!UICONTROL Catalog]** exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria **[!UICONTROL Payments]**, selecione **[!UICONTROL PayPal]**. Se esta for a primeira vez que você usa esse conector, selecione **[!UICONTROL Configure]**. Caso contrário, selecione **[!UICONTROL Add data]** para criar um novo conector [!DNL PayPal].

![catálogo](../../../../images/tutorials/create/paypal/catalog.png)

A página **[!UICONTROL Connect to PayPal]** é exibida. Nesta página, você pode usar novas credenciais ou credenciais existentes.

### Nova conta

Se estiver usando novas credenciais, selecione **[!UICONTROL New account]**. No formulário de entrada exibido, forneça um nome, uma descrição opcional e suas credenciais [!DNL PayPal]. Quando terminar, selecione **[!UICONTROL Connect]** e aguarde algum tempo para que a nova conexão seja estabelecida.

![connect](../../../../images/tutorials/create/paypal/connect.png)

### Conta existente

Para conectar uma conta existente, selecione a conta [!DNL PayPal] com a qual deseja se conectar e selecione **[!UICONTROL Next]** para prosseguir.

![existente](../../../../images/tutorials/create/paypal/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta [!DNL PayPal]. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer dados de Pagamento para [!DNL Platform]](../../dataflow/payments.md).
