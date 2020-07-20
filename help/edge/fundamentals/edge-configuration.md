---
title: Configuração do Edge
seo-title: Configuração de borda para o SDK da Web Experience Platform
description: 'Saiba como configurar a rede Experience Platform Edge. '
seo-description: 'Saiba como configurar a rede Experience Platform Edge. '
translation-type: tm+mt
source-git-commit: 7b07a974e29334cde2dee7027b9780a296db7b20
workflow-type: tm+mt
source-wordcount: '870'
ht-degree: 2%

---


# Configuração do Edge

A configuração do Adobe Experience Platform [!DNL Web SDK] é dividida entre dois locais. O comando [configure](configuring-the-sdk.md) no SDK controla os itens que devem ser manipulados no cliente, como o `edgeDomain`. A configuração da borda lida com todas as outras configurações do SDK. Quando uma solicitação é enviada para o Adobe Experience Platform [!DNL Edge Network], o `edgeConfigId` é usado para fazer referência à configuração do lado do servidor. Isso permite que você atualize a configuração sem precisar fazer alterações de código em seu site.

## Criando uma ID de configuração de borda

As IDs de configuração de borda podem ser criadas no Adobe [!DNL Launch] usando a ferramenta de configuração de borda. Essa ferramenta permite criar a configuração da borda, bem como ambientes nessas configurações.

![navegação da ferramenta de configuração de borda](../../assets/edge_configuration_nav.png)

>[!NOTE]
>
>
>
>A ferramenta de configuração de borda está disponível para os clientes na lista de permissões, independentemente de usarem [!DNL Launch] como gerenciador de tags. Além disso, os usuários exigem permissões de Desenvolvimento em [!DNL Launch]. Consulte o artigo Permissões [do](https://docs.adobe.com/content/help/pt-BR/launch/using/reference/admin/user-permissions.html) usuário na [!DNL Launch] documentação para obter mais detalhes.

Você pode criar uma configuração de borda clicando em **[!UICONTROL Nova configuração]** de borda na área superior direita da tela. Depois de fornecer um nome e uma descrição, você será solicitado a fornecer as configurações padrão para cada ambiente.

### Configurações de Ambiente padrão

Essas configurações padrão são usadas para criar os três primeiros ambientes com configurações idênticas. Esses três ambientes são *dev*, *stage* e *prod*. Eles correspondem aos três ambientes padrão em [!DNL Launch]. Quando você cria uma [!DNL Launch] biblioteca para um ambiente dev, a biblioteca usa automaticamente o ambiente dev de sua configuração. Você pode editar as configurações em ambientes individuais tanto quanto desejar.

A ID usada no SDK como `edgeConfigId` é uma ID composta que especifica a configuração e o ambiente. Se nenhum ambiente estiver presente, o ambiente de produção será usado.

### Configurações do Ambiente

Abaixo estão cada uma das configurações disponíveis para um ambiente. A maioria das seções pode ser ativada ou desativada. Quando desativadas, suas configurações são salvas, mas não estão ativas.

#### [!UICONTROL Identidade]

A seção de identidade é a única seção que está sempre ativada. Ele tem duas configurações disponíveis: [!UICONTROL Sincronizações de ID ativadas] e ID [!UICONTROL de Container de sincronização de]ID.

![Seção de identidade da interface de usuário de configuração](../../assets/edge_configuration_identity.png)

##### [!UICONTROL Sincronização de ID ativada]

Controla se o SDK realiza ou não sincronizações de identidade com parceiros de terceiros.

##### [!UICONTROL ID do Container de sincronização de ID]

As sincronizações de ID podem ser agrupadas em container para permitir que sincronizações de ID diferentes sejam executadas em momentos diferentes. Isso controla qual container de sincronização de ID é executado para uma determinada ID de configuração.

#### Adobe Experience Platform

As configurações listadas aqui permitem que você envie dados para o Adobe Experience Platform. Você só deverá ativar esta seção se tiver comprado o Adobe Experience Platform.

![bloco de configurações Adobe Experience Platform](../../assets/edge_configuration_aep.png)

##### [!UICONTROL Sandbox]

As caixas de proteção são locais no Adobe Experience Platform que permitem que os clientes isolem seus dados e implementações uns dos outros. Para obter mais detalhes sobre como funcionam, consulte a documentação [](../../sandboxes/home.md)Sandboxes.

##### [!UICONTROL Entrada de fluxo]

Uma entrada de fluxo contínuo é uma fonte HTTP no Adobe Experience Platform. Eles são criados na guia [!UICONTROL Fontes] no Adobe Experience Platform como uma API HTTP.

##### [!UICONTROL Conjunto de dados do Evento]

As configurações de borda suportam o envio de dados para conjuntos de dados com um schema de  de classe do [!UICONTROL Experience Evento].

#### Adobe Target

Para configurar o Adobe Target, você deve fornecer um código de cliente. Os outros campos são opcionais.

![bloco de configurações Adobe Target](../../assets/edge_configuration_target.png)

>[!NOTE]
>
>
>
>A Organização associada ao código do cliente deve corresponder à organização em que a ID de configuração é criada.

##### [!UICONTROL Código do cliente]

A ID exclusiva de uma conta de público alvo. Para encontrar isso, você pode navegar até [!UICONTROL Adobe Target] > [!UICONTROL Configuração]> [!UICONTROL Implementação] > [!UICONTROL editar configurações] ao lado do botão [!UICONTROL de download]  [!UICONTROL para o arquivo at.js ou o arquivo mbox.js]

##### [!UICONTROL Token de propriedade]

[!DNL Target] permite que os clientes controlem permissões por meio do uso de propriedades. Os detalhes podem ser encontrados na seção Permissões [](https://docs.adobe.com/content/help/en/target/using/administer/manage-users/enterprise/properties-overview.html) empresariais da [!DNL Target] documentação.

O token de propriedade pode ser encontrado em [!UICONTROL Adobe Target] > [!UICONTROL configuração] > [!UICONTROL Propriedades]

##### [!UICONTROL ID do Ambiente do Público alvo]

[Ambientes](https://docs.adobe.com/content/help/en/target/using/administer/hosts.html) no Adobe Target ajudam você a gerenciar sua implementação em todos os estágios de desenvolvimento. Essa configuração especifica qual ambiente você usará com cada ambiente.

A Adobe recomenda configurar isso de forma diferente para cada um dos seus ambientes de configuração de `dev`borda, `stage`e `prod` para manter as coisas simples. No entanto, se você já tiver ambientes  Adobe Target definidos, poderá usá-los.

#### Adobe Audience Manager

Tudo o que é necessário para enviar dados ao Adobe Audience Manager é ativar esta seção. As outras configurações são opcionais, mas são recomendadas.

![Bloco de configurações do Adobe Audiência Manage](../../assets/edge_configuration_aam.png)

##### [!UICONTROL Destinos de cookies ativados]

Permite que o SDK compartilhe informações do segmento por meio dos Destinos [de](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/destinations/custom-destinations/create-cookie-destination.html) cookies [!DNL Audience Manager].

##### [!UICONTROL Destinos de URL ativados]

Permite que o SDK compartilhe informações do segmento por meio de Destinos [de](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/destinations/custom-destinations/create-url-destination.html)URL. Eles estão configurados em [!DNL Audience Manager].

#### Adobe Analytics

Controla se os dados são enviados para o Adobe Analytics. Detalhes adicionais estão na Visão geral [do](../solution-specific/analytics/analytics-overview.md)Analytics.

![Bloco de configurações do Adobe Analytics](../../assets/edge_configuration_aa.png)

##### [!UICONTROL ID de conjunto de relatórios]

O conjunto de relatórios pode ser encontrado na seção Adobe Analytics Admin em [!UICONTROL Admin > ReportSuites]. Se vários conjuntos de relatórios forem especificados, os dados serão copiados para cada conjunto de relatórios.
