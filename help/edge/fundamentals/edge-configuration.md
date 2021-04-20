---
title: Criar uma configuração de borda para o SDK da Web do Experience Platform.
description: 'Saiba como configurar a Rede de borda do Experience Platform. '
keywords: configuração; borda; id de configuração de borda; Configurações do ambiente; edgeConfigId; identidade; sincronização de id habilitada; ID do contêiner de sincronização de ID; sandbox; entrada de fluxo; conjunto de dados de eventos; target; código do cliente; Token de propriedade; ID do ambiente do Target; Destinos de cookies; Destinos de url; Configurações do Analytics; ID do conjunto de relatórios do bloco;
exl-id: 736c75cb-e290-474e-8c47-2a031f215a56
translation-type: tm+mt
source-git-commit: d4ed6c8fa9c86eb2beec829ab24c381b665c2f03
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 2%

---

# Criar uma configuração de borda

A configuração do SDK da Web da Adobe Experience Platform é dividida entre dois lugares. O [configure command](configuring-the-sdk.md) no SDK controla os itens que devem ser manipulados no cliente, como o `edgeDomain`. A configuração de borda lida com todas as outras configurações do SDK. Quando uma solicitação é enviada para a Rede de borda do Adobe Experience Platform, o `edgeConfigId` é usado para fazer referência à configuração do lado do servidor. Isso permite atualizar a configuração sem precisar fazer alterações de código no site.

Sua organização deve ser provisionada para esse recurso. Entre em contato com o Gerente de sucesso do cliente (CSM) para obter informações sobre a lista de permissões.

## Criação de uma configuração de borda

As configurações de borda podem ser criadas no Adobe [!DNL Experience Platform Launch] usando a ferramenta de configuração de borda.

![navegação da ferramenta de configuração de borda](../../assets/edge_configuration_nav.png)

