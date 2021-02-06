---
keywords: Experience Platform;home;popular topics;tableau;Tableau;query service;Query service;connect to query service;
solution: Experience Platform
title: Conectar Tableau ao Serviço de Query
topic: connect
description: Este documento percorre as etapas para conectar o Tableau ao Adobe Experience Platform Query Service.
translation-type: tm+mt
source-git-commit: 6655714d4b57d9c414cd40529bcee48c7bcd862d
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 0%

---


# Conectar [!DNL Tableau] ao Serviço de Query

Este documento cobre as etapas para conectar Tableau ao Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Este guia supõe que você já tenha acesso a [!DNL Tableau] e esteja familiarizado com como navegar em sua interface. Mais informações sobre [!DNL Tableau] podem ser encontradas na [oficial [!DNL Tableau] documentação](https://help.tableau.com/current/pro/desktop/en-us/default.htm).

Para conectar [!DNL Tableau] a [!DNL Query Service], abra [!DNL Tableau] e, na seção **[!DNL To a Server]**, selecione **[!DNL More]** seguido por **[!DNL PostgreSQL]**

![](../images/clients/tableau/open-connection.png)

Agora você pode inserir valores para se conectar ao Adobe Experience Platform. Para obter mais informações sobre como localizar seu nome de banco de dados, host, porta e credenciais de logon, visite a página [credenciais em Platform](https://platform.adobe.com/query/configuration). Para localizar suas credenciais, faça logon em [!DNL Platform] e selecione **[!UICONTROL Query]**, seguido por **[!UICONTROL Credenciais]**.

Verifique se você marcou a caixa **[!UICONTROL SSL Obrigatório]** antes de tentar se conectar.

Depois de preencher todas as suas credenciais, selecione **[!DNL Sign In]** para continuar.

![](../images/clients/tableau/sign-in.png)

Agora você se conectou ao Adobe Experience Platform, com uma lista de suas tabelas exibida ao lado.

![](../images/clients/tableau/connected.png)

## Próximas etapas

Agora que você se conectou a [!DNL Query Service], é possível usar [!DNL Tableau] para gravar query. Para obter mais informações sobre como gravar e executar query, leia o guia em [query em execução](../best-practices/writing-queries.md).