---
title: Conectar sua conta da Salesforce Service Cloud usando a interface do usuário da Experience Platform
description: Saiba como conectar sua conta da Salesforce Service Cloud e trazer seus dados de sucesso do cliente para a Experience Platform usando a interface do usuário.
exl-id: 38480a29-7852-46c6-bcea-5dc6bffdbd15
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '844'
ht-degree: 3%

---

# Conectar sua conta do [!DNL Salesforce Service Cloud] à Experience Platform usando a interface

Este tutorial fornece etapas sobre como conectar sua conta do [!DNL Salesforce Service Cloud] e trazer seus dados de sucesso do cliente para a Adobe Experience Platform usando a interface do usuário do Experience Platform.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): a estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
   * [Noções básicas sobre a composição de esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os blocos de construção básicos de esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição de esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

Se você já tiver uma conexão válida do [!DNL Salesforce Service Cloud], ignore o restante deste documento e prossiga para o tutorial em [configurando um fluxo de dados para o sucesso de um cliente](../../dataflow/customer-success.md)

### Coletar credenciais necessárias

A origem [!DNL Salesforce Service Cloud] dá suporte à autenticação básica e à Credencial do Cliente OAuth2.

>[!BEGINTABS]

>[!TAB Autenticação básica]

Você deve fornecer valores para as credenciais a seguir para conectar sua conta do [!DNL Salesforce Service Cloud] usando autenticação básica.

| Credencial | Descrição |
| --- | --- |
| URL do ambiente | A URL da instância de origem [!DNL Salesforce Service Cloud]. |
| Nome de usuário | O nome de usuário da conta de usuário [!DNL Salesforce Service Cloud]. |
| Senha | A senha da conta de usuário [!DNL Salesforce Service Cloud]. |
| Token de segurança | O token de segurança para a conta de usuário [!DNL Salesforce Service Cloud]. |
| Versão da API | (Opcional) A versão da API REST da instância [!DNL Salesforce Service Cloud] que você está usando. O valor da versão da API deve ser formatado com um decimal. Por exemplo, se você estiver usando a versão da API `52`, será necessário inserir o valor como `52.0`. Se esse campo ficar em branco, o Experience Platform usará automaticamente a versão mais recente disponível. |

Para obter mais informações sobre autenticação, consulte [este [!DNL Salesforce Service Cloud] guia de autenticação](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/quickstart_oauth.htm).

>[!TAB Credencial do Cliente OAuth2]

Você deve fornecer valores para as credenciais a seguir para conectar sua conta do [!DNL Salesforce Service Cloud] usando a Credencial do Cliente OAuth2.

| Credencial | Descrição |
| --- | --- |
| URL do ambiente | A URL da instância de origem [!DNL Salesforce Service Cloud]. |
| ID de cliente | A ID do cliente é usada em conjunto com o segredo do cliente como parte da autenticação OAuth2. Juntos, a ID do cliente e o segredo do cliente permitem que o aplicativo opere em nome da sua conta, identificando o aplicativo no [!DNL Salesforce Service Cloud]. |
| Segredo do cliente | O segredo do cliente é usado em conjunto com a ID do cliente como parte da autenticação OAuth2. Juntos, a ID do cliente e o segredo do cliente permitem que o aplicativo opere em nome da sua conta, identificando o aplicativo no [!DNL Salesforce Service Cloud]. |
| Versão da API | A versão da API REST da instância [!DNL Salesforce Service Cloud] que você está usando. O valor da versão da API deve ser formatado com um decimal. Por exemplo, se você estiver usando a versão da API `52`, será necessário inserir o valor como `52.0`. Se esse campo ficar em branco, o Experience Platform usará automaticamente a versão mais recente disponível. |

Para obter mais informações sobre como usar o OAuth para [!DNL Salesforce Service Cloud], leia o [[!DNL Salesforce Service Cloud] guia sobre Fluxos de Autorização do OAuth](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&amp;type=5).

>[!ENDTABS]

Depois de obter as credenciais necessárias, você poderá seguir as etapas abaixo para conectar sua conta do [!DNL Salesforce Service Cloud] à Experience Platform.

## Conectar sua conta do [!DNL Salesforce Service Cloud]

Na interface do Experience Platform, selecione **[!UICONTROL Fontes]** na navegação à esquerda para acessar o espaço de trabalho [!UICONTROL Fontes]. Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Selecione **[!DNL Salesforce Service Cloud]** na categoria *[!UICONTROL Sucesso do cliente]* e selecione **[!UICONTROL Adicionar dados]**.

>[!TIP]
>
>As origens no catálogo de origens exibem a opção **[!UICONTROL Configurar]** quando uma determinada origem ainda não tem uma conta autenticada. Quando uma conta autenticada existir, esta opção será alterada para **[!UICONTROL Adicionar dados]**.

![O catálogo de origens na interface do usuário do Experience Platform com o cartão de origem do Salesforce Service Cloud selecionado.](../../../../images/tutorials/create/salesforce-service-cloud/catalog.png)

A página **[!UICONTROL Conectar-se à Salesforce Service Cloud]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Usar uma conta existente

Para usar uma conta existente, selecione **[!UICONTROL Conta existente]** e a conta desejada na lista exibida. Quando terminar, selecione **[!UICONTROL Avançar]** para continuar.

![Uma lista de contas autenticadas da Salesforce Service Cloud que já existem em sua organização.](../../../../images/tutorials/create/salesforce-service-cloud/existing.png)

### Criar uma nova conta

Para criar uma nova conta, selecione **[!UICONTROL Nova conta]** e forneça um nome e uma descrição para sua nova conta [!DNL Salesforce Service Cloud].

![A interface na qual você pode criar uma nova conta da Salesforce Service Cloud fornecendo as credenciais de autenticação apropriadas.](../../../../images/tutorials/create/salesforce-service-cloud/new.png)

Em seguida, selecione o tipo de autenticação que deseja usar para a nova conta.

>[!BEGINTABS]

>[!TAB Autenticação básica]

Para autenticação básica, selecione **[!UICONTROL Autenticação básica]** e forneça valores para as seguintes credenciais:

* URL do ambiente
* Nome de usuário
* Senha
* Versão da API (opcional)

Quando terminar, selecione **[!UICONTROL Conectar à origem]**.

![A interface de autenticação básica para a criação de conta do Salesforce.](../../../../images/tutorials/create/salesforce-service-cloud/basic.png)

>[!TAB Credencial do Cliente OAuth2]

Para a Credencial do cliente OAuth 2, selecione **[!UICONTROL Credencial do cliente OAuth2]** e forneça valores para as seguintes credenciais:

* URL do ambiente
* ID de cliente
* Segredo do cliente
* Versão da API

Quando terminar, selecione **[!UICONTROL Conectar à origem]**.

![A interface OAuth para a criação de conta do Salesforce.](../../../../images/tutorials/create/salesforce-service-cloud/oauth2.png)

>[!ENDTABS]

## Próximas etapas

Seguindo este tutorial, você estabeleceu uma conexão com sua conta do [!DNL Salesforce Service Cloud]. Agora você pode seguir para o próximo tutorial e [configurar um fluxo de dados para trazer os dados de Sucesso do cliente para a Experience Platform](../../dataflow/customer-success.md).
