---
keywords: Experience Platform;página inicial;tópicos populares;atualizar fluxos de dados;editar programação;;home;popular topics;update dataflows;edit schedule
description: Este tutorial aborda as etapas para atualizar uma programação de fluxo de dados, incluindo a frequência de assimilação e a taxa de intervalo, usando o espaço de trabalho Origens.
solution: Experience Platform
title: Atualizar um fluxo de dados de conexão de origem na interface
type: Tutorial
exl-id: 0499a2a3-5a22-47b1-ac0e-76a432bd26c0
source-git-commit: cef5c203acf3318445399669336166e6627ebe66
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 1%

---

# Atualizar fluxos de dados na interface do

Este tutorial fornece etapas sobre como atualizar um fluxo de dados existente, incluindo sua programação e mapeamento, usando o espaço de trabalho de origens.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Origens](../../home.md): o Experience Platform permite que os dados sejam assimilados de várias fontes e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.
* [Sandboxes](../../../sandboxes/home.md): o Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

## Atualizar fluxos de dados {#update-dataflows}

>[!CONTEXTUALHELP]
>id="platform_sources_dataflows_daysRemaining"
>title="Expiração do conjunto de dados"
>abstract="Essa coluna indica o número de dias que o conjunto de dados de destino deixou antes de expirar automaticamente.<br>Um fluxo de dados falhará se o conjunto de dados de destino expirar. Para evitar que um fluxo de dados falhe, verifique se um conjunto de dados de destino está definido para expirar na data correta. Consulte a documentação para saber como atualizar datas de expiração."

Na interface do usuário da Platform, selecione **[!UICONTROL Origens]** na navegação à esquerda, para acessar a [!UICONTROL Origens] espaço de trabalho. Selecionar **[!UICONTROL Fluxos de dados]** no cabeçalho superior para exibir uma lista de fluxos de dados existentes.

![catálogo](../../images/tutorials/update-dataflows/catalog.png)

A variável [!UICONTROL Fluxos de dados] A página contém uma lista de todos os fluxos de dados existentes, incluindo informações sobre seu conjunto de dados de destino correspondente, origem e nome da conta.

Para classificar pela lista, selecione o ícone de filtro ![filtro](../../images/tutorials/update/filter.png) na parte superior esquerda para usar o painel classificar.

![filtro-fluxos de dados](../../images/tutorials/update-dataflows/filter-dataflows.png)

O painel de classificação fornece uma lista de todas as fontes disponíveis. Você pode selecionar mais de uma origem na lista para acessar uma seleção filtrada de fluxos de dados pertencentes a origens diferentes.

Selecione a fonte com a qual deseja trabalhar para ver uma lista de fluxos de dados existentes. Depois de identificar o fluxo de dados que deseja atualizar, selecione as reticências (`...`) ao lado do nome do fluxo de dados.

![edit-source](../../images/tutorials/update-dataflows/edit-source.png)

Um menu suspenso é exibido, fornecendo opções para atualizar o fluxo de dados selecionado. Aqui, você pode optar por atualizar os conjuntos de mapeamento e a programação de assimilação de um fluxo de dados. Você também pode selecionar opções para inspecionar o fluxo de dados no painel de monitoramento, assinar alertas, bem como desativar ou excluir o fluxo de dados.

Para atualizar as informações do fluxo de dados, selecione **[!UICONTROL Atualizar fluxo de dados]**.

![update-dataflow](../../images/tutorials/update-dataflows/update-dataflow.png)

### Adicionar dados

A variável [!UICONTROL Adicionar dados] é exibida. Selecione o formato de dados apropriado para revisar o conteúdo dos dados selecionados e selecione **[!UICONTROL Próxima]** para continuar.

![add-data](../../images/tutorials/update-dataflows/add-data.png)

### Detalhes do fluxo de dados

No [!UICONTROL Detalhes do fluxo de dados] você pode fornecer um nome e uma descrição atualizados para o fluxo de dados, bem como reconfigurar o limite de erros do fluxo de dados. Durante essa etapa, você também pode definir ou modificar as configurações da sua assinatura de alertas.

Depois de fornecer os valores atualizados, selecione **[!UICONTROL Próxima]**.

![detalhes do fluxo de dados](../../images/tutorials/update-dataflows/dataflow-detail.png)

### Mapeamento

>[!NOTE]
>
>No momento, o recurso de mapeamento de edição não é compatível com as seguintes fontes: Adobe Analytics, Adobe Audience Manager, API HTTP e [!DNL Marketo Engage].

A variável [!UICONTROL Mapeamento] A página fornece uma interface na qual você pode adicionar e remover conjuntos de mapeamento associados ao seu fluxo de dados.

A interface de mapeamento exibe o conjunto de mapeamento existente do fluxo de dados e não um novo conjunto de mapeamento recomendado. As atualizações de mapeamento são aplicadas apenas a execuções de fluxo de dados agendadas no futuro. Um fluxo de dados agendado para assimilação única não pode ter seus conjuntos de mapeamento atualizados.

Aqui, você pode usar a interface de mapeamento para modificar os conjuntos de mapeamento aplicados ao seu fluxo de dados. Para obter etapas abrangentes sobre como usar a interface de mapeamento, consulte [guia da interface de preparação de dados](../../../data-prep/ui/mapping.md) para obter mais informações.

![mapeamento](../../images/tutorials/update-dataflows/mapping.png)

### Programação

A variável [!UICONTROL Agendamento] A etapa é exibida, permitindo atualizar a programação de assimilação do fluxo de dados e assimilar automaticamente os dados de origem selecionados com os mapeamentos atualizados.

>[!NOTE]
>
>Não é possível reagendar um fluxo de dados que foi agendado para assimilação única.

![new-schedule](../../images/tutorials/update-dataflows/new-schedule.png)

Você também pode atualizar a programação de assimilação do fluxo de dados usando a opção de atualização em linha fornecida na página Fluxos de dados.

Na página fluxos de dados, selecione as reticências (`...`) ao lado do nome do fluxo de dados e selecione **[!UICONTROL Editar programação]** no menu suspenso exibido.

![edit-schedule](../../images/tutorials/update-dataflows/edit-schedule.png)

A variável **[!UICONTROL Editar programação]** A caixa de diálogo fornece opções para atualizar a frequência de assimilação e a taxa de intervalo do fluxo de dados. Depois de definir os valores atualizados de frequência e intervalo, selecione **[!UICONTROL Salvar]**.

![agenda-pop-up](../../images/tutorials/update-dataflows/schedule-pop-up.png)

### Consulte a seção

A variável **[!UICONTROL Revisão]** é exibida, permitindo que você revise seu fluxo de dados antes que ele seja atualizado.

Depois de revisar o fluxo de dados, selecione **[!UICONTROL Concluir]** e aguarde algum tempo para que o fluxo de dados com os novos conjuntos de mapeamento seja criado.

![revisão](../../images/tutorials/update-dataflows/review.png)

## Próximas etapas

Ao seguir este tutorial, você usou com êxito o [!UICONTROL Origens] espaço de trabalho para atualizar o agendamento de assimilação e os conjuntos de mapeamento do fluxo de dados.

Para obter etapas sobre como executar essas operações de forma programática usando o [!DNL Flow Service] , consulte o tutorial em [atualização de fluxos de dados usando a API do Serviço de fluxo](../../tutorials/api/update-dataflows.md).
