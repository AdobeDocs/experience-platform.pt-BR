---
title: Criar uma conexão do Google Ads Source na interface
description: Saiba como criar uma conexão de origem do Google Ads usando a interface do usuário do Adobe Experience Platform.
exl-id: 33dd2857-aed3-4e35-bc48-1c756a8b3638
source-git-commit: ce3dabe4ab08a41e581b97b74b3abad352e3267c
workflow-type: tm+mt
source-wordcount: '680'
ht-degree: 2%

---

# Criar uma conexão de origem do Google Ads na interface

>[!WARNING]
>
>A origem [!DNL Google Ads] está temporariamente indisponível. O Adobe está trabalhando para resolver problemas com esta fonte.

>[!NOTE]
>
>A fonte do Google Ads está na versão beta. Consulte a [Visão geral das fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de fontes com rótulo beta.

Este tutorial fornece etapas para criar uma conexão de origem do Google Ads usando a interface do usuário do Adobe Experience Platform.

## Introdução

Este tutorial requer um entendimento prático dos seguintes componentes do Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): a estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
   * [Noções básicas sobre a composição de esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os blocos de construção básicos de esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição de esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

Se você já tiver uma conexão válida com o Google Ads, ignore o restante deste documento e prossiga para o tutorial em [configurando um fluxo de dados](../../dataflow/advertising.md)

### Coletar credenciais necessárias

Para acessar a plataforma da conta do Google Ads, é necessário fornecer os seguintes valores:

| Credencial | Descrição |
| ---------- | ----------- |
| ID de cliente do cliente | A ID do cliente é o número da conta que corresponde à conta do cliente do Google Ads que você deseja gerenciar com a API do Google Ads. Esta ID segue o modelo de `123-456-7890`. |
| ID do cliente de logon | A ID do cliente de logon é o número da conta que corresponde à sua conta de gerente do Google Ads e é usada para buscar dados de relatório de um cliente operacional específico. Para obter mais informações sobre como fazer logon na ID do cliente, leia a [documentação da API do Google Ads](https://developers.google.com/search-ads/reporting/concepts/login-customer-id). |
| Token do desenvolvedor | O token do desenvolvedor permite acessar a API do Google Ads. Você pode usar o mesmo token do desenvolvedor para fazer solicitações em relação a todas as suas contas do Google Ads. Recupere seu token de desenvolvedor [fazendo logon em sua conta de gerente](https://ads.google.com/home/tools/manager-accounts/) e navegando até a página da Central de API. |
| Atualizar token | O token de atualização faz parte da autenticação [!DNL OAuth2]. Esse token permite gerar novamente os tokens de acesso após a expiração. |
| ID de cliente | A ID do cliente é usada em conjunto com o segredo do cliente como parte da autenticação [!DNL OAuth2]. Juntas, a ID do cliente e a senha do cliente permitem que o aplicativo opere em nome da sua conta, identificando o aplicativo na Google. |
| Segredo do cliente | O segredo do cliente é usado em conjunto com a ID do cliente como parte da autenticação [!DNL OAuth2]. Juntas, a ID do cliente e a senha do cliente permitem que o aplicativo opere em nome da sua conta, identificando o aplicativo na Google. |

Leia o documento de visão geral da API para [mais informações sobre a introdução ao Google Ads](https://developers.google.com/google-ads/api/docs/first-call/overview).

## Conectar sua conta do Google Ads

Na interface da Platform, selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar o espaço de trabalho [!UICONTROL Fontes]. A tela [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria **[!UICONTROL Advertising]**, selecione **[!UICONTROL Google Ads]** e **[!UICONTROL Adicionar dados]**.

![O catálogo de fontes na interface do Experience Platform.](../../../../images/tutorials/create/ads/catalog.png).

A página **[!UICONTROL Conectar-se ao Google Ads]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Conta existente

Para conectar uma conta existente, selecione a conta do Google Ads à qual deseja se conectar e selecione **[!UICONTROL Avançar]** para continuar.

![A página de seleção das contas existentes no fluxo de trabalho de origem.](../../../../images/tutorials/create/ads/existing.png).

### Nova conta

Se você estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada que aparece, forneça um nome, uma descrição opcional e suas credenciais do Google Ads. Quando terminar, selecione **[!UICONTROL Conectar à origem]** e aguarde algum tempo para que a nova conexão seja estabelecida.

![A nova interface de conta no fluxo de trabalho de origens.](../../../../images/tutorials/create/ads/new.png).

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta do Google Ads. Agora você pode seguir para o próximo tutorial e [configurar um fluxo de dados para trazer dados de publicidade para a Platform](../../dataflow/advertising.md).
