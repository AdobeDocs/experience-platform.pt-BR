---
keywords: Experience Platform, home, tópicos populares, Microsoft Dynamics, microsoft dynamics, Dynamics, dinâmica
solution: Experience Platform
title: Criar uma conexão de origem do Microsoft Dynamics na interface do usuário
type: Tutorial
description: Saiba como criar uma conexão de origem do Microsoft Dynamics usando a interface do usuário do Adobe Experience Platform.
exl-id: 1a7a66de-dc57-4a72-8fdd-5fd80175db69
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 1%

---

# Crie um [!DNL Microsoft Dynamics] conexão de origem na interface do usuário

Este tutorial fornece etapas para criar um [!DNL Microsoft Dynamics] (a seguir designado por &quot;[!DNL Dynamics]&quot;) conexão de origem usando a interface do usuário do Adobe Experience Platform.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): A estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
   * [Noções básicas da composição do schema](../../../../../xdm/schema/composition.md): Saiba mais sobre os elementos básicos dos esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.

Se você já tiver um [!DNL Dynamics] , você pode ignorar o restante deste documento e prosseguir para o tutorial em [configuração de um fluxo de dados para uma fonte CRM](../../dataflow/crm.md).

### Obter credenciais necessárias

| Credencial | Descrição |
| ---------- | ----------- |
| `serviceUri` | O URL de serviço do [!DNL Dynamics] instância. |
| `username` | O nome de usuário para seu [!DNL Dynamics] conta do usuário. |
| `password` | A senha de seu [!DNL Dynamics] conta. |
| `servicePrincipalId` | A ID de cliente do [!DNL Dynamics] conta. Essa ID é necessária ao usar a principal de serviço e a autenticação baseada em chave. |
| `servicePrincipalKey` | A chave secreta da entidade de serviço. Essa credencial é necessária ao usar a entidade de serviço e a autenticação baseada em chave. |

Para obter mais informações sobre a introdução, consulte [this [!DNL Dynamics] documento](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

## Conecte seu [!DNL Dynamics] account

Depois de reunir suas credenciais necessárias, siga as etapas abaixo para vincular seus [!DNL Dynamics] para a Platform.

Faça logon em [Adobe Experience Platform](https://platform.adobe.com) e depois selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar o [!UICONTROL Fontes] espaço de trabalho. O **[!UICONTROL Catálogo]** exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Em **[!UICONTROL CRM]** categoria , selecione **[!UICONTROL Microsoft Dynamics]**. Se esta for a primeira vez que você usa esse conector, selecione **[!UICONTROL Configurar]**. Caso contrário, selecione **[!UICONTROL Adicionar dados]** para criar um novo [!DNL Dynamics] conector.

![catálogo](../../../../images/tutorials/create/ms-dynamics/catalog.png)

O **[!UICONTROL Conectar ao Dynamics]** será exibida. Nesta página, você pode usar novas credenciais ou credenciais existentes.

### Nova conta

Se estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada exibido, forneça um nome e uma descrição opcional para o novo [!DNL Dynamics] conta.

O [!DNL Dynamics] O conector fornece tipos de autenticação diferentes para acesso. Em [!UICONTROL Autenticação da conta] select **[!UICONTROL Autenticação básica]** para usar credenciais baseadas em senha.

Quando terminar, selecione **[!UICONTROL Conectar-se à origem]** e, em seguida, permitir que a nova conta seja criada.

![autenticação básica](../../../../images/tutorials/create/ms-dynamics/basic-auth.png)

Como alternativa, você pode selecionar **[!UICONTROL Autenticação de chave e principal de serviço]** e conecte seu [!DNL Dynamics] conta usando uma combinação de [!UICONTROL ID da entidade de serviço] e [!UICONTROL Chave de entidade de serviço].

>[!IMPORTANT]
>
> Autenticação básica em [!DNL Dynamics] pode ser bloqueada pela autenticação de dois fatores, que atualmente não é compatível com a Platform. Nesse caso, é recomendável usar a autenticação baseada em chave para criar um conector de origem usando [!DNL Dynamics].

![autenticação baseada em chave](../../../../images/tutorials/create/ms-dynamics/key-based-auth.png)

| Credencial | Descrição |
| ---------- | ----------- |
| [!UICONTROL ID da entidade de serviço] | A ID de cliente do [!DNL Dynamics] conta. Essa ID é necessária ao usar a principal de serviço e a autenticação baseada em chave. |
| [!UICONTROL Chave de entidade de serviço] | A chave secreta da entidade de serviço. Essa credencial é necessária ao usar a entidade de serviço e a autenticação baseada em chave. |

### Conta existente

Para conectar uma conta existente, selecione a [!DNL Dynamics] conta com a qual deseja se conectar e selecione **[!UICONTROL Próximo]** no canto superior direito para continuar.

![existente](../../../../images/tutorials/create/ms-dynamics/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com seu [!DNL Dynamics] conta. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer dados para a plataforma](../../dataflow/crm.md).
