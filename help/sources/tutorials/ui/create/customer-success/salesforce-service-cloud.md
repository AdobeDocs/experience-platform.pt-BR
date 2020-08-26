---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Criar um conector de origem da Salesforce Service Cloud na interface do usuário
topic: overview
translation-type: tm+mt
source-git-commit: 690ddbd92f0a2e4e06b988e761dabff399cd2367
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 1%

---


# Criar um conector [!DNL Salesforce Service Cloud] de origem na interface do usuário

>[!NOTE]
>
>O [!DNL Salesforce Service Cloud] conector está em beta. Consulte a visão geral [das](../../../../home.md#terms-and-conditions) Fontes para obter mais informações sobre o uso de conectores com rótulo beta.

Os conectores de origem na Adobe Experience Platform fornecem a capacidade de assimilar dados de origem externa de forma programada. Este tutorial fornece etapas para a criação de um conector de origem [!DNL Salesforce Service Cloud] (a seguir denominado &quot;SSC&quot;) usando a interface do [!DNL Platform] usuário.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model] (XDM) Sistema](../../../../../xdm/home.md): A estrutura padronizada pela qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição](../../../../../xdm/schema/composition.md)do schema: Saiba mais sobre os elementos básicos dos schemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)do Editor de schemas: Saiba como criar schemas personalizados usando a interface do editor de Schemas.
* [[!DNL Perfil do cliente em tempo real]](../../../../../profile/home.md): Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

Se você já tiver uma conexão SSC válida, poderá ignorar o restante deste documento e prosseguir para o tutorial sobre como [configurar um fluxo de dados](../../dataflow/customer-success.md)

### Reunir credenciais obrigatórias

Para acessar sua conta SSC em [!DNL Platform], forneça os seguintes valores:

| Credencial | Descrição |
| ---------- | ----------- |
| `username` | O nome de usuário da conta de usuário. |
| `password` | A senha da conta de usuário. |
| `securityToken` | O token de segurança da conta de usuário. |

Para obter mais informações sobre a introdução, consulte [ [!DNL Salesforce Service Cloud] este documento](https://developer.salesforce.com/docs/atlas.en-us.api_iot.meta/api_iot/qs_auth_access_token.htm).

## Conectar sua [!DNL Salesforce Service Cloud] conta

Depois de reunir as credenciais necessárias, siga as etapas abaixo para vincular sua conta SSC a [!DNL Platform].

Faça logon no [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar a área de trabalho **[!UICONTROL Fontes]** . A tela **[!UICONTROL Catálogo]** exibe várias fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Em **[!UICONTROL categoria de sucesso]** do cliente, selecione **[!UICONTROL Salesforce Service Cloud]**. Se esta for a sua primeira vez usando este conector, selecione **[!UICONTROL Configurar]**. Caso contrário, selecione **[!UICONTROL Adicionar dados]** para criar um novo conector SSC.

![catálogo](../../../../images/tutorials/create/ssc/catalog.png)

A página **[!UICONTROL Conectar-se ao Salesforce Service Cloud]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se você estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada exibido, forneça um nome, uma descrição opcional e suas credenciais do SSC. Quando terminar, selecione **[!UICONTROL Connect]** e aguarde algum tempo para a nova conexão ser estabelecida.

![connect](../../../../images/tutorials/create/ssc/connect.png)

### Conta existente

Para conectar uma conta existente, selecione a conta SSC à qual deseja se conectar e, em seguida, selecione **[!UICONTROL Avançar]** para continuar.

![existente](../../../../images/tutorials/create/ssc/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta SSC. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer os dados de sucesso do cliente para [!DNL Platform]](../../dataflow/customer-success.md)o