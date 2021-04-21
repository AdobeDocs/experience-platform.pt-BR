---
keywords: Experience Platform, home, tópicos populares, Google AdWords, conector de origem do Google AdWords, conector do google adwords
solution: Experience Platform
title: Criar uma conexão de origem do Google AdWords na interface do usuário
topic-legacy: overview
type: Tutorial
description: Saiba como criar uma conexão de origem do Google AdWords usando a interface do usuário do Adobe Experience Platform.
exl-id: 33dd2857-aed3-4e35-bc48-1c756a8b3638
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 1%

---

# Criar uma conexão de origem [!DNL Google AdWords] na interface do usuário

>[!NOTE]
>
>O conector [!DNL Google AdWords] está em beta. Consulte a [Visão geral das Fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores com marca beta.

Os conectores de origem no Adobe Experience Platform oferecem a capacidade de assimilar dados de origem externa de acordo com a programação. Este tutorial fornece etapas para criar um conector de origem [!DNL Google AdWords] usando a interface do usuário [!DNL Platform].

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): A estrutura padronizada pela qual  [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição](../../../../../xdm/schema/composition.md) do schema: Saiba mais sobre os elementos básicos dos esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md) do Editor de esquema: Saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.

Se você já tiver uma conexão válida [!DNL Google AdWords], poderá ignorar o restante deste documento e prosseguir para o tutorial em [configurar um fluxo de dados](../../dataflow/payments.md)

### Obter credenciais necessárias

Para acessar sua conta [!DNL Google AdWords] [!DNL Platform], você deve fornecer os seguintes valores:

| Credencial | Descrição |
| ---------- | ----------- |
| `clientCustomerId` | A ID do cliente do cliente da conta [!DNL AdWords]. |
| `developerToken` | O token do desenvolvedor associado à conta do gerente. |
| `refreshToken` | O token de atualização obtido de [!DNL Google] para autorizar acesso a [!DNL AdWords]. |
| `clientId` | A ID do cliente do aplicativo [!DNL Google] usada para adquirir o token de atualização. |
| `clientSecret` | O segredo do cliente do aplicativo [!DNL Google] usado para adquirir o token de atualização. |

Para obter mais informações sobre a introdução, consulte este [[!DNL Google AdWords] documento](https://developers.google.com/adwords/api/docs/guides/authentication).

## Conecte sua conta [!DNL Google AdWords]

Depois de coletar suas credenciais necessárias, siga as etapas abaixo para vincular sua conta [!DNL Google AdWords] a [!DNL Platform].

Faça logon em [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Sources]** na barra de navegação esquerda para acessar o espaço de trabalho **[!UICONTROL Sources]**. A tela **[!UICONTROL Catalog]** exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria **[!UICONTROL Advertising]**, selecione **[!UICONTROL Google AdWords]**. Se esta for a primeira vez que você usa esse conector, selecione **[!UICONTROL Configure]**. Caso contrário, selecione **[!UICONTROL Add data]** para criar um novo conector [!DNL Google AdWords].

![catálogo](../../../../images/tutorials/create/ads/catalog.png)

A página **[!UICONTROL Connect to Google AdWords]** é exibida. Nesta página, você pode usar novas credenciais ou credenciais existentes.

### Nova conta

Se estiver usando novas credenciais, selecione **[!UICONTROL New account]**. No formulário de entrada exibido, forneça um nome, uma descrição opcional e suas credenciais [!DNL Google AdWords]. Quando terminar, selecione **[!UICONTROL Connect]** e aguarde algum tempo para que a nova conexão seja estabelecida.

![connect](../../../../images/tutorials/create/ads/connect.png)

### Conta existente

Para conectar uma conta existente, selecione a conta [!DNL Google AdWords] com a qual deseja se conectar e selecione **[!UICONTROL Next]** para prosseguir.

![existente](../../../../images/tutorials/create/ads/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta [!DNL Google AdWords]. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer dados de publicidade para [!DNL Platform]](../../dataflow/advertising.md).
