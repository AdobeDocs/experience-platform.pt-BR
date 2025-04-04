---
keywords: Experience Platform;página inicial;tópicos populares;sistema local;upload de arquivo;mapear csv;mapear arquivo csv;mapear arquivo csv para xdm;mapear csv para xdm;guia da interface do usuário;
solution: Experience Platform
title: Criar um Conector Source para upload de arquivo local na interface
type: Tutorial
description: Saiba como criar uma conexão de origem para seu sistema local para trazer arquivos locais para o Experience Platform
exl-id: 9ce15362-c30d-40cc-9d9c-caa650579390
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '777'
ht-degree: 0%

---

# Criar um conector de origem de upload de arquivo local na interface

Este tutorial fornece etapas para a criação de um conector de origem de upload de arquivo local para assimilar arquivos locais no Experience Platform usando a interface do usuário.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): a estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
   * [Noções básicas sobre a composição de esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os blocos de construção básicos de esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição de esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

## Fazer upload de arquivos locais para o Experience Platform

Na interface do usuário do Experience Platform, selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar o espaço de trabalho [!UICONTROL Fontes]. A tela [!UICONTROL Catálogo] exibe uma variedade de fontes para as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria [!UICONTROL Sistema local], selecione **[!UICONTROL Carregamento de arquivo local]** e **[!UICONTROL Adicionar dados]**.

![catálogo](../../../../images/tutorials/create/local/catalog.png)

### Usar um conjunto de dados existente

A página [!UICONTROL Detalhes do fluxo de dados] permite selecionar se você deseja assimilar os dados CSV em um conjunto de dados existente ou em um novo conjunto de dados.

Para assimilar seus dados CSV em um conjunto de dados existente, selecione **[!UICONTROL Conjunto de dados existente]**. Você pode recuperar um conjunto de dados existente usando a opção [!UICONTROL Pesquisa avançada] ou rolando pela lista de conjuntos de dados existentes no menu suspenso.

Com um conjunto de dados selecionado, forneça um nome para o fluxo de dados e uma descrição opcional.

Durante esse processo, você também pode habilitar o [!UICONTROL Diagnóstico de erro] e a [!UICONTROL Assimilação parcial]. O [!UICONTROL Diagnóstico de erro] habilita a geração de mensagens de erro detalhadas para todos os registros incorretos que ocorrem no fluxo de dados, enquanto a [!UICONTROL Assimilação parcial] permite assimilar dados que contêm erros, até um determinado limite definido manualmente. Consulte a [visão geral da assimilação parcial de lotes](../../../../../ingestion/batch-ingestion/partial.md) para obter mais informações.

![conjunto de dados existente](../../../../images/tutorials/create/local/existing-dataset.png)

### Usar um novo conjunto de dados

Para assimilar seus dados CSV em um novo conjunto de dados, selecione **[!UICONTROL Novo conjunto de dados]** e forneça um nome de conjunto de dados de saída e uma descrição opcional. Em seguida, selecione um esquema para mapear usando a opção [!UICONTROL Pesquisa avançada] ou rolando pela lista de esquemas existentes no menu suspenso.

Com um esquema selecionado, forneça um nome para o fluxo de dados e uma descrição opcional e aplique as [!UICONTROL configurações de diagnóstico de erro] e [!UICONTROL assimilação parcial] desejadas para o fluxo de dados. Quando terminar, selecione **[!UICONTROL Próximo]**.

![novo-conjunto-de-dados](../../../../images/tutorials/create/local/new-dataset.png)

### Selecionar dados

A etapa [!UICONTROL Selecionar dados] é exibida, fornecendo uma interface para carregar seus arquivos locais e pré-visualizar sua estrutura e conteúdo. Selecione **[!UICONTROL Escolher arquivos]** para carregar um arquivo CSV do seu sistema local. Como alternativa, você pode arrastar e soltar o arquivo CSV que deseja carregar no painel [!UICONTROL Arrastar e soltar arquivos].

>[!TIP]
>
>No momento, somente arquivos CSV são compatíveis com o upload de arquivo local. O tamanho máximo para cada arquivo é de 1 GB.

![escolher-arquivos](../../../../images/tutorials/create/local/choose-files.png)

Depois que o arquivo for carregado, a interface de visualização será atualizada para exibir o conteúdo e a estrutura do arquivo.

![visualizar-amostra-dados](../../../../images/tutorials/create/local/preview-sample-data.png)

Dependendo do arquivo, você pode selecionar um delimitador de coluna, como guias, vírgulas, barras verticais ou um delimitador de coluna personalizado para seus dados de origem. Selecione a seta suspensa **[!UICONTROL Delimitador]** e selecione o delimitador apropriado no menu.

Quando terminar, selecione **[!UICONTROL Próximo]**.

![delimitador](../../../../images/tutorials/create/local/delimiter.png)

## Mapeamento

A etapa [!UICONTROL Mapeamento] é exibida, fornecendo uma interface para mapear os campos de origem do esquema de origem para os campos XDM de destino apropriados no esquema de destino.

Com base nas suas necessidades, você pode optar por mapear campos diretamente ou usar funções de preparação de dados para transformar dados de origem para derivar valores calculados ou calculados. Para obter etapas abrangentes sobre como usar a interface de mapeamento, consulte o [guia da interface de Preparo de Dados](../../../../../data-prep/ui/mapping.md).

Quando os conjuntos de mapeamento estiverem prontos, selecione **[!UICONTROL Concluir]** e aguarde alguns momentos para criar o novo fluxo de dados.

![mapeamento](../../../../images/tutorials/create/local/mapping.png)

## Monitorar assimilação de dados

Depois que o arquivo CSV for mapeado e criado, você poderá monitorar os dados que estão sendo assimilados por meio dele usando o painel de monitoramento. Para obter mais informações, consulte o tutorial sobre [fluxos de dados de fontes de monitoramento na interface](../../../../../dataflows/ui/monitor-sources.md).

## Próximas etapas

Ao seguir este tutorial, você mapeou com sucesso um arquivo CSV simples para um esquema XDM e o assimilou na Experience Platform. Esses dados agora podem ser usados por serviços [!DNL Experience Platform] downstream, como [!DNL Real-Time Customer Profile]. Consulte a visão geral de [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) para obter mais informações.
