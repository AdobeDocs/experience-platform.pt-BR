---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Criar um conector de origem HubSpot na interface do usuário
topic: overview
translation-type: tm+mt
source-git-commit: 598b29f681ac930a4e1781f7f298608c8344d807
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 1%

---


# Criar um conector [!DNL HubSpot] de origem na interface do usuário

>[!NOTE]
> O [!DNL HubSpot] conector está em beta. Consulte a visão geral [das](../../../../home.md#terms-and-conditions) Fontes para obter mais informações sobre o uso de conectores com rótulo beta.

Os conectores de origem na Adobe Experience Platform fornecem a capacidade de assimilar dados de origem externa de forma programada. Este tutorial fornece etapas para criar um conector de [!DNL HubSpot] origem usando a interface do [!DNL Platform] usuário.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Sistema](../../../../../xdm/home.md)do Experience Data Model (XDM): A estrutura padronizada pela qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição](../../../../../xdm/schema/composition.md)do schema: Saiba mais sobre os elementos básicos dos schemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)do Editor de schemas: Saiba como criar schemas personalizados usando a interface do editor de Schemas.
* [Perfil](../../../../../profile/home.md)do cliente em tempo real: Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

Se você já tiver uma conexão [!DNL HubSpot] básica, poderá ignorar o restante deste documento e prosseguir para o tutorial sobre como [configurar um fluxo de dados](../../dataflow/marketing-automation.md)de automação de marketing.

### Reunir credenciais obrigatórias

Para acessar sua [!DNL HubSpot] conta em [!DNL Platform], forneça os seguintes valores:

| Credencial | Descrição |
| ---------- | ----------- |
| `clientId` | A ID do cliente associada ao seu [!DNL HubSpot] aplicativo. |
| `clientSecret` | O segredo do cliente associado ao seu [!DNL HubSpot] aplicativo. |
| `accessToken` | O token de acesso obtido ao autenticar inicialmente sua integração OAuth. |
| `refreshToken` | O token de atualização obtido ao autenticar inicialmente sua integração OAuth. |

Para obter mais informações sobre a introdução, consulte este documento [HubSpot](https://developers.hubspot.com/docs/methods/oauth2/oauth2-overview).

## Conectar sua [!DNL HubSpot] conta

Depois de reunir as credenciais necessárias, siga as etapas abaixo para criar uma nova conexão básica de entrada para vincular sua [!DNL HubSpot] conta [!DNL Platform].

Faça logon no [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar a área de trabalho *[!UICONTROL Fontes]* . A tela *[!UICONTROL Catálogo]* exibe várias fontes com as quais você pode criar conexões base de entrada e cada fonte mostra o número de conexões base existentes associadas a elas.

Na categoria *[!UICONTROL de automação]* de marketing, selecione **[!UICONTROL HubSpot]** para expor uma barra de informações no lado direito da tela. A barra de informações fornece uma breve descrição para a fonte selecionada, bem como opções para se conectar à fonte ou à sua documentação de visualização. Para criar uma nova conexão de base de entrada, selecione **[!UICONTROL Adicionar dados]**.

![catálogo](../../../../images/tutorials/create/hubspot/catalog.png)

A página *[!UICONTROL Conectar-se ao HubSpot]* é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se você estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada exibido, forneça um nome, uma descrição opcional e suas [!DNL HubSpot] credenciais à conexão básica. Quando terminar, selecione **[!UICONTROL Connect]** e aguarde algum tempo para a nova conexão básica ser estabelecida.

![connect](../../../../images/tutorials/create/hubspot/connect.png)

### Conta existente

Para conectar uma conta existente, selecione a [!DNL HubSpot] conta à qual deseja se conectar e, em seguida, selecione **[!UICONTROL Avançar]** para continuar.

![existente](../../../../images/tutorials/create/hubspot/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão básica com sua [!DNL HubSpot] conta. Agora você pode continuar com o próximo tutorial e [configurar um fluxo de dados para trazer os dados do sistema de automação de marketing para a Plataforma](../../dataflow/marketing-automation.md).