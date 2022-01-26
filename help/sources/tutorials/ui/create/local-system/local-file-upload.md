---
keywords: Experience Platform; home; tópicos populares; sistema local; upload de arquivo; mapear csv; mapear arquivo csv; mapear arquivo csv para xdm; mapear csv para xdm; guia da interface do usuário;
solution: Experience Platform
title: Criar um conector de origem de upload de arquivo local na interface do usuário
topic-legacy: overview
type: Tutorial
description: Saiba como criar uma conexão de origem para seu sistema local para trazer arquivos locais para o Platform
exl-id: 9ce15362-c30d-40cc-9d9c-caa650579390
source-git-commit: 08805ed0d89d3d6908ddccdafda55d2f862e727e
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 0%

---

# Crie um conector de origem de upload de arquivo local na interface do usuário

Este tutorial fornece etapas para criar um conector de origem de upload de arquivo local para assimilar arquivos locais na plataforma usando a interface do usuário do .

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes da Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): A estrutura padronizada pela qual a Platform organiza os dados de experiência do cliente.
   * [Noções básicas da composição do schema](../../../../../xdm/schema/composition.md): Saiba mais sobre os elementos básicos dos esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.

## Fazer upload de arquivos locais para a plataforma

Na interface do usuário da plataforma, selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar o [!UICONTROL Fontes] espaço de trabalho. O [!UICONTROL Catálogo] exibe uma variedade de fontes para as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Em [!UICONTROL Sistema local] categoria , selecione **[!UICONTROL Upload de arquivo local]** e selecione **[!UICONTROL Adicionar dados]**.

![catálogo](../../../../images/tutorials/create/local/catalog.png)

### Usar um conjunto de dados existente

O [!UICONTROL Detalhes do fluxo de dados] permite selecionar se deseja assimilar seus dados CSV em um conjunto de dados existente ou em um novo conjunto de dados.

Para assimilar seus dados CSV em um conjunto de dados existente, selecione **[!UICONTROL Conjunto de dados existente]**. Você pode recuperar um conjunto de dados existente usando o [!UICONTROL Pesquisa avançada] ou percorrendo a lista de conjuntos de dados existentes no menu suspenso.

Com um conjunto de dados selecionado, forneça um nome para o seu fluxo de dados e uma descrição opcional.

Durante esse processo, também é possível ativar [!UICONTROL Diagnóstico de erros] e [!UICONTROL Ingestão parcial]. [!UICONTROL Diagnóstico de erros] permite a geração detalhada de mensagens de erro para qualquer registro incorreto que ocorra no seu fluxo de dados, enquanto [!UICONTROL Ingestão parcial] O permite assimilar dados contendo erros, até um determinado limite definido manualmente. Consulte a [visão geral da ingestão parcial de lote](../../../../../ingestion/batch-ingestion/partial.md) para obter mais informações.

![conjunto de dados existente](../../../../images/tutorials/create/local/existing-dataset.png)

### Usar um novo conjunto de dados

Para assimilar seus dados CSV em um novo conjunto de dados, selecione **[!UICONTROL Novo conjunto de dados]** e, em seguida, forneça um nome de conjunto de dados de saída e uma descrição opcional. Em seguida, selecione um esquema para mapear usando o [!UICONTROL Pesquisa avançada] ou rolando pela lista de schemas existentes no menu suspenso.

Com um esquema selecionado, forneça um nome para o seu fluxo de dados e uma descrição opcional e, em seguida, aplique a variável [!UICONTROL Diagnóstico de erros] e [!UICONTROL Ingestão parcial] configurações desejadas para o fluxo de dados. Quando terminar, selecione **[!UICONTROL Próximo]**.

![novo conjunto de dados](../../../../images/tutorials/create/local/new-dataset.png)

### Selecionar dados

O [!UICONTROL Selecionar dados] será exibida, fornecendo uma interface para carregar seus arquivos locais e visualizar sua estrutura e conteúdo. Selecionar **[!UICONTROL Escolher arquivos]** para fazer upload de um arquivo CSV em seu sistema local. Como alternativa, você pode arrastar e soltar o arquivo CSV que deseja fazer upload no [!UICONTROL Arrastar e soltar arquivos] painel.

>[!TIP]
>
>Atualmente, apenas os arquivos CSV são compatíveis com o upload de arquivo local. O tamanho máximo de arquivo para cada arquivo é de 1 GB.

![choice-files](../../../../images/tutorials/create/local/choose-files.png)

Depois que o arquivo é carregado, a interface de visualização é atualizada para exibir o conteúdo e a estrutura do arquivo.

![preview-sample-data](../../../../images/tutorials/create/local/preview-sample-data.png)

Dependendo do arquivo, é possível selecionar um delimitador de coluna, como guias, vírgulas, barra vertical ou um delimitador de coluna personalizado para os dados de origem. Selecione o **[!UICONTROL Delimitador]** seta suspensa e selecione o delimitador apropriado no menu.

Quando terminar, selecione **[!UICONTROL Próximo]**.

![delimiter](../../../../images/tutorials/create/local/delimiter.png)

## Mapeamento

O [!UICONTROL Mapeamento] é exibida, fornecendo uma interface para mapear os campos de origem do esquema de origem para os campos XDM de destino apropriados no esquema de destino.

Com base em suas necessidades, você pode optar por mapear campos diretamente ou usar funções de preparação de dados para transformar dados de origem em valores calculados ou calculados. Para obter etapas abrangentes sobre o uso da interface de mapeamento, consulte o [Guia da interface do usuário de preparação de dados](../../../../../data-prep/ui/mapping.md).

Quando os conjuntos de mapeamento estiverem prontos, selecione **[!UICONTROL Concluir]** e aguarde alguns instantes para que o novo fluxo de dados seja criado.

![mapeamento](../../../../images/tutorials/create/local/mapping.png)

## Monitorar assimilação de dados

Depois que o arquivo CSV for mapeado e criado, você poderá monitorar os dados que estão sendo assimilados por meio dele usando o painel de monitoramento. Para obter mais informações, consulte o tutorial em [monitoramento de fluxos de dados de fontes na interface do usuário](../../../../../dataflows/ui/monitor-sources.md).

## Próximas etapas

Ao seguir este tutorial, você mapeou com sucesso um arquivo CSV simples para um esquema XDM e o assimilou na Platform. Esses dados agora podem ser usados pelo downstream [!DNL Platform] serviços como [!DNL Real-time Customer Profile]. Consulte a visão geral para [[!DNL Real-time Customer Profile]](../../../../../profile/home.md) para obter mais informações.
