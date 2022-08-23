---
keywords: Experience Platform, home, tópicos populares, Teradata Vantagem
title: Criar uma conexão de origem de vantagem de Teradata na interface do usuário
description: Saiba como criar uma conexão fonte de Vantagem do Teradata usando a interface do usuário do Adobe Experience Platform.
source-git-commit: f140dac67ccd09ec1e6cab794f53e0090af55442
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 1%

---

# (Beta) Criar um [!DNL Teradata Vantage] conexão de origem na interface do usuário

>[!NOTE]
>
> O [!DNL Teradata Vantage] A fonte está em beta. Consulte a [Visão geral das fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de fontes com rótulo beta.

Este tutorial fornece etapas para criar um [!DNL Teradata Vantage] conector de origem usando a interface do usuário do Adobe Experience Platform.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes da Platform:

* [Fontes](../../../../home.md): O Experience Platform permite que os dados sejam assimilados de várias fontes, fornecendo a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços do Experience Platform.
* [Sandboxes](../../../../../sandboxes/home.md): O Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

### Obter credenciais necessárias

Para acessar o [!DNL Teradata Vantage] na Platform, você deve fornecer o seguinte valor de autenticação:

| Credencial | Descrição |
| ---------- | ----------- |
| Cadeia de conexão | Uma string de conexão é uma string que fornece informações sobre uma fonte de dados e como você pode se conectar a ela. O padrão da string de conexão para [!DNL Teradata Vantage] é `DBCName={SERVER};Uid={USERNAME};Pwd={PASSWORD}`. |

Para obter mais informações sobre a introdução, consulte esta seção [[!DNL Teradata Vantage] documento](https://docs.teradata.com/r/Teradata-VantageTM-Advanced-SQL-Engine-Security-Administration/July-2021/Setting-Up-the-Administrative-Infrastructure/Controlling-Access-to-the-Operating-System/Working-with-OS-Level-Security-Options).

## Conecte seu [!DNL Teradata Vantage] account

Na interface do usuário da plataforma, selecione **[!UICONTROL Fontes]** na navegação à esquerda para acessar o [!UICONTROL Fontes] espaço de trabalho. O [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a barra de pesquisa.

Em [!UICONTROL Bancos de dados] categoria , selecione **[!UICONTROL Vantagem do teradata]** e depois selecione **[!UICONTROL Adicionar dados]**.

![](../../../../images/tutorials/create/teradata/catalog.png)

O **[!UICONTROL Conectar-se à Vantagem do Teradata]** será exibida. Nesta página, você pode usar novas credenciais ou credenciais existentes.

### Conta existente

Para conectar uma conta existente, selecione a [!DNL Teradata Vantage] conta com a qual deseja se conectar e selecione **[!UICONTROL Próximo]** para continuar.

![](../../../../images/tutorials/create/teradata/existing.png)

### Nova conta

Se estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada exibido, forneça um nome, uma descrição opcional e [!DNL Teradata Vantage] credenciais. Quando terminar, selecione **[!UICONTROL Connect]** e, em seguida, permitir que a nova conexão seja estabelecida.

![](../../../../images/tutorials/create/teradata/new.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta do Teradata Vantage. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer dados para a plataforma](../../dataflow/databases.md).
