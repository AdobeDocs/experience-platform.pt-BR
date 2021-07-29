---
title: Configurar o conjunto de dados para o SDK da Web do Experience Platform
description: 'Saiba como configurar os fluxos de dados. '
keywords: configuração; datastreams; datastreamId; edge; datastream id; Configurações do ambiente; edgeConfigId; identidade; sincronização de id ativada; ID do contêiner de sincronização de ID; Sandbox; Streaming Inlet; Conjunto de dados de eventos; target; código do cliente; ID do ambiente do Target; Destinos de cookies; Destinos de url; ID do conjunto de relatórios de bloqueio de configurações do Analytics;
exl-id: 736c75cb-e290-474e-8c47-2a031f215a56
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '901'
ht-degree: 1%

---


# Configurar um conjunto de dados

A configuração do SDK da Web da Adobe Experience Platform é dividida entre dois lugares. O [configure command](configuring-the-sdk.md) no SDK controla os itens que devem ser manipulados no cliente, como o `edgeDomain`. Os datastreams lidam com todas as outras configurações do SDK. Quando uma solicitação é enviada para a Rede de borda do Adobe Experience Platform, o `edgeConfigId` é usado para fazer referência à configuração do lado do servidor. Isso permite atualizar a configuração sem precisar fazer alterações de código no site.

Sua organização deve ser provisionada para esse recurso. Entre em contato com o Gerente de sucesso do cliente (CSM) para obter informações sobre a lista de permissões.

## Criação de uma configuração de conjunto de dados

Os conjuntos de dados podem ser criados na interface do usuário da Coleta de dados usando a ferramenta de configuração do conjunto de dados.

![navegação de ferramentas de datastreams](../images/datastreams/config.png)

>[!NOTE]
>
>A ferramenta de configuração de conjuntos de dados está disponível para os clientes na lista de permissões, independentemente de usarem a Platform como um gerenciador de tags. Além disso, os usuários exigem permissões de desenvolvimento. Consulte o artigo [permissões do usuário](../../tags/ui/administration/user-permissions.md) na documentação das tags para obter mais detalhes.

Crie um armazenamento de dados clicando em **[!UICONTROL New Datastream]** na área superior direita da tela. Depois de fornecer um nome e uma descrição, você é solicitado a fornecer as configurações padrão para cada ambiente. As configurações disponíveis são detalhadas abaixo.

Ao criar um armazenamento de dados, três ambientes são criados automaticamente com configurações idênticas. Esses três ambientes são *dev*, *stage* e *prod*. Eles correspondem aos três ambientes padrão para tags. Ao criar uma biblioteca de tags em um ambiente de desenvolvimento, a biblioteca usa automaticamente o ambiente de desenvolvimento de sua configuração. Você pode editar as configurações em ambientes individuais tanto quanto desejar.

A ID usada no SDK como `edgeConfigId` é uma ID composta que especifica a configuração e o ambiente (por exemplo, `1c86778b-cdba-4684-9903-750e52912ad1:stage`). Se nenhum ambiente estiver presente na ID composta (por exemplo, `stage` no exemplo anterior), o ambiente de produção será usado.

Abaixo estão as configurações disponíveis para cada ambiente de configuração. A maioria das seções pode ser ativada ou desativada. Quando desativadas, as configurações são salvas, mas não estão ativas.

## [!UICONTROL Configurações ] IDS de terceiros

A seção ID de terceiros é a única seção que está sempre ativa. Ele tem duas configurações disponíveis: &quot;[!UICONTROL Sincronização de ID de terceiros ativada]&quot; e &quot;[!UICONTROL ID do contêiner de sincronização de ID de terceiros]&quot;.

![Seção de identidade da interface do usuário de configuração](../images/datastreams/edge_configuration_identity.png)

### [!UICONTROL Sincronização de ID de terceiros ativada]

Controla se o SDK executa ou não sincronizações de identidade com parceiros de terceiros.

### [!UICONTROL ID do contêiner de sincronização de ID de terceiros]

As sincronizações de ID podem ser agrupadas em contêineres para permitir que sincronizações de ID diferentes sejam executadas em momentos diferentes. Isso controla qual contêiner de sincronizações de ID é executado para uma determinada ID de configuração.

