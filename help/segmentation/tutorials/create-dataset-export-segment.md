---
keywords: Experience Platform;home;popular topics;Serviço de segmentação;segmentação;segmentação;criar um conjunto de dados;exportar segmento de audiência;exportar segmento;
solution: Experience Platform
title: Criar um conjunto de dados para exportar um segmento de Audiência
topic: tutorial
type: Tutorial
description: Este tutorial percorre as etapas necessárias para criar um conjunto de dados que pode ser usado para exportar um segmento de audiência usando a interface do usuário do Experience Platform.
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 1%

---


# Criar um conjunto de dados para exportar um segmento de audiência

[!DNL Adobe Experience Platform] permite segmentar facilmente perfis de clientes em audiências com base em atributos específicos. Depois que os segmentos forem criados, você poderá exportar essa audiência para um conjunto de dados no qual ela possa ser acessada e executada. Para que a exportação seja bem-sucedida, o conjunto de dados deve ser configurado corretamente.

Este tutorial percorre as etapas necessárias para criar um conjunto de dados que pode ser usado para exportar um segmento de audiência usando a interface do usuário [!DNL Experience Platform].

Este tutorial está diretamente relacionado às etapas descritas no tutorial para [avaliar e acessar os resultados do segmento](./evaluate-a-segment.md). O tutorial de avaliação de um segmento fornece etapas para a criação de um conjunto de dados usando a API [!DNL Catalog Service], enquanto este tutorial descreve as etapas para criar um conjunto de dados usando a interface do usuário [!DNL Experience Platform].

## Introdução

Para exportar um segmento, o conjunto de dados deve ser baseado em [!DNL XDM Individual Profile Union Schema]. Um schema de união é um schema gerado pelo sistema e somente leitura que agregação os campos de todos os schemas que compartilham a mesma classe, neste caso a classe [!DNL XDM Individual Profile]. Para obter mais informações sobre schemas de visualização de união, consulte a seção [Perfil do cliente em tempo real do guia do desenvolvedor do Registro do Schema](../../xdm/schema/composition.md#union).

Para visualização de schemas de união na interface do usuário, clique em **[!UICONTROL Perfis]** no menu de navegação esquerdo e clique na guia **[!UICONTROL schema]** como mostrado abaixo.

![Guia schema de união na interface do usuário do Experience Platform](../images/tutorials/segment-export-dataset/union-schema-ui.png)


## Área de trabalho de conjuntos de dados

A área de trabalho dos conjuntos de dados na interface do usuário [!DNL Experience Platform] permite que você visualização e gerencie todos os conjuntos de dados criados pela organização IMS, bem como criar novos conjuntos.

Para visualização da área de trabalho dos conjuntos de dados, clique em **[!UICONTROL Conjuntos de dados]** na navegação à esquerda e, em seguida, clique na guia **[!UICONTROL Procurar]**. A área de trabalho dos conjuntos de dados contém uma lista de conjuntos de dados, incluindo colunas que mostram o nome, a data e a hora, a origem, o schema e o status do último lote, bem como a data e a hora em que o conjunto de dados foi atualizado pela última vez. Dependendo da largura de cada coluna, talvez seja necessário rolar para a esquerda ou para a direita para ver todas as colunas.

>[!NOTE]
>
>Clique no ícone de filtro ao lado da barra de pesquisa para usar os recursos de filtragem para visualização somente dos conjuntos de dados habilitados para [!DNL Real-time Customer Profile].

![Visualização de todos os conjuntos de dados](../images/tutorials/segment-export-dataset/datasets-workspace.png)

## Criar um conjunto de dados

Para criar um conjunto de dados, clique em **[!UICONTROL Criar conjunto de dados]** no canto superior direito da área de trabalho **[!UICONTROL Conjuntos de dados]**.

![Clique em Criar conjunto de dados](../images/tutorials/segment-export-dataset/dataset-click-create.png)

Na tela **[!UICONTROL Criar conjunto de dados]**, clique em **[!UICONTROL Criar conjunto de dados a partir do Schema]** para continuar.

![Selecionar fonte de dados](../images/tutorials/segment-export-dataset/create-dataset.png)

## Selecionar Schema de União de Perfil individual XDM

Para selecionar [!DNL XDM Individual Profile Union Schema] para usar no conjunto de dados, localize o schema &quot;[!UICONTROL Perfil Individual XDM]&quot; com um tipo de &quot;[!UICONTROL União]&quot; na tela **[!UICONTROL Selecionar Schema]**.

Selecionado o botão de opção ao lado de **[!UICONTROL Perfil individual XDM]**, em seguida, clique em **[!UICONTROL Próximo]** no canto superior direito.

![Selecionar schema](../images/tutorials/segment-export-dataset/select-schema.png)

## Configurar conjunto de dados

Na tela **[!UICONTROL Configurar conjunto de dados]**, você deverá fornecer um nome ao conjunto de dados e também poderá fornecer uma descrição do conjunto de dados.

**Notas sobre os nomes dos conjuntos de dados:**
- Os nomes dos conjuntos de dados devem ser curtos e descritivos para que o conjunto de dados possa ser facilmente encontrado na biblioteca posteriormente.
- Os nomes dos conjuntos de dados devem ser exclusivos, o que significa que também devem ser específicos o suficiente para que não sejam reutilizados no futuro.
- É prática recomendada fornecer informações adicionais sobre o conjunto de dados usando o campo de descrição, pois pode ajudar outros usuários a diferenciarem entre conjuntos de dados no futuro.

Depois que o conjunto de dados tiver um nome e uma descrição, clique em **[!UICONTROL Concluir]**.

![Configurar conjunto de dados](../images/tutorials/segment-export-dataset/configure-dataset.png)

## Atividade do conjunto de dados

Um conjunto de dados vazio foi criado e você foi retornado para a guia **[!UICONTROL Atividade de conjunto de dados]** na área de trabalho **[!UICONTROL Conjuntos de dados]**. Você deve ver o nome do conjunto de dados no canto superior esquerdo do espaço de trabalho, juntamente com uma notificação de que &quot;Nenhum lote foi adicionado.&quot; Isso é esperado, pois você ainda não adicionou nenhum lote a esse conjunto de dados.

No lado direito da área de trabalho dos conjuntos de dados, você verá a guia **[!UICONTROL Info]** contendo informações relacionadas ao seu novo conjunto de dados, como ID do conjunto de dados, nome, descrição, nome da tabela, schema, transmissão e origem. A guia **[!UICONTROL Info]** também inclui informações sobre quando o conjunto de dados foi criado e sua última data de modificação.

Anote a **[!UICONTROL ID do conjunto de dados]**, pois esse valor é necessário para concluir o fluxo de trabalho de exportação do segmento de audiência.

![Atividade do conjunto de dados](../images/tutorials/segment-export-dataset/dataset-activity.png)

## Próximas etapas

Agora que você criou um conjunto de dados com base em [!DNL XDM Individual Profile Union Schema], é possível usar a ID do conjunto de dados para continuar o tutorial [avaliando e acessando os resultados do segmento](./evaluate-a-segment.md).

No momento, volte ao tutorial de resultados do segmento de avaliação e pegue na etapa [gerando perfis para membros da audiência](./evaluate-a-segment.md#generate-profiles) de exportação de um fluxo de trabalho de segmento.
