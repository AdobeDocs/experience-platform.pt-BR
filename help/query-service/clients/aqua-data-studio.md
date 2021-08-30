---
keywords: Experience Platform, home, tópicos populares, serviço de consulta, serviço de consulta, Aqua Data Studio, Aqua data studio, conectar ao serviço de consulta;
solution: Experience Platform
title: Conectar o Aqua Data Studio ao Serviço de Consulta
topic-legacy: connect
description: Este documento aborda as etapas para conectar o Aqua Data Studio com o Adobe Experience Platform Query Service.
exl-id: 4770e221-48a7-45d8-80a4-60b5cbc0ec33
source-git-commit: 910a38ccb556ec427584d9b522e29f6877d1c987
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 1%

---

# Conectar [!DNL Aqua Data Studio] ao Serviço de Consulta

Este documento aborda as etapas para conectar [!DNL Aqua Data Studio] com Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Este guia pressupõe que você já tenha acesso a [!DNL Aqua Data Studio] e esteja familiarizado com como navegar em sua interface. Mais informações sobre [!DNL Aqua Data Studio] podem ser encontradas na documentação [oficial [!DNL Aqua Data Studio] documentação](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation21.1/page/0/Aqua-Data-Studio-21-1).

Depois de instalar [!DNL Aqua Data Studio], primeiro registre o servidor. No menu principal, selecione **[!DNL Server]**, seguido por **[!DNL Register Server]**.

![](../images/clients/aqua-data-studio/register-server.png)

A caixa de diálogo **[!DNL Register Server]** é exibida. Na guia **[!DNL General]**, selecione **[!DNL PostgreSQL]** na lista no lado esquerdo. Na caixa de diálogo exibida, forneça os seguintes detalhes para as configurações do servidor.

- **[!DNL Name]**: O nome da sua conexão.
- **[!DNL Login Name and Password]**: As credenciais de logon que serão usadas. O nome de usuário assume a forma de `ORG_ID@AdobeOrg`.
- **[!DNL Host and Port]**: O terminal do host e sua porta para  [!DNL Query Service]. Você deve usar a porta 80 para se conectar com [!DNL Query Service].
- **[!DNL Database]:** o banco de dados que será usado.

>[!NOTE]
>
>Para obter mais informações sobre como encontrar suas credenciais de logon, host, porta e nome do banco de dados, leia o [guia de credenciais](../ui/credentials.md). Para localizar suas credenciais, faça logon em [!DNL Platform], selecione **[!UICONTROL Queries]**, seguido por **[!UICONTROL Credentials]**.

![](../images/clients/aqua-data-studio/register-server-general-tab.png)

Selecione a guia **[!DNL Driver]**. Em **[!DNL Parameters]**, defina o valor como `?sslmode=require`

![](../images/clients/aqua-data-studio/register-server-driver-tab.png)

Depois de inserir os detalhes da conexão, selecione **[!DNL Test Connection]** para garantir que suas credenciais funcionem corretamente. Se a conexão for bem-sucedida, selecione **[!DNL Save]** para registrar o servidor. A conexão aparece no painel após o registro bem-sucedido, confirmando que agora você pode se conectar ao servidor e exibir seus objetos de esquema.

## Próximas etapas

Agora que você se conectou a [!DNL Query Service], é possível usar **[!DNL Query Analyzer]** dentro de [!DNL Aqua Data Studio] para executar e editar instruções SQL. Para obter mais informações sobre como gravar e executar consultas, leia o [guia de consultas em execução](../best-practices/writing-queries.md).
