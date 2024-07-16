---
keywords: Experience Platform;página inicial;tópicos populares;campanha;campanha;serviços gerenciados;;home;popular topics;Adobe Campaign Managed Cloud Services;campaign;campaign managed services
title: Adobe Campaign Managed Cloud Services
description: Saiba como conectar Cloud Service do Campaign Managed à Platform usando a interface do usuário
exl-id: 8f18bf73-ebf1-4b4e-a12b-964faa0e24cc
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 1%

---

# Adobe Campaign Managed Cloud Services

O Adobe Experience Platform permite que os dados sejam assimilados de fontes externas e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, bancos de dados e muitas outras.

O Adobe Campaign Managed Cloud Services fornece uma plataforma Managed Services para criação de experiências para clientes entre canais, além de um ambiente para a orquestração visual de campanhas, o gerenciamento de interação em tempo real e a execução entre canais. Visite a [documentação do Adobe Campaign v8](https://experienceleague.adobe.com/docs/campaign/campaign-v8/campaign-home.html?lang=pt-BR) para obter mais informações.

A fonte do Adobe Campaign Managed Cloud Services permite trazer registros de entrega e dados de logs de rastreamento do Adobe Campaign v8 para a Adobe Experience Platform.

## Pré-requisitos

Antes de criar uma conexão de origem para trazer seu Campaign v8 para o Experience Platform, primeiro complete os seguintes pré-requisitos:

* [Configure a importação do log de eventos usando o console do cliente Adobe Campaign](#view-delivery-and-tracking-log-data)
* [Criar um esquema XDM ExperienceEvent](#create-a-schema)
* [Criar um conjunto de dados](#create-a-dataset)

### Exibir dados de log de rastreamento e entrega {#view-delivery-and-tracking-log-data}

>[!IMPORTANT]
>
>Você deve ter acesso ao Console do cliente do Adobe Campaign v8 para visualizar os dados de log no Campaign. Visite a [documentação do Campaign v8](https://experienceleague.adobe.com/docs/campaign/campaign-v8/deploy/connect.html) para obter informações sobre como baixar e instalar o console do cliente.

Faça logon na instância do Campaign v8 por meio do Console do cliente. Na guia [!DNL Explorer], selecione [!DNL Administration] e [!DNL Configuration]. Em seguida, selecione [!DNL Data schemas] e aplique o filtro `broadLog` para nome ou rótulo. Na lista exibida, selecione o esquema de origem dos logs de entrega do destinatário com o nome `broadLogRcp`.

![O console do cliente Adobe Campaign v8 com a guia Explorer selecionada, os nós Administração, Configuração e Esquemas de dados foram expandidos e a filtragem foi definida como &quot;ampla&quot;.](./images/campaign/explorer.png)

Em seguida, selecione a guia **Dados**.

![O console do cliente Adobe Campaign v8 com a guia de dados selecionada.](./images/campaign/data.png)

Clique com o botão direito do mouse/toque com a tecla no painel de dados para abrir o menu contextual. Aqui, selecione **Configurar lista...**

![O console do cliente Adobe Campaign v8 com o menu contextual aberto e a opção Configurar lista selecionada.](./images/campaign/configure.png)

A janela de configuração de lista é exibida, fornecendo uma interface na qual você pode adicionar os campos desejados à lista pré-existente para visualizar os dados no painel de dados.

![Uma lista de configurações para logs de entrega de destinatários que podem ser adicionadas para exibição.](./images/campaign/list-configuration.png)

Agora é possível visualizar os logs do delivery do recipient, incluindo os campos de configuração adicionados na etapa anterior.

>[!TIP]
>
>Você pode repetir as mesmas etapas, mas filtrar por `tracking` para exibir os dados do log de rastreamento.

![Os logs de entrega do destinatário foram exibidos com informações sobre seu nome da última modificação, canal de entrega, nome de entrega interno e rótulo.](./images/campaign/recipient-delivery-logs.png)

### Criar um esquema {#create-a-schema}

Em seguida, crie um esquema XDM ExperienceEvent para logs do delivery e logs de rastreamento. Você deve aplicar o grupo de campos Logs de entrega da campanha ao esquema de logs de entrega e o grupo de campos Logs de rastreamento da campanha ao esquema de logs de rastreamento. Você também deve definir o campo `externalID` como a identidade principal do esquema.

>[!NOTE]
>
>Seu esquema XDM ExperienceEvent deve ser habilitado para perfil para assimilar os dados do Campaign para [!DNL Real-Time Customer Profile].

Para obter instruções detalhadas sobre como criar um esquema, leia o manual sobre [criação de um esquema XDM na interface](../../../xdm/tutorials/create-schema-ui.md).

### Criar um conjunto de dados {#create-a-dataset}

Por fim, você deve criar um conjunto de dados para seus esquemas. Para obter instruções detalhadas sobre como criar um conjunto de dados, leia o manual sobre [criação de um conjunto de dados na interface](../../../catalog/datasets/user-guide.md).

## Criar uma conexão de origem do Adobe Campaign Managed Cloud Services usando a interface do usuário da Platform

Agora que você acessou os logs de dados no console do cliente do Campaign, criou um esquema e um conjunto de dados, é possível continuar a criar uma conexão de origem para trazer os dados do Campaign Managed Services para a Platform.

Para obter instruções detalhadas sobre como trazer os dados dos logs de entrega e de rastreamento do Campaign v8 para a Experience Platform, leia o manual sobre [criação de uma conexão de origem do Campaign Managed Services na interface](../../tutorials/ui/create/adobe-applications/campaign.md).

>[!IMPORTANT]
>
>Há um caso periférico em que a interação de um destinatário de email recentemente removido com um email pode assimilar novamente informações pessoais no Experience Platform. Em alguns casos, isso poderia reativar o marketing para esse usuário.
>
>* Esse cenário só estará ativo entre o momento em que uma solicitação de acesso a dados pessoais for executada no Experience Platform e o momento em que for executada no Adobe Campaign Classic. Depois que a solicitação é executada no Campaign, há uma verificação para garantir que o registro não seja exportado para o Campaign. Para resolver esse problema, emita novamente uma solicitação de GDPR após 72 horas da execução.