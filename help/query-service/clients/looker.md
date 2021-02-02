---
keywords: Experience Platform;home;popular topics;Query service;query service;Looker;looker;connect to query service;
solution: Experience Platform
title: Conectar com o Looker
topic: connect
description: Este documento percorre as etapas para conectar o Looker ao Adobe Experience Platform Query Service.
translation-type: tm+mt
source-git-commit: bc1bbdddd75b11ac180b5e6faa391fd74e5f7e02
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 0%

---


# [!DNL Looker]

Este documento cobre as etapas para conectar [!DNL Looker] ao Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Este guia supõe que você já tenha acesso a [!DNL Looker] e esteja familiarizado com como navegar em sua interface. Mais informações sobre [!DNL Looker] podem ser encontradas na [oficial [!DNL Looker] documentação](https://docs.looker.com/).

## Conectar [!DNL Looker] com a plataforma

Depois de fazer logon em [!DNL Looker], selecione **[!DNL Admin]**, seguido por **[!DNL Connections]**.

![](../images/clients/looker/click-admin-connections.png)

Nesta página, selecione **[!DNL New Connection]**.

![](../images/clients/looker/click-new-connection.png)

Aqui, você pode preencher os detalhes das configurações de conexão.

![](../images/clients/looker/new-connection.png)

- **[!DNL Name]:** O nome da sua conexão.
- **[!DNL Dialect]:** O dialeto usado para o banco de dados SQL. [!DNL Query Service] usa  **[!DNL PostgreSQL]**.
- **[!DNL Host and Port]:** O terminal do host e sua porta para  [!DNL Query Service].
- **[!DNL Database]:** O banco de dados que será usado.
- **[!DNL Username and Password]:** As credenciais de logon que serão usadas. O nome de usuário estará na forma de `ORG_ID@AdobeOrg`.

>[!NOTE]
>
>Para obter mais informações sobre como localizar seu host e porta, nome do banco de dados e credenciais de logon, visite a página [credenciais em Platform](https://platform.adobe.com/query/configuration). Para localizar suas credenciais, faça logon em [!DNL Platform] e selecione **[!UICONTROL Query]**, seguido por **[!UICONTROL Credenciais]**.

Depois de inserir os detalhes da conexão, selecione **[!DNL Test These Settings]** para garantir que suas credenciais funcionem corretamente. Se o fizerem, uma mensagem indicando que você pode se conectar será exibida abaixo. Se sua conexão for realmente bem-sucedida, selecione **[!DNL Add Connection]** para criar sua conexão.

![](../images/clients/looker/click-test-connection.png)

## Próximas etapas

Agora que você se conectou a [!DNL Query Service], é possível usar [!DNL Looker] para gravar query. Para obter mais informações sobre como gravar e executar query, leia o [guia de query em execução](../best-practices/writing-queries.md).