---
title: Visão geral da fonte de chatlio
description: Saiba como conectar o Chatlio ao Adobe Experience Platform usando APIs ou a interface do usuário, aproveitando webhooks
badge: Beta
last-substantial-update: 2023-03-29T00:00:00Z
exl-id: 4a71d1dc-e0eb-443e-a956-8caa0e82fa18
source-git-commit: 0cc4eab97dcd56d2b1d679cf5f35932976d22634
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# [!DNL Chatlio]

>[!NOTE]
>
>O [!DNL Chatlio] A fonte está em beta. Leia o [visão geral das fontes](../../home.md#terms-and-conditions) para obter mais informações sobre o uso de fontes com rótulo beta.

O Adobe Experience Platform permite que os dados sejam assimilados de fontes externas e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, bancos de dados e muitas outras.

O Experience Platform oferece suporte para assimilar dados de aplicativos de transmissão. O suporte para provedores de transmissão inclui [!DNL Chatlio].

[[!DNL Chatlio]](https://chatlio.com/) O é um aplicativo de bate-papo ao vivo totalmente integrado ao [!DNL Slack] e facilita vários agentes de suporte para ajudar simultaneamente um visitante individual do site. [!DNL Chatlio] usa a variável [!DNL Chatio Zapier App] para conectar [!DNL Chatlio] com mais de 2000 aplicativos e serviços diferentes.

O [!DNL Chatlio] A fonte permite assimilar esquemas de evento do webhook compatíveis e seus dados de evento associados a partir de [!DNL Chatlio.com] usando o [[!DNL Chatlio] Webhooks](https://chatlio.com/docs/webhooks/).

Os webhooks compatíveis são:

* Exportação de transcrições de chat
* Exportar mensagens offline
* Nova conversa foi iniciada
* O visitante não recebeu uma resposta a tempo
* O visitante deixou o feedback após o chat

## Pré-requisitos {#prerequisites}

Antes de criar um [!DNL Chatlio] conexão de origem, você deve primeiro garantir que tenha o seguinte:

* A [!DNL Chatlio] conta. Se você ainda não tiver um, visite o [[!DNL Chatlio] página de inscrição](https://chatlio.com/app/#/signup) para registrar-se e criar sua conta.
* Depois de registrar uma conta com êxito, siga as [[!DNL Chatlio] documentação de configuração](https://chatlio.com/docs/setup/) para concluir a configuração da sua conta.

### Configuração [!DNL Chatlio] webhook {#set-up-webhook}

Depois de criar seu fluxo de dados com sucesso, você deve configurar um webhook para informar a Platform sobre [!DNL Chatlio] eventos. Os Webhooks podem notificá-lo imediatamente quando os atributos do cliente mudarem ou quando as pessoas abrirem suas mensagens e enviarem essas informações para suas [!DNL Chatlio] fonte.

Para obter mais informações, leia os tutoriais em [obter o URL do terminal de transmissão](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md#get-streaming-endpoint) e [configurar um [!DNL Chatlio] Webhook](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md#set-up-webhook).

## Connect [!DNL Chatlio] para a plataforma {#connect-to-platform}

A documentação abaixo fornece informações sobre como criar um [!DNL Chatlio] conector de transmissão para conexão com [!DNL Platform] usando APIs ou a interface do usuário:

### Connect [!DNL Chatlio] para Plataforma usando APIs {#connect-to-platform-using-api}

* [Criar uma conexão de origem para trazer [!DNL Chatlio] dados para a Platform usando APIs.](../../tutorials/api/create/marketing-automation/chatlio-webhook.md)

### Connect [!DNL Chatlio] para Plataforma usando a interface do usuário {#connect-to-platform-using-ui}

* [Criar uma conexão de origem para trazer [!DNL Chatlio] dados para a Platform usando a interface do usuário](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md)
