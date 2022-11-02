---
keywords: conectar destino, conexão de destino, como conectar destino
title: Criar uma nova conexão de destino
type: Tutorial
description: Saiba como se conectar a um destino no Adobe Experience Platform, ativar alertas e configurar ações de marketing para seu destino conectado.
exl-id: 56d7799a-d1da-4727-ae79-fb2c775fe5a5
source-git-commit: 434b9ed4f64320b5fd73b752716cb34a8e48aec9
workflow-type: tm+mt
source-wordcount: '1106'
ht-degree: 0%

---

# Criar uma nova conexão de destino

>[!IMPORTANT]
> 
>* Para se conectar a um destino, é necessário **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.
>* Para se conectar a um destino que seja compatível com exportações de conjunto de dados, é necessário **[!UICONTROL Gerenciar e ativar destinos do conjunto de dados]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.


## Visão geral {#overview}

Antes de enviar dados do público-alvo para um destino, você deve configurar uma conexão com a plataforma de destino. Este artigo mostra como configurar uma nova conexão de destino, para a qual você pode ativar segmentos ou exportar conjuntos de dados usando a interface do usuário do Adobe Experience Platform.

## Encontre o destino desejado no catálogo {#setup}

1. Ir para **[!UICONTROL Conexões]** > **[!UICONTROL Destinos]** e selecione o **[!UICONTROL Catálogo]** guia .

   ![Captura de tela da interface do usuário do Experience Platform, mostrando a página de catálogo de destinos.](../assets/ui/connect-destinations/catalog.png)

