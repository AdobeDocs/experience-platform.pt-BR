---
keywords: Experience Platform;página inicial;tópicos populares;Serviço de consulta;serviço de consulta;Pesquisador;observador;conectar ao serviço de consulta;
solution: Experience Platform
title: Conectar Pesquisador ao Serviço de Consulta
description: Este documento aborda as etapas para conectar o Looker ao Serviço de consulta da Adobe Experience Platform.
exl-id: 806e9077-533a-4546-b5ca-8124751957f5
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---

# Conectar [!DNL Looker] ao Serviço de consulta

Este documento aborda as etapas para conectar o [!DNL Looker] ao Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Este guia supõe que você já tenha acesso ao [!DNL Looker] e esteja familiarizado com como navegar em sua interface. Mais informações sobre [!DNL Looker] podem ser encontradas na [documentação [!DNL Looker] oficial](https://docs.looker.com/).

## Criar uma nova conexão de banco de dados {#create-connection}

Depois de fazer logon em [!DNL Looker], selecione **[!DNL Admin]**, seguido por **[!DNL Connections]**. A página [!DNL Connections] é aberta. Na página [!DNL Connections], selecione **[!DNL Add Connection]**.

Aqui, insira os detalhes das configurações de conexão listadas abaixo. Consulte a documentação oficial do Looker para obter [instruções sobre como criar uma nova conexão de banco de dados e descrições das propriedades disponíveis](https://cloud.google.com/looker/docs/connecting-to-your-db#creating_a_new_database_connection).

- **[!DNL Name]:** O nome da sua conexão.
- **[!DNL Dialect]:** O dialeto usado para o banco de dados SQL. [!DNL Query Service] usa **[!DNL PostgreSQL]**.
- **[!DNL Host and Port]:** O ponto de extremidade do host e sua porta para [!DNL Query Service].
- **[!DNL Database]:** O banco de dados que será usado.
- **[!DNL Username and Password]:** As credenciais de logon que serão usadas. O nome de usuário terá o formato de `ORG_ID@AdobeOrg`.
- **SSL**: habilite o SSL para garantir uma conexão segura na rede.

Para localizar as credenciais necessárias para conectar o Looker ao Serviço de Consulta, faça logon na interface do usuário do Experience Platform e selecione **[!UICONTROL Consultas]** na navegação à esquerda, seguido de **[!UICONTROL Credenciais]**. Para obter mais informações sobre como localizar suas credenciais de **host**, **porta**, **banco de dados**, **nome de usuário** e **senha**, leia o [guia de credenciais](../ui/credentials.md).

![A página Credenciais do espaço de trabalho Consultas do Experience Platform com as Credenciais e as Credenciais que Estão Expirando foi realçada.](../images/clients/looker/query-service-credentials-page.png)

>[!IMPORTANT]
>
>[!DNL Query Service] também oferece credenciais sem expiração para permitir uma configuração única com clientes de terceiros. Consulte a documentação de [instruções completas sobre como gerar e usar credenciais sem expiração](../ui/credentials.md#non-expiring-credentials). É necessário concluir esse processo se desejar conectar o Looker como uma configuração única. Os valores `credential` e `technicalAccountId` adquiridos compõem o valor do parâmetro Looker `password`.

Para saber mais sobre o suporte SSL para conexões de terceiros no Adobe Experience Platform, consulte a [[!DNL Query Service] documentação SSL](./ssl-modes.md). Este documento fornece instruções sobre como se conectar usando o modo SSL do `verify-full`.

Depois de inserir os detalhes da conexão, selecione **[!DNL Test These Settings]** para garantir que suas credenciais funcionem corretamente. Mais informações sobre [teste das configurações de conexão](https://cloud.google.com/looker/docs/connecting-to-your-db#testing_your_connection_settings) são fornecidas na documentação oficial do Looker. Após uma conexão bem-sucedida, uma mensagem é exibida na tela para indicar que você pode se conectar. Depois que a conexão for bem-sucedida, selecione **[!DNL Add Connection]** para criar a conexão.

## Próximas etapas

Agora que você se conectou com [!DNL Query Service], pode usar [!DNL Looker] para gravar consultas. Para obter mais informações sobre como gravar e executar consultas, leia o [guia de execução de consultas](../best-practices/writing-queries.md).
