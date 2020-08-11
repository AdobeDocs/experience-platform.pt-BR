---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Criar um conector de origem da Salesforce Service Cloud na interface do usuário
topic: overview
translation-type: tm+mt
source-git-commit: 41fe3e5b2a830c3182b46b3e0873b1672a1f1b03
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 0%

---


# Criar um conector [!DNL Salesforce Service Cloud] de origem na interface do usuário

>[!NOTE]
>O [!DNL Salesforce Service Cloud] conector está em beta. Consulte a visão geral [das](../../../../home.md#terms-and-conditions) Fontes para obter mais informações sobre o uso de conectores com rótulo beta.

Os conectores de origem na Adobe Experience Platform fornecem a capacidade de assimilar dados de origem externa de forma programada. Este tutorial fornece etapas para a criação de um conector de origem [!DNL Salesforce Service Cloud] (a seguir denominado &quot;SSC&quot;) usando a interface do [!DNL Platform] usuário.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Sistema](../../../../../xdm/home.md)do Experience Data Model (XDM): A estrutura padronizada pela qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição](../../../../../xdm/schema/composition.md)do schema: Saiba mais sobre os elementos básicos dos schemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)do Editor de schemas: Saiba como criar schemas personalizados usando a interface do editor de Schemas.
* [Perfil](../../../../../profile/home.md)do cliente em tempo real: Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

Se você já tiver uma conexão SSC válida, poderá ignorar o restante deste documento e prosseguir para o tutorial sobre como [configurar um fluxo de dados](../../dataflow/customer-success.md)

### Reunir credenciais obrigatórias

Para acessar sua conta SSC em [!DNL Platform], forneça os seguintes valores:

| Credencial | Descrição |
| ---------- | ----------- |
| `username` | O nome de usuário da conta de usuário. |
| `password` | A senha da conta de usuário. |
| `securityToken` | O token de segurança da conta de usuário. |

Para obter mais informações sobre a introdução, consulte [este documento](https://developer.salesforce.com/docs/atlas.en-us.api_iot.meta/api_iot/qs_auth_access_token.htm)da Salesforce Service Cloud.

## Conectar sua [!DNL Salesforce Service Cloud] conta

Depois de reunir as credenciais necessárias, siga as etapas abaixo para criar uma nova conta SSC à qual se conectar [!DNL Platform].

Faça logon no [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar a área de trabalho *[!UICONTROL Fontes]* . A tela *[!UICONTROL Catálogo]* exibe várias fontes para as quais você pode criar uma conta de entrada, e cada fonte mostra o número de contas e fluxos de conjunto de dados existentes associados a elas.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria *[!UICONTROL Customer Success (Sucesso]* do cliente), selecione **[!UICONTROL Salesforce Service Cloud]** para exibir uma barra de informações no lado direito da tela. A barra de informações fornece uma breve descrição para a fonte selecionada, bem como opções para se conectar à fonte ou à sua documentação de visualização. Para criar uma nova conexão de entrada, selecione **[!UICONTROL Adicionar dados]**.

![catálogo](../../../../images/tutorials/create/ssc/catalog.png)

A página *[!UICONTROL Conectar-se ao Salesforce Service Cloud]* é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se você estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada exibido, forneça à conexão um nome, uma descrição opcional e suas credenciais do SSC. Quando terminar, selecione **[!UICONTROL Connect]** e aguarde algum tempo para a nova conta ser estabelecida.

![connect](../../../../images/tutorials/create/ssc/connect.png)

### Conta existente

Para conectar uma conta existente, selecione a conta SSC à qual deseja se conectar e, em seguida, selecione **[!UICONTROL Avançar]** para continuar.

![existente](../../../../images/tutorials/create/ssc/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta SSC. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer os dados de sucesso do cliente para a Plataforma](../../dataflow/customer-success.md).