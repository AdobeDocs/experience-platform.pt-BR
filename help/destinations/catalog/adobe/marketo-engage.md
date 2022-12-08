---
title: Destino de Marketo Engage
description: O Marketo Engage é a única solução completa de gerenciamento de experiência do cliente (CXM) para marketing, publicidade, análise e comércio. Ele permite automatizar e gerenciar atividades do gerenciamento de clientes potenciais CRM e do engajamento do cliente para marketing baseado em conta e atribuição de receita.
exl-id: 5ae5f114-47ba-4ff6-8e42-f8f43eb079f7
source-git-commit: e68bbc07f7d2e4e05b725cbef37a1810a5825742
workflow-type: tm+mt
source-wordcount: '870'
ht-degree: 2%

---

# destino Marketo Engage {#beta-marketo-engage-destination}

## Log de alterações de destino {#changelog}

>[!IMPORTANT]
>
>Com o lançamento do [conector de destino avançado Marketo V2](/help/release-notes/2022/july-2022.md#destinations), agora você está vendo dois cartões Marketo no catálogo de destinos.
>* Se você já estiver ativando os dados para a variável **[!UICONTROL Marketo V1]** destino: Crie novos fluxos de dados para a **[!UICONTROL Marketo V2]** e exclua os fluxos de dados existentes para a **[!UICONTROL Marketo V1]** até fevereiro de 2023. A partir dessa data, o **[!UICONTROL Marketo V1]** o cartão de destino será removido.
>* Se você ainda não tiver criado nenhum fluxo de dados para a **[!UICONTROL Marketo V1]** destino, use o novo **[!UICONTROL Marketo V2]** cartão para se conectar e exportar dados para o Marketo.


![Imagem dos dois cartões de destino do Marketo em uma exibição lado a lado.](../..//assets/catalog/adobe/marketo-side-by-side-view.png)

As melhorias no destino Marketo V2 incluem:

* No **[!UICONTROL Programar segmento]** etapa do fluxo de trabalho de ativação, no Marketo V1, é necessário adicionar manualmente um **ID de mapeamento** para exportar dados para o Marketo com êxito. Esta etapa manual não é mais necessária no Marketo V2.
* No **[!UICONTROL Mapeamento]** etapa do fluxo de trabalho de ativação, no Marketo V1, era possível mapear campos XDM para apenas três campos de destino no Marketo: `firstName`, `lastName`e `companyName`. Com a versão Marketo V2, agora é possível mapear campos XDM para muitos mais campos no Marketo. Para obter mais informações, leia a [atributos compatíveis](#supported-attributes) mais abaixo.

## Visão geral {#overview}

[!DNL Marketo Engage] O é a única solução completa de gerenciamento de experiência do cliente (CXM) para marketing, publicidade, análise e comércio. Ele permite automatizar e gerenciar atividades do gerenciamento de clientes potenciais CRM e do engajamento do cliente para marketing baseado em conta e atribuição de receita.

O destino permite que os profissionais de marketing enviem segmentos criados no Adobe Experience Platform para o Marketo, onde serão exibidos como listas estáticas.

## Identidades e atributos compatíveis {#supported-identities-attributes}

>[!NOTE]
>
>No [etapa de mapeamento](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) do workflow ativar destino, ele é *mandatory* para mapear identidades e *opcional* para mapear atributos. Mapear o email e/ou a ECID na guia Namespace de identidade é a coisa mais importante a se fazer para garantir que a pessoa corresponda no Marketo. Mapear email garante a maior taxa de correspondência.

### Identidades suportadas {#supported-identities}

| Identidade do Target | Descrição |
|---|---|
| ECID | Um namespace que representa ECID. Esse namespace também pode ser mencionado pelos seguintes aliases: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Consulte o seguinte documento em [ECID](/help/identity-service/ecid.md) para obter mais informações. |
| Email | Um namespace que representa um endereço de email. Esse tipo de namespace geralmente é associado a uma única pessoa e, portanto, pode ser usado para identificá-la em diferentes canais. |

{style=&quot;table-layout:auto&quot;}

### Atributos compatíveis {#supported-attributes}

Você pode mapear atributos do Experience Platform para qualquer um dos atributos aos quais sua organização tem acesso no Marketo. No Marketo, você pode usar a variável [Descrever solicitação da API](https://developers.marketo.com/rest-api/lead-database/leads/#describe) para recuperar os campos de atributo aos quais sua organização tem acesso.

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Exportar segmento]** | Você está exportando todos os membros de um segmento (público-alvo) com os identificadores (email, ECID) usados na [!DNL Marketo Engage] destino. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões &quot;sempre ativas&quot; baseadas em API. Assim que um perfil é atualizado no Experience Platform com base na avaliação do segmento, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Configurar destinos e ativar segmentos {#set-up}

>[!IMPORTANT]
> 
>* Para se conectar ao destino, é necessário **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions).
>* Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]** e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.


Para obter instruções detalhadas sobre como configurar o destino e ativar segmentos, leia [Encaminhar um segmento do Adobe Experience Platform para uma lista estática do Marketo](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html?lang=en) na documentação do Marketo.

O vídeo abaixo também demonstra as etapas para configurar um destino do Marketo e ativar segmentos.

>[!IMPORTANT]
>
>O vídeo não reflete totalmente a capacidade atual. Para obter as informações mais atualizadas, consulte o guia vinculado acima. As seguintes partes do vídeo estão desatualizadas:
> 
>* A placa de destino que você deve usar na interface do usuário do Experience Platform é **[!UICONTROL Marketo V2]**.
>* O vídeo não mostra o novo **[!UICONTROL Criação da pessoa]** campo seletor no workflow conectar ao destino.
>* As duas limitações chamadas no vídeo não se aplicam mais. Agora é possível mapear muitos outros campos de atributos de perfil, além das informações de associação de segmento que eram compatíveis no momento em que o vídeo foi gravado. Também é possível exportar membros do segmento para o Marketo que ainda não existem em suas listas estáticas do Marketo e eles serão adicionados às listas.
>* No **[!UICONTROL Etapa agendar segmento]** do fluxo de trabalho de ativação, no Marketo V1, é necessário adicionar manualmente um **[!UICONTROL ID de mapeamento]** para exportar dados para o Marketo com êxito. Esta etapa manual não é mais necessária no Marketo V2.


>[!VIDEO](https://video.tv.adobe.com/v/338248?quality=12)

<!--

## Connect to the destination {#connect}

To connect to this destination, follow the steps described in the [destination configuration tutorial](../../ui/connect-destination.md).

-->

## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] Os destinos são compatíveis com as políticas de uso de dados ao manipular os dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] aplica o controle de dados, consulte [visão geral de governança de dados](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=pt-BR).

<!--

## Activate segments to this destination {#activate}

See [Activate audience data to streaming segment export destinations](../../ui/activate-segment-streaming-destinations.md) for instructions on activating audience segments to this destination.

-->
