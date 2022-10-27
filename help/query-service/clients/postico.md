---
keywords: Experience Platform, home, tópicos populares, serviço de query, postico, Postico, conectar ao serviço de query;
solution: Experience Platform
title: Ligar Postico ao Serviço de Consulta
topic-legacy: connect
description: Este documento contém o link para instalar o cliente de backup Postico for Adobe Experience Platform Query Service.
exl-id: a19abfc8-b431-4e57-b44d-c6130041af4a
source-git-commit: 75e97efcb68439f1b837af93b62c96f43e5d7a31
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 0%

---

# Connect [!DNL Postico] para o Serviço de Consulta (Mac)

Este documento aborda as etapas para conexão [!DNL Postico] com o Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Este guia supõe que você já tenha acesso ao [!DNL Postico] e estão familiarizados com como navegar em sua interface. Mais informações sobre [!DNL Postico] podem ser encontradas no [funcionário [!DNL Postico] documentação](https://eggerapps.at/postico/docs).
> 
> Além disso, [!DNL Postico] é **only** disponível em dispositivos macOS.

Para ligar [!DNL Postico] para o Serviço de Consulta, abra [!DNL Postico] e selecione **[!DNL New Favorite]**.

![O [!DNL Postico] Interface do usuário com Novo favorito destacado.](../images/clients/postico/open-postico.png)

Agora você pode inserir valores para se conectar ao Adobe Experience Platform.

Para obter mais informações sobre como encontrar o nome do banco de dados, o host, a porta e as credenciais de logon, leia a [guia de credenciais](../ui/credentials.md). Para localizar suas credenciais, faça logon em [!DNL Platform], em seguida selecione **[!UICONTROL Queries]**, seguida de **[!UICONTROL Credenciais]**.

Depois de inserir suas credenciais, selecione **[!DNL Connect]** para se conectar ao Serviço de query.

![A caixa de diálogo Novo favorito com conexão realçada.](../images/clients/postico/authentication-details.png)

Após se conectar à Platform, você poderá ver uma lista de todas as relações feitas anteriormente com o Serviço de query.

![Uma lista de conexões na [!DNL Postico] IU.](../images/clients/postico/show-queries.png)

## Criar instruções SQL

Para criar uma nova consulta SQL, selecione e abra &quot;Consulta SQL&quot;.

![O [!DNL Postico] Interface do usuário com o atalho de Consulta SQL realçado.](../images/clients/postico/create-query.png)

Uma caixa é exibida e aqui você pode digitar a consulta que deseja executar. Quando terminar, selecione **[!DNL Execute Statement]** para executar o query.

![Destaque o editor SQL com a instrução Execute.](../images/clients/postico/run-statement.png)

Uma tabela é exibida mostrando os resultados da execução de query concluída.

![Uma tabela de resultados da query de exemplo.](../images/clients/postico/query-results.png)

## Próximas etapas

Agora que você se conectou a [!DNL Query Service], você pode usar [!DNL Postico] para gravar queries. Para obter mais informações sobre como gravar e executar consultas, leia o [guia de execução de consultas](../best-practices/writing-queries.md).
