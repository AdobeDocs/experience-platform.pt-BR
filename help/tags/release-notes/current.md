---
title: Notas de versão para Tags e Encaminhamento de eventos
description: As notas de versão mais recentes para tags e encaminhamento de eventos na Adobe Experience Platform.
exl-id: 2ebeaa1e-64b8-48fd-b4e8-419663271a87
source-git-commit: 3ebf8df16f88660eab481bd0a0ba88816b470255
workflow-type: tm+mt
source-wordcount: '720'
ht-degree: 4%

---

# Notas de versão para tags e encaminhamento de eventos

## 29 de março de 2023

**Fluxos de trabalho iniciais rápidos (Beta)**

Acesse novos fluxos de trabalho de início rápido em &quot;Introdução&quot; na tela inicial da Coleta de dados! Os workflows a seguir agora estão disponíveis para clientes como uma versão beta pública.
* **[API Meta conversões](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/meta/overview.html?lang=en#quick-start)**: Os clientes do Encaminhamento de eventos podem coletar e encaminhar rapidamente os dados do evento, do lado do servidor para o Meta para conversões de anúncios em apenas algumas etapas simples.
* **[SDK móvel](https://developer.adobe.com/client-sdks/documentation/)**: Os clientes podem implementar rapidamente o SDK móvel e validar eventos móveis básicos em apenas algumas etapas simples.

Novas extensões foram lançadas:

* **[!DNL Braze]extensão de encaminhamento de eventos**: O [[!DNL Braze Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) a extensão de encaminhamento de eventos permite aproveitar os dados capturados na Rede de borda do Adobe Experience Platform e enviá-los para [!DNL Braze] na forma de eventos do lado do servidor usando o [!DNL Braze] APIs de rastreamento de usuário.
* **[API de Eventos Epsilon] extensão de encaminhamento de eventos**: O [[!DNL Epsilon Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) A extensão permite aproveitar o encaminhamento do evento para capturar informações do evento na Rede de borda do Adobe Experience Platform e enviá-las para [!DNL Epsilon] usando o [!DNL Epsilon] API de evento.
* **[!DNL Mixpanel]extensão de encaminhamento de eventos**: O [[!DNL Mixpanel Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) A extensão permite aproveitar o encaminhamento do evento para capturar informações do evento na Rede de borda do Adobe Experience Platform e enviá-las para [!DNL Mixpanel] usando a API de eventos de rastreamento.

## 25 de janeiro de 2023

* **Nova tela inicial**: A página inicial da interface do usuário da coleta de dados foi atualizada para incluir informações úteis sobre integração e links para simplificar a produtividade. Isso inclui:
   1. Documentação e fluxos de trabalho recomendados para começar
   1. Propriedades, regras e elementos de dados recentes
   1. Extensões populares
   1. Novas atualizações de extensão com um recurso de instalação rápida
* **Enviar dados para [!DNL Google Ads] uso do encaminhamento de eventos**: Agora você pode usar o [[!DNL Google Ads Enhanced Conversions] Extensão da API](../extensions/server/google-ads-enhanced-conversions/overview.md) para encaminhamento de eventos, combinado com [Segredo do Google Oauth 2](../ui/event-forwarding/secrets.md#google-oauth2), para enviar dados do lado do servidor para o [!DNL Google Ads] em tempo real.

## 23 de novembro de 2022

* **[!DNL AWS]extensão para encaminhamento de eventos**: Agora é possível enviar dados para o [!DNL Amazon Web Services] ([!DNL AWS]) usando um [encaminhamento de eventos](../../tags/ui/event-forwarding/overview.md) extensão. Consulte a [[!DNL AWS] visão geral da extensão](../../tags/extensions/server/aws/overview.md) para obter mais informações.
* **[!DNL Google Ads Enhanced Conversions]extensão para encaminhamento de eventos**: Agora é possível enviar dados de conversão para [!DNL Google Ads] usando um [encaminhamento de eventos](../../tags/ui/event-forwarding/overview.md) extensão. Consulte a [[!DNL Google Ads Enhanced Conversions] visão geral da extensão](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md) para obter mais informações.
* **[!DNL Microsoft Azure]extensão para encaminhamento de eventos**: Agora é possível enviar dados para o [!DNL Microsoft Azure] usando um [encaminhamento de eventos](../../tags/ui/event-forwarding/overview.md) extensão. Consulte a [[!DNL Microsoft Azure] visão geral da extensão](../../tags/extensions/server/azure/overview.md) para obter mais informações.

## 26 de outubro de 2022

* **Tratamento de dados confidenciais para conjuntos de dados**: Os datastreams agora usam várias tecnologias da plataforma para lidar adequadamente com dados confidenciais, conforme empregado por regulamentos, como o Health Insurance Portability and Accountability Act (HIPAA). Consulte a seção sobre [tratamento de dados confidenciais em fluxos de dados](../../edge/datastreams/overview.md#sensitive) para obter mais informações.
* **[!DNL Splunk]extensão para encaminhamento de eventos**: Agora é possível enviar dados para o [!DNL Splunk] usando um [encaminhamento de eventos](../ui/event-forwarding/overview.md) extensão. Consulte a [[!DNL Splunk] visão geral da extensão](../extensions/server/splunk/overview.md) para obter mais informações.
* **[!DNL Zendesk]extensão para encaminhamento de eventos**: Agora é possível enviar dados para o [!DNL Zendesk] usando um [encaminhamento de eventos](../ui/event-forwarding/overview.md) extensão. Consulte a [[!DNL Zendesk] visão geral da extensão](../extensions/server/zendesk/overview.md) para obter mais informações.

## 28 de setembro de 2022

* **Integração de navegação esquerda do Adobe Experience Platform**: Todos os recursos que antes eram exclusivos da interface do usuário da coleta de dados (incluindo tags e encaminhamento de eventos) agora também estão disponíveis na navegação à esquerda na interface do usuário do Experience Platform, na categoria **[!UICONTROL Coleta de dados]**. Isso elimina a necessidade de alternar entre interfaces do usuário ao trabalhar com recursos de coleta de dados na Plataforma.
* **Atribuição de usuário em tags e encaminhamento de evento**: Ao listar as propriedades disponíveis nas tags e no encaminhamento de eventos, cada propriedade listada agora mostra quando foi atualizada pela última vez e por quem.
* **[[!DNL Snap Conversions API] extensão](https://exchange.adobe.com/apps/ec/108550) para encaminhamento de eventos**: Agora é possível enviar dados para a [!DNL Snapchat Conversions API] usando um [encaminhamento de eventos](../../tags/ui/event-forwarding/overview.md) extensão. Para obter mais informações sobre como autenticar e usar a API, consulte o [[!DNL Snapchat Marketing API] documentação](https://marketingapi.snapchat.com/docs/conversion.html).

## 27 de julho de 2022

* O acesso a tags e recursos de encaminhamento de eventos agora é gerenciado pelo Adobe Admin Console no cartão da Coleta de dados do Adobe Experience Platform. Consulte o guia sobre [permissões de coleta de dados](../../collection/permissions.md) para obter mais informações.
* O suporte para Internet Explorer 10 e 11 foi [obsoleto](../ie-deprecation.md).

## 22 de junho de 2022

Novas extensões foram lançadas:

* [Extensão de tag da Camada de dados Google](../extensions/client/google-data-layer/overview.md): Permite usar uma camada de dados do Google na implementação de tags.
* [Extensão de encaminhamento de eventos de Conversões aprimoradas do Google Ads](https://partners.adobe.com/exchangeprogram/experiencecloud/exchange.details.108630.html): Permite que você aprimore suas conversões do Google Ads em tempo real.
* [Extensão de encaminhamento de evento de mailchimp](../extensions/server/mailchimp/overview.md): Envia eventos para a API de marketing Mailchimp, que pode acionar emails para campanhas de marketing, jornadas ou transações de Mailchimp.