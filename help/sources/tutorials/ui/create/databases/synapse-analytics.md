---
keywords: Experience Platform, home, tópicos populares, Azure synapse Analytics, Synapse, sinapse, azure synapse analytics
solution: Experience Platform
title: Criar uma conexão de origem do Azure synapse Analytics na interface do usuário
topic-legacy: overview
type: Tutorial
description: Saiba como criar uma conexão de origem do Azure synapse Analytics (a seguir, "Synapse") usando a interface do usuário do Adobe Experience Platform.
exl-id: 1f1ce317-eaaf-4ad2-a5fb-236983220bd7
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 1%

---

# Criar uma conexão de origem [!DNL Azure Synapse Analytics] na interface do usuário

>[!NOTE]
>
> O conector [!DNL Azure Synapse Analytics] está em beta. Consulte a [Visão geral das Fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores com marca beta.

Os conectores de origem no Adobe Experience Platform oferecem a capacidade de assimilar dados de origem externa de acordo com a programação. Este tutorial fornece etapas para criar um conector de origem [!DNL Azure Synapse Analytics] (a seguir chamado &quot;[!DNL Synapse]&quot;) usando a interface do usuário [!DNL Platform].

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): A estrutura padronizada pela qual  [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição](../../../../../xdm/schema/composition.md) do schema: Saiba mais sobre os elementos básicos dos esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md) do Editor de esquema: Saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.

Se você já tiver uma conexão válida [!DNL Synapse], poderá ignorar o restante deste documento e prosseguir para o tutorial em [configurar um fluxo de dados](../../dataflow/databases.md).

### Obter credenciais necessárias

Para acessar sua conta [!DNL Synapse] em [!DNL Platform], você deve fornecer os seguintes valores:

| Credencial | Descrição |
| ---------- | ----------- |
| `connectionString` | A cadeia de conexão associada à autenticação [!DNL Synapse]. O padrão da string de conexão [!DNL Synapse] é `Server=tcp:{SERVER_NAME}.database.windows.net,1433;Database={DATABASE};User ID={USERNAME}@{SERVER_NAME};Password={PASSWORD};Trusted_Connection=False;Encrypt=True;Connection Timeout=30`. |

Para obter mais informações sobre esse valor, consulte [this [!DNL Synapse] document](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-sql-data-warehouse).

## Conecte sua conta [!DNL Synapse]

Depois de coletar suas credenciais necessárias, siga as etapas abaixo para vincular sua conta [!DNL Synapse] a [!DNL Platform].

Faça logon em [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Sources]** na barra de navegação esquerda para acessar o espaço de trabalho **[!UICONTROL Sources]**. A tela **[!UICONTROL Catalog]** exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria **[!UICONTROL Databases]**, selecione **[!UICONTROL Azure Synapse Analytics]**. Se esta for a primeira vez que você usa esse conector, selecione **[!UICONTROL Configure]**. Caso contrário, selecione **[!UICONTROL Add data]** para criar um novo conector [!DNL Synapse].

![](../../../../images/tutorials/create/azure-synapse-analytics/catalog.png)

A página **[!UICONTROL Connect to Azure Synapse Analytics]** é exibida. Nesta página, você pode usar novas credenciais ou credenciais existentes.

### Nova conta

Se estiver usando novas credenciais, selecione **[!UICONTROL New account]**. No formulário de entrada exibido, forneça um nome, uma descrição opcional e suas credenciais [!DNL Synapse]. Quando terminar, selecione **[!UICONTROL Connect]** e aguarde algum tempo para que a nova conexão seja estabelecida.

![](../../../../images/tutorials/create/azure-synapse-analytics/new.png)

### Conta existente

Para conectar uma conta existente, selecione a conta [!DNL Synapse] com a qual deseja se conectar e selecione **[!UICONTROL Next]** para prosseguir.

![](../../../../images/tutorials/create/azure-synapse-analytics/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta [!DNL Synapse]. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer dados para [!DNL Platform]](../../dataflow/databases.md).
