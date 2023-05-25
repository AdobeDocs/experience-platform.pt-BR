---
title: Criar uma conexão de origem do Adobe Analytics na interface
description: Saiba como criar uma conexão de origem do Adobe Analytics na interface do usuário para trazer dados do consumidor para o Adobe Experience Platform.
exl-id: 5ddbaf63-feaa-44f5-b2f2-2d5ae507f423
source-git-commit: b8764b4b39aba43687c7ac0540d392a3aa808df4
workflow-type: tm+mt
source-wordcount: '2299'
ht-degree: 6%

---

# Criar uma conexão de origem do Adobe Analytics na interface

Este tutorial fornece etapas para a criação de uma conexão de origem do Adobe Analytics na interface do usuário para trazer os dados do conjunto de relatórios do Adobe Analytics para a Adobe Experience Platform.

## Introdução

Este tutorial requer um entendimento prático dos seguintes componentes do Experience Platform:

* [Sistema do Experience Data Model (XDM)](../../../../../xdm/home.md): a estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
* [Perfil do cliente em tempo real](../../../../../profile/home.md): fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.
* [Sandboxes](../../../../../sandboxes/home.md): o Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

### Terminologia principal

É importante entender os seguintes termos principais usados neste documento:

* **Atributo padrão**: atributos padrão são qualquer atributo que seja predefinido pelo Adobe. Eles contêm o mesmo significado para todos os clientes e estão disponíveis na [!DNL Analytics] dados de origem e [!DNL Analytics] grupos de campos de esquema.
* **Atributo personalizado**: atributos personalizados são qualquer atributo na hierarquia de variáveis personalizadas no [!DNL Analytics]. Os atributos personalizados são usados em uma implementação do Adobe Analytics para capturar informações específicas em um conjunto de relatórios e podem diferir no uso de cada conjunto de relatórios. Os atributos personalizados incluem eVars, propriedades e listas. Consulte o seguinte [[!DNL Analytics] documentação sobre variáveis de conversão](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/conversion-variables/conversion-var-admin.html?lang=en) para obter mais informações sobre eVars.
* **Qualquer atributo em grupos de campos personalizados**: os atributos originados de grupos de campos criados por clientes são todos definidos pelo usuário e não são considerados atributos padrão nem personalizados.
* **Nomes amigáveis**: os nomes amigáveis são rótulos fornecidos por humanos para variáveis personalizadas em uma [!DNL Analytics] execução. Consulte o seguinte [[!DNL Analytics] documentação sobre variáveis de conversão](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/conversion-variables/conversion-var-admin.html?lang=en) para obter mais informações sobre nomes amigáveis.

## Criar uma conexão de origem com o Adobe Analytics

>[!NOTE]
>
>Ao criar um fluxo de dados de origem do Analytics em uma sandbox de produção, dois fluxos de dados são criados:
>
>* Um fluxo de dados que faz um preenchimento retroativo de 13 meses de dados históricos do conjunto de relatórios no data lake. Esse fluxo de dados termina quando o preenchimento retroativo é concluído.
>* Um fluxo de dados que envia dados em tempo real para o data lake e o [!DNL Real-Time Customer Profile]. Esse fluxo de dados é executado continuamente.


