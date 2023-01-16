---
keywords: Experience Platform, home, tópicos populares, serviço de query, postico, Postico, conectar ao serviço de query;
solution: Experience Platform
title: Ligar Postico ao Serviço de Consulta
description: Este documento contém o link para instalar o cliente de backup Postico for Adobe Experience Platform Query Service.
exl-id: a19abfc8-b431-4e57-b44d-c6130041af4a
source-git-commit: 9fe7e618d251867c90c88f8bee6ef5863ae78f60
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 0%

---

# Connect [!DNL Postico] para o Serviço de Consulta (Mac)

Este documento aborda as etapas para conexão [!DNL Postico] com o Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Este guia supõe que você já tenha acesso ao [!DNL Postico] e estão familiarizados com como navegar em sua interface. Mais informações sobre [!DNL Postico] podem ser encontradas no [funcionário [!DNL Postico] documentação](https://eggerapps.at/postico/docs).
> 
> Além disso, [!DNL Postico] é **only** disponível em dispositivos macOS.

Para ligar [!DNL Postico] para o Serviço de Consulta, abra [!DNL Postico] e selecione **[!DNL New Favorite]**. A caixa de diálogo para configurações de conexão é exibida. Aqui, você pode inserir valores de parâmetro para se conectar com o Adobe Experience Platform. Insira as configurações de conexão listadas abaixo. Instruções sobre como [conectar-se a um servidor PostgreSQL com Postico](https://eggerapps.at/postico/docs/v1.5.21/favorite-window.html) também estão disponíveis no site oficial Postico.

| Parâmetro de conexão | Descrição |
|---|---|
| **[!DNL Host]:** | O nome do host do servidor PostgreSQL. |
| **[!DNL Port]:** | A porta para [!DNL Query Service]. Você deve usar a porta **80º** ou **5432** para conectar-se com [!DNL Query Service]. |
| **[!DNL User]** | Crie um nome para a conexão específica. Deixe o campo em branco para usar seu nome de logon do Mac. |
| **[!DNL Password]** | Esta sequência alfanumérica é o seu Experience Platform **[!UICONTROL Senha]** credencial. Se você quiser usar credenciais que não estejam expirando, esse valor será o argumento concatenado da variável `technicalAccountID` e `credential` baixado no arquivo JSON de configuração. O valor da senha assume o formulário: {technicalAccountId}:{credential}. O arquivo JSON de configuração para credenciais que não expiram é um download único durante a inicialização que o Adobe não mantém uma cópia. |
| **[!DNL Database]** | Use seu Experience Platform **[!UICONTROL Banco de dados]** valor da credencial: `prod:all`. |

Para obter mais informações sobre como encontrar o nome do banco de dados, o host, a porta e as credenciais de logon, leia a [guia de credenciais](../ui/credentials.md). Para localizar suas credenciais, faça logon em [!DNL Platform], em seguida selecione **[!UICONTROL Queries]**, seguida de **[!UICONTROL Credenciais]**.

Depois de inserir suas credenciais, selecione **[!DNL Connect]** para se conectar ao Serviço de query.

Após se conectar à Platform, você poderá ver uma lista de todas as relações feitas anteriormente com o Serviço de query.

## Criar instruções SQL

Para criar uma nova consulta SQL, selecione **[!DNL SQL Query]** na barra lateral. Como alternativa, use o atalho de teclado ( ⇧ ⌘ T) para navegar até a exibição de query e inserir a consulta que deseja executar. Quando terminar, selecione **[!DNL Execute Statement]** para executar o query. Uma tabela é exibida com os resultados da execução de query concluída.

Consulte a documentação oficial do Postico para obter mais informações sobre [uso da exibição de query](https://eggerapps.at/postico/docs/v1.3.1/sql-query-view.html).

## Próximas etapas

Agora que você se conectou a [!DNL Query Service], você pode usar [!DNL Postico] para gravar queries. Para obter mais informações sobre como gravar e executar consultas, leia o [guia de execução de consultas](../best-practices/writing-queries.md).
