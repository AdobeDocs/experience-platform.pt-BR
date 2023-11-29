---
title: Mapear um arquivo CSV para um esquema XDM usando o Recommendations gerado por IA
description: Este tutorial aborda como mapear um arquivo CSV para um esquema XDM usando recomendações geradas por IA.
exl-id: 1daedf0b-5a25-4ca5-ae5d-e9ee1eae9e4d
source-git-commit: 6632086641004c2b788a28cbc47ac6d8bd4eace3
workflow-type: tm+mt
source-wordcount: '1102'
ht-degree: 2%

---

# Mapear um arquivo CSV para um esquema XDM usando recomendações geradas por IA

>[!NOTE]
>
>Para obter informações sobre recursos de mapeamento de CSV geralmente disponíveis na Platform, consulte o documento em [mapeamento de um arquivo CSV para um esquema existente](./existing-schema.md).

Para assimilar dados CSV em [!DNL Adobe Experience Platform], os dados devem ser mapeados para um [!DNL Experience Data Model] Esquema de (XDM). Você pode optar por mapear para [um schema existente](./existing-schema.md), mas se você não souber exatamente qual esquema usar ou como ele deve ser estruturado, será possível usar recomendações dinâmicas com base em modelos de aprendizado de máquina (ML) na interface do usuário da Platform.

## Introdução

Este tutorial requer um entendimento prático dos seguintes componentes do [!DNL Platform]:

* [[!DNL Experience Data Model (XDM System)]](../../../xdm/home.md): a estrutura padronizada pela qual a [!DNL Platform] organiza os dados de experiência do cliente.
   * No mínimo, você deve entender o conceito de [comportamentos no XDM](../../../xdm/home.md#data-behaviors), para que você possa decidir se deseja mapear seus dados para um [!UICONTROL Perfil] classe (comportamento de registro) ou [!UICONTROL ExperienceEvent] classe (comportamento de série temporal).
* [Assimilação em lote](../../batch-ingestion/overview.md): o método pelo qual [!DNL Platform] assimila dados de arquivos de dados fornecidos pelo usuário.
* [Preparação de dados do Adobe Experience Platform](../../batch-ingestion/overview.md): um conjunto de recursos que permitem mapear e transformar dados assimilados para estarem em conformidade com esquemas XDM. A documentação sobre [Funções de Preparo de dados](../../../data-prep/functions.md) é especificamente relevante para o mapeamento de esquema.

## Fornecer detalhes do fluxo de dados

Na interface do Experience Platform, selecione **[!UICONTROL Origens]** no painel de navegação esquerdo. No **[!UICONTROL Catálogo]** exibir, navegue até o **[!UICONTROL Sistema local]** categoria. Em **[!UICONTROL Upload de arquivo local]**, selecione **[!UICONTROL Adicionar dados]**.

![A variável [!UICONTROL Origens] catálogo na interface do Platform, com [!UICONTROL Adicionar dados] em [!UICONTROL Upload de arquivo local] selecionada.](../../images/tutorials/map-csv-recommendations/local-file-upload.png)

A variável **[!UICONTROL Mapear esquema XDM do CSV]** fluxo de trabalho é exibido, começando no **[!UICONTROL Detalhes do fluxo de dados]** etapa.

Selecionar **[!UICONTROL Criar um novo esquema usando recomendações de ML]**, fazendo com que novos controles sejam exibidos. Escolha a classe apropriada para os dados CSV que deseja mapear ([!UICONTROL Perfil] ou [!UICONTROL ExperienceEvent]). Opcionalmente, é possível usar o menu suspenso para selecionar o setor relevante para sua empresa, ou deixá-lo em branco se as categorias fornecidas não se aplicarem a você. Se sua organização operar sob um [B2B (B2B)](../../../xdm/tutorials/relationship-b2b.md) , selecione o **[!UICONTROL Dados B2B]** caixa de seleção

![A variável [!UICONTROL Detalhes do fluxo de dados] etapa com a opção de recomendação ML selecionada. [!UICONTROL Perfil] está selecionado para a classe e [!UICONTROL Telecomunicações] selecionado para o setor](../../images/tutorials/map-csv-recommendations/select-class-and-industry.png)

Aqui, forneça um nome para o esquema que será criado a partir dos dados CSV e um nome para o conjunto de dados de saída que conterá os dados assimilados sob esse esquema.

Opcionalmente, é possível configurar os seguintes recursos adicionais para o fluxo de dados antes de continuar:

| Nome de entrada | Descrição |
| --- | --- |
| [!UICONTROL Descrição] | Uma descrição para o fluxo de dados. |
| [!UICONTROL Diagnóstico de erro] | Quando ativadas, as mensagens de erro são geradas para lotes recém-assimilados, que podem ser visualizadas ao buscar o lote correspondente no [API](../../batch-ingestion/api-overview.md). |
| [!UICONTROL Assimilação parcial] | Quando ativados, os registros válidos para novos dados em lote serão assimilados dentro de um limite de erro especificado. Esse limite permite configurar a porcentagem de erros aceitáveis antes que todo o lote falhe. |
| [!UICONTROL Detalhes do fluxo de dados] | Forneça um nome e uma descrição opcional para o fluxo de dados que trará os dados CSV para a plataforma. O fluxo de dados recebe automaticamente um nome padrão ao iniciar esse fluxo de trabalho. A alteração do nome é opcional. |
| [!UICONTROL Alertas] | Selecione de uma lista de [alertas no produto](../../../observability/alerts/overview.md) que você deseja receber em relação ao status do fluxo de dados depois de iniciado. |

{style="table-layout:auto"}

Quando terminar de configurar o fluxo de dados, selecione **[!UICONTROL Próxima]**.

![A variável [!UICONTROL Detalhes do fluxo de dados] seção foi concluída.](../../images/tutorials/map-csv-recommendations/dataflow-detail-complete.png)

## Selecionar dados

No **[!UICONTROL Selecionar dados]** use a coluna da esquerda para fazer upload do arquivo CSV. É possível selecionar **[!UICONTROL Escolher arquivos]** para abrir uma caixa de diálogo do explorador de arquivos para selecionar o arquivo, ou você pode arrastar e soltar o arquivo diretamente na coluna.

![A variável [!UICONTROL Escolher arquivos] botão e a área de arrastar e soltar realçada dentro do [!UICONTROL Selecionar dados] etapa.](../../images/tutorials/map-csv-recommendations/upload-files.png)

Após o upload do arquivo, é exibida uma seção de dados de amostra que mostra as dez primeiras linhas dos dados recebidos para que você possa verificar se o upload foi feito corretamente. Clique em **[!UICONTROL Avançar]** para continuar.

![Linhas de dados de exemplo são preenchidas no espaço de trabalho](../../images/tutorials/map-csv-recommendations/data-uploaded.png)

## Configurar mapeamentos de esquema

Os modelos ML são executados para gerar um novo esquema com base na configuração do fluxo de dados e no arquivo CSV carregado. Quando o processo estiver concluído, a variável [!UICONTROL Mapeamento] A etapa é preenchida para mostrar os mapeamentos de cada campo individual ao lado da exibição totalmente navegável da estrutura do esquema gerada.

![A variável [!UICONTROL Mapeamento] etapa na interface do usuário, mostrando todos os campos CSV mapeados e a estrutura de esquema resultante.](../../images/tutorials/map-csv-recommendations/schema-generated.png)

>[!NOTE]
>
>Você pode filtrar todos os campos no esquema com base em vários critérios durante o fluxo de trabalho de mapeamento de campos da origem para o destino. O comportamento padrão é exibir todos os campos mapeados. Para alterar os campos exibidos, selecione o ícone de filtro ao lado do campo de entrada de pesquisa e escolha entre as opções suspensas.<br> ![A etapa de mapeamento do fluxo de trabalho de criação do esquema CSV para XDM com o ícone de filtro e o menu suspenso destacados.](../../images/tutorials/map-csv-recommendations/source-field-to-target-mapping-filter.png "A etapa de mapeamento do fluxo de trabalho de criação do esquema CSV para XDM com o ícone de filtro e o menu suspenso destacados."){width="100" zoomable="yes"}

Aqui, você pode, opcionalmente, [editar os mapeamentos de campo](#edit-mappings) ou [alterar os grupos de campos aos quais estão associados](#edit-schema) de acordo com suas necessidades. Quando satisfeito, selecione **[!UICONTROL Concluir]** para concluir o mapeamento e iniciar o fluxo de dados configurado anteriormente. Os dados do CSV são assimilados no sistema e preenchem um conjunto de dados com base na estrutura de esquema gerada, pronta para ser consumida pelos serviços downstream da plataforma.

![A variável [!UICONTROL Concluir] sendo selecionado, concluindo o processo de mapeamento de CSV.](../../images/tutorials/map-csv-recommendations/finish-mapping.png)

### Editar mapeamentos de campo {#edit-mappings}

Use a visualização de mapeamento de campo para editar os mapeamentos existentes ou removê-los totalmente. Para obter mais informações sobre como gerenciar um conjunto de mapeamento na interface, consulte [Guia de interface do usuário para mapeamento de preparação de dados](../../../data-prep/ui/mapping.md#mapping-interface).

### Editar grupos de campos {#edit-field-groups}

Os campos CSV são mapeados automaticamente para grupos de campos XDM existentes usando modelos ML. Se desejar alterar o grupo de campos para qualquer campo CSV específico, selecione **[!UICONTROL Editar]** ao lado da árvore de esquema.

![A variável [!UICONTROL Editar] botão sendo selecionado ao lado da árvore de esquema.](../../images/tutorials/map-csv-recommendations/edit-schema-structure.png)

Uma caixa de diálogo é exibida, permitindo editar o nome de exibição, o tipo de dados e o grupo de campos de qualquer campo no mapeamento. Selecione o ícone de edição (![Ícone Editar](../../images/tutorials/map-csv-recommendations/edit-icon.png)) ao lado de um campo de origem para editar seus detalhes na coluna direita antes de selecionar **[!UICONTROL Aplicar]**.

![O grupo de campos recomendado para um campo de origem que está sendo alterado.](../../images/tutorials/map-csv-recommendations/select-schema-field.png)

Quando terminar de ajustar as recomendações do esquema para seus campos de origem, selecione **[!UICONTROL Salvar]** para aplicar as alterações.

## Próximas etapas

Este guia abordou como mapear um arquivo CSV para um esquema XDM usando recomendações geradas por IA, permitindo que você traga esses dados para a Platform por meio da assimilação em lote.

Para obter etapas sobre como mapear um arquivo CSV para um esquema existente, consulte o [fluxo de trabalho de mapeamento de esquema existente](./existing-schema.md). Para obter informações sobre transmissão de dados para a Platform em tempo real por meio de conexões de origem pré-criadas, consulte o [visão geral das origens](../../../sources/home.md).
