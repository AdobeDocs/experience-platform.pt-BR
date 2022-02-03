---
title: Configurar o conjunto de dados para o SDK da Web do Experience Platform
description: 'Saiba como configurar os fluxos de dados. '
keywords: configuração; datastreams; datastreamId; edge; datastream id; Configurações do ambiente; edgeConfigId; identidade; sincronização de id ativada; ID do contêiner de sincronização de ID; Sandbox; Streaming Inlet; Conjunto de dados de eventos; target; código do cliente; ID do ambiente do Target; Destinos de cookies; Destinos de url; ID do conjunto de relatórios de bloqueio de configurações do Analytics;
exl-id: 736c75cb-e290-474e-8c47-2a031f215a56
source-git-commit: d3f1a6a5f3f10b8ccbe73ebc744dc60bbbf1bb07
workflow-type: tm+mt
source-wordcount: '1064'
ht-degree: 2%

---


# Configurar um conjunto de dados

A configuração do SDK da Web da Adobe Experience Platform é dividida entre dois lugares. O [comando configurar](configuring-the-sdk.md) no SDK controla os itens que devem ser manipulados no cliente, como o `edgeDomain`. Os datastreams lidam com todas as outras configurações do SDK. Quando uma solicitação é enviada para a rede de borda da Adobe Experience Platform, a variável `edgeConfigId` é usado para referenciar a configuração do lado do servidor. Isso permite atualizar a configuração sem precisar fazer alterações de código no site.

Sua organização deve ser provisionada para esse recurso. Entre em contato com o Gerente de sucesso do cliente (CSM) para obter informações sobre a lista de permissões.

## Criar uma configuração de armazenamento de dados

Você pode criar e gerenciar conjuntos de dados na interface do usuário da Coleta de dados selecionando **[!UICONTROL Datastreams]** no painel de navegação esquerdo.

![navegação de ferramentas de datastreams](../images/datastreams/config.png)

>[!NOTE]
>
>Ao acessar o [!UICONTROL Datastreams] independentemente de usar os recursos de gerenciamento de tags da Platform, você deve ter permissões de desenvolvedor para gerenciar os próprios conjuntos de dados. Consulte a [permissões do usuário](../../tags/ui/administration/user-permissions.md) na documentação das tags para obter mais detalhes.

Crie um armazenamento de dados clicando em **[!UICONTROL Novo fluxo de dados]** na área superior direita da tela. Depois de fornecer um nome e uma descrição, você é solicitado a fornecer as configurações padrão para cada ambiente. As configurações disponíveis são detalhadas abaixo.

Ao criar um armazenamento de dados, três ambientes são criados automaticamente com configurações idênticas. Esses três ambientes são *dev*, *estágio* e *prod*. Eles correspondem aos três ambientes padrão para tags. Ao criar uma biblioteca de tags em um ambiente de desenvolvimento, a biblioteca usa automaticamente o ambiente de desenvolvimento de sua configuração. Você pode editar as configurações em ambientes individuais tanto quanto desejar.

A ID usada no SDK como a `edgeConfigId` é uma ID composta que especifica a configuração e o ambiente (por exemplo, `1c86778b-cdba-4684-9903-750e52912ad1:stage`). Se nenhum ambiente estiver presente na ID composta (por exemplo, `stage` no exemplo anterior), o ambiente de produção é usado.

Abaixo estão as configurações disponíveis para cada ambiente de configuração. A maioria das seções pode ser ativada ou desativada. Quando desativadas, as configurações são salvas, mas não estão ativas.

## [!UICONTROL ID de terceiros] configurações

A seção ID de terceiros é a única seção que está sempre ativa. Ele tem duas configurações disponíveis: &quot;[!UICONTROL Sincronização de ID de terceiros ativada]&quot; e &quot;[!UICONTROL ID do contêiner de sincronização de ID de terceiros]&quot;.

![Seção de identidade da interface do usuário de configuração](../images/datastreams/edge_configuration_identity.png)

### [!UICONTROL Sincronização de ID de terceiros ativada]

Controla se o SDK executa ou não sincronizações de identidade com parceiros de terceiros.

### [!UICONTROL ID do contêiner de sincronização de ID de terceiros]

As sincronizações de ID podem ser agrupadas em contêineres para permitir que sincronizações de ID diferentes sejam executadas em momentos diferentes. Isso controla qual contêiner de sincronizações de ID é executado para uma determinada ID de configuração.

## Configurações do Adobe Experience Platform

As configurações listadas aqui permitem enviar dados para o Adobe Experience Platform. Você só deve ativar essa seção se tiver comprado a Adobe Experience Platform.

![Bloco de configurações do Adobe Experience Platform](../images/datastreams/platform-config.png)

