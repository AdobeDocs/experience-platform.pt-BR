---
title: Mapear um arquivo CSV para um esquema XDM usando recomendações geradas por IA
description: Este tutorial aborda como mapear um arquivo CSV para um esquema XDM usando recomendações geradas por IA.
exl-id: 1daedf0b-5a25-4ca5-ae5d-e9ee1eae9e4d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1179'
ht-degree: 1%

---

# Mapear um arquivo CSV para um esquema XDM usando recomendações geradas por IA

>[!NOTE]
>
>Para obter informações sobre recursos de mapeamento de arquivos CSV geralmente disponíveis no Experience Platform, consulte o documento sobre [mapeamento de um arquivo CSV para um esquema existente](./existing-schema.md).

Para assimilar dados CSV em [!DNL Adobe Experience Platform], os dados devem ser mapeados para um esquema [!DNL Experience Data Model] (XDM). Você pode optar por mapear para [um esquema existente](./existing-schema.md), mas se não souber exatamente qual esquema usar ou como ele deve ser estruturado, você poderá usar recomendações dinâmicas com base em modelos de aprendizado de máquina (ML) na interface do Experience Platform.

## Introdução

Este tutorial requer entendimento prático dos seguintes componentes do [!DNL Experience Platform]:

* [[!DNL Experience Data Model (XDM System)]](../../../xdm/home.md): a estrutura padronizada pela qual o [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * No mínimo, você deve entender o conceito de [comportamentos no XDM](../../../xdm/home.md#data-behaviors), para que possa decidir se deseja mapear seus dados para uma classe de [!UICONTROL Perfil] (comportamento de registro) ou de [!UICONTROL ExperienceEvent] (comportamento de série temporal).
* [Assimilação em lote](../../batch-ingestion/overview.md): o método pelo qual [!DNL Experience Platform] assimila dados de arquivos de dados fornecidos pelo usuário.
* [Preparo de dados do Adobe Experience Platform](../../batch-ingestion/overview.md): um conjunto de recursos que permitem mapear e transformar dados assimilados para estarem em conformidade com esquemas XDM. A documentação sobre [funções de Preparo de Dados](../../../data-prep/functions.md) é especificamente relevante para o mapeamento de esquema.

## Fornecer detalhes do fluxo de dados

Na interface do usuário do Experience Platform, selecione **[!UICONTROL Fontes]** na navegação à esquerda. Na exibição **[!UICONTROL Catálogo]**, navegue até a categoria **[!UICONTROL Sistema local]**. Em **[!UICONTROL Carregamento de arquivo local]**, selecione **[!UICONTROL Adicionar dados]**.

![O catálogo [!UICONTROL Fontes] na interface do usuário do Experience Platform, com [!UICONTROL Adicionar dados] em [!UICONTROL Carregamento de arquivo local] sendo selecionado.](../../images/tutorials/map-csv-recommendations/local-file-upload.png)

O fluxo de trabalho **[!UICONTROL Mapear esquema XDM do CSV]** é exibido, iniciando na etapa **[!UICONTROL Detalhes do fluxo de dados]**.

Selecione **[!UICONTROL Criar um novo esquema usando recomendações de ML]**, fazendo com que novos controles apareçam. Escolha a classe apropriada para os dados CSV que você deseja mapear ([!UICONTROL Perfil] ou [!UICONTROL ExperienceEvent]). Opcionalmente, é possível usar o menu suspenso para selecionar o setor relevante para sua empresa, ou deixá-lo em branco se as categorias fornecidas não se aplicarem a você. Se sua organização opera sob um modelo [B2B (B2B)](../../../xdm/tutorials/relationship-b2b.md), marque a caixa de seleção **[!UICONTROL Dados B2B]**.

![A etapa [!UICONTROL Detalhes do fluxo de dados] com a opção de recomendação ML selecionada. [!UICONTROL O perfil] está selecionado para a classe e [!UICONTROL Telecomunicações] está selecionado para o setor](../../images/tutorials/map-csv-recommendations/select-class-and-industry.png)

Aqui, forneça um nome para o esquema que será criado a partir dos dados CSV e um nome para o conjunto de dados de saída que conterá os dados assimilados sob esse esquema.

Opcionalmente, é possível configurar os seguintes recursos adicionais para o fluxo de dados antes de continuar:

| Nome de entrada | Descrição |
| --- | --- |
| [!UICONTROL Descrição] | Uma descrição para o fluxo de dados. |
| [!UICONTROL Diagnóstico de erro] | Quando habilitadas, mensagens de erro são geradas para lotes recém-assimilados, que podem ser visualizadas ao buscar o lote correspondente na [API](../../batch-ingestion/api-overview.md). |
| [!UICONTROL Assimilação parcial] | Quando ativados, os registros válidos para novos dados em lote serão assimilados dentro de um limite de erro especificado. Esse limite permite configurar a porcentagem de erros aceitáveis antes que todo o lote falhe. |
| [!UICONTROL Detalhes do fluxo de dados] | Forneça um nome e uma descrição opcional para o fluxo de dados que trará os dados CSV para a Experience Platform. O fluxo de dados recebe automaticamente um nome padrão ao iniciar esse fluxo de trabalho. A alteração do nome é opcional. |
| [!UICONTROL Alertas] | Selecione de uma lista de [alertas no produto](../../../observability/alerts/overview.md) que você deseja receber sobre o status do fluxo de dados depois de ele ter sido iniciado. |

{style="table-layout:auto"}

Quando terminar de configurar o fluxo de dados, selecione **[!UICONTROL Avançar]**.

![A seção [!UICONTROL Detalhes do fluxo de dados] foi concluída.](../../images/tutorials/map-csv-recommendations/dataflow-detail-complete.png)

## Selecionar dados

Na etapa **[!UICONTROL Selecionar dados]**, use a coluna da esquerda para carregar seu arquivo CSV. Você pode selecionar **[!UICONTROL Escolher arquivos]** para abrir uma caixa de diálogo do explorador de arquivos para selecionar o arquivo, ou pode arrastar e soltar o arquivo diretamente na coluna.

![O botão [!UICONTROL Escolher arquivos] e a área de arrastar e soltar destacados na etapa [!UICONTROL Selecionar dados].](../../images/tutorials/map-csv-recommendations/upload-files.png)

Após o upload do arquivo, é exibida uma seção de dados de amostra que mostra as dez primeiras linhas dos dados recebidos para que você possa verificar se o upload foi feito corretamente. Clique em **[!UICONTROL Avançar]** para continuar.

![Linhas de dados de exemplo são populadas dentro do espaço de trabalho](../../images/tutorials/map-csv-recommendations/data-uploaded.png)

## Configurar mapeamentos de esquema

Os modelos ML são executados para gerar um novo esquema com base na configuração do fluxo de dados e no arquivo CSV carregado. Quando o processo for concluído, a etapa [!UICONTROL Mapping] será preenchida para mostrar os mapeamentos para cada campo individual ao lado da exibição totalmente navegável da estrutura de esquema gerada.

![A etapa [!UICONTROL Mapeamento] na interface do usuário, mostrando todos os campos CSV mapeados e a estrutura de esquema resultante.](../../images/tutorials/map-csv-recommendations/schema-generated.png)

>[!NOTE]
>
>Você pode filtrar todos os campos no esquema com base em vários critérios durante o fluxo de trabalho de mapeamento de campos da origem para o destino. O comportamento padrão é exibir todos os campos mapeados. Para alterar os campos exibidos, selecione o ícone de filtro ao lado do campo de entrada de pesquisa e escolha entre as opções suspensas.<br> ![O estágio de mapeamento do fluxo de trabalho de criação do esquema CSV para XDM com o ícone de filtro e o menu suspenso realçados.](../../images/tutorials/map-csv-recommendations/source-field-to-target-mapping-filter.png "O estágio de mapeamento do fluxo de trabalho de criação do esquema CSV para XDM com o ícone de filtro e o menu suspenso realçados."){width="100" zoomable="yes"}

Aqui, você pode, opcionalmente, [editar os mapeamentos de campo](#edit-mappings) ou [alterar os grupos de campos aos quais estão associados](#edit-schema) de acordo com as suas necessidades. Quando satisfeito, selecione **[!UICONTROL Concluir]** para concluir o mapeamento e iniciar o fluxo de dados configurado anteriormente. Os dados do CSV são assimilados no sistema e preenchem um conjunto de dados com base na estrutura de esquema gerada, pronta para ser consumida pelos serviços downstream da Experience Platform.

![O botão [!UICONTROL Concluir] sendo selecionado, concluindo o processo de mapeamento de CSV.](../../images/tutorials/map-csv-recommendations/finish-mapping.png)

### Editar mapeamentos de campo {#edit-mappings}

Use a visualização de mapeamento de campo para editar os mapeamentos existentes ou removê-los totalmente. Para obter mais informações sobre como gerenciar um conjunto de mapeamento na interface, consulte o [manual da interface para mapeamento de Preparo de Dados](../../../data-prep/ui/mapping.md#mapping-interface).

### Editar grupos de campos {#edit-field-groups}

Os campos CSV são mapeados automaticamente para grupos de campos XDM existentes usando modelos ML. Se quiser alterar o grupo de campos para qualquer campo CSV específico, selecione **[!UICONTROL Editar]** ao lado da árvore de esquema.

![O botão [!UICONTROL Editar] que está sendo selecionado ao lado da árvore de esquemas.](../../images/tutorials/map-csv-recommendations/edit-schema-structure.png)

Uma caixa de diálogo é exibida, permitindo editar o nome de exibição, o tipo de dados e o grupo de campos de qualquer campo no mapeamento. Selecione o ícone de edição (![Ícone de edição](/help/images/icons/edit.png)) ao lado de um campo de origem para editar seus detalhes na coluna direita antes de selecionar **[!UICONTROL Aplicar]**.

![O grupo de campos recomendado para um campo de origem que está sendo alterado.](../../images/tutorials/map-csv-recommendations/select-schema-field.png)

Quando você terminar de ajustar as recomendações de esquema para seus campos de origem, selecione **[!UICONTROL Salvar]** para aplicar as alterações.

## Próximas etapas

Este guia abordou como mapear um arquivo CSV para um esquema XDM usando recomendações geradas por IA, permitindo que você traga esses dados para a Experience Platform por meio da assimilação em lote.

Para obter etapas sobre como mapear um arquivo CSV para um esquema existente, consulte o [fluxo de trabalho de mapeamento de esquema existente](./existing-schema.md). Para obter informações sobre dados de transmissão para o Experience Platform em tempo real por meio de conexões de origem pré-criadas, consulte a [visão geral das fontes](../../../sources/home.md).

Você também pode usar algoritmos de aprendizado de máquina (ML) para **gerar um esquema a partir de dados CSV de amostra**. Esse fluxo de trabalho cria automaticamente um novo esquema com base na estrutura e no conteúdo do arquivo CSV. Esse esquema recém-criado corresponde ao formato dos seus dados para economizar tempo e aumentar a precisão ao definir a estrutura, os campos e os tipos de dados para conjuntos de dados grandes e complexos. Consulte o [Guia de criação de esquema com assistência de ML](../../../xdm/ui/ml-assisted-schema-creation.md) para obter mais informações sobre este fluxo de trabalho.
