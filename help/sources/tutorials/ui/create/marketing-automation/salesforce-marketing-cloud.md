---
keywords: Experience Platform;página inicial;tópicos populares;salesforce marketing cloud;Salesforce Marketing Cloud
solution: Experience Platform
title: Criar uma conexão de origem de Marketing Cloud do Salesforce na interface
type: Tutorial
description: Saiba como criar uma conexão de origem do Salesforce Marketing Cloud usando a interface do usuário do Adobe Experience Platform.
exl-id: 1d9bde60-31e0-489c-9c1c-b6471e0ea554
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 1%

---

# Criar um [!DNL Salesforce Marketing Cloud] conexão de origem na interface

>[!NOTE]
>
> A variável [!DNL Salesforce Marketing Cloud] a fonte está na versão beta. Consulte a [visão geral das origens](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de fontes rotuladas como beta.

Os conectores de origem no Adobe Experience Platform fornecem a capacidade de assimilar dados originados externamente de forma programada. Este tutorial fornece etapas para a criação de um [!DNL Salesforce Marketing Cloud] conector de origem usando a interface do usuário da Platform.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): o quadro normalizado pelo qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição do esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os componentes básicos dos esquemas XDM, incluindo princípios fundamentais e práticas recomendadas na composição do esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

Se você já tiver uma [!DNL Salesforce Marketing Cloud] conexão, você pode ignorar o restante deste documento e prosseguir para o tutorial em [configuração de um fluxo de dados](../../dataflow/marketing-automation.md).

### Coletar credenciais necessárias

Para acessar seu [!DNL Salesforce Marketing Cloud] na Platform, você deve fornecer os seguintes valores:

| Credencial | Descrição |
| ---------- | ----------- |
| `host` | O servidor host do aplicativo. Esse geralmente é o seu subdomínio. **Nota:** Ao inserir seu `host` , você só precisa especificar o subdomínio e não o URL inteiro. Por exemplo, se o URL do host for `https://abcd-ab12c3d4e5fg6hijk7lmnop8qrst.auth.marketingcloudapis.com/`, então você só precisa inserir `abcd-ab12c3d4e5fg6hijk7lmnop8qrst` como valor de host. |
| `clientId` | A ID do cliente associada à [!DNL Salesforce Marketing Cloud] aplicação. |
| `clientSecret` | O segredo do cliente associado à [!DNL Salesforce Marketing Cloud] aplicação. |

Para obter mais informações sobre a introdução, consulte esta [[!DNL Salesforce Marketing Cloud] documento](https://developer.salesforce.com/docs/atlas.en-us.mc-apis.meta/mc-apis/authentication.htm).

## Conecte seu [!DNL Salesforce Marketing Cloud] account

Depois de obter as credenciais necessárias, siga as etapas abaixo para vincular [!DNL Salesforce Marketing Cloud] para a Platform.

Na interface do usuário da Platform, selecione **[!UICONTROL Origens]** na navegação à esquerda, para acessar a [!UICONTROL Origens] espaço de trabalho. A variável [!UICONTROL Catálogo] A tela exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Você também pode usar a barra de pesquisa para restringir os conectores exibidos.

No [!UICONTROL Automação de marketing] categoria, selecione **[!UICONTROL Marketing Cloud do Salesforce]** e selecione **[!UICONTROL Configurar]**.

![catálogo](../../../../images/tutorials/create/salesforce-marketing-cloud/catalog.png)

A variável **[!UICONTROL Conectar-se ao Salesforce Marketing Cloud]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada que aparece, forneça um nome, uma descrição opcional e [!DNL Salesforce Marketing Cloud] credenciais. Quando terminar, selecione **[!UICONTROL Conectar]** e aguarde algum tempo para estabelecer a nova conexão.

![novo](../../../../images/tutorials/create/salesforce-marketing-cloud/new.png)

### Conta existente

Para conectar uma conta existente, selecione a [!DNL Salesforce Marketing Cloud] conta à qual deseja se conectar e selecione **[!UICONTROL Próxima]** para continuar.

![existente](../../../../images/tutorials/create/salesforce-marketing-cloud/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com o seu [!DNL Salesforce Marketing Cloud] conta. Agora você pode seguir para o próximo tutorial e [configurar um fluxo de dados para trazer dados do sistema de automação de marketing para a Platform](../../dataflow/marketing-automation.md).
