---
keywords: Experience Platform;home;popular topics;ServiceNow;servicenow
solution: Experience Platform
title: Criar um conector de origem ServiceNow na interface do usuário
topic: overview
description: Este tutorial fornece etapas para a criação de um conector de origem ServiceNow usando a interface do usuário da plataforma.
translation-type: tm+mt
source-git-commit: f82dfee2c75a0b8b2ec1615266780b309152ead4
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 1%

---


# Criar um conector [!DNL ServiceNow] de origem na interface do usuário

>[!NOTE]
>
>O [!DNL ServiceNow] conector está em beta. Consulte a visão geral [das](../../../../home.md#terms-and-conditions) Fontes para obter mais informações sobre o uso de conectores com rótulo beta.

Os conectores de origem na Adobe Experience Platform fornecem a capacidade de assimilar dados de origem externa de forma programada. Este tutorial fornece etapas para criar um conector de [!DNL ServiceNow] origem usando a interface do [!DNL Platform] usuário.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model] (XDM) Sistema](../../../../../xdm/home.md): A estrutura padronizada pela qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição](../../../../../xdm/schema/composition.md)do schema: Saiba mais sobre os elementos básicos dos schemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)do Editor de schemas: Saiba como criar schemas personalizados usando a interface do editor de Schemas.
* [[!DNL Perfil do cliente em tempo real]](../../../../../profile/home.md): Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

Se você já tiver uma [!DNL ServiceNow] conexão válida, poderá ignorar o restante desse documento e prosseguir para o tutorial sobre como [configurar um fluxo de dados](../../dataflow/customer-success.md)

### Reunir credenciais obrigatórias

Para acessar sua [!DNL ServiceNow] conta em [!DNL Platform], forneça os seguintes valores:

| Credencial | Descrição |
| ---------- | ----------- |
| `endpoint` | The endpoint of the [!DNL ServiceNow] server. |
| `username` | O nome de usuário usado para se conectar ao [!DNL ServiceNow] servidor para autenticação. |
| `password` | A senha para conectar-se ao [!DNL ServiceNow] servidor para autenticação. |

Para obter mais informações sobre a introdução, consulte [ [!DNL ServiceNow] este documento](https://developer.servicenow.com/app.do#!/rest_api_doc?v=newyork&amp;id=r_TableAPI-GET).

## Conectar sua [!DNL ServiceNow] conta

Depois de reunir as credenciais necessárias, siga as etapas abaixo para vincular sua [!DNL ServiceNow] conta a [!DNL Platform].

Faça logon no [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar a área de trabalho **[!UICONTROL Fontes]** . A tela **[!UICONTROL Catálogo]** exibe várias fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Em **[!UICONTROL categoria de sucesso]** do cliente, selecione **[!UICONTROL ServiceNow]**. Se esta for a sua primeira vez usando este conector, selecione **[!UICONTROL Configurar]**. Caso contrário, selecione **[!UICONTROL Conectar fonte]** para criar um novo [!DNL ServiceNow] conector.

![](../../../../images/tutorials/create/servicenow/catalog.png)

A página **[!UICONTROL Conectar-se ao ServiceNow]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se você estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada exibido, forneça um nome, uma descrição opcional e suas [!DNL ServiceNow] credenciais. Quando terminar, selecione **[!UICONTROL Connect]** e aguarde algum tempo para a nova conexão ser estabelecida.

![](../../../../images/tutorials/create/servicenow/new.png)

### Conta existente

Para conectar uma conta existente, selecione a [!DNL ServiceNow] conta à qual deseja se conectar e, em seguida, selecione **[!UICONTROL Avançar]** para continuar.

![](../../../../images/tutorials/create/servicenow/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua [!DNL ServiceNow] conta. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer [!DNL Platform]](../../dataflow/customer-success.md)os dados para o