Na interface do usuário da Platform, selecione **[!UICONTROL Origens]** na navegação à esquerda, para acessar a [!UICONTROL Origens] espaço de trabalho. A variável [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Você também pode usar a barra de pesquisa para restringir as fontes exibidas.

No **[!UICONTROL aplicativos Adobe]** categoria, selecione **[!UICONTROL Adobe Analytics]** e selecione **[!UICONTROL Adicionar dados]**.

![catálogo](../../../../images/tutorials/create/analytics/catalog.png)

### Selecionar dados

>[!IMPORTANT]
>
>Os conjuntos de relatórios listados na tela podem vir de várias regiões. Você é responsável por entender as limitações e obrigações de seus dados e como usá-los entre regiões do Adobe Experience Platform. Verifique se isso é permitido pela sua empresa.

A variável **[!UICONTROL Adicionar dados da fonte do Analytics]** A etapa fornece uma lista de [!DNL Analytics] dados do conjunto de relatórios para criar uma conexão de origem com o.

Um conjunto de relatórios é um container de dados que forma a base do [!DNL Analytics] relatórios. Uma organização pode ter muitos conjuntos de relatórios, cada um contendo diferentes conjuntos de dados.

Você pode assimilar conjuntos de relatórios de qualquer região (Estados Unidos, Reino Unido ou Cingapura) desde que eles estejam mapeados para a mesma organização da instância de sandbox de Experience Platform em que a conexão de origem está sendo criada. Um conjunto de relatórios pode ser assimilado usando apenas um único fluxo de dados ativo. Um conjunto de relatórios que não pode ser selecionado já foi assimilado, na sandbox que você está usando ou em uma sandbox diferente.

Várias conexões de entrada podem ser feitas para trazer vários conjuntos de relatórios para a mesma sandbox. Se os conjuntos de relatórios tiverem esquemas diferentes para variáveis (como eVars ou eventos), eles deverão ser mapeados para campos específicos nos grupos de campos personalizados e evitar conflitos de dados usando [Preparação de dados](../../../../../data-prep/ui/mapping.md). Os conjuntos de relatórios podem ser adicionados somente a uma única sandbox.

![](../../../../images/tutorials/create/analytics/report-suite.png)

>[!NOTE]
>
>Os dados de vários conjuntos de relatórios podem ser ativados para o Perfil do cliente em tempo real somente se não houver conflitos de dados, como duas propriedades personalizadas (eVars, listas e props) com significado diferente.

Para criar uma [!DNL Analytics] conexão de origem, selecione um conjunto de relatórios e selecione **[!UICONTROL Próxima]** para continuar.

![](../../../../images/tutorials/create/analytics/add-data.png)

&lt;!—Os Conjuntos de relatórios do Analytics podem ser configurados para uma sandbox por vez. Para importar o mesmo Conjunto de relatórios para uma sandbox diferente, o fluxo do conjunto de dados terá de ser excluído e instanciado novamente por meio da configuração de uma sandbox diferente.—>

### Mapeamento

>[!IMPORTANT]
>
>As transformações de Preparo de dados podem adicionar latência ao fluxo de dados geral. A latência adicional adicionada varia de acordo com a complexidade da lógica de transformação.

Antes de poder mapear seus [!DNL Analytics] para direcionar esquema XDM, você deve primeiro selecionar se está usando um esquema padrão ou personalizado.

Um esquema padrão cria um novo esquema em seu nome, contendo o [!DNL Adobe Analytics ExperienceEvent Template] grupo de campos. Para usar um esquema padrão, selecione **[!UICONTROL Esquema padrão]**.

![default-schema](../../../../images/tutorials/create/analytics/default-schema.png)

Com um esquema personalizado, você pode escolher qualquer esquema disponível para seu [!DNL Analytics] dados, desde que esse esquema tenha a [!DNL Adobe Analytics ExperienceEvent Template] grupo de campos. Para usar um esquema personalizado, selecione **[!UICONTROL Esquema personalizado]**.

![custom-schema](../../../../images/tutorials/create/analytics/custom-schema.png)

A variável [!UICONTROL Mapeamento] fornece uma interface para mapear campos de origem para seus campos de esquema de destino apropriados. Aqui, é possível mapear variáveis personalizadas para novos grupos de campos de esquema e aplicar cálculos de acordo com o Preparo de dados. Selecione um schema de destino para iniciar o processo de mapeamento.

>[!TIP]
>
>Somente esquemas que tenham o [!DNL Adobe Analytics ExperienceEvent Template] grupo de campos são exibidos no menu de seleção de esquema. Outros esquemas são omitidos. Se não houver esquemas apropriados disponíveis para seus dados do Conjunto de relatórios, você deve criar um novo esquema. Para obter etapas detalhadas sobre como criar schemas, consulte o guia em [criação e edição de esquemas na interface](../../../../../xdm/ui/resources/schemas.md).

![select-schema](../../../../images/tutorials/create/analytics/select-schema.png)

A variável [!UICONTROL Mapear campos padrão] A seção exibe painéis para [!UICONTROL Mapeamentos padrão aplicados], [!UICONTROL Mapeamentos padrão não correspondentes] e [!UICONTROL Mapeamentos personalizados]. Consulte a tabela a seguir para obter informações específicas sobre cada categoria:

| Mapear campos padrão | Descrição |
| --- | --- |
| [!UICONTROL Mapeamentos padrão aplicados] | A variável [!UICONTROL Mapeamentos padrão aplicados] exibe o número total de atributos mapeados. Mapeamentos padrão referem-se a conjuntos de mapeamento entre todos os atributos na origem [!DNL Analytics] dados e atributos correspondentes no [!DNL Analytics] grupo de campos. Eles são pré-mapeados e não podem ser editados. |
| [!UICONTROL Mapeamentos padrão não correspondentes] | A variável [!UICONTROL Mapeamentos padrão não correspondentes] painel refere-se ao número de atributos mapeados que contêm conflitos de nome amigável. Esses conflitos aparecem quando você está reutilizando um esquema que já tem um conjunto preenchido de descritores de campo de um conjunto de relatórios diferente. Você pode continuar com seu [!DNL Analytics] fluxo de dados mesmo com conflitos de nome amigáveis. |
| [!UICONTROL Mapeamentos personalizados] | A variável [!UICONTROL Mapeamentos personalizados] O painel exibe o número de atributos personalizados mapeados, incluindo eVars, propriedades e listas. Mapeamentos personalizados se referem aos conjuntos de mapeamento entre atributos personalizados na origem [!DNL Analytics] dados e atributos em grupos de campos personalizados incluídos no esquema selecionado. |

![map-standard-fields](../../../../images/tutorials/create/analytics/map-standard-fields.png)

Para visualizar o [!DNL Analytics] Grupo de campos de esquema de modelo ExperienceEvent, selecione **[!UICONTROL Exibir]** no [!UICONTROL Mapeamentos padrão aplicados] painel.

![view](../../../../images/tutorials/create/analytics/view.png)

A variável [!UICONTROL Grupo de campos de esquema de modelo do Adobe Analytics ExperienceEvent] Esta página fornece uma interface a ser usada para inspecionar a estrutura do esquema. Quando terminar, selecione **[!UICONTROL Fechar]**.

![field-group-preview](../../../../images/tutorials/create/analytics/field-group-preview.png)

O Platform detecta automaticamente seus conjuntos de mapeamento para qualquer conflito de nome amigável. Se não houver conflitos com seus conjuntos de mapeamento, selecione **[!UICONTROL Próxima]** para continuar.

![mapeamento](../../../../images/tutorials/create/analytics/mapping.png)

>[!TIP]
>
>Se houver conflitos de nome amigável entre seu Conjunto de relatórios de origem e seu esquema selecionado, você ainda poderá continuar com seu [!DNL Analytics] fluxo de dados, reconhecendo que os descritores de campo não serão alterados. Como alternativa, você pode optar por criar um novo esquema com um conjunto de descritores em branco.

#### Mapeamentos personalizados

É possível usar as funções de Preparo de dados para adicionar novos mapeamentos personalizados ou campos calculados para atributos personalizados. Para adicionar mapeamentos personalizados, selecione **[!UICONTROL Personalizado]**.

![personalizado](../../../../images/tutorials/create/analytics/custom.png)

Dependendo das suas necessidades, você pode selecionar **[!UICONTROL Adicionar novo mapeamento]** ou **[!UICONTROL Adicionar campo calculado]** e prossiga para criar mapeamentos personalizados para seus atributos personalizados. Para obter etapas abrangentes sobre como usar as funções de Preparo de dados, leia a [Guia da interface de preparação de dados](../../../../../data-prep/ui/mapping.md).

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

### Filtragem para o Perfil do cliente em tempo real {#filtering-for-profile}

>[!CONTEXTUALHELP]
>id="platform_data_prep_analytics_filtering"
>title="Criar regras de filtro"
>abstract="Defina as regras de filtragem em nível de linha e coluna ao enviar dados para o perfil do cliente em tempo real. Use a filtragem de nível de linha para aplicar condições e determinar quais dados **incluir para ingestão de perfil**. Use a filtragem de nível de coluna para selecionar as colunas de dados que deseja **excluir para ingestão de perfil**. As regras de filtragem não se aplicam aos dados enviados para o data lake."

Depois de concluir os mapeamentos para o [!DNL Analytics] dados do conjunto de relatórios, você pode aplicar regras e condições de filtragem para incluir ou excluir seletivamente dados da assimilação para o Perfil do cliente em tempo real. O suporte para filtragem só está disponível para [!DNL Analytics] Os dados do e do são filtrados somente antes da entrada [!DNL Profile.] Todos os dados são assimilados no data lake.

#### Filtragem em nível de linha

>[!IMPORTANT]
>
>Use a filtragem de nível de linha para aplicar condições e determinar quais dados **incluir para ingestão de perfil**. Use a filtragem de nível de coluna para selecionar as colunas de dados que deseja **excluir para ingestão de perfil**.

É possível filtrar dados para [!DNL Profile] assimilação no nível da linha e no nível da coluna. A filtragem em nível de linha permite definir critérios como cadeia de caracteres contém, é igual a, começa ou termina com. Também é possível usar a filtragem em nível de linha para unir condições usando `AND` bem como `OR`e negar condições usando `NOT`.

Para filtrar o [!DNL Analytics] dados no nível da linha, selecione **[!UICONTROL Filtro de linha]**.

![row-filter](../../../../images/tutorials/create/analytics/row-filter.png)

Use o painel à esquerda para navegar pela hierarquia do esquema e selecione o atributo de esquema de sua escolha para detalhar ainda mais um esquema específico.

![painel esquerdo](../../../../images/tutorials/create/analytics/left-rail.png)

Depois de identificar o atributo que deseja configurar, selecione e arraste o atributo do painel esquerdo para o painel Filtragem.

![painel de filtragem](../../../../images/tutorials/create/analytics/filtering-panel.png)

Para configurar condições diferentes, selecione **[!UICONTROL igual a]** e selecione uma condição na janela suspensa que é exibida.

A lista de condições configuráveis inclui:

* [!UICONTROL igual a]
* [!UICONTROL não é igual]
* [!UICONTROL começa com]
* [!UICONTROL termina com]
* [!UICONTROL não termina com]
* [!UICONTROL contém]
* [!UICONTROL não contém]
* [!UICONTROL existe]
* [!UICONTROL não existe]

![condições](../../../../images/tutorials/create/analytics/conditions.png)

Em seguida, insira os valores que deseja incluir com base no atributo selecionado. No exemplo abaixo, [!DNL Apple] e [!DNL Google] são selecionados para assimilação como parte da **[!UICONTROL Fabricante]** atributo.

![fabricante do include](../../../../images/tutorials/create/analytics/include-manufacturer.png)

Para especificar ainda mais suas condições de filtragem, adicione outro atributo do esquema e adicione valores com base nesse atributo. No exemplo abaixo, a variável **[!UICONTROL Modelo]** atributo é adicionado e modelos como o [!DNL iPhone 13] e [!DNL Google Pixel 6] são filtrados para assimilação.

![include-model](../../../../images/tutorials/create/analytics/include-model.png)

Para adicionar um novo container, selecione as reticências (`...`) na parte superior direita da interface do filtro e selecione **[!UICONTROL Adicionar contêiner]**.

![add-container](../../../../images/tutorials/create/analytics/add-container.png)

Depois que um novo container é adicionado, selecione **[!UICONTROL Incluir]** e selecione **[!UICONTROL Excluir]** na janela suspensa exibida.

![excluir](../../../../images/tutorials/create/analytics/exclude.png)

Em seguida, conclua o mesmo processo arrastando os atributos do esquema e adicionando os valores correspondentes que deseja excluir da filtragem. No exemplo abaixo, a variável [!DNL iPhone 12], [!DNL iPhone 12 mini], e [!DNL Google Pixel 5] são todos filtrados da exclusão do **[!UICONTROL Modelo]** atributo, paisagem é excluída da variável **[!UICONTROL Orientação da tela]**, e número do modelo [!DNL A1633] está excluído de **[!UICONTROL Número do modelo]**.

Quando terminar, selecione **[!UICONTROL Próxima]**.

![exclude-examples](../../../../images/tutorials/create/analytics/exclude-examples.png)

#### Filtragem em nível de coluna

Selecionar **[!UICONTROL Filtro de coluna]** no cabeçalho para aplicar a filtragem em nível de coluna.

![column-filter](../../../../images/tutorials/create/analytics/column-filter.png)

A página é atualizada em uma árvore de esquema interativa, exibindo os atributos do esquema no nível da coluna. Aqui, é possível selecionar as colunas de dados que deseja excluir [!DNL Profile] assimilação. Como alternativa, é possível expandir uma coluna e selecionar atributos específicos para exclusão.

Por padrão, todas as [!DNL Analytics] ir para [!DNL Profile] e esse processo permite que ramificações de dados XDM sejam excluídas do [!DNL Profile] assimilação.

Quando terminar, selecione **[!UICONTROL Próxima]**.

![colunas selecionadas](../../../../images/tutorials/create/analytics/columns-selected.png)

### Fornecer detalhes do fluxo de dados

A variável **[!UICONTROL Detalhes do fluxo de dados]** é exibida, onde você deve fornecer um nome e uma descrição opcional para o fluxo de dados. Selecionar **[!UICONTROL Próxima]** quando terminar.

![detalhes do fluxo de dados](../../../../images/tutorials/create/analytics/dataflow-detail.png)

### Consulte a seção

A variável [!UICONTROL Revisão] é exibida, permitindo que você revise seu novo fluxo de dados do Analytics antes de ele ser criado. Os detalhes da conexão são agrupados por categorias, incluindo:

* [!UICONTROL Conexão]: exibe a plataforma de origem da conexão.
* [!UICONTROL Tipo de dados]: exibe o Conjunto de relatórios selecionado e sua ID de conjunto de relatórios correspondente.

![revisão](../../../../images/tutorials/create/analytics/review.png)

### Monitorar seu fluxo de dados

Depois que o fluxo de dados for criado, você poderá monitorar os dados que estão sendo assimilados por meio dele. No [!UICONTROL Catálogo] , selecione **[!UICONTROL Fluxos de dados]** para exibir uma lista de fluxos estabelecidos associados à sua conta do Analytics.

![select-datafflows](../../../../images/tutorials/create/analytics/select-dataflows.png)

A variável **Fluxos de dados** é exibida. Nesta página há um par de fluxos de conjunto de dados, incluindo informações sobre seu nome, dados de origem, hora de criação e status.

O conector instancia dois fluxos de conjunto de dados. Um fluxo representa dados de preenchimento retroativo e o outro é para dados em tempo real. Os dados de preenchimento retroativo não são configurados para o Perfil, mas são enviados ao data lake para casos de uso analíticos e de ciência de dados.

Para obter mais informações sobre preenchimento retroativo, dados em tempo real e suas respectivas latências, consulte a [Visão geral do Conector de dados do Analytics](../../../../connectors/adobe-applications/analytics.md).

Selecione o fluxo do conjunto de dados que deseja exibir na lista.

![select-target-dataset](../../../../images/tutorials/create/analytics/select-target-dataset.png)

A variável **[!UICONTROL Atividade do conjunto de dados]** é exibida. Esta página exibe a taxa de mensagens que estão sendo consumidas no formato de um gráfico. Selecionar **[!UICONTROL Governança de dados]** no cabeçalho superior para acessar os campos de rotulagem.

![atividade do conjunto de dados](../../../../images/tutorials/create/analytics/dataset-activity.png)

Você pode visualizar os rótulos herdados de um fluxo do conjunto de dados a partir da [!UICONTROL Governança de dados] tela. Para obter mais informações sobre como rotular dados provenientes do Analytics, visite o [guia de rótulos de uso de dados](../../../../../data-governance/labels/user-guide.md).

![data-gov](../../../../images/tutorials/create/analytics/data-gov.png)

Para excluir um fluxo de dados, vá para a guia [!UICONTROL Fluxos de dados] e selecione as reticências (`...`) ao lado do nome do fluxo de dados e selecione [!UICONTROL Excluir].

![delete](../../../../images/tutorials/create/analytics/delete.png)

## Próximas etapas e recursos adicionais

Depois que a conexão é criada, o fluxo de dados é criado automaticamente para conter os dados recebidos e preencher um conjunto de dados com o esquema selecionado. Além disso, ocorre o preenchimento retroativo de dados e a assimilação de até 13 meses de dados históricos. Quando a assimilação inicial for concluída, [!DNL Analytics] dados e ser usado por serviços downstream da Platform, como [!DNL Real-Time Customer Profile] e Serviço de segmentação. Consulte os seguintes documentos para obter mais detalhes:

* [Visão geral do [!DNL Real-Time Customer Profile]](../../../../../profile/home.md)
* [Visão geral do [!DNL Segmentation Service]](../../../../../segmentation/home.md)
* [Visão geral do [!DNL Data Science Workspace]](../../../../../data-science-workspace/home.md)
* [Visão geral do [!DNL Query Service]](../../../../../query-service/home.md)

O vídeo a seguir é destinado a ajudá-lo a entender a assimilação de dados usando o Conector de origem do Adobe Analytics:

>[!WARNING]
>
> A variável [!DNL Platform] A interface mostrada no vídeo a seguir está desatualizada. Consulte a documentação acima para obter as capturas de tela e a funcionalidade mais recentes da interface.

>[!VIDEO](https://video.tv.adobe.com/v/29687?quality=12&learn=on)
