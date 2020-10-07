---
keywords: Experience Platform;home;popular topics;query service;Query service;Aqua Data Studio;Aqua data studio;connect to query service;
solution: Experience Platform
title: Conectar-se ao Aqua Data Studio
topic: connect
description: Este documento percorre as etapas para conectar o Aqua Data Studio com o Adobe Experience Platform Query Service.
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 0%

---


# Conectar-se com [!DNL Aqua Data Studio]

Este documento percorre as etapas para conexão [!DNL Aqua Data Studio] com o Adobe Experience Platform [!DNL Query Service].

Depois de instalar [!DNL Aqua Data Studio], você deve primeiro registrar o servidor. No menu principal, clique em **[!UICONTROL Servidor]** e, em seguida, clique em **[!UICONTROL Registrar servidor]**.

![](../images/clients/aqua-data-studio/register-server.png)

A caixa de diálogo **[!UICONTROL Registrar servidor]** é exibida. Na guia **[!UICONTROL Geral]** , selecione **[!UICONTROL PostgreSQL]** na lista no lado esquerdo. Na caixa de diálogo exibida, forneça os detalhes a seguir para as configurações do servidor.

- **[!UICONTROL Nome]**: O nome da sua conexão.
- **[!UICONTROL Nome de login e senha]**: As credenciais de logon que serão usadas. O nome de usuário assume a forma de `ORG_ID@AdobeOrg`.
- **[!UICONTROL Host e porta]**: O terminal do host e sua porta para [!DNL Query Service]. Você deve usar a porta 80 para se conectar com [!DNL Query Service].
- **[!UICONTROL Banco de dados]:** O banco de dados que será usado.

>[!NOTE]
>
>Para obter mais informações sobre como localizar suas credenciais de logon, host, porta e nome do banco de dados, visite a página de [credenciais na Plataforma](https://platform.adobe.com/query/configuration). Para localizar suas credenciais, faça logon [!DNL Platform], clique em **[!UICONTROL Query]** e, em seguida, clique em **[!UICONTROL Credenciais]**.

![](../images/clients/aqua-data-studio/register-server-general-tab.png)

Select the **[!UICONTROL Driver]** tab. Em **[!UICONTROL Parâmetros]**, defina o valor como `?sslmode=require`

![](../images/clients/aqua-data-studio/register-server-driver-tab.png)

Depois de inserir os detalhes da conexão, clique em **[!UICONTROL Testar conexão]** para garantir que suas credenciais funcionem corretamente. Se a conexão for bem-sucedida, clique em **[!UICONTROL Salvar]** para registrar o servidor. A conexão é exibida no **Painel** após o registro bem-sucedido, confirmando que agora você pode se conectar ao servidor e visualização seus objetos de schema.

## Próximas etapas

Agora que você se conectou a [!DNL Query Service], é possível usar o Analisador **[!UICONTROL de]** Query dentro [!DNL Aqua Data Studio] para executar e editar instruções SQL. Para obter mais informações sobre como gravar e executar query, leia o guia [de query](../creating-queries/creating-queries.md)em execução.