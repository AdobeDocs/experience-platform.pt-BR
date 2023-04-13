---
title: Visão geral da origem de pendo
description: Saiba como conectar o Pendo ao Adobe Experience Platform usando APIs ou a interface do usuário, aproveitando webhooks
badge: Beta
last-substantial-update: 2023-03-29T00:00:00Z
exl-id: 376f18ef-1eea-4c42-8041-6fadb5906e9b
source-git-commit: 0cc4eab97dcd56d2b1d679cf5f35932976d22634
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# [!DNL Pendo]

>[!NOTE]
>
>O [!DNL Pendo] A fonte está em beta. Leia o [visão geral das fontes](../../home.md#terms-and-conditions) para obter mais informações sobre o uso de fontes com rótulo beta.

O Adobe Experience Platform permite que os dados sejam assimilados de fontes externas e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, bancos de dados e muitas outras.

O Experience Platform oferece suporte para assimilar dados de aplicativos de análises de terceiros. O suporte para provedores de análise inclui [!DNL Pendo].

[[!DNL Pendo]](https://pendo.io/) O é um aplicativo de análise de produto criado para ajudar empresas de software a desenvolver produtos que ressoem com os clientes. O aplicativo permite que os fabricantes de software incorporem seus produtos a uma grande variedade de ferramentas que podem levar a uma melhor experiência de produto para os usuários e a novos insights para a equipe de produtos.

O [!DNL Pendo] A fonte permite assimilar esquemas de evento do webhook compatíveis e seus dados de evento associados a partir de [!DNL Pendo.io] usando o [[!DNL Pendo] Webhooks](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks). O [!DNL Pendo] O código-fonte funciona com [!DNL Pendo] Webhooks do URL.

Os webhooks compatíveis são:

* [Guia](https://support.pendo.io/hc/en-us/articles/8146679315867-Creating-a-Guide) Exibido
* [Pesquisa](https://support.pendo.io/hc/en-us/articles/360031867152-Polls-Classic-) Exibido/Enviado
* [Pontuação de promoção de rede](https://support.pendo.io/hc/en-us/articles/360033527151-Set-up-an-NPS-Survey) Exibido/Enviado

## Pré-requisitos {#prerequisites}

Antes de criar um [!DNL Pendo] conexão de origem, você deve primeiro garantir que tenha o seguinte:

A [!DNL Pendo] conta. Se você não tiver um já visualize o [[!DNL Pendo] registrar](https://app.pendo.io/register) para registrar e criar sua conta.

### Configurar [!DNL Pendo] Webhook {#set-up-webhook}

Depois de criar seu fluxo de dados com sucesso, você deve configurar um webhook para informar a Platform sobre [!DNL Pendo] eventos. [!DNL Pendo] Os Webhooks podem enviar notificações em tempo real a outros serviços quando eventos específicos ocorrem e enviar essas informações para seus [!DNL Pendo] fonte. Para obter mais informações, leia os tutoriais em [obter o URL do terminal de transmissão](../../tutorials/ui/create/analytics/pendo-webhook.md#get-streaming-endpoint) e [configurar um [!DNL Pendo] Webhook](../../tutorials/ui/create/analytics/pendo-webhook.md#set-up-webhook).

## Conexão [!DNL Pendo] para a plataforma {#connect-to-platform}

A documentação abaixo fornece informações sobre como criar um [!DNL Pendo] conector de transmissão para conexão com [!DNL Platform] usando APIs ou a interface do usuário:

### Connect [!DNL Pendo] para Plataforma usando APIs {#connect-to-platform-using-api}

* [Criar uma conexão de origem para trazer [!DNL Pendo] dados para a Platform usando APIs.](../../tutorials/api/create/analytics/pendo-webhook.md)

### Connect [!DNL Pendo] para Plataforma usando a interface do usuário {#connect-to-platform-using-ui}

* [Criar uma conexão de origem para trazer [!DNL Pendo] dados para a Platform usando a interface do usuário](../../tutorials/ui/create/analytics/pendo-webhook.md)
