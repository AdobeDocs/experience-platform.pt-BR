---
title: Criar uma conexão do Adobe Analytics Source na interface
description: Saiba como criar uma conexão de origem do Adobe Analytics na interface do usuário para trazer dados do consumidor para o Adobe Experience Platform.
exl-id: 5ddbaf63-feaa-44f5-b2f2-2d5ae507f423
source-git-commit: 71932d6f743d8cf767ce4e088231e61e9c2160e0
workflow-type: tm+mt
source-wordcount: '2672'
ht-degree: 3%

---

# Criar uma conexão de origem do Adobe Analytics na interface

Este tutorial fornece etapas para a criação de uma conexão de origem do Adobe Analytics na interface do usuário para trazer os dados do conjunto de relatórios do Adobe Analytics para a Adobe Experience Platform.

## Introdução

Este tutorial requer um entendimento prático dos seguintes componentes do Experience Platform:

* [Sistema do Experience Data Model (XDM)](../../../../../xdm/home.md): a estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
* [Perfil de cliente em tempo real](../../../../../profile/home.md): fornece um perfil de cliente unificado em tempo real com base em dados agregados de várias fontes.
* [Sandboxes](../../../../../sandboxes/home.md): o Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

### Terminologia principal

É importante entender os seguintes termos principais usados neste documento:

* **Atributo padrão**: atributos padrão são todos os atributos predefinidos pelo Adobe. Eles contêm o mesmo significado para todos os clientes e estão disponíveis nos grupos de campos de dados de origem [!DNL Analytics] e esquema [!DNL Analytics].
* **Atributo personalizado**: atributos personalizados são qualquer atributo na hierarquia de variáveis personalizadas em [!DNL Analytics]. Os atributos personalizados são usados em uma implementação do Adobe Analytics para capturar informações específicas em um conjunto de relatórios e podem diferir no uso de cada conjunto de relatórios. Os atributos personalizados incluem eVars, propriedades e listas. Consulte a [[!DNL Analytics] documentação sobre variáveis de conversão](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/conversion-variables/conversion-var-admin.html) a seguir para obter mais informações sobre eVars.
* **Qualquer atributo em grupos de campos personalizados**: atributos originários de grupos de campos criados por clientes são todos definidos pelo usuário e não são considerados atributos padrão nem personalizados.
* **Nomes amigáveis**: nomes amigáveis são rótulos fornecidos por humanos para variáveis personalizadas em uma implementação [!DNL Analytics]. Consulte a seguinte [[!DNL Analytics] documentação sobre variáveis de conversão](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/conversion-variables/conversion-var-admin.html) para obter mais informações sobre nomes amigáveis.

## Criar uma conexão de origem com o Adobe Analytics

>[!NOTE]
>
>Ao criar um fluxo de dados de origem do Analytics em uma sandbox de produção, dois fluxos de dados são criados:
>
>* Um fluxo de dados que faz um preenchimento retroativo de 13 meses de dados históricos do conjunto de relatórios no data lake. Esse fluxo de dados termina quando o preenchimento retroativo é concluído.
>* Um fluxo de dados que envia dados em tempo real para o data lake e para [!DNL Real-Time Customer Profile]. Esse fluxo de dados é executado continuamente.

