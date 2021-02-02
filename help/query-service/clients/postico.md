---
keywords: Experience Platform;home;popular topics;Query service;query service;postico;Postico;connect to query service;
solution: Experience Platform
title: Conecte-se com o Postico
topic: connect
description: Este documento contém o link para instalar o cliente de backup Postico for Adobe Experience Platform Query Service.
translation-type: tm+mt
source-git-commit: eac93f3465fa6ce4af7a6aa783cf5f8fb4ac9b9b
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---


# [!DNL Postico]

Este documento cobre as etapas para conectar [!DNL Postico] ao Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Este guia supõe que você já tenha acesso a [!DNL Postico] e esteja familiarizado com como navegar em sua interface. Mais informações sobre [!DNL Postico] podem ser encontradas na [oficial [!DNL Postico] documentação](https://eggerapps.at/postico/docs).
> 
> Além disso, [!DNL Postico] está **apenas** disponível em dispositivos macOS.

## Conectar [!DNL Postico] ao Serviço de Query

Para conectar [!DNL Postico] ao Query Service, abra [!DNL Postico] e selecione **[!DNL New Favorite]**.

![](../images/clients/postico/open-postico.png)

Agora você pode inserir valores para se conectar ao Adobe Experience Platform.

Para obter mais informações sobre como localizar seu nome de banco de dados, host, porta e credenciais de logon, visite a página [credenciais em Platform](https://platform.adobe.com/query/configuration). Para localizar suas credenciais, faça logon em [!DNL Platform] e selecione **[!UICONTROL Query]**, seguido por **[!UICONTROL Credenciais]**.

Depois de inserir suas credenciais, selecione **[!DNL Connect]** para se conectar ao Serviço de Query.

![](../images/clients/postico/authentication-details.png)

Depois de se conectar à plataforma, você poderá ver uma lista de todas as relações feitas anteriormente com o Query Service.

![](../images/clients/postico/show-queries.png)

## Criar instruções SQL

Para criar um novo query SQL, selecione e abra &quot;Query SQL&quot;.

![](../images/clients/postico/create-query.png)

Uma caixa é exibida e, a partir daí, você pode digitar o query que deseja executar. Quando terminar, selecione **[!DNL Execute Statement]** para executar o query.

![](../images/clients/postico/run-statement.png)

Uma tabela é exibida, mostrando os resultados da execução de seu query concluído.

![](../images/clients/postico/query-results.png)

## Próximas etapas

Agora que você se conectou a [!DNL Query Service], é possível usar [!DNL Postico] para gravar query. Para obter mais informações sobre como gravar e executar query, leia o [guia de query em execução](../best-practices/writing-queries.md).