---
keywords: Experience Platform;início;tópicos populares;serviço de consulta;serviço de consulta;Aqua Data Studio;Aqua data studio;conectar ao serviço de consulta;
solution: Experience Platform
title: Conectar o Aqua Data Studio ao Serviço de consulta
description: Este documento aborda as etapas para conectar o Aqua Data Studio ao Serviço de consulta do Adobe Experience Platform.
exl-id: 4770e221-48a7-45d8-80a4-60b5cbc0ec33
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 0%

---

# Conectar [!DNL Aqua Data Studio] para o Serviço de consulta

Este documento aborda as etapas para a conexão [!DNL Aqua Data Studio] com o Adobe Experience Platform [!DNL Query Service].

## Introdução

Este guia requer que você já tenha acesso ao [!DNL Aqua Data Studio] e familiarizar-se com a navegação em sua interface. Mais informações sobre [!DNL Aqua Data Studio] pode ser encontrado no [oficial [!DNL Aqua Data Studio] documentação](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation21.1/page/0/Aqua-Data-Studio-21-1).

>[!NOTE]
>
>Há [!DNL Windows] e [!DNL macOS] versões de [!DNL Aqua Data Studio]. As capturas de tela neste guia foram feitas usando o [!DNL macOS] aplicativo de desktop. Pode haver pequenas discrepâncias na interface do usuário entre as versões.

Para adquirir as credenciais necessárias para conexão [!DNL Aqua Data Studio] para Experience Platform, você deve ter acesso à [!UICONTROL Consultas] espaço de trabalho na interface do usuário da Platform. Entre em contato com o administrador da organização se você não tiver acesso à [!UICONTROL Consultas] espaço de trabalho.

## Registrar o servidor {#register-server}

Após a instalação [!DNL Aqua Data Studio], você deve primeiro registrar o servidor. Consulte a documentação oficial do Aqua Data Studio para obter instruções sobre como [inicie o [!DNL Register Server] caixa de diálogo](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation18/page/81/Registering-a-Database-Server#launching_the_register_server_dialog) e [registrar o servidor](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation18/page/81/Registering-a-Database-Server#steps_to_register_a_server_in_aqua_data_studio).

Quando a variável **[!DNL Register Server]** para um servidor PostgresSQL, forneça os seguintes detalhes para as configurações do servidor.

- **[!DNL Name]**: o nome da sua conexão. É recomendável fornecer um nome amigável para reconhecer a conexão.
- **[!DNL Login Name]**: o nome de logon é sua ID da Platform Organization. Assume a forma de `ORG_ID@AdobeOrg`.
- **[!DNL Password]**: esta é uma sequência alfanumérica encontrada no [!DNL Query Service] painel de credenciais.
- **[!DNL Host and Port]**: O endpoint do host e sua porta para [!DNL Query Service]. Você deve usar a porta 80 para se conectar com [!DNL Query Service].
- **[!DNL Database]:** O banco de dados que será usado. Usar o valor para a credencial da interface do usuário da Platform `dbname`: `prod:all`.

### [!DNL Query Service] credenciais

Para encontrar suas credenciais, faça logon na [!DNL Platform] Interface do usuário e selecione **[!UICONTROL Consultas]** na navegação à esquerda, seguido por **[!UICONTROL Credenciais]**. Para obter instruções completas para localizar suas credenciais de logon, host, porta e nome do banco de dados, leia o [guia de credenciais](../ui/credentials.md).

[!DNL Query Service] O também oferece credenciais sem expiração para permitir uma configuração única com clientes de terceiros. Consulte a documentação para [instruções completas sobre como gerar e usar credenciais sem expiração](../ui/credentials.md#non-expiring-credentials).

### Definição do modo SSL

Em seguida, defina o valor do modo SSL como `?sslmode=require`. Isso é feito a partir do [!DNL Driver] guia do [!DNL Edit Server Properties] diálogo. Consulte a documentação oficial do Aqua Data Studio para obter instruções sobre como [editar propriedades do driver](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation13/page/116/PostgreSQL#drivers) e [configurar SSL para [!DNL PostgreSQL]](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation20/page/SSL-Configuration/SSL-Configuration). Use a barra de pesquisa para localizar o `sslmode` propriedade.

>[!IMPORTANT]
>
>Consulte a [[!DNL Query Service] Documentação do SSL](./ssl-modes.md) para saber mais sobre o suporte SSL para conexões de terceiros ao Adobe Experience Platform Query Service e como se conectar usando `verify-full` Modo SSL.

Depois de inserir os detalhes da conexão, na mesma guia, selecione **[!DNL Test Connection]** para garantir que suas credenciais funcionem corretamente. Se o teste de conexão for bem-sucedido, selecione **[!DNL Save]** para registrar o servidor. Uma caixa de diálogo de confirmação é exibida confirmando a conexão, e o ícone de conexão é exibido no painel. Agora você pode se conectar ao servidor e visualizar seus objetos de esquema.

## Próximas etapas

Agora que você se conectou ao [!DNL Query Service], você pode usar o **[!DNL Query Analyzer]** no prazo de [!DNL Aqua Data Studio] para executar e editar instruções SQL. Para obter mais informações sobre como gravar e executar consultas, leia o [guia de execução de consultas](../best-practices/writing-queries.md).
