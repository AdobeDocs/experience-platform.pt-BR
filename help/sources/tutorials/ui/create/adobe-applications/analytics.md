---
title: Criar uma conexão de origem do Adobe Analytics na interface do usuário
description: Saiba como criar uma conexão de origem do Adobe Analytics na interface do usuário para trazer dados do consumidor para o Adobe Experience Platform.
exl-id: 5ddbaf63-feaa-44f5-b2f2-2d5ae507f423
source-git-commit: 3b86c071c4b5dc151bf83ad0042c10ac7a5648db
workflow-type: tm+mt
source-wordcount: '2352'
ht-degree: 5%

---

# Criar uma conexão de origem do Adobe Analytics na interface do usuário

Este tutorial fornece etapas para criar uma conexão de origem Adobe Analytics na interface do usuário para trazer os dados do conjunto de relatórios do Adobe Analytics para o Adobe Experience Platform.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Experience Platform:

* [Sistema do Experience Data Model (XDM)](../../../../../xdm/home.md): A estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
* [Perfil do cliente em tempo real](../../../../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.
* [Sandboxes](../../../../../sandboxes/home.md): O Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

### Terminologia principal

É importante entender os seguintes termos principais usados em todo este documento:

* **Atributo padrão**: Atributos padrão são qualquer atributo predefinido pelo Adobe. Eles contêm o mesmo significado para todos os clientes e estão disponíveis no [!DNL Analytics] dados de origem e [!DNL Analytics] grupos de campos de esquema.
* **Atributo personalizado**: Atributos personalizados são qualquer atributo na hierarquia de variável personalizada em [!DNL Analytics]. Os atributos personalizados são usados em uma implementação do Adobe Analytics para capturar informações específicas em um conjunto de relatórios e podem diferir em seu uso, de conjunto de relatórios a conjunto de relatórios. Os atributos personalizados incluem eVars, props e listas. Veja o seguinte [[!DNL Analytics] documentação sobre variáveis de conversão](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/conversion-variables/conversion-var-admin.html?lang=en) para obter mais informações sobre eVars.
* **Qualquer atributo em grupos de campos personalizados**: Os atributos originados de grupos de campos criados por clientes são definidos pelo usuário e não são considerados atributos padrão ou personalizados.
* **Nomes amigáveis**: Nomes amigáveis são rótulos fornecidos por humanos para variáveis personalizadas em um [!DNL Analytics] implementação. Veja o seguinte [[!DNL Analytics] documentação sobre variáveis de conversão](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/conversion-variables/conversion-var-admin.html?lang=en) para obter mais informações sobre nomes amigáveis.

## Criar uma conexão de origem com o Adobe Analytics

Na interface do usuário da plataforma, selecione **[!UICONTROL Fontes]** na navegação à esquerda para acessar o [!UICONTROL Fontes] espaço de trabalho. O [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Também é possível usar a barra de pesquisa para restringir as fontes exibidas.

Em **[!UICONTROL Aplicativos Adobe]** categoria , selecione **[!UICONTROL Adobe Analytics]** e depois selecione **[!UICONTROL Adicionar dados]**.

![catálogo](../../../../images/tutorials/create/analytics/catalog.png)

### Selecionar dados

>[!IMPORTANT]
>
>Os conjuntos de relatórios listados na tela podem vir de várias regiões. Você é responsável por entender as limitações e obrigações dos dados e como usá-los nas regiões cruzadas do Adobe Experience Platform. Certifique-se de que isso seja permitido pela sua empresa.

O **[!UICONTROL Adicionar dados de origem do Analytics]** fornece uma lista de [!DNL Analytics] dados do conjunto de relatórios para criar uma conexão de origem com o .

Um conjunto de relatórios é um contêiner de dados que forma a base de [!DNL Analytics] relatórios. Uma organização pode ter vários conjuntos de relatórios, cada um contendo diferentes conjuntos de dados.

É possível assimilar conjuntos de relatórios de qualquer região (Estados Unidos, Reino Unido ou Cingapura), desde que eles sejam mapeados para a mesma organização da instância Experience Platform sandbox em que a conexão de origem está sendo criada. Um conjunto de relatórios pode ser assimilado usando apenas um único fluxo de dados ativo. Um conjunto de relatórios que não pode ser selecionado já foi assimilado na sandbox que você está usando ou em uma sandbox diferente.

Várias conexões vinculadas podem ser feitas para trazer vários conjuntos de relatórios para a mesma sandbox. Se os conjuntos de relatórios tiverem esquemas diferentes para variáveis (como eVars ou eventos), eles deverão ser mapeados para campos específicos nos grupos de campos personalizados e evitar conflitos de dados usando [Preparação de dados](../../../../../data-prep/ui/mapping.md). Os conjuntos de relatórios só podem ser adicionados a uma única sandbox.

![](../../../../images/tutorials/create/analytics/report-suite.png)

>[!NOTE]
>
>Os dados de vários conjuntos de relatórios podem ser ativados para o Perfil do cliente em tempo real somente se não houver conflitos de dados, como duas propriedades personalizadas (eVars, listas e props) que tenham um significado diferente.

Para criar um [!DNL Analytics] conexão de origem, selecione um conjunto de relatórios e depois selecione **[!UICONTROL Próximo]** para continuar.

![](../../../../images/tutorials/create/analytics/add-data.png)

&lt;!—Os Conjuntos de relatórios do Analytics podem ser configurados para uma sandbox de cada vez. Para importar o mesmo Conjunto de relatórios para uma sandbox diferente, o fluxo do conjunto de dados precisará ser excluído e instanciado novamente por meio da configuração de uma sandbox diferente.—>

### Mapeamento

>[!IMPORTANT]
>
>As transformações da Preparação de dados podem adicionar latência ao fluxo de dados geral. A latência adicional adicionada varia com base na complexidade da lógica de transformação.

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

### Filtragem para o perfil do cliente em tempo real {#filtering-for-profile}

>[!CONTEXTUALHELP]
>id="platform_data_prep_analytics_filtering"
>title="Criar regras de filtro"
>abstract="Defina as regras de filtragem em nível de linha e coluna ao enviar dados para o perfil do cliente em tempo real. Use a filtragem de nível de linha para aplicar condições e determinar quais dados **incluir para ingestão de perfil**. Use a filtragem de nível de coluna para selecionar as colunas de dados que deseja **excluir para ingestão de perfil**. As regras de filtragem não se aplicam aos dados enviados para o data lake."

Depois de concluir os mapeamentos para [!DNL Analytics] dados do conjunto de relatórios, você pode aplicar regras e condições de filtragem para incluir ou excluir seletivamente os dados da assimilação para o Perfil do cliente em tempo real. O suporte para filtragem só está disponível para [!DNL Analytics] os dados e dados são filtrados somente antes de inserir [!DNL Profile.] Todos os dados são assimilados no lago de dados.

#### Filtragem em nível de linha

>[!IMPORTANT]
>
>Use a filtragem de nível de linha para aplicar condições e determinar quais dados **incluir para ingestão de perfil**. Use a filtragem de nível de coluna para selecionar as colunas de dados que deseja **excluir para ingestão de perfil**.

Você pode filtrar dados para [!DNL Profile] assimilação no nível da linha e da coluna. A filtragem em nível de linha permite definir critérios, como a string contém, é igual a, começa ou termina com. Você também pode usar a filtragem em nível de linha para unir condições usando `AND` bem como `OR`e negar as condições usando `NOT`.

Para filtrar [!DNL Analytics] no nível da linha, selecione **[!UICONTROL Filtro de linha]**.

![filtro de linha](../../../../images/tutorials/create/analytics/row-filter.png)

Use o painel esquerdo para navegar pela hierarquia do schema e selecionar o atributo do schema de sua escolha para detalhar ainda mais um schema específico.

![painel esquerdo](../../../../images/tutorials/create/analytics/left-rail.png)

Depois de identificar o atributo que deseja configurar, selecione e arraste o atributo do painel esquerdo para o painel de filtragem.

![painel de filtragem](../../../../images/tutorials/create/analytics/filtering-panel.png)

Para configurar condições diferentes, selecione **[!UICONTROL igual]** e selecione uma condição na janela suspensa que é exibida.

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

Em seguida, insira os valores que deseja incluir com base no atributo selecionado. No exemplo abaixo, [!DNL Apple] e [!DNL Google] são selecionadas para ingestão como parte do **[!UICONTROL Fabricante]** atributo.

![fabricante de inclusão](../../../../images/tutorials/create/analytics/include-manufacturer.png)

Para especificar ainda mais as condições de filtragem, adicione outro atributo do schema e, em seguida, adicione valores com base nesse atributo. No exemplo abaixo, a variável **[!UICONTROL Modelo]** é adicionado e modelos como [!DNL iPhone 13] e [!DNL Google Pixel 6] são filtrados para assimilação.

![modelo de inclusão](../../../../images/tutorials/create/analytics/include-model.png)

Para adicionar um novo contêiner, selecione as reticências (`...`) na parte superior direita da interface do filtro e selecione **[!UICONTROL Adicionar contêiner]**.

![add-container](../../../../images/tutorials/create/analytics/add-container.png)

Após adicionar um novo contêiner, selecione **[!UICONTROL Incluir]** e depois selecione **[!UICONTROL Excluir]** na janela suspensa que é exibida.

![exclude](../../../../images/tutorials/create/analytics/exclude.png)

Em seguida, conclua o mesmo processo arrastando os atributos do esquema e adicionando os valores correspondentes que deseja excluir da filtragem. No exemplo abaixo, a variável [!DNL iPhone 12], [!DNL iPhone 12 mini]e [!DNL Google Pixel 5] são todos filtrados da exclusão do **[!UICONTROL Modelo]** , paisagem é excluída do **[!UICONTROL Orientação da tela]** e número do modelo [!DNL A1633] é excluído de **[!UICONTROL Número do modelo]**.

Quando terminar, selecione **[!UICONTROL Próximo]**.

![exclude-example](../../../../images/tutorials/create/analytics/exclude-examples.png)

#### Filtragem em nível de coluna

Selecionar **[!UICONTROL Filtro de colunas]** no cabeçalho para aplicar a filtragem em nível de coluna.

![filtro de coluna](../../../../images/tutorials/create/analytics/column-filter.png)

A página é atualizada em uma árvore de esquema interativa, exibindo seus atributos de esquema no nível da coluna. Aqui, você pode selecionar as colunas de dados que deseja excluir [!DNL Profile] ingestão. Como alternativa, é possível expandir uma coluna e selecionar atributos específicos para exclusão.

Por padrão, todas [!DNL Analytics] ir para [!DNL Profile] e esse processo permite que ramificações de dados XDM sejam excluídas do [!DNL Profile] ingestão.

Quando terminar, selecione **[!UICONTROL Próximo]**.

![columns-seleted](../../../../images/tutorials/create/analytics/columns-selected.png)

### Fornecer detalhes do fluxo de dados

O **[!UICONTROL Detalhes do fluxo de dados]** é exibida, onde você deve fornecer um nome e uma descrição opcional para o fluxo de dados. Selecionar **[!UICONTROL Próximo]** quando terminar.

![detalhe do fluxo de dados](../../../../images/tutorials/create/analytics/dataflow-detail.png)

### Consulte a seção

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

![delete](../../../../images/tutorials/create/analytics/delete.png)

## Próximas etapas e recursos adicionais

Depois que a conexão é criada, o fluxo de dados é criado automaticamente para conter os dados recebidos e preencher um conjunto de dados com o esquema selecionado. Além disso, ocorre o preenchimento retroativo de dados e a assimilação de até 13 meses de dados históricos. Quando a ingestão inicial for concluída, [!DNL Analytics] dados e ser usado por serviços de plataforma downstream, como [!DNL Real-Time Customer Profile] e Serviço de segmentação. Consulte os seguintes documentos para obter mais detalhes:

* [Visão geral do [!DNL Real-Time Customer Profile]](../../../../../profile/home.md)
* [Visão geral do [!DNL Segmentation Service]](../../../../../segmentation/home.md)
* [Visão geral do [!DNL Data Science Workspace]](../../../../../data-science-workspace/home.md)
* [Visão geral do [!DNL Query Service]](../../../../../query-service/home.md)

O vídeo a seguir é destinado a respaldar a compreensão da assimilação de dados pelo uso do conector do Adobe Analytics Source:

>[!WARNING]
>
> O [!DNL Platform] A interface do usuário exibida no vídeo a seguir está desatualizada. Consulte a documentação acima para obter as capturas de tela e a funcionalidade mais recentes da interface do usuário.

>[!VIDEO](https://video.tv.adobe.com/v/29687?quality=12&learn=on)
