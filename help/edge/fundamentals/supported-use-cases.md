---
title: Casos de uso compatíveis com o SDK da Web da Adobe Experience Platform
description: Saiba quais casos de uso são compatíveis com o SDK da Web da Adobe Experience Platform.
keywords: web sdk; casos de uso
exl-id: e0643c2c-ceb3-4ea2-aafa-1e18e0c66453
source-git-commit: ed092b85d74eaa0fdc29f3a8d28f84fe81ccca17
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 18%

---

# Casos de uso suportados

Esta página lista os casos de uso compatíveis com o SDK da Web, com links para informações adicionais.

## Geral

| Caso de uso | Mais Informações |
| --- | --- |
| SDK único simplificado |  |
| Rede global de coleta de dados |  |
| Consentimento adquirido do curso |  |
| Colete o consentimento do cliente de acordo com vários padrões | <ul><li>[Suporte ao Adobe Consent 2.0](../../landing/governance-privacy-security/consent/adobe/overview.md)</li><li>[Suporte à TCF 2.0 do IAB](../../landing/governance-privacy-security/consent/iab/overview.md)</li><li>[Integre o SDK para enviar sinais de consentimento à rede de borda](../../landing/governance-privacy-security/consent/sdk.md)</li></ul> |
| Suporte à ECID | Para obter informações sobre como recuperar o ECID, consulte nossa documentação [aqui](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#first-party-identity) e [aqui](https://experienceleague.adobe.com/docs/experience-platform/edge/extension/accessing-the-ecid.html?lang=en#extension) |
| Coletar várias entidades |  |
| Suporte ao Gráfico de dispositivos (público/privado) | [Documentação](https://experienceleague.adobe.com/docs/analytics/components/cda/device-graph.html?lang=en) |
| Enviar dados para várias organizações na página | [Documentação](./interacting-with-multiple-properties.md) |
| Registros e relatórios detalhados de erros |  |
| Rastrear solicitações do lado do cliente e do lado do servidor |  |
| extensão de tag | [Documentos de extensão do SDK da Web](../../tags/extensions/web/sdk/overview.md) |
| Ferramentas de depuração disponíveis | [Extensão do Debugger ](https://experienceleague.adobe.com/docs/debugger-learn/tutorials/experience-platform-debugger/introduction-to-the-experience-platform-debugger.html?lang=en) e  [Griffon](https://aep-sdks.gitbook.io/docs/beta/project-griffon) |

{style=&quot;table-layout:auto&quot;}

## Adobe Experience Platform

| Caso de uso | Mais Informações |
| --- | --- |
| Enviar eventos de experiência |  |
| Offer Decisioning | [Documentação](../personalization/offer-decisioning/offer-decisioning-overview.md) |
| Se o conjunto de dados estiver ativado para o perfil, a capacidade de enviar dados para o Perfil de dados do cliente em tempo real |  |
| Enviar dados para o Customer Journey Analytics em tempo real |  |
| Consentimento de gravação no perfil | [Documentação](../../landing/governance-privacy-security/consent/sdk.md) |
| Encaminhar dados do lado do servidor em tempo real para terceiros | [Documentação](../../tags/ui/event-forwarding/overview.md) |
| Suporte ao namespace de identidade |  |

{style=&quot;table-layout:auto&quot;}

## Adobe Analytics

| Caso de uso | Mais Informações |
| --- | --- |
| Analytics for Target (A4T) |  |
| Sem latência do Analytics for Target (A4T) |  |
| Marcação de vários relatórios |  |
| Filtragem de bot |  |
| Props, eVars e eventos |  |
| Suporte a ListVar para Adobe Analytics |  |
| Versão do SO e do navegador |  |
| Variáveis prontas para uso | [Variáveis mapeadas automaticamente](../data-collection/adobe-analytics/automatically-mapped-vars.md) |
| Regras VISTA/regras de processamento |  |
| Suporte a atributos do visitante |  |
| Suporte a link de saída |  |
| Links personalizados/links de download |  |
| Rastreamento de estado e ação |  |
| Serialização de eventos para eventos padrão |  |
| Variável products  | [Documentação](../data-collection/collect-commerce-data.md#actions-related-to-products) |

{style=&quot;table-layout:auto&quot;}

## Adobe Target

| Caso de uso | Mais Informações |
| --- | --- |
| Todos os tipos de atividades |  |
| Suporte nativo e SPA do Visual Experience Composer | [Documentação](../personalization/adobe-target/spa-implementation.md) |
| Compositor baseado em formulário |  |
| Suporte para mbox global | [Documentação](../personalization/rendering-personalization-content.md#automatically-rendering-content) |
| MBoxes personalizadas | [Documentação](../personalization/rendering-personalization-content.md#manually-rendering-content) |
| Analytics for Target (A4T) |  |
| Suporte ao ambiente |  |
| Suporte ao espaço de trabalho |  |
| Links de Controle de qualidade no Adobe Target |  |
| Definir metas com base na localização geográfica/do dispositivo no Adobe Target |  |
| Suporte a atributos do visitante |  |
| Scripts de perfil |  |
| XDM se tornar parâmetros da mbox |  |
| Ofertas de redirecionamento compatíveis com relatórios A4T | [Documentação](https://experienceleague.adobe.com/docs/target/using/experiences/offers/offer-redirect.html?lang=en) |
| Atualização do perfil do Target | [Documentação](../personalization/adobe-target/target-overview.md#single-profile-update) |
| Recomendações |  |
| ID de terceiros da mBox |  |
| Tokens de resposta | [Documentação](../personalization/adobe-target/accessing-response-tokens.md) |

{style=&quot;table-layout:auto&quot;}

## Adobe Audience Manager

| Caso de uso | Mais Informações |
| --- | --- |
| Audience Analytics |  |
| Compartilhamento de segmentos no Adobe Analytics |  |
| Suporte a atributos do visitante |  |
| Sincronizações de parceiros |  |
| Destinos de URL |  |
| Destinos de cookie |  |
| Suporte ao ambiente |  |
| Sincronizar namespaces do Adobe Experience Platform com fontes de dados do Audience Manager |  |
| IDs autenticadas ou conhecidas |  |

{style=&quot;table-layout:auto&quot;}
