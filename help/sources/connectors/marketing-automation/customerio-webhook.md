---
title: Visão geral da origem do Customer.io
description: Saiba como conectar o Customer.io à Adobe Experience Platform usando APIs ou a interface do usuário, aproveitando webhooks
badge: "Beta"
source-git-commit: cb4b92f4d71d42d57363e16d4764217b6de7f8ee
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 0%

---

# [!DNL Customer.io]

>[!NOTE]
>
>O [!DNL Customer.io] A fonte está em beta. Leia o [visão geral das fontes](../../home.md#terms-and-conditions) para obter mais informações sobre o uso de fontes com rótulo beta.

O Adobe Experience Platform permite que os dados sejam assimilados de fontes externas e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, bancos de dados e muitas outras.

O Experience Platform oferece suporte para assimilar dados de aplicativos de transmissão. O suporte para provedores de transmissão inclui [!DNL Customer.io].

[[!DNL Customer.io]](https://customer.io/) é uma plataforma de mensagens automatizadas para profissionais de marketing que desejam ter mais controle e flexibilidade para criar e enviar emails orientados por dados, notificações por push, mensagens no aplicativo e SMS.

O [!DNL Customer.io] A fonte permite que você assimile esquemas de evento do Webhook compatíveis e seus dados de evento associados de [!DNL Customer.io] usando o [[!DNL Customer.io] Webhooks de relatórios](https://customer.io/docs/api/webhooks/).

Os esquemas de evento do Webhook compatíveis são:

* Eventos do cliente
* Eventos de email
* Eventos de SMS
* Eventos de notificação por push
* Eventos de mensagens no aplicativo
* Slack Events
* Eventos do Webhook

Para obter uma lista de eventos que estão disponíveis por meio de webhooks, consulte o [[!DNL Customer.io] Relatar eventos do Webhook](https://customer.io/docs/webhooks/#events) documentação.

## Pré-requisitos {#prerequisites}

Antes de criar um [!DNL Customer.io] conexão de origem, você deve primeiro garantir que tenha o seguinte:

* A [!DNL Customer.io] conta. Se você não tiver um, leia o [[!DNL Customer.io] página de inscrição](https://fly.customer.io/signup) para registrar-se e criar sua conta.
* Depois de criar a conta, também será necessário validar a conta. Siga as etapas documentadas na [[!DNL Customer.io] Verificação de conta](https://customer.io/docs/account-verification/) para concluir o processo.

### Configurar [!DNL Customer.io] Webhook {#set-up-webhook}

Depois de criar seu fluxo de dados com sucesso, você deve configurar um Webhook de relatórios para informar a plataforma sobre [!DNL Customer.io] eventos. Os Webhooks podem notificá-lo imediatamente quando os atributos do cliente mudarem ou quando as pessoas abrirem suas mensagens e enviar essas informações para sua [!DNL Customer.io] fonte. Para obter mais informações, leia os tutoriais em [obter o URL do terminal de transmissão](../../tutorials/ui/create/marketing-automation/customerio-webhook.md#get-streaming-endpoint) e [configurar um [!DNL Customer.io] Webhook](../../tutorials/ui/create/marketing-automation/customerio-webhook.md#set-up-webhook).

## Conexão [!DNL Customer.io] para a plataforma {#connect-to-platform}

A documentação abaixo fornece informações sobre como criar um [!DNL Customer.io] conexão de transmissão para conexão com [!DNL Platform] usando APIs ou a interface do usuário:

### Connect [!DNL Customer.io] para Plataforma usando APIs {#connect-to-platform-using-api}

* [Criar uma conexão de origem e um fluxo de dados para trazer [!DNL Customer.io] dados para a Platform usando APIs.](../../tutorials/api/create/marketing-automation/customerio-webhook.md)

### Connect [!DNL Customer.io] para Plataforma usando a interface do usuário {#connect-to-platform-using-ui}

* [Criar uma conexão de origem e um fluxo de dados para trazer [!DNL Customer.io] dados para a Platform usando a interface do usuário](../../tutorials/ui/create/marketing-automation/customerio-webhook.md)

