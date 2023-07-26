---
title: Configurar uma sequência de dados
description: Saiba como conectar sua integração do SDK da Web do lado do cliente com outros produtos Adobe e destinos de terceiros.
exl-id: 4924cd0f-5ec6-49ab-9b00-ec7c592397c8
source-git-commit: ac0d92938332f04d0b2813172d0d4a75cacdcd1d
workflow-type: tm+mt
source-wordcount: '2247'
ht-degree: 2%

---


# Configurar uma sequência de dados

Este documento aborda as etapas para configurar um [sequência de dados](./overview.md) na interface.

## Acesse o [!UICONTROL Datastreams] espaço de trabalho

Você pode criar e gerenciar fluxos de dados na interface da Coleção de dados ou na interface do Experience Platform selecionando **[!UICONTROL Datastreams]** no painel de navegação esquerdo.

![Guia Fluxos de dados na interface da Coleção de dados](assets/configure/datastreams-tab.png)

A variável **[!UICONTROL Datastreams]** A guia exibe uma lista de fluxos de dados existentes, incluindo o nome amigável, a ID e a data da última modificação. Selecione o nome de um fluxo de dados para [exibir os detalhes e configurar serviços](#view-details).

Selecione o ícone &quot;mais&quot; (**..**) para que um fluxo de dados específico revele mais opções. Selecionar **[!UICONTROL Editar]** para atualizar o [configuração básica](#configure) para o fluxo de dados ou selecione **[!UICONTROL Excluir]** para remover o fluxo de dados.

![Opções para editar ou excluir um fluxo de dados existente](assets/configure/edit-datastream.png)

## Criar um novo fluxo de dados {#create}

Para criar um fluxo de dados, comece selecionando **[!UICONTROL Nova sequência de dados]**.

![Selecione Novo fluxo de dados](assets/configure/new-datastream-button.png)

O workflow de criação de sequência de dados é exibido, iniciando na etapa de configuração. Aqui, você deve fornecer um nome e uma descrição opcional para o fluxo de dados.

Se estiver configurando esse fluxo de dados para uso no Experience Platform e estiver usando o SDK da Web da plataforma, você também deve selecionar um [esquema do Experience Data Model (XDM) baseado em eventos](../xdm/classes/experienceevent.md) para representar os dados que você planeja assimilar.

![Configuração básica para um fluxo de dados](assets/configure/configure.png)

Selecionar **[!UICONTROL Opções avançadas]** para revelar controles adicionais para configurar o fluxo de dados.

![Opções de configuração avançadas](assets/configure/advanced-options.png) {#advanced-options}

>[!IMPORTANT]
>
> Você é responsável por garantir que obteve todas as permissões, consentimentos, autorizações e a autorização necessários, exigidos pelas leis e regulamentos aplicáveis, para coletar, processar e transmitir dados pessoais, incluindo informações precisas de geolocalização.
> 
> A seleção de ofuscação do endereço IP não afeta o nível de informações de geolocalização que serão derivadas do endereço IP e enviadas para as soluções de Adobe configuradas. As pesquisas de geolocalização devem ser limitadas ou desabilitadas separadamente.

| Configuração | Descrição |
| --- | --- |
| [!UICONTROL Pesquisa geográfica] | Permite pesquisas de geolocalização para as opções selecionadas, com base no endereço IP do visitante. Opções disponíveis: <ul><li>País</li><li>Código postal</li><li>Estado/Província</li><li>DMA</li><li>Cidade</li><li>Latitude </li><li>Longitude</li></ul>Selecionar **[!UICONTROL Cidade]**, **[!UICONTROL Latitude]** ou **[!UICONTROL Longitude]** O fornece coordenadas com até duas casas decimais, independentemente de quais outras opções estão selecionadas. Essa é considerada granularidade no nível da cidade. <br> <br>Não selecionar nenhuma opção desativa pesquisas de geolocalização. A geolocalização ocorre antes [!UICONTROL Ofuscação de IP] e não for afetado pelo  [!UICONTROL Ofuscação de IP] configuração. |
| [!UICONTROL Pesquisa de rede] | Ativa pesquisas de rede para as opções selecionadas, com base no endereço IP do visitante. Opções disponíveis: <ul><li>Operadora</li><li>Domain</li><li>ISP</li></ul>Use essas opções para fornecer mais informações a outros serviços sobre a rede específica em que as solicitações se originaram. |
| [!UICONTROL Ofuscação de IP] | Indica o tipo de ofuscação de IP a ser aplicado ao fluxo de dados. Qualquer processamento baseado no IP do cliente será afetado pela configuração de ofuscação de IP. Isso inclui todos os serviços de Experience Cloud que recebem dados do seu fluxo de dados. <p>Opções disponíveis:</p> <ul><li>**[!UICONTROL Nenhum]**: desativa a ofuscação de IP. O endereço IP completo do usuário será enviado por meio do fluxo de dados.</li><li>**[!UICONTROL Parcial]**: Para endereços IPv4, ofusca o último octeto do endereço IP do usuário. Para endereços IPv6, ofusca os últimos 80 bits do endereço. <p>Exemplos:</p> <ul><li>IPv4: `1.2.3.4` -> `1.2.3.0`</li><li>IPv6: `2001:0db8:1345:fd27:0000:ff00:0042:8329` -> `2001:0db8:1345:0000:0000:0000:0000:0000`</li></ul></li><li>**[!UICONTROL Completo]**: ofusca todo o endereço IP. <p>Exemplos:</p> <ul><li>IPv4: `1.2.3.4` -> `0.0.0.0`</li><li>IPv6: `2001:0db8:1345:fd27:0000:ff00:0042:8329` -> `0:0:0:0:0:0:0:0`</li></ul></li></ul> Impacto de ofuscação de IP em outros produtos Adobe: <ul><li>**Adobe Target**: o nível do fluxo de dados [!UICONTROL Ofuscação de IP] A configuração tem prioridade sobre qualquer opção de ofuscação de IP definida no Adobe Target. Por exemplo, se o nível de fluxo de dados [!UICONTROL Ofuscação de IP] está definida como **[!UICONTROL Completo]** e a opção de ofuscação de IP do Adobe Target estiver definida como **[!UICONTROL Ofuscação do último octeto]**, o Adobe Target receberá um IP totalmente ofuscado. Consulte a documentação do Adobe Target em [Ofuscação de IP](https://developer.adobe.com/target/before-implement/privacy/privacy/) e [localização geográfica](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/geo.html?lang=en) para obter mais detalhes.</li><li>**Audience Manager**: a configuração de ofuscação de IP no nível do fluxo de dados tem prioridade sobre qualquer opção de ofuscação de IP definida no Audience Manager e é aplicada a todos os endereços IP. Qualquer pesquisa de geolocalização feita pelo Audience Manager é afetada pelo nível de fluxo de dados [!UICONTROL Ofuscação de IP] opção. Uma pesquisa de geolocalização no Audience Manager, com base em um IP totalmente ofuscado, resultará em uma região desconhecida e todos os segmentos baseados nos dados de geolocalização resultantes não serão realizados. Consulte a documentação do Audience Manager em [Ofuscação de IP](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/administration/ip-obfuscation.html?lang=en) para obter mais detalhes.</li><li>**Adobe Analytics**: no momento, o Adobe Analytics recebe os endereços IP parcialmente ofuscados se qualquer opção de ofuscação de IP estiver selecionada, diferente de NENHUM. Para que o Analytics receba endereços IP totalmente ofuscados, você deve configurar a ofuscação de IP separadamente no Adobe Analytics. Esse comportamento será atualizado em versões futuras. Consulte a Adobe Analytics [documentação](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/general-acct-settings-admin.html) para obter detalhes sobre como ativar a ofuscação de IP no Analytics.</li></ul> |
| [!UICONTROL Cookie de ID próprio] | Quando ativada, essa configuração informa à Rede de borda que se refira a um cookie especificado ao procurar um [ID do dispositivo primário](../edge/identity/first-party-device-ids.md), em vez de pesquisar esse valor no Mapa de identidade.<br><br>Ao ativar essa configuração, você deve fornecer o nome do cookie no qual a ID deve ser armazenada. |
| [!UICONTROL Sincronização de ID de terceiros] | As sincronizações de ID podem ser agrupadas em contêineres para permitir que diferentes sincronizações de ID sejam executadas em momentos diferentes. Quando habilitada, essa configuração permite especificar qual contêiner de sincronizações de ID é executado para esse fluxo de dados. |
| [!UICONTROL ID de contêiner de sincronização de ID de terceiros] | A ID numérica do contêiner a ser usada para sincronização de ID de terceiros. |
| [!UICONTROL Substituições de ID de contêiner] | Nesta seção, você pode definir IDs adicionais de contêiner de sincronização de ID de terceiros, que podem ser usadas para substituir a padrão. |
| [!UICONTROL Tipo de acesso] | Define o tipo de autenticação que a Rede de borda aceita para a sequência de dados. <ul><li>**[!UICONTROL Autenticação mista]**: quando essa opção é selecionada, a Rede de borda aceita solicitações autenticadas e não autenticadas. Selecione esta opção quando planejar usar o SDK da Web ou [SDK móvel](https://aep-sdks.gitbook.io/docs/), juntamente com o [API do servidor](../server-api/overview.md). </li><li>**[!UICONTROL Somente autenticado]**: quando essa opção é selecionada, a Rede de borda aceita somente solicitações autenticadas. Selecione essa opção quando planejar usar somente a API do servidor e quiser impedir que qualquer solicitação não autenticada seja processada pela Rede de borda.</li></ul> |

Daqui, se você estiver configurando seu fluxo de dados para o Experience Platform, siga o tutorial em [Preparação de dados para coleção de dados](./data-prep.md) para mapear seus dados a um esquema de evento da Platform antes de retornar a este guia. Caso contrário, selecione **[!UICONTROL Salvar]** e continue para a próxima seção.

## Exibir detalhes da sequência de dados {#view-details}

Depois de configurar um novo fluxo de dados ou selecionar um existente para exibir, a página de detalhes desse fluxo de dados é exibida. Aqui você pode encontrar mais informações sobre o fluxo de dados, incluindo a ID.

![Página de detalhes de um fluxo de dados criado](assets/configure/view-details.png)

Na tela de detalhes do fluxo de dados, é possível [adicionar serviços](#add-services) para ativar recursos dos produtos Adobe Experience Cloud aos quais você tem acesso. Também é possível editar as configurações do fluxo de dados [configuração básica](#create), atualize seu [regras de mapeamento](./data-prep.md), [copiar a sequência de dados](#copy)ou exclua completamente.

## Adicionar serviços a um fluxo de dados {#add-services}

Na página de detalhes de um fluxo de dados, selecione **[!UICONTROL Adicionar serviço]** para começar a adicionar os serviços disponíveis para esse fluxo de dados.

![Selecione Adicionar serviço para continuar](assets/configure/add-service.png)

Na próxima tela, use o menu suspenso para selecionar um serviço a ser configurado para esse fluxo de dados. Somente os serviços aos quais você tem acesso aparecerão nesta lista.

![Selecione um serviço na lista](assets/configure/service-selection.png)

Selecione o serviço desejado, preencha as opções de configuração exibidas e selecione **[!UICONTROL Salvar]** para adicionar o serviço ao fluxo de dados. Todos os serviços adicionados aparecem na visualização de detalhes do fluxo de dados.

![Serviços adicionados a um fluxo de dados](assets/configure/services-added.png)

As subseções abaixo descrevem as opções de configuração para cada serviço.

>[!NOTE]
>
>Cada configuração de serviço contém um **[!UICONTROL Ativado]** alternância que é ativada automaticamente quando o serviço é selecionado. Para desativar o serviço selecionado para esse fluxo de dados, selecione o **[!UICONTROL Ativado]** alterne novamente.

### Configurações do Adobe Analytics {#analytics}

Este serviço controla se e como os dados são enviados para o Adobe Analytics. Detalhes adicionais podem ser encontrados no guia sobre [envio de dados para o Analytics](../edge/data-collection/adobe-analytics/analytics-overview.md).

![Bloco de configurações do Adobe Analytics](assets/configure/analytics-config.png)

| Configuração | Descrição |
| --- | --- |
| [!UICONTROL ID de conjunto de relatórios] | **(Obrigatório)** A ID do conjunto de relatórios do Analytics para o qual você deseja enviar dados. Essa ID pode ser encontrada na interface do usuário do Adobe Analytics em [!UICONTROL Admin] > [!UICONTROL ReportSuites]. Se vários conjuntos de relatórios forem especificados, os dados serão copiados para cada conjunto de relatórios. |
| [!UICONTROL Substituições do conjunto de relatórios] | Nesta seção, você pode adicionar outras IDs de conjunto de relatórios que podem ser usadas para substituir a padrão. |

### Configurações do Adobe Audience Manager {#audience-manager}

Este serviço controla se e como os dados são enviados para o Adobe Audience Manager. Tudo o que é necessário para enviar dados para o Audience Manager é ativar esta seção. As outras configurações são opcionais, mas são incentivadas.

![Bloco de configurações do Adobe Audience Manager](assets/configure/audience-manager-config.png)

| Configuração | Descrição |
| --- | --- |
| [!UICONTROL Destinos de cookies ativados] | Permite que o SDK compartilhe informações de segmento via [destinos de cookies](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-cookie-destination.html) de [!DNL Audience Manager]. |
| [!UICONTROL Destinos do URL habilitados] | Permite que o SDK compartilhe informações de segmento via [Destinos do URL](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-url-destination.html) de [!DNL Audience Manager]. |

### Configurações do Adobe Experience Platform {#aep}

>[!IMPORTANT]
>
>Ao ativar um fluxo de dados para a Platform, anote a sandbox da Platform que você está usando no momento, como exibida na faixa superior da interface do usuário.
>
>![Sandbox selecionada](assets/configure/platform-sandbox.png)
>
>As sandboxes são partições virtuais na Adobe Experience Platform que permitem isolar seus dados e implementações de outras pessoas em sua organização. Depois que uma sequência de dados é criada, sua sandbox não pode ser alterada. Para obter mais detalhes sobre a função das sandboxes no Experience Platform, consulte o [documentação de sandboxes](../sandboxes/home.md).

Este serviço controla se e como os dados são enviados para o Adobe Experience Platform.

![Bloco de configurações do Adobe Experience Platform](assets/configure/platform-config.png)

| Configuração | Descrição |
|---| --- |
| [!UICONTROL Conjunto de dados do evento] | **(Obrigatório)** Selecione o conjunto de dados da plataforma para o qual os dados do evento do cliente serão transmitidos. Este esquema deve usar o [Classe XDM ExperienceEvent](../xdm/classes/experienceevent.md). Para adicionar conjuntos de dados adicionais, selecione **[!UICONTROL Adicionar conjunto de dados do evento]**. |
| [!UICONTROL Conjunto de dados do perfil] | Selecione o conjunto de dados da plataforma para o qual os dados do atributo do cliente serão enviados. Este esquema deve usar o [Classe Perfil individual XDM](../xdm/classes/individual-profile.md). |
| [!UICONTROL Offer Decisioning] | Marque esta caixa de seleção para ativar o Offer Decisioning para uma implementação do SDK da Web da plataforma. Consulte o guia sobre [utilização do Offer Decisioning com o SDK da Web da plataforma](../edge/personalization/offer-decisioning/offer-decisioning-overview.md) para obter mais detalhes sobre a implementação.<br><br>Para obter mais informações sobre os recursos do Offer Decisioning, consulte [Documentação do Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started/starting-offer-decisioning.html?lang=pt-BR). |
| [!UICONTROL Segmentação de borda] | Marque esta caixa de seleção para ativar [segmentação de borda](../segmentation/ui/edge-segmentation.md) para esse fluxo de dados. Quando o SDK envia dados por meio de uma sequência de dados habilitada para segmentação de borda, todas as associações de segmento atualizadas para o perfil em questão são enviadas de volta na resposta.<br><br>Essa opção pode ser usada em combinação com [!UICONTROL Destinos de personalização] para [casos de uso de personalização da próxima página](../destinations/ui/activate-edge-personalization-destinations.md). |
| [!UICONTROL Destinos de personalização] | Ao ativar isso após ativar o [!UICONTROL Segmentação de borda] , essa opção permite que o fluxo de dados se conecte a destinos de personalização, como [Personalização personalizada](../destinations/catalog/personalization/custom-personalization.md).<br><br>Consulte a documentação de destinos para obter etapas específicas sobre [configuração de destinos de personalização](../destinations/ui/activate-edge-personalization-destinations.md). |
| [!UICONTROL Adobe Journey Optimizer] | Marque esta caixa de seleção para ativar [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=pt-BR) para esse fluxo de dados. <br><br> Habilitar essa opção permite que a sequência de dados retorne conteúdo personalizado de campanhas de entrada baseadas na Web e em aplicativos no [!DNL Adobe Journey Optimizer]. Esta opção requer [!UICONTROL Segmentação de borda] para estar ativo. Se [!UICONTROL Segmentação de borda] estiver desmarcada, essa opção ficará esmaecida. |

### Configurações do Adobe Target {#target}

Este serviço controla se e como os dados são enviados para o Adobe Target.

![Bloco de configurações do Adobe Target](assets/configure/target-config.png)

| Configuração | Descrição |
| --- | --- |
| [!UICONTROL Token de propriedade] | [!DNL Target] O permite que os clientes controlem permissões por meio do uso de propriedades. Para obter mais informações sobre propriedades, consulte o manual sobre [configuração de permissões empresariais](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html?lang=pt-BR) no [!DNL Target] documentação.<br><br>O token de propriedade pode ser encontrado na interface do usuário do Adobe Target em [!UICONTROL Configuração] > [!UICONTROL Propriedades]. |
| [!UICONTROL ID do ambiente de destino] | [Ambientes no Adobe Target](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html) ajudar você a gerenciar a implementação em todos os estágios de desenvolvimento. Essa configuração especifica qual ambiente você usará com esse fluxo de dados.<br><br>A prática recomendada é definir isso de forma diferente para cada um dos `dev`, `stage`, e `prod` ambientes de sequência de dados para simplificar as coisas. No entanto, se você já tiver ambientes Adobe Target definidos, poderá usá-los. |
| [!UICONTROL Namespace da ID de terceiros do Target] | O namespace de identidade para o `mbox3rdPartyId` você deseja usar para esta sequência de dados. Consulte o guia sobre [implementação `mbox3rdPartyId` com o SDK da Web](../edge/personalization/adobe-target/using-mbox-3rdpartyid.md) para obter mais informações. |
| [!UICONTROL Substituições do token de propriedade] | Nesta seção, você pode definir tokens de propriedade adicionais que podem ser usados para substituir o padrão. |

### [!UICONTROL Encaminhamento de evento] configurações

Este serviço controla se e como os dados são enviados para [encaminhamento de eventos](../tags/ui/event-forwarding/overview.md).

![Seção Encaminhamento de eventos da interface do usuário de configuração](assets/configure/event-forwarding-config.png)

| Configuração | Descrição |
| --- | --- |
| [!UICONTROL Iniciar propriedade] | **(Obrigatório)** A propriedade de encaminhamento de eventos para a qual você deseja enviar dados. |
| [!UICONTROL Ambiente do Launch] | **(Obrigatório)** O ambiente na propriedade selecionada para a qual você deseja enviar dados. |

>[!NOTE]
>
>É possível selecionar **[!UICONTROL Inserir IDs manualmente]** para digitar os nomes da propriedade e do ambiente em vez de usar os menus suspensos.

## Copiar um fluxo de dados {#copy}

É possível criar uma cópia de um fluxo de dados existente e alterar seus detalhes conforme necessário.

>[!NOTE]
>
>As sequências de dados só podem ser copiadas na mesma [sandbox](../sandboxes/home.md). Em outras palavras, não é possível copiar um fluxo de dados de uma sandbox para outra.

Na página principal do [!UICONTROL Datastreams] , selecione as reticências (**...**) para o fluxo de dados em questão, selecione **[!UICONTROL Copiar]**.

![Imagem mostrando o [!UICONTROL Copiar] opção selecionada na exibição de lista do fluxo de dados](assets/configure/copy-datastream-list.png)

Como alternativa, você pode selecionar **[!UICONTROL Copiar fluxo de dados]** na visualização de detalhes de um determinado fluxo de dados.

![Imagem mostrando o [!UICONTROL Copiar] opção selecionada na visualização de detalhes do fluxo de dados](assets/configure/copy-datastream-details.png)

Uma caixa de diálogo de confirmação é exibida, solicitando que você forneça um nome exclusivo para o novo fluxo de dados a ser criado, juntamente com detalhes sobre as opções de configuração que serão copiadas. Quando estiver pronto, selecione **[!UICONTROL Copiar]**.

![Imagem da caixa de diálogo de confirmação para copiar um fluxo de dados](assets/configure/copy-datastream-confirm.png)

A página principal do [!UICONTROL Datastreams] O espaço de trabalho será exibido novamente com o novo fluxo de dados listado.

## Próximas etapas

Este guia abordou como gerenciar fluxos de dados na interface da Coleção de dados. Para obter mais informações sobre como instalar e configurar o SDK da Web após configurar um fluxo de dados, consulte o [Guia da Coleção de dados E2E](../collection/e2e.md#install).
