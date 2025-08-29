---
title: Destino do Marketo Engage
description: O Marketo Engage é a única solução completa de gerenciamento de experiência do cliente (CXM) para marketing, publicidade, análises e comércio. Ele permite automatizar e gerenciar atividades do gerenciamento de clientes potenciais de CRM e do envolvimento do cliente para o marketing baseado em conta e a atribuição de receita.
exl-id: 5ae5f114-47ba-4ff6-8e42-f8f43eb079f7
source-git-commit: 891484b279d2521115c6b1edc58f45c594a55382
workflow-type: tm+mt
source-wordcount: '874'
ht-degree: 1%

---

# (Herdado) (V2) Destino do Marketo Engage {#beta-marketo-engage-destination}

## Log de alterações de destino {#changelog}

<!--
>[!IMPORTANT]
>
>The **[!UICONTROL (Legacy) (V2) Marketo Engage]** will be deprecated in **March 2026**.
>
>To ensure a smooth transition to the new **[[!UICONTROL Marketo Engage]](marketo-engage-connection.md)** destination, review the following key points and required actions:
>
>* All users of the existing **[!UICONTROL (Legacy) (V2) Marketo Engage]** must migrate to the new **[!UICONTROL Marketo Engage]** destination by March 2026.
>* **Existing dataflows will not be migrated automatically.** You must [set up a new connection](../../ui/connect-destination.md) to the new **[!UICONTROL Marketo Engage]** destination and activate your audiences there.

-->

