---
keywords: Experience Platform, home, tópicos populares, serviço de consulta, serviço de consulta, Looker, looker, conectar ao serviço de consulta;
solution: Experience Platform
title: Conectar Looker ao Serviço de Consulta
description: Este documento aborda as etapas para conectar o Looker ao Adobe Experience Platform Query Service.
exl-id: 806e9077-533a-4546-b5ca-8124751957f5
source-git-commit: b059a0191fbf2c3e5d2dfceb9802e2aaa429f7ed
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 0%

---

# Connect [!DNL Looker] para Serviço de Consulta

Este documento aborda as etapas para conexão [!DNL Looker] com o Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Este guia supõe que você já tenha acesso ao [!DNL Looker] e estão familiarizados com como navegar em sua interface. Mais informações sobre [!DNL Looker] podem ser encontradas no [funcionário [!DNL Looker] documentação](https://docs.looker.com/).

## Criar uma nova conexão de banco de dados {#create-connection}

Depois de fazer logon em [!DNL Looker], selecione **[!DNL Admin]**, seguida de **[!DNL Connections]**. O [!DNL Connections] será aberta. No [!DNL Connections] página, selecione **[!DNL Add Connection]**.

Aqui, insira os detalhes das configurações de conexão listadas abaixo. Consulte a documentação oficial do Looker para [instruções para criar uma nova conexão de banco de dados e descrições das propriedades disponíveis](https://cloud.google.com/looker/docs/connecting-to-your-db#creating_a_new_database_connection).

- **[!DNL Name]:** O nome da sua conexão.
- **[!DNL Dialect]:** O dialeto usado para o banco de dados SQL. [!DNL Query Service] uses **[!DNL PostgreSQL]**.
- **[!DNL Host and Port]:** O terminal do host e sua porta para [!DNL Query Service].
- **[!DNL Database]:** O banco de dados que será usado.
- **[!DNL Username and Password]:** As credenciais de logon que serão usadas. O nome de usuário estará no formato de `ORG_ID@AdobeOrg`.
- **SSL**: Ative o SSL para garantir uma conexão segura na rede.

Para localizar as credenciais necessárias para conectar o Looker ao Serviço de Consulta, faça logon na interface do usuário da plataforma e selecione **[!UICONTROL Queries]** no menu de navegação esquerdo, seguido por **[!UICONTROL Credenciais]**. Para obter mais informações sobre como encontrar seu **host**, **porta**, **banco de dados**, **username** e **senha** credenciais, leia a [guia de credenciais](../ui/credentials.md).

![A página Credenciais do espaço de trabalho Consultas do Experience Platform com Credenciais e as Credenciais de Expiração destacadas.](../images/clients/looker/query-service-credentials-page.png)

>[!IMPORTANT]
>
>[!DNL Query Service] O também oferece credenciais que não estão expirando para permitir uma configuração única com clientes de terceiros. Consulte a documentação para [instruções completas sobre como gerar e usar credenciais que não estão expirando](../ui/credentials.md#non-expiring-credentials). É necessário concluir esse processo se você quiser conectar o Looker como uma configuração única. O `credential` e `technicalAccountId` os valores adquiridos incluem o valor do Looker `password` parâmetro.

Para saber mais sobre o suporte SSL para conexões de terceiros no Adobe Experience Platform, consulte o [[!DNL Query Service] Documentação SSL](./ssl-modes.md). Este documento fornece instruções sobre como se conectar usando `verify-full` Modo SSL.

Depois de ter inserido os detalhes da conexão, selecione **[!DNL Test These Settings]** para garantir que suas credenciais funcionem corretamente. Mais informações sobre [teste das configurações de conexão](https://cloud.google.com/looker/docs/connecting-to-your-db#testing_your_connection_settings) são fornecidas na documentação oficial do Looker. Após uma conexão bem-sucedida, uma mensagem é exibida na tela para indicar que você pode se conectar. Depois que a conexão for bem-sucedida, selecione **[!DNL Add Connection]** para criar a conexão.

## Próximas etapas

Agora que você se conectou a [!DNL Query Service], você pode usar [!DNL Looker] para gravar queries. Para obter mais informações sobre como gravar e executar consultas, leia o [guia de execução de consultas](../best-practices/writing-queries.md).
