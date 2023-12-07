---
title: Destino do Marketo Engage
description: O Marketo Engage é a única solução completa de gerenciamento de experiência do cliente (CXM) para marketing, publicidade, análises e comércio. Ele permite automatizar e gerenciar atividades do gerenciamento de clientes potenciais de CRM e do envolvimento do cliente para o marketing baseado em conta e a atribuição de receita.
exl-id: 5ae5f114-47ba-4ff6-8e42-f8f43eb079f7
source-git-commit: 34ae6f0f791a40584c2d476ed715bb7c5b733c42
workflow-type: tm+mt
source-wordcount: '882'
ht-degree: 1%

---

# destino Marketo Engage {#beta-marketo-engage-destination}

## Log de alterações de destino {#changelog}

>[!IMPORTANT]
>
>Com o lançamento do [conector de destino aprimorado do Marketo V2](/help/release-notes/2022/july-2022.md#destinations), agora você está vendo dois cartões Marketo no catálogo de destinos.
>* Se você já estiver ativando os dados para a variável **[!UICONTROL Marketo V1]** destino: crie novos fluxos de dados para o **[!UICONTROL Marketo V2]** destino e excluir os fluxos de dados existentes para o **[!UICONTROL Marketo V1]** destino até fevereiro de 2023. A partir dessa data, a **[!UICONTROL Marketo V1]** o cartão de destino será removido.
>* Se você ainda não tiver criado nenhum fluxo de dados para a variável **[!UICONTROL Marketo V1]** destino, use o novo **[!UICONTROL Marketo V2]** para conectar-se e exportar dados para o Marketo.

![Imagem dos dois cartões de destino do Marketo em uma visualização lado a lado.](../..//assets/catalog/adobe/marketo-side-by-side-view.png)

As melhorias no destino do Marketo V2 incluem:

* No **[!UICONTROL Agendar segmento]** etapa do fluxo de trabalho de ativação, no Marketo V1, era necessário adicionar um **ID do mapeamento** para exportar dados com sucesso para o Marketo. Esta etapa manual não é mais necessária no Marketo V2.
* No **[!UICONTROL Mapeamento]** etapa do fluxo de trabalho de ativação, no Marketo V1, você conseguiu mapear campos XDM para apenas três campos de destino no Marketo: `firstName`, `lastName`, e `companyName`. Com a versão Marketo V2, agora é possível mapear campos XDM para muitos mais campos no Marketo. Para obter mais informações, leia a [atributos suportados](#supported-attributes) seção mais abaixo.

## Visão geral {#overview}

[!DNL Marketo Engage] O é a única solução completa de gerenciamento de experiência do cliente (CXM) para marketing, publicidade, análises e comércio. Ele permite automatizar e gerenciar atividades do gerenciamento de clientes potenciais de CRM e do envolvimento do cliente para o marketing baseado em conta e a atribuição de receita.

O destino permite que os profissionais de marketing enviem públicos-alvo criados no Adobe Experience Platform para o Marketo, onde serão exibidos como listas estáticas.

## Identidades e atributos compatíveis {#supported-identities-attributes}

>[!NOTE]
>
>No [etapa de mapeamento](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) do workflow ativar destino, é *obrigatório* para mapear identidades e *opcional* para mapear atributos. Mapear o email e/ou a ECID da guia Namespace de identidade é a coisa mais importante a ser feita para garantir que a pessoa seja correspondida no Marketo. O mapeamento de email garante a taxa de correspondência mais alta.

### Identidades suportadas {#supported-identities}

| Identidade de destino | Descrição |
|---|---|
| ECID | Um namespace que representa a ECID. Esse namespace também pode ser referenciado pelos seguintes aliases: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Consulte o seguinte documento em [ECID](/help/identity-service/ecid.md) para obter mais informações. |
| Email | Um namespace que representa um endereço de email. Esse tipo de namespace é frequentemente associado a uma única pessoa e, portanto, pode ser usado para identificá-la em diferentes canais. |

{style="table-layout:auto"}

### Atributos compatíveis {#supported-attributes}

Você pode mapear atributos do Experience Platform para qualquer um dos atributos aos quais sua organização tem acesso no Marketo. No Marketo, você pode usar a variável [Descrever solicitação de API](https://developers.marketo.com/rest-api/lead-database/leads/#describe) para recuperar os campos de atributo aos quais sua organização tem acesso.

## Públicos-alvo compatíveis {#supported-audiences}

Esta seção descreve quais tipos de públicos-alvo você pode exportar para esse destino.

| Origem do público | Suportado | Descrição |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Públicos-alvo gerados pelo Experience Platform [Serviço de segmentação](../../../segmentation/home.md). |
| Uploads personalizados | ✓ | Públicos-alvo [importado](../../../segmentation/ui/overview.md#import-audience) para o Experience Platform de arquivos CSV. |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Exportação de público]** | Você está exportando todos os membros de um público-alvo com os identificadores (email, ECID) usados no [!DNL Marketo Engage] destino. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões baseadas em API &quot;sempre ativas&quot;. Assim que um perfil é atualizado em Experience Platform com base na avaliação do público-alvo, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Configurar destino e ativar públicos {#set-up}

>[!IMPORTANT]
> 
>* Para se conectar ao destino, você precisa da variável **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions).
>* Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]**, e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para obter instruções detalhadas sobre como configurar o destino e ativar públicos, leia [Encaminhar um público-alvo do Adobe Experience Platform para uma lista estática do Marketo](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html) na documentação do Marketo.

O vídeo abaixo também demonstra as etapas para configurar um destino do Marketo e ativar públicos-alvo.

>[!IMPORTANT]
>
>O vídeo não reflete totalmente a capacidade atual. Para obter as informações mais atualizadas, consulte o manual vinculado acima. As seguintes partes do vídeo estão desatualizadas:
> 
>* O cartão de destino que deve ser usado na interface do usuário do Experience Platform é **[!UICONTROL Marketo V2]**.
>* O vídeo não mostra as novas **[!UICONTROL Criação de pessoa]** campo seletor no fluxo de trabalho conectar ao destino.
>* As duas limitações chamadas no vídeo não se aplicam mais. Agora é possível mapear vários outros campos de atributo de perfil, além das informações de associação de público-alvo aceitas no momento em que o vídeo foi gravado. Você também pode exportar membros do público-alvo para o Marketo que ainda não existem nas listas estáticas do Marketo e eles serão adicionados às listas.
>* No **[!UICONTROL Agendar etapa de público]** do fluxo de trabalho de ativação, no Marketo V1, era necessário adicionar manualmente uma **[!UICONTROL ID do mapeamento]** para exportar dados com sucesso para o Marketo. Esta etapa manual não é mais necessária no Marketo V2.

>[!VIDEO](https://video.tv.adobe.com/v/338248?quality=12)

<!--

## Connect to the destination {#connect}

To connect to this destination, follow the steps described in the [destination configuration tutorial](../../ui/connect-destination.md).

-->

## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] os destinos estão em conformidade com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] fiscaliza a governança de dados, consulte o [visão geral da governança de dados](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=pt-BR).

<!--

## Activate audiences to this destination {#activate}

See [Activate audience data to streaming audience export destinations](../../ui/activate-segment-streaming-destinations.md) for instructions on activating audiences to this destination.

-->