| Campo | Descrição |
| --- | --- |
| [!UICONTROL Sandbox] | **(Obrigatório)** Selecione a sandbox da Platform para a qual deseja enviar dados. As sandboxes são partições virtuais no Adobe Experience Platform que permitem isolar seus dados e implementações de outras pessoas na organização. Para obter mais detalhes sobre como elas funcionam, consulte a [documentação das sandboxes](../../sandboxes/home.md). |
| [!UICONTROL Conjunto de dados do evento] | **(Obrigatório)** Selecione o conjunto de dados da plataforma para o qual os dados do evento do cliente serão transmitidos. Esse schema deve usar o [Classe XDM ExperienceEvent](../../xdm/classes/experienceevent.md). |
| [!UICONTROL Conjunto de dados de perfil] | Selecione o conjunto de dados da plataforma para o qual os dados do atributo do cliente serão enviados. Esse schema deve usar o [Classe de perfil individual XDM](../../xdm/classes/individual-profile.md). |
| [!UICONTROL Offer Decisioning] | Marque essa caixa de seleção para ativar o Offer Decisioning para uma implementação do SDK da Web da plataforma. Consulte o guia sobre [uso do Offer Decisioning com o SDK da Web da plataforma](../personalization/offer-decisioning/offer-decisioning-overview.md) para obter mais detalhes sobre a implementação. Para obter mais informações sobre recursos do Offer Decisioning, consulte [Documentação do Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started/starting-offer-decisioning.html?lang=pt-BR). |
| [!UICONTROL Segmentação de borda] | Marque essa caixa de seleção para ativar [segmentação de borda](../../segmentation/ui/edge-segmentation.md) para esse armazenamento de dados. Quando o SDK da Web da plataforma envia dados por meio de um conjunto de dados habilitado para a segmentação de borda, qualquer associação de segmento atualizada para o perfil em questão é enviada de volta na resposta.<br><br>Essa opção pode ser usada em combinação com [!UICONTROL Destinos de personalização] para [casos de uso de personalização de próxima página](../../destinations/ui/configure-personalization-destinations.md). |
| [!UICONTROL Destinos de personalização] | Quando usado em combinação com [!UICONTROL Segmentação de borda] , essa opção permite que o conjunto de dados se conecte a mecanismos de personalização como o Adobe Target. Consulte a documentação de destinos para obter etapas específicas sobre [configuração de destinos de personalização](../../destinations/ui/configure-personalization-destinations.md). |

## Configurações do Adobe Target

Para configurar o Adobe Target, você deve fornecer um código de cliente. Os outros campos são opcionais.

![Bloco de configurações do Adobe Target](../images/datastreams/edge_configuration_target.png)

>[!NOTE]
>
>A Organização associada ao código de cliente deve corresponder à organização em que a ID de configuração é criada.

### [!UICONTROL Código do cliente]

A ID exclusiva de uma conta de destino. Para encontrar isso, você pode navegar até [!UICONTROL Adobe Target] > [!UICONTROL Configuração]> [!UICONTROL Implementação] > [!UICONTROL editar configurações] ao lado do [!UICONTROL download] botão para [!UICONTROL at.js] ou [!UICONTROL mbox.js]

### [!UICONTROL Token de propriedade]

[!DNL Target] O permite que os clientes controlem permissões por meio do uso de propriedades do . Os detalhes podem ser encontrados no [Permissões empresariais](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html?lang=pt-BR) da seção [!DNL Target] documentação.

O token de propriedade pode ser encontrado em [!UICONTROL Adobe Target] > [!UICONTROL configuração] > [!UICONTROL Propriedades]

### [!UICONTROL ID do ambiente do Target]

[Ambientes](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html) no Adobe Target ajuda você a gerenciar a implementação em todos os estágios de desenvolvimento. Essa configuração especifica qual ambiente você usará com cada ambiente.

O Adobe recomenda definir isso de forma diferente para cada um de seus `dev`, `stage`e `prod` ambientes de fluxo de dados para simplificar as coisas. No entanto, se você já tiver ambientes Adobe Target definidos, poderá usá-los.

## Configurações do Adobe Audience Manager

Tudo o que é necessário para enviar dados para o Adobe Audience Manager é habilitar esta seção. As outras configurações são opcionais, mas são incentivadas.

![Bloco de configurações do Adobe Audience Manager](../images/datastreams/edge_configuration_aam.png)

### [!UICONTROL Destinos de cookies ativados]

Permite que o SDK compartilhe informações do segmento por meio de [Destinos de cookies](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-cookie-destination.html) from [!DNL Audience Manager].

### [!UICONTROL Destinos de URL ativados]

Permite que o SDK compartilhe informações do segmento por meio de [Destinos do URL](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-url-destination.html). Eles são configurados em [!DNL Audience Manager].

## Configurações do Adobe Analytics

Controla se os dados são enviados para o Adobe Analytics. Os detalhes adicionais estão no [Visão geral do Analytics](../data-collection/adobe-analytics/analytics-overview.md).

![Bloco de configurações do Adobe Analytics](../images/datastreams/edge_configuration_aa.png)

### [!UICONTROL ID de conjunto de relatórios]

O conjunto de relatórios pode ser encontrado na seção Admin do Adobe Analytics em [!UICONTROL Administração > ReportSuites]. Se vários conjuntos de relatórios forem especificados, os dados serão copiados para cada conjunto de relatórios.
