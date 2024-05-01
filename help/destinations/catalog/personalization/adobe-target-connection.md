---
keywords: personalização do target, destino, destino do experience platform target, destino do adobe target,
title: Conexão com o Adobe Target
description: O Adobe Target é um aplicativo que fornece recursos de personalização e experimentação em tempo real e alimentados por IA em todas as interações de entrada de clientes em sites, aplicativos móveis e muito mais.
exl-id: 3e3c405b-8add-4efb-9389-5ad695bc9799
source-git-commit: c113d9615a276af67714f38b8325e69737b23964
workflow-type: tm+mt
source-wordcount: '1303'
ht-degree: 13%

---

# Conexão com o Adobe Target {#adobe-target-connection}

## Log de alterações de destino {#changelog}

| Mês de lançamento | Tipo de atualização | Descrição |
|---|---|---|
| Abril de 2024 | Atualização de funcionalidade e documentação | Ao se conectar ao destino com o usando uma ID de fluxo de dados, você agora *não precisam* para ativar necessariamente a sequência de dados para segmentação de borda. Isso significa que o destino funcionará com públicos-alvo em lote e de transmissão, embora os casos de uso que você pode fazer sejam diferentes. Exibir a tabela no [parâmetros de conexão](#parameters) para obter mais informações. |
| Janeiro de 2024 | Atualização de funcionalidade e documentação | Agora é possível compartilhar públicos-alvo e atributos de perfil na conexão do Adobe Target para a sandbox de produção padrão e outras sandboxes não padrão. |
| Junho de 2023 | Atualização de funcionalidade e documentação | A partir de junho de 2023, você poderá selecionar o espaço de trabalho do Adobe Target para o qual deseja compartilhar públicos ao configurar uma nova conexão de destino do Adobe Target. Consulte a seção [parâmetros de conexão](#parameters) para obter mais informações. Além disso, consulte o tutorial sobre a [configuração de espaços de trabalho](https://experienceleague.adobe.com/docs/target-learn/tutorials/administration/set-up-workspaces.html?lang=pt-BR) no Adobe Target para obter mais informações sobre espaços de trabalho. |
| Maio de 2023 | Atualização de funcionalidade e documentação | A partir de maio de 2023, a **[!UICONTROL Adobe Target]** suporte para conexão [personalização baseada em atributos](../../ui/activate-edge-personalization-destinations.md#map-attributes) e está disponível para todos os clientes. |

{style="table-layout:auto"}

## Visão geral {#overview}

O Adobe Target é um aplicativo que fornece recursos de personalização e experimentação em tempo real e alimentados por IA em todas as interações de entrada de clientes em sites, aplicativos móveis e muito mais.

O Adobe Target é uma conexão de personalização no catálogo de destinos do Adobe Experience Platform.

## Vídeo da visão geral {#video-overview}

Para obter uma breve visão geral sobre como configurar a conexão do Adobe Target no Experience Platform, assista ao vídeo abaixo.

>[!VIDEO](https://video.tv.adobe.com/v/3418799/?quality=12&learn=on)

## Pré-requisitos {#prerequisites}

### ID da sequência de dados {#datastream-id}

Ao configurar a conexão do Adobe Target com o [usar uma ID de sequência de dados](#parameters), você deve ter o [Adobe Experience Platform Web SDK](/help/web-sdk/home.md) implementado.

Configurar a conexão do Adobe Target sem usar uma ID de sequência de dados não requer a implementação do SDK da Web.

>[!IMPORTANT]
>
>Antes de criar um [!DNL Adobe Target] conexão, leia o guia sobre como [configurar destinos de personalização para personalização de mesma página e próxima página](../../ui/activate-edge-personalization-destinations.md). Este guia orienta você sobre as etapas de configuração necessárias para casos de uso de personalização de mesma página e próxima página, em vários componentes do Experience Platform. Para obter casos de uso de personalização de mesma página e próxima página, você deve usar uma ID de fluxo de dados ao configurar a conexão do Adobe Target.

### Pré-requisitos no Adobe Target {#prerequisites-in-adobe-target}

No Adobe Target, verifique se o usuário tem:

* O acesso à [espaço de trabalho padrão](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html#default-workspace);
* A variável **Aprovador** [função](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html#roles-and-permissions).

Leia mais sobre a concessão de permissões para [Target Premium](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html#section_8C425E43E5DD4111BBFC734A2B7ABC80) e para [Target Standard](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/users/user-management.html#roles-permissions).

## Públicos-alvo compatíveis {#supported-audiences}

Esta seção descreve quais tipos de públicos-alvo você pode exportar para esse destino.

| Origem do público | Suportado | Descrição |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Públicos-alvo gerados pelo Experience Platform [Serviço de segmentação](../../../segmentation/home.md). |
| Uploads personalizados | X | Públicos-alvo [importado](../../../segmentation/ui/overview.md#import-audience) para o Experience Platform de arquivos CSV. |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!DNL Profile request]** | Você está solicitando todos os públicos mapeados no destino do Adobe Target para um único perfil. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões baseadas em API &quot;sempre ativas&quot;. Assim que um perfil é atualizado em Experience Platform com base na avaliação do público-alvo, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conectar ao destino {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_target_datastream"
>title="Sobre IDs de sequências de dados"
>abstract="Essa opção determina em qual sequência de coleção de dados os públicos-alvo serão incluídos. O menu suspenso mostra apenas as sequências de dados que têm a configuração do Target ativada. Para usar a segmentação de borda, você deve selecionar uma ID de sequência de dados. Selecionar Nenhum desabilita todos os casos de uso que usam segmentação de borda."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html?lang=pt-BR#parameters" text="Saiba mais sobre a seleção de sequências de dados"

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa da variável **[!UICONTROL Exibir destinos]** e **[!UICONTROL Gerenciar destinos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md).

O Adobe Experience Platform se conecta automaticamente à instância Adobe Target da sua empresa. Não é necessária nenhuma autenticação.

### Parâmetros de conexão {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_target_workspace"
>title="Sobre o os Espaços de trabalho do Adobe Target"
>abstract="Selecione o espaço de trabalho do Adobe Target para o qual os públicos-alvo serão compartilhados. Você pode selecionar um único espaço de trabalho para cada conexão do Adobe Target. Após a ativação, os públicos-alvo são roteados para o espaço de trabalho selecionado, seguindo os rótulos de uso de dados aplicáveis da Experience Platform."
>additional-url="https://experienceleague.adobe.com/docs/target-learn/tutorials/administration/set-up-workspaces.html?lang=pt-BR" text="Saiba mais sobre os espaços de trabalho do Adobe Target"

Enquanto [configuração](../../ui/connect-destination.md) Para esse destino, você deve fornecer as seguintes informações:

* **Nome**: Preencha o nome preferencial para este destino.
* **Descrição**: digite uma descrição para o destino. Por exemplo, você pode mencionar para qual campanha está usando esse destino. Este campo é opcional.
* **ID da sequência de dados**: determina em qual sequência de dados de Coleção de dados os públicos-alvo serão incluídos. O menu suspenso mostra somente os fluxos de dados que têm os serviços Target e Adobe Experience Platform ativados. Consulte [configurar um fluxo de dados](../../../datastreams/configure.md#aep) para obter informações detalhadas sobre como configurar um fluxo de dados para o Adobe Experience Platform e o Adobe Target.

  >[!IMPORTANT]
  >
  >A ID do fluxo de dados é exclusiva para cada conexão de destino do Adobe Target. Se você precisar mapear os mesmos públicos-alvo para vários fluxos de dados, é necessário [criar uma nova conexão de destino](../../ui/connect-destination.md) para cada ID de fluxo de dados e passe pelo [fluxo de ativação de público](#activate).

   * **[!UICONTROL Nenhum]**: selecione essa opção se precisar configurar a personalização do Adobe Target, mas não puder implementar o [Experience Platform Web SDK](/help/web-sdk/home.md). Ao usar essa opção, os públicos-alvo exportados do Experience Platform para o Target serão compatíveis apenas com a personalização da próxima sessão e a segmentação de borda será desativada. Consulte a tabela abaixo para obter uma comparação dos casos de uso disponíveis por tipo de implementação.

  | Implementação do Adobe Target *sem* SDK da Web | Implementação do Adobe Target *com* SDK da Web | Implementação do Adobe Target *com* SDK da Web *e* segmentação de borda desativada |
  |---|---|---|
  | <ul><li>Uma sequência de dados não é necessária. O Adobe Target pode ser implantado por meio de [at.js](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/overview.html?lang=pt-BR), [lado do servidor](https://experienceleague.adobe.com/docs/target-dev/developer/overview.html#server-side-implementation)ou [híbrido](https://experienceleague.adobe.com/docs/target-dev/developer/overview.html#hybrid-implementation) métodos de implementação.</li><li>[Segmentação de borda](../../../segmentation/ui/edge-segmentation.md) não é compatível.</li><li>[Personalização de mesma página e próxima página](../../ui/activate-edge-personalization-destinations.md) não são compatíveis.</li><li>É possível compartilhar públicos-alvo e atributos de perfil na conexão do Adobe Target para a *sandbox de produção padrão* sandboxes e não padrão.</li><li>Para configurar a personalização da próxima sessão sem usar uma ID de fluxo de dados, use [at.js](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/at-js/how-atjs-works.html).</li></ul> | <ul><li>É necessário um fluxo de dados com o Adobe Target e o Experience Platform configurados como serviços.</li><li>A segmentação de borda funciona conforme esperado.</li><li>[Personalização de mesma página e próxima página](../../ui/activate-edge-personalization-destinations.md#use-cases) são compatíveis.</li><li>O compartilhamento de públicos-alvo e atributos de perfil de outras sandboxes é compatível.</li></ul> | <ul><li>É necessário um fluxo de dados com o Adobe Target e o Experience Platform configurados como serviços.</li><li>Quando [configuração do fluxo de dados](/help/destinations/ui/activate-edge-personalization-destinations.md#configure-datastream), não selecione a variável **Segmentação de borda** caixa de seleção</li><li>[Personalização da próxima sessão](../../ui/activate-edge-personalization-destinations.md#next-session) é compatível.</li><li>O compartilhamento de públicos-alvo e atributos de perfil de outras sandboxes é compatível.</li></ul> |

* **Workspace**: selecione a Adobe Target [espaço de trabalho](https://experienceleague.adobe.com/docs/target-learn/tutorials/administration/set-up-workspaces.html?lang=pt-BR) para os quais os públicos-alvo serão compartilhados. Você pode selecionar um único espaço de trabalho para cada conexão do Adobe Target. Após a ativação, os públicos-alvo são roteados para o espaço de trabalho selecionado enquanto seguem o caminho [rótulos de uso de dados do Experience Platform](../../../data-governance/labels/overview.md).

>[!NOTE]
>
>Ao usar um espaço de trabalho personalizado do Target para [personalização de mesma página e próxima página com atributos](../../ui/activate-edge-personalization-destinations.md), somente o [públicos selecionados](../../ui/activate-edge-personalization-destinations.md#select-audiences) são enviados para o espaço de trabalho do Target selecionado. A variável [atributos mapeados](../../ui/activate-edge-personalization-destinations.md#mapping) são enviados para o espaço de trabalho padrão do Target.
><br>
>Esse comportamento será alterado em uma atualização futura.

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface do](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Próxima]**.

## Ativar públicos-alvo para esse destino {#activate}

>[!IMPORTANT]
> 
>Para ativar os dados, é necessário **[!UICONTROL Exibir destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]**, e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Ler [Ativar públicos para destinos de personalização de borda](../../ui/activate-edge-personalization-destinations.md) para obter instruções sobre como ativar públicos-alvo para esse destino.

## Dados exportados {#exported-data}

Adobe Target *leituras* dados de perfil da Rede de borda da Adobe Experience Platform, de modo que nenhum dado é exportado.

## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] os destinos estão em conformidade com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] fiscaliza a governança de dados, leia o [Visão geral da governança de dados](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=pt-BR).
