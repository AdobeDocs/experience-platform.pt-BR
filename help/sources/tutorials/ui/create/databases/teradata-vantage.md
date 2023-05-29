---
keywords: Experience Platform;página inicial;tópicos populares;Vantagem de Teradata
title: Criar uma Conexão de Origem do Teradata Vantage na interface do usuário
description: Saiba como criar uma conexão de origem do Teradata Vantage usando a interface do usuário do Adobe Experience Platform.
exl-id: 3fdb09fa-128a-477b-9144-d4ef3ed18ea6
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 1%

---

# (Beta) Criar um [!DNL Teradata Vantage] conexão de origem na interface

>[!NOTE]
>
> A variável [!DNL Teradata Vantage] a fonte está na versão beta. Consulte a [Visão geral das fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de fontes rotuladas como beta.

Este tutorial fornece etapas para a criação de um [!DNL Teradata Vantage] conector de origem usando a interface do usuário do Adobe Experience Platform.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes da Platform:

* [Origens](../../../../home.md): o Experience Platform permite que os dados sejam assimilados de várias fontes e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços Experience Platform.
* [Sandboxes](../../../../../sandboxes/home.md): o Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

### Coletar credenciais necessárias

Para acessar seu [!DNL Teradata Vantage] na Platform, você deve fornecer o seguinte valor de autenticação:

| Credencial | Descrição |
| ---------- | ----------- |
| String de conexão | Uma cadeia de conexão é uma cadeia que fornece informações sobre uma fonte de dados e como você pode se conectar a ela. O padrão da cadeia de conexão para [!DNL Teradata Vantage] é `DBCName={SERVER};Uid={USERNAME};Pwd={PASSWORD}`. |

Para obter mais informações sobre a introdução, consulte esta [[!DNL Teradata Vantage] documento](https://docs.teradata.com/r/Teradata-VantageTM-Advanced-SQL-Engine-Security-Administration/July-2021/Setting-Up-the-Administrative-Infrastructure/Controlling-Access-to-the-Operating-System/Working-with-OS-Level-Security-Options).

## Conecte seu [!DNL Teradata Vantage] account

Na interface do usuário da Platform, selecione **[!UICONTROL Origens]** na navegação à esquerda, para acessar a [!UICONTROL Origens] espaço de trabalho. A variável [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a barra de pesquisa.

No [!UICONTROL Bancos de dados] categoria, selecione **[!UICONTROL Vantagem do teradata]** e selecione **[!UICONTROL Adicionar dados]**.

![](../../../../images/tutorials/create/teradata/catalog.png)

A variável **[!UICONTROL Conectar ao Teradata Vantage]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Conta existente

Para conectar uma conta existente, selecione a [!DNL Teradata Vantage] conta à qual deseja se conectar e selecione **[!UICONTROL Próxima]** para continuar.

![](../../../../images/tutorials/create/teradata/existing.png)

### Nova conta

Se estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada que aparece, forneça um nome, uma descrição opcional e [!DNL Teradata Vantage] credenciais. Quando terminar, selecione **[!UICONTROL Conectar]** e aguarde algum tempo para estabelecer a nova conexão.

![](../../../../images/tutorials/create/teradata/new.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta do Teradata Vantage. Agora você pode seguir para o próximo tutorial e [configurar um fluxo de dados para trazer dados para a Platform](../../dataflow/databases.md).
