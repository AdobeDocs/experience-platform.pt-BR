---
title: Notas de versão para tags e encaminhamento de eventos
description: As notas de versão mais recentes para tags e encaminhamento de eventos na Adobe Experience Platform.
exl-id: 2ebeaa1e-64b8-48fd-b4e8-419663271a87
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 87%

---

# Notas de versão para tags e encaminhamento de eventos

>[!IMPORTANT]
>
>A partir de agora, as notas de versão para tags e encaminhamento de eventos não serão mais fornecidas nesta página. Consulte as mais recentes [notas de versão da Adobe Experience Platform](/help/release-notes/latest/latest.md) para obter as atualizações detalhadas das tags e do encaminhamento de eventos.

## 26 de abril de 2023

* **Segredo JWT do OAuth**: o [segredo JWT do OAuth](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html?lang=pt-br) permite que clientes usem tokens de serviço da Adobe e do Google para possibilitar interações de servidor para servidor no encaminhamento de eventos.

Lançamento da nova extensão a seguir:

* Extensão da **[!DNL Pinterest Conversions API]**: a extensão de encaminhamento de eventos da [[!DNL Pinterest Conversions API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/pinterest/overview.html?lang=pt-BR) permite aproveitar os dados capturados na Adobe Experience Platform Edge Network e enviá-los para o [!DNL Pinterest] na forma de eventos do lado do servidor usando a [!DNL Pinterest Conversions API].

## 29 de março de 2023

**Fluxos de trabalho de início rápido (Beta)**

Acesse os novos fluxos de trabalho de início rápido na seção de “Introdução” da página inicial da Coleção de dados. Os fluxos de trabalho a seguir agora estão disponíveis para clientes como um Beta público.

* **[API de conversões da Meta](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/meta/overview.html?lang=pt-br#quick-start)**: clientes que encaminham eventos podem coletar e encaminhar dados de eventos do lado do servidor para a Meta rapidamente, a fim de realizar conversões de anúncios em apenas algumas etapas simples.
* **[SDK móvel](https://developer.adobe.com/client-sdks/documentation/)**: clientes podem implementar rapidamente o SDK móvel e validar eventos móveis básicos em apenas algumas etapas simples.

Lançamento de novas extensões:

* Extensão de encaminhamento de eventos da **[!DNL Braze]**: a extensão de encaminhamento de eventos da [[!DNL Braze Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html?lang=pt-br) permite aproveitar os dados capturados na Adobe Experience Platform Edge Network e enviá-los para o [!DNL Braze] na forma de eventos do lado do servidor usando as APIs de rastreamento de usuário do [!DNL Braze].
* Extensão de encaminhamento de eventos da **[API Epsilon Events]**: a extensão da [[!DNL Epsilon Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html?lang=pt-br) permite aproveitar o encaminhamento de eventos para capturar informações de eventos na Adobe Experience Platform Edge Network e enviá-las para a [!DNL Epsilon] usando a API [!DNL Epsilon] Event.
* Extensão de encaminhamento de eventos do **[!DNL Mixpanel]**: a extensão da [[!DNL Mixpanel Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html?lang=pt-br) permite aproveitar o encaminhamento de eventos para capturar informações de eventos na Adobe Experience Platform Edge Network e enviá-las para a [!DNL Mixpanel] usando a API de rastreamento de eventos.

## 25 de janeiro de 2023

* **Nova página inicial**: atualização da página inicial da interface da Coleção de dados para incluir informações de integração úteis e links para simplificar a produtividade. Isso inclui:
   1. Documentação e fluxos de trabalho recomendados para começar
   1. Propriedades, regras e elementos de dados recentes
   1. Extensões populares
   1. Novas atualizações de extensão com recurso de instalação rápida
* **Enviar dados para o [!DNL Google Ads] usando o encaminhamento de eventos**: agora é possível usar a extensão da API [[!DNL Google Ads Enhanced Conversions] &#x200B;](../extensions/server/google-ads-enhanced-conversions/overview.md) para encaminhamento de eventos juntamente com os [segredos do Google Oauth 2](../ui/event-forwarding/secrets.md#google-oauth2) para enviar dados do lado do servidor para o [!DNL Google Ads] em tempo real e com segurança.

## 23 de novembro de 2022

* Extensão do **[!DNL AWS]para encaminhamento de eventos**: agora é possível enviar dados para o [!DNL Amazon Web Services] ([!DNL AWS]) usando uma extensão de [encaminhamento de eventos](../../tags/ui/event-forwarding/overview.md). Consulte a [[!DNL AWS] Visão geral de extensões](../../tags/extensions/server/aws/overview.md) para obter mais informações.
* Extensão de **[!DNL Google Ads Enhanced Conversions]para encaminhamento de eventos**: agora é possível enviar dados de conversão para o [!DNL Google Ads] usando uma extensão de [encaminhamento de eventos](../../tags/ui/event-forwarding/overview.md). Consulte a [[!DNL Google Ads Enhanced Conversions] Visão geral de extensões](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md) para obter mais informações.
* Extensão do **[!DNL Microsoft Azure]para encaminhamento de eventos**: agora é possível enviar dados para o [!DNL Microsoft Azure] usando uma extensão de [encaminhamento de eventos](../../tags/ui/event-forwarding/overview.md). Consulte a [[!DNL Microsoft Azure] Visão geral de extensões](../../tags/extensions/server/azure/overview.md) para obter mais informações.

## 26 de outubro de 2022

* **Manipulação de dados confidenciais para sequências de dados**: as sequências de dados agora usam várias tecnologias da Experience Platform para manipular adequadamente dados confidenciais conforme aplicado por regulamentações, como a HIPAA (Lei de Portabilidade e Responsabilidade do Seguro de Saúde). Consulte a seção sobre [manipulação de dados sensíveis em sequências de dados](../../datastreams/overview.md#sensitive) para obter mais informações.
* Extensão do **[!DNL Splunk]para encaminhamento de eventos**: agora é possível enviar dados para o [!DNL Splunk] usando uma extensão de [encaminhamento de eventos](../ui/event-forwarding/overview.md). Consulte a [[!DNL Splunk] Visão geral de extensões](../extensions/server/splunk/overview.md) para obter mais informações.
* Extensão do **[!DNL Zendesk]para encaminhamento de eventos**: agora é possível enviar dados para o [!DNL Zendesk] usando uma extensão de [encaminhamento de eventos](../ui/event-forwarding/overview.md). Consulte a [[!DNL Zendesk] Visão geral de extensões](../extensions/server/zendesk/overview.md) para obter mais informações.

## 28 de setembro de 2022

* **Integração com a navegação à esquerda do Adobe Experience Platform**: todos os recursos que antes eram exclusivos da interface da Coleção de Dados (incluindo marcas e encaminhamento de eventos) agora também estão disponíveis através da navegação à esquerda na interface da Experience Platform, na categoria **[!UICONTROL Data Collection]**. Isso elimina a necessidade de alternar entre interfaces do usuário ao trabalhar com recursos de coleta de dados no Experience Platform.
* **Atribuição de usuário em tags e encaminhamento de eventos**: ao listar propriedades disponíveis em tags e no encaminhamento de eventos, cada propriedade listada agora mostra quando foi atualizada pela última vez e por quem.
* Extensão da **[[!DNL Snap Conversions API] &#x200B;](https://exchange.adobe.com/apps/ec/108550) para encaminhamento de eventos**: agora é possível enviar dados para a [!DNL Snapchat Conversions API] usando uma extensão de [encaminhamento de eventos](../../tags/ui/event-forwarding/overview.md). Para obter mais informações sobre como autenticar e usar a API, consulte a [[!DNL Snapchat Marketing API] documentação](https://marketingapi.snapchat.com/docs/conversion.html).

## 27 de julho de 2022

* O acesso aos recursos de tags e encaminhamento de eventos agora é gerenciado por meio do Adobe Admin Console no cartão da Coleção de dados da Adobe Experience Platform. Consulte o guia sobre [permissões da coleção de dados](../../collection/permissions.md) para obter mais informações.
* O suporte para o Internet Explorer 10 e 11 foi descontinuado.

## 22 de junho de 2022

Lançamento de novas extensões:

* [Extensão de tag da camada de dados do Google](../extensions/client/google-data-layer/overview.md): permite usar uma camada de dados do Google na implementação de tags.
* [Extensão de encaminhamento de eventos para conversões aprimoradas do Google Ads](https://partners.adobe.com/exchangeprogram/experiencecloud/exchange.details.108630.html): permite aprimorar as conversões do Google Ads em tempo real.
* [Extensão de encaminhamento de eventos do Mailchimp](../extensions/server/mailchimp/overview.md): envia eventos para a API de marketing do Mailchimp, que pode acionar emails para campanhas de marketing, jornadas ou transações do Mailchimp.