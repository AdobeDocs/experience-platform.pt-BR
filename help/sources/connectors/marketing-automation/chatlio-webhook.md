---
title: Visão geral da origem do Chatlio
description: Saiba como conectar o Chatlio ao Adobe Experience Platform usando APIs ou a interface do usuário utilizando webhooks
exl-id: 4a71d1dc-e0eb-443e-a956-8caa0e82fa18
source-git-commit: 68c14d7b187075b4af6b019a8bd1ca2625beabde
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 0%

---

# [!DNL Chatlio]

O Adobe Experience Platform permite que os dados sejam assimilados de fontes externas e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, bancos de dados e muitas outras.

O Experience Platform fornece suporte para assimilação de dados de aplicativos de transmissão. O suporte para provedores de transmissão inclui [!DNL Chatlio].

[[!DNL Chatlio]](https://chatlio.com/) é um aplicativo de chat ao vivo totalmente integrado ao [!DNL Slack] e facilita que vários agentes de suporte ajudem simultaneamente um visitante individual do site. [!DNL Chatlio] usa o [!DNL Chatio Zapier App] para conectar [!DNL Chatlio] com mais de 2000 aplicativos e serviços diferentes.

A variável [!DNL Chatlio] A fonte de permite assimilar esquemas de evento de webhook compatíveis e seus dados de evento associados de [!DNL Chatlio.com] usando o [[!DNL Chatlio] Webhooks](https://chatlio.com/docs/webhooks/).

Os webhooks compatíveis são:

* Exportar transcrições do chat
* Exportar mensagens offline
* Nova conversa iniciada
* O visitante não recebeu uma resposta a tempo
* O visitante deixou o feedback após um chat

## Pré-requisitos {#prerequisites}

Antes de criar um [!DNL Chatlio] conexão de origem, você deve primeiro garantir que tenha o seguinte:

* A [!DNL Chatlio] conta. Se você ainda não tiver um, visite o [[!DNL Chatlio] página de inscrição](https://chatlio.com/app/#/signup) para registrar e criar sua conta.
* Depois de registrar uma conta com êxito, siga as instruções [[!DNL Chatlio] documentação de configuração](https://chatlio.com/docs/setup/) para concluir a configuração da sua conta.

### Configuração [!DNL Chatlio] webhook {#set-up-webhook}

Depois de criar o fluxo de dados com êxito, você deve configurar um webhook para informar a Platform sobre [!DNL Chatlio] eventos. Os webhooks podem notificá-lo imediatamente quando os atributos do cliente mudarem ou quando as pessoas abrirem suas mensagens e enviarem essas informações para o seu [!DNL Chatlio] origem.

Para obter mais informações, leia os tutoriais no [obter o URL do ponto de extremidade de streaming](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md#get-streaming-endpoint) e [configurar um [!DNL Chatlio] Webhook](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md#set-up-webhook).

## Conectar [!DNL Chatlio] para a Platform {#connect-to-platform}

A documentação abaixo fornece informações sobre como criar um [!DNL Chatlio] conector de transmissão para conexão com o [!DNL Platform] uso de APIs ou da interface do usuário:

### Conectar [!DNL Chatlio] para a Platform usando APIs {#connect-to-platform-using-api}

* [Crie uma conexão de origem para trazer [!DNL Chatlio] para a Platform usando APIs.](../../tutorials/api/create/marketing-automation/chatlio-webhook.md)

### Conectar [!DNL Chatlio] para a Platform usando a interface {#connect-to-platform-using-ui}

* [Crie uma conexão de origem para trazer [!DNL Chatlio] dados para a Platform usando a interface do usuário](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md)
