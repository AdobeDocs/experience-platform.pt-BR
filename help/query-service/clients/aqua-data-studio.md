---
keywords: Experience Platform;home;tópicos populares;serviço de consulta;serviço de consulta;Aqua Data Studio;Aqua data studio;conectar ao serviço de consulta;
solution: Experience Platform
title: Conectar o Aqua Data Studio ao Serviço de consulta
description: Este documento aborda as etapas para conectar o Aqua Data Studio ao Serviço de consulta do Adobe Experience Platform.
exl-id: 4770e221-48a7-45d8-80a4-60b5cbc0ec33
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---

# Conectar [!DNL Aqua Data Studio] ao Serviço de consulta

Este documento aborda as etapas para conectar o [!DNL Aqua Data Studio] ao Adobe Experience Platform [!DNL Query Service].

## Introdução

Este guia requer que você já tenha acesso ao [!DNL Aqua Data Studio] e esteja familiarizado com como navegar em sua interface. Mais informações sobre [!DNL Aqua Data Studio] podem ser encontradas na [documentação [!DNL Aqua Data Studio] oficial](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation21.1/page/0/Aqua-Data-Studio-21-1).

>[!NOTE]
>
>Há [!DNL Windows] e [!DNL macOS] versões de [!DNL Aqua Data Studio]. As capturas de tela neste guia foram feitas usando o aplicativo de desktop [!DNL macOS]. Pode haver pequenas discrepâncias na interface do usuário entre as versões.

Para adquirir as credenciais necessárias para conectar [!DNL Aqua Data Studio] ao Experience Platform, você deve ter acesso ao espaço de trabalho [!UICONTROL Consultas] na interface do usuário do Experience Platform. Entre em contato com o administrador da organização se você não tiver acesso ao espaço de trabalho [!UICONTROL Consultas].

## Registrar o servidor {#register-server}

Depois de instalar o [!DNL Aqua Data Studio], primeiro você deve registrar o servidor. Consulte a documentação oficial do Aqua Data Studio para obter instruções sobre como [iniciar a [!DNL Register Server] caixa de diálogo](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation18/page/81/Registering-a-Database-Server#launching_the_register_server_dialog) e [registrar o servidor](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation18/page/81/Registering-a-Database-Server#steps_to_register_a_server_in_aqua_data_studio).

Quando a caixa de diálogo **[!DNL Register Server]** for exibida para um servidor PostgresSQL, forneça os detalhes a seguir para as configurações do servidor.

- **[!DNL Name]**: O nome da sua conexão. É recomendável fornecer um nome amigável para reconhecer a conexão.
- **[!DNL Login Name]**: O nome de logon é sua ID da organização da Experience Platform. Ele assume a forma de `ORG_ID@AdobeOrg`.
- **[!DNL Password]**: esta é uma cadeia de caracteres alfanumérica encontrada no painel de credenciais [!DNL Query Service].
- **[!DNL Host and Port]**: O ponto de extremidade do host e sua porta para [!DNL Query Service]. Você deve usar a porta 80 para se conectar com [!DNL Query Service].
- **[!DNL Database]:** O banco de dados que será usado. Use o valor para a credencial de interface do usuário do Experience Platform `dbname`: `prod:all`.

### [!DNL Query Service] credenciais

Para encontrar suas credenciais, faça logon na interface do usuário do [!DNL Experience Platform] e selecione **[!UICONTROL Consultas]** na navegação à esquerda, seguido de **[!UICONTROL Credenciais]**. Para obter instruções completas para localizar suas credenciais de logon, host, porta e nome do banco de dados, leia o [guia de credenciais](../ui/credentials.md).

[!DNL Query Service] também oferece credenciais sem expiração para permitir uma configuração única com clientes de terceiros. Consulte a documentação de [instruções completas sobre como gerar e usar credenciais sem expiração](../ui/credentials.md#non-expiring-credentials).

### Definição do modo SSL

Em seguida, defina o valor do modo SSL como `?sslmode=require`. Isso é feito na guia [!DNL Driver] da caixa de diálogo [!DNL Edit Server Properties]. Consulte a documentação oficial do Aqua Data Studio para obter instruções sobre como [editar propriedades do driver](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation13/page/116/PostgreSQL#drivers) e [configurar o SSL para [!DNL PostgreSQL]](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation20/page/SSL-Configuration/SSL-Configuration). Use a barra de pesquisa para localizar a propriedade `sslmode`.

>[!IMPORTANT]
>
>Consulte a [[!DNL Query Service] documentação SSL](./ssl-modes.md) para saber mais sobre o suporte SSL para conexões de terceiros ao Serviço de Consulta da Adobe Experience Platform e como se conectar usando o modo SSL `verify-full`.

Depois de inserir os detalhes da conexão, na mesma guia, selecione **[!DNL Test Connection]** para garantir que suas credenciais funcionem corretamente. Se o teste de conexão for bem-sucedido, selecione **[!DNL Save]** para registrar o servidor. Uma caixa de diálogo de confirmação é exibida confirmando a conexão, e o ícone de conexão é exibido no painel. Agora você pode se conectar ao servidor e visualizar seus objetos de esquema.

## Próximas etapas

Agora que você se conectou a [!DNL Query Service], é possível usar **[!DNL Query Analyzer]** em [!DNL Aqua Data Studio] para executar e editar instruções SQL. Para obter mais informações sobre como gravar e executar consultas, leia o [guia de execução de consultas](../best-practices/writing-queries.md).
