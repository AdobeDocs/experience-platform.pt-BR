---
title: Visão geral do Source do Customer.io
description: Saiba como conectar o Customer.io ao Adobe Experience Platform usando APIs ou a interface do usuário utilizando webhooks
badge: Beta
exl-id: 0f4ee106-c22b-465c-9c5e-83709e8424f5
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 0%

---

# [!DNL Customer.io]

>[!NOTE]
>
>A origem [!DNL Customer.io] está na versão beta. Leia a [visão geral das fontes](../../home.md#terms-and-conditions) para obter mais informações sobre o uso de fontes com rótulo beta.

O Adobe Experience Platform permite que os dados sejam assimilados de fontes externas e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, bancos de dados e muitas outras.

O Experience Platform fornece suporte para assimilação de dados de aplicativos de transmissão contínua. O suporte para provedores de streaming inclui [!DNL Customer.io].

[[!DNL Customer.io]](https://customer.io/) é uma plataforma de mensagens automatizada para profissionais de marketing que desejam mais controle e flexibilidade para criar e enviar emails orientados por dados, notificações por push, mensagens no aplicativo e SMS.

A origem [!DNL Customer.io] permite assimilar esquemas de evento de webhook com suporte e seus dados de evento associados de [!DNL Customer.io] usando os [[!DNL Customer.io] Webhooks de relatórios](https://customer.io/docs/api/webhooks/).

Os esquemas de evento de webhook compatíveis são:

* Eventos para clientes
* Eventos de e-mail
* Eventos de SMS
* Eventos de notificação por push
* Eventos de mensagem no aplicativo
* Eventos Slack
* Eventos do Webhook

Para obter uma lista de eventos que estão disponíveis por meio de webhooks, consulte a documentação [[!DNL Customer.io] Eventos do Webhook de relatórios](https://customer.io/docs/webhooks/#events).

## Pré-requisitos {#prerequisites}

Antes de criar uma conexão de origem [!DNL Customer.io], primeiro verifique se você tem o seguinte:

* Uma conta [!DNL Customer.io]. Se você não tiver uma, leia a [[!DNL Customer.io] página de inscrição](https://fly.customer.io/signup) para registrar e criar sua conta.
* Depois de criar sua conta, também será necessário validá-la. Siga as etapas documentadas na página [[!DNL Customer.io] Verificação de conta](https://customer.io/docs/account-verification/) para concluir o processo.

### Configurar Webhook [!DNL Customer.io] {#set-up-webhook}

Depois de criar o fluxo de dados com êxito, você deve configurar um Webhook de relatórios para informar a Platform sobre eventos do [!DNL Customer.io]. Os webhooks podem notificá-lo imediatamente quando os atributos do cliente forem alterados ou quando as pessoas abrirem suas mensagens e enviar essas informações para sua origem [!DNL Customer.io]. Para obter mais informações, leia os tutoriais em [obtendo a URL do ponto de extremidade de streaming](../../tutorials/ui/create/marketing-automation/customerio-webhook.md#get-streaming-endpoint) e [configurando um [!DNL Customer.io] Webhook](../../tutorials/ui/create/marketing-automation/customerio-webhook.md#set-up-webhook).

## Conectando [!DNL Customer.io] à plataforma {#connect-to-platform}

A documentação abaixo fornece informações sobre como criar uma conexão de streaming do [!DNL Customer.io] para se conectar ao [!DNL Platform] usando APIs ou a interface do usuário:

### Conectar [!DNL Customer.io] à plataforma usando APIs {#connect-to-platform-using-api}

* [Crie uma conexão de origem e um fluxo de dados para trazer  [!DNL Customer.io]  dados para a Platform usando APIs.](../../tutorials/api/create/marketing-automation/customerio-webhook.md)

### Conectar [!DNL Customer.io] à Plataforma usando a interface {#connect-to-platform-using-ui}

* [Crie uma conexão de origem e um fluxo de dados para trazer  [!DNL Customer.io]  dados para a Platform usando a interface do usuário](../../tutorials/ui/create/marketing-automation/customerio-webhook.md)