>[!NOTE]
>
>A ferramenta de configuração de borda está disponível para os clientes na lista de permissões, independentemente de usarem [!DNL Experience Platform Launch] como um gerenciador de tags. Além disso, os usuários exigem permissões de desenvolvimento em [!DNL Experience Platform Launch]. Consulte o artigo [Permissões do usuário](https://docs.adobe.com/content/help/pt-BR/launch/using/reference/admin/user-permissions.html) na documentação [!DNL Experience Platform Launch] para obter mais detalhes.

Crie uma configuração de borda clicando em **[!UICONTROL New Edge Configuration]** na área superior direita da tela. Depois de fornecer um nome e uma descrição, você é solicitado a fornecer as configurações padrão para cada ambiente. As configurações disponíveis são detalhadas abaixo.

Ao criar uma configuração de borda, três ambientes são criados automaticamente com configurações idênticas. Esses três ambientes são *dev*, *stage* e *prod*. Eles correspondem aos três ambientes padrão em [!DNL Experience Platform Launch]. Quando você cria uma biblioteca [!DNL Experience Platform Launch] em um ambiente de desenvolvimento, a biblioteca usa automaticamente o ambiente de desenvolvimento de sua configuração. Você pode editar as configurações em ambientes individuais tanto quanto desejar.

A ID usada no SDK como `edgeConfigId` é uma ID composta que especifica a configuração e o ambiente (por exemplo, `1c86778b-cdba-4684-9903-750e52912ad1:stage`). Se nenhum ambiente estiver presente na ID composta (por exemplo, `stage` no exemplo anterior), o ambiente de produção será usado.

Abaixo você encontrará as configurações disponíveis para cada ambiente de configuração. A maioria das seções pode ser ativada ou desativada. Quando desativadas, as configurações são salvas, mas não estão ativas.

## [!UICONTROL Third Party ID] Configurações

A seção ID de terceiros é a única seção que está sempre ativa. Ele tem duas configurações disponíveis: &quot;[!UICONTROL Third Party ID Sync Enabled]&quot; e &quot;[!UICONTROL Third Party ID Sync Container ID]&quot;.

![Seção de identidade da interface do usuário de configuração](../../assets/edge_configuration_identity.png)

### [!UICONTROL Third Party ID Sync Enabled]

Controla se o SDK executa ou não sincronizações de identidade com parceiros de terceiros.

### [!UICONTROL Third Party ID Sync Container ID]

As sincronizações de ID podem ser agrupadas em contêineres para permitir que sincronizações de ID diferentes sejam executadas em momentos diferentes. Isso controla qual contêiner de sincronizações de ID é executado para uma determinada ID de configuração.

## Configurações do Adobe Experience Platform

As configurações listadas aqui permitem enviar dados para o Adobe Experience Platform. Você só deve ativar essa seção se tiver comprado a Adobe Experience Platform.

![Bloco de configurações do Adobe Experience Platform](../../assets/edge_configuration_aep.png)

### [!UICONTROL Sandbox]

As sandboxes são locais na Adobe Experience Platform que permitem aos clientes isolar os dados e as implementações uns dos outros. Para obter mais detalhes sobre como elas funcionam, consulte a [documentação de sandboxes](../../sandboxes/home.md).

### [!UICONTROL Streaming Inlet]

Uma entrada de transmissão é uma fonte HTTP no Adobe Experience Platform. Eles são criados na guia &quot;[!UICONTROL Sources]&quot; no Adobe Experience Platform como uma API HTTP.

### [!UICONTROL Event Dataset]

As configurações de borda suportam o envio de dados para conjuntos de dados que têm um esquema de classe [!UICONTROL Experience Event].

## Configurações do Adobe Target

Para configurar o Adobe Target, você deve fornecer um código de cliente. Os outros campos são opcionais.

![Bloco de configurações do Adobe Target](../../assets/edge_configuration_target.png)

>[!NOTE]
>
>A Organização associada ao código de cliente deve corresponder à organização em que a ID de configuração é criada.

### [!UICONTROL Client Code]

A ID exclusiva de uma conta de destino. Para encontrar isso, você pode navegar até [!UICONTROL Adobe Target] > [!UICONTROL Setup] > [!UICONTROL Implementation] > [!UICONTROL edit settings] ao lado do botão [!UICONTROL download] para [!UICONTROL at.js] ou [!UICONTROL mbox.js]

### [!UICONTROL Property Token]

[!DNL Target] O permite que os clientes controlem permissões por meio do uso de propriedades do . Os detalhes podem ser encontrados na seção [Permissões empresariais](https://docs.adobe.com/content/help/pt-BR/target/using/administer/manage-users/enterprise/properties-overview.html) da documentação [!DNL Target].

O token de propriedade pode ser encontrado em [!UICONTROL Adobe Target] > [!UICONTROL setup] > [!UICONTROL Properties]

### [!UICONTROL Target Environment ID]

[](https://docs.adobe.com/content/help/en/target/using/administer/hosts.html) Os ambientes no Adobe Target ajudam você a gerenciar a implementação em todos os estágios de desenvolvimento. Essa configuração especifica qual ambiente você usará com cada ambiente.

O Adobe recomenda definir isso de forma diferente para cada um dos `dev`, `stage` e `prod` ambientes de configuração de borda para manter as coisas simples. No entanto, se você já tiver ambientes Adobe Target definidos, poderá usá-los.

## Configurações do Adobe Audience Manager

Tudo o que é necessário para enviar dados para o Adobe Audience Manager é habilitar esta seção. As outras configurações são opcionais, mas são incentivadas.

![Bloco de configurações do Adobe Audience Manager](../../assets/edge_configuration_aam.png)

### [!UICONTROL Cookie Destinations Enabled]

Permite que o SDK compartilhe informações do segmento por meio de [Destinos de cookies](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/destinations/custom-destinations/create-cookie-destination.html) de [!DNL Audience Manager].

### [!UICONTROL URL Destinations Enabled]

Permite que o SDK compartilhe informações do segmento por meio de [URL Destinations](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/destinations/custom-destinations/create-url-destination.html). Eles são configurados em [!DNL Audience Manager].

## Configurações do Adobe Analytics

Controla se os dados são enviados para o Adobe Analytics. Detalhes adicionais estão na [Visão geral do Analytics](../data-collection/adobe-analytics/analytics-overview.md).

![Bloco de configurações do Adobe Analytics](../../assets/edge_configuration_aa.png)

### [!UICONTROL Report Suite ID]

O conjunto de relatórios pode ser encontrado na seção Admin do Adobe Analytics em [!UICONTROL Admin > ReportSuites]. Se vários conjuntos de relatórios forem especificados, os dados serão copiados para cada conjunto de relatórios.
