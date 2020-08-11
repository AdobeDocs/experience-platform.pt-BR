---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Criar um conector de origem do Microsoft Dynamics na interface do usuário
topic: overview
translation-type: tm+mt
source-git-commit: 41fe3e5b2a830c3182b46b3e0873b1672a1f1b03
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 1%

---


# Criar um conector [!DNL Microsoft Dynamics] de origem na interface do usuário

Os conectores de origem na Adobe Experience Platform fornecem a capacidade de assimilar dados CRM de origem externa de forma programada. Este tutorial fornece etapas para a criação de um conector de origem [!DNL Microsoft Dynamics] (a seguir denominado &quot;[!DNL Dynamics]&quot;) usando a interface do [!DNL Platform] usuário.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Sistema](../../../../../xdm/home.md)do Experience Data Model (XDM): A estrutura padronizada pela qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição](../../../../../xdm/schema/composition.md)do schema: Saiba mais sobre os elementos básicos dos schemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)do Editor de schemas: Saiba como criar schemas personalizados usando a interface do editor de Schemas.
* [Perfil](../../../../../profile/home.md)do cliente em tempo real: Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

Se você já tiver uma [!DNL Dynamics] conta válida, poderá ignorar o restante deste documento e prosseguir para o tutorial sobre como [configurar um fluxo de dados](../../dataflow/crm.md).

### Reunir credenciais obrigatórias

| Credencial | Descrição |
| ---------- | ----------- |
| `serviceUri` | O URL de serviço da sua [!DNL Dynamics] instância. |
| `username` | O nome de usuário da sua conta [!DNL Dynamics] de usuário. |
| `password` | A senha da sua conta do Dynamics. |

Para obter mais informações sobre a introdução, visite [este documento](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth)do Dynamics.

## Conectar sua [!DNL Dynamics] conta

Depois de reunir as credenciais necessárias, siga as etapas abaixo para criar uma nova [!DNL Dynamics] conta à qual se conectar [!DNL Platform].

Faça logon no [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar a área de trabalho *[!UICONTROL Fontes]* . A tela *[!UICONTROL Catálogo]* exibe várias fontes nas quais você pode criar uma conta de entrada e cada fonte mostra o número de contas e fluxos de conjunto de dados associados a elas.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria *[!UICONTROL Bancos]* de dados, selecione **[!UICONTROL Dinâmica]** seguida por **[!UICONTROL Adicionar dados]** para criar um novo [!DNL Dynamics] conector.

![catálogo](../../../../images/tutorials/create/ms-dynamics/catalog.png)

A página *[!UICONTROL Conectar-se ao Dynamics]* é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se você estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada exibido, forneça à conexão um nome, uma descrição opcional e suas [!DNL Dynamics] credenciais. Quando terminar, selecione **[!UICONTROL Connect]** e aguarde algum tempo para a nova conta ser estabelecida.

![connect](../../../../images/tutorials/create/ms-dynamics/new.png)

### Conta existente

Para conectar uma conta existente, selecione a [!DNL Dynamics] conta à qual deseja se conectar e, em seguida, selecione **[!UICONTROL Próximo]** no canto superior direito para continuar.

![existente](../../../../images/tutorials/create/ms-dynamics/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua [!DNL Dynamics] conta. Agora você pode continuar com o próximo tutorial e [configurar um fluxo de dados para trazer dados para a Plataforma](../../dataflow/crm.md).