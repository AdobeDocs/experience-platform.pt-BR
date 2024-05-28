---
title: Conecte sua conta da Salesforce Service Cloud usando a interface do usuário do Experience Platform
description: Saiba como conectar sua conta do Salesforce Service Cloud e trazer seus dados de sucesso do cliente para o Experience Platform usando a interface do usuário.
exl-id: 38480a29-7852-46c6-bcea-5dc6bffdbd15
source-git-commit: 7930a869627130a5db34780e64b809cda0c1e5f4
workflow-type: tm+mt
source-wordcount: '843'
ht-degree: 3%

---

# Conecte seu [!DNL Salesforce Service Cloud] conta para Experience Platform usando a interface do usuário

Este tutorial fornece etapas sobre como conectar seus [!DNL Salesforce Service Cloud] e traga seus dados de sucesso do cliente para a Adobe Experience Platform usando a interface do Experience Platform.

## Introdução

Este tutorial requer um entendimento prático dos seguintes componentes do Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): a estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
   * [Noções básicas da composição do esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os componentes básicos dos esquemas XDM, incluindo princípios fundamentais e práticas recomendadas na composição do esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

Se você já tiver um [!DNL Salesforce Service Cloud] conexão, você pode ignorar o restante deste documento e prosseguir para o tutorial em [configuração de um fluxo de dados para o sucesso de um cliente](../../dataflow/customer-success.md)

### Coletar credenciais necessárias

A variável [!DNL Salesforce Service Cloud] A origem oferece suporte à autenticação básica e à Credencial do Cliente OAuth2.

>[!BEGINTABS]

>[!TAB Autenticação básica]

Você deve fornecer valores para as credenciais a seguir para conectar seu [!DNL Salesforce Service Cloud] conta usando autenticação básica.

| Credencial | Descrição |
| --- | --- |
| URL do ambiente | O URL do [!DNL Salesforce Service Cloud] instância de origem. |
| Nome de usuário | O nome de usuário para o [!DNL Salesforce Service Cloud] conta de usuário. |
| Senha | A senha para o [!DNL Salesforce Service Cloud] conta de usuário. |
| Token de segurança | O token de segurança para o [!DNL Salesforce Service Cloud] conta de usuário. |
| Versão da API | (Opcional) A versão da API REST do [!DNL Salesforce Service Cloud] instância que você está usando. O valor da versão da API deve ser formatado com um decimal. Por exemplo, se você estiver usando a versão da API `52`, você deverá inserir o valor como `52.0`. Se esse campo ficar em branco, o Experience Platform usará automaticamente a versão mais recente disponível. |

Para obter mais informações sobre autenticação, consulte [este [!DNL Salesforce Service Cloud] guia de autenticação](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/quickstart_oauth.htm).

>[!TAB Credencial do cliente OAuth2]

Você deve fornecer valores para as credenciais a seguir para conectar seu [!DNL Salesforce Service Cloud] usando a credencial do cliente OAuth2.

| Credencial | Descrição |
| --- | --- |
| URL do ambiente | O URL do [!DNL Salesforce Service Cloud] instância de origem. |
| ID de cliente | A ID do cliente é usada em conjunto com o segredo do cliente como parte da autenticação OAuth2. Juntos, a ID do cliente e o segredo do cliente permitem que o aplicativo opere em nome da sua conta, identificando o aplicativo para [!DNL Salesforce Service Cloud]. |
| Segredo do cliente | O segredo do cliente é usado em conjunto com a ID do cliente como parte da autenticação OAuth2. Juntos, a ID do cliente e o segredo do cliente permitem que o aplicativo opere em nome da sua conta, identificando o aplicativo para [!DNL Salesforce Service Cloud]. |
| Versão da API | A versão da API REST do [!DNL Salesforce Service Cloud] instância que você está usando. O valor da versão da API deve ser formatado com um decimal. Por exemplo, se você estiver usando a versão da API `52`, você deverá inserir o valor como `52.0`. Se esse campo ficar em branco, o Experience Platform usará automaticamente a versão mais recente disponível. |

Para obter mais informações sobre como usar o OAuth para [!DNL Salesforce Service Cloud], leia o [[!DNL Salesforce Service Cloud] guia sobre fluxos de autorização OAuth](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&amp;type=5).

>[!ENDTABS]

Depois de obter as credenciais necessárias, siga as etapas abaixo para conectar seu [!DNL Salesforce Service Cloud] conta para Experience Platform.

## Conecte seu [!DNL Salesforce Service Cloud] account

Na interface do usuário da Platform, selecione **[!UICONTROL Origens]** na navegação à esquerda, para acessar a [!UICONTROL Origens] espaço de trabalho. Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Selecionar **[!DNL Salesforce Service Cloud]** no *[!UICONTROL Sucesso do cliente]* e selecione **[!UICONTROL Adicionar dados]**.

>[!TIP]
>
>As origens no catálogo de origens exibem a variável **[!UICONTROL Configurar]** opção quando uma determinada fonte ainda não tiver uma conta autenticada. Quando uma conta autenticada existir, essa opção será alterada para **[!UICONTROL Adicionar dados]**.

![O catálogo de origens na interface do usuário do Experience Platform com o cartão de origem do Salesforce Service Cloud selecionado.](../../../../images/tutorials/create/salesforce-service-cloud/catalog.png)

A variável **[!UICONTROL Conectar-se à Salesforce Service Cloud]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Usar uma conta existente

Para usar uma conta existente, selecione **[!UICONTROL Conta existente]** e selecione a conta desejada na lista exibida. Quando terminar, selecione **[!UICONTROL Próxima]** para continuar.

![Uma lista de contas autenticadas do Salesforce Service Cloud que já existem em sua organização.](../../../../images/tutorials/create/salesforce-service-cloud/existing.png)

### Criar uma nova conta

Para criar uma nova conta, selecione **[!UICONTROL Nova conta]** e forneça um nome e uma descrição para o seu novo [!DNL Salesforce Service Cloud] conta.

![A interface na qual você pode criar uma nova conta do Salesforce Service Cloud fornecendo as credenciais de autenticação apropriadas.](../../../../images/tutorials/create/salesforce-service-cloud/new.png)

Em seguida, selecione o tipo de autenticação que deseja usar para a nova conta.

>[!BEGINTABS]

>[!TAB Autenticação básica]

Para autenticação básica, selecione **[!UICONTROL Autenticação básica]** e, em seguida, forneça valores para as seguintes credenciais:

* URL do ambiente
* Nome de usuário
* Senha
* Versão da API (opcional)

Quando terminar, selecione **[!UICONTROL Conectar à origem]**.

![A interface de autenticação básica para a criação de conta do Salesforce.](../../../../images/tutorials/create/salesforce-service-cloud/basic.png)

>[!TAB Credencial do cliente OAuth2]

Para a credencial do cliente OAuth 2, selecione **[!UICONTROL Credencial do cliente OAuth2]** e, em seguida, forneça valores para as seguintes credenciais:

* URL do ambiente
* ID de cliente
* Segredo do cliente
* Versão da API

Quando terminar, selecione **[!UICONTROL Conectar à origem]**.

![A interface OAuth para a criação de conta do Salesforce.](../../../../images/tutorials/create/salesforce-service-cloud/oauth2.png)

>[!ENDTABS]

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com o seu [!DNL Salesforce Service Cloud] conta. Agora você pode seguir para o próximo tutorial e [configurar um fluxo de dados para trazer os dados de sucesso do cliente para o Experience Platform](../../dataflow/customer-success.md).
