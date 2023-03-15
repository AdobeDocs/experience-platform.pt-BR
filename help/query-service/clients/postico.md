---
keywords: Experience Platform;página inicial;tópicos populares;Serviço de consulta;serviço de consulta;postico;Postico;conectar ao serviço de consulta;
solution: Experience Platform
title: Conectar o Postico ao Serviço de consulta
description: Este documento contém o link para instalar o cliente de backup Postico para o Serviço de Consulta do Adobe Experience Platform.
exl-id: a19abfc8-b431-4e57-b44d-c6130041af4a
source-git-commit: 9fe7e618d251867c90c88f8bee6ef5863ae78f60
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 0%

---

# Conectar [!DNL Postico] para o Serviço de consulta (Mac)

Este documento aborda as etapas para a conexão [!DNL Postico] com o Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Este guia supõe que você já tenha acesso ao [!DNL Postico] e estão familiarizados com como navegar em sua interface. Mais informações sobre [!DNL Postico] pode ser encontrado no [oficial [!DNL Postico] documentação](https://eggerapps.at/postico/docs).
> 
> Além disso, [!DNL Postico] é **somente** disponível em dispositivos macOS.

Para conectar [!DNL Postico] para o Serviço de consulta, abra [!DNL Postico] e selecione **[!DNL New Favorite]**. A caixa de diálogo para configurações de conexão é exibida. Aqui, você pode inserir valores de parâmetros para se conectar com o Adobe Experience Platform. Insira as configurações de conexão listadas abaixo. Instruções sobre como [conectar-se a um servidor PostgreSQL com Postico](https://eggerapps.at/postico/docs/v1.5.21/favorite-window.html) também estão disponíveis no site oficial do Postico.

| Parâmetro de conexão | Descrição |
|---|---|
| **[!DNL Host]:** | O nome do host do servidor PostgreSQL. |
| **[!DNL Port]:** | A porta para [!DNL Query Service]. Você deve usar a porta **80** ou **5432** para se conectar com [!DNL Query Service]. |
| **[!DNL User]** | Crie um nome para a conexão específica. Deixe o campo em branco para usar seu nome de logon no Mac. |
| **[!DNL Password]** | Esta sequência alfanumérica é o seu Experience Platform **[!UICONTROL Senha]** credencial. Se você quiser usar credenciais sem expiração, esse valor será os argumentos concatenados do `technicalAccountID` e a variável `credential` baixado no arquivo JSON de configuração. O valor da senha tem o formato: {technicalAccountId}:{credential}. O arquivo JSON de configuração para credenciais sem expiração é um download único durante a inicialização do qual o Adobe não mantém uma cópia. |
| **[!DNL Database]** | Use seu Experience Platform **[!UICONTROL Banco de dados]** valor da credencial: `prod:all`. |

Para obter mais informações sobre como localizar o nome do banco de dados, o host, a porta e as credenciais de logon, leia a [guia de credenciais](../ui/credentials.md). Para encontrar suas credenciais, faça logon no [!DNL Platform]e selecione **[!UICONTROL Consultas]**, seguido por **[!UICONTROL Credenciais]**.

Depois de inserir suas credenciais, selecione **[!DNL Connect]** para conectar-se ao Serviço de consulta.

Depois de se conectar à Platform, você poderá ver uma lista de todas as relações feitas anteriormente com o Serviço de consulta.

## Criar instruções SQL

Para criar uma nova consulta SQL, selecione **[!DNL SQL Query]** na barra lateral. Como alternativa, use o atalho de teclado ( T) para navegar até a exibição de consulta e inserir a consulta que deseja executar. Quando terminar, selecione **[!DNL Execute Statement]** para executar a consulta. Uma tabela é exibida com os resultados da execução concluída da consulta.

Consulte a documentação oficial do Postico para obter mais informações sobre [uso da visualização de consulta](https://eggerapps.at/postico/docs/v1.3.1/sql-query-view.html).

## Próximas etapas

Agora que você se conectou com [!DNL Query Service], você pode usar [!DNL Postico] para gravar consultas. Para obter mais informações sobre como gravar e executar consultas, leia o [guia de execução de consultas](../best-practices/writing-queries.md).
