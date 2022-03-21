---
keywords: Experience Platform, home, tópicos populares, atualizar fluxos de dados, editar programação
description: Este tutorial aborda as etapas para atualizar uma programação de fluxo de dados, incluindo sua frequência de assimilação e taxa de intervalo, usando a área de trabalho Fontes .
solution: Experience Platform
title: Atualizar um fluxo de dados da conexão de origem na interface do usuário
topic-legacy: overview
type: Tutorial
exl-id: 0499a2a3-5a22-47b1-ac0e-76a432bd26c0
source-git-commit: 6a9ad0ce5d664e3b32cab4183b54fabd5d9d19e3
workflow-type: tm+mt
source-wordcount: '724'
ht-degree: 0%

---

# Atualizar fluxos de dados na interface do usuário

Este tutorial fornece etapas sobre como atualizar um fluxo de dados existente, incluindo seu agendamento e mapeamento, usando o espaço de trabalho de fontes.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../home.md): O Experience Platform permite que os dados sejam assimilados de várias fontes, fornecendo a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.
* [Sandboxes](../../../sandboxes/home.md): O Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

## Atualizar fluxos de dados

Na interface do usuário da plataforma, selecione **[!UICONTROL Fontes]** na navegação à esquerda para acessar o [!UICONTROL Fontes] espaço de trabalho. Selecionar **[!UICONTROL Fluxos de dados]** no cabeçalho superior para exibir uma lista de fluxos de dados existentes.

![catálogo](../../images/tutorials/update-dataflows/catalog.png)

O [!UICONTROL Fluxos de dados] contém uma lista de todos os fluxos de dados existentes, incluindo informações sobre o conjunto de dados de destino, a fonte e o nome da conta correspondentes.

Para classificar pela lista, selecione o ícone de filtro ![filter](../../images/tutorials/update/filter.png) no canto superior esquerdo para usar o painel de classificação.

![filter-dataflows](../../images/tutorials/update-dataflows/filter-dataflows.png)

O painel de classificação fornece uma lista de todas as fontes disponíveis. Você pode selecionar mais de uma fonte na lista para acessar uma seleção filtrada de fluxos de dados pertencentes a fontes diferentes.

Selecione a fonte com a qual deseja trabalhar para ver uma lista de seus fluxos de dados existentes. Depois de identificar o fluxo de dados que deseja atualizar, selecione as reticências (`...`) ao lado do nome do fluxo de dados.

![editar-fonte](../../images/tutorials/update-dataflows/edit-source.png)

Um menu suspenso é exibido, fornecendo opções para atualizar o fluxo de dados selecionado. Aqui, você pode optar por atualizar os conjuntos de mapeamento e o agendamento de ingestão de um fluxo de dados. Você também pode selecionar opções para inspecionar o fluxo de dados no painel de monitoramento, assinar alertas, bem como desativar ou excluir o fluxo de dados.

Para atualizar as informações do seu fluxo de dados, selecione **[!UICONTROL Atualizar fluxo de dados]**.

![update-dataflow](../../images/tutorials/update-dataflows/update-dataflow.png)

### Adicionar dados

O [!UICONTROL Adicionar dados] será exibida. Selecione o formato de dados apropriado para revisar o conteúdo dos dados selecionados e selecione **[!UICONTROL Próximo]** para continuar.

![add-data](../../images/tutorials/update-dataflows/add-data.png)

### Detalhes do fluxo de dados

No [!UICONTROL Detalhes do fluxo de dados] , você pode fornecer um nome e uma descrição atualizados para o fluxo de dados, bem como reconfigurar o limite de erro do fluxo de dados. Durante essa etapa, você também pode configurar ou modificar as configurações para sua assinatura de alerta.

Após fornecer os valores atualizados, selecione **[!UICONTROL Próximo]**.

![detalhe do fluxo de dados](../../images/tutorials/update-dataflows/dataflow-detail.png)

### Mapeamento

>[!NOTE]
>
>No momento, o recurso de edição de mapeamento não é compatível com as seguintes fontes: Adobe Analytics, Adobe Audience Manager, API HTTP e [!DNL Marketo Engage].

O [!UICONTROL Mapeamento] fornece uma interface na qual você pode adicionar e remover conjuntos de mapeamento associados ao seu fluxo de dados.

A interface de mapeamento exibe o conjunto de mapeamento existente do seu fluxo de dados e não um novo conjunto de mapeamento recomendado. As atualizações de mapeamento são aplicadas apenas a execuções de fluxo de dados agendadas no futuro. Um fluxo de dados agendado para assimilação única não pode ter seus conjuntos de mapeamento atualizados.

Aqui, você pode usar a interface de mapeamento para modificar os conjuntos de mapeamento aplicados ao seu fluxo de dados. Para obter etapas abrangentes sobre como usar a interface de mapeamento, consulte o [guia da interface do usuário de preparação de dados](../../../data-prep/ui/mapping.md) para obter mais informações.

![mapeamento](../../images/tutorials/update-dataflows/mapping.png)

### Agendamento

O [!UICONTROL Agendamento] é exibida, permitindo atualizar o agendamento de assimilação do fluxo de dados e assimilar automaticamente os dados de origem selecionados com os mapeamentos atualizados.

>[!NOTE]
>
>Não é possível reprogramar um fluxo de dados agendado para uma ingestão única.

![nova programação](../../images/tutorials/update-dataflows/new-schedule.png)

Você também pode atualizar o agendamento de assimilação do seu fluxo de dados usando a opção de atualização em linha fornecida na página de fluxos de dados.

Na página de fluxos de dados, selecione as reticências (`...`) ao lado do nome do fluxo de dados e selecione **[!UICONTROL Editar programação]** no menu suspenso exibido.

![editar programação](../../images/tutorials/update-dataflows/edit-schedule.png)

O **[!UICONTROL Editar programação]** A caixa de diálogo fornece opções para atualizar a frequência de assimilação e a taxa de intervalo do fluxo de dados. Depois de definir os valores de frequência e intervalo atualizados, selecione **[!UICONTROL Salvar]**.

![pop-up de programação](../../images/tutorials/update-dataflows/schedule-pop-up.png)

### Revisão

O **[!UICONTROL Revisão]** é exibida, permitindo que você revise o fluxo de dados antes de atualizá-lo.

Depois de revisar o fluxo de dados, selecione **[!UICONTROL Concluir]** e permita que o fluxo de dados com os novos conjuntos de mapeamento seja criado.

![revisão](../../images/tutorials/update-dataflows/review.png)

## Próximas etapas

Ao seguir este tutorial, você usou com sucesso a variável [!UICONTROL Fontes] espaço de trabalho para atualizar o agendamento de assimilação e os conjuntos de mapeamento do seu fluxo de dados.

Para obter etapas sobre como executar essas operações de forma programática usando o [!DNL Flow Service] Consulte o tutorial em [atualização de fluxos de dados usando a API do Serviço de Fluxo](../../tutorials/api/update-dataflows.md).