![Imagem dos dois cartões de destino do Marketo em uma exibição lado a lado.](../..//assets/catalog/adobe/marketo-side-by-side-view.png)

As melhorias no destino do Marketo V2 incluem:

* Na etapa **[!UICONTROL Segmento de agendamento]** do fluxo de trabalho de ativação, no Marketo V1, foi necessário adicionar manualmente uma **ID de Mapeamento** para exportar dados com êxito para o Marketo. Esta etapa manual não é mais necessária no Marketo V2.
* Na etapa **[!UICONTROL Mapeamento]** do fluxo de trabalho de ativação, no Marketo V1, você conseguiu mapear campos XDM para apenas três campos de destino no Marketo: `firstName`, `lastName` e `companyName`. Com a versão Marketo V2, agora é possível mapear campos XDM para muitos mais campos no Marketo. Para obter mais informações, leia a seção [atributos suportados](#supported-attributes) mais abaixo.

## Visão geral {#overview}

O [!DNL Marketo Engage] é a única solução CXM (gerenciamento de experiência do cliente) completa para marketing, publicidade, análises e comércio. Ele permite automatizar e gerenciar atividades do gerenciamento de clientes potenciais de CRM e do envolvimento do cliente para o marketing baseado em conta e a atribuição de receita.

O destino permite que os profissionais de marketing enviem públicos-alvo criados no Adobe Experience Platform para o Marketo, onde serão exibidos como listas estáticas.

## Identidades e atributos compatíveis {#supported-identities-attributes}

>[!NOTE]
>
>Na [etapa de mapeamento](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) do fluxo de trabalho de destino ativado, é *obrigatório* mapear identidades e *opcional* mapear atributos. Mapear o email e/ou a ECID da guia Namespace de identidade é a coisa mais importante a ser feita para garantir que a pessoa seja correspondida no Marketo. O mapeamento de email garante a taxa de correspondência mais alta.

### Identidades suportadas {#supported-identities}

| Identidade de destino | Descrição |
|---|---|
| ECID | Um namespace que representa a ECID. Esse namespace também pode ser referenciado pelos seguintes aliases: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Consulte o seguinte documento no [ECID](/help/identity-service/features/ecid.md) para obter mais informações. |
| Email | Um namespace que representa um endereço de email. Esse tipo de namespace é frequentemente associado a uma única pessoa e, portanto, pode ser usado para identificá-la em diferentes canais. |

{style="table-layout:auto"}

### Atributos compatíveis {#supported-attributes}

Você pode mapear atributos do Experience Platform para qualquer um dos atributos aos quais sua organização tem acesso no Marketo. No Marketo, você pode usar a [Solicitação de API de descrição](https://developers.marketo.com/rest-api/lead-database/leads/#describe) para recuperar os campos de atributo aos quais sua organização tem acesso.

## Públicos-alvo compatíveis {#supported-audiences}

Esta seção descreve quais tipos de públicos-alvo você pode exportar para esse destino.

| Origem do público | Suportado | Descrição |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Públicos-alvo gerados pelo [Serviço de Segmentação](../../../segmentation/home.md) da Experience Platform. |
| Uploads personalizados | ✓ | Públicos [importados](../../../segmentation/ui/audience-portal.md#import-audience) para o Experience Platform de arquivos CSV. |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Exportação de público-alvo]** | Você está exportando todos os membros de um público com os identificadores (email, ECID) usados no destino [!DNL Marketo Engage]. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões baseadas em API &quot;sempre ativas&quot;. Assim que um perfil for atualizado no Experience Platform com base na avaliação do público-alvo, o conector enviará a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Configurar destino e ativar públicos {#set-up}

>[!IMPORTANT]
> 
>* Para se conectar ao destino, você precisa de **[!UICONTROL Exibir Destinos]** e **[!UICONTROL Gerenciar Destinos]** [permissões de controle de acesso](/help/access-control/home.md#permissions).
>* Para ativar dados, você precisa de **[!UICONTROL Exibir Destinos]**, **[!UICONTROL Ativar Destinos]**, **[!UICONTROL Exibir Perfis]** e **[!UICONTROL Exibir Segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.

Para obter instruções detalhadas sobre como configurar o destino e ativar públicos, leia [Enviar um público-alvo da Adobe Experience Platform para uma lista estática do Marketo](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html) na documentação do Marketo.

O vídeo abaixo também demonstra as etapas para configurar um destino do Marketo e ativar públicos-alvo.

>[!IMPORTANT]
>
>O vídeo não reflete totalmente a capacidade atual. Para obter as informações mais atualizadas, consulte o manual vinculado acima. As seguintes partes do vídeo estão desatualizadas:
> 
>* O cartão de destino que você deve usar na interface do Experience Platform é o **[!UICONTROL Marketo V2]**.
>* O vídeo não mostra o novo campo seletor **[!UICONTROL Criação de pessoa]** na conexão com o fluxo de trabalho de destino. Para usar esse campo, você deve mapear o nome e o sobrenome durante a etapa de mapeamento do atributo.
>* As duas limitações chamadas no vídeo não se aplicam mais. Agora é possível mapear vários outros campos de atributo de perfil, além das informações de associação de público-alvo aceitas no momento em que o vídeo foi gravado. Você também pode exportar membros do público-alvo para o Marketo que ainda não existem nas listas estáticas do Marketo e eles serão adicionados às listas.
>* Na **[!UICONTROL etapa Agendar público-alvo]** do fluxo de trabalho de ativação, no Marketo V1, foi necessário adicionar manualmente uma **[!UICONTROL ID de Mapeamento]** para exportar dados com êxito para o Marketo. Esta etapa manual não é mais necessária no Marketo V2.

>[!VIDEO](https://video.tv.adobe.com/v/338248?quality=12)

## Monitorar destino {#monitor-destination}

Depois de se conectar ao destino e estabelecer um fluxo de dados de destino, você pode usar a [funcionalidade de monitoramento](/help/dataflows/ui/monitor-destinations.md) do Real-Time CDP para obter informações abrangentes sobre os registros de perfil ativados para o destino em cada execução de fluxo de dados.

As informações de monitoramento da conexão [!DNL Marketo Engage] incluem informações de nível de público relacionadas a identidades ativadas, excluídas e com falha em cada execução de fluxo de dados e fluxo de dados. [Leia mais](/help/dataflows/ui/monitor-destinations.md#segment-level-view) sobre a funcionalidade.

## Uso e governança de dados {#data-usage-governance}

Todos os destinos do [!DNL Adobe Experience Platform] são compatíveis com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como o [!DNL Adobe Experience Platform] impõe a governança de dados, consulte a [visão geral da governança de dados](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=pt-BR).
