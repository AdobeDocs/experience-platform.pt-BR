---
title: Conectar sua conta do Salesforce Marketing Cloud ao Experience Platform por meio da interface
description: Saiba como conectar sua conta do Marketing Cloud Salesforce ao Experience Platform por meio da interface.
exl-id: 1d9bde60-31e0-489c-9c1c-b6471e0ea554
source-git-commit: 474b81aa8caf58013f8ea7cff9ad59d92466aac8
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 2%

---

# Conecte sua conta do [!DNL Salesforce Marketing Cloud] ao Experience Platform por meio da interface

>[!WARNING]
>
>A origem [!DNL Salesforce Marketing Cloud] será substituída no final de maio de 2025.

Este tutorial fornece etapas sobre como conectar sua conta do [!DNL Salesforce Marketing Cloud] à Adobe Experience Platform por meio da interface do usuário.

## Introdução

Este tutorial requer um entendimento prático dos seguintes componentes do Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): a estrutura padronizada pela qual o [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas sobre a composição de esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os blocos de construção básicos de esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição de esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

Se você já tiver uma conta [!DNL Salesforce Marketing Cloud], ignore o restante deste documento e prossiga para o tutorial em [trazendo dados de automação de marketing para o Experience Platform usando a interface](../../dataflow/marketing-automation.md).

### Coletar credenciais necessárias

Para acessar sua conta do [!DNL Salesforce Marketing Cloud] na Platform, você deve fornecer os seguintes valores:

| Credencial | Descrição |
| ---------- | ----------- |
| Host | O servidor host do aplicativo. Esse geralmente é o seu subdomínio. **Observação:** ao inserir seu valor `host`, você precisa especificar o `{subdomain}.rest.marketingcloudapis.com`. Por exemplo, se a URL do host for `https://acme-ab12c3d4e5fg6hijk7lmnop8qrst.auth.marketingcloudapis.com/`, você deve inserir `acme-ab12c3d4e5fg6hijk7lmnop8qrst.rest.marketingcloudapis.com/` como valor do host. |
| ID de cliente | A ID do cliente associada ao aplicativo [!DNL Salesforce Marketing Cloud]. |
| Segredo do cliente | O segredo do cliente associado ao aplicativo [!DNL Salesforce Marketing Cloud]. |

Para obter mais informações sobre autenticação para [!DNL Salesforce Marketing Cloud], consulte a [[!DNL Salesforce] documentação de autenticação](https://developer.salesforce.com/docs/atlas.en-us.mc-apis.meta/mc-apis/authentication.htm).

## Conectar sua conta do [!DNL Salesforce Marketing Cloud]

>[!IMPORTANT]
>
>No momento, a assimilação de objetos personalizados não tem suporte da integração de origem [!DNL Salesforce Marketing Cloud].

Na interface da Platform, selecione **[!UICONTROL Fontes]** na navegação à esquerda para acessar o espaço de trabalho [!UICONTROL Fontes]. O [!UICONTROL Catálogo] exibe uma variedade de fontes suportadas pelo Experience Platform.

Você pode selecionar a categoria apropriada na lista de categorias. Você também pode usar a barra de pesquisa para filtrar por uma fonte específica.

Na categoria [!UICONTROL Automação de marketing], selecione **[!UICONTROL Marketing Cloud do Salesforce]** e **[!UICONTROL Configurar]**.

![O catálogo de origens com a origem de Marketing Cloud Salesforce selecionada.](../../../../images/tutorials/create/salesforce-marketing-cloud/catalog.png)

A página **[!UICONTROL Conectar-se ao Marketing Cloud do Salesforce]** é exibida. Nesta página, você pode criar uma nova conta ou usar uma conta existente.

### Nova conta

Para criar uma nova conta, selecione **[!UICONTROL Nova conta]** e forneça um nome para a sua conta, uma descrição opcional e as credenciais de autenticação que correspondem à sua conta do [!DNL Salesforce Marketing Cloud].

Quando terminar, selecione **[!UICONTROL Conectar à origem]** e aguarde algum tempo para que a nova conexão seja estabelecida.

![A nova interface de conta na qual você pode autenticar uma nova conta para o Salesforce Marketing Cloud.](../../../../images/tutorials/create/salesforce-marketing-cloud/new.png)

### Conta existente

Se você já tiver uma conta existente, selecione **[!UICONTROL Conta existente]** e, em seguida, selecione a conta que deseja usar na lista exibida.

![A interface de conta existente onde você pode selecionar em uma lista de contas existentes do Salesforce Marketing Cloud.](../../../../images/tutorials/create/salesforce-marketing-cloud/existing.png)

## Próximas etapas

Seguindo este tutorial, você estabeleceu uma conexão entre sua conta do [!DNL Salesforce Marketing Cloud] e o Experience Platform. Agora você pode seguir para o próximo tutorial e [criar um fluxo de dados para trazer seus dados de automação de marketing para o Experience Platform](../../dataflow/marketing-automation.md).
