---
keywords: Experience Platform;home;popular topics;Google AdWords;conector de origem Google AdWords;conector google adwords
solution: Experience Platform
title: Criar uma conexão de origem do Google AdWords na interface do usuário
topic: overview
type: Tutorial
description: Saiba como criar uma conexão de origem do Google AdWords usando a interface do usuário do Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 0%

---


# Criar uma conexão de origem [!DNL Google AdWords] na interface do usuário

>[!NOTE]
>
>O conector [!DNL Google AdWords] está em beta. Consulte a [Visão geral das fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores marcados com beta.

Os conectores de origem na Adobe Experience Platform fornecem a capacidade de assimilar dados de origem externa de forma programada. Este tutorial fornece etapas para criar um conector de origem [!DNL Google AdWords] usando a interface do usuário [!DNL Platform].

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): A estrutura padronizada pela qual  [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição](../../../../../xdm/schema/composition.md) do schema: Saiba mais sobre os elementos básicos dos schemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md) do Editor de schemas: Saiba como criar schemas personalizados usando a interface do editor de Schemas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

Se você já tiver uma conexão válida [!DNL Google AdWords], poderá ignorar o restante desse documento e prosseguir para o tutorial em [configurar um fluxo de dados](../../dataflow/payments.md)

### Reunir credenciais obrigatórias

Para acessar sua conta [!DNL Google AdWords] [!DNL Platform], forneça os seguintes valores:

| Credencial | Descrição |
| ---------- | ----------- |
| `clientCustomerId` | A ID do cliente do cliente da conta [!DNL AdWords]. |
| `developerToken` | O token do desenvolvedor associado à conta do gerente. |
| `refreshToken` | O token de atualização obtido de [!DNL Google] para autorizar o acesso a [!DNL AdWords]. |
| `clientId` | A ID do cliente do aplicativo [!DNL Google] usada para adquirir o token de atualização. |
| `clientSecret` | O segredo do cliente do aplicativo [!DNL Google] usado para adquirir o token de atualização. |

Para obter mais informações sobre a introdução, consulte este [[!DNL Google AdWords] documento](https://developers.google.com/adwords/api/docs/guides/authentication).

## Conectar sua conta [!DNL Google AdWords]

Depois de reunir as credenciais necessárias, siga as etapas abaixo para vincular sua conta [!DNL Google AdWords] a [!DNL Platform].

Faça logon em [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar a área de trabalho **[!UICONTROL Fontes]**. A tela **[!UICONTROL Catalog]** exibe várias fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria **[!UICONTROL Advertising]**, selecione **[!UICONTROL Google AdWords]**. Se esta for a sua primeira vez usando este conector, selecione **[!UICONTROL Configurar]**. Caso contrário, selecione **[!UICONTROL Adicionar dados]** para criar um novo conector [!DNL Google AdWords].

![catálogo](../../../../images/tutorials/create/ads/catalog.png)

A página **[!UICONTROL Conectar-se ao Google AdWords]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se você estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada exibido, forneça um nome, uma descrição opcional e suas credenciais [!DNL Google AdWords]. Quando terminar, selecione **[!UICONTROL Connect]** e aguarde algum tempo para a nova conexão ser estabelecida.

![connect](../../../../images/tutorials/create/ads/connect.png)

### Conta existente

Para conectar uma conta existente, selecione a conta [!DNL Google AdWords] com a qual você deseja se conectar e selecione **[!UICONTROL Próximo]** para prosseguir.

![existente](../../../../images/tutorials/create/ads/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta [!DNL Google AdWords]. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer dados de publicidade para [!DNL Platform]](../../dataflow/advertising.md).