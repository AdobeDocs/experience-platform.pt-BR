---
keywords: Experience Platform;home;popular topics;query service;Query service;Aqua Data Studio;Aqua data studio;conectar ao serviço do query;
solution: Experience Platform
title: Conectar o Aqua Data Studio ao serviço do Query
topic: connect
description: Este documento percorre as etapas para conectar o Aqua Data Studio com o Adobe Experience Platform Query Service.
translation-type: tm+mt
source-git-commit: 6655714d4b57d9c414cd40529bcee48c7bcd862d
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 1%

---


# Conectar [!DNL Aqua Data Studio] ao Serviço de Query

Este documento cobre as etapas para conectar [!DNL Aqua Data Studio] ao Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Este guia supõe que você já tenha acesso a [!DNL Aqua Data Studio] e esteja familiarizado com como navegar em sua interface. Mais informações sobre [!DNL Aqua Data Studio] podem ser encontradas na [oficial [!DNL Aqua Data Studio] documentação](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation21.1/page/0/Aqua-Data-Studio-21-1).

Depois de instalar [!DNL Aqua Data Studio], primeiro registre o servidor. No menu principal, selecione **[!DNL Server]**, seguido por **[!DNL Register Server]**.

![](../images/clients/aqua-data-studio/register-server.png)

A caixa de diálogo **[!DNL Register Server]** é exibida. Na guia **[!DNL General]**, selecione **[!DNL PostgreSQL]** na lista do lado esquerdo. Na caixa de diálogo exibida, forneça os detalhes a seguir para as configurações do servidor.

- **[!DNL Name]**: O nome da sua conexão.
- **[!DNL Login Name and Password]**: As credenciais de logon que serão usadas. O nome de usuário assume a forma de `ORG_ID@AdobeOrg`.
- **[!DNL Host and Port]**: O terminal do host e sua porta para  [!DNL Query Service]. Você deve usar a porta 80 para se conectar com [!DNL Query Service].
- **[!DNL Database]:** O banco de dados que será usado.

>[!NOTE]
>
>Para obter mais informações sobre como localizar suas credenciais de logon, host, porta e nome do banco de dados, visite a página [credenciais em Platform](https://platform.adobe.com/query/configuration). Para localizar suas credenciais, faça logon em [!DNL Platform] e selecione **[!UICONTROL Query]**, seguido por **[!UICONTROL Credenciais]**.

![](../images/clients/aqua-data-studio/register-server-general-tab.png)

Selecione a guia **[!DNL Driver]**. Em **[!DNL Parameters]**, defina o valor como `?sslmode=require`

![](../images/clients/aqua-data-studio/register-server-driver-tab.png)

Depois de inserir os detalhes da conexão, selecione **[!DNL Test Connection]** para garantir que suas credenciais funcionem corretamente. Se a conexão for bem-sucedida, selecione **[!DNL Save]** para registrar o servidor. A conexão é exibida no painel após o registro bem-sucedido, confirmando que agora você pode se conectar ao servidor e visualização seus objetos de schema.

## Próximas etapas

Agora que você se conectou a [!DNL Query Service], é possível usar **[!DNL Query Analyzer]** em [!DNL Aqua Data Studio] para executar e editar instruções SQL. Para obter mais informações sobre como gravar e executar query, leia o [guia de query em execução](../best-practices/writing-queries.md).