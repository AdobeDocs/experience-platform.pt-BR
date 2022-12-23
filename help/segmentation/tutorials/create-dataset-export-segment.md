---
keywords: Experience Platform, home, tópicos populares, Serviço de segmentação, segmentação, Segmentação, criar um conjunto de dados, exportar segmento do público-alvo, exportar segmento;
solution: Experience Platform
title: Criar um conjunto de dados para exportar um segmento de público-alvo
topic-legacy: tutorial
type: Tutorial
description: Este tutorial percorre as etapas necessárias para criar um conjunto de dados que pode ser usado para exportar um segmento de público-alvo usando a interface do usuário do Experience Platform.
exl-id: 1cd16e43-b050-42ba-a894-d7ea477b65f3
source-git-commit: f7d204442c8bc2355671ba2adffff4c40ce08784
workflow-type: tm+mt
source-wordcount: '757'
ht-degree: 0%

---

# Criar um conjunto de dados para exportar um segmento de público-alvo

[!DNL Adobe Experience Platform] O permite segmentar perfis de clientes em públicos-alvo com base em atributos específicos. Depois que um segmento é criado, você pode exportar esse público para um conjunto de dados, onde ele pode ser acessado e tratado. Para que a exportação seja bem-sucedida, o conjunto de dados deve ser configurado corretamente.

Este tutorial aborda as etapas necessárias para criar um conjunto de dados que pode ser usado para exportar um segmento de público usando o [!DNL Experience Platform] IU.

Este tutorial está diretamente relacionado às etapas descritas no tutorial em [avaliação e acesso aos resultados do segmento](./evaluate-a-segment.md). O tutorial de avaliação de segmento fornece etapas para a criação de um conjunto de dados usando o [!DNL Catalog Service] API, enquanto este tutorial descreve as etapas para criar um conjunto de dados usando o [!DNL Experience Platform] IU.

## Introdução

Para exportar um segmento, o conjunto de dados deve ser baseado na variável [!DNL XDM Individual Profile Union Schema]. Um schema de união é um schema somente leitura gerado pelo sistema que agrega os campos de todos os esquemas que compartilham a mesma classe. Para obter mais informações sobre schemas de união, consulte o guia em [as noções básicas da composição do schema](../../xdm/schema/composition.md#union).

Para exibir esquemas de união na interface do usuário, selecione **[!UICONTROL Perfis]** na navegação à esquerda, selecione **[!UICONTROL Esquema de união]** conforme mostrado abaixo.

![A guia union schema é realçada.](../images/tutorials/segment-export-dataset/union.png)

## Espaço de trabalho Conjuntos de dados

O [!UICONTROL Conjuntos de dados] O workspace permite visualizar e gerenciar todos os conjuntos de dados da sua organização.

Selecionar **[!UICONTROL Conjuntos de dados]** na navegação à esquerda para acessar o espaço de trabalho, selecione **[!UICONTROL Procurar]**. Essa guia exibe uma lista de conjuntos de dados e seus detalhes. Dependendo da largura de cada coluna, talvez seja necessário rolar a tela para a esquerda ou para a direita para ver todas as colunas.

>[!NOTE]
>
>Selecione o ícone de filtro ao lado da barra de pesquisa para usar os recursos de filtragem para exibir somente os conjuntos de dados habilitados para [!DNL Real-time Customer Profile].

![O espaço de trabalho de conjuntos de dados é exibido.](../images/tutorials/segment-export-dataset/browse.png)

## Criar um conjunto de dados

Para criar um conjunto de dados, selecione **[!UICONTROL Criar conjunto de dados]**.

![O botão Criar conjunto de dados é realçado.](../images/tutorials/segment-export-dataset/create-dataset.png)

Na próxima tela, selecione **[!UICONTROL Criar conjunto de dados a partir do esquema]**.

![A opção Create dataset from schema (Criar conjunto de dados a partir do esquema) é realçada.](../images/tutorials/segment-export-dataset/create-from-schema.png)

## Selecionar Esquema de União de Perfil Individual XDM

Para selecionar o [!DNL XDM Individual Profile Union Schema] para usar em seu conjunto de dados, encontre o &quot;[!UICONTROL Perfil individual XDM]&quot; no schema **[!UICONTROL Selecionar esquema]** tela. Depois de selecionar o schema, você pode confirmar se ele é o schema de união em **[!UICONTROL Uso da API]** no painel direito. Se a variável [!UICONTROL Esquema] o caminho termina com `_union`, é um schema de união.

>[!NOTE]
>
>Apesar do fato de que os esquemas de união participam do Perfil do cliente em tempo real por definição, eles são listados como &quot;Não ativado&quot; porque não estão habilitados para o Perfil da mesma forma que os esquemas tradicionais.

Selecione o botão de opção ao lado de **[!UICONTROL Perfil individual XDM]**, em seguida selecione **[!UICONTROL Próximo]**.

![O esquema Perfil individual XDM é realçado.](../images/tutorials/segment-export-dataset/select-schema.png)

## Configurar conjunto de dados

Na próxima tela, você deve dar um nome ao seu conjunto de dados. Você também pode adicionar uma descrição opcional.

**Observações sobre os nomes dos conjuntos de dados:**

* Os nomes dos conjuntos de dados devem ser curtos e descritivos para que o conjunto de dados possa ser facilmente encontrado na biblioteca posteriormente.
* Os nomes do conjunto de dados devem ser exclusivos, o que significa que também devem ser específicos o suficiente para que não sejam reutilizados no futuro.
* É uma prática recomendada fornecer informações adicionais sobre o conjunto de dados usando o campo de descrição, pois pode ajudar outros usuários a diferenciar os conjuntos de dados no futuro.

Depois que o conjunto de dados tiver um nome e uma descrição, selecione **[!UICONTROL Concluir]**.

![A página Configurar conjunto de dados é exibida. As opções de configuração são realçadas.](../images/tutorials/segment-export-dataset/configure-dataset.png)

## Atividade do conjunto de dados

Depois que o conjunto de dados for criado, você receberá a página de atividade desse conjunto de dados. Você deve ver o nome do conjunto de dados no canto superior esquerdo do espaço de trabalho, juntamente com uma notificação de que &quot;Nenhum lote foi adicionado&quot;. Isso é esperado, pois você ainda não adicionou nenhum lote a esse conjunto de dados.

O painel direito contém informações relacionadas ao novo conjunto de dados, como ID do conjunto de dados, nome, descrição, esquema e muito mais. Por favor, anote a **[!UICONTROL ID do conjunto de dados]**, pois esse valor é necessário para concluir o fluxo de trabalho de exportação do segmento de público-alvo.

![A página de atividade do conjunto de dados é exibida. A ID do conjunto de dados é realçada, pois esse valor precisa ser anotado para etapas futuras.](../images/tutorials/segment-export-dataset/activity.png)

## Próximas etapas

Agora que você criou um conjunto de dados com base na variável [!DNL XDM Individual Profile Union Schema], você pode usar a ID do conjunto de dados para continuar o [avaliação e acesso aos resultados do segmento](./evaluate-a-segment.md) tutorial.

Nesse momento, retorne ao tutorial de resultados do segmento de avaliação e selecione [geração de perfis para membros do público-alvo](./evaluate-a-segment.md#generate-profiles) etapa do fluxo de trabalho de exportação de segmento.
