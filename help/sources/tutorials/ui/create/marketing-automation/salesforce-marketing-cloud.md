---
title: Conecte sua conta do Salesforce Marketing Cloud ao Experience Platform por meio da interface
description: Saiba como conectar sua conta do Salesforce Marketing Cloud ao Experience Platform por meio da interface do usuário.
exl-id: 1d9bde60-31e0-489c-9c1c-b6471e0ea554
source-git-commit: 635ab266fac9d3dc232307d7cb49f83904197782
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 1%

---

# Conecte seu [!DNL Salesforce Marketing Cloud] conta para o Experience Platform por meio da interface

>[!IMPORTANT]
>
>No momento, a assimilação de objetos personalizados não é compatível com o [!DNL Salesforce Marketing Cloud] integração de origem.

Este tutorial fornece etapas sobre como conectar seus [!DNL Salesforce Marketing Cloud] para a Adobe Experience Platform por meio da interface do usuário.

## Introdução

Este tutorial requer um entendimento prático dos seguintes componentes do Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): o quadro normalizado pelo qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição do esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os componentes básicos dos esquemas XDM, incluindo princípios fundamentais e práticas recomendadas na composição do esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

Se você já tiver uma [!DNL Salesforce Marketing Cloud] conta, você pode ignorar o restante deste documento e prosseguir para o tutorial em [como trazer dados de automação de marketing para o Experience Platform usando a interface do](../../dataflow/marketing-automation.md).

### Coletar credenciais necessárias

Para acessar seu [!DNL Salesforce Marketing Cloud] na Platform, você deve fornecer os seguintes valores:

| Credencial | Descrição |
| ---------- | ----------- |
| Host | O servidor host do aplicativo. Esse geralmente é o seu subdomínio. **Nota:** Ao inserir seu `host` , é necessário especificar o `{subdomain}.rest.marketingcloudapis.com`. Por exemplo, se o URL do host for `https://acme-ab12c3d4e5fg6hijk7lmnop8qrst.auth.marketingcloudapis.com/`, então você só precisa inserir `acme-ab12c3d4e5fg6hijk7lmnop8qrstauth.marketingcloudapis.com/` como valor de host. |
| ID do cliente | A ID do cliente associada à [!DNL Salesforce Marketing Cloud] aplicação. |
| Client secret | O segredo do cliente associado à [!DNL Salesforce Marketing Cloud] aplicação. |

Para obter mais informações sobre autenticação para [!DNL Salesforce Marketing Cloud], visite o [[!DNL Salesforce] documentação de autenticação](https://developer.salesforce.com/docs/atlas.en-us.mc-apis.meta/mc-apis/authentication.htm).

## Conecte seu [!DNL Salesforce Marketing Cloud] account

Na interface do usuário da Platform, selecione **[!UICONTROL Origens]** na navegação à esquerda, para acessar a [!UICONTROL Origens] espaço de trabalho. A variável [!UICONTROL Catálogo] exibe uma variedade de fontes suportadas pelo Experience Platform.

Você pode selecionar a categoria apropriada na lista de categorias. Você também pode usar a barra de pesquisa para filtrar por uma fonte específica.

No [!UICONTROL Automação de marketing] categoria, selecione **[!UICONTROL Marketing Cloud do Salesforce]** e selecione **[!UICONTROL Configurar]**.

![O catálogo de origens com a origem de Marketing Cloud do Salesforce selecionada.](../../../../images/tutorials/create/salesforce-marketing-cloud/catalog.png)

A variável **[!UICONTROL Conectar-se ao Salesforce Marketing Cloud]** é exibida. Nesta página, você pode criar uma nova conta ou usar uma conta existente.

### Nova conta

Para criar uma nova conta, selecione **[!UICONTROL Nova conta]** e forneça um nome para sua conta, uma descrição opcional e as credenciais de autenticação que correspondem à [!DNL Salesforce Marketing Cloud] conta.

Quando terminar, selecione **[!UICONTROL Conectar à origem]** e aguarde algum tempo para estabelecer a nova conexão.

![A nova interface de conta, onde é possível autenticar uma nova conta para o Salesforce Marketing Cloud.](../../../../images/tutorials/create/salesforce-marketing-cloud/new.png)

### Conta existente

Se você já tiver uma conta existente, selecione **[!UICONTROL Conta existente]** e, em seguida, selecione a conta que deseja usar na lista exibida.

![A interface de conta existente onde é possível selecionar em uma lista de contas existentes do Salesforce Marketing Cloud.](../../../../images/tutorials/create/salesforce-marketing-cloud/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão entre suas [!DNL Salesforce Marketing Cloud] conta e Experience Platform. Agora você pode seguir para o próximo tutorial e [crie um fluxo de dados para trazer seus dados de automação de marketing para o Experience Platform](../../dataflow/marketing-automation.md).
