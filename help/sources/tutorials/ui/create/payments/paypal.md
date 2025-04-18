---
keywords: Experience Platform;página inicial;tópicos populares;paypal;Paypal
solution: Experience Platform
title: Criar uma Conexão do PayPal Source na interface do usuário
type: Tutorial
description: Saiba como criar uma conexão de origem do PayPal usando a interface do Adobe Experience Platform.
exl-id: bbd3f634-cb28-45d8-9b7b-ed3873101882
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 1%

---

# Criar uma conexão de origem [!DNL PayPal] na interface

>[!WARNING]
>
>A origem [!DNL PayPal] será substituída no final de junho de 2025.

Os conectores do Source no Adobe Experience Platform fornecem a capacidade de assimilar dados obtidos externamente de forma programada. Este tutorial fornece etapas para a criação de um conector de origem [!DNL PayPal] usando a interface do usuário do Experience Platform.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): a estrutura padronizada pela qual o [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas sobre a composição de esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os blocos de construção básicos de esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição de esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

Se você já tiver uma conexão [!DNL PayPal] válida, ignore o restante deste documento e prossiga para o tutorial em [configurando um fluxo de dados](../../dataflow/payments.md)

### Coletar credenciais necessárias

Para acessar sua Experience Platform de conta [!DNL PayPal], você deve fornecer os seguintes valores:

| Credencial | Descrição |
| ---------- | ----------- |
| `host` | A URL da instância [!DNL PayPal]. |
| `clientID` | A ID do cliente associada ao aplicativo [!DNL PayPal]. |
| `clientSecret` | O segredo do cliente associado ao aplicativo [!DNL PayPal]. |

Para obter mais informações sobre a introdução, consulte este [[!DNL PayPal] documento](https://developer.paypal.com/docs/api/overview/#get-credentials)

## Conectar sua conta do [!DNL PayPal]

Depois de obter as credenciais necessárias, siga as etapas abaixo para vincular sua conta do [!DNL PayPal] à Experience Platform.

Faça logon em [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar o espaço de trabalho **[!UICONTROL Fontes]**. A tela **[!UICONTROL Catálogo]** exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria **[!UICONTROL Pagamentos]**, selecione **[!UICONTROL PayPal]**. Se esta for a primeira vez que você usa este conector, selecione **[!UICONTROL Configurar]**. Caso contrário, selecione **[!UICONTROL Adicionar dados]** para criar um novo conector [!DNL PayPal].

![catálogo](../../../../images/tutorials/create/paypal/catalog.png)

A página **[!UICONTROL Conectar-se ao PayPal]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se você estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada que aparece, forneça um nome, uma descrição opcional e suas credenciais do [!DNL PayPal]. Quando terminar, selecione **[!UICONTROL Conectar]** e aguarde algum tempo para que a nova conexão seja estabelecida.

![conectar](../../../../images/tutorials/create/paypal/connect.png)

### Conta existente

Para conectar uma conta existente, selecione a conta [!DNL PayPal] com a qual deseja se conectar e clique em **[!UICONTROL Avançar]** para continuar.

![existente](../../../../images/tutorials/create/paypal/existing.png)

## Próximas etapas

Seguindo este tutorial, você estabeleceu uma conexão com sua conta do [!DNL PayPal]. Agora você pode seguir para o próximo tutorial e [configurar um fluxo de dados para trazer dados de Pagamento para a Experience Platform](../../dataflow/payments.md).
