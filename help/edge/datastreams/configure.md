---
title: Configurar uma sequência de dados
description: Saiba como conectar a integração do SDK da Web do lado do cliente com outros produtos do Adobe e destinos de terceiros.
exl-id: 4924cd0f-5ec6-49ab-9b00-ec7c592397c8
source-git-commit: 3de929fb17f8b0b6ca4f6f2c7dd0c5a9a26001b2
workflow-type: tm+mt
source-wordcount: '2116'
ht-degree: 2%

---


# Configurar uma sequência de dados

Este documento aborda as etapas para configurar um [datastream](./overview.md) na interface do usuário do .

## Acesse o [!UICONTROL Datastreams] espaço de trabalho

Você pode criar e gerenciar conjuntos de dados na interface do usuário da coleta de dados ou na interface do usuário do Experience Platform selecionando **[!UICONTROL Datastreams]** no painel de navegação esquerdo.

![Guia Datastreams na interface do usuário da coleta de dados](../assets/datastreams/configure/datastreams-tab.png)

O **[!UICONTROL Datastreams]** A guia exibe uma lista de conjuntos de dados existentes, incluindo o nome amigável, a ID e a data da última modificação. Selecione o nome de um armazenamento de dados para [exibir seus detalhes e configurar serviços](#view-details).

Selecione o ícone &quot;mais&quot; (**...**) para um armazenamento de dados específico revelar mais opções. Selecionar **[!UICONTROL Editar]** para atualizar o [configuração básica](#configure) para o armazenamento de dados, ou selecione **[!UICONTROL Excluir]** para remover o armazenamento de dados.

![Opções para editar ou excluir um conjunto de dados existente](../assets/datastreams/configure/edit-datastream.png)

## Criar um novo armazenamento de dados {#create}

Para criar um armazenamento de dados, comece selecionando **[!UICONTROL Novo fluxo de dados]**.

![Selecione Novo fluxo de dados](../assets/datastreams/configure/new-datastream-button.png)

O fluxo de trabalho de criação do armazenamento de dados é exibido, começando na etapa de configuração. Aqui, você deve fornecer um nome e uma descrição opcional para o armazenamento de dados.

Se você estiver configurando esse armazenamento de dados para uso no Experience Platform e estiver usando o SDK da Web da plataforma, também deverá selecionar um [esquema do Experience Data Model (XDM) baseado em eventos](../../xdm/classes/experienceevent.md) para representar os dados que você planeja assimilar.

![Configuração básica para um armazenamento de dados](../assets/datastreams/configure/configure.png)

Selecionar **[!UICONTROL Opções avançadas]** para revelar controles adicionais para configurar o conjunto de dados.

![Opções de configuração avançadas](../assets/datastreams/configure/advanced-options.png) {#advanced-options}

| Configuração | Descrição |
| --- | --- |
| [!UICONTROL Localização geográfica] | Determina se as pesquisas de geolocalização ocorrem com base no endereço IP do usuário. A configuração padrão **[!UICONTROL Nenhum]** desativa qualquer pesquisa de geolocalização, enquanto a variável **[!UICONTROL Cidade]** A configuração fornece coordenadas GPS com duas casas decimais. A geolocalização ocorre antes de [!UICONTROL Ofuscação de IP] e não é afetada pela  [!UICONTROL Ofuscação de IP] configuração. |
| [!UICONTROL Ofuscação de IP] | Indica o tipo de ofuscação de IP a ser aplicada ao conjunto de dados. Qualquer processamento baseado no IP do cliente será afetado pela configuração de ofuscação de IP. Isso inclui todos os serviços do Experience Cloud que recebem dados do seu armazenamento de dados. <p>Opções disponíveis:</p> <ul><li>**[!UICONTROL Nenhum]**: Desativa a ofuscação de IP. O endereço IP do usuário completo será enviado por meio do armazenamento de dados.</li><li>**[!UICONTROL Parcial]**: Para endereços IPv4, ofusca o último octeto do endereço IP do usuário. Para endereços IPv6, ofusca os últimos 80 bits do endereço. <p>Exemplos:</p> <ul><li>IPv4: `1.2.3.4` -> `1.2.3.0`</li><li>IPv6: `2001:0db8:1345:fd27:0000:ff00:0042:8329` -> `2001:0db8:1345:0000:0000:0000:0000:0000`</li></ul></li><li>**[!UICONTROL Total]**: Ofusca todo o endereço IP. <p>Exemplos:</p> <ul><li>IPv4: `1.2.3.4` -> `0.0.0.0`</li><li>IPv6: `2001:0db8:1345:fd27:0000:ff00:0042:8329` -> `::/128`</li></ul></li></ul> Impacto da ofuscação de IP em outros produtos de Adobe: <ul><li>**Adobe Target**: O nível do conjunto de dados [!UICONTROL Ofuscação de IP] tem prioridade sobre qualquer opção de ofuscação de IP definida no Adobe Target. Por exemplo, se o nível de conjunto de dados [!UICONTROL Ofuscação de IP] está definida como **[!UICONTROL Total]** e a opção Adobe Target IP ofuscation está definida como **[!UICONTROL Ofuscação do último octeto]**, a Adobe Target receberá um IP totalmente ofuscado. Consulte a documentação do Adobe Target em [Ofuscação de IP](https://developer.adobe.com/target/before-implement/privacy/privacy/) e [geolocalização](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/geo.html?lang=en) para obter mais detalhes.</li><li>**Audience Manager**: A configuração de ofuscação de IP no nível do conjunto de dados tem prioridade sobre qualquer opção de ofuscação de IP definida no Audience Manager e é aplicada a todos os endereços IP. Qualquer pesquisa de geolocalização feita pelo Audience Manager é afetada pelo nível do conjunto de dados [!UICONTROL Ofuscação de IP] opção. Uma pesquisa de geolocalização no Audience Manager, baseada em um IP totalmente ofuscado, resultará em uma região desconhecida e nenhum segmento baseado nos dados de geolocalização resultantes será realizado. Consulte a documentação do Audience Manager em [Ofuscação de IP](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/administration/ip-obfuscation.html?lang=en) para obter mais detalhes.</li><li>**Adobe Analytics**: Os dados enviados para a Adobe Analytics não são afetados pelo nível do conjunto de dados [!UICONTROL Ofuscação de IP] configuração. No momento, a Adobe Analytics recebe endereços IP não ofuscados. Para que o Analytics receba endereços IP ofuscados, é necessário configurar a ofuscação de IP separadamente, no Adobe Analytics. Esse comportamento será atualizado em versões futuras. Consulte a Adobe Analytics [documentação](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/general-acct-settings-admin.html) para obter detalhes sobre como ativar a ofuscação de IP no Analytics.</li></ul> |
| [!UICONTROL Cookie da ID própria] | Quando habilitada, essa configuração informa à Edge Network para fazer referência a um cookie especificado ao pesquisar um [ID de dispositivo próprio](../identity/first-party-device-ids.md), em vez de pesquisar esse valor no Mapa de identidade.<br><br>Ao ativar essa configuração, você deve fornecer o nome do cookie no qual a ID deve ser armazenada. |
| [!UICONTROL Sincronização de ID de terceiros] | As sincronizações de ID podem ser agrupadas em contêineres para permitir que sincronizações de ID diferentes sejam executadas em momentos diferentes. Quando ativada, essa configuração permite especificar qual contêiner de sincronizações de ID é executado para esse armazenamento de dados. |
| [!UICONTROL ID do contêiner de sincronização de ID de terceiros] | A ID numérica do contêiner a ser usada para sincronização de ID de terceiros. |
| [!UICONTROL Substituições da ID do contêiner] | Nesta seção, é possível definir IDs de contêiner de sincronização de ID de terceiros adicionais que podem ser usadas para substituir a padrão. |
| [!UICONTROL Tipo de acesso] | Define o tipo de autenticação aceito pela Rede de Borda para o armazenamento de dados. <ul><li>**[!UICONTROL Autenticação mista]**: Quando essa opção é selecionada, a Edge Network aceita solicitações autenticadas e não autenticadas. Selecione essa opção quando planeja usar o SDK da Web ou [SDK móvel](https://aep-sdks.gitbook.io/docs/), juntamente com o [API do servidor](../../server-api/overview.md). </li><li>**[!UICONTROL Apenas Autenticado]**: Quando essa opção é selecionada, a Rede de Borda aceita apenas solicitações autenticadas. Selecione essa opção quando planeja usar somente a API do Servidor e deseja impedir que qualquer solicitação não autenticada seja processada pela Rede de Borda.</li></ul> |

A partir daqui, se você estiver configurando seu conjunto de dados para o Experience Platform, siga o tutorial em [Preparação de dados para coleta de dados](./data-prep.md) para mapear seus dados para um esquema de evento da plataforma antes de retornar a este guia. Caso contrário, selecione **[!UICONTROL Salvar]** e continue para a próxima seção.

## Exibir detalhes do armazenamento de dados {#view-details}

Após configurar um novo armazenamento de dados ou selecionar um existente para exibir, a página de detalhes desse armazenamento de dados será exibida. Aqui você pode encontrar mais informações sobre o armazenamento de dados, incluindo sua ID.

![Página de detalhes de um armazenamento de dados criado](../assets/datastreams/configure/view-details.png)

Na tela de detalhes do armazenamento de dados, é possível [adicionar serviços](#add-services) para ativar os recursos dos produtos da Adobe Experience Cloud aos quais você tem acesso. Também é possível editar o armazenamento de dados [configuração básica](#create), atualizar [regras de mapeamento](./data-prep.md), [copiar o datastream](#copy)ou exclua-a totalmente.

## Adicionar serviços a um armazenamento de dados {#add-services}

Na página de detalhes de um armazenamento de dados, selecione **[!UICONTROL Adicionar Serviço]** para começar a adicionar os serviços disponíveis para esse armazenamento de dados.

![Selecione Adicionar serviço para continuar](../assets/datastreams/configure/add-service.png)

Na próxima tela, use o menu suspenso para selecionar um serviço a ser configurado para esse armazenamento de dados. Somente os serviços aos quais você tem acesso serão exibidos nesta lista.

![Selecione um serviço na lista](../assets/datastreams/configure/service-selection.png)

Selecione o serviço desejado, preencha as opções de configuração exibidas e selecione **[!UICONTROL Salvar]** para adicionar o serviço ao armazenamento de dados. Todos os serviços adicionados aparecem na visualização de detalhes do armazenamento de dados.

![Serviços adicionados a um armazenamento de dados](../assets/datastreams/configure/services-added.png)

As subseções abaixo descrevem as opções de configuração para cada serviço.

>[!NOTE]
>
>Cada configuração de serviço contém um **[!UICONTROL Ativado]** alternar que é ativado automaticamente quando o serviço é selecionado. Para desabilitar o serviço selecionado para esse armazenamento de dados, selecione o **[!UICONTROL Ativado]** alternar novamente.

### Configurações do Adobe Analytics {#analytics}

Esse serviço controla se e como os dados são enviados para a Adobe Analytics. Podem ser encontrados detalhes adicionais no guia sobre [envio de dados para o Analytics](../data-collection/adobe-analytics/analytics-overview.md).

![Bloco de configurações do Adobe Analytics](../assets/datastreams/configure/analytics-config.png)

| Configuração | Descrição |
| --- | --- |
| [!UICONTROL ID de conjunto de relatórios] | **(Obrigatório)** A ID do conjunto de relatórios do Analytics para o qual você deseja enviar dados. Essa ID pode ser encontrada na interface do usuário do Adobe Analytics em [!UICONTROL Administrador] > [!UICONTROL ReportSuites]. Se vários conjuntos de relatórios forem especificados, os dados serão copiados para cada conjunto de relatórios. |
| [!UICONTROL Substituições do conjunto de relatórios] | Nesta seção, você pode adicionar outras IDs de conjunto de relatórios que podem ser usadas para substituir a padrão. |

### Configurações do Adobe Audience Manager {#audience-manager}

Esse serviço controla se e como os dados são enviados para a Adobe Audience Manager. Tudo o que é necessário para enviar dados para o Audience Manager é habilitar esta seção. As outras configurações são opcionais, mas são incentivadas.

![Bloco de configurações do Adobe Audience Manager](../assets/datastreams/configure/audience-manager-config.png)

| Configuração | Descrição |
| --- | --- |
| [!UICONTROL Destinos de cookies ativados] | Permite que o SDK compartilhe informações do segmento por meio de [destinos de cookie](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-cookie-destination.html) from [!DNL Audience Manager]. |
| [!UICONTROL Destinos de URL ativados] | Permite que o SDK compartilhe informações do segmento por meio de [Destinos de URL](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-url-destination.html) from [!DNL Audience Manager]. |

### Configurações do Adobe Experience Platform {#aep}

>[!IMPORTANT]
>
>Ao ativar um armazenamento de dados para a Platform, tome nota da sandbox da Platform que você está usando no momento, conforme exibido na faixa superior da interface do usuário.
>
>![Sandbox selecionada](../assets/datastreams/configure/platform-sandbox.png)
>
>As sandboxes são partições virtuais no Adobe Experience Platform que permitem isolar seus dados e implementações de outras pessoas na organização. Depois que um conjunto de dados é criado, sua sandbox não pode ser alterada. Para obter mais detalhes sobre a função das sandboxes no Experience Platform, consulte o [documentação das sandboxes](../../sandboxes/home.md).

Esse serviço controla se e como os dados são enviados para a Adobe Experience Platform.

![Bloco de configurações do Adobe Experience Platform](../assets/datastreams/configure/platform-config.png)

| Configuração | Descrição |
|---| --- |
| [!UICONTROL Conjunto de dados do evento] | **(Obrigatório)** Selecione o conjunto de dados da plataforma para o qual os dados do evento do cliente serão transmitidos. Esse schema deve usar o [Classe XDM ExperienceEvent](../../xdm/classes/experienceevent.md). Para adicionar outros conjuntos de dados, selecione **[!UICONTROL Adicionar conjunto de dados de evento]**. |
| [!UICONTROL Conjunto de dados de perfil] | Selecione o conjunto de dados da plataforma para o qual os dados do atributo do cliente serão enviados. Esse schema deve usar o [Classe de perfil individual XDM](../../xdm/classes/individual-profile.md). |
| [!UICONTROL Offer Decisioning] | Marque essa caixa de seleção para ativar o Offer Decisioning para uma implementação do SDK da Web da plataforma. Consulte o guia sobre [uso do Offer Decisioning com o SDK da Web da plataforma](../personalization/offer-decisioning/offer-decisioning-overview.md) para obter mais detalhes sobre a implementação.<br><br>Para obter mais informações sobre recursos do Offer Decisioning, consulte [Documentação do Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started/starting-offer-decisioning.html?lang=pt-BR). |
| [!UICONTROL Segmentação de borda] | Marque essa caixa de seleção para ativar [segmentação de borda](../../segmentation/ui/edge-segmentation.md) para esse armazenamento de dados. Quando o SDK envia dados por meio de um conjunto de dados habilitado para a segmentação de borda, qualquer associação de segmento atualizada para o perfil em questão é enviada de volta na resposta.<br><br>Essa opção pode ser usada em combinação com [!UICONTROL Destinos de personalização] para [casos de uso de personalização de próxima página](../../destinations/ui/configure-personalization-destinations.md). |
| [!UICONTROL Destinos de personalização] | Ao ativar isso depois de ativar a variável [!UICONTROL Segmentação de borda] , essa opção permite que o conjunto de dados se conecte a destinos de personalização, como [Personalização personalizada](../../destinations/catalog/personalization/custom-personalization.md).<br><br>Consulte a documentação de destinos para obter etapas específicas sobre [configuração de destinos de personalização](../../destinations/ui/configure-personalization-destinations.md). |
| [!UICONTROL Adobe Journey Optimizer] | Marque essa caixa de seleção para ativar [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=pt-BR) para esse armazenamento de dados. <br><br> Ativar essa opção permite que o armazenamento de dados retorne conteúdo personalizado de campanhas de entrada com base na Web e no aplicativo em [!DNL Adobe Journey Optimizer]. Esta opção requer [!UICONTROL Segmentação de borda] para estar ativo. If [!UICONTROL Segmentação de borda] estiver desmarcada, essa opção ficará esmaecida. |

### Configurações do Adobe Target {#target}

Esse serviço controla se e como os dados são enviados para a Adobe Target.

![Bloco de configurações do Adobe Target](../assets/datastreams/configure/target-config.png)

| Configuração | Descrição |
| --- | --- |
| [!UICONTROL Token de propriedade] | [!DNL Target] O permite que os clientes controlem permissões por meio do uso de propriedades do . Para obter mais informações sobre propriedades, consulte o guia sobre [configuração de permissões empresariais](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html?lang=pt-BR) no [!DNL Target] documentação.<br><br>O token de propriedade pode ser encontrado na interface do usuário do Adobe Target em [!UICONTROL Configuração] > [!UICONTROL Propriedades]. |
| [!UICONTROL ID do ambiente do Target] | [Ambientes no Adobe Target](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html) Ajudar você a gerenciar sua implementação em todos os estágios de desenvolvimento. Essa configuração especifica qual ambiente você usará com esse conjunto de dados.<br><br>A prática recomendada é definir isso de forma diferente para cada um de seus `dev`, `stage`e `prod` ambientes de fluxo de dados para simplificar as coisas. No entanto, se você já tiver ambientes Adobe Target definidos, poderá usá-los. |
| [!UICONTROL Namespace da ID de terceiros do Target] | O namespace de identidade do `mbox3rdPartyId` você deseja usar para esse armazenamento de dados. Consulte o guia sobre [implementação `mbox3rdPartyId` com o SDK da Web](../personalization/adobe-target/using-mbox-3rdpartyid.md) para obter mais informações. |
| [!UICONTROL Substituições de token de propriedade] | Nesta seção você pode definir tokens de propriedade adicionais que podem ser usados para substituir o padrão. |

### [!UICONTROL Encaminhamento de evento] configurações

Esse serviço controla se e como os dados são enviados para [encaminhamento de eventos](../../tags/ui/event-forwarding/overview.md).

![Seção Encaminhamento de eventos da interface do usuário de configuração](../assets/datastreams/configure/event-forwarding-config.png)

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

![Imagem que mostra o [!UICONTROL Copiar] opção sendo selecionada na exibição de lista do armazenamento de dados](../assets/datastreams/configure/copy-datastream-list.png)

Como alternativa, você pode selecionar **[!UICONTROL Copiar fluxo de dados]** na exibição de detalhes de um determinado conjunto de dados.

![Imagem que mostra o [!UICONTROL Copiar] opção sendo selecionada na visualização de detalhes do armazenamento de dados](../assets/datastreams/configure/copy-datastream-details.png)

Uma caixa de diálogo de confirmação é exibida, solicitando que você forneça um nome exclusivo para o novo armazenamento de dados a ser criado, juntamente com detalhes sobre as opções de configuração que serão copiadas. Quando estiver pronto, selecione **[!UICONTROL Copiar]**.

![Imagem da caixa de diálogo de confirmação para copiar um conjunto de dados](../assets/datastreams/configure/copy-datastream-confirm.png)

A página principal do [!UICONTROL Datastreams] o workspace é exibido novamente com o novo datastream listado.

## Próximas etapas

Este guia cobriu como gerenciar conjuntos de dados na interface do usuário da Coleta de dados. Para obter mais informações sobre como instalar e configurar o SDK da Web após configurar um conjunto de dados, consulte o [Guia E2E de coleta de dados](../../collection/e2e.md#install).
