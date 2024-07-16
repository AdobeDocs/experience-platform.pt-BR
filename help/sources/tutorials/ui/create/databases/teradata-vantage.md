---
keywords: Experience Platform;página inicial;tópicos populares;Vantagem de Teradata
title: Criar uma Conexão do Teradata Vantage Source na interface
description: Saiba como criar uma conexão de origem do Teradata Vantage usando a interface do usuário do Adobe Experience Platform.
exl-id: 3fdb09fa-128a-477b-9144-d4ef3ed18ea6
source-git-commit: 625a7959f48a0b16c3228d4555e046b5f67c51b7
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 2%

---

# Criar uma conexão de origem [!DNL Teradata Vantage] na interface

Este tutorial fornece etapas para a criação de um conector de origem [!DNL Teradata Vantage] usando a interface do usuário do Adobe Experience Platform.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes da Platform:

* [Fontes](../../../../home.md): o Experience Platform permite a assimilação de dados de várias fontes, além de fornecer a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços Experience Platform.
* [Sandboxes](../../../../../sandboxes/home.md): o Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

### Coletar credenciais necessárias

Para acessar sua conta do [!DNL Teradata Vantage] na Platform, você deve fornecer o seguinte valor de autenticação:

| Credencial | Descrição |
| ---------- | ----------- |
| String de conexão | Uma cadeia de conexão é uma cadeia que fornece informações sobre uma fonte de dados e como você pode se conectar a ela. O padrão da cadeia de conexão para [!DNL Teradata Vantage] é `DBCName={SERVER};Uid={USERNAME};Pwd={PASSWORD}`. |

Para obter mais informações sobre a introdução, consulte este [[!DNL Teradata Vantage] documento](https://docs.teradata.com/r/Teradata-VantageTM-Advanced-SQL-Engine-Security-Administration/July-2021/Setting-Up-the-Administrative-Infrastructure/Controlling-Access-to-the-Operating-System/Working-with-OS-Level-Security-Options).

## Conectar sua conta do [!DNL Teradata Vantage]

Na interface da Platform, selecione **[!UICONTROL Fontes]** na navegação à esquerda para acessar o espaço de trabalho [!UICONTROL Fontes]. Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria [!UICONTROL Bancos de Dados], selecione **[!UICONTROL Vantagem de Teradata]** e **[!UICONTROL Configurar]**.

>[!TIP]
>
>As origens no catálogo de origens exibem a opção **[!UICONTROL Configurar]** quando uma determinada origem ainda não tem uma conta autenticada. Quando uma conta autenticada existir, esta opção será alterada para **[!UICONTROL Adicionar dados]**.

![O catálogo de origens com a origem do Teradata Vantage selecionada.](../../../../images/tutorials/create/teradata/catalog.png)

A página **[!UICONTROL Conectar-se ao Teradata Vantage]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Conta existente

Para conectar uma conta existente, selecione a conta [!DNL Teradata Vantage] com a qual deseja se conectar e clique em **[!UICONTROL Avançar]** para continuar.

![A página de contas existente no espaço de trabalho de origens.](../../../../images/tutorials/create/teradata/existing.png)

### Nova conta

Se você estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada que aparece, forneça um nome, uma descrição opcional e suas credenciais do [!DNL Teradata Vantage]. Quando terminar, selecione **[!UICONTROL Conectar]** e aguarde algum tempo para que a nova conexão seja estabelecida.

![A nova interface de criação de conta no espaço de trabalho de origens.](../../../../images/tutorials/create/teradata/new.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta do Teradata Vantage. Agora você pode seguir para o próximo tutorial e [configurar um fluxo de dados para trazer dados para a Platform](../../dataflow/databases.md).
