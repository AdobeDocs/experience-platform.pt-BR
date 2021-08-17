---
title: Destino de Marketo Engage
description: O Marketo Engage é a única solução completa de gerenciamento de experiência do cliente (CXM) para marketing, publicidade, análise e comércio. Ele permite automatizar e gerenciar atividades do gerenciamento de clientes potenciais CRM e do engajamento do cliente para marketing baseado em conta e atribuição de receita.
source-git-commit: 3aac1e7c7fe838201368379da8504efc8e316e1c
workflow-type: tm+mt
source-wordcount: '327'
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

## Configurar {#set-up}

As instruções sobre como configurar o destino [podem ser encontradas aqui](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html?lang=en).

## Conecte-se ao destino {#connect}

Para se conectar a esse destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md).

## Uso e governança de dados {#data-usage-governance}

Todos os destinos [!DNL Adobe Experience Platform] são compatíveis com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] aplica o controle de dados, consulte a [visão geral do controle de dados](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).

## Ativar segmentos para este destino {#activate}

Consulte [Ativar os dados do público-alvo para os destinos de exportação de segmentos de fluxo](../../ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para esse destino.
