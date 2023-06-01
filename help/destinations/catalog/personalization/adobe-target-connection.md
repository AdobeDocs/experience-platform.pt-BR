---
keywords: personalização do target, destino, destino do experience platform target, destino do adobe target,
title: Conexão com o Adobe Target
description: O Adobe Target é um aplicativo que fornece recursos de personalização e experimentação em tempo real e alimentados por IA em todas as interações de entrada de clientes em sites, aplicativos móveis e muito mais.
exl-id: 3e3c405b-8add-4efb-9389-5ad695bc9799
source-git-commit: bee1bf0ec9cbf35ea7303921059068c01cb9f54a
workflow-type: tm+mt
source-wordcount: '908'
ht-degree: 8%

---

# Conexão com o Adobe Target {#adobe-target-connection}

## Log de alterações de destino {#changelog}

| Mês de lançamento | Tipo de atualização | Descrição |
|---|---|---|
| Abril de 2023 | Atualização de funcionalidade e documentação | A partir de abril de 2023, a **[!UICONTROL Adobe Target]** suporte para conexão [personalização baseada em atributos](../../ui/activate-edge-personalization-destinations.md#map-attributes) e está disponível para todos os clientes. |

{style="table-layout:auto"}

## Visão geral {#overview}

O Adobe Target é um aplicativo que fornece recursos de personalização e experimentação em tempo real e alimentados por IA em todas as interações de entrada de clientes em sites, aplicativos móveis e muito mais.

O Adobe Target é uma conexão de personalização no catálogo de destinos do Adobe Experience Platform.

Para obter uma breve visão geral sobre como configurar a conexão do Adobe Target no Experience Platform, assista ao vídeo abaixo.

>[!VIDEO](https://video.tv.adobe.com/v/3418799/?quality=12&learn=on)

## Pré-requisitos {#prerequisites}

### ID da sequência de dados {#datastream-id}

Ao configurar a conexão do Adobe Target com o [usar uma ID de sequência de dados](#parameters), você deve ter o [Adobe Experience Platform Web SDK](../../../edge/home.md) implementado.

Configurar a conexão do Adobe Target sem usar uma ID de sequência de dados não requer a implementação do SDK da Web.

>[!IMPORTANT]
>
>Antes de criar um [!DNL Adobe Target] conexão, leia o guia sobre como [configurar destinos de personalização para personalização de mesma página e próxima página](../../ui/activate-edge-personalization-destinations.md). Este guia orienta você sobre as etapas de configuração necessárias para casos de uso de personalização de mesma página e próxima página, em vários componentes do Experience Platform. A personalização de mesma página e próxima página requer que você use uma ID de fluxo de dados ao configurar a conexão do Adobe Target.

### Pré-requisitos no Adobe Target {#prerequisites-in-adobe-target}

No Adobe Target, verifique se o usuário tem:

* O acesso à [espaço de trabalho padrão](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html?lang=en#default-workspace);
* A variável **Aprovador** [função](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html?lang=en#roles-and-permissions).

Leia mais sobre a concessão de permissões para [Target Premium](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html?lang=en#section_8C425E43E5DD4111BBFC734A2B7ABC80) e para [Target Standard](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/users/user-management.html?lang=en#roles-permissions).

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!DNL Profile request]** | Você está solicitando todos os segmentos mapeados no destino do Adobe Target para um único perfil. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões baseadas em API &quot;sempre ativas&quot;. Assim que um perfil é atualizado em Experience Platform com base na avaliação do segmento, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conectar ao destino {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_target_datastream"
>title="Sobre IDs de sequência de dados"
>abstract="Essa opção determina em qual sequência de dados de coleção de dados os segmentos serão incluídos. O menu suspenso mostra apenas as sequências de dados que têm a configuração do Target ativada. Para usar a segmentação de borda, você deve selecionar uma ID de sequência de dados. Selecionar Nenhum desabilita todos os casos de uso que usam segmentação de borda."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html#parameters" text="Saiba mais sobre a seleção de sequências de dados"

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa da variável **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md).

O Adobe Experience Platform se conecta automaticamente à instância Adobe Target da sua empresa. Não é necessária nenhuma autenticação.

### Parâmetros de conexão {#parameters}

Enquanto [configuração](../../ui/connect-destination.md) Para esse destino, você deve fornecer as seguintes informações:

* **Nome**: Preencha o nome preferencial para este destino.
* **Descrição**: digite uma descrição para o destino. Por exemplo, você pode mencionar para qual campanha está usando esse destino. Este campo é opcional.
* **ID da sequência de dados**: determina em qual sequência de dados de Coleção de dados os segmentos serão incluídos. O menu suspenso mostra somente os fluxos de dados que têm os serviços Target e Adobe Experience Platform ativados. Consulte [configurar um fluxo de dados](../../../edge/datastreams/configure.md#aep) para obter informações detalhadas sobre como configurar um fluxo de dados para o Adobe Experience Platform e o Adobe Target.
   * **[!UICONTROL Nenhum]**: selecione essa opção se precisar configurar a personalização do Adobe Target, mas não puder implementar o [Experience Platform Web SDK](../../../edge/home.md). Ao usar essa opção, os segmentos exportados do Experience Platform para o Target suportam apenas a personalização da próxima sessão e a segmentação de borda é desativada. Consulte a tabela abaixo para obter mais informações.

| Nenhum fluxo de dados selecionado | Sequência de dados selecionada |
|---|---|
| <ul><li>[Segmentação de borda](../../../segmentation/ui/edge-segmentation.md) não é compatível.</li><li>[Personalização de mesma página e próxima página](../../ui/activate-edge-personalization-destinations.md) não são compatíveis.</li><li>Você pode compartilhar segmentos com a conexão do Adobe Target somente para o *sandbox de produção padrão*.</li><li>Para configurar a personalização da próxima sessão sem usar uma ID de fluxo de dados, use [at.js](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/at-js/how-atjs-works.html?lang=en).</li></ul> | <ul><li>A segmentação de borda funciona conforme esperado.</li><li>[Personalização de mesma página e próxima página](../../ui/activate-edge-personalization-destinations.md) são compatíveis.</li><li>O compartilhamento de segmentos é compatível com outras sandboxes.</li></ul> |

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface do](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Próxima]**.

## Ativar segmentos para este destino {#activate}

>[!IMPORTANT]
> 
>Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]**, e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Ler [Ativar perfis e segmentos para destinos de solicitação de perfil](../../ui/activate-edge-personalization-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para esse destino.

## Dados exportados {#exported-data}

O Adobe Target lê os dados do perfil da Rede de borda da Adobe Experience Platform, de modo que nenhum dado é exportado.

## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] os destinos estão em conformidade com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] fiscaliza a governança de dados, leia o [Visão geral da governança de dados](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=pt-BR).
