---
keywords: Experience Platform;página inicial;tópicos populares;Microsoft Dynamics;microsoft dynamics;Dynamics;dynamics
solution: Experience Platform
title: Criar uma conexão de origem do Microsoft Dynamics na interface
type: Tutorial
description: Saiba como criar uma conexão de origem do Microsoft Dynamics usando a interface do usuário do Adobe Experience Platform.
exl-id: 1a7a66de-dc57-4a72-8fdd-5fd80175db69
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 1%

---

# Criar um [!DNL Microsoft Dynamics] conexão de origem na interface

Este tutorial fornece etapas para a criação de um [!DNL Microsoft Dynamics] (a seguir designado por &quot;[!DNL Dynamics]&quot;) conexão de origem usando a interface do Adobe Experience Platform.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): a estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
   * [Noções básicas da composição do esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os componentes básicos dos esquemas XDM, incluindo princípios fundamentais e práticas recomendadas na composição do esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

Se você já tiver um [!DNL Dynamics] conta, você pode ignorar o restante deste documento e prosseguir para o tutorial em [configuração de um fluxo de dados para uma origem de CRM](../../dataflow/crm.md).

### Coletar credenciais necessárias

| Credencial | Descrição |
| ---------- | ----------- |
| `serviceUri` | O URL de serviço do [!DNL Dynamics] instância. |
| `username` | O nome de usuário do seu [!DNL Dynamics] conta de usuário. |
| `password` | A senha do [!DNL Dynamics] conta. |
| `servicePrincipalId` | A ID do cliente do [!DNL Dynamics] conta. Essa ID é necessária ao usar a entidade de serviço e a autenticação baseada em chave. |
| `servicePrincipalKey` | A chave secreta da entidade de serviço. Essa credencial é necessária ao usar a entidade de serviço e a autenticação baseada em chave. |

Para obter mais informações sobre a introdução, consulte [este [!DNL Dynamics] documento](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

## Conecte seu [!DNL Dynamics] account

Depois de obter as credenciais necessárias, siga as etapas abaixo para vincular [!DNL Dynamics] para a Platform.

Efetue logon no [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Origens]** na barra de navegação esquerda, para acessar a [!UICONTROL Origens] espaço de trabalho. A variável **[!UICONTROL Catálogo]** A tela exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

No **[!UICONTROL CRM]** categoria, selecione **[!UICONTROL Microsoft Dynamics]**. Se esta for a primeira vez que você usa este conector, selecione **[!UICONTROL Configurar]**. Caso contrário, selecione **[!UICONTROL Adicionar dados]** para criar um novo [!DNL Dynamics] conector.

![catálogo](../../../../images/tutorials/create/ms-dynamics/catalog.png)

A variável **[!UICONTROL Conectar-se ao Dynamics]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada que aparece, forneça um nome e uma descrição opcional para o novo [!DNL Dynamics] conta.

A variável [!DNL Dynamics] O conector da fornece tipos de autenticação de acesso diferentes. Em [!UICONTROL Autenticação de conta] selecionar **[!UICONTROL Autenticação básica]** para usar credenciais baseadas em senha.

Quando terminar, selecione **[!UICONTROL Conectar à origem]** e aguarde algum tempo para a nova conta ser estabelecida.

![basic-authentication](../../../../images/tutorials/create/ms-dynamics/basic-auth.png)

Como alternativa, você pode selecionar **[!UICONTROL Autenticação da entidade de serviço e da chave]** e conecte seu [!DNL Dynamics] conta usando uma combinação de [!UICONTROL ID principal de serviço] e [!UICONTROL Chave principal de serviço].

>[!IMPORTANT]
>
> Autenticação básica no [!DNL Dynamics] pode ser bloqueado pela autenticação de dois fatores, que atualmente não é compatível com a Platform. Nesse caso, é recomendável usar a autenticação baseada em chave para criar um conector de origem usando [!DNL Dynamics].

![autenticação baseada em chave](../../../../images/tutorials/create/ms-dynamics/key-based-auth.png)

| Credencial | Descrição |
| ---------- | ----------- |
| [!UICONTROL ID principal de serviço] | A ID do cliente do [!DNL Dynamics] conta. Essa ID é necessária ao usar a entidade de serviço e a autenticação baseada em chave. |
| [!UICONTROL Chave principal de serviço] | A chave secreta da entidade de serviço. Essa credencial é necessária ao usar a entidade de serviço e a autenticação baseada em chave. |

### Conta existente

Para conectar uma conta existente, selecione a [!DNL Dynamics] conta à qual deseja se conectar e selecione **[!UICONTROL Próxima]** no canto superior direito para continuar.

![existente](../../../../images/tutorials/create/ms-dynamics/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com o seu [!DNL Dynamics] conta. Agora você pode seguir para o próximo tutorial e [configurar um fluxo de dados para trazer dados para a Platform](../../dataflow/crm.md).
