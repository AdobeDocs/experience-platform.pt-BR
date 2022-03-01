---
keywords: Experience Platform, home, tópicos populares, conector de origem do Analytics, conector do Analytics, fonte do Analytics, analytics
solution: Experience Platform
title: Criar uma conexão de origem do Adobe Analytics na interface do usuário
topic-legacy: overview
type: Tutorial
description: Saiba como criar uma conexão de origem do Adobe Analytics na interface do usuário para trazer dados do consumidor para o Adobe Experience Platform.
exl-id: 5ddbaf63-feaa-44f5-b2f2-2d5ae507f423
source-git-commit: 06232d4b567ba1d6bed55226aaa08147510c4498
workflow-type: tm+mt
source-wordcount: '1578'
ht-degree: 1%

---

# Criar uma conexão de origem do Adobe Analytics na interface do usuário

Este tutorial fornece etapas para criar uma conexão de origem Adobe Analytics na interface do usuário para trazer [!DNL Analytics] Dados do Conjunto de relatórios no Adobe Experience Platform.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Sistema do Experience Data Model (XDM)](../../../../../xdm/home.md): A estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
* [Perfil do cliente em tempo real](../../../../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.
* [Sandboxes](../../../../../sandboxes/home.md): O Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

### Terminologia principal

É importante entender os seguintes termos principais usados em todo este documento:

* **Atributo padrão**: Atributos padrão são qualquer atributo predefinido pelo Adobe. Eles contêm o mesmo significado para todos os clientes e estão disponíveis no [!DNL Analytics] dados de origem e [!DNL Analytics] grupos de campos de esquema.
* **Atributo personalizado**: Atributos personalizados são qualquer atributo na hierarquia de variável personalizada em [!DNL Analytics]. Os atributos personalizados são usados em uma implementação do Adobe Analytics para capturar informações específicas em um Conjunto de relatórios e podem diferir em seu uso, de Conjunto de relatórios a Conjunto de relatórios. Os atributos personalizados incluem eVars, props e listas. Veja o seguinte [[!DNL Analytics] documentação sobre variáveis de conversão](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/conversion-variables/conversion-var-admin.html?lang=en) para obter mais informações sobre eVars.
* **Qualquer atributo em grupos de campos personalizados**: Os atributos originados de grupos de campos criados por clientes são definidos pelo usuário e não são considerados atributos padrão ou personalizados.
* **Nomes amigáveis**: Nomes amigáveis são rótulos fornecidos por humanos para variáveis personalizadas em um [!DNL Analytics] implementação. Veja o seguinte [[!DNL Analytics] documentação sobre variáveis de conversão](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/conversion-variables/conversion-var-admin.html?lang=en) para obter mais informações sobre nomes amigáveis.

## Criar uma conexão de origem com o Adobe Analytics

Na interface do usuário da plataforma, selecione **[!UICONTROL Fontes]** na navegação à esquerda para acessar o [!UICONTROL Fontes] espaço de trabalho. O [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Também é possível usar a barra de pesquisa para restringir as fontes exibidas.

Em **[!UICONTROL Aplicativos Adobe]** categoria , selecione **[!UICONTROL Adobe Analytics]** e depois selecione **[!UICONTROL Adicionar dados]**.

![catálogo](../../../../images/tutorials/create/analytics/catalog.png)

### Selecionar dados

O **[!UICONTROL Adicionar dados de origem do Analytics]** será exibida. Selecionar **[!UICONTROL Conjunto de relatórios]** para começar a criar uma conexão de origem para os dados do Conjunto de relatórios do Analytics e, em seguida, selecione o Conjunto de relatórios que deseja assimilar. Os Conjuntos de relatórios que não podem ser selecionados já foram assimilados nessa sandbox ou em uma sandbox diferente. Selecionar **[!UICONTROL Próximo]** para continuar.

>[!NOTE]
>
>Várias conexões de entrada podem ser feitas para trazer vários Conjuntos de relatórios, no entanto, apenas um Conjunto de relatórios pode ser usado com o Real-time Customer Data Platform de cada vez.

![](../../../../images/tutorials/create/analytics/add-data.png)

<!---Analytics Report Suites can be configured for one sandbox at a time. To import the same Report Suite into a different sandbox, the dataset flow will have to be deleted and instantiated again via configuration for a different sandbox.--->

### Mapeamento

>[!IMPORTANT]
>
>Suporte à Preparação de dados para o [!DNL Analytics] no momento, a fonte está em beta. O recurso e a documentação estão sujeitos a alterações.

Antes de mapear a [!DNL Analytics] para direcionar o esquema XDM, primeiro você deve selecionar se está usando um esquema padrão ou um esquema personalizado.

Um schema padrão cria um novo schema em seu nome, contendo a variável [!DNL Adobe Analytics ExperienceEvent Template] grupo de campos. Para usar um schema padrão, selecione **[!UICONTROL Esquema padrão]**.

![default-schema](../../../../images/tutorials/create/analytics/default-schema.png)

Com um esquema personalizado, você pode escolher qualquer esquema disponível para [!DNL Analytics] dados, desde que esse schema tenha a variável [!DNL Adobe Analytics ExperienceEvent Template] grupo de campos. Para usar um esquema personalizado, selecione **[!UICONTROL Esquema personalizado]**.

![custom-schema](../../../../images/tutorials/create/analytics/custom-schema.png)

O [!UICONTROL Mapeamento] fornece uma interface para mapear campos de origem para seus campos de esquema de destino apropriados. A partir daqui, você pode mapear variáveis personalizadas para novos grupos de campos do esquema e aplicar cálculos, conforme suportado pela Preparação de dados. Selecione um schema de target para iniciar o processo de mapeamento.

>[!TIP]
>
>Somente schemas que têm a variável [!DNL Adobe Analytics ExperienceEvent Template] grupo de campos são exibidos no menu de seleção de schema. Outros esquemas são omitidos. Se não houver esquemas apropriados disponíveis para seus dados do Conjunto de relatórios, você deverá criar um novo esquema. Para obter etapas detalhadas sobre a criação de schemas, consulte o guia em [criar e editar esquemas na interface do usuário](../../../../../xdm/ui/resources/schemas.md).

![select-schema](../../../../images/tutorials/create/analytics/select-schema.png)

O [!UICONTROL Mapear campos padrão] seção exibe painéis para [!UICONTROL Mapeamentos padrão aplicados], [!UICONTROL Mapeamentos padrão não correspondentes] e [!UICONTROL Mapeamentos personalizados]. Consulte a tabela a seguir para obter informações específicas sobre cada categoria:

| Mapear campos padrão | Descrição |
| --- | --- |
| [!UICONTROL Mapeamentos padrão aplicados] | O [!UICONTROL Mapeamentos padrão aplicados] painel exibe o número total de atributos mapeados. Os mapeamentos padrão se referem a conjuntos de mapeamento entre todos os atributos na origem [!DNL Analytics] dados e atributos correspondentes em [!DNL Analytics] grupo de campos. Eles são pré-mapeados e não podem ser editados. |
| [!UICONTROL Mapeamentos padrão não correspondentes] | O [!UICONTROL Mapeamentos padrão não correspondentes] painel refere-se ao número de atributos mapeados que contêm conflitos de nome amigáveis. Esses conflitos são exibidos quando você está reutilizando um esquema que já tem um conjunto preenchido de descritores de campo de um conjunto de relatórios diferente. Você pode continuar com seu [!DNL Analytics] fluxo de dados, mesmo com conflitos de nome amigáveis. |
| [!UICONTROL Mapeamentos personalizados] | O [!UICONTROL Mapeamentos personalizados] O painel exibe o número de atributos personalizados mapeados, incluindo eVars, props e listas. Os mapeamentos personalizados referem-se a conjuntos de mapeamento entre atributos personalizados na origem [!DNL Analytics] dados e atributos em grupos de campos personalizados incluídos no schema selecionado. |

![campos padrão do mapa](../../../../images/tutorials/create/analytics/map-standard-fields.png)

Para visualizar o [!DNL Analytics] Grupo de campos do esquema do modelo ExperienceEvent, selecione **[!UICONTROL Exibir]** no [!UICONTROL Mapeamentos padrão aplicados] painel.

![view](../../../../images/tutorials/create/analytics/view.png)

O [!UICONTROL Grupo de campos do esquema de modelo do Adobe Analytics ExperienceEvent] fornece uma interface para usar na inspeção da estrutura do esquema. Quando terminar, selecione **[!UICONTROL Fechar]**.

![visualização de grupo de campos](../../../../images/tutorials/create/analytics/field-group-preview.png)

A Platform detecta automaticamente seus conjuntos de mapeamento para qualquer conflito de nome amigável. Se não houver conflitos com seus conjuntos de mapeamento, selecione **[!UICONTROL Próximo]** para continuar.

![mapeamento](../../../../images/tutorials/create/analytics/mapping.png)

Se houver conflitos de nome amigáveis entre seu Conjunto de relatórios de origem e seu esquema selecionado, você ainda poderá continuar com seu [!DNL Analytics] fluxo de dados, reconhecendo que os descritores de campo não serão alterados. Como alternativa, você pode optar por criar um novo schema com um conjunto em branco de descritores.

Selecionar **[!UICONTROL Próximo]** para continuar.

![cautela](../../../../images/tutorials/create/analytics/caution.png)

#### Mapeamentos personalizados

Para usar as funções de Preparação de dados e adicionar um novo mapeamento ou campos calculados para atributos personalizados, selecione **[!UICONTROL Exibir mapeamentos personalizados]**.

![view-custom-mapping](../../../../images/tutorials/create/analytics/view-custom-mapping.png)

Em seguida, selecione **[!UICONTROL Adicionar novo mapeamento]**.

Dependendo das suas necessidades, você pode selecionar **[!UICONTROL Adicionar novo mapeamento]** ou **[!UICONTROL Adicionar campo calculado]** nas opções exibidas.

![add-new-mapping](../../../../images/tutorials/create/analytics/add-new-mapping.png)

Um conjunto de mapeamento vazio é exibido. Selecione o ícone de mapeamento para adicionar um campo de origem.

![select-source-field](../../../../images/tutorials/create/analytics/select-source-field.png)

Você pode usar a interface para navegar pela estrutura do schema de origem e identificar o novo campo de origem que deseja usar. Após selecionar o campo de origem que deseja mapear, selecione **[!UICONTROL Selecionar]**.

![select-mapping](../../../../images/tutorials/create/analytics/select-mapping.png)

Em seguida, selecione o ícone de mapeamento em [!UICONTROL Campo de destino] para mapear o campo de origem selecionado para o campo de destino apropriado.

![select-target-field](../../../../images/tutorials/create/analytics/select-target-field.png)

Semelhante ao schema de origem, você pode usar a interface para navegar pela estrutura do schema de destino e selecionar o campo de destino para o qual deseja mapear. Depois de selecionar o campo de destino apropriado, selecione **[!UICONTROL Selecionar]**.

![select-target-mapping](../../../../images/tutorials/create/analytics/select-target-mapping.png)

Com seu conjunto de mapeamento personalizado concluído, selecione **[!UICONTROL Próximo]** para continuar.

![complete-custom-mapping](../../../../images/tutorials/create/analytics/complete-custom-mapping.png)

A documentação a seguir fornece mais recursos para entender a Preparação de dados, os campos calculados e as funções de mapeamento:

* [Visão geral da preparação de dados](../../../../../data-prep/home.md)
* [Funções de mapeamento da preparação de dados](../../../../../data-prep/functions.md)
* [Adicionar campos calculados](../../../../../data-prep/ui/mapping.md#calculated-fields)

### Fornecer detalhes do fluxo de dados

O **[!UICONTROL Detalhes do fluxo de dados]** é exibida, onde você deve fornecer um nome e uma descrição opcional para o fluxo de dados. Selecionar **[!UICONTROL Próximo]** quando terminar.

![detalhe do fluxo de dados](../../../../images/tutorials/create/analytics/dataflow-detail.png)

### Revisão

O [!UICONTROL Revisão] é exibida, permitindo que você revise o novo fluxo de dados do Analytics antes de criá-lo. Os detalhes da conexão são agrupados por categorias, incluindo:

* [!UICONTROL Conexão]: Exibe a plataforma de origem da conexão.
* [!UICONTROL Tipo de dados]: Exibe o Conjunto de relatórios selecionado e sua ID de conjunto de relatórios correspondente.

![revisão](../../../../images/tutorials/create/analytics/review.png)

### Monitorar o fluxo de dados

Depois que o fluxo de dados for criado, é possível monitorar os dados que estão sendo assimilados por meio dele. No [!UICONTROL Catálogo] , selecione **[!UICONTROL Fluxos de dados]** para visualizar uma lista de fluxos estabelecidos associados à sua conta do Analytics.

![select-dataflows](../../../../images/tutorials/create/analytics/select-dataflows.png)

O **Fluxos de dados** será exibida. Nesta página há um par de fluxos de conjunto de dados, incluindo informações sobre seu nome, dados de origem, tempo de criação e status.

O conector instancia dois fluxos de conjunto de dados. Um fluxo representa dados de preenchimento retroativo e o outro é dados em tempo real. Os dados de preenchimento retroativo não são configurados para Perfil, mas são enviados para o lago de dados para casos de uso analíticos e da ciência de dados.

Para obter mais informações sobre preenchimento retroativo, dados em tempo real e suas respectivas latências, consulte o [Visão geral do Conector de dados do Analytics](../../../../connectors/adobe-applications/analytics.md).

Selecione o fluxo do conjunto de dados que deseja visualizar na lista.

![select-target-dataset](../../../../images/tutorials/create/analytics/select-target-dataset.png)

O **[!UICONTROL Atividade do conjunto de dados]** será exibida. Essa página exibe a taxa de mensagens que estão sendo consumidas no formato de um gráfico. Selecionar **[!UICONTROL Governança de dados]** no cabeçalho superior para acessar os campos de rotulagem.

![atividade do conjunto de dados](../../../../images/tutorials/create/analytics/dataset-activity.png)

Você pode visualizar os rótulos herdados de um fluxo de conjunto de dados da variável [!UICONTROL Governança de dados] tela. Para obter mais informações sobre como rotular dados provenientes do Analytics, visite o [guia de rótulos de uso de dados](../../../../../data-governance/labels/user-guide.md).

![data-gov](../../../../images/tutorials/create/analytics/data-gov.png)

Para excluir um fluxo de dados, direcione para [!UICONTROL Fluxos de dados] e, em seguida, selecione as reticências (`...`) ao lado do nome do fluxo de dados e selecione [!UICONTROL Excluir].

![excluir](../../../../images/tutorials/create/analytics/delete.png)

## Próximas etapas e recursos adicionais

Depois que a conexão é criada, o fluxo de dados é criado automaticamente para conter os dados recebidos e preencher um conjunto de dados com o esquema selecionado. Além disso, ocorre o preenchimento retroativo de dados e a assimilação de até 13 meses de dados históricos. Quando a ingestão inicial for concluída, [!DNL Analytics] dados e ser usado por serviços de plataforma downstream, como [!DNL Real-time Customer Profile] e Serviço de segmentação. Consulte os seguintes documentos para obter mais detalhes:

* [[!DNL Real-time Customer Profile] visão geral](../../../../../profile/home.md)
* [[!DNL Segmentation Service] visão geral](../../../../../segmentation/home.md)
* [[!DNL Data Science Workspace] visão geral](../../../../../data-science-workspace/home.md)
* [[!DNL Query Service] visão geral](../../../../../query-service/home.md)

O vídeo a seguir é destinado a respaldar a compreensão da assimilação de dados pelo uso do conector do Adobe Analytics Source:

>[!WARNING]
>
> O [!DNL Platform] A interface do usuário exibida no vídeo a seguir está desatualizada. Consulte a documentação acima para obter as capturas de tela e a funcionalidade mais recentes da interface do usuário.

>[!VIDEO](https://video.tv.adobe.com/v/29687?quality=12&learn=on)
