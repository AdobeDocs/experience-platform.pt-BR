---
keywords: Experience Platform;home;popular topics;Segmentation Service;segmentation;Segmentation;create a dataset;export audience segment;export segment;
solution: Experience Platform
title: Criar um conjunto de dados para exportar um segmento de audiência
topic: tutorial
translation-type: tm+mt
source-git-commit: d2f098cb9e4aaf5beaad02173a22a25a87a43756
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 1%

---


# Criar um conjunto de dados para exportar um segmento de audiência

[!DNL Adobe Experience Platform] permite segmentar facilmente perfis de clientes em audiências com base em atributos específicos. Depois que os segmentos forem criados, você poderá exportar essa audiência para um conjunto de dados no qual ela possa ser acessada e executada. Para que a exportação seja bem-sucedida, o conjunto de dados deve ser configurado corretamente.

Este tutorial percorre as etapas necessárias para criar um conjunto de dados que pode ser usado para exportar um segmento de audiência usando a [!DNL Experience Platform] interface do usuário.

Este tutorial está diretamente relacionado às etapas descritas no tutorial para [avaliar e acessar os resultados](./evaluate-a-segment.md)do segmento. O tutorial de avaliação de um segmento fornece etapas para a criação de um conjunto de dados usando a [!DNL Catalog Service] API, enquanto este tutorial descreve as etapas para criar um conjunto de dados usando a [!DNL Experience Platform] interface do usuário.

## Introdução

Para exportar um segmento, o conjunto de dados deve ser baseado no [!DNL XDM Individual Profile Union Schema]. Um schema de união é um schema gerado pelo sistema e somente leitura que agregação os campos de todos os schemas que compartilham a mesma classe, neste caso, que é a [!DNL XDM Individual Profile] classe. Para obter mais informações sobre schemas de visualização de união, consulte a seção Perfil do cliente em tempo [real do guia](../../xdm/schema/composition.md#union)do desenvolvedor do Registro de Schemas.

Para visualização de schemas de união na interface do usuário, clique em **[!UICONTROL Perfis]** na navegação à esquerda e clique na guia schema **[!UICONTROL de]** União, como mostrado abaixo.

![Guia schema de união na interface do usuário do Experience Platform](../images/tutorials/segment-export-dataset/union-schema-ui.png)


## Área de trabalho de conjuntos de dados

A área de trabalho dos conjuntos de dados na [!DNL Experience Platform] interface do usuário permite que você visualização e gerencie todos os conjuntos de dados criados pela organização do IMS, bem como criar novos conjuntos.

Para visualização da área de trabalho dos conjuntos de dados, clique em **[!UICONTROL Conjuntos]** de dados na navegação à esquerda e, em seguida, clique na guia **[!UICONTROL Procurar]** . A área de trabalho dos conjuntos de dados contém uma lista de conjuntos de dados, incluindo colunas que mostram **[!UICONTROL Nome]**, **[!UICONTROL Criado]** (data e hora), **[!UICONTROL Origem]**, **[!UICONTROL Schema]** e Status **[!UICONTROL do]******&#x200B;Último Lote, bem como a data e a hora em que o conjunto de dados foi Última Atualização. Dependendo da largura de cada coluna, talvez seja necessário rolar para a esquerda ou para a direita para ver todas as colunas.

>[!NOTE]
>
>Clique no ícone de filtro ao lado da barra de pesquisa para usar os recursos de filtragem para visualização somente dos conjuntos de dados habilitados para [!DNL Real-time Customer Profile].

![Visualização de todos os conjuntos de dados](../images/tutorials/segment-export-dataset/datasets-workspace.png)

## Criar um conjunto de dados

Para criar um conjunto de dados, clique em **[!UICONTROL Criar conjunto]** de dados no canto superior direito da área de trabalho [!UICONTROL Conjuntos] de dados.

![Clique em Criar conjunto de dados](../images/tutorials/segment-export-dataset/dataset-click-create.png)

Na tela **[!UICONTROL Criar conjunto de dados]** , clique em **[!UICONTROL Criar conjunto de dados do Schema]** para continuar.

![Selecionar fonte de dados](../images/tutorials/segment-export-dataset/create-dataset.png)

## Selecionar Schema de União de Perfil individual XDM

Para selecionar o Perfil a ser usado no conjunto de dados, localize o schema &quot; [!DNL XDM Individual Profile Union Schema] individual[!UICONTROL XDM&quot; com um tipo de &quot;]União[!UICONTROL &quot; na tela]Selecionar Schema **** .

Selecionado o botão de opção ao lado de Perfil **[!UICONTROL individual]** XDM e, em seguida, clique em **[!UICONTROL Avançar]** no canto superior direito.

![Selecionar schema](../images/tutorials/segment-export-dataset/select-schema.png)

## Configurar conjunto de dados

Na tela **[!UICONTROL Configurar conjunto de dados]** , será necessário fornecer um **[!UICONTROL Nome]** ao conjunto de dados e também uma **[!UICONTROL Descrição]** do conjunto de dados.

**Notas sobre os nomes dos conjuntos de dados:**
- Os nomes dos conjuntos de dados devem ser curtos e descritivos para que o conjunto de dados possa ser facilmente encontrado na biblioteca posteriormente.
- Os nomes dos conjuntos de dados devem ser exclusivos, o que significa que também devem ser específicos o suficiente para que não sejam reutilizados no futuro.
- É prática recomendada fornecer informações adicionais sobre o conjunto de dados usando o campo de descrição, pois pode ajudar outros usuários a diferenciarem entre conjuntos de dados no futuro.

Depois que o conjunto de dados tiver um nome e uma descrição, clique em **[!UICONTROL Concluir]**.

![Configurar conjunto de dados](../images/tutorials/segment-export-dataset/configure-dataset.png)

## Atividade do conjunto de dados

Um conjunto de dados vazio foi criado e você foi retornado para a guia Atividade **** Conjunto de dados na área de trabalho [!UICONTROL Conjuntos] de dados. Você deve ver o nome do conjunto de dados no canto superior esquerdo do espaço de trabalho, juntamente com uma notificação de que &quot;Nenhum lote foi adicionado.&quot; Isso é esperado, pois você ainda não adicionou nenhum lote a esse conjunto de dados.

No lado direito da área de trabalho dos Conjuntos de dados, você verá a guia **[!UICONTROL Informações]** contendo informações relacionadas ao seu novo conjunto de dados, como ID **[!UICONTROL do]** Conjunto de dados, **[!UICONTROL Nome]**, **[!UICONTROL Descrição]**, Nome **[!UICONTROL da]************** tabela, Schema, Streaming eSource. A guia [!UICONTROL Informações] também inclui informações sobre quando o conjunto de dados foi **[!UICONTROL criado]** e sua data de **[!UICONTROL última modificação]** .

Anote a ID **[!UICONTROL do]** conjunto de dados, pois esse valor é necessário para concluir o fluxo de trabalho de exportação do segmento de audiência.

![Atividade do conjunto de dados](../images/tutorials/segment-export-dataset/dataset-activity.png)

## Próximas etapas

Agora que você criou um conjunto de dados com base no [!DNL XDM Individual Profile Union Schema], é possível usar a ID **[!UICONTROL do]** conjunto de dados para continuar o tutorial de [avaliação e acesso aos resultados](./evaluate-a-segment.md) do segmento.

Neste momento, volte ao tutorial de resultados do segmento de avaliação e pegue na etapa de [geração de perfis para membros](./evaluate-a-segment.md#generate-profiles) da audiência de exportar um fluxo de trabalho de segmento.
