---
title: Visão geral do Pendo Source
description: Saiba como conectar o Pendo ao Adobe Experience Platform usando APIs ou a interface do usuário utilizando webhooks
badge: Beta
exl-id: 376f18ef-1eea-4c42-8041-6fadb5906e9b
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 0%

---

# [!DNL Pendo]

>[!NOTE]
>
>A origem [!DNL Pendo] está na versão beta. Leia a [visão geral das fontes](../../home.md#terms-and-conditions) para obter mais informações sobre o uso de fontes com rótulo beta.

O Adobe Experience Platform permite que os dados sejam assimilados de fontes externas e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da Experience Platform. Você pode assimilar dados de várias fontes, como aplicativos da Adobe, armazenamento baseado em nuvem, bancos de dados e muitas outras.

O Experience Platform oferece suporte para assimilação de dados de aplicativos de análise de terceiros. O suporte para provedores de análise inclui [!DNL Pendo].

[[!DNL Pendo]](https://pendo.io/) é um aplicativo de análise de produtos criado para ajudar empresas de software a desenvolver produtos que repercutem com os clientes. O aplicativo permite que os fabricantes de software incorporem seus produtos a uma grande variedade de ferramentas, o que pode resultar em uma melhor experiência do produto para os usuários e em novos insights para a equipe de produtos.

A origem [!DNL Pendo] permite assimilar esquemas de evento de webhook com suporte e seus dados de evento associados de [!DNL Pendo.io] usando os [[!DNL Pendo] Webhooks](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks). A origem [!DNL Pendo] funciona com webhooks de URL [!DNL Pendo].

Os webhooks compatíveis são:

* [Guia](https://support.pendo.io/hc/en-us/articles/8146679315867-Creating-a-Guide) Exibido
* [Votação](https://support.pendo.io/hc/en-us/articles/360031867152-Polls-Classic-) Exibida/Enviada
* [Pontuação do Net Promoter](https://support.pendo.io/hc/en-us/articles/360033527151-Set-up-an-NPS-Survey) exibida/enviada

## Pré-requisitos {#prerequisites}

Antes de criar uma conexão de origem [!DNL Pendo], primeiro verifique se você tem o seguinte:

Uma conta [!DNL Pendo]. Caso ainda não tenha uma, consulte a página [[!DNL Pendo] registrar](https://app.pendo.io/register) para registrar e criar sua conta.

### Configurar Webhook [!DNL Pendo] {#set-up-webhook}

Depois de criar o fluxo de dados com êxito, você deve configurar um webhook para informar a Experience Platform sobre [!DNL Pendo] eventos. Os Webhooks do [!DNL Pendo] podem enviar notificações em tempo real para outros serviços quando determinados eventos ocorrem e enviar essas informações para a origem do [!DNL Pendo]. Para obter mais informações, leia os tutoriais em [obtendo a URL do ponto de extremidade de streaming](../../tutorials/ui/create/analytics/pendo-webhook.md#get-streaming-endpoint) e [configurando um [!DNL Pendo] Webhook](../../tutorials/ui/create/analytics/pendo-webhook.md#set-up-webhook).

## Conectando [!DNL Pendo] ao Experience Platform {#connect-to-platform}

A documentação abaixo fornece informações sobre como criar um conector de streaming [!DNL Pendo] para se conectar ao [!DNL Experience Platform] usando APIs ou a interface do usuário:

### Conectar o [!DNL Pendo] ao Experience Platform usando APIs {#connect-to-platform-using-api}

* [Crie uma conexão de origem para trazer dados do  [!DNL Pendo]  para a Experience Platform usando APIs.](../../tutorials/api/create/analytics/pendo-webhook.md)

### Conectar o [!DNL Pendo] ao Experience Platform usando a interface {#connect-to-platform-using-ui}

* [Criar uma conexão de origem para trazer dados do  [!DNL Pendo]  para o Experience Platform usando a interface do usuário](../../tutorials/ui/create/analytics/pendo-webhook.md)
