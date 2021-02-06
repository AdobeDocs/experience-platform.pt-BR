---
keywords: Experience Platform;home;popular tópicos;Microsoft Dynamics;Microsoft Dynamics;Dynamics;dynamic;dynamics;;home;popular topics;Microsoft Dynamics;Microsoft Dynamics;Dynamics;dynamics
solution: Experience Platform
title: Criar uma conexão de origem do Microsoft Dynamics na interface do usuário
topic: overview
type: Tutorial
description: Saiba como criar uma conexão de origem do Microsoft Dynamics usando a interface do usuário do Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 1%

---


# Criar uma conexão de origem [!DNL Microsoft Dynamics] na interface do usuário

Este tutorial fornece etapas para a criação de uma conexão de origem [!DNL Microsoft Dynamics] (a seguir denominada &quot;[!DNL Dynamics]&quot;) usando a interface do usuário do Adobe Experience Platform.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): A estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
   * [Noções básicas da composição](../../../../../xdm/schema/composition.md) do schema: Saiba mais sobre os elementos básicos dos schemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md) do Editor de schemas: Saiba como criar schemas personalizados usando a interface do editor de Schemas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

Se você já tiver uma conta [!DNL Dynamics] válida, poderá ignorar o restante deste documento e prosseguir para o tutorial em [configurar um fluxo de dados para uma fonte CRM](../../dataflow/crm.md).

### Reunir credenciais obrigatórias

| Credencial | Descrição |
| ---------- | ----------- |
| `serviceUri` | O URL de serviço da sua instância [!DNL Dynamics]. |
| `username` | O nome de usuário para sua conta de usuário [!DNL Dynamics]. |
| `password` | A senha da sua conta [!DNL Dynamics]. |
| `servicePrincipalId` | A ID do cliente da sua conta [!DNL Dynamics]. Essa ID é necessária ao usar a principal do serviço e a autenticação baseada em chave. |
| `servicePrincipalKey` | A chave secreta principal do serviço. Essa credencial é necessária ao usar a principal do serviço e a autenticação baseada em chave. |

Para obter mais informações sobre a introdução, consulte [this [!DNL Dynamics] documento](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

## Conectar sua conta [!DNL Dynamics]

Depois de reunir as credenciais necessárias, siga as etapas abaixo para vincular sua conta [!DNL Dynamics] à Plataforma.

Faça logon em [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar a área de trabalho [!UICONTROL Fontes]. A tela **[!UICONTROL Catalog]** exibe várias fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria **[!UICONTROL CRM]**, selecione **[!UICONTROL Microsoft Dynamics]**. Se esta for a sua primeira vez usando este conector, selecione **[!UICONTROL Configurar]**. Caso contrário, selecione **[!UICONTROL Adicionar dados]** para criar um novo conector [!DNL Dynamics].

![catálogo](../../../../images/tutorials/create/ms-dynamics/catalog.png)

A página **[!UICONTROL Conectar-se ao Dynamics]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se você estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada exibido, forneça um nome e uma descrição opcional para sua nova conta [!DNL Dynamics].

O conector [!DNL Dynamics] fornece tipos de autenticação diferentes para acesso. Em [!UICONTROL Autenticação de conta] selecione **[!UICONTROL Autenticação básica]** para utilizar credenciais baseadas em senha.

Quando terminar, selecione **[!UICONTROL Ligar à origem]** e, em seguida, conceda algum tempo para a nova conta estabelecer.

![autenticação básica](../../../../images/tutorials/create/ms-dynamics/basic-auth.png)

Como alternativa, você pode selecionar **[!UICONTROL Autenticação principal do serviço e da chave]** e conectar sua conta [!DNL Dynamics] usando uma combinação de [!UICONTROL ID principal do serviço] e [!UICONTROL Chave principal do serviço].

>[!IMPORTANT]
>
> A autenticação básica em [!DNL Dynamics] pode ser bloqueada pela autenticação de dois fatores, que atualmente não é suportada pela Plataforma. Nesse caso, é recomendável usar a autenticação baseada em chave para criar um conector de origem usando [!DNL Dynamics].

![autenticação baseada em chave](../../../../images/tutorials/create/ms-dynamics/key-based-auth.png)

| Credencial | Descrição |
| ---------- | ----------- |
| [!UICONTROL ID do principal do serviço] | A ID do cliente da sua conta [!DNL Dynamics]. Essa ID é necessária ao usar a principal do serviço e a autenticação baseada em chave. |
| [!UICONTROL Chave principal do serviço] | A chave secreta principal do serviço. Essa credencial é necessária ao usar a principal do serviço e a autenticação baseada em chave. |

### Conta existente

Para conectar uma conta existente, selecione a conta [!DNL Dynamics] com a qual deseja se conectar e, em seguida, selecione **[!UICONTROL Próximo]** no canto superior direito para prosseguir.

![existente](../../../../images/tutorials/create/ms-dynamics/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta [!DNL Dynamics]. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer dados para a Plataforma](../../dataflow/crm.md).