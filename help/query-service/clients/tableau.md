---
keywords: Experience Platform, home, tópicos populares, tableau, Tableau, serviço de consulta, serviço de consulta, conectar ao serviço de consulta;
solution: Experience Platform
title: Conectar o Tableau ao Serviço de Consulta
topic-legacy: connect
description: Este documento aborda as etapas para conectar o Tableau ao Adobe Experience Platform Query Service.
exl-id: f380aacd-5091-41bc-97ca-593e0b1670fd
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

---

# Conectar [!DNL Tableau] ao Serviço de Consulta

Este documento aborda as etapas para conectar o Tableau com o Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Este guia pressupõe que você já tenha acesso a [!DNL Tableau] e esteja familiarizado com como navegar em sua interface. Mais informações sobre [!DNL Tableau] podem ser encontradas na documentação [oficial [!DNL Tableau] documentação](https://help.tableau.com/current/pro/desktop/en-us/default.htm).

Para conectar [!DNL Tableau] a [!DNL Query Service], abra [!DNL Tableau] e, na seção **[!DNL To a Server]**, selecione **[!DNL More]** seguido por **[!DNL PostgreSQL]**

![](../images/clients/tableau/open-connection.png)

Agora você pode inserir valores para se conectar ao Adobe Experience Platform. Para obter mais informações sobre como encontrar o nome do banco de dados, o host, a porta e as credenciais de logon, visite a página [credenciais no Platform](https://platform.adobe.com/query/configuration). Para localizar suas credenciais, faça logon em [!DNL Platform], selecione **[!UICONTROL Queries]**, seguido por **[!UICONTROL Credentials]**.

Verifique se você marcou a caixa **[!UICONTROL SSL Required]** antes de tentar se conectar.

Depois de preencher todas as suas credenciais, selecione **[!DNL Sign In]** para continuar.

![](../images/clients/tableau/sign-in.png)

Agora você se conectou ao Adobe Experience Platform, com uma lista das tabelas exibidas no lado.

![](../images/clients/tableau/connected.png)

## Próximas etapas

Agora que você se conectou a [!DNL Query Service], é possível usar [!DNL Tableau] para gravar consultas. Para obter mais informações sobre como gravar e executar consultas, leia o guia em [executar consultas](../best-practices/writing-queries.md).
