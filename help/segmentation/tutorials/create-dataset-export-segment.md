---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Criar um conjunto de dados para exportar um segmento de audiência
topic: tutorial
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '766'
ht-degree: 0%

---


# Criar um conjunto de dados para exportar um segmento de audiência

O Adobe Experience Platform permite segmentar facilmente perfis de clientes em audiências com base em atributos específicos. Depois que os segmentos forem criados, você poderá exportar essa audiência para um conjunto de dados no qual ela possa ser acessada e executada. Para que a exportação seja bem-sucedida, o conjunto de dados deve ser configurado corretamente.

Este tutorial percorre as etapas necessárias para criar um conjunto de dados que pode ser usado para exportar um segmento de audiência usando a interface do usuário do Experience Platform.

Este tutorial está diretamente relacionado às etapas descritas no tutorial para [avaliar e acessar os resultados](./evaluate-a-segment.md)do segmento. O tutorial de avaliação de um segmento fornece etapas para a criação de um conjunto de dados usando a API de catálogo, enquanto este tutorial descreve as etapas para criar um conjunto de dados usando a interface do usuário do Experience Platform.

## Introdução

Para exportar um segmento, o conjunto de dados deve ser baseado no Schema de União de Perfil individual do XDM. Um schema união é um schema gerado pelo sistema e somente leitura que agregação os campos de todos os schemas que compartilham a mesma classe, neste caso, que é a classe de Perfil Individual XDM. Para obter mais informações sobre schemas de visualização de união, consulte a seção Perfil do cliente em tempo [real do guia](../../xdm/schema/composition.md#union)do desenvolvedor do Registro de Schemas.

Para visualização de schemas de união na interface do usuário, clique em **Perfis** na navegação à esquerda e clique na guia schema *de* União, como mostrado abaixo.

![Guia schema de União na interface do usuário do Experience Platform](../images/tutorials/segment-export-dataset/union-schema-ui.png)


## Área de trabalho de conjuntos de dados

A área de trabalho dos conjuntos de dados na interface do Experience Platform permite que você visualização e gerencie todos os conjuntos de dados criados pela organização do IMS, bem como criar novos.

Para visualização da área de trabalho dos conjuntos de dados, clique em **Conjuntos** de dados na navegação à esquerda e, em seguida, clique na guia *Procurar* . A área de trabalho dos conjuntos de dados contém uma lista de conjuntos de dados, incluindo colunas que mostram *Nome*, *Criado* (data e hora), *Origem*, *Schema* e Status *do***&#x200B;Último Lote, bem como a data e a hora em que o conjunto de dados foi Última Atualização. Dependendo da largura de cada coluna, talvez seja necessário rolar para a esquerda ou para a direita para ver todas as colunas.

>[!NOTE]
>
>Clique no ícone de filtro ao lado da barra de pesquisa para usar os recursos de filtragem para visualização somente dos conjuntos de dados habilitados para o Perfil do cliente em tempo real.

![Visualização de todos os conjuntos de dados](../images/tutorials/segment-export-dataset/datasets-workspace.png)

## Criar um conjunto de dados

Para criar um conjunto de dados, clique em **Criar conjunto** de dados no canto superior direito da área de trabalho Conjuntos de dados.

![Clique em Criar conjunto de dados](../images/tutorials/segment-export-dataset/dataset-click-create.png)

Na tela *Criar conjunto de dados* , clique em **Criar conjunto de dados do Schema** para continuar.

![Selecionar fonte de dados](../images/tutorials/segment-export-dataset/create-dataset.png)

## Selecionar Schema de União de Perfil individual XDM

Para selecionar o Schema de União individual do Perfil XDM para uso em seu conjunto de dados, localize o schema &quot;Perfil individual XDM&quot; com um tipo de &quot;União&quot; na tela *Selecionar Schema* .

Selecionado o botão de opção ao lado de Perfil **individual** XDM e, em seguida, clique em **Avançar** no canto superior direito.

![Selecionar schema](../images/tutorials/segment-export-dataset/select-schema.png)

## Configurar conjunto de dados

Na tela **Configurar conjunto de dados** , será necessário fornecer um *Nome* ao conjunto de dados e também uma *Descrição* do conjunto de dados.

**Notas sobre os nomes dos conjuntos de dados:**
- Os nomes dos conjuntos de dados devem ser curtos e descritivos para que o conjunto de dados possa ser facilmente encontrado na biblioteca posteriormente.
- Os nomes dos conjuntos de dados devem ser exclusivos, o que significa que também devem ser específicos o suficiente para que não sejam reutilizados no futuro.
- É prática recomendada fornecer informações adicionais sobre o conjunto de dados usando o campo de descrição, pois pode ajudar outros usuários a diferenciarem entre conjuntos de dados no futuro.

Depois que o conjunto de dados tiver um nome e uma descrição, clique em **Concluir**.

![Configurar conjunto de dados](../images/tutorials/segment-export-dataset/configure-dataset.png)

## atividade do conjunto de dados

Um conjunto de dados vazio foi criado e você foi retornado para a guia Atividade ** Conjunto de dados na área de trabalho Conjuntos de dados. Você deve ver o nome do conjunto de dados no canto superior esquerdo do espaço de trabalho, juntamente com uma notificação de que &quot;Nenhum lote foi adicionado.&quot; Isso é esperado, pois você ainda não adicionou nenhum lote a esse conjunto de dados.

No lado direito da área de trabalho dos Conjuntos de dados, você verá a guia **Informações** contendo informações relacionadas ao seu novo conjunto de dados, como ID *do* Conjunto de dados, *Nome*, *Descrição*, Nome *da******* tabela, Schema, Streaming eSource. A guia Informações também inclui informações sobre quando o conjunto de dados foi *criado* e sua data de *Última modificação* .

Anote a ID **do** conjunto de dados, pois esse valor é necessário para concluir o fluxo de trabalho de exportação do segmento de audiência.

![atividade do conjunto de dados](../images/tutorials/segment-export-dataset/dataset-activity.png)

## Próximas etapas

Agora que você criou um conjunto de dados com base no Schema de União de Perfil individual do XDM, é possível usar a ID **do** conjunto de dados para continuar a [avaliação e o acesso ao tutorial de resultados](./evaluate-a-segment.md) do segmento.

No momento, volte ao tutorial de resultados do segmento de avaliação e pegue na etapa [Gerar Perfis individuais XDM para membros](./evaluate-a-segment.md#generate-profiles-for-audience-members) da audiência da etapa de [exportação de um fluxo de trabalho de segmento](./evaluate-a-segment.md#export-a-segment) .
