---
title: Notas de versão para tags e encaminhamento de eventos
description: As notas de versão mais recentes para tags e encaminhamento de eventos na Adobe Experience Platform.
exl-id: 2ebeaa1e-64b8-48fd-b4e8-419663271a87
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '835'
ht-degree: 12%

---

# Notas de versão de tags e encaminhamento de eventos

>[!IMPORTANT]
>
>A movimentação das tags e das notas de versão do encaminhamento de eventos não será mais fornecida nesta página. Consulte a versão mais recente [Notas de versão do Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/release-notes/latest.html#data-collection) para obter tags detalhadas e atualizações de encaminhamento de eventos.

## 26 de abril de 2023

* **Segredo JWT do OAuth**: A variável [Segredo JWT do OAuth](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html) O permite que os clientes usem os tokens de serviço do Adobe e do Google para oferecer suporte às interações servidor a servidor no encaminhamento de eventos.

A nova extensão a seguir foi lançada:

* **[!DNL Pinterest Conversions API]extensão**: A variável [[!DNL Pinterest Conversions API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/pinterest/overview.html?lang=pt-BR) a extensão de encaminhamento de eventos permite aproveitar os dados capturados na rede de borda da Adobe Experience Platform e enviá-los para o [!DNL Pinterest] na forma de eventos do lado do servidor usando o [!DNL Pinterest Conversions API].

## 29 de março de 2023

**Fluxos de trabalho rápidos do Stark (Beta)**

Acesse os novos fluxos de trabalho de início rápido na seção de “Introdução” da página inicial da Coleção de dados. Os workflows a seguir agora estão disponíveis para clientes como um Beta público.
* **[API de meta conversões](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/meta/overview.html#quick-start)**: os clientes do encaminhamento de eventos podem coletar e encaminhar rapidamente os dados do evento, do lado do servidor para o Meta, para conversões de anúncios em apenas algumas etapas simples.
* **[SDK móvel](https://developer.adobe.com/client-sdks/documentation/)**: os clientes podem implementar rapidamente o SDK móvel e validar eventos móveis básicos em apenas algumas etapas simples.

Novas extensões foram lançadas:

* **[!DNL Braze]extensão de encaminhamento de eventos**: A variável [[!DNL Braze Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html?lang=pt-BR) A extensão de encaminhamento de eventos permite aproveitar os dados capturados na Rede de borda da Adobe Experience Platform e enviá-los para o [!DNL Braze] na forma de eventos do lado do servidor usando o [!DNL Braze] APIs de rastreamento de usuários.
* **[API de eventos Epsilon] extensão de encaminhamento de eventos**: A variável [[!DNL Epsilon Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html?lang=pt-BR) A extensão do permite aproveitar o encaminhamento de eventos para capturar informações de eventos na Adobe Experience Platform Edge Network e enviá-las para o [!DNL Epsilon] usando o [!DNL Epsilon] API de evento.
* **[!DNL Mixpanel]extensão de encaminhamento de eventos**: A variável [[!DNL Mixpanel Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html?lang=pt-BR) A extensão do permite aproveitar o encaminhamento de eventos para capturar informações de eventos na Adobe Experience Platform Edge Network e enviá-las para o [!DNL Mixpanel] usando a API Rastrear eventos.

## 25 de janeiro de 2023

* **Nova tela inicial**: a home page da interface da Coleção de dados foi atualizada para incluir informações de integração úteis e links para simplificar a produtividade. Isso inclui:
   1. Documentação e fluxos de trabalho recomendados para começar
   1. Propriedades, regras e elementos de dados recentes
   1. Extensões populares
   1. Novas atualizações de extensão com recurso de instalação rápida
* **Enviar dados para [!DNL Google Ads] usar o encaminhamento de eventos**: Agora você pode usar o [[!DNL Google Ads Enhanced Conversions] Extensão da API](../extensions/server/google-ads-enhanced-conversions/overview.md) para encaminhamento de eventos, combinado com [Segredos do Google Oauth 2](../ui/event-forwarding/secrets.md#google-oauth2), para enviar com segurança os dados do lado do servidor para o [!DNL Google Ads] em tempo real.

## 23 de novembro de 2022

* **[!DNL AWS]extensão para encaminhamento de eventos**: Agora você pode enviar dados para o [!DNL Amazon Web Services] ([!DNL AWS]) usando um [encaminhamento de eventos](../../tags/ui/event-forwarding/overview.md) extensão. Consulte a [[!DNL AWS] visão geral da extensão](../../tags/extensions/server/aws/overview.md) para obter mais informações.
* **[!DNL Google Ads Enhanced Conversions]extensão para encaminhamento de eventos**: Agora você pode enviar dados de conversão para o [!DNL Google Ads] usando um [encaminhamento de eventos](../../tags/ui/event-forwarding/overview.md) extensão. Consulte a [[!DNL Google Ads Enhanced Conversions] visão geral da extensão](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md) para obter mais informações.
* **[!DNL Microsoft Azure]extensão para encaminhamento de eventos**: Agora você pode enviar dados para o [!DNL Microsoft Azure] usando um [encaminhamento de eventos](../../tags/ui/event-forwarding/overview.md) extensão. Consulte a [[!DNL Microsoft Azure] visão geral da extensão](../../tags/extensions/server/azure/overview.md) para obter mais informações.

## 26 de outubro de 2022

* **Manuseio de dados confidenciais para fluxos de dados**: as sequências de dados agora usam várias tecnologias da Platform para lidar adequadamente com dados confidenciais, conforme aplicado por regulamentações como a HIPAA (Health Insurance Portability and Accountability Act, Lei de Portabilidade e Responsabilidade do Seguro de Saúde). Consulte a seção sobre [tratamento de dados confidenciais em fluxos de dados](../../datastreams/overview.md#sensitive) para obter mais informações.
* **[!DNL Splunk]extensão para encaminhamento de eventos**: Agora você pode enviar dados para o [!DNL Splunk] usando um [encaminhamento de eventos](../ui/event-forwarding/overview.md) extensão. Consulte a [[!DNL Splunk] visão geral da extensão](../extensions/server/splunk/overview.md) para obter mais informações.
* **[!DNL Zendesk]extensão para encaminhamento de eventos**: Agora você pode enviar dados para o [!DNL Zendesk] usando um [encaminhamento de eventos](../ui/event-forwarding/overview.md) extensão. Consulte a [[!DNL Zendesk] visão geral da extensão](../extensions/server/zendesk/overview.md) para obter mais informações.

## 28 de setembro de 2022

* **Integração de navegação à esquerda do Adobe Experience Platform**: todos os recursos que antes eram exclusivos da interface da Coleção de dados (incluindo tags e encaminhamento de eventos) agora também estão disponíveis por meio da navegação à esquerda na interface do Experience Platform, na categoria **[!UICONTROL Coleta de dados]**. Isso elimina a necessidade de alternar entre as interfaces do usuário ao trabalhar com recursos de coleção de dados na Platform.
* **Atribuição de usuário em tags e encaminhamento de eventos**: ao listar propriedades disponíveis em tags e no encaminhamento de eventos, cada propriedade listada agora mostra quando foi atualizada pela última vez e por quem.
* **[[!DNL Snap Conversions API] extensão](https://exchange.adobe.com/apps/ec/108550) para encaminhamento de eventos**: Agora você pode enviar dados para o [!DNL Snapchat Conversions API] usando um [encaminhamento de eventos](../../tags/ui/event-forwarding/overview.md) extensão. Para obter mais informações sobre como autenticar e usar a API, consulte o [[!DNL Snapchat Marketing API] documentação](https://marketingapi.snapchat.com/docs/conversion.html).

## 27 de julho de 2022

* O acesso a tags e recursos de encaminhamento de eventos agora é gerenciado por meio da Adobe Admin Console no cartão da Coleção de dados da Adobe Experience Platform. Consulte o guia sobre [permissões de coleção de dados](../../collection/permissions.md) para obter mais informações.
* O suporte para o Internet Explorer 10 e 11 foi [obsoleto](../ie-deprecation.md).

## 22 de junho de 2022

Novas extensões foram lançadas:

* [Extensão de tag da Camada de dados do Google](../extensions/client/google-data-layer/overview.md): permite usar uma camada de dados do Google na implementação de tags.
* [Extensão de encaminhamento de eventos de Conversões aprimoradas do Google Ads](https://partners.adobe.com/br/exchangeprogram/experiencecloud/exchange.details.108630.html): permite aprimorar as conversões de anúncios do Google em tempo real.
* [Extensão de encaminhamento de eventos do Mailchimp](../extensions/server/mailchimp/overview.md): envia eventos para a API de marketing do Mailchimp, que pode acionar emails para campanhas de marketing, jornadas ou transações do Mailchimp.