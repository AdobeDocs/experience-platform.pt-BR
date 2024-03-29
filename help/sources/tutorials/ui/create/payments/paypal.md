---
keywords: Experience Platform;página inicial;tópicos populares;paypal;Paypal
solution: Experience Platform
title: Criar uma Conexão de Origem do PayPal na interface do usuário
type: Tutorial
description: Saiba como criar uma conexão de origem do PayPal usando a interface do Adobe Experience Platform.
exl-id: bbd3f634-cb28-45d8-9b7b-ed3873101882
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 1%

---

# Criar um [!DNL PayPal] conexão de origem na interface

Os conectores de origem no Adobe Experience Platform fornecem a capacidade de assimilar dados originados externamente de forma programada. Este tutorial fornece etapas para a criação de um [!DNL PayPal] conector de origem usando a interface do usuário da Platform.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): o quadro normalizado pelo qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição do esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os componentes básicos dos esquemas XDM, incluindo princípios fundamentais e práticas recomendadas na composição do esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

Se você já tiver um [!DNL PayPal] conexão, você pode ignorar o restante deste documento e prosseguir para o tutorial em [configuração de um fluxo de dados](../../dataflow/payments.md)

### Coletar credenciais necessárias

Para acessar seu [!DNL PayPal] Plataforma da conta, você deve fornecer os seguintes valores:

| Credencial | Descrição |
| ---------- | ----------- |
| `host` | O URL do [!DNL PayPal] instância. |
| `clientID` | A ID do cliente associada à [!DNL PayPal] aplicação. |
| `clientSecret` | O segredo do cliente associado à [!DNL PayPal] aplicação. |

Para obter mais informações sobre a introdução, consulte esta [[!DNL PayPal] documento](https://developer.paypal.com/docs/api/overview/#get-credentials)

## Conecte seu [!DNL PayPal] account

Depois de obter as credenciais necessárias, siga as etapas abaixo para vincular [!DNL PayPal] para a Platform.

Efetue logon no [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Origens]** na barra de navegação esquerda, para acessar a **[!UICONTROL Origens]** espaço de trabalho. A variável **[!UICONTROL Catálogo]** A tela exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

No **[!UICONTROL Pagamentos]** categoria, selecione **[!UICONTROL PayPal]**. Se esta for a primeira vez que você usa este conector, selecione **[!UICONTROL Configurar]**. Caso contrário, selecione **[!UICONTROL Adicionar dados]** para criar um novo [!DNL PayPal] conector.

![catálogo](../../../../images/tutorials/create/paypal/catalog.png)

A variável **[!UICONTROL Conectar-se ao PayPal]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada que aparece, forneça um nome, uma descrição opcional e [!DNL PayPal] credenciais. Quando terminar, selecione **[!UICONTROL Conectar]** e aguarde algum tempo para estabelecer a nova conexão.

![conectar](../../../../images/tutorials/create/paypal/connect.png)

### Conta existente

Para conectar uma conta existente, selecione a [!DNL PayPal] conta à qual deseja se conectar e selecione **[!UICONTROL Próxima]** para continuar.

![existente](../../../../images/tutorials/create/paypal/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com o seu [!DNL PayPal] conta. Agora você pode seguir para o próximo tutorial e [configurar um fluxo de dados para trazer dados de pagamento para a Platform](../../dataflow/payments.md).
