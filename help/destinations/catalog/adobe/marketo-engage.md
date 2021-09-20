---
title: Destino de Marketo Engage
description: O Marketo Engage é a única solução completa de gerenciamento de experiência do cliente (CXM) para marketing, publicidade, análise e comércio. Ele permite automatizar e gerenciar atividades do gerenciamento de clientes potenciais CRM e do engajamento do cliente para marketing baseado em conta e atribuição de receita.
exl-id: 5ae5f114-47ba-4ff6-8e42-f8f43eb079f7
source-git-commit: 1f18e07af7ef0d90f882fa668c5659330bce5960
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 1%

---

# (Beta) Marketo Engage destination {#beta-marketo-engage-destination}

>[!IMPORTANT]
>
>O Destino do Marketo Engage no Adobe Experience Platform está atualmente na versão beta. A documentação e a funcionalidade estão sujeitas a alterações.

## Visão geral {#overview}

O Marketo Engage é a única solução completa de gerenciamento de experiência do cliente (CXM) para marketing, publicidade, análise e comércio. Ele permite automatizar e gerenciar atividades do gerenciamento de clientes potenciais CRM e do engajamento do cliente para marketing baseado em conta e atribuição de receita.

O conector de segmento permite que os profissionais de marketing enviem segmentos criados no Adobe Experience Platform para o Marketo, onde serão exibidos como listas estáticas.

## Identidades suportadas {#supported-identities}

| Identidade do Target | Descrição |
|---|---|
| ECID | Um namespace que representa ECID. Esse namespace também pode ser mencionado pelos seguintes aliases: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Consulte o seguinte documento em [ECID](/help/identity-service/ecid.md) para obter mais informações. |
| Email | Um namespace que representa um endereço de email. Esse tipo de namespace geralmente é associado a uma única pessoa e, portanto, pode ser usado para identificá-la em diferentes canais. |

## Tipo de exportação {#export-type}

Exportar segmento - você está exportando todos os membros de um segmento (público-alvo) com os identificadores (nome, número de telefone ou outros) usados no destino do Marketo Engage.

## Configurar destinos e ativar segmentos {#set-up}

Para obter instruções detalhadas sobre como configurar o destino e ativar segmentos, leia [Encaminhar um segmento do Adobe Experience Platform para uma Lista Estática do Marketo](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html?lang=en) na documentação do Marketo.

<!--

## Connect to the destination {#connect}

To connect to this destination, follow the steps described in the [destination configuration tutorial](../../ui/connect-destination.md).

-->

## Uso e governança de dados {#data-usage-governance}

Todos os destinos [!DNL Adobe Experience Platform] são compatíveis com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] aplica o controle de dados, consulte a [visão geral do controle de dados](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).

<!--

## Activate segments to this destination {#activate}

See [Activate audience data to streaming segment export destinations](../../ui/activate-segment-streaming-destinations.md) for instructions on activating audience segments to this destination.

-->