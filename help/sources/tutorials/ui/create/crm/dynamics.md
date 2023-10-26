---
keywords: Experience Platform;página inicial;tópicos populares;Microsoft Dynamics;microsoft dynamics;Dynamics;dynamics
solution: Experience Platform
title: Criar uma conexão de origem do Microsoft Dynamics na interface
type: Tutorial
description: Saiba como criar uma conexão de origem do Microsoft Dynamics usando a interface do usuário do Adobe Experience Platform.
exl-id: 1a7a66de-dc57-4a72-8fdd-5fd80175db69
source-git-commit: d22c71fb77655c401f4a336e339aaf8b3125d1b6
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 0%

---

# Criar um [!DNL Microsoft Dynamics] conexão de origem na interface

Este tutorial fornece etapas para criar um [!DNL Microsoft Dynamics] (a seguir designado por &quot;[!DNL Dynamics]&quot;) conexão de origem usando a interface do Adobe Experience Platform.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): a estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
   * [Noções básicas da composição do esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os componentes básicos dos esquemas XDM, incluindo princípios fundamentais e práticas recomendadas na composição do esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

Se você já tiver um [!DNL Dynamics] conta, você pode ignorar o restante deste documento e prosseguir para o tutorial em [configuração de um fluxo de dados para uma origem de CRM](../../dataflow/crm.md).

### Coletar credenciais necessárias

Para autenticar seu [!DNL Dynamics] , você deve fornecer valores para as seguintes propriedades de conexão:

>[!BEGINTABS]

>[!TAB Autenticação básica]

| Credencial | Descrição |
| --- | --- |
| `serviceUri` | O URL de serviço do [!DNL Dynamics] instância. |
| `username` | O nome de usuário do seu [!DNL Dynamics] conta de usuário. |
| `password` | A senha do [!DNL Dynamics] conta. |

>[!TAB Autenticação da entidade de serviço e da chave]

| Credencial | Descrição |
| --- | --- |
| `servicePrincipalId` | A ID do cliente do [!DNL Dynamics] conta. Essa ID é necessária ao usar a entidade de serviço e a autenticação baseada em chave. |
| `servicePrincipalKey` | A chave secreta da entidade de serviço. Essa credencial é necessária ao usar a entidade de serviço e a autenticação baseada em chave. |

>[!ENDTABS]

Para obter mais informações sobre a introdução, consulte [este [!DNL Dynamics] documento](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

## Conecte seu [!DNL Dynamics] account

Na interface do usuário da Platform, selecione **[!UICONTROL Origens]** na navegação à esquerda, para acessar a [!UICONTROL Origens] espaço de trabalho. A variável [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

No [!UICONTROL CRM] categoria, selecione **[!UICONTROL Microsoft Dynamics]** e selecione **[!UICONTROL Adicionar dados]**.

![O catálogo de origens com o Microsoft Dynamics selecionado.](../../../../images/tutorials/create/ms-dynamics/catalog.png)

A variável **[!UICONTROL Conectar a conta do Microsoft Dynamics]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Conta existente

Para usar uma conta existente, selecione a variável [!DNL Dynamics] conta que deseja usar e selecione **[!UICONTROL Próxima]** no canto superior direito para continuar.

![A interface de conta existente.](../../../../images/tutorials/create/ms-dynamics/existing.png)

### Nova conta

>[!TIP]
>
>Depois de criado, não é possível alterar o tipo de autenticação de um [!DNL Dynamics] conexão básica. Para alterar o tipo de autenticação, você deve criar uma nova conexão base.

Para criar uma nova conta, selecione **[!UICONTROL Nova conta]** e forneça um nome e uma descrição opcional para o novo [!DNL Dynamics] conta.

![A interface de criação de novas contas.](../../../../images/tutorials/create/ms-dynamics/new.png)

Você pode usar a autenticação básica ou a autenticação de entidade de serviço e chave ao criar uma [!DNL Dynamics] conta.

>[!BEGINTABS]

>[!TAB Autenticação básica]

Para criar um [!DNL Dynamics] com autenticação básica, selecione [!UICONTROL Autenticação básica] e forneça valores para o [!UICONTROL URI do serviço], [!UICONTROL Nome de usuário], e [!UICONTROL Senha]. **Nota**: Autenticação básica no [!DNL Dynamics] pode ser bloqueado pela autenticação de dois fatores, que atualmente não é compatível com a Platform. Nesse caso, é recomendável usar a autenticação baseada em chave para criar um conector de origem usando [!DNL Dynamics].

Quando terminar, selecione **[!UICONTROL Conectar à origem]** e aguarde algum tempo para a nova conta ser estabelecida.

![A interface de autenticação básica.](../../../../images/tutorials/create/ms-dynamics/basic-authentication.png)

>[!TAB Autenticação da entidade de serviço e da chave]

Para criar um [!DNL Dynamics] conta com autenticação de entidade de serviço e chave, selecione **[!UICONTROL Autenticação da entidade de serviço e da chave]** e forneça valores para o [!UICONTROL ID principal de serviço] e [!UICONTROL Chave principal de serviço].

Quando terminar, selecione **[!UICONTROL Conectar à origem]** e aguarde algum tempo para a nova conta ser estabelecida.

![A interface de autenticação da chave da entidade de serviço.](../../../../images/tutorials/create/ms-dynamics/service-principal.png)

>[!ENDTABS]

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com o seu [!DNL Dynamics] conta. Agora você pode seguir para o próximo tutorial e [configurar um fluxo de dados para trazer dados para a Platform](../../dataflow/crm.md).
