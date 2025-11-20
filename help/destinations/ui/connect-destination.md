---
title: Criar uma nova conexão de destino
type: Tutorial
description: Saiba como se conectar a um destino no Adobe Experience Platform, ativar alertas e configurar ações de marketing para o destino conectado.
exl-id: 56d7799a-d1da-4727-ae79-fb2c775fe5a5
source-git-commit: ec6f055de02610e23f30051c4fed4f362e9fbc53
workflow-type: tm+mt
source-wordcount: '1236'
ht-degree: 4%

---

# Criar uma nova conexão de destino

>[!IMPORTANT]
> 
>* Para se conectar a um destino, você precisa das **[!UICONTROL View Destinations]** e **[!UICONTROL Manage Destinations]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.
>* Para se conectar a um destino compatível com exportações de conjunto de dados, você precisa das **[!UICONTROL View Destinations]** e **[!UICONTROL Manage and Activate Dataset Destinations]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.

## Visão geral {#overview}

Antes de enviar dados do público-alvo para um destino, é necessário configurar uma conexão com a plataforma de destino. Este artigo mostra como configurar uma nova conexão de destino, para a qual você pode ativar públicos ou exportar conjuntos de dados usando a interface do usuário do Adobe Experience Platform.

## Localize o destino desejado no catálogo {#setup}

1. Vá para **[!UICONTROL Connections]** > **[!UICONTROL Destinations]** e selecione a guia **[!UICONTROL Catalog]**.

   ![Captura de tela da interface do usuário do Experience Platform mostrando a página do catálogo de destinos.](../assets/ui/connect-destinations/catalog.png)