2. Os cartões de destino no catálogo podem ter controles de ação diferentes, dependendo se você tem uma conexão existente com o destino e se os destinos oferecem suporte para a ativação de segmentos, a exportação de conjuntos de dados ou ambos. Você pode ver qualquer um dos seguintes controles para cartões de destino:

   * **[!UICONTROL Configurar]**. Primeiro, é necessário configurar uma conexão com esse destino antes de ativar segmentos ou exportar conjuntos de dados.
   * **[!UICONTROL Ativar]**. Uma conexão já foi configurada para esse destino. Esse destino oferece suporte à ativação de segmentos e às exportações de conjunto de dados.
   * **[!UICONTROL Ativar segmentos]**. Uma conexão já foi configurada para esse destino. Este destino suporta apenas a ativação de segmentos.

   Para obter mais informações sobre a diferença entre esses controles, consulte também [Catálogo](../ui/destinations-workspace.md#catalog) da documentação do espaço de trabalho de destino.

   Selecione um **[!UICONTROL Configurar]**, **[!UICONTROL Ativar]** ou **[!UICONTROL Ativar segmentos]**, dependendo do controle disponível para você.

   ![Captura de tela da interface do usuário do Experience Platform, mostrando a página de catálogo de destinos com o controle Configurar destacado.](../assets/ui/connect-destinations/set-up.png)

   ![Captura de tela da interface do usuário do Experience Platform, mostrando a página de catálogo de destinos com o controle Ativate segments destacado.](../assets/ui/connect-destinations/activate-segments.png)

3. Se você selecionou **[!UICONTROL Configurar]**, pule para a próxima etapa, para [autenticar](#authenticate) ao destino.

   Se você selecionou **[!UICONTROL Ativar]**, **[!UICONTROL Ativar segmentos]** ou **[!UICONTROL Exportar conjuntos de dados]**, agora é possível ver uma lista de conexões de destino existentes.

   Selecionar **[!UICONTROL Configurar novo destino]** para estabelecer uma nova conexão com o destino.

   ![Captura de tela da interface do usuário do Experience Platform, mostrando uma lista de destinos disponíveis e o campo Configure new destination control realçado.](../assets/ui/connect-destinations/configure-new-destination.png)

## Autenticar para destino {#authenticate}

A primeira etapa na conexão com um destino é autenticar para a plataforma de destino.

Dependendo do destino ao qual você está se conectando, você pode ser levado à página do parceiro de destino para autenticar, ou pode ser solicitado a inserir credenciais de autenticação diretamente no fluxo de trabalho da Plataforma. Abaixo está um exemplo da entrada necessária para autenticação em um [!DNL Amazon S3] destino. Instruções detalhadas sobre a entrada necessária são fornecidas em cada página de documentação de destino (consulte, por exemplo, a seção de autenticação para [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#authenticate) e [[!DNL Facebook]](/help/destinations/catalog/social/facebook.md#authenticate)).

**[!DNL Amazon S3]parâmetros de autenticação obrigatórios e opcionais**

![Imagem que mostra os parâmetros de entrada obrigatórios e opcionais ao autenticar para um destino Amazon S3.](../assets/ui/connect-destinations/authenticate-amazon-s3-example.png)

## Configurar parâmetros de conexão {#set-up-connection-parameters}

Se você já tiver configurado a autenticação para o destino, poderá continuar com a conta existente ou poderá configurar uma nova conta.

Dependendo do destino ao qual você está se conectando, talvez você seja solicitado a inserir diferentes tipos de parâmetros de conexão. Por exemplo, ao se conectar a um [!DNL Amazon S3] , você será solicitado a fornecer detalhes sobre o [!DNL Amazon S3] nome do bucket e caminho da pasta onde os arquivos serão depositados. Abaixo estão dois exemplos de entradas necessárias para um [!DNL Amazon S3] e um [!DNL Trade Desk] destino. Instruções detalhadas sobre a entrada necessária são fornecidas em cada página de documentação de destino.

>[!IMPORTANT]
>
>As imagens abaixo são usadas somente para fins ilustrativos. Os detalhes da conexão de destino variam entre destinos. Para obter informações detalhadas sobre os detalhes da conexão com seu destino, leia o **Conecte-se ao destino** em cada [catálogo de destino](../catalog/overview.md) page (por exemplo, [[!DNL Google Customer Match]](../catalog/advertising/google-customer-match.md#connect), [[!DNL Trade Desk]](/help/destinations/catalog/advertising/tradedesk.md#connect)ou [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details)).

**[!DNL Amazon S3]parâmetros de entrada obrigatórios e opcionais**

![Imagem que mostra os parâmetros de entrada obrigatórios e opcionais ao se conectar a um destino Amazon S3.](../assets/ui/connect-destinations/connect-destination-amazons3-example.png)

**[!DNL The Trade Desk]parâmetros de entrada obrigatórios e opcionais**

![Imagem mostrando os parâmetros de entrada obrigatórios e opcionais ao se conectar a um destino do Trade Desk.](../assets/ui/connect-destinations/connect-destination-trade-desk-example.png)

### Configurar opções de formatação de arquivo para arquivos exportados {#file-formatting-and-compression-options}

Para destinos com base em arquivos, você pode definir várias configurações relacionadas à forma como os arquivos exportados são formatados e compactados. Para obter mais informações sobre todas as opções disponíveis de formatação e compactação, leia a [Tutorial Configurar opções de formatação de arquivo para destinos com base em arquivo](/help/destinations/ui/batch-destinations-file-formatting-options.md).

![Imagem que mostra a seleção do tipo de arquivo e várias opções para arquivos CSV.](/help/destinations/assets/ui/connect-destinations/file-formatting-options.png)

### Configurar a conexão de destino para ativação de segmento ou exportações de conjunto de dados {#segment-activation-or-dataset-exports}

Alguns destinos com base em arquivos suportam a ativação de segmentos e exportações de conjuntos de dados. Para esses destinos, você pode escolher se deseja criar uma conexão que permite ativar segmentos ou exportar conjuntos de dados.

![Imagem que mostra o controle de seleção do tipo de dados que permite aos usuários selecionar entre ativação de segmento e exportações de conjunto de dados.](/help/destinations/assets/ui/connect-destinations/data-type-selection.png)

### Ativar alertas de destino {#enable-alerts}

1. (Opcional) Selecione os alertas de fluxo de dados de destino que você deseja assinar. Você pode assinar alertas ao criar um fluxo de dados para receber mensagens de alerta sobre o status, o sucesso ou a falha da execução do fluxo. Os alertas disponíveis diferem com base no tipo de destino (baseado em arquivo ou streaming) ao qual você está se conectando. Ler [Assinar alertas de destino no contexto](alerts.md) para obter informações detalhadas sobre alertas de fluxo de dados de destino.

   ![A caixa de diálogo Configure new destination with the in-context destination subscription options (Configurar novo destino com as opções de assinatura de alertas de destino no contexto) foi realçada.](../assets/ui/connect-destinations/subscribe-to-alerts.png)

2. Selecione **[!UICONTROL Próximo]**.

   ![A caixa de diálogo Configurar novo destino com o Próximo controle é realçada, permitindo que o usuário continue para a próxima etapa do fluxo de trabalho.](../assets/ui/connect-destinations/next.png)

## Selecionar ações de marketing {#select-marketing-actions}

1. Selecione as ações de marketing aplicáveis aos dados que você deseja exportar para o destino. As ações de marketing indicam a intenção para a qual os dados serão exportados para o destino. Você pode selecionar ações de marketing definidas pelo Adobe ou criar sua própria ação de marketing. Para obter mais informações sobre ações de marketing, consulte o [visão geral das políticas de uso de dados](../../data-governance/policies/overview.md) página.

   ![A caixa de diálogo Configure new destination with the available marketing actions (Configurar novo destino com as ações de marketing disponíveis) é realçada. Os controles disponíveis para concluir o workflow Conectar ao destino também são destacados.](../assets/ui/connect-destinations/governance.png)

2. Selecionar **[!UICONTROL Salvar e sair]** para salvar a configuração de destino, ou selecione **[!UICONTROL Próximo]** para prosseguir para os dados do público-alvo [fluxo de ativação](activation-overview.md).

## Próximas etapas {#next-steps}

Ao ler este documento, você aprendeu a usar a interface do usuário do Experience Platform para estabelecer uma conexão com um destino. Como lembrete, os parâmetros de conexão disponíveis e necessários variam de destino para destino. Você também deve consultar a página de documentação de destino na [catálogo de destinos](/help/destinations/catalog/overview.md) para obter informações específicas sobre as entradas necessárias e as opções disponíveis por tipo de destino.

Em seguida, você pode prosseguir para [ativação de segmentos](/help/destinations/ui/activation-overview.md) ou [exportação de conjuntos de dados](/help/destinations/ui/export-datasets.md) ao seu destino.