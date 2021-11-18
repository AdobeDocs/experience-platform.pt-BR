---
title: Destino de Marketo Engage
description: O Marketo Engage é a única solução completa de gerenciamento de experiência do cliente (CXM) para marketing, publicidade, análise e comércio. Ele permite automatizar e gerenciar atividades do gerenciamento de clientes potenciais CRM e do engajamento do cliente para marketing baseado em conta e atribuição de receita.
exl-id: 5ae5f114-47ba-4ff6-8e42-f8f43eb079f7
source-git-commit: 05b97e8bdeb4ffb81a4a671d282d0d8ebc7e870a
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 1%

---

# destino Marketo Engage {#beta-marketo-engage-destination}

## Visão geral {#overview}

O Marketo Engage é a única solução completa de gerenciamento de experiência do cliente (CXM) para marketing, publicidade, análise e comércio. Ele permite automatizar e gerenciar atividades do gerenciamento de clientes potenciais CRM e do engajamento do cliente para marketing baseado em conta e atribuição de receita.

O destino permite que os profissionais de marketing enviem segmentos criados no Adobe Experience Platform para o Marketo, onde serão exibidos como listas estáticas.

## Identidades suportadas {#supported-identities}

| Identidade do Target | Descrição |
|---|---|
| ECID | Um namespace que representa ECID. Esse namespace também pode ser mencionado pelos seguintes aliases: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Consulte o seguinte documento em [ECID](/help/identity-service/ecid.md) para obter mais informações. |
| Email | Um namespace que representa um endereço de email. Esse tipo de namespace geralmente é associado a uma única pessoa e, portanto, pode ser usado para identificá-la em diferentes canais. |

>[!NOTE]
>
>No [etapa de mapeamento](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) do workflow ativar destino, ele é *mandatory* para mapear identidades e *opcional* para mapear atributos. Mapear o email e/ou a ECID na guia Namespace de identidade é a coisa mais importante a se fazer para garantir que a pessoa corresponda no Marketo. Mapear email garante a maior taxa de correspondência.

## Tipo de exportação {#export-type}

Exportar segmento - você está exportando todos os membros de um segmento (público-alvo) com os identificadores (email, ECID) usados no destino do Marketo Engage.

## Configurar destinos e ativar segmentos {#set-up}

Para obter instruções detalhadas sobre como configurar o destino e ativar segmentos, leia [Encaminhar um segmento do Adobe Experience Platform para uma lista estática do Marketo](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html?lang=en) na documentação do Marketo.

O vídeo abaixo também demonstra as etapas para configurar um destino do Marketo e ativar segmentos.

>[!NOTE]
>
>A interface do usuário do Experience Platform é atualizada com frequência e pode ter sido alterada desde a gravação deste vídeo. Para obter as informações mais atualizadas, consulte o guia vinculado acima.

>[!VIDEO](https://video.tv.adobe.com/v/338248?quality=12)

<!--

## Connect to the destination {#connect}

To connect to this destination, follow the steps described in the [destination configuration tutorial](../../ui/connect-destination.md).

-->

## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] Os destinos são compatíveis com as políticas de uso de dados ao manipular os dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] aplica o controle de dados, consulte [visão geral de governança de dados](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).

<!--

## Activate segments to this destination {#activate}

See [Activate audience data to streaming segment export destinations](../../ui/activate-segment-streaming-destinations.md) for instructions on activating audience segments to this destination.

-->
