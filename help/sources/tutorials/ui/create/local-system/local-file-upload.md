---
keywords: Experience Platform;página inicial;tópicos populares;sistema local;upload de arquivo;mapear csv;mapear arquivo csv;mapear arquivo csv para xdm;mapear csv para xdm;guia da interface do usuário;
solution: Experience Platform
title: Criar um Conector de origem de upload de arquivo local na interface
type: Tutorial
description: Saiba como criar uma conexão de origem para seu sistema local para trazer arquivos locais para a Platform
exl-id: 9ce15362-c30d-40cc-9d9c-caa650579390
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 1%

---

# Criar um conector de origem de upload de arquivo local na interface

Este tutorial fornece etapas para criar um conector de origem de upload de arquivo local para assimilar arquivos locais na Platform usando a interface do usuário.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes da Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): a estrutura padronizada pela qual a Platform organiza os dados de experiência do cliente.
   * [Noções básicas da composição do esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os componentes básicos dos esquemas XDM, incluindo princípios fundamentais e práticas recomendadas na composição do esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

## Fazer upload de arquivos locais para a Platform

Na interface do usuário da Platform, selecione **[!UICONTROL Origens]** na barra de navegação esquerda, para acessar a [!UICONTROL Origens] espaço de trabalho. A variável [!UICONTROL Catálogo] exibe uma variedade de fontes para as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

No [!UICONTROL Sistema local] categoria, selecione **[!UICONTROL Upload de arquivo local]** e selecione **[!UICONTROL Adicionar dados]**.

![catálogo](../../../../images/tutorials/create/local/catalog.png)

### Usar um conjunto de dados existente

A variável [!UICONTROL Detalhes do fluxo de dados] permite selecionar se você deseja assimilar os dados CSV em um conjunto de dados existente ou em um novo conjunto de dados.

Para assimilar dados CSV em um conjunto de dados existente, selecione **[!UICONTROL Conjunto de dados existente]**. É possível recuperar um conjunto de dados existente usando o [!UICONTROL Pesquisa avançada] ou rolando pela lista de conjuntos de dados existentes no menu suspenso.

Com um conjunto de dados selecionado, forneça um nome para o fluxo de dados e uma descrição opcional.

Durante esse processo, você também pode ativar [!UICONTROL Diagnóstico de erro] e [!UICONTROL Assimilação parcial]. [!UICONTROL Diagnóstico de erro] permite a geração de mensagens de erro detalhadas para qualquer registro incorreto que ocorra em seu fluxo de dados, enquanto [!UICONTROL Assimilação parcial] O permite assimilar dados que contêm erros, até um determinado limite definido manualmente. Consulte a [visão geral da assimilação parcial de lotes](../../../../../ingestion/batch-ingestion/partial.md) para obter mais informações.

![conjunto de dados existente](../../../../images/tutorials/create/local/existing-dataset.png)

### Usar um novo conjunto de dados

Para assimilar seus dados CSV em um novo conjunto de dados, selecione **[!UICONTROL Novo conjunto de dados]** e forneça um nome de conjunto de dados de saída e uma descrição opcional. Em seguida, selecione um esquema para mapear usando o [!UICONTROL Pesquisa avançada] ou rolando pela lista de esquemas existentes no menu suspenso.

Com um esquema selecionado, forneça um nome para o fluxo de dados e uma descrição opcional e aplique a [!UICONTROL Diagnóstico de erro] e [!UICONTROL Assimilação parcial] as configurações desejadas para o seu fluxo de dados. Quando terminar, selecione **[!UICONTROL Próxima]**.

![novo conjunto de dados](../../../../images/tutorials/create/local/new-dataset.png)

### Selecionar dados

A variável [!UICONTROL Selecionar dados] é exibida, fornecendo uma interface para fazer upload dos arquivos locais e visualizar sua estrutura e conteúdo. Selecionar **[!UICONTROL Escolher arquivos]** para carregar um arquivo CSV do seu sistema local. Como alternativa, você pode arrastar e soltar o arquivo CSV que deseja fazer upload na [!UICONTROL Arrastar e soltar arquivos] painel.

>[!TIP]
>
>No momento, somente arquivos CSV são compatíveis com o upload de arquivo local. O tamanho máximo para cada arquivo é de 1 GB.

![choose-files](../../../../images/tutorials/create/local/choose-files.png)

Depois que o arquivo for carregado, a interface de visualização será atualizada para exibir o conteúdo e a estrutura do arquivo.

![preview-sample-data](../../../../images/tutorials/create/local/preview-sample-data.png)

Dependendo do arquivo, você pode selecionar um delimitador de coluna, como guias, vírgulas, barras verticais ou um delimitador de coluna personalizado para seus dados de origem. Selecione o **[!UICONTROL Delimitador]** e selecione o delimitador apropriado no menu.

Quando terminar, selecione **[!UICONTROL Próxima]**.

![delimitador](../../../../images/tutorials/create/local/delimiter.png)

## Mapeamento

A variável [!UICONTROL Mapeamento] é exibida, fornecendo uma interface para mapear os campos de origem do esquema de origem para os campos XDM de destino apropriados no esquema de destino.

Com base nas suas necessidades, você pode optar por mapear campos diretamente ou usar funções de preparação de dados para transformar dados de origem para derivar valores calculados ou calculados. Para obter etapas abrangentes sobre como usar a interface de mapeamento, consulte [Guia da interface de preparação de dados](../../../../../data-prep/ui/mapping.md).

Quando os conjuntos de mapeamento estiverem prontos, selecione **[!UICONTROL Concluir]** e aguarde alguns instantes para que o novo fluxo de dados seja criado.

![mapeamento](../../../../images/tutorials/create/local/mapping.png)

## Monitorar assimilação de dados

Depois que o arquivo CSV for mapeado e criado, você poderá monitorar os dados que estão sendo assimilados por meio dele usando o painel de monitoramento. Para obter mais informações, consulte o tutorial em [monitoramento de fluxos de dados de fontes na interface do](../../../../../dataflows/ui/monitor-sources.md).

## Próximas etapas

Ao seguir este tutorial, você mapeou com sucesso um arquivo CSV simples para um esquema XDM e o assimilou na Platform. Esses dados agora podem ser usados por downstream [!DNL Platform] serviços como [!DNL Real-Time Customer Profile]. Consulte a visão geral do [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) para obter mais informações.
