---
title: Visão geral do Chatlio Source
description: Saiba como conectar o Chatlio ao Adobe Experience Platform usando APIs ou a interface do usuário utilizando webhooks
badge: Beta
exl-id: 4a71d1dc-e0eb-443e-a956-8caa0e82fa18
source-git-commit: 8de45a54607bed17fd79bbed693666beb09c0502
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 0%

---

# [!DNL Chatlio]

>[!NOTE]
>
>A origem [!DNL Chatlio] está na versão beta. Leia a [visão geral das fontes](../../home.md#terms-and-conditions) para obter mais informações sobre o uso de fontes com rótulo beta.

O Adobe Experience Platform permite que os dados sejam assimilados de fontes externas e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, bancos de dados e muitas outras.

O Experience Platform fornece suporte para assimilação de dados de aplicativos de transmissão. O suporte para provedores de streaming inclui [!DNL Chatlio].

[[!DNL Chatlio]](https://chatlio.com/) é um aplicativo de chat ao vivo totalmente integrado ao [!DNL Slack] e que facilita o uso de vários agentes de suporte para ajudar simultaneamente um visitante individual do site. [!DNL Chatlio] usa [!DNL Chatio Zapier App] para conectar [!DNL Chatlio] com mais de 2000 aplicativos e serviços diferentes.

A origem [!DNL Chatlio] permite assimilar esquemas de evento de webhook com suporte e seus dados de evento associados de [!DNL Chatlio.com] usando os [[!DNL Chatlio] Webhooks](https://chatlio.com/docs/webhooks/).

Os webhooks compatíveis são:

* Exportar transcrições do chat
* Exportar mensagens offline
* Nova conversa iniciada
* O visitante não recebeu uma resposta a tempo
* O visitante deixou o feedback após um chat

## Pré-requisitos {#prerequisites}

Antes de criar uma conexão de origem [!DNL Chatlio], primeiro verifique se você tem o seguinte:

* Uma conta [!DNL Chatlio]. Caso ainda não tenha uma, visite a [[!DNL Chatlio] página de inscrição](https://chatlio.com/app/#/signup) para registrar-se e criar sua conta.
* Depois de registrar uma conta com êxito, siga a [[!DNL Chatlio] documentação de configuração](https://chatlio.com/docs/setup/) para concluir a configuração da conta.

### Configurar webhook [!DNL Chatlio] {#set-up-webhook}

Depois de criar o fluxo de dados com êxito, você deve configurar um webhook para informar à Plataforma sobre eventos [!DNL Chatlio]. Os webhooks podem notificá-lo imediatamente quando os atributos do cliente forem alterados ou quando as pessoas abrirem suas mensagens e enviarem essas informações para sua origem [!DNL Chatlio].

Para obter mais informações, leia os tutoriais em [obtendo a URL do ponto de extremidade de streaming](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md#get-streaming-endpoint) e [configurando um [!DNL Chatlio] Webhook](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md#set-up-webhook).

## Conectar [!DNL Chatlio] à plataforma {#connect-to-platform}

A documentação abaixo fornece informações sobre como criar um conector de streaming [!DNL Chatlio] para se conectar ao [!DNL Platform] usando APIs ou a interface do usuário:

### Conectar [!DNL Chatlio] à plataforma usando APIs {#connect-to-platform-using-api}

* [Crie uma conexão de origem para trazer dados do  [!DNL Chatlio]  para a Platform usando APIs.](../../tutorials/api/create/marketing-automation/chatlio-webhook.md)

### Conectar [!DNL Chatlio] à Plataforma usando a interface {#connect-to-platform-using-ui}

* [Criar uma conexão de origem para trazer dados do  [!DNL Chatlio]  para a Platform usando a interface do usuário](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md)
