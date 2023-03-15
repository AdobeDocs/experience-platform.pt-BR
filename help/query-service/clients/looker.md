---
keywords: Experience Platform;início;tópicos populares;Serviço de consulta;serviço de consulta;Pesquisador;observador;conectar ao serviço de consulta;
solution: Experience Platform
title: Conectar Pesquisador ao Serviço de Consulta
description: Este documento aborda as etapas para conectar o Looker ao Serviço de consulta da Adobe Experience Platform.
exl-id: 806e9077-533a-4546-b5ca-8124751957f5
source-git-commit: b059a0191fbf2c3e5d2dfceb9802e2aaa429f7ed
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 0%

---

# Conectar [!DNL Looker] para o Serviço de consulta

Este documento aborda as etapas para a conexão [!DNL Looker] com o Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Este guia supõe que você já tenha acesso ao [!DNL Looker] e estão familiarizados com como navegar em sua interface. Mais informações sobre [!DNL Looker] pode ser encontrado no [oficial [!DNL Looker] documentação](https://docs.looker.com/).

## Criar uma nova conexão de banco de dados {#create-connection}

Depois de fazer logon no [!DNL Looker], selecione **[!DNL Admin]**, seguido por **[!DNL Connections]**. A variável [!DNL Connections] é aberta. No [!DNL Connections] selecione **[!DNL Add Connection]**.

Aqui, insira os detalhes das configurações de conexão listadas abaixo. Consulte a documentação oficial do Looker para [instruções para criar uma nova conexão de banco de dados e descrições das propriedades disponíveis](https://cloud.google.com/looker/docs/connecting-to-your-db#creating_a_new_database_connection).

- **[!DNL Name]:** O nome da sua conexão.
- **[!DNL Dialect]:** O dialeto usado para o banco de dados SQL. [!DNL Query Service] usos **[!DNL PostgreSQL]**.
- **[!DNL Host and Port]:** O endpoint do host e sua porta para [!DNL Query Service].
- **[!DNL Database]:** O banco de dados que será usado.
- **[!DNL Username and Password]:** As credenciais de logon que serão usadas. O nome de usuário estará no formato de `ORG_ID@AdobeOrg`.
- **SSL**: habilite o SSL para garantir uma conexão segura na rede.

Para encontrar as credenciais necessárias para conectar o Looker ao Serviço de consulta, faça logon na interface do usuário da plataforma e selecione **[!UICONTROL Consultas]** na navegação à esquerda, seguido por **[!UICONTROL Credenciais]**. Para obter mais informações sobre como encontrar **host**, **porta**, **banco de dados**, **nome de usuário**, e **senha** credenciais, leia as [guia de credenciais](../ui/credentials.md).

![A página Credenciais do espaço de trabalho Consultas do Experience Platform com as Credenciais e as Credenciais que Estão Expirando são destacadas.](../images/clients/looker/query-service-credentials-page.png)

>[!IMPORTANT]
>
>[!DNL Query Service] O também oferece credenciais sem expiração para permitir uma configuração única com clientes de terceiros. Consulte a documentação para [instruções completas sobre como gerar e usar credenciais sem expiração](../ui/credentials.md#non-expiring-credentials). É necessário concluir esse processo se desejar conectar o Looker como uma configuração única. A variável `credential` e `technicalAccountId` valores adquiridos compõem o valor para o Pesquisador `password` parâmetro.

Para saber mais sobre o suporte SSL para conexões de terceiros no Adobe Experience Platform, consulte [[!DNL Query Service] Documentação do SSL](./ssl-modes.md). Este documento fornece instruções sobre como se conectar usando o `verify-full` Modo SSL.

Depois de inserir os detalhes da conexão, selecione **[!DNL Test These Settings]** para garantir que suas credenciais funcionem corretamente. Mais informações sobre [testando suas configurações de conexão](https://cloud.google.com/looker/docs/connecting-to-your-db#testing_your_connection_settings) são fornecidos na documentação oficial do Looker. Após uma conexão bem-sucedida, uma mensagem é exibida na tela para indicar que você pode se conectar. Depois que a conexão for bem-sucedida, selecione **[!DNL Add Connection]** para criar sua conexão.

## Próximas etapas

Agora que você se conectou com [!DNL Query Service], você pode usar [!DNL Looker] para gravar consultas. Para obter mais informações sobre como gravar e executar consultas, leia o [guia de execução de consultas](../best-practices/writing-queries.md).
