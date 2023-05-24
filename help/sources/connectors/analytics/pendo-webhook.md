---
title: Visão geral da origem do Pendo
description: Saiba como conectar o Pendo ao Adobe Experience Platform usando APIs ou a interface do usuário utilizando webhooks
badge: Beta
last-substantial-update: 2023-03-29T00:00:00Z
exl-id: 376f18ef-1eea-4c42-8041-6fadb5906e9b
source-git-commit: 0cc4eab97dcd56d2b1d679cf5f35932976d22634
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# [!DNL Pendo]

>[!NOTE]
>
>A variável [!DNL Pendo] a fonte está na versão beta. Leia as [visão geral das origens](../../home.md#terms-and-conditions) para obter mais informações sobre o uso de fontes rotuladas como beta.

O Adobe Experience Platform permite que os dados sejam assimilados de fontes externas e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, bancos de dados e muitas outras.

O Experience Platform fornece suporte para assimilação de dados de aplicativos de análise de terceiros. O suporte para provedores de análise inclui [!DNL Pendo].

[[!DNL Pendo]](https://pendo.io/) O é um aplicativo de análise de produtos criado para ajudar empresas de software a desenvolver produtos que repercutem com os clientes. O aplicativo permite que os fabricantes de software incorporem seus produtos a uma grande variedade de ferramentas, o que pode resultar em uma melhor experiência do produto para os usuários e em novos insights para a equipe de produtos.

A variável [!DNL Pendo] A fonte de permite assimilar esquemas de evento de webhook compatíveis e seus dados de evento associados de [!DNL Pendo.io] usando o [[!DNL Pendo] Webhooks](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks). A variável [!DNL Pendo] a origem funciona com [!DNL Pendo] Webhooks de URL.

Os webhooks compatíveis são:

* [Guia](https://support.pendo.io/hc/en-us/articles/8146679315867-Creating-a-Guide) Exibido
* [Enquete](https://support.pendo.io/hc/en-us/articles/360031867152-Polls-Classic-) Exibido/Enviado
* [Pontuação líquida de promotor](https://support.pendo.io/hc/en-us/articles/360033527151-Set-up-an-NPS-Survey) Exibido/Enviado

## Pré-requisitos {#prerequisites}

Antes de criar um [!DNL Pendo] conexão de origem, você deve primeiro garantir que tenha o seguinte:

A [!DNL Pendo] conta. Se você ainda não tiver um, consulte o [[!DNL Pendo] registrar](https://app.pendo.io/register) página para registrar e criar sua conta.

### Configurar [!DNL Pendo] Webhook {#set-up-webhook}

Depois de criar o fluxo de dados com êxito, você deve configurar um webhook para informar a Platform sobre [!DNL Pendo] eventos. [!DNL Pendo] Os webhooks podem enviar notificações em tempo real para outros serviços quando determinados eventos ocorrem e enviar essas informações para o [!DNL Pendo] origem. Para obter mais informações, leia os tutoriais no [obter o URL do ponto de extremidade de streaming](../../tutorials/ui/create/analytics/pendo-webhook.md#get-streaming-endpoint) e [configurar um [!DNL Pendo] Webhook](../../tutorials/ui/create/analytics/pendo-webhook.md#set-up-webhook).

## Conectando [!DNL Pendo] para a Platform {#connect-to-platform}

A documentação abaixo fornece informações sobre como criar um [!DNL Pendo] conector de transmissão para conexão com o [!DNL Platform] uso de APIs ou da interface do usuário:

### Conectar [!DNL Pendo] para a Platform usando APIs {#connect-to-platform-using-api}

* [Crie uma conexão de origem para trazer [!DNL Pendo] para a Platform usando APIs.](../../tutorials/api/create/analytics/pendo-webhook.md)

### Conectar [!DNL Pendo] para a Platform usando a interface {#connect-to-platform-using-ui}

* [Crie uma conexão de origem para trazer [!DNL Pendo] dados para a Platform usando a interface do usuário](../../tutorials/ui/create/analytics/pendo-webhook.md)
