---
keywords: Experience Platform, home, tópicos populares, serviço de consulta, serviço de consulta, Aqua Data Studio, Aqua data studio, conectar ao serviço de consulta;
solution: Experience Platform
title: Conectar o Aqua Data Studio ao Serviço de Consulta
description: Este documento aborda as etapas para conectar o Aqua Data Studio com o Adobe Experience Platform Query Service.
exl-id: 4770e221-48a7-45d8-80a4-60b5cbc0ec33
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 0%

---

# Connect [!DNL Aqua Data Studio] para Serviço de Consulta

Este documento aborda as etapas para conexão [!DNL Aqua Data Studio] com o Adobe Experience Platform [!DNL Query Service].

## Introdução

Este guia requer que você já tenha acesso ao [!DNL Aqua Data Studio] e familiarize-se com como navegar em sua interface. Mais informações sobre [!DNL Aqua Data Studio] podem ser encontradas no [funcionário [!DNL Aqua Data Studio] documentação](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation21.1/page/0/Aqua-Data-Studio-21-1).

>[!NOTE]
>
>Existem [!DNL Windows] e [!DNL macOS] versões de [!DNL Aqua Data Studio]. As capturas de tela deste guia foram realizadas com o uso da variável [!DNL macOS] aplicativo de desktop. Pode haver pequenas discrepâncias na interface do usuário entre as versões do .

Para adquirir as credenciais necessárias para conexão [!DNL Aqua Data Studio] para o Experience Platform, você deve ter acesso ao [!UICONTROL Queries] na interface do usuário da plataforma. Entre em contato com o administrador da organização caso não tenha acesso ao [!UICONTROL Queries] espaço de trabalho.

## Registrar o servidor {#register-server}

Depois de instalar [!DNL Aqua Data Studio], primeiro registre o servidor . Consulte a documentação oficial do Aqua Data Studio para obter instruções sobre como [inicie o [!DNL Register Server] diálogo](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation18/page/81/Registering-a-Database-Server#launching_the_register_server_dialog) e [registrar o servidor](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation18/page/81/Registering-a-Database-Server#steps_to_register_a_server_in_aqua_data_studio).

Uma vez **[!DNL Register Server]** for exibida em um servidor PostgresSQL, forneça os seguintes detalhes para as configurações do servidor.

- **[!DNL Name]**: O nome da sua conexão. É recomendável fornecer um nome amigável para reconhecer a conexão.
- **[!DNL Login Name]**: O nome de logon é a ID da organização da plataforma. Assume a forma de `ORG_ID@AdobeOrg`.
- **[!DNL Password]**: Esta é uma sequência de caracteres alfanuméricos encontrada no [!DNL Query Service] painel de credenciais.
- **[!DNL Host and Port]**: O terminal do host e sua porta para [!DNL Query Service]. Você deve usar a porta 80 para se conectar [!DNL Query Service].
- **[!DNL Database]:** O banco de dados que será usado. Usar o valor da credencial da interface do usuário da plataforma `dbname`: `prod:all`.

### [!DNL Query Service] credenciais

Para localizar suas credenciais, faça logon no [!DNL Platform] IU e selecione **[!UICONTROL Queries]** no menu de navegação esquerdo, seguido por **[!UICONTROL Credenciais]**. Para obter instruções completas para encontrar suas credenciais de logon, host, porta e nome do banco de dados, leia a [guia de credenciais](../ui/credentials.md).

[!DNL Query Service] O também oferece credenciais que não estão expirando para permitir uma configuração única com clientes de terceiros. Consulte a documentação para [instruções completas sobre como gerar e usar credenciais que não estão expirando](../ui/credentials.md#non-expiring-credentials).

### Configuração do modo SSL

Em seguida, defina o valor do modo SSL como `?sslmode=require`. Isso é feito da [!DNL Driver] da guia [!DNL Edit Server Properties] caixa de diálogo. Consulte a documentação oficial do Aqua Data Studio para obter instruções sobre como [editar propriedades do driver](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation13/page/116/PostgreSQL#drivers) e [configurar SSL para [!DNL PostgreSQL]](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation20/page/SSL-Configuration/SSL-Configuration). Use a barra de pesquisa para localizar a variável `sslmode` propriedade.

>[!IMPORTANT]
>
>Consulte a [[!DNL Query Service] Documentação SSL](./ssl-modes.md) para saber mais sobre o suporte SSL para conexões de terceiros com o Adobe Experience Platform Query Service e como se conectar usando `verify-full` Modo SSL.

Depois de inserir os detalhes da conexão, na mesma guia, selecione **[!DNL Test Connection]** para garantir que suas credenciais funcionem corretamente. Se o teste de conexão for bem-sucedido, selecione **[!DNL Save]** para registrar seu servidor. Uma caixa de diálogo de confirmação é exibida confirmando a conexão e o ícone de conexão é exibido no painel. Agora é possível se conectar ao servidor e exibir seus objetos de esquema.

## Próximas etapas

Agora que você se conectou a [!DNL Query Service], você pode usar o **[!DNL Query Analyzer]** within [!DNL Aqua Data Studio] para executar e editar instruções SQL. Para obter mais informações sobre como gravar e executar consultas, leia o [guia de execução de consultas](../best-practices/writing-queries.md).
