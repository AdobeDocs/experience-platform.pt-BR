---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Conectar com o Looker
topic: connect
translation-type: tm+mt
source-git-commit: 3b710e7a20975880376f7e434ea4d79c01fa0ce5
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---


# Conectar-se com [!DNL Looker]

Para conectar-se [!DNL Looker] com [!DNL Query Service] no Adobe Experience Platform, siga as etapas abaixo:

Depois de fazer logon [!DNL Looker], clique em **[!UICONTROL Admin]**, seguido por **[!UICONTROL Conexões]**.

![](../images/clients/looker/click-admin-connections.png)

Nesta página, clique em **Nova conexão**.

![](../images/clients/looker/click-new-connection.png)

Aqui, você pode preencher os detalhes das Configurações de conexão.

![](../images/clients/looker/new-connection.png)

- **Nome:** O nome da sua conexão.
- **Dialeto:** O dialeto usado para o banco de dados SQL. [!DNL Query Service] usa **[!DNL PostgreSQL]**.
- **Host e porta:** O terminal do host e sua porta para [!DNL Query Service].
- **Banco de dados:** O banco de dados que será usado.
- **Nome de usuário e senha:** As credenciais de logon que serão usadas. O nome de usuário estará na forma de `ORG_ID@AdobeOrg`.

>[!NOTE]
>
>Para obter mais informações sobre como localizar seu host e porta, nome do banco de dados e credenciais de logon, visite a página de [credenciais no Platform](https://platform.adobe.com/query/configuration). Para localizar suas credenciais, faça logon [!DNL Platform], clique em **[!UICONTROL Query]** e, em seguida, clique em **[!UICONTROL Credenciais]**.

Depois de inserir os detalhes da conexão, clique em **[!UICONTROL Testar essas configurações]** para garantir que suas credenciais funcionem corretamente. Se o fizerem, uma mensagem informando que você pode se conectar será exibida abaixo. Se a conexão for realmente bem-sucedida, clique em **[!UICONTROL Adicionar conexão]** para criar a conexão.

![](../images/clients/looker/click-test-connection.png)

## Próximas etapas

Agora que você se conectou com [!DNL Query Service], você pode usar [!DNL Looker] para escrever query. Para obter mais informações sobre como gravar e executar query, leia o guia [de query](../creating-queries/creating-queries.md)em execução.