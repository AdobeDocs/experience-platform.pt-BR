---
title: Visão geral dos conjuntos de dados
description: Conecte sua integração do SDK da Experience Platform do lado do cliente aos produtos da Adobe e destinos de terceiros.
keywords: configuração; datastreams; datastreamId; edge; datastream id; Configurações do ambiente; edgeConfigId; identidade; sincronização de id ativada; ID do contêiner de sincronização de ID; Sandbox; Streaming Inlet; Conjunto de dados de eventos; target; código do cliente; ID do ambiente do Target; Destinos de cookies; Destinos de url; ID do conjunto de relatórios de configurações do Analytics; Predefinição de dados para dados Coleção; Preparação de dados; Mapeador; Mapeador XDM; Mapeador no Edge;
exl-id: 736c75cb-e290-474e-8c47-2a031f215a56
source-git-commit: fe66cbd61d546da8fb6621ef78b3565126cb193d
workflow-type: tm+mt
source-wordcount: '1686'
ht-degree: 2%

---

# Visão geral dos conjuntos de dados

Um armazenamento de dados representa a configuração do lado do servidor ao implementar os SDKs móveis e da Web do Adobe Experience Platform. Enquanto a variável [comando configurar](../fundamentals/configuring-the-sdk.md) no SDK controla os itens que devem ser manipulados no cliente (como `edgeDomain`), os conjuntos de dados lidam com todas as outras configurações do SDK. Quando uma solicitação é enviada para a rede de borda da Adobe Experience Platform, a variável `edgeConfigId` é usada para fazer referência ao armazenamento de dados. Isso permite atualizar a configuração do lado do servidor sem precisar fazer alterações de código no site.

Este documento aborda as etapas para configurar um armazenamento de dados na interface do usuário da coleta de dados.

>[!NOTE]
>
>Sua organização deve ser provisionada para esse recurso para acessá-lo na interface do usuário do . Preencha o seguinte [formulário](https://adobe.ly/websdkaccess) para solicitar o acesso necessário. Para gerenciar conjuntos de dados, sua conta de usuário deve ser adicionada a um perfil de produto para tags em [!DNL Adobe Experience Platform].

## Acesse o [!UICONTROL Datastreams] espaço de trabalho

Você pode criar e gerenciar conjuntos de dados na interface do usuário da Coleta de dados selecionando **[!UICONTROL Datastreams]** no painel de navegação esquerdo.

![Guia Datastreams na interface do usuário da coleta de dados](../images/datastreams/overview/datastreams-tab.png)

O [!UICONTROL Datastreams] A guia exibe uma lista de conjuntos de dados existentes, incluindo o nome amigável, a ID e a data da última modificação. Selecione o nome de um armazenamento de dados para [exibir seus detalhes e configurar serviços](#view-details).

Selecione o ícone &quot;mais&quot; (**...**) para um armazenamento de dados específico revelar mais opções. Selecionar **[!UICONTROL Editar]** para atualizar o [configuração básica](#configure) para o armazenamento de dados, ou selecione **[!UICONTROL Excluir]** para remover o armazenamento de dados.

![Opções para editar ou excluir o conjunto de dados existente](../images/datastreams/overview/edit-datastream.png)

## Criar um novo armazenamento de dados {#create}

Para criar um armazenamento de dados, comece selecionando **[!UICONTROL Novo fluxo de dados]**.

![Selecionar novo fluxo de dados](../images/datastreams/overview/new-datastream-button.png)

O fluxo de trabalho de criação do armazenamento de dados é exibido, começando na etapa de configuração. Aqui, você deve fornecer um nome e uma descrição opcional para o armazenamento de dados.

Se você estiver configurando esse armazenamento de dados para uso no Experience Platform e estiver usando o SDK da Web da plataforma, também deverá selecionar um [esquema do Experience Data Model (XDM) baseado em eventos](../../xdm/classes/experienceevent.md) para representar os dados que você planeja assimilar.

![Configuração básica para um armazenamento de dados](../images/datastreams/overview/configure.png)

Selecionar **[!UICONTROL Opções avançadas]** para revelar controles adicionais para configurar o conjunto de dados.

![Opções de configuração avançadas](../images/datastreams/overview/advanced-options.png)

| Configuração | Descrição |
| --- | --- |
| [!UICONTROL Localização geográfica] | Determina se as pesquisas de GPS ocorrem com base no endereço IP do usuário. A configuração padrão **[!UICONTROL Nenhum]** desativa qualquer pesquisa de GPS, enquanto a variável **[!UICONTROL Cidade]** A configuração fornece coordenadas GPS com duas casas decimais. |
| [!UICONTROL Cookie da ID própria] | Quando habilitada, essa configuração informa à Edge Network para fazer referência a um cookie especificado ao pesquisar um [ID de dispositivo próprio](../identity/first-party-device-ids.md), em vez de pesquisar esse valor no Mapa de identidade.<br><br>Ao ativar essa configuração, você deve fornecer o nome do cookie no qual a ID deve ser armazenada. |
| [!UICONTROL Sincronização de ID de terceiros] | As sincronizações de ID podem ser agrupadas em contêineres para permitir que sincronizações de ID diferentes sejam executadas em momentos diferentes. Quando ativada, essa configuração permite especificar qual contêiner de sincronizações de ID é executado para esse armazenamento de dados. |

A partir daqui, se você estiver configurando seu conjunto de dados para o Experience Platform, siga o tutorial em [Preparação de dados para coleta de dados](./data-prep.md) para mapear seus dados para um esquema de evento da plataforma antes de retornar a este guia. Caso contrário, selecione **[!UICONTROL Salvar]** e continue para a próxima seção.

## Exibir detalhes do armazenamento de dados {#view-details}

Após configurar um novo armazenamento de dados ou selecionar um existente para exibir, a página de detalhes desse armazenamento de dados será exibida. Aqui você pode encontrar mais informações sobre o armazenamento de dados, incluindo sua ID.

![Página de detalhes de um armazenamento de dados criado](../images/datastreams/overview/view-details.png)

Na tela de detalhes do armazenamento de dados, é possível [adicionar serviços](#add-services) para ativar os recursos dos produtos da Adobe Experience Cloud aos quais você tem acesso. Também é possível editar o armazenamento de dados [configuração básica](#create), atualizar [regras de mapeamento](./data-prep.md), [copiar o datastream](#copy)ou exclua-a totalmente.

## Adicionar serviços a um armazenamento de dados {#add-services}

Na página de detalhes de um armazenamento de dados, selecione **[!UICONTROL Adicionar Serviço]** para começar a adicionar os serviços disponíveis para esse armazenamento de dados.

![Selecione Adicionar serviço para continuar](../images/datastreams/overview/add-service.png)

Na próxima tela, use o menu suspenso para selecionar um serviço a ser configurado para esse armazenamento de dados. Somente os serviços aos quais você tem acesso serão exibidos nesta lista.

![Selecione um serviço na lista](../images/datastreams/overview/service-selection.png)

Selecione o serviço desejado, preencha as opções de configuração exibidas e selecione **[!UICONTROL Salvar]** para adicionar o serviço ao armazenamento de dados. Todos os serviços adicionados aparecem na visualização de detalhes do armazenamento de dados.

![Serviços adicionados a um armazenamento de dados](../images/datastreams/overview/services-added.png)

As subseções abaixo descrevem as opções de configuração para cada serviço.

>[!NOTE]
>
>Cada configuração de serviço contém um **[!UICONTROL Ativado]** alternar que é ativado automaticamente quando o serviço é selecionado. Para desabilitar o serviço selecionado para esse armazenamento de dados, selecione o **[!UICONTROL Ativado]** alternar novamente.

### Configurações do Adobe Analytics

Esse serviço controla se e como os dados são enviados para a Adobe Analytics. Podem ser encontrados detalhes adicionais no guia sobre [envio de dados para o Analytics](../data-collection/adobe-analytics/analytics-overview.md).

![Bloco de configurações do Adobe Analytics](../images/datastreams/overview/analytics-config.png)

| Configuração | Descrição |
| --- | --- |
| [!UICONTROL ID de conjunto de relatórios] | **(Obrigatório)** A ID do conjunto de relatórios do Analytics para o qual você deseja enviar dados. Essa ID pode ser encontrada na interface do usuário do Adobe Analytics em [!UICONTROL Administrador] > [!UICONTROL ReportSuites]. Se vários conjuntos de relatórios forem especificados, os dados serão copiados para cada conjunto de relatórios. |

### Configurações do Adobe Audience Manager

Esse serviço controla se e como os dados são enviados para a Adobe Audience Manager. Tudo o que é necessário para enviar dados para o Audience Manager é habilitar esta seção. As outras configurações são opcionais, mas são incentivadas.

![Bloco de configurações do Adobe Audience Manager](../images/datastreams/overview/audience-manager-config.png)

| Configuração | Descrição |
| --- | --- |
| [!UICONTROL Destinos de cookies ativados] | Permite que o SDK compartilhe informações do segmento por meio de [destinos de cookie](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-cookie-destination.html) from [!DNL Audience Manager]. |
| [!UICONTROL Destinos de URL ativados] | Permite que o SDK compartilhe informações do segmento por meio de [Destinos de URL](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-url-destination.html) from [!DNL Audience Manager]. |

### Configurações do Adobe Experience Platform

>[!IMPORTANT]
>
>Ao ativar um conjunto de dados para a Platform, observe a sandbox da Platform que você está usando no momento, como exibido na faixa superior da interface do usuário de coleta de dados.
>
>![Sandbox selecionada](../images/datastreams/overview/platform-sandbox.png)
>
>As sandboxes são partições virtuais no Adobe Experience Platform que permitem isolar seus dados e implementações de outras pessoas na organização. Depois que um conjunto de dados é criado, sua sandbox não pode ser alterada. Para obter mais detalhes sobre a função das sandboxes no Experience Platform, consulte o [documentação das sandboxes](../../sandboxes/home.md).

Esse serviço controla se e como os dados são enviados para a Adobe Experience Platform.

![Bloco de configurações do Adobe Experience Platform](../images/datastreams/overview/platform-config.png)

| Configuração | Descrição |
| --- | --- |
| [!UICONTROL Conjunto de dados do evento] | **(Obrigatório)** Selecione o conjunto de dados da plataforma para o qual os dados do evento do cliente serão transmitidos. Esse schema deve usar o [Classe XDM ExperienceEvent](../../xdm/classes/experienceevent.md). |
| [!UICONTROL Conjunto de dados de perfil] | Selecione o conjunto de dados da plataforma para o qual os dados do atributo do cliente serão enviados. Esse schema deve usar o [Classe de perfil individual XDM](../../xdm/classes/individual-profile.md). |
| [!UICONTROL Offer Decisioning] | Marque essa caixa de seleção para ativar o Offer Decisioning para uma implementação do SDK da Web da plataforma. Consulte o guia sobre [uso do Offer Decisioning com o SDK da Web da plataforma](../personalization/offer-decisioning/offer-decisioning-overview.md) para obter mais detalhes sobre a implementação. Para obter mais informações sobre recursos do Offer Decisioning, consulte [Documentação do Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started/starting-offer-decisioning.html?lang=pt-BR). |
| [!UICONTROL Segmentação de borda] | Marque essa caixa de seleção para ativar [segmentação de borda](../../segmentation/ui/edge-segmentation.md) para esse armazenamento de dados. Quando o SDK envia dados por meio de um conjunto de dados habilitado para a segmentação de borda, qualquer associação de segmento atualizada para o perfil em questão é enviada de volta na resposta.<br><br>Essa opção pode ser usada em combinação com [!UICONTROL Destinos de personalização] para [casos de uso de personalização de próxima página](../../destinations/ui/configure-personalization-destinations.md). |
| [!UICONTROL Destinos de personalização] | Quando usado em combinação com [!UICONTROL Segmentação de borda] , essa opção permite que o conjunto de dados se conecte a mecanismos de personalização como o Adobe Target. Consulte a documentação de destinos para obter etapas específicas sobre [configuração de destinos de personalização](../../destinations/ui/configure-personalization-destinations.md). |

### Configurações do Adobe Target {#target}

Esse serviço controla se e como os dados são enviados para a Adobe Target.

![Bloco de configurações do Adobe Target](../images/datastreams/overview/target-config.png)

| Configuração | Descrição |
| --- | --- |
| [!UICONTROL Token de propriedade] | [!DNL Target] O permite que os clientes controlem permissões por meio do uso de propriedades do . Para obter mais informações sobre propriedades, consulte o guia sobre [configuração de permissões empresariais](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html?lang=pt-BR) no [!DNL Target] documentação.<br><br>O token de propriedade pode ser encontrado na interface do usuário do Adobe Target em [!UICONTROL Configuração] > [!UICONTROL Propriedades]. |
| [!UICONTROL ID do ambiente do Target] | [Ambientes no Adobe Target](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html) Ajudar você a gerenciar sua implementação em todos os estágios de desenvolvimento. Essa configuração especifica qual ambiente você usará com esse conjunto de dados.<br><br>A prática recomendada é definir isso de forma diferente para cada um de seus `dev`, `stage`e `prod` ambientes de fluxo de dados para simplificar as coisas. No entanto, se você já tiver ambientes Adobe Target definidos, poderá usá-los. |
| [!UICONTROL Namespace da ID de terceiros do Target] | O namespace de identidade do `mbox3rdPartyId` você deseja usar para esse armazenamento de dados. Consulte o guia sobre [implementação `mbox3rdPartyId` com o SDK da Web](../personalization/adobe-target/using-mbox-3rdpartyid.md) para obter mais informações. |

### [!UICONTROL Encaminhamento de evento] configurações

Esse serviço controla se e como os dados são enviados para [encaminhamento de eventos](../../tags/ui/event-forwarding/overview.md).

![Seção Encaminhamento de eventos da interface do usuário de configuração](../images/datastreams/overview/event-forwarding-config.png)

| Configuração | Descrição |
| --- | --- |
| [!UICONTROL Propriedade do Launch] | **(Obrigatório)** A propriedade de encaminhamento de evento para a qual você deseja enviar dados. |
| [!UICONTROL Ambiente do Launch] | **(Obrigatório)** O ambiente na propriedade selecionada para a qual você deseja enviar dados. |

>[!NOTE]
>
>Você pode selecionar **[!UICONTROL Inserir IDs manualmente]** para digitar os nomes da propriedade e do ambiente em vez de usar os menus suspensos.

## Copiar um conjunto de dados {#copy}

Você pode criar uma cópia de um conjunto de dados existente e alterar seus detalhes, conforme necessário.

>[!NOTE]
>
>Os conjuntos de dados só podem ser copiados dentro do mesmo [sandbox](../../sandboxes/home.md). Em outras palavras, não é possível copiar um armazenamento de dados de uma sandbox para outra.

Na página principal do [!UICONTROL Datastreams] no espaço de trabalho, selecione as reticências (**....**) para o armazenamento de dados em questão, selecione **[!UICONTROL Copiar]**.

![Imagem que mostra o [!UICONTROL Copiar] opção sendo selecionada na exibição de lista do armazenamento de dados](../images/datastreams/overview/copy-datastream-list.png)

Como alternativa, você pode selecionar **[!UICONTROL Copiar fluxo de dados]** na exibição de detalhes de um determinado conjunto de dados.

![Imagem que mostra o [!UICONTROL Copiar] opção sendo selecionada na visualização de detalhes do armazenamento de dados](../images/datastreams/overview/copy-datastream-details.png)

Uma caixa de diálogo de confirmação é exibida, solicitando que você forneça um nome exclusivo para o novo armazenamento de dados a ser criado, juntamente com detalhes sobre as opções de configuração que serão copiadas. Quando estiver pronto, selecione **[!UICONTROL Copiar]**.

![Imagem da caixa de diálogo de confirmação para copiar um conjunto de dados](../images/datastreams/overview/copy-datastream-confirm.png)

A página principal do [!UICONTROL Datastreams] o workspace é exibido novamente com o novo datastream listado.

## Próximas etapas

Este guia cobriu como gerenciar conjuntos de dados na interface do usuário da Coleta de dados. Para obter mais informações sobre como instalar e configurar o SDK da Web após configurar um conjunto de dados, consulte o [Guia E2E de coleta de dados](../../collection/e2e.md#install).