2. Os cartões de destino no catálogo podem ter controles de ação diferentes, dependendo se você tem uma conexão existente com o destino e se os destinos oferecem suporte à ativação de públicos, exportação de conjuntos de dados ou ambos. Você pode ver qualquer um dos seguintes controles para cartões de destino:

   * **[!UICONTROL Set up]**. Primeiro, é necessário configurar uma conexão com esse destino para que você possa ativar públicos ou exportar conjuntos de dados.
   * **[!UICONTROL Activate]**. Já foi configurada uma conexão com este destino. Esse destino oferece suporte à ativação de públicos-alvo e exportações de conjunto de dados.
   * **[!UICONTROL Activate audiences]**. Já foi configurada uma conexão com este destino. Este destino oferece suporte somente à ativação de público-alvo.

   Para obter mais informações sobre a diferença entre esses controles, consulte também a seção [Catálogo](../ui/destinations-workspace.md#catalog) da documentação do espaço de trabalho de destino.

   Selecione **[!UICONTROL Set up]**, **[!UICONTROL Activate]** ou **[!UICONTROL Activate audiences]**, dependendo de qual controle está disponível para você.

   ![Captura de tela da interface do Experience Platform, mostrando a página do catálogo de destinos com o controle Configurar realçado.](../assets/ui/connect-destinations/set-up.png)

   ![Captura de tela da interface do usuário do Experience Platform mostrando a página do catálogo de destinos com o controle Ativar públicos destacado.](../assets/ui/connect-destinations/activate-segments.png)

3. Se você selecionou **[!UICONTROL Set up]**, pule para a próxima etapa para [autenticar](#authenticate) para o destino.

   Se você selecionou **[!UICONTROL Activate]**, **[!UICONTROL Activate audiences]** ou **[!UICONTROL Export datasets]**, agora é possível ver uma lista de conexões de destino existentes.

   Selecione **[!UICONTROL Configure new destination]** para estabelecer uma nova conexão com o destino.

   ![Captura de tela da interface do usuário do Experience Platform, mostrando uma lista de destinos disponíveis e o controle Configurar novo destino destacado.](../assets/ui/connect-destinations/configure-new-destination.png)

## Autenticar para o destino {#authenticate}

>[!CONTEXTUALHELP]
>id="platform_destinations_account_name"
>title="Nome da conta"
>abstract="Insira um nome que ajudará a identificar facilmente esta conta de destino no futuro. Isso é especialmente útil se você tiver várias conexões com o mesmo destino."

A primeira etapa na conexão com um destino é autenticar na plataforma de destino.

Dependendo do destino ao qual você está se conectando, você pode ser levado à página do parceiro de destino para autenticar ou pode ser solicitado a inserir credenciais de autenticação diretamente no fluxo de trabalho do Experience Platform.

Ao configurar uma nova conexão de destino, você deve fornecer um **[!UICONTROL Account name]** e, opcionalmente, um **[!UICONTROL Description]**. Esses campos estão disponíveis para todos os destinos.

* **[!UICONTROL Account name]**: Digite um nome que o ajudará a identificar facilmente esta conta de destino no futuro. Isso é especialmente útil se você tiver várias conexões com o mesmo destino.
* **[!UICONTROL Description]** (opcional): adicione detalhes adicionais que ajudarão você ou sua equipe a distinguir contas, como a finalidade da conexão ou o contexto comercial relevante.

Fornecer informações claras e descritivas nesses campos facilita o gerenciamento e a seleção da conta de destino correta ao ativar públicos.

Veja abaixo um exemplo da entrada necessária para autenticar em um destino [!DNL Amazon S3]. Instruções detalhadas sobre a entrada necessária são fornecidas em cada página de documentação de destino (consulte, por exemplo, a seção de autenticação para [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#authenticate) e para [[!DNL Facebook]](/help/destinations/catalog/social/facebook.md#authenticate)).

**[!DNL Amazon S3]parâmetros de autenticação obrigatórios e opcionais**

![Imagem mostrando os parâmetros de entrada obrigatórios e opcionais ao autenticar em um destino do Amazon S3.](../assets/ui/connect-destinations/s3-new-acc.png)

## Configurar parâmetros de conexão {#set-up-connection-parameters}

Se você já tiver configurado a autenticação para o destino, poderá continuar com a conta existente ou configurar uma nova conta.

Dependendo do destino ao qual você está se conectando, talvez seja solicitado que você insira diferentes tipos de parâmetros de conexão. Por exemplo, ao conectar-se a um destino [!DNL Amazon S3], você é solicitado a fornecer detalhes sobre o nome do bucket e o caminho da pasta [!DNL Amazon S3] onde os arquivos serão depositados. Abaixo estão dois exemplos de entradas necessárias para um destino [!DNL Amazon S3] e um destino [!DNL Trade Desk]. Instruções detalhadas sobre a entrada necessária são fornecidas em cada página de documentação de destino.

>[!IMPORTANT]
>
>As imagens abaixo são usadas apenas para fins ilustrativos. Os detalhes da conexão de destino variam entre os destinos. Para obter informações detalhadas sobre os detalhes da conexão para o seu destino, leia a seção **Conectar ao destino** em cada página do [catálogo de destino](../catalog/overview.md) (por exemplo, [[!DNL Google Customer Match]](../catalog/advertising/google-customer-match.md#connect), [[!DNL Trade Desk]](/help/destinations/catalog/advertising/tradedesk.md#connect) ou [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details)).

**[!DNL Amazon S3]parâmetros de entrada obrigatórios e opcionais**

![Imagem mostrando os parâmetros de entrada obrigatórios e opcionais ao conectar-se a um destino do Amazon S3.](../assets/ui/connect-destinations/connect-destination-amazons3-example.png)

**[!DNL The Trade Desk]parâmetros de entrada obrigatórios e opcionais**

![Imagem mostrando os parâmetros de entrada obrigatórios e opcionais ao conectar-se a um destino de Trade Desk.](../assets/ui/connect-destinations/connect-destination-trade-desk-example.png)

### Configurar opções de formatação de arquivo para arquivos exportados {#file-formatting-and-compression-options}

Para destinos baseados em arquivo, é possível definir várias configurações relacionadas ao modo como os arquivos exportados são formatados e compactados. Para obter mais informações sobre todas as opções disponíveis de formatação e compactação, leia o [tutorial Configurar opções de formatação de arquivo para destinos baseados em arquivo](/help/destinations/ui/batch-destinations-file-formatting-options.md).

![Imagem mostrando a seleção do tipo de arquivo e várias opções para arquivos CSV.](/help/destinations/assets/ui/connect-destinations/file-formatting-options.png)

### Configurar a conexão de destino para ativação de público, ativação de conta, ativação de clientes potenciais ou exportações de conjunto de dados {#segment-activation-or-dataset-exports}

Alguns destinos baseados em arquivo oferecem suporte à ativação de públicos-alvo para clientes conhecidos, clientes da conta ou clientes potenciais, bem como exportações de conjuntos de dados. Para esses destinos, você pode criar uma conexão que permita [ativar públicos](/help/destinations/ui/activate-batch-profile-destinations.md), [contas](/help/destinations/ui/activate-account-audiences.md), [prospetos](/help/destinations/ui/activate-prospect-audiences.md) ou [exportar conjuntos de dados](/help/destinations/ui/export-datasets.md).

>[!WARNING]
>
>Ao exportar conjuntos de dados, observe que as exportações para arquivos JSON são compatíveis somente no modo compactado. Há suporte para exportações para [!DNL Parquet] arquivos em um modo compactado e descompactado.

![Imagem mostrando o controle de seleção de tipo de dados que permite aos usuários escolher entre ativação de público-alvo e exportações de conjunto de dados.](/help/destinations/assets/ui/connect-destinations/data-type-selection.png)

### Ativar alertas de destino {#enable-alerts}

1. (Opcional) Selecione os alertas de fluxo de dados de destino que você deseja assinar. Você pode assinar alertas ao criar um fluxo de dados para receber mensagens de alerta sobre o status, o sucesso ou a falha da execução do fluxo. Os alertas disponíveis diferem com base no tipo de destino (baseado em arquivo ou transmissão) ao qual você está se conectando. Leia [Assinar alertas de destino em contexto](alerts.md) para obter informações detalhadas sobre alertas de fluxo de dados de destino.

   ![A caixa de diálogo Configurar novo destino com as opções de assinatura de alertas de destino em contexto foi realçada.](../assets/ui/connect-destinations/subscribe-to-alerts.png)

2. Selecione **[!UICONTROL Next]**.

   ![A caixa de diálogo Configurar novo destino com o controle Avançar foi realçada, permitindo que o usuário prossiga para a próxima etapa do fluxo de trabalho.](../assets/ui/connect-destinations/next.png)

## Selecionar ações de marketing {#select-marketing-actions}

1. Selecione as ações de marketing aplicáveis aos dados que você deseja exportar para o destino. As ações de marketing indicam a intenção para a qual os dados serão exportados para o destino. Você pode selecionar entre ações de marketing definidas pela Adobe ou criar sua própria ação de marketing. Para obter mais informações sobre ações de marketing, consulte a página [visão geral das políticas de uso de dados](../../data-governance/policies/overview.md).

   ![A caixa de diálogo Configurar novo destino com as ações de marketing disponíveis foi realçada. Os controles disponíveis para concluir o fluxo de trabalho Conectar ao destino também são destacados.](../assets/ui/connect-destinations/governance.png)

2. Selecione **[!UICONTROL Save & Exit]** para salvar a configuração de destino ou **[!UICONTROL Next]** para prosseguir para o [fluxo de ativação](activation-overview.md) dos dados de público-alvo.

## Próximas etapas {#next-steps}

Ao ler este documento, você aprendeu a usar a interface do usuário do Experience Platform para estabelecer uma conexão com um destino. Lembrando que os parâmetros de conexão disponíveis e necessários variam de destino para destino. Você também deve consultar a página de documentação de destino no [catálogo de destinos](/help/destinations/catalog/overview.md) para obter informações específicas sobre as entradas necessárias e as opções disponíveis por tipo de destino.

Em seguida, você pode prosseguir para [ativando públicos-alvo](/help/destinations/ui/activation-overview.md) ou [exportando conjuntos de dados](/help/destinations/ui/export-datasets.md) para o seu destino.