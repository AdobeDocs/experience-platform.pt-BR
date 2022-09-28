---
keywords: Experience Platform, home, tópicos populares, Adobe Campaign Managed Cloud Services, campanha, serviços gerenciados de campanha
title: Adobe Campaign Managed Cloud Services
description: Saiba como conectar o Campaign Managed Cloud Services à Platform usando a interface do usuário
source-git-commit: 99f65889aecf8c045dbb72053ebaca9429c3ebe1
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Adobe Campaign Managed Cloud Services

O Adobe Experience Platform permite que os dados sejam assimilados de fontes externas e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, bancos de dados e muitas outras.

O Adobe Campaign Managed Cloud Services oferece uma plataforma Managed Services para projetar experiências de clientes entre canais e fornece um ambiente para a orquestração visual de campanhas, o gerenciamento de interação em tempo real e a execução entre canais. Visite o [Documentação do Adobe Campaign v8](https://experienceleague.adobe.com/docs/campaign/campaign-v8/campaign-home.html?lang=en) para obter mais informações.

A fonte do Adobe Campaign Managed Cloud Services permite trazer logs do delivery e dados de logs de rastreamento do Adobe Campaign v8 para o Adobe Experience Platform.

## Pré-requisitos

Antes de criar uma conexão de origem para trazer seu Campaign v8 para o Experience Platform, primeiro complete os seguintes pré-requisitos:

* [Configure sua importação de log de eventos usando o console do cliente do Adobe Campaign](#view-delivery-and-tracking-log-data)
* [Criar um esquema XDM ExperienceEvent](#create-a-schema)
* [Criar um conjunto de dados](#create-a-dataset)

### Exibir dados de log de delivery e rastreamento {#view-delivery-and-tracking-log-data}

>[!IMPORTANT]
>
>Você deve ter acesso ao Console do Cliente do Adobe Campaign v8 para visualizar seus dados de log no Campaign. Visite o [Documentação do Campaign v8](https://experienceleague.adobe.com/docs/campaign/campaign-v8/deploy/connect.html?lang=en) para obter informações sobre como baixar e instalar o console do cliente.

Faça logon na instância do Campaign v8 por meio do Console do cliente. Em [!DNL Explorer] guia , selecione [!DNL Administration] e depois selecione [!DNL Configuration]. Em seguida, selecione [!DNL Data schemas] e, em seguida, aplique a variável `broadLog` filtro para nome ou rótulo. Na lista exibida, selecione o schema de origem dos logs do delivery do recipient com o nome `broadLogRcp`.

![O console do cliente Adobe Campaign v8 com a guia Explorer selecionada, os nós de schemas Administração, Configuração e Dados expandiram e a filtragem foi definida como &quot;ampla&quot;.](./images/campaign/explorer.png)

Em seguida, selecione o **Dados** guia .

![O console do cliente Adobe Campaign v8 com a guia de dados selecionada.](./images/campaign/data.png)

Clique com o botão direito/pressionamento de tecla no painel de dados para abrir o menu contextual. Aqui, selecione **Configurar lista...**

![O console do cliente Adobe Campaign v8 com o menu contextual aberto e a opção Configure list selecionada.](./images/campaign/configure.png)

A janela de configuração da lista é exibida, fornecendo uma interface onde é possível adicionar os campos desejados à lista preexistente para exibir os dados no painel de dados.

![Uma lista de configurações para logs de delivery de recipients que podem ser adicionadas para visualização.](./images/campaign/list-configuration.png)

Agora é possível visualizar os logs do delivery do recipient, incluindo os campos de configuração adicionados na etapa anterior.

>[!TIP]
>
>Você pode repetir as mesmas etapas, mas filtrar por `tracking` para exibir seus dados de log de rastreamento.

![Os logs do delivery do recipient são exibidos com informações sobre seu sobrenome modificado, canal de delivery, nome do delivery interno e rótulo.](./images/campaign/recipient-delivery-logs.png)

### Criar um esquema {#create-a-schema}

Em seguida, crie um esquema XDM ExperienceEvent para logs de delivery e de rastreamento. Você deve aplicar o grupo de campos Campaign Delivery Logs ao schema de logs do delivery e ao grupo de campos Campaign Tracking Logs ao schema de logs de rastreamento. Você também deve definir a variável `externalID` como a identidade primária do esquema.

>[!NOTE]
>
>O esquema XDM ExperienceEvent deve estar habilitado para o perfil para assimilar os dados do Campaign para [!DNL Real-time Customer Profile].

Para obter instruções detalhadas sobre como criar um schema, leia o guia em [criação de um esquema XDM na interface do usuário](../../../xdm/tutorials/create-schema-ui.md).

### Criar um conjunto de dados {#create-a-dataset}

Por fim, você deve criar um conjunto de dados para seus esquemas. Para obter instruções detalhadas sobre como criar um conjunto de dados, leia o guia em [criação de um conjunto de dados na interface do usuário](../../../catalog/datasets/user-guide.md).

## Criar uma conexão de origem do Adobe Campaign Managed Cloud Services usando a interface do usuário da plataforma

Agora que você acessou seus logs de dados no console do cliente Campaign, criou um esquema e um conjunto de dados, agora é possível continuar a criar uma conexão de origem para trazer seus dados do Campaign Managed Services para a Platform.

Para obter instruções detalhadas sobre como trazer seus logs de delivery e dados de logs de rastreamento do Campaign v8 para a Experience Platform, leia o guia em [criação de uma conexão de origem Managed Services do Campaign na interface do usuário](../../tutorials/ui/create/adobe-applications/campaign.md).