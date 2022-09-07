---
keywords: Experience Platform, home, tópicos populares, Google Ads, conector de origem do Google Ads, conector do google ads
title: Criar uma conexão de fonte de anúncios do Google na interface do usuário
description: Saiba como criar uma conexão de origem do Google Ads usando a interface do usuário do Adobe Experience Platform.
exl-id: 33dd2857-aed3-4e35-bc48-1c756a8b3638
source-git-commit: 56419f41188c9bfdbeda7dde680f269b980a37f0
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 1%

---

# Criar uma conexão de origem do Google Ads na interface do usuário

>[!NOTE]
>
>A origem dos anúncios do Google está em beta. Consulte a [Visão geral das fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de fontes com rótulo beta.

Este tutorial fornece etapas para criar um conector de origem do Google Ads usando a interface do usuário do Adobe Experience Platform.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): O quadro normalizado pelo qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição do schema](../../../../../xdm/schema/composition.md): Saiba mais sobre os elementos básicos dos esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.

Se você já tiver uma conexão válida do Google Ads, poderá ignorar o restante deste documento e prosseguir para o tutorial em [configuração de um fluxo de dados](../../dataflow/advertising.md)

### Obter credenciais necessárias

Para acessar sua Plataforma de conta do Google Ads, você deve fornecer os seguintes valores:

| Credencial | Descrição |
| ---------- | ----------- |
| ID do cliente | A ID do cliente é o número da conta que corresponde à conta de cliente do Google Ads que você deseja gerenciar com a API do Google Ads. Essa ID segue o modelo de `123-456-7890`. |
| Token do desenvolvedor | O token do desenvolvedor permite acessar a API de anúncios do Google. Você pode usar o mesmo token de desenvolvedor para fazer solicitações em relação a todas as suas contas do Google Ads. Recupere o token do desenvolvedor por [fazer logon em sua conta do gerente](https://ads.google.com/home/tools/manager-accounts/) e navegue até a página do Centro de API. |
| Atualizar token | O token de atualização faz parte de [!DNL OAuth2] autenticação. Esse token permite gerar seus tokens de acesso novamente após expirarem. |
| ID do cliente | A ID do cliente é usada em conjunto com o segredo do cliente como parte de [!DNL OAuth2] autenticação. Juntas, a ID do cliente e o segredo do cliente permitem que o aplicativo opere em nome da sua conta, identificando seu aplicativo para a Google. |
| Segredo do cliente | O segredo do cliente é usado em conjunto com a ID do cliente como parte de [!DNL OAuth2] autenticação. Juntas, a ID do cliente e o segredo do cliente permitem que o aplicativo opere em nome da sua conta, identificando seu aplicativo para a Google. |

Leia o documento de visão geral da API para [mais informações sobre a introdução ao Google Ads](https://developers.google.com/google-ads/api/docs/first-call/overview).

## Conecte sua conta do Google Ads

Na interface do usuário da plataforma, selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar o [!UICONTROL Fontes] espaço de trabalho. O [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Em **[!UICONTROL Publicidade]** categoria , selecione **[!UICONTROL Anúncios do Google]** e selecione **[!UICONTROL Adicionar dados]**.

![Uma imagem da fonte dos anúncios do Google no catálogo de fontes da interface do usuário do Experience Platform](../../../../images/tutorials/create/ads/catalog.png).

O **[!UICONTROL Conectar-se aos anúncios do Google]** será exibida. Nesta página, você pode usar novas credenciais ou credenciais existentes.

### Conta existente

Para conectar uma conta existente, selecione a conta do Google Ads com a qual deseja se conectar e selecione **[!UICONTROL Próximo]** para continuar.

![Uma imagem de uma lista de contas existentes que você pode usar para criar um fluxo de dados do Google Ads com](../../../../images/tutorials/create/ads/existing.png).

### Nova conta

Se estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada exibido, forneça um nome, uma descrição opcional e suas credenciais do Google Ads. Quando terminar, selecione **[!UICONTROL Conectar-se à origem]** e, em seguida, permitir que a nova conexão seja estabelecida.

![Uma imagem da nova tela de conexão da conta na interface do usuário do Experience Platform](../../../../images/tutorials/create/ads/connect.png).

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta do Google Ads. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer dados de publicidade para a plataforma](../../dataflow/advertising.md).