Na interface da Platform, selecione **[!UICONTROL Fontes]** na navegação à esquerda para acessar o espaço de trabalho [!UICONTROL Fontes]. A tela [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Você também pode usar a barra de pesquisa para restringir as fontes exibidas.

Na categoria **[!UICONTROL aplicativos de Adobe]**, selecione **[!UICONTROL Adobe Analytics]** e **[!UICONTROL Adicionar dados]**.

![catálogo](../../../../images/tutorials/create/analytics/catalog.png)

### Selecionar dados

>[!IMPORTANT]
>
>Os conjuntos de relatórios listados na tela podem vir de várias regiões. Você é responsável por entender as limitações e obrigações de seus dados e como usá-los entre regiões do Adobe Experience Platform. Verifique se isso é permitido pela sua empresa.

A etapa **[!UICONTROL Adicionar dados]** da origem do Analytics fornece uma lista de dados do conjunto de relatórios [!DNL Analytics] para criar uma conexão de origem com.

Um conjunto de relatórios é um contêiner de dados que forma a base do relatório [!DNL Analytics]. Uma organização pode ter muitos conjuntos de relatórios, cada um contendo diferentes conjuntos de dados.

Você pode assimilar conjuntos de relatórios de qualquer região (Estados Unidos, Reino Unido ou Cingapura) desde que eles estejam mapeados para a mesma organização da instância de sandbox de Experience Platform em que a conexão de origem está sendo criada. Um conjunto de relatórios pode ser assimilado usando apenas um único fluxo de dados ativo. Um conjunto de relatórios que não pode ser selecionado já foi assimilado, na sandbox que você está usando ou em uma sandbox diferente.

Várias conexões de entrada podem ser feitas para trazer vários conjuntos de relatórios para a mesma sandbox. Se os conjuntos de relatórios tiverem esquemas diferentes para variáveis (como eVars ou eventos), eles deverão ser mapeados para campos específicos nos grupos de campos personalizados e evitar conflitos de dados usando o [Preparo de dados](../../../../../data-prep/ui/mapping.md). Os conjuntos de relatórios podem ser adicionados somente a uma única sandbox.

![](../../../../images/tutorials/create/analytics/report-suite.png)

>[!NOTE]
>
>Os dados de vários conjuntos de relatórios podem ser ativados para o Perfil do cliente em tempo real somente se não houver conflitos de dados, como duas propriedades personalizadas (eVars, listas e props) com significado diferente.

Para criar uma conexão de origem [!DNL Analytics], selecione um conjunto de relatórios e clique em **[!UICONTROL Avançar]** para continuar.

![](../../../../images/tutorials/create/analytics/add-data.png)

&lt;!—Os Conjuntos de relatórios do Analytics podem ser configurados para uma sandbox por vez. Para importar o mesmo Conjunto de relatórios para uma sandbox diferente, o fluxo do conjunto de dados terá de ser excluído e instanciado novamente por meio da configuração de uma sandbox diferente.—>

### Mapeamento

>[!IMPORTANT]
>
>As transformações de Preparo de dados podem adicionar latência ao fluxo de dados geral. A latência adicional adicionada varia de acordo com a complexidade da lógica de transformação.

Antes de mapear os dados do [!DNL Analytics] para o esquema XDM de destino, você deve primeiro selecionar se está usando um esquema padrão ou um esquema personalizado.

Um esquema padrão cria um novo esquema em seu nome, contendo o grupo de campos [!DNL Adobe Analytics ExperienceEvent Template]. Para usar um esquema padrão, selecione **[!UICONTROL Esquema padrão]**.

![esquema-padrão](../../../../images/tutorials/create/analytics/default-schema.png)

Com um esquema personalizado, você pode escolher qualquer esquema disponível para seus dados do [!DNL Analytics], desde que esse esquema tenha o grupo de campos [!DNL Adobe Analytics ExperienceEvent Template]. Para usar um esquema personalizado, selecione **[!UICONTROL Esquema personalizado]**.

![esquema personalizado](../../../../images/tutorials/create/analytics/custom-schema.png)

A página [!UICONTROL Mapping] fornece uma interface para mapear campos de origem para seus campos de esquema de destino apropriados. Aqui, é possível mapear variáveis personalizadas para novos grupos de campos de esquema e aplicar cálculos de acordo com o Preparo de dados. Selecione um schema de destino para iniciar o processo de mapeamento.

>[!TIP]
>
>Somente esquemas que têm o grupo de campos [!DNL Adobe Analytics ExperienceEvent Template] são exibidos no menu de seleção de esquema. Outros esquemas são omitidos. Se não houver esquemas apropriados disponíveis para seus dados do Conjunto de relatórios, você deve criar um novo esquema. Para obter etapas detalhadas sobre como criar esquemas, consulte o guia em [criar e editar esquemas na interface](../../../../../xdm/ui/resources/schemas.md).

![selecionar-esquema](../../../../images/tutorials/create/analytics/select-schema.png)

A seção [!UICONTROL Mapear campos padrão] exibe painéis para [!UICONTROL Mapeamentos padrão aplicados], [!UICONTROL Mapeamentos padrão não correspondentes] e [!UICONTROL Mapeamentos personalizados]. Consulte a tabela a seguir para obter informações específicas sobre cada categoria:

| Mapear campos padrão | Descrição |
| --- | --- |
| [!UICONTROL Mapeamentos padrão aplicados] | O painel [!UICONTROL Mapeamentos padrão aplicados] exibe o número total de atributos mapeados. Os mapeamentos padrão se referem aos conjuntos de mapeamento entre todos os atributos nos dados de origem [!DNL Analytics] e atributos correspondentes no grupo de campos [!DNL Analytics]. Eles são pré-mapeados e não podem ser editados. |
| [!UICONTROL Mapeamentos padrão não correspondentes] | O painel [!UICONTROL Mapeamentos padrão não correspondentes] refere-se ao número de atributos mapeados que contêm conflitos de nome amigável. Esses conflitos aparecem quando você está reutilizando um esquema que já tem um conjunto preenchido de descritores de campo de um conjunto de relatórios diferente. Você pode continuar com o fluxo de dados do [!DNL Analytics] mesmo com conflitos de nome amigáveis. |
| [!UICONTROL Mapeamentos personalizados] | O painel [!UICONTROL Mapeamentos personalizados] exibe o número de atributos personalizados mapeados, incluindo eVars, propriedades e listas. Mapeamentos personalizados se referem aos conjuntos de mapeamento entre atributos personalizados nos dados de origem [!DNL Analytics] e atributos nos grupos de campos personalizados incluídos no esquema selecionado. |

![mapear-campos-padrão](../../../../images/tutorials/create/analytics/map-standard-fields.png)

Para visualizar o grupo de campos de esquema de modelo ExperienceEvent [!DNL Analytics], selecione **[!UICONTROL Exibir]** no painel [!UICONTROL Mapeamentos padrão aplicados].

![exibir](../../../../images/tutorials/create/analytics/view.png)

A página [!UICONTROL Grupo de campos do esquema do modelo de ExperienceEvent do Adobe Analytics] fornece uma interface a ser usada para inspecionar a estrutura do esquema. Quando terminar, selecione **[!UICONTROL Fechar]**.

![visualização de grupo de campos](../../../../images/tutorials/create/analytics/field-group-preview.png)

O Platform detecta automaticamente seus conjuntos de mapeamento para qualquer conflito de nome amigável. Se não houver conflitos com seus conjuntos de mapeamento, selecione **[!UICONTROL Avançar]** para continuar.

![mapeamento](../../../../images/tutorials/create/analytics/mapping.png)

>[!TIP]
>
>Se houver conflitos de nome amigável entre seu Conjunto de relatórios de origem e o esquema selecionado, você ainda poderá continuar com o fluxo de dados do [!DNL Analytics], reconhecendo que os descritores de campo não serão alterados. Como alternativa, você pode optar por criar um novo esquema com um conjunto de descritores em branco.

#### Mapeamentos personalizados

É possível usar as funções de Preparo de dados para adicionar novos mapeamentos personalizados ou campos calculados para atributos personalizados. Para adicionar mapeamentos personalizados, selecione **[!UICONTROL Personalizado]**.

![personalizado](../../../../images/tutorials/create/analytics/custom.png)

Dependendo das suas necessidades, você pode selecionar **[!UICONTROL Adicionar novo mapeamento]** ou **[!UICONTROL Adicionar campo calculado]** e continuar criando mapeamentos personalizados para seus atributos personalizados. Para obter etapas abrangentes sobre como usar as funções de Preparo de dados, leia o [guia da interface do usuário do Preparo de dados](../../../../../data-prep/ui/mapping.md).

A documentação a seguir fornece mais recursos sobre como entender o Preparo de dados, campos calculados e funções de mapeamento:

* [Visão geral do Preparo de dados](../../../../../data-prep/home.md)
* [Funções de mapeamento de Preparo de dados](../../../../../data-prep/functions.md)
* [Adicionar campos calculados](../../../../../data-prep/ui/mapping.md#calculated-fields)

<!-- 
To use Data Prep functions and add new mapping or calculated fields for custom attributes, select **[!UICONTROL View custom mappings]**.

![view-custom-mapping](../../../../images/tutorials/create/analytics/view-custom-mapping.png)

Next, select **[!UICONTROL Add new mapping]**.

Depending on your needs, you can select either **[!UICONTROL Add new mapping]** or **[!UICONTROL Add calculated field]** from the options that appear. 

![add-new-mapping](../../../../images/tutorials/create/analytics/add-new-mapping.png)

An empty mapping set appears. Select the mapping icon to add a source field.

![select-source-field](../../../../images/tutorials/create/analytics/select-source-field.png)

You can use the interface to navigate through the source schema structure and identify the new source field that you want to use. Once you have selected the source field that you want to map, select **[!UICONTROL Select]**.

![select-mapping](../../../../images/tutorials/create/analytics/select-mapping.png)

Next, select the mapping icon under [!UICONTROL Target Field] to map your selected source field to its appropriate target field.

![select-target-field](../../../../images/tutorials/create/analytics/select-target-field.png)

Similar to the source schema, you can use the interface to navigate through the target schema structure and select the target field you want to map to. Once you have selected the appropriate target field, select **[!UICONTROL Select]**.

![select-target-mapping](../../../../images/tutorials/create/analytics/select-target-mapping.png)

With your custom mapping set completed, select **[!UICONTROL Next]** to proceed.

![complete-custom-mapping](../../../../images/tutorials/create/analytics/complete-custom-mapping.png) -->

## Filtragem para o perfil do cliente em tempo real {#filtering-for-profile}

>[!CONTEXTUALHELP]
>id="platform_data_prep_analytics_filtering"
>title="Criar regras de filtro"
>abstract="Defina as regras de filtragem em nível de linha e coluna ao enviar dados para o perfil do cliente em tempo real. Use a filtragem de nível de linha para aplicar condições e determinar quais dados **incluir para ingestão de perfil**. Use a filtragem de nível de coluna para selecionar as colunas de dados que deseja **excluir para ingestão de perfil**. As regras de filtragem não se aplicam aos dados enviados para o data lake."

Depois de concluir os mapeamentos dos dados do conjunto de relatórios do [!DNL Analytics], você poderá aplicar regras e condições de filtragem para incluir ou excluir seletivamente os dados da assimilação no Perfil do cliente em tempo real. O suporte para filtragem está disponível apenas para dados do [!DNL Analytics] e os dados são filtrados apenas antes da inserção de [!DNL Profile.]. Todos os dados são assimilados no data lake.

>[!BEGINSHADEBOX]

**Informações adicionais sobre Preparação de dados e filtragem de dados do Analytics para o Perfil de cliente em tempo real**

* Você pode usar a funcionalidade de filtragem para dados que vão para o Perfil, mas não para dados que vão para o data lake.
* Você pode usar a filtragem para dados em tempo real, mas não pode filtrar dados de preenchimento retroativo.
   * A origem [!DNL Analytics] não preenche dados retroativamente com o Perfil.
* Se você utilizar as configurações de Preparo de dados durante a configuração inicial de um fluxo do [!DNL Analytics], essas alterações também serão aplicadas ao preenchimento retroativo automático de 13 meses.
   * No entanto, esse não é o caso da filtragem, pois ela é reservada apenas para dados em tempo real.
* O Preparo de dados é aplicado aos caminhos de transmissão e assimilação em lote. Se você modificar uma configuração existente de Preparo de dados, essas alterações serão aplicadas aos novos dados recebidos pelos caminhos de transmissão e assimilação em lote.
   * No entanto, qualquer configuração de Preparo de dados não se aplica a dados que já foram assimilados no Experience Platform, independentemente de serem dados de transmissão ou em lote.
* Os atributos padrão do Analytics são sempre mapeados automaticamente. Portanto, não é possível aplicar transformações a atributos padrão.
   * No entanto, você pode filtrar atributos padrão, desde que eles não sejam necessários no Serviço de identidade ou Perfil.
* Não é possível usar a filtragem em nível de coluna para filtrar campos obrigatórios e campos de identidade.
* Embora seja possível filtrar identidades secundárias, especificamente AAID e AACustomID, não é possível filtrar a ECID.
* Quando ocorre um erro de transformação, a coluna correspondente resulta em NULL.

>[!ENDSHADEBOX]

### Filtragem em nível de linha

>[!IMPORTANT]
>
>Use a filtragem de nível de linha para aplicar condições e determinar quais dados **incluir para ingestão de perfil**. Use a filtragem em nível de coluna para selecionar as colunas de dados que você deseja **excluir para assimilação de perfil**.

Você pode filtrar dados para assimilação de [!DNL Profile] em nível de linha e em nível de coluna. A filtragem em nível de linha permite definir critérios como cadeia de caracteres contém, é igual a, começa ou termina com. Você também pode usar a filtragem em nível de linha para unir condições usando `AND` e `OR`, e negar condições usando `NOT`.

Para filtrar os dados do [!DNL Analytics] no nível de linha, selecione **[!UICONTROL Filtro de linha]**.

![filtro-linha](../../../../images/tutorials/create/analytics/row-filter.png)

Use o painel à esquerda para navegar pela hierarquia do esquema e selecione o atributo de esquema de sua escolha para detalhar ainda mais um esquema específico.

![painel esquerdo](../../../../images/tutorials/create/analytics/left-rail.png)

Depois de identificar o atributo que deseja configurar, selecione e arraste o atributo do painel esquerdo para o painel Filtragem.

![painel-filtro](../../../../images/tutorials/create/analytics/filtering-panel.png)

Para configurar condições diferentes, selecione **[!UICONTROL igual a]** e selecione uma condição na janela suspensa que aparece.

A lista de condições configuráveis inclui:

* [!UICONTROL é igual a]
* [!UICONTROL não é igual a]
* [!UICONTROL começa com]
* [!UICONTROL termina com]
* [!UICONTROL não termina com]
* [!UICONTROL contém]
* [!UICONTROL não contém]
* [!UICONTROL existe]
* [!UICONTROL não existe]

![condições](../../../../images/tutorials/create/analytics/conditions.png)

Em seguida, insira os valores que deseja incluir com base no atributo selecionado. No exemplo abaixo, [!DNL Apple] e [!DNL Google] são selecionados para assimilação como parte do atributo **[!UICONTROL Manufaturer]**.

![include-manufaturer](../../../../images/tutorials/create/analytics/include-manufacturer.png)

Para especificar ainda mais suas condições de filtragem, adicione outro atributo do esquema e adicione valores com base nesse atributo. No exemplo abaixo, o atributo **[!UICONTROL Model]** é adicionado e modelos como [!DNL iPhone 13] e [!DNL Google Pixel 6] são filtrados para assimilação.

![include-model](../../../../images/tutorials/create/analytics/include-model.png)

Para adicionar um novo contêiner, selecione as reticências (`...`) na parte superior direita da interface de filtragem e selecione **[!UICONTROL Adicionar contêiner]**.

![adicionar-contêiner](../../../../images/tutorials/create/analytics/add-container.png)

Depois que um novo contêiner for adicionado, selecione **[!UICONTROL Incluir]** e **[!UICONTROL Excluir]** da janela suspensa exibida.

![excluir](../../../../images/tutorials/create/analytics/exclude.png)

Em seguida, conclua o mesmo processo arrastando os atributos do esquema e adicionando os valores correspondentes que deseja excluir da filtragem. No exemplo abaixo, [!DNL iPhone 12], [!DNL iPhone 12 mini] e [!DNL Google Pixel 5] são todos filtrados da exclusão do atributo **[!UICONTROL Modelo]**, paisagem é excluída da **[!UICONTROL Orientação da tela]** e número do modelo [!DNL A1633] é excluída do **[!UICONTROL Número do modelo]**.

Quando terminar, selecione **[!UICONTROL Próximo]**.

![excluir-exemplos](../../../../images/tutorials/create/analytics/exclude-examples.png)

### Filtragem em nível de coluna

Selecione **[!UICONTROL Filtro de coluna]** no cabeçalho para aplicar a filtragem em nível de coluna.

![filtro-coluna](../../../../images/tutorials/create/analytics/column-filter.png)

A página é atualizada em uma árvore de esquema interativa, exibindo os atributos do esquema no nível da coluna. Aqui, você pode selecionar as colunas de dados que deseja excluir da assimilação de [!DNL Profile]. Como alternativa, é possível expandir uma coluna e selecionar atributos específicos para exclusão.

Por padrão, todos os [!DNL Analytics] vão para [!DNL Profile] e esse processo permite que ramificações de dados XDM sejam excluídas da assimilação de [!DNL Profile].

Quando terminar, selecione **[!UICONTROL Próximo]**.

![colunas-selecionadas](../../../../images/tutorials/create/analytics/columns-selected.png)

### Filtrar identidades secundárias

Use um filtro de coluna para excluir identidades secundárias da assimilação de perfis. Para filtrar identidades secundárias, selecione **[!UICONTROL Filtro de coluna]** e **[!UICONTROL _identidades]**.

O filtro se aplica somente quando uma identidade é marcada como secundária. Se as identidades forem selecionadas, mas um evento chegar com uma das identidades marcadas como primárias, elas não serão filtradas.

![identidades-secundárias](../../../../images/tutorials/create/analytics/secondary-identities.png)

### Fornecer detalhes do fluxo de dados

A etapa **[!UICONTROL Detalhes do fluxo de dados]** é exibida, onde você deve fornecer um nome e uma descrição opcional para o fluxo de dados. Selecione **[!UICONTROL Avançar]** quando terminar.

![detalhes do fluxo de dados](../../../../images/tutorials/create/analytics/dataflow-detail.png)

### Revisar

A etapa [!UICONTROL Revisão] é exibida, permitindo que você revise o novo fluxo de dados do Analytics antes que ele seja criado. Os detalhes da conexão são agrupados por categorias, incluindo:

* [!UICONTROL Conexão]: exibe a plataforma de origem da conexão.
* [!UICONTROL Tipo de dados]: exibe o Conjunto de relatórios selecionado e sua ID de Conjunto de relatórios correspondente.

![avaliação](../../../../images/tutorials/create/analytics/review.png)

## Monitorar seu fluxo de dados {#monitor-your-dataflow}

Depois que o fluxo de dados for concluído, selecione **[!UICONTROL Fluxos de dados]** no catálogo de fontes para monitorar a atividade e o status dos seus dados.

![O catálogo de fontes com a guia de fluxos de dados selecionada.](../../../../images/tutorials/create/analytics/select-dataflows.png)

Uma lista dos fluxos de dados existentes do Analytics em sua organização é exibida. Aqui, selecione um conjunto de dados de destino para visualizar sua respectiva atividade de assimilação.

![Uma lista de fluxos de dados existentes do Adobe Analytics em sua organização.](../../../../images/tutorials/create/analytics/select-target-dataset.png)

A página [!UICONTROL Atividade do conjunto de dados] fornece informações sobre o progresso dos dados que estão sendo enviados do Analytics para o Experience Platform. A interface exibe métricas como o total de registros no mês anterior, o total de registros assimilados nos últimos sete dias e o tamanho dos dados no mês anterior.

A origem instancia dois fluxos de conjunto de dados. Um fluxo representa dados de preenchimento retroativo e o outro é para dados em tempo real. Os dados de preenchimento retroativo não são configurados para assimilação no Perfil do cliente em tempo real, mas são enviados ao data lake para casos de uso analíticos e de ciência de dados.

Para obter mais informações sobre preenchimento retroativo, dados em tempo real e suas respectivas latências, leia a [Visão geral da origem do Analytics](../../../../connectors/adobe-applications/analytics.md).

![A página de atividade do conjunto de dados para um determinado conjunto de dados de destino para dados do Adobe Analytics.](../../../../images/tutorials/create/analytics/dataset-activity.png)

>[!NOTE]
>
>A página de atividade do conjunto de dados não exibe informações sobre lotes, pois o conector de origem do Analytics é totalmente gerenciado pelo Adobe. É possível monitorar se os dados estão fluindo observando as métricas sobre registros assimilados.

## Excluir seu fluxo de dados {#delete-dataflow}

Para excluir o fluxo de dados do Analytics, selecione **[!UICONTROL Fluxos de dados]** no cabeçalho superior do espaço de trabalho de fontes. Use a página de fluxos de dados para localizar o fluxo de dados do Analytics que você deseja excluir e selecione as reticências (`...`) ao lado dela. Em seguida, use o menu suspenso e selecione **[!UICONTROL Excluir]**.

* A exclusão do fluxo de dados ativo do Analytics também excluirá seu conjunto de dados subjacente.
* A exclusão do fluxo de dados de preenchimento retroativo do Analytics não exclui o conjunto de dados subjacente, mas interromperá o processo de preenchimento retroativo do conjunto de relatórios correspondente. Se você excluir o fluxo de dados de preenchimento retroativo, os dados assimilados ainda poderão ser visualizados no conjunto de dados.

## Próximas etapas e recursos adicionais

Depois que a conexão é criada, o fluxo de dados é criado automaticamente para conter os dados recebidos e preencher um conjunto de dados com o esquema selecionado. Além disso, ocorre o preenchimento retroativo de dados e a assimilação de até 13 meses de dados históricos. Quando a assimilação inicial for concluída, [!DNL Analytics] dados e serão usados por serviços downstream da plataforma, como o [!DNL Real-Time Customer Profile] e o Serviço de segmentação. Consulte os seguintes documentos para obter mais detalhes:

* [Visão geral do [!DNL Real-Time Customer Profile]](../../../../../profile/home.md)
* [Visão geral do [!DNL Segmentation Service]](../../../../../segmentation/home.md)
* [Visão geral do [!DNL Data Science Workspace]](../../../../../data-science-workspace/home.md)
* [Visão geral do [!DNL Query Service]](../../../../../query-service/home.md)

O vídeo a seguir é destinado a ajudá-lo a entender a assimilação de dados usando o conector do Adobe Analytics Source:

>[!WARNING]
>
> A interface do usuário [!DNL Platform] mostrada no vídeo a seguir está desatualizada. Consulte a documentação acima para obter as capturas de tela e a funcionalidade mais recentes da interface.

>[!VIDEO](https://video.tv.adobe.com/v/29687?quality=12&learn=on)
