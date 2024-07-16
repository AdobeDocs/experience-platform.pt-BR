---
title: Notas de versão para tags e encaminhamento de eventos
description: As notas de versão mais recentes para tags e encaminhamento de eventos na Adobe Experience Platform.
exl-id: 2ebeaa1e-64b8-48fd-b4e8-419663271a87
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 7%

---

# Notas de versão de tags e encaminhamento de eventos

>[!IMPORTANT]
>
>A movimentação das tags e das notas de versão do encaminhamento de eventos não será mais fornecida nesta página. Consulte as [notas de versão do Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/release-notes/latest.html#data-collection) mais recentes para obter as atualizações detalhadas das tags e do encaminhamento de eventos.

## 26 de abril de 2023

* **Segredo JWT do OAuth**: o [Segredo JWT do OAuth](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html) permite que os clientes usem tokens do Adobe e do Google Service para oferecer suporte às interações entre servidores no Encaminhamento de Eventos.

A nova extensão a seguir foi lançada:

* **[!DNL Pinterest Conversions API]extensão**: a extensão de encaminhamento de eventos [[!DNL Pinterest Conversions API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/pinterest/overview.html?lang=pt-BR) permite que você aproveite os dados capturados no Edge Network do Adobe Experience Platform e os envie para [!DNL Pinterest] na forma de eventos do lado do servidor usando o [!DNL Pinterest Conversions API].

## 29 de março de 2023

**Fluxos de Trabalho Rápidos Stark (Beta)**

Acesse os novos fluxos de trabalho de início rápido na seção de “Introdução” da página inicial da Coleção de dados. Os workflows a seguir agora estão disponíveis para clientes como um Beta público.
* **[API de Meta Conversões](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/meta/overview.html#quick-start)**: os clientes do Encaminhamento de Eventos podem coletar e encaminhar rapidamente dados do evento, do lado do servidor para Meta, para conversões de anúncios em apenas algumas etapas simples.
* **[SDK móvel](https://developer.adobe.com/client-sdks/documentation/)**: os clientes podem implementar rapidamente o SDK móvel e validar eventos móveis básicos em apenas algumas etapas simples.

Novas extensões foram lançadas:

* Extensão de encaminhamento de eventos do **[!DNL Braze]**: a extensão de encaminhamento de eventos do [[!DNL Braze Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html?lang=pt-BR) permite que você aproveite os dados capturados no Edge Network Adobe Experience Platform e os envie para o [!DNL Braze] na forma de eventos do lado do servidor usando as APIs de rastreamento de usuários do [!DNL Braze].
* **[Extensão de encaminhamento de eventos da API de Eventos Epsilon]**: a extensão [[!DNL Epsilon Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html?lang=pt-BR) permite aproveitar o encaminhamento de eventos para capturar informações de eventos no Edge Network Adobe Experience Platform e enviá-las para [!DNL Epsilon] usando a API de Eventos [!DNL Epsilon].
* **[!DNL Mixpanel]extensão de encaminhamento de eventos**: a extensão [[!DNL Mixpanel Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html?lang=pt-BR) permite que você aproveite o encaminhamento de eventos para capturar informações de eventos no Edge Network Adobe Experience Platform e enviá-las para [!DNL Mixpanel] usando a API de Eventos de Rastreamento.

## 25 de janeiro de 2023

* **Nova tela inicial**: a página inicial da interface da Coleção de dados foi atualizada para incluir informações de integração úteis e links para simplificar a produtividade. Isso inclui:
   1. Documentação e fluxos de trabalho recomendados para começar
   1. Propriedades, regras e elementos de dados recentes
   1. Extensões populares
   1. Novas atualizações de extensão com recurso de instalação rápida
* **Enviar dados para [!DNL Google Ads] usando o encaminhamento de eventos**: Agora você pode usar a [[!DNL Google Ads Enhanced Conversions] extensão de API](../extensions/server/google-ads-enhanced-conversions/overview.md) para o encaminhamento de eventos, combinada com os [segredos do Google Oauth 2](../ui/event-forwarding/secrets.md#google-oauth2), para enviar com segurança os dados do lado do servidor para [!DNL Google Ads] em tempo real.

## quinta-feira, 23 de novembro de 2022

* Extensão **[!DNL AWS]para encaminhamento de eventos**: agora é possível enviar dados para [!DNL Amazon Web Services] ([!DNL AWS]) usando uma extensão [encaminhamento de eventos](../../tags/ui/event-forwarding/overview.md). Consulte a [[!DNL AWS] visão geral da extensão](../../tags/extensions/server/aws/overview.md) para obter mais informações.
* Extensão **[!DNL Google Ads Enhanced Conversions]para encaminhamento de eventos**: agora é possível enviar dados de conversão para [!DNL Google Ads] usando uma extensão [encaminhamento de eventos](../../tags/ui/event-forwarding/overview.md). Consulte a [[!DNL Google Ads Enhanced Conversions] visão geral da extensão](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md) para obter mais informações.
* Extensão **[!DNL Microsoft Azure]para encaminhamento de eventos**: agora é possível enviar dados para [!DNL Microsoft Azure] usando uma extensão [encaminhamento de eventos](../../tags/ui/event-forwarding/overview.md). Consulte a [[!DNL Microsoft Azure] visão geral da extensão](../../tags/extensions/server/azure/overview.md) para obter mais informações.

## 26 de outubro de 2022

* **Manipulação de dados confidenciais para sequências de dados**: as sequências de dados agora usam várias tecnologias da Platform para manipular adequadamente dados confidenciais conforme aplicado por regulamentações, como a HIPAA (Lei de Portabilidade e Responsabilidade do Seguro de Saúde). Consulte a seção sobre [manipulação de dados confidenciais em fluxos de dados](../../datastreams/overview.md#sensitive) para obter mais informações.
* Extensão **[!DNL Splunk]para encaminhamento de eventos**: agora é possível enviar dados para [!DNL Splunk] usando uma extensão [encaminhamento de eventos](../ui/event-forwarding/overview.md). Consulte a [[!DNL Splunk] visão geral da extensão](../extensions/server/splunk/overview.md) para obter mais informações.
* Extensão **[!DNL Zendesk]para encaminhamento de eventos**: agora é possível enviar dados para [!DNL Zendesk] usando uma extensão [encaminhamento de eventos](../ui/event-forwarding/overview.md). Consulte a [[!DNL Zendesk] visão geral da extensão](../extensions/server/zendesk/overview.md) para obter mais informações.

## 28 de setembro de 2022

* **Integração com a navegação à esquerda do Adobe Experience Platform**: todos os recursos anteriormente exclusivos da interface da Coleção de Dados (incluindo marcas e encaminhamento de eventos) agora também estão disponíveis por meio da navegação à esquerda na interface do Experience Platform, na categoria **[!UICONTROL Coleção de Dados]**. Isso elimina a necessidade de alternar entre as interfaces do usuário ao trabalhar com recursos de coleção de dados na Platform.
* **Atribuição de usuário em marcas e encaminhamento de eventos**: ao listar propriedades disponíveis em marcas e encaminhamento de eventos, cada propriedade listada agora mostra quando foi atualizada pela última vez e por quem.
* **[[!DNL Snap Conversions API] extensão](https://exchange.adobe.com/apps/ec/108550) para encaminhamento de eventos**: agora é possível enviar dados para o [!DNL Snapchat Conversions API] usando uma extensão [encaminhamento de eventos](../../tags/ui/event-forwarding/overview.md). Para obter mais informações sobre como autenticar e usar a API, consulte a [[!DNL Snapchat Marketing API] documentação](https://marketingapi.snapchat.com/docs/conversion.html).

## 27 de julho de 2022

* O acesso a tags e recursos de encaminhamento de eventos agora é gerenciado por meio da Adobe Admin Console no cartão da Coleção de dados da Adobe Experience Platform. Consulte o manual sobre [permissões de coleta de dados](../../collection/permissions.md) para obter mais informações.
* O suporte para o Internet Explorer 10 e 11 foi [descontinuado](../ie-deprecation.md).

## 22 de junho de 2022

Novas extensões foram lançadas:

* [Extensão de marca da Camada de Dados do Google](../extensions/client/google-data-layer/overview.md): permite usar uma camada de dados do Google na implementação de marcas.
* [Extensão de encaminhamento de eventos de Conversões aprimoradas do Google Ads](https://partners.adobe.com/exchangeprogram/experiencecloud/exchange.details.108630.html): permite aprimorar as conversões de anúncios do Google em tempo real.
* [Extensão de encaminhamento de eventos do Mailchimp](../extensions/server/mailchimp/overview.md): envia eventos para a API de marketing do Mailchimp, que pode disparar emails para campanhas de marketing, jornadas ou transações do Mailchimp.