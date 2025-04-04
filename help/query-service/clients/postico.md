---
keywords: Experience Platform;página inicial;tópicos populares;Serviço de consulta;serviço de consulta;postico;Postico;conectar-se ao serviço de consulta;
solution: Experience Platform
title: Conectar o Postico ao Serviço de consulta
description: Este documento contém o link para instalar o cliente de backup Postico para o Serviço de Consulta do Adobe Experience Platform.
exl-id: a19abfc8-b431-4e57-b44d-c6130041af4a
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---

# Conectar [!DNL Postico] ao Serviço de Consulta (Mac)

Este documento aborda as etapas para conectar o [!DNL Postico] ao Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Este guia supõe que você já tenha acesso ao [!DNL Postico] e esteja familiarizado com como navegar em sua interface. Mais informações sobre [!DNL Postico] podem ser encontradas na [documentação [!DNL Postico] oficial](https://eggerapps.at/postico/docs).
> 
> Além disso, [!DNL Postico] está **somente** disponível em dispositivos macOS.

Para conectar [!DNL Postico] ao Serviço de Consulta, abra [!DNL Postico] e selecione **[!DNL New Favorite]**. A caixa de diálogo para configurações de conexão é exibida. Aqui, você pode inserir valores de parâmetros para se conectar com o Adobe Experience Platform. Insira as configurações de conexão listadas abaixo. Instruções sobre como [conectar-se a um servidor PostgreSQL com Postico](https://eggerapps.at/postico/docs/v1.5.21/favorite-window.html) também estão disponíveis no site oficial do Postico.

| Parâmetro de conexão | Descrição |
|---|---|
| **[!DNL Host]:** | O nome do host do servidor PostgreSQL. |
| **[!DNL Port]:** | A porta para [!DNL Query Service]. Você deve usar a porta **80** ou **5432** para se conectar com [!DNL Query Service]. |
| **[!DNL User]** | Crie um nome para a conexão específica. Deixe o campo em branco para usar seu nome de logon no Mac. |
| **[!DNL Password]** | Esta sequência alfanumérica é a credencial **[!UICONTROL Senha]** da Experience Platform. Se você quiser usar credenciais sem expiração, esse valor serão os argumentos concatenados de `technicalAccountID` e `credential` baixados no arquivo JSON de configuração. O valor da senha tem o formato: {technicalAccountId}:{credential}. O arquivo JSON de configuração para credenciais sem expiração é um download único durante a inicialização do qual a Adobe não mantém uma cópia. |
| **[!DNL Database]** | Use seu valor de credencial do **[!UICONTROL Banco de Dados]** do Experience Platform: `prod:all`. |

Para obter mais informações sobre como localizar o nome do banco de dados, o host, a porta e as credenciais de logon, leia o [guia de credenciais](../ui/credentials.md). Para encontrar suas credenciais, faça logon em [!DNL Experience Platform] e selecione **[!UICONTROL Consultas]**, seguido de **[!UICONTROL Credenciais]**.

Depois de inserir suas credenciais, selecione **[!DNL Connect]** para se conectar ao Serviço de Consulta.

Depois de se conectar ao Experience Platform, você poderá ver uma lista de todas as relações feitas anteriormente com o Serviço de consulta.

## Criar instruções SQL

Para criar uma nova consulta SQL, selecione **[!DNL SQL Query]** na barra lateral. Como alternativa, use o atalho de teclado ( T) para navegar até a exibição de consulta e inserir a consulta que deseja executar. Quando terminar, selecione **[!DNL Execute Statement]** para executar a consulta. Uma tabela é exibida com os resultados da execução concluída da consulta.

Consulte a documentação oficial do Postico para obter mais informações sobre [como usar a exibição de consulta](https://eggerapps.at/postico/docs/v1.3.1/sql-query-view.html).

## Próximas etapas

Agora que você se conectou com [!DNL Query Service], pode usar [!DNL Postico] para gravar consultas. Para obter mais informações sobre como gravar e executar consultas, leia o [guia de execução de consultas](../best-practices/writing-queries.md).
