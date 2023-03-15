---
keywords: Experience Platform;página inicial;tópicos populares;Serviço de segmentação;segmentação;segmentação;criar um conjunto de dados;exportar segmento de público;exportar segmento;
solution: Experience Platform
title: Criar um conjunto de dados para exportar um segmento de público-alvo
type: Tutorial
description: Este tutorial aborda as etapas necessárias para criar um conjunto de dados que pode ser usado para exportar um segmento de público-alvo usando a interface do usuário do Experience Platform.
exl-id: 1cd16e43-b050-42ba-a894-d7ea477b65f3
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '757'
ht-degree: 0%

---

# Criar um conjunto de dados para exportar um segmento de público

[!DNL Adobe Experience Platform] O permite segmentar perfis de clientes em públicos com base em atributos específicos. Depois que um segmento é criado, você pode exportar esse público-alvo para um conjunto de dados em que ele possa ser acessado e aplicado. Para que a exportação seja bem-sucedida, o conjunto de dados deve ser configurado corretamente.

Este tutorial aborda as etapas necessárias para criar um conjunto de dados que pode ser usado para exportar um segmento de público-alvo usando o [!DNL Experience Platform] IU.

Este tutorial está diretamente relacionado às etapas descritas no tutorial em [avaliação e acesso aos resultados do segmento](./evaluate-a-segment.md). O tutorial de avaliação de segmento fornece etapas para a criação de um conjunto de dados usando o [!DNL Catalog Service] , enquanto este tutorial descreve as etapas para criar um conjunto de dados usando o [!DNL Experience Platform] IU.

## Introdução

Para exportar um segmento, o conjunto de dados deve ser baseado na variável [!DNL XDM Individual Profile Union Schema]. Um esquema de união é um esquema somente leitura gerado pelo sistema que agrega os campos de todos os esquemas que compartilham a mesma classe. Para obter mais informações sobre schemas de união, consulte o guia em [as noções básicas da composição do esquema](../../xdm/schema/composition.md#union).

Para exibir esquemas de união na interface do usuário, selecione **[!UICONTROL Perfis]** no painel de navegação esquerdo, selecione **[!UICONTROL Esquema de união]** conforme mostrado abaixo.

![A guia Esquema de união é realçada.](../images/tutorials/segment-export-dataset/union.png)

## Espaço de trabalho de conjuntos de dados

A variável [!UICONTROL Conjuntos de dados] o espaço de trabalho permite exibir e gerenciar todos os conjuntos de dados da sua organização.

Selecionar **[!UICONTROL Conjuntos de dados]** na navegação à esquerda para acessar o espaço de trabalho, selecione **[!UICONTROL Procurar]**. Essa guia exibe uma lista de conjuntos de dados e seus detalhes. Dependendo da largura de cada coluna, talvez seja necessário rolar a tela para a esquerda ou para a direita para ver todas as colunas.

>[!NOTE]
>
>Selecione o ícone de filtro ao lado da barra de pesquisa para usar os recursos de filtragem para exibir apenas os conjuntos de dados habilitados para [!DNL Real-Time Customer Profile].

![O espaço de trabalho dos conjuntos de dados é exibido.](../images/tutorials/segment-export-dataset/browse.png)

## Criar um conjunto de dados

Para criar um conjunto de dados, selecione **[!UICONTROL Criar conjunto de dados]**.

![O botão Criar conjunto de dados é realçado.](../images/tutorials/segment-export-dataset/create-dataset.png)

Na tela seguinte, selecione **[!UICONTROL Criar conjunto de dados a partir do esquema]**.

![A opção Criar conjunto de dados a partir do esquema é realçada.](../images/tutorials/segment-export-dataset/create-from-schema.png)

## Selecionar esquema de união do perfil individual XDM

Para selecionar o [!DNL XDM Individual Profile Union Schema] para uso no conjunto de dados, localize o &quot;[!UICONTROL Perfil individual XDM]&quot;esquema&quot; no **[!UICONTROL Selecionar esquema]** tela. Depois de selecionar o esquema, você pode confirmar se é o esquema de união em **[!UICONTROL Uso da API]** no painel direito. Se a variável [!UICONTROL Esquema] o caminho termina com `_union`, é um esquema de união.

>[!NOTE]
>
>Embora os esquemas de união participem do Perfil de cliente em tempo real por definição, eles são listados como &quot;Não ativado&quot; devido ao fato de que não estão ativados para Perfil da mesma forma que os esquemas tradicionais.

Selecione o botão de opção ao lado de **[!UICONTROL Perfil individual XDM]** e selecione **[!UICONTROL Próxima]**.

![O esquema do Perfil individual XDM é realçado.](../images/tutorials/segment-export-dataset/select-schema.png)

## Configurar conjunto de dados

Na próxima tela, você deve dar um nome ao conjunto de dados. Você também pode adicionar uma descrição opcional.

**Observações sobre os nomes dos conjuntos de dados:**

* Os nomes dos conjuntos de dados devem ser curtos e descritivos para que possam ser facilmente encontrados na biblioteca posteriormente.
* Os nomes dos conjuntos de dados devem ser exclusivos, o que significa que eles também devem ser específicos o suficiente para não serem reutilizados no futuro.
* É uma prática recomendada fornecer informações adicionais sobre o conjunto de dados usando o campo de descrição, pois pode ajudar outros usuários a diferenciar entre conjuntos de dados no futuro.

Depois que o conjunto de dados tiver um nome e uma descrição, selecione **[!UICONTROL Concluir]**.

![A página Configurar conjunto de dados é exibida. As opções de configuração são realçadas.](../images/tutorials/segment-export-dataset/configure-dataset.png)

## Atividade do conjunto de dados

Depois que o conjunto de dados é criado, você acessa a página de atividade desse conjunto de dados. Você deve ver o nome do conjunto de dados no canto superior esquerdo do espaço de trabalho, juntamente com uma notificação de que &quot;Nenhum lote foi adicionado&quot;. Isso é esperado, pois você ainda não adicionou lotes a esse conjunto de dados.

O painel direito contém informações relacionadas ao novo conjunto de dados, como ID do conjunto de dados, nome, descrição, esquema e muito mais. Anote a **[!UICONTROL ID do conjunto de dados]**, pois esse valor é necessário para concluir o fluxo de trabalho de exportação do segmento de público-alvo.

![A página de atividade do conjunto de dados é exibida. A ID do conjunto de dados é destacada, pois esse valor precisa ser anotado para etapas futuras.](../images/tutorials/segment-export-dataset/activity.png)

## Próximas etapas

Agora que você criou um conjunto de dados com base na variável [!DNL XDM Individual Profile Union Schema], você pode usar a ID do conjunto de dados para continuar a [avaliação e acesso aos resultados do segmento](./evaluate-a-segment.md) tutorial.

Nesse momento, retorne ao tutorial de avaliação de resultados do segmento e selecione no [geração de perfis para membros do público](./evaluate-a-segment.md#generate-profiles) etapa do fluxo de trabalho exportar um segmento.
