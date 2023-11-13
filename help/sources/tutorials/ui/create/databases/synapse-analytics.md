---
title: Criar uma conexão de origem do Azure synapse Analytics na interface
description: Saiba como criar uma conexão de origem do Azure synapse Analytics (doravante "Synapse") usando a interface do usuário do Adobe Experience Platform.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 1f1ce317-eaaf-4ad2-a5fb-236983220bd7
source-git-commit: a7c2c5e4add5c80e0622d5aeb766cec950d79dbb
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 1%

---

# Criar um [!DNL Azure Synapse Analytics] conexão de origem na interface

>[!IMPORTANT]
>
>A variável [!DNL Azure Synapse Analytics] origem está disponível no catálogo de origens para usuários que compraram o Real-time Customer Data Platform Ultimate.

Este tutorial fornece etapas para a criação de um [!DNL Azure Synapse Analytics] (a seguir designado por &quot;[!DNL Synapse]&quot;) conector de origem usando o [!DNL Platform] interface do usuário.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): o quadro normalizado pelo qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição do esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os componentes básicos dos esquemas XDM, incluindo princípios fundamentais e práticas recomendadas na composição do esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

Se você já tiver um [!DNL Synapse] conexão, você pode ignorar o restante deste documento e prosseguir para o tutorial em [configuração de um fluxo de dados](../../dataflow/databases.md).

### Coletar credenciais necessárias

Para acessar seu [!DNL Synapse] conta em [!DNL Platform], você deve fornecer os seguintes valores:

| Credencial | Descrição |
| ---------- | ----------- |
| `connectionString` | A cadeia de conexão associada ao seu [!DNL Synapse] autenticação. A variável [!DNL Synapse] o padrão da cadeia de conexão é `Server=tcp:{SERVER_NAME}.database.windows.net,1433;Database={DATABASE};User ID={USERNAME}@{SERVER_NAME};Password={PASSWORD};Trusted_Connection=False;Encrypt=True;Connection Timeout=30`. |

Para obter mais informações sobre esse valor, consulte [este [!DNL Synapse] documento](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-sql-data-warehouse).

## Conecte seu [!DNL Synapse] account

Depois de obter as credenciais necessárias, siga as etapas abaixo para vincular [!DNL Synapse] conta para [!DNL Platform].

Efetue logon no [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Origens]** na barra de navegação esquerda, para acessar a **[!UICONTROL Origens]** espaço de trabalho. A variável **[!UICONTROL Catálogo]** A tela exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

No **[!UICONTROL Bancos de dados]** categoria, selecione **[!UICONTROL Azure synapse Analytics]**. Se esta for a primeira vez que você usa este conector, selecione **[!UICONTROL Configurar]**. Caso contrário, selecione **[!UICONTROL Adicionar dados]** para criar um novo [!DNL Synapse] conector.

![](../../../../images/tutorials/create/azure-synapse-analytics/catalog.png)

A variável **[!UICONTROL Conectar ao Azure synapse Analytics]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada que aparece, forneça um nome, uma descrição opcional e [!DNL Synapse] credenciais. Quando terminar, selecione **[!UICONTROL Conectar]** e aguarde algum tempo para estabelecer a nova conexão.

![](../../../../images/tutorials/create/azure-synapse-analytics/new.png)

### Conta existente

Para conectar uma conta existente, selecione a [!DNL Synapse] conta à qual deseja se conectar e selecione **[!UICONTROL Próxima]** para continuar.

![](../../../../images/tutorials/create/azure-synapse-analytics/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com o seu [!DNL Synapse] conta. Agora você pode seguir para o próximo tutorial e [configurar um fluxo de dados para trazer dados para o [!DNL Platform]](../../dataflow/databases.md).