## Configurações do Adobe Experience Platform

As configurações listadas aqui permitem enviar dados para o Adobe Experience Platform. Você só deve ativar essa seção se tiver comprado a Adobe Experience Platform.

![Bloco de configurações do Adobe Experience Platform](../images/datastreams/edge_configuration_aep.png)

### [!UICONTROL Sandbox]

As sandboxes são locais na Adobe Experience Platform que permitem aos clientes isolar os dados e as implementações uns dos outros. Para obter mais detalhes sobre como elas funcionam, consulte a [documentação de sandboxes](../../sandboxes/home.md).

### [!UICONTROL Entrada de transmissão]

Uma entrada de transmissão é uma fonte HTTP no Adobe Experience Platform. Eles são criados na guia &quot;[!UICONTROL Sources]&quot; no Adobe Experience Platform como uma API HTTP.

### [!UICONTROL Conjunto de dados do evento]

Os datastreams suportam o envio de dados para conjuntos de dados que têm um esquema da classe [!UICONTROL Experience Event].

## Configurações do Adobe Target

Para configurar o Adobe Target, você deve fornecer um código de cliente. Os outros campos são opcionais.

![Bloco de configurações do Adobe Target](../images/datastreams/edge_configuration_target.png)

>[!NOTE]
>
>A Organização associada ao código de cliente deve corresponder à organização em que a ID de configuração é criada.

### [!UICONTROL Código do cliente]

A ID exclusiva de uma conta de destino. Para encontrar isso, você pode navegar até [!UICONTROL Adobe Target] > [!UICONTROL Configuração] [!UICONTROL Implementação] > [!UICONTROL editar configurações] ao lado do botão [!UICONTROL baixar] para [!UICONTROL at.js] ou &lt;a1 2/>mbox.js][!UICONTROL 

### [!UICONTROL Token de propriedade]

[!DNL Target] O permite que os clientes controlem permissões por meio do uso de propriedades do . Os detalhes podem ser encontrados na seção [Permissões empresariais](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html?lang=pt-BR) da documentação [!DNL Target].

O token de propriedade pode ser encontrado em [!UICONTROL Adobe Target] > [!UICONTROL configuração] > [!UICONTROL Propriedades]

### [!UICONTROL ID do ambiente do Target]

[](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html) Os ambientes no Adobe Target ajudam você a gerenciar a implementação em todos os estágios de desenvolvimento. Essa configuração especifica qual ambiente você usará com cada ambiente.

O Adobe recomenda definir isso de forma diferente para cada um dos ambientes de armazenamento de dados `dev`, `stage` e `prod` para simplificar as coisas. No entanto, se você já tiver ambientes Adobe Target definidos, poderá usá-los.

## Configurações do Adobe Audience Manager

Tudo o que é necessário para enviar dados para o Adobe Audience Manager é habilitar esta seção. As outras configurações são opcionais, mas são incentivadas.

![Bloco de configurações do Adobe Audience Manager](../images/datastreams/edge_configuration_aam.png)

### [!UICONTROL Destinos de cookies ativados]

Permite que o SDK compartilhe informações do segmento por meio de [Destinos de cookies](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-cookie-destination.html) de [!DNL Audience Manager].

### [!UICONTROL Destinos de URL ativados]

Permite que o SDK compartilhe informações do segmento por meio de [URL Destinations](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-url-destination.html). Eles são configurados em [!DNL Audience Manager].

## Configurações do Adobe Analytics

Controla se os dados são enviados para o Adobe Analytics. Detalhes adicionais estão na [Visão geral do Analytics](../data-collection/adobe-analytics/analytics-overview.md).

![Bloco de configurações do Adobe Analytics](../images/datastreams/edge_configuration_aa.png)

### [!UICONTROL ID de conjunto de relatórios]

O conjunto de relatórios pode ser encontrado na seção Admin do Adobe Analytics em [!UICONTROL Admin > ReportSuites]. Se vários conjuntos de relatórios forem especificados, os dados serão copiados para cada conjunto de relatórios.
