---
title: Conecte sua conta do Salesforce usando a interface do Experience Platform
description: Saiba como conectar sua conta do Salesforce e trazer seus dados de CRM para o Experience Platform usando a interface do usuário.
exl-id: b67fa4c4-d8ff-4d2d-aa76-5d9d32aa22d6
source-git-commit: c543590ef1806e5259da2ffb6833cd030d573ca7
workflow-type: tm+mt
source-wordcount: '737'
ht-degree: 1%

---

# Conecte seu [!DNL Salesforce] conta para Experience Platform usando a interface do usuário

Este tutorial fornece etapas sobre como conectar seus [!DNL Salesforce] e traga seus dados do CRM para a Adobe Experience Platform usando a interface do usuário do Experience Platform.

## Introdução

Este tutorial requer um entendimento prático dos seguintes componentes do Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): a estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
   * [Noções básicas da composição do esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os componentes básicos dos esquemas XDM, incluindo princípios fundamentais e práticas recomendadas na composição do esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

Se você já tiver um [!DNL Salesforce] conta, você pode ignorar o restante deste documento e prosseguir para o tutorial em [configuração de um fluxo de dados para dados do CRM](../../dataflow/crm.md).

### Coletar credenciais necessárias {#gather-required-credentials}

A variável [!DNL Salesforce] A origem oferece suporte à autenticação básica e à Credencial do Cliente OAuth2.

>[!BEGINTABS]

>[!TAB Autenticação básica]

Você deve fornecer valores para as credenciais a seguir para conectar seu [!DNL Salesforce] conta usando autenticação básica.

| Credencial | Descrição |
| --- | --- |
| URL do ambiente | O URL do [!DNL Salesforce] instância de origem. |
| Nome de usuário | O nome de usuário para o [!DNL Salesforce] conta de usuário. |
| Senha | A senha para o [!DNL Salesforce] conta de usuário. |
| Token de segurança | O token de segurança para o [!DNL Salesforce] conta de usuário. |
| Versão da API | (Opcional) A versão da API REST do [!DNL Salesforce] instância que você está usando. O valor da versão da API deve ser formatado com um decimal. Por exemplo, se você estiver usando a versão da API `52`, você deverá inserir o valor como `52.0` Se esse campo ficar em branco, o Experience Platform usará automaticamente a versão mais recente disponível. |

Para obter mais informações sobre autenticação, consulte [este [!DNL Salesforce] guia de autenticação](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/quickstart_oauth.htm).

>[!TAB Credencial do cliente OAuth2]

Você deve fornecer valores para as credenciais a seguir para conectar seu [!DNL Salesforce] usando a credencial do cliente OAuth2.

| Credencial | Descrição |
| --- | --- |
| URL do ambiente | O URL do [!DNL Salesforce] instância de origem. |
| ID do cliente | A ID do cliente é usada em conjunto com o segredo do cliente como parte da autenticação OAuth2. Juntas, a ID do cliente e o segredo do cliente permitem que o aplicativo opere em nome da conta identificando o aplicativo para [!DNL Salesforce]. |
| Client secret | O segredo do cliente é usado em conjunto com a ID do cliente como parte da autenticação OAuth2. Juntas, a ID do cliente e o segredo do cliente permitem que o aplicativo opere em nome da conta identificando o aplicativo para [!DNL Salesforce]. |
| Versão da API | (Opcional) A versão da API REST do [!DNL Salesforce] instância que você está usando. O valor da versão da API deve ser formatado com um decimal. Por exemplo, se você estiver usando a versão da API `52`, você deverá inserir o valor como `52.0` Se esse campo ficar em branco, o Experience Platform usará automaticamente a versão mais recente disponível. |

Para obter mais informações sobre como usar o OAuth para [!DNL Salesforce], leia o [[!DNL Salesforce] guia sobre fluxos de autorização OAuth](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&amp;type=5).

>[!ENDTABS]

Depois de obter as credenciais necessárias, siga as etapas abaixo para conectar seu [!DNL Salesforce] conta para Experience Platform.

## Conecte seu [!DNL Salesforce] account

Na interface do usuário da Platform, selecione **[!UICONTROL Origens]** na navegação à esquerda, para acessar o espaço de trabalho de fontes. A variável *[!UICONTROL Catálogo]* A tela exibe uma variedade de fontes disponíveis no catálogo de fontes do Experience Platform.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar uma fonte específica usando a opção de pesquisa.

Selecionar **[!UICONTROL CRM]** na lista de categorias de origens e selecione **[!UICONTROL Adicionar dados]** do [!DNL Salesforce] cartão.

![O catálogo de origens na interface do usuário do Experience Platform com o cartão de origem do Salesforce selecionado.](../../../../images/tutorials/create/salesforce/catalog.png)

A variável **[!UICONTROL Conectar-se ao Salesforce]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

>[!BEGINTABS]

>[!TAB Usar uma conta existente do Salesforce]

Para usar uma conta existente, selecione **[!UICONTROL Conta existente]** e, em seguida, selecione a conta que deseja usar na lista exibida. Quando terminar, selecione **[!UICONTROL Próxima]** para continuar.

![Uma lista de contas autenticadas do Salesforce que já existem em sua organização.](../../../../images/tutorials/create/salesforce/existing.png)

>[!TAB Criar uma nova conta do Salesforce]

Para usar uma nova conta, selecione **[!UICONTROL Nova conta]** e forneça um nome, uma descrição e sua [!DNL Salesforce] credenciais de autenticação. Quando terminar, selecione **[!UICONTROL Conectar à origem]** e aguarde alguns segundos para que a nova conexão seja estabelecida.

![A interface na qual você pode criar uma nova conta do Salesforce fornecendo as credenciais de autenticação apropriadas.](../../../../images/tutorials/create/salesforce/new.png)

>[!ENDTABS]

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com o seu [!DNL Salesforce] conta. Agora você pode seguir para o próximo tutorial e [configurar um fluxo de dados para trazer dados para o [!DNL Platform]](../../dataflow/crm.md).
