---
solution: Experience Platform
title: Criar um conjunto de dados para exportar um público
type: Tutorial
description: Saiba como criar um conjunto de dados que pode ser usado para exportar um público-alvo usando a interface do Experience Platform.
exl-id: 1cd16e43-b050-42ba-a894-d7ea477b65f3
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '732'
ht-degree: 1%

---

# Criar um conjunto de dados para exportar um público

O [!DNL Adobe Experience Platform] permite segmentar perfis de clientes em públicos com base em atributos específicos. Depois que uma definição de segmento é criada, você pode exportar o público-alvo resultante para um conjunto de dados em que ele possa ser acessado e reagido. Para que a exportação seja bem-sucedida, o conjunto de dados deve ser configurado corretamente.

Este tutorial aborda as etapas necessárias para criar um conjunto de dados que pode ser usado para exportar um público usando a interface do usuário do [!DNL Experience Platform].

Este tutorial está diretamente relacionado às etapas descritas no tutorial sobre [avaliação e acesso aos resultados da segmentação](./evaluate-a-segment.md). O tutorial de avaliação da definição de segmento fornece etapas para a criação de um conjunto de dados usando a API [!DNL Catalog Service], enquanto este tutorial descreve etapas para a criação de um conjunto de dados usando a interface do usuário [!DNL Experience Platform].

## Introdução

Para exportar um público-alvo, o conjunto de dados deve ser baseado no [!DNL XDM Individual Profile Union Schema]. Um esquema de união é um esquema somente leitura gerado pelo sistema que agrega os campos de todos os esquemas que compartilham a mesma classe. Para obter mais informações sobre esquemas de união, consulte o manual sobre [as noções básicas da composição de esquema](../../xdm/schema/composition.md#union).

Para exibir esquemas de união na interface do usuário, selecione **[!UICONTROL Perfis]** na navegação à esquerda e selecione **[!UICONTROL Esquema de união]** conforme mostrado abaixo.

![A guia de esquema de união está realçada.](../images/tutorials/segment-export-dataset/union.png)

## Espaço de trabalho de conjuntos de dados

O espaço de trabalho [!UICONTROL Conjuntos de Dados] permite exibir e gerenciar todos os conjuntos de dados da sua organização.

Selecione **[!UICONTROL Conjuntos de Dados]** na navegação à esquerda para acessar o espaço de trabalho e selecione **[!UICONTROL Procurar]**. Essa guia exibe uma lista de conjuntos de dados e seus detalhes. Dependendo da largura de cada coluna, talvez seja necessário rolar a tela para a esquerda ou para a direita para ver todas as colunas.

>[!NOTE]
>
>Selecione o ícone de filtro ao lado da barra de pesquisa para usar os recursos de filtragem para exibir apenas os conjuntos de dados habilitados para [!DNL Real-Time Customer Profile].

![O espaço de trabalho dos conjuntos de dados é exibido.](../images/tutorials/segment-export-dataset/browse.png)

## Criar um conjunto de dados

Para criar um conjunto de dados, selecione **[!UICONTROL Criar Conjunto de Dados]**.

![O botão Criar conjunto de dados está realçado.](../images/tutorials/segment-export-dataset/create-dataset.png)

Na próxima tela, selecione **[!UICONTROL Criar Conjunto de Dados do Esquema]**.

![A opção Criar conjunto de dados a partir do esquema está realçada.](../images/tutorials/segment-export-dataset/create-from-schema.png)

## Selecionar esquema de união do perfil individual XDM

Para selecionar o [!DNL XDM Individual Profile Union Schema] para uso em seu conjunto de dados, localize o esquema &quot;[!UICONTROL Perfil Individual XDM]&quot; na tela **[!UICONTROL Selecionar Esquema]**. Após selecionar o esquema, você pode confirmar se ele é o esquema de união em **[!UICONTROL Uso da API]** no painel direito. Se o caminho [!UICONTROL Esquema] termina com `_union`, ele é um esquema de união.

>[!NOTE]
>
>Embora os esquemas de união participem do Perfil de cliente em tempo real por definição, eles são listados como &quot;Não ativado&quot; devido ao fato de que não estão ativados para Perfil da mesma forma que os esquemas tradicionais.

Selecione o botão de opção ao lado de **[!UICONTROL Perfil Individual XDM]** e selecione **[!UICONTROL Avançar]**.

![O esquema do Perfil Individual XDM está realçado.](../images/tutorials/segment-export-dataset/select-schema.png)

## Configurar conjunto de dados

Na próxima tela, você deve dar um nome ao conjunto de dados. Você também pode adicionar uma descrição opcional.

**Observações sobre nomes de conjunto de dados:**

* Os nomes dos conjuntos de dados devem ser curtos e descritivos para que possam ser facilmente encontrados na biblioteca posteriormente.
* Os nomes dos conjuntos de dados devem ser exclusivos, o que significa que eles também devem ser específicos o suficiente para não serem reutilizados no futuro.
* Você deve fornecer informações adicionais sobre o conjunto de dados usando o campo de descrição, pois pode ajudar outros usuários a diferenciar entre conjuntos de dados no futuro.

Depois que o conjunto de dados tiver um nome e uma descrição, selecione **[!UICONTROL Concluir]**.

![A página Configurar conjunto de dados é exibida. As opções de configuração estão realçadas.](../images/tutorials/segment-export-dataset/configure-dataset.png)

## Atividade do conjunto de dados

Depois que o conjunto de dados é criado, você acessa a página de atividade desse conjunto de dados. Você deve ver o nome do conjunto de dados no canto superior esquerdo do espaço de trabalho, juntamente com uma notificação de que &quot;Nenhum lote foi adicionado&quot;. Isso é esperado, pois você ainda não adicionou lotes a esse conjunto de dados.

O painel direito contém informações relacionadas ao novo conjunto de dados, como ID do conjunto de dados, nome, descrição, esquema e muito mais. Anote a **[!UICONTROL ID do conjunto de dados]**, pois esse valor é necessário para concluir o fluxo de trabalho de exportação de público-alvo.

![A página de atividade do conjunto de dados é exibida. A ID do conjunto de dados é destacada, pois esse valor precisa ser anotado para etapas futuras.](../images/tutorials/segment-export-dataset/activity.png)

## Próximas etapas

Agora que você criou um conjunto de dados com base no [!DNL XDM Individual Profile Union Schema], é possível usar a ID do conjunto de dados para continuar o tutorial [avaliando e acessando resultados de definição de segmento](./evaluate-a-segment.md).

Neste momento, retorne ao tutorial de avaliação dos resultados da definição de segmento e selecione na [etapa de geração de perfis para membros do público-alvo](./evaluate-a-segment.md#generate-profiles) da exportação de um fluxo de trabalho de público-alvo.
