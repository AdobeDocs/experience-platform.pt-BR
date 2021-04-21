---
keywords: Experience Platform, home, tópicos populares, Serviço de segmentação, segmentação, Segmentação, criar um conjunto de dados, exportar segmento do público-alvo, exportar segmento;
solution: Experience Platform
title: Criar um conjunto de dados para exportar um segmento de público-alvo
topic-legacy: tutorial
type: Tutorial
description: Este tutorial percorre as etapas necessárias para criar um conjunto de dados que pode ser usado para exportar um segmento de público-alvo usando a interface do usuário do Experience Platform.
exl-id: 1cd16e43-b050-42ba-a894-d7ea477b65f3
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '739'
ht-degree: 1%

---

# Criar um conjunto de dados para exportar um segmento de público-alvo

[!DNL Adobe Experience Platform] O permite segmentar facilmente os perfis do cliente em públicos-alvo com base em atributos específicos. Após criar os segmentos, é possível exportar esse público para um conjunto de dados, onde ele pode ser acessado e aplicado. Para que a exportação seja bem-sucedida, o conjunto de dados deve ser configurado corretamente.

Este tutorial percorre as etapas necessárias para criar um conjunto de dados que pode ser usado para exportar um segmento de público-alvo usando a interface [!DNL Experience Platform].

Este tutorial está diretamente relacionado às etapas descritas no tutorial para [avaliar e acessar os resultados do segmento](./evaluate-a-segment.md). O tutorial de avaliação de um segmento fornece etapas para a criação de um conjunto de dados usando a API [!DNL Catalog Service], enquanto este tutorial descreve etapas para criar um conjunto de dados usando a interface [!DNL Experience Platform].

## Introdução

Para exportar um segmento, o conjunto de dados deve ser baseado no [!DNL XDM Individual Profile Union Schema]. Um schema de união é um schema gerado pelo sistema e somente leitura que agrega os campos de todos os schemas que compartilham a mesma classe, neste caso, que é a classe [!DNL XDM Individual Profile]. Para obter mais informações sobre schemas de exibição de união, consulte a seção [Real-time Customer Profile do Schema Registry developer guide](../../xdm/schema/composition.md#union).

Para exibir esquemas de união na interface do usuário, clique em **[!UICONTROL Profiles]** na navegação à esquerda e, em seguida, clique na guia **[!UICONTROL Union schema]** , conforme mostrado abaixo.

![Guia Union schema na interface do usuário do Experience Platform](../images/tutorials/segment-export-dataset/union-schema-ui.png)


## Espaço de trabalho Conjuntos de dados

A área de trabalho dos conjuntos de dados na interface do usuário [!DNL Experience Platform] permite visualizar e gerenciar todos os conjuntos de dados que sua organização IMS fez, bem como criar novos conjuntos.

Para exibir o espaço de trabalho dos conjuntos de dados, clique em **[!UICONTROL Datasets]** na navegação à esquerda e, em seguida, clique na guia **[!UICONTROL Browse]** . O espaço de trabalho de conjuntos de dados contém uma lista de conjuntos de dados, incluindo colunas que mostram o nome, a data e a hora criadas, a origem, o esquema e o status do último lote, bem como a data e a hora em que o conjunto de dados foi atualizado pela última vez. Dependendo da largura de cada coluna, talvez seja necessário rolar a tela para a esquerda ou para a direita para ver todas as colunas.

>[!NOTE]
>
>Clique no ícone de filtro ao lado da barra de pesquisa para usar os recursos de filtragem para exibir apenas os conjuntos de dados habilitados para [!DNL Real-time Customer Profile].

![Exibir todos os conjuntos de dados](../images/tutorials/segment-export-dataset/datasets-workspace.png)

## Criar um conjunto de dados

Para criar um conjunto de dados, clique em **[!UICONTROL Create Dataset]** no canto superior direito do espaço de trabalho **[!UICONTROL Datasets]**.

![Clique em Criar conjunto de dados](../images/tutorials/segment-export-dataset/dataset-click-create.png)

Na tela **[!UICONTROL Create Dataset]**, clique em **[!UICONTROL Create Dataset from Schema]** para continuar.

![Selecionar fonte de dados](../images/tutorials/segment-export-dataset/create-dataset.png)

## Selecionar Esquema de União de Perfil Individual XDM

Para selecionar o [!DNL XDM Individual Profile Union Schema] para usar em seu conjunto de dados, encontre o schema &quot;[!UICONTROL XDM Individual Profile]&quot; com um tipo de &quot;[!UICONTROL Union]&quot; na tela **[!UICONTROL Select Schema]**.

Selecionado o botão de opção ao lado de **[!UICONTROL XDM Individual Profile]**, em seguida, clique em **[!UICONTROL Next]** no canto superior direito.

![Selecionar esquema](../images/tutorials/segment-export-dataset/select-schema.png)

## Configurar conjunto de dados

Na tela **[!UICONTROL Configure Dataset]**, será necessário fornecer um nome ao conjunto de dados e também pode fornecer uma descrição do conjunto de dados.

**Notas sobre os nomes dos conjuntos de dados:**
- Os nomes dos conjuntos de dados devem ser curtos e descritivos para que o conjunto de dados possa ser facilmente encontrado na biblioteca posteriormente.
- Os nomes do conjunto de dados devem ser exclusivos, o que significa que também devem ser específicos o suficiente para que não sejam reutilizados no futuro.
- É uma prática recomendada fornecer informações adicionais sobre o conjunto de dados usando o campo de descrição, pois pode ajudar outros usuários a diferenciar os conjuntos de dados no futuro.

Depois que o conjunto de dados tiver um nome e uma descrição, clique em **[!UICONTROL Finish]**.

![Configurar conjunto de dados](../images/tutorials/segment-export-dataset/configure-dataset.png)

## Atividade do conjunto de dados

Um conjunto de dados vazio foi criado e você foi retornado à guia **[!UICONTROL Dataset Activity]** no espaço de trabalho **[!UICONTROL Datasets]**. Você deve ver o nome do conjunto de dados no canto superior esquerdo do espaço de trabalho, juntamente com uma notificação de que &quot;Nenhum lote foi adicionado&quot;. Isso é esperado, pois você ainda não adicionou nenhum lote a esse conjunto de dados.

No lado direito do espaço de trabalho Conjuntos de dados, você verá a guia **[!UICONTROL Info]** contendo informações relacionadas ao novo conjunto de dados, como ID do conjunto de dados, nome, descrição, nome da tabela, esquema, transmissão e origem. A guia **[!UICONTROL Info]** também inclui informações sobre quando o conjunto de dados foi criado e sua última data de modificação.

Anote o **[!UICONTROL Dataset ID]**, pois esse valor é necessário para concluir o fluxo de trabalho de exportação do segmento de público-alvo.

![Atividade do conjunto de dados](../images/tutorials/segment-export-dataset/dataset-activity.png)

## Próximas etapas

Agora que você criou um conjunto de dados com base em [!DNL XDM Individual Profile Union Schema], é possível usar a ID do conjunto de dados para continuar o tutorial [avaliar e acessar os resultados do segmento](./evaluate-a-segment.md).

No momento, retorne ao tutorial de resultados do segmento de avaliação e escolha na etapa [gerar perfis para membros do público-alvo](./evaluate-a-segment.md#generate-profiles) do fluxo de trabalho de exportação de segmento.
