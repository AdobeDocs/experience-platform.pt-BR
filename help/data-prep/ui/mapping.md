---
keywords: Experience Platform;página inicial;tópicos populares;mapear csv;mapear arquivo csv;mapear arquivo csv para xdm;mapear csv para xdm;guia de interface do usuário;mapeador;mapeamento;preparação de dados;preparação de dados;
title: Guia da interface de preparação de dados
description: Este documento fornece instruções sobre como usar as funções de preparação de dados na interface do usuário da plataforma para mapear arquivos CSV para um esquema XDM.
exl-id: fafa4aca-fb64-47ff-a97d-c18e58ae4dae
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1847'
ht-degree: 1%

---

# Guia da interface de preparação de dados

Este documento fornece instruções sobre como usar as funções de preparação de dados na interface do usuário do Adobe Experience Platform para mapear arquivos CSV para um esquema XDM.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes da Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../xdm/home.md): a estrutura padronizada pela qual a Platform organiza os dados de experiência do cliente.
   * [Noções básicas sobre a composição de esquema](../../xdm/schema/composition.md): saiba mais sobre os blocos de construção básicos de esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição de esquema.
   * [Tutorial do Editor de esquemas](../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [Serviço de identidade](../../identity-service/home.md): obtenha uma melhor visão dos clientes individuais e de seu comportamento unindo as identidades de vários dispositivos e sistemas.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md): Fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.
* [Fontes](../../sources/home.md): o Experience Platform permite que os dados sejam assimilados de várias fontes e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.

## Detalhes do fluxo de dados

>[!TIP]
>
>Você pode acessar os detalhes do fluxo de dados selecionando qualquer origem no catálogo de origens. Para obter mais informações, consulte a [visão geral das fontes](../../sources/home.md).

Antes de mapear os dados CSV para um esquema XDM, primeiro estabeleça os detalhes do fluxo de dados.

A página [!UICONTROL Detalhes do fluxo de dados] permite selecionar se você deseja assimilar os dados CSV em um conjunto de dados de destino existente ou em um novo conjunto de dados de destino. Um conjunto de dados existente vem com um esquema de destino pré-criado para mapear seus dados, enquanto um novo conjunto de dados exige que você selecione um esquema existente ou crie um novo esquema para mapear seus dados.

### Usar um conjunto de dados de destino existente

Para assimilar seus dados CSV em um conjunto de dados existente, selecione **[!UICONTROL Conjunto de dados existente]**. Você pode recuperar um conjunto de dados existente usando a opção [!UICONTROL Pesquisa avançada] ou rolando pela lista de conjuntos de dados existentes no menu suspenso.

Com um conjunto de dados selecionado, forneça um nome para o fluxo de dados e uma descrição opcional.

Durante esse processo, você também pode habilitar o [!UICONTROL Diagnóstico de erro] e a [!UICONTROL Assimilação parcial]. O [!UICONTROL Diagnóstico de erro] habilita a geração de mensagens de erro detalhadas para todos os registros incorretos que ocorrem no fluxo de dados, enquanto a [!UICONTROL Assimilação parcial] permite assimilar dados que contêm erros, até um determinado limite definido manualmente. Consulte a [visão geral da assimilação parcial de lotes](../../ingestion/batch-ingestion/partial.md) para obter mais informações.

![conjunto de dados existente](../images/ui/mapping/existing-dataset.png)

### Usar um novo conjunto de dados de destino

Para assimilar seus dados CSV em um novo conjunto de dados, selecione **[!UICONTROL Novo conjunto de dados]** e forneça um nome de conjunto de dados de saída e uma descrição opcional. Em seguida, selecione um esquema para mapear usando a opção [!UICONTROL Pesquisa avançada] ou rolando pela lista de esquemas existentes no menu suspenso.

Com um esquema selecionado, forneça um nome para o fluxo de dados e uma descrição opcional e aplique as [!UICONTROL configurações de diagnóstico de erro] e [!UICONTROL assimilação parcial] desejadas para o fluxo de dados. Quando terminar, selecione **[!UICONTROL Próximo]**.

![novo-conjunto-de-dados](../images/ui/mapping/new-dataset.png)

## Selecionar dados

A etapa [!UICONTROL Selecionar dados] é exibida, fornecendo uma interface para carregar seus arquivos locais e pré-visualizar sua estrutura e conteúdo. Selecione **[!UICONTROL Escolher arquivos]** para carregar um arquivo CSV do seu sistema local. Como alternativa, você pode arrastar e soltar o arquivo CSV que deseja carregar no painel [!UICONTROL Arrastar e soltar arquivos].

>[!TIP]
>
>No momento, somente arquivos CSV são compatíveis com o upload de arquivo local. O tamanho máximo para cada arquivo é de 1 GB.

![escolher-arquivos](../images/ui/mapping/choose-files.png)

Depois que o arquivo for carregado, a interface de visualização será atualizada para exibir o conteúdo e a estrutura do arquivo.

![visualizar-amostra-dados](../images/ui/mapping/preview-sample-data.png)

Dependendo do arquivo, você pode selecionar um delimitador de coluna, como guias, vírgulas, barras verticais ou um delimitador de coluna personalizado para seus dados de origem. Selecione a seta suspensa **[!UICONTROL Delimitador]** e selecione o delimitador apropriado no menu.

Quando terminar, selecione **[!UICONTROL Próximo]**.

![delimitador](../images/ui/mapping/delimiter.png)

## Mapeamento

A interface **[!UICONTROL mapping]** fornece uma ferramenta abrangente para mapear campos de origem do esquema de origem para os campos XDM de destino apropriados no esquema de destino.

![map-csv-to-xdm](../images/ui/mapping/map-csv-to-xdm.png)

### Noções básicas sobre a interface de mapeamento {#mapping-interface}

A interface de mapeamento inclui um painel que fornece informações sobre a integridade dos campos de mapeamento no contexto do fluxo de trabalho de assimilação. O painel exibe os seguintes detalhes em relação aos campos de mapeamento:

| Propriedade | Descrição |
| --- | --- |
| [!UICONTROL Campos mapeados] | Exibe o número total de campos de origem que foram mapeados para um campo XDM de destino, independentemente de erros. |
| [!UICONTROL Campos obrigatórios] | Exibe o número de campos de mapeamento necessários. |
| [!UICONTROL Campos de identidade] | Exibe o número total de campos de mapeamento definidos como identidade. Esses campos de mapeamento são representados por um ícone de impressão digital. |
| [!UICONTROL Erros] | Exibe o número de campos de mapeamento incorretos. |

![painel superior](../images/ui/mapping/top-panel.png)

A interface de mapeamento também fornece um painel de opções que você pode escolher para interagir ou filtrar melhor pelos campos de mapeamento.

![segundo-painel](../images/ui/mapping/second-panel.png)

Para procurar um conjunto de mapeamento específico, selecione **[!UICONTROL Pesquisar campos de origem]** e insira o nome dos dados de origem que deseja isolar.

![pesquisar](../images/ui/mapping/search.png)

Selecione **[!UICONTROL Todos os campos de origem]** para ver um menu suspenso de opções de filtragem para restringir melhor sua exibição da interface de mapeamento.

As opções de filtro são:

| Campos do Source | Descrição |
| --- | --- |
| [!UICONTROL Todos os campos de origem] | Essa opção exibe todos os campos de origem do esquema de origem. Essa opção é exibida por padrão. |
| [!UICONTROL Campos obrigatórios] | Essa opção filtra o esquema de origem para exibir apenas os campos necessários para concluir o mapeamento. |
| [!UICONTROL Campos de identidade] | Essa opção filtra o esquema de origem para exibir apenas os campos marcados para Identidade. |
| [!UICONTROL Campos mapeados] | Essa opção filtra o esquema de origem para exibir apenas os campos que já foram mapeados. |
| [!UICONTROL Campos não mapeados] | Essa opção filtra o esquema de origem para exibir apenas os campos que ainda não foram mapeados. |
| [!UICONTROL Campos com recomendação] | Essa opção filtra o esquema de origem para exibir apenas os campos que contêm recomendações de mapeamento. |

Selecione **[!UICONTROL Campos com erros]** para ver todos os campos de mapeamento com erros.

![filtro](../images/ui/mapping/filter.png)

Uma exibição isolada de campos de mapeamento incorretos é exibida, permitindo que você solucione erros por meio de recomendações de mapeamento inteligentes ou pela árvore de mapeamento manual.

![campos com erros](../images/ui/mapping/fields-with-errors.png)

### Adicionar um novo tipo de campo

Você pode adicionar um novo campo de mapeamento ou um campo calculado selecionando **[!UICONTROL Novo tipo de campo]**.

#### Novo campo de mapeamento

Para adicionar um novo campo de mapeamento, selecione **[!UICONTROL Novo tipo de campo]** e **[!UICONTROL Adicionar novo campo]** no menu suspenso exibido.

![adicionar-novo-campo](../images/ui/mapping/add-new-field.png)

Em seguida, selecione o campo de origem que deseja adicionar da árvore de esquema de origem exibida e selecione **[!UICONTROL Selecionar]**.

![selecionar novo campo](../images/ui/mapping/select-new-field.png)

A interface de mapeamento é atualizada com o campo de origem selecionado e um campo de destino vazio. Selecione **[!UICONTROL Mapear campo de destino]** para começar a mapear o novo campo de origem para seu campo XDM de destino apropriado.

![campo-alvo-mapa](../images/ui/mapping/map-target-field.png)

Uma árvore de esquema de destino interativa é exibida, permitindo navegar manualmente pelo esquema de destino e localizar o campo XDM de destino apropriado para o campo de origem.

![mapeamento manual](../images/ui/mapping/manual-mapping.png)

Quando terminar, selecione o ícone do esquema para fechar a interface do esquema de destino.

![árvore-esquema](../images/ui/mapping/schema-tree.png)

#### Campos calculados {#calculated-fields}

Os campos calculados permitem que valores sejam criados com base nos atributos no esquema de entrada. Esses valores podem ser atribuídos a atributos no esquema de destino e receber um nome e uma descrição para facilitar a referência. Os campos calculados têm um comprimento máximo de 4096 caracteres.

Para criar um campo calculado, selecione **[!UICONTROL Novo tipo de campo]** e **[!UICONTROL Adicionar campo calculado]**

![adicionar-campo-calculado](../images/ui/mapping/add-calculated-field.png)

O painel **[!UICONTROL Criar campo calculado]** é exibido. A caixa de diálogo à esquerda contém os campos, funções e operadores compatíveis com os campos calculados. Selecione uma das guias para começar a adicionar funções, campos ou operadores ao editor de expressão.

| Tabulação | Descrição |
| --- | ----------- |
| [!UICONTROL Função] | A guia functions lista as funções disponíveis para transformar os dados. Para saber mais sobre as funções que você pode usar em campos calculados, leia o guia em [usando funções de Preparo de Dados (Mapeador)](../functions.md). |
| [!UICONTROL Campo] | A guia fields lista campos e atributos disponíveis no schema de origem. |
| [!UICONTROL Operador] | A guia operators lista os operadores disponíveis para transformar os dados. |

![guias](../images/ui/mapping/tabs.png)

Você pode adicionar campos, funções e operadores manualmente usando o editor de expressão no centro. Selecione o editor para começar a criar uma expressão. Depois de concluir, selecione **[!UICONTROL Salvar]** para continuar.

![criar-campo-calculado](../images/ui/mapping/create-calculated-field.png)

### Importar mapeamento {#import}

Você pode reutilizar o mapeamento de um fluxo de dados existente para reduzir o tempo de configuração manual de sua assimilação de dados e limitar erros. Selecione **[!UICONTROL Importar mapeamento]** para reutilizar um mapeamento existente.

![import-mapping](../images/ui/mapping/import-mapping.png)

A janela [!UICONTROL Importar mapeamento] é exibida, fornecendo uma lista de fluxos de dados para escolher.

Selecione o ícone de visualização para visualizar o mapeamento do fluxo de dados selecionado.

![list-mapping](../images/ui/mapping/list-mapping.png)

A janela de visualização permite inspecionar o mapeamento existente antes de importar para o fluxo de dados. Depois de verificar o mapeamento, você pode selecionar **[!UICONTROL Voltar]** para retornar à lista de fluxos de dados e inspecionar outro conjunto de mapeamentos, ou pode selecionar **[!UICONTROL Selecionar]** para continuar.

![mapeamento de visualização](../images/ui/mapping/preview-mapping.png)

Como alternativa, você pode selecionar o mapeamento que deseja importar na janela da lista de fluxos de dados. Selecione o fluxo de dados que contém o mapeamento que você deseja importar e selecione **[!UICONTROL Selecionar]** para continuar.

![selecionar-mapeamento](../images/ui/mapping/select-mapping.png)

A interface é atualizada com o mapeamento importado.

>[!NOTE]
>
>Todos os conjuntos de mapeamento existentes que você estabelecer ou as recomendações de mapeamento de ML serão substituídos pelo mapeamento que você importou de um fluxo de dados existente.

![mapeamento-importado](../images/ui/mapping/mapping-imported.png)

Selecione **[!UICONTROL Visualizar dados]** para ver os resultados do mapeamento de até 100 linhas de dados de amostra do conjunto de dados selecionado.

![dados de visualização](../images/ui/mapping/preview-data.png)

Durante a visualização, a coluna de identidade é priorizada como o primeiro campo, pois são as informações principais necessárias ao validar os resultados do mapeamento. Quando terminar, selecione **[!UICONTROL Fechar]**.

![tela de visualização](../images/ui/mapping/preview-screen.png)

Para remover todos os campos de mapeamento, selecione **[!UICONTROL Limpar todos os mapeamentos]**.

![limpar-tudo](../images/ui/mapping/clear-all.png)

### Uso da interface de mapeamento

A Platform fornece recomendações inteligentes automaticamente para campos mapeados automaticamente com base no esquema ou conjunto de dados de destino selecionado. Você pode ajustar manualmente as regras de mapeamento para atender aos seus casos de uso ou corrigir campos de mapeamento duplicados para eliminar erros.

![interface-mapeamento](../images/ui/mapping/mapping-interface.png)

Selecione o ícone de lâmpada no campo de destino que você deseja ajustar.

![mapeamento-recc](../images/ui/mapping/mapping-recc.png)

O painel pop-up [!UICONTROL Recomendações de mapeamento] é exibido, exibindo uma lista de campos de destino recomendados que podem ser mapeados para um campo de origem específico. Por padrão, a primeira recomendação é aplicada automaticamente.

Às vezes, mais de uma recomendação está disponível para o esquema de origem. Quando isso acontece, o cartão de mapeamento exibe a recomendação mais proeminente, seguida por um ícone que contém o número de recomendações adicionais disponíveis. Selecionar o ícone de lâmpada mostrará uma lista das recomendações adicionais. Você pode escolher uma das recomendações alternativas marcando a caixa de seleção ao lado da recomendação para a qual deseja mapear.

Aqui, você pode alterar o campo de destino selecionado para corrigir um erro ou corresponder ao seu caso de uso.

Como alternativa, você pode selecionar **[!UICONTROL Selecionar manualmente]** para usar manualmente a árvore de mapeamento do esquema de destino interativo.

![recc-panel](../images/ui/mapping/recc-panel.png)

A interface de mapeamento do esquema de destino aparece na mesma exibição dos campos de mapeamento, permitindo modificar pares de mapeamento na mesma tela. Selecione o campo de destino que se ajusta ao seu caso de uso ou que corrige seus erros.

![selecionar-campo-alvo](../images/ui/mapping/select-target-field.png)

Quando terminar, selecione **[!UICONTROL Concluir]** para continuar.

![concluir](../images/ui/mapping/finish.png)

## Próximas etapas

Ao ler este documento, você mapeou com êxito um arquivo CSV para um esquema XDM de destino usando a interface de mapeamento na interface da Platform. Consulte os seguintes documentos para obter mais informações:

* [Visão geral do Preparo de dados](../home.md)
* [Visão geral das fontes](../../sources/home.md)
* [Monitorar fluxos de dados de fontes na interface do usuário](../../dataflows/ui/monitor-sources.md)
