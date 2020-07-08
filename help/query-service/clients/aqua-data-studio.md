---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Conectar-se ao Aqua Data Studio
topic: connect
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 0%

---


# Conectar-se ao Aqua Data Studio

Este documento percorre as etapas para conectar o Aqua Data Studio ao serviço de Query.

Depois de instalar o Aqua Data Studio, você deve primeiro registrar o servidor. No menu principal, clique em **Servidor** e, em seguida, clique em **Registrar servidor**.

![](../images/clients/aqua-data-studio/register-server.png)

A caixa de diálogo *Registrar servidor* é exibida. Na guia *Geral* , selecione **PostgreSQL** na lista no lado esquerdo. Na caixa de diálogo exibida, forneça os detalhes a seguir para as configurações do servidor.

- **Nome**: O nome da sua conexão.
- **Nome de login e senha**: As credenciais de logon que serão usadas. O nome de usuário assume a forma de `ORG_ID@AdobeOrg`.
- **Host e porta**: O terminal do host e sua porta para o Serviço de Query.
- **Banco de dados:** O banco de dados que será usado.

>[!NOTE]
>
>Para obter mais informações sobre como localizar suas credenciais de logon, host, porta e nome do banco de dados, visite a página de [credenciais no Platform](https://platform.adobe.com/query/configuration). Para localizar suas credenciais, faça logon no Platform, clique em **Query** e, em seguida, clique em **Credenciais**.

![](../images/clients/aqua-data-studio/register-server-general-tab.png)

Select the **Driver** tab. Em *Parâmetros*, defina o valor como `?sslmode=require`

![](../images/clients/aqua-data-studio/register-server-driver-tab.png)

Depois de inserir os detalhes da conexão, clique em **Testar conexão** para garantir que suas credenciais funcionem corretamente. Se a conexão for bem-sucedida, clique em **Salvar** para registrar o servidor. A conexão é exibida no *Painel* após o registro bem-sucedido, confirmando que agora você pode se conectar ao servidor e visualização seus objetos de schema.

## Próximas etapas

Agora que você se conectou ao Serviço de Query, é possível usar o Analisador *de* Query no Aqua Data Studio para executar e editar instruções SQL. Para obter mais informações sobre como gravar e executar query, leia o guia [de query](../creating-queries/creating-queries.md)em execução.