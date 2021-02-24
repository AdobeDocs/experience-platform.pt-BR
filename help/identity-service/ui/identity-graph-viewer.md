---
keywords: Experience Platform;home;popular topics;visualizador de gráfico de identidade;Visualizador de gráfico de identidade;Visualizador de gráfico;Visualizador de gráfico;namespace de identidade;namespace de identidade;identidade;serviço de identidade;serviço de identidade
solution: Experience Platform
title: Visão geral do visualizador do gráfico de identidade
topic: tutorial
description: Um gráfico de identidade é um mapa de relacionamentos entre diferentes identidades para um cliente específico, fornecendo uma representação visual de como o cliente interage com sua marca em diferentes canais.
translation-type: tm+mt
source-git-commit: f4326c7a8bb8af90c092d3790e51c133744d498f
workflow-type: tm+mt
source-wordcount: '1038'
ht-degree: 1%

---


# Visão geral do visualizador de gráficos de identidade

Um gráfico de identidade é um mapa de relacionamentos entre diferentes identidades para um cliente específico, fornecendo uma representação visual de como o cliente interage com sua marca em diferentes canais. Todos os gráficos de identidade do cliente são gerenciados e atualizados coletivamente pelo Adobe Experience Platform Identity Service em tempo quase real, em resposta à atividade do cliente.

O visualizador de gráficos de identidade na interface do usuário da Plataforma permite visualizar e entender melhor quais identidades de clientes são agrupadas e de que maneiras. O visualizador permite que você arraste e interaja com diferentes partes do gráfico, permitindo que você examine relações de identidade complexas, depure com mais eficiência e se beneficie de maior transparência com a forma como as informações estão sendo utilizadas.

## Vídeo tutorial

O vídeo a seguir é destinado a suportar sua compreensão do visualizador de gráficos de identidade.

>[!VIDEO](https://video.tv.adobe.com/v/331030/?quality=12&learn=on)

## Introdução

Trabalhar com o visualizador de gráficos de identidade requer uma compreensão dos vários serviços da Adobe Experience Platform envolvidos. Antes de começar a trabalhar com o visualizador de gráficos de identidade, consulte a documentação dos seguintes serviços:

- [[!DNL Identity Service]](../home.md): Obtenha uma melhor visualização de clientes individuais e de seu comportamento ao unir identidades entre dispositivos e sistemas.

### Terminologia

- **Identidade (nó):** uma identidade ou um nó são dados exclusivos de uma entidade, normalmente uma pessoa. Uma identidade é composta de uma namespace e um valor de identidade.
- **Link (borda):** Um link ou uma borda representa a conexão entre identidades.
- **Gráfico (cluster):** Um gráfico ou cluster é um grupo de identidades e links que representam uma pessoa.

## Acessar o visualizador de gráficos de identidade

Para usar o visualizador de gráficos de identidade na interface, selecione **[!UICONTROL Identidades]** no painel de navegação esquerdo e selecione a guia **[!UICONTROL Gráfico de identidade]**. Na tela **[!UICONTROL Namespace de identidade]**, clique no ícone **[!UICONTROL Selecionar namespace de identidade]** para procurar a namespace que pretende utilizar.

![namespace](../images/identity-graph-viewer/identity-namespace.png)

O painel **[!UICONTROL Selecionar namespace de identidade]** é exibido. Esta tela contém uma lista de namespaces disponíveis para sua organização, incluindo informações sobre uma namespace **[!UICONTROL Nome de exibição]**, **[!UICONTROL Símbolo de identidade]**, **[!UICONTROL Proprietário]**, **[!UICONTROL Data da última atualização]** e **[!UICONTROL Descrição]**. Você pode usar qualquer uma das namespaces fornecidas, desde que tenha um valor de identidade válido conectado a elas.

Selecione a namespace que pretende utilizar e clique em **[!UICONTROL Selecione]** para prosseguir.

![select-identity-namespace](../images/identity-graph-viewer/select-identity-namespace.png)

Depois de selecionar uma namespace, digite o valor correspondente para um cliente específico na caixa de texto **[!UICONTROL Valor de identidade]** e selecione **[!UICONTROL Visualização]**.

![add-identity-value](../images/identity-graph-viewer/identity-value-filled.png)

### Acessar o visualizador de gráficos de identidade a partir de conjuntos de dados

Você também pode acessar o visualizador de gráficos de identidade usando a interface de conjuntos de dados. Na página de conjuntos de dados [!UICONTROL Procurar], selecione um conjunto de dados com o qual deseja interagir e selecione **[!UICONTROL conjunto de dados de Pré-visualização]**

![Conjunto de dados de pré-visualização](../images/identity-graph-viewer/preview-dataset.png)

Na janela pré-visualização, selecione um ícone de impressão digital para ver as identidades representadas pelo visualizador de gráficos de identidade.

>[!TIP]
>
>O ícone de impressão digital só será exibido se o conjunto de dados tiver duas ou mais identidades.

![impressão digital](../images/identity-graph-viewer/fingerprint.png)

O visualizador de gráficos de identidade é exibido. No lado esquerdo da tela está o gráfico de identidade que exibe todas as identidades vinculadas à namespace selecionada e o valor de identidade inserido. Cada nó de identidade consiste em uma namespace e seu valor de ID correspondente. Você pode selecionar e manter qualquer identidade para arrastar e interagir com o gráfico. Como alternativa, você pode passar o mouse sobre uma identidade para ver informações sobre seu valor de ID. A saída do gráfico também é exibida como uma lista com guias no centro da tela.

>[!IMPORTANT]
>
>Um gráfico de identidade requer no mínimo duas identidades vinculadas para serem geradas, bem como uma namespace e um par de ID válidos. O número máximo de identidades que o visualizador de gráficos pode exibir é 150. Consulte a seção [Appendix](#appendix) abaixo para obter mais informações.

![gráfico de identidade](../images/identity-graph-viewer/graph-viewer.png)

Selecione uma identidade para atualizar a linha realçada na tabela **[!UICONTROL Identidades]** e para atualizar as informações fornecidas no painel direito, que inclui **[!UICONTROL Valor]**, **[!UICONTROL ID do lote]** e a data **[!UICONTROL Última atualização]** da identidade.

![select-identity](../images/identity-graph-viewer/select-identity.png)

Você pode filtrar por um gráfico e isolar uma namespace específica usando a opção de classificação na parte superior da tabela **[!UICONTROL Identidades]**. No menu suspenso, selecione a namespace que deseja realçar.

![filtrar por namespace](../images/identity-graph-viewer/filter-namespace.png)

O visualizador de gráficos retorna, destacando a namespace selecionada. A opção de filtro também atualiza a tabela **[!UICONTROL Identidades]** para retornar informações somente para a namespace selecionada.

![filtrado](../images/identity-graph-viewer/filtered.png)

A parte superior direita da caixa do visualizador de gráficos contém opções de ampliação. Selecione o ícone **(+)** para aplicar zoom no gráfico ou no ícone **(-)** para aplicar menos zoom.

![zoom](../images/identity-graph-viewer/zoom.png)

Você pode visualização mais informações sobre lotes selecionando **[!UICONTROL Fonte de dados]** no cabeçalho. A tabela **[!UICONTROL Fonte de dados]** exibe uma lista de **[!UICONTROL IDs de lote]** associadas ao gráfico, bem como suas **[!UICONTROL IDs vinculadas]**, schema de origem e data de ingestão.

![fonte de dados](../images/identity-graph-viewer/data-source-table.png)

Você pode selecionar qualquer um dos links em um gráfico de identidade para ver todos os lotes de origem que contribuíram para o link.

![links selecionados](../images/identity-graph-viewer/select-edge.png)

Como alternativa, você pode selecionar um lote para ver todos os links para os quais esse lote contribuiu.

![links selecionados](../images/identity-graph-viewer/select-batch.png)

Gráficos de identidade com grupos maiores de identidades também são acessíveis por meio do visualizador de gráficos de identidade.

![cluster grande](../images/identity-graph-viewer/large-cluster.png)

## Apêndice

A seção a seguir fornece informações adicionais para trabalhar com o visualizador de gráficos de identidade.

### Noções básicas sobre mensagens de erro

Erros podem ocorrer ao acessar o visualizador de gráficos de identidade. A seguir está uma lista de pré-requisitos e limitações que devem ser observados ao trabalhar com o visualizador de gráficos de identidade.

- Deve existir um valor de identidade na namespace selecionada.
- O visualizador de gráficos de identidade requer no mínimo duas identidades vinculadas para serem geradas. É possível que haja apenas um valor de identidade e nenhuma identidade vinculada, e nesse caso, o valor só existiria no visualizador [!DNL Profile].
- O visualizador de gráficos de identidade não pode exceder o máximo de 150 identidades.

![tela de erro](../images/identity-graph-viewer/error-screen.png)

## Próximas etapas

Ao ler este documento, você aprendeu a explorar os gráficos de identidade de seus clientes na interface do usuário da plataforma. Para obter mais informações sobre identidades na Plataforma, consulte a [visão geral do Serviço de Identidade](../home.md)

## Changelog

| Data | Ação |
| ---- | ------ |
| 2021-01 | <ul><li>Adicionado suporte para streaming de dados ingeridos e caixa de proteção de não produção.</li><li>Correção de erros secundários.</li></ul> |
| 2021-02 | <ul><li>O visualizador de gráficos de identidade é tornado acessível por meio da pré-visualização do conjunto de dados.</li><li>Correção de erros secundários.</li><li>O visualizador de gráficos de identidade é disponibilizado Geralmente.</li></ul> |
