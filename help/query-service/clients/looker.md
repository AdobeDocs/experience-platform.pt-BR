---
keywords: Experience Platform, home, tópicos populares, serviço de consulta, serviço de consulta, Looker, looker, conectar ao serviço de consulta;
solution: Experience Platform
title: Conectar Looker ao Serviço de Consulta
description: Este documento aborda as etapas para conectar o Looker ao Adobe Experience Platform Query Service.
exl-id: 806e9077-533a-4546-b5ca-8124751957f5
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 0%

---

# Connect [!DNL Looker] para Serviço de Consulta

Este documento aborda as etapas para conexão [!DNL Looker] com o Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Este guia supõe que você já tenha acesso ao [!DNL Looker] e estão familiarizados com como navegar em sua interface. Mais informações sobre [!DNL Looker] podem ser encontradas no [funcionário [!DNL Looker] documentação](https://docs.looker.com/).

Depois de fazer logon em [!DNL Looker], selecione **[!DNL Admin]**, seguida de **[!DNL Connections]**.

![O [!DNL Looker] painel com Conexões , realçado no menu suspenso Admin .](../images/clients/looker/click-admin-connections.png)

Nesta página, selecione **[!DNL New Connection]**.

![A área de trabalho Connections with New Connection (Conexões com nova conexão) foi realçada.](../images/clients/looker/click-new-connection.png)

Aqui, você pode preencher os detalhes das configurações de conexão.

![A página de configurações de Conexões para uma Nova Conexão.](../images/clients/looker/new-connection.png)

- **[!DNL Name]:** O nome da sua conexão.
- **[!DNL Dialect]:** O dialeto usado para o banco de dados SQL. [!DNL Query Service] uses **[!DNL PostgreSQL]**.
- **[!DNL Host and Port]:** O terminal do host e sua porta para [!DNL Query Service].
- **[!DNL Database]:** O banco de dados que será usado.
- **[!DNL Username and Password]:** As credenciais de logon que serão usadas. O nome de usuário estará no formato de `ORG_ID@AdobeOrg`.
- **SSL**: Ative o SSL para garantir uma conexão segura na rede.

>[!IMPORTANT]
>
>Consulte a [[!DNL Query Service] Documentação SSL](./ssl-modes.md) para saber mais sobre o suporte SSL para conexões de terceiros com o Adobe Experience Platform Query Service e como se conectar usando `verify-full` Modo SSL.

Para obter mais informações sobre como localizar o host e a porta, o nome do banco de dados e as credenciais de logon, leia a [guia de credenciais](../ui/credentials.md). Para localizar suas credenciais, faça logon em [!DNL Platform], em seguida selecione **[!UICONTROL Queries]**, seguida de **[!UICONTROL Credenciais]**.

Depois de inserir os detalhes da conexão, selecione **[!DNL Test These Settings]** para garantir que suas credenciais funcionem corretamente. Se o fizerem, uma mensagem indicando que você pode se conectar será exibida abaixo. Se a conexão for bem-sucedida, selecione **[!DNL Add Connection]** para criar a conexão.

![A página de configurações de Conexões para uma nova conexão com Testar essas configurações foi realçada.](../images/clients/looker/click-test-connection.png)

## Próximas etapas

Agora que você se conectou a [!DNL Query Service], você pode usar [!DNL Looker] para gravar queries. Para obter mais informações sobre como gravar e executar consultas, leia o [guia de execução de consultas](../best-practices/writing-queries.md).
