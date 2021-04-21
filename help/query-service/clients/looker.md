---
keywords: Experience Platform, home, tópicos populares, serviço de consulta, serviço de consulta, Looker, looker, conectar ao serviço de consulta;
solution: Experience Platform
title: Conectar Looker ao Serviço de Consulta
topic-legacy: connect
description: Este documento aborda as etapas para conectar o Looker ao Adobe Experience Platform Query Service.
exl-id: 806e9077-533a-4546-b5ca-8124751957f5
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---

# Conectar [!DNL Looker] ao Serviço de Consulta

Este documento aborda as etapas para conectar [!DNL Looker] com Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Este guia pressupõe que você já tenha acesso a [!DNL Looker] e esteja familiarizado com como navegar em sua interface. Mais informações sobre [!DNL Looker] podem ser encontradas na documentação [oficial [!DNL Looker] documentação](https://docs.looker.com/).

Depois de fazer logon em [!DNL Looker], selecione **[!DNL Admin]**, seguido por **[!DNL Connections]**.

![](../images/clients/looker/click-admin-connections.png)

Nesta página, selecione **[!DNL New Connection]**.

![](../images/clients/looker/click-new-connection.png)

Aqui, você pode preencher os detalhes das configurações de conexão.

![](../images/clients/looker/new-connection.png)

- **[!DNL Name]:** o nome da sua conexão.
- **[!DNL Dialect]:** o dialeto usado para o banco de dados SQL. [!DNL Query Service] usa  **[!DNL PostgreSQL]**.
- **[!DNL Host and Port]:** o terminal do host e sua porta para  [!DNL Query Service].
- **[!DNL Database]:** o banco de dados que será usado.
- **[!DNL Username and Password]:** As credenciais de logon que serão usadas. O nome de usuário estará no formato `ORG_ID@AdobeOrg`.

>[!NOTE]
>
>Para obter mais informações sobre como encontrar o host e a porta, o nome do banco de dados e as credenciais de logon, visite a página [credenciais no Platform](https://platform.adobe.com/query/configuration). Para localizar suas credenciais, faça logon em [!DNL Platform], selecione **[!UICONTROL Queries]**, seguido por **[!UICONTROL Credentials]**.

Depois de inserir os detalhes da conexão, selecione **[!DNL Test These Settings]** para garantir que suas credenciais funcionem corretamente. Se o fizerem, uma mensagem indicando que você pode se conectar será exibida abaixo. Se a conexão for realmente bem-sucedida, selecione **[!DNL Add Connection]** para criar a conexão.

![](../images/clients/looker/click-test-connection.png)

## Próximas etapas

Agora que você se conectou a [!DNL Query Service], é possível usar [!DNL Looker] para gravar consultas. Para obter mais informações sobre como gravar e executar consultas, leia o [guia de consultas em execução](../best-practices/writing-queries.md).
