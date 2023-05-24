---
title: Criar uma conexão de origem de anúncios do Google na interface
description: Saiba como criar uma conexão de origem do Google Ads usando a interface do usuário do Adobe Experience Platform.
exl-id: 33dd2857-aed3-4e35-bc48-1c756a8b3638
source-git-commit: ac87434c857a39f4be3714cba57519cbb4fa54a6
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 1%

---

# Criar uma conexão de origem do Google Ads na interface

>[!NOTE]
>
>A fonte do Google Ads está na versão beta. Consulte a [Visão geral das fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de fontes rotuladas como beta.

Este tutorial fornece etapas para criar uma conexão de origem do Google Ads usando a interface do usuário do Adobe Experience Platform.

## Introdução

Este tutorial requer um entendimento prático dos seguintes componentes do Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): a estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
   * [Noções básicas da composição do esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os componentes básicos dos esquemas XDM, incluindo princípios fundamentais e práticas recomendadas na composição do esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

Se você já tiver uma conexão válida com o Google Ads, ignore o restante deste documento e prossiga para o tutorial em [configuração de um fluxo de dados](../../dataflow/advertising.md)

### Coletar credenciais necessárias

Para acessar a plataforma da conta do Google Ads, é necessário fornecer os seguintes valores:

| Credencial | Descrição |
| ---------- | ----------- |
| ID de cliente do cliente | A ID do cliente é o número da conta que corresponde à conta do cliente do Google Ads que você deseja gerenciar com a API do Google Ads. Essa ID segue o modelo de `123-456-7890`. |
| ID do cliente de logon | A ID do cliente de logon é o número da conta que corresponde à sua conta de gerente do Google Ads e é usada para buscar dados de relatório de um cliente operacional específico. Para obter mais informações sobre a ID do cliente de logon, leia a [Documentação da API do Google Ads](https://developers.google.com/google-ads/api/docs/migration/login-customer-id). |
| Token do desenvolvedor | O token do desenvolvedor permite acessar a API do Google Ads. Você pode usar o mesmo token do desenvolvedor para fazer solicitações em relação a todas as suas contas do Google Ads. Recupere o token do desenvolvedor até [efetuar login em sua conta de gerente](https://ads.google.com/home/tools/manager-accounts/) e navegue até a página Centro de API. |
| Atualizar token | O token de atualização faz parte de [!DNL OAuth2] autenticação. Esse token permite gerar novamente os tokens de acesso após a expiração. |
| ID do cliente | A ID do cliente é usada em conjunto com o segredo do cliente como parte de [!DNL OAuth2] autenticação. Juntas, a ID do cliente e a senha do cliente permitem que o aplicativo opere em nome da sua conta, identificando o aplicativo na Google. |
| Segredo do cliente | O segredo do cliente é usado em conjunto com a ID do cliente como parte de [!DNL OAuth2] autenticação. Juntas, a ID do cliente e a senha do cliente permitem que o aplicativo opere em nome da sua conta, identificando o aplicativo na Google. |

Leia o documento de visão geral da API para [mais informações sobre a introdução aos anúncios do Google](https://developers.google.com/google-ads/api/docs/first-call/overview).

## Conectar sua conta do Google Ads

Na interface do usuário da Platform, selecione **[!UICONTROL Origens]** na barra de navegação esquerda, para acessar a [!UICONTROL Origens] espaço de trabalho. A variável [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

No **[!UICONTROL Publicidade]** categoria, selecione **[!UICONTROL Anúncios do Google]** e selecione **[!UICONTROL Adicionar dados]**.

![O catálogo de fontes na interface do usuário do Experience Platform.](../../../../images/tutorials/create/ads/catalog.png).

A variável **[!UICONTROL Conectar-se ao Google Ads]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Conta existente

Para conectar uma conta existente, selecione a conta do Google Ads à qual deseja se conectar e selecione **[!UICONTROL Próxima]** para continuar.

![A página de seleção das contas existentes no fluxo de trabalho de origens.](../../../../images/tutorials/create/ads/existing.png).

### Nova conta

Se estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada que aparece, forneça um nome, uma descrição opcional e suas credenciais do Google Ads. Quando terminar, selecione **[!UICONTROL Conectar à origem]** e aguarde algum tempo para estabelecer a nova conexão.

![A nova interface de conta no workflow de origens.](../../../../images/tutorials/create/ads/new.png).

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta do Google Ads. Agora você pode seguir para o próximo tutorial e [configurar um fluxo de dados para trazer dados de publicidade para a Platform](../../dataflow/advertising.md).
