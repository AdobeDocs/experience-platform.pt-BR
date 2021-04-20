---
keywords: Experience Platform, home, tópicos populares, atualizar fluxos de dados, editar programação
description: Este tutorial aborda as etapas para atualizar uma programação de fluxo de dados, incluindo sua frequência de assimilação e taxa de intervalo, usando a área de trabalho Fontes .
solution: Experience Platform
title: Atualizar um fluxo de dados da conexão de origem na interface do usuário
topic: visão geral
type: Tutorial
exl-id: 0499a2a3-5a22-47b1-ac0e-76a432bd26c0
translation-type: tm+mt
source-git-commit: 3a36996b43760bc9161b8d4750a1121e9ada8d30
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 1%

---

# Atualizar fluxos de dados na interface do usuário

Este tutorial fornece etapas sobre como atualizar um fluxo de dados de fontes existentes, incluindo informações sobre como editar um agendamento e mapeamento de fluxo de dados, usando o espaço de trabalho [!UICONTROL Sources].

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

- [Fontes](../../home.md): O Experience Platform permite que os dados sejam assimilados de várias fontes, fornecendo a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.
- [Sandboxes](../../../sandboxes/home.md): O Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

## Editar mapeamento

>[!NOTE]
>
>No momento, o recurso de edição de mapeamento não é compatível com as seguintes fontes: Adobe Analytics, Adobe Audience Manager, API HTTP e [!DNL Marketo Engage].

Na interface do usuário da plataforma, selecione **[!UICONTROL Sources]** na navegação à esquerda para acessar o espaço de trabalho [!UICONTROL Sources]. Selecione **[!UICONTROL Dataflows]** no cabeçalho superior para exibir uma lista de fluxos de dados existentes.

![catálogo](../../images/tutorials/update-dataflows/catalog.png)

A página [!UICONTROL Dataflows] contém uma lista de todos os fluxos de dados existentes, incluindo informações sobre o status de execução, a data da última execução e o nome da conta.

Selecione o ícone de filtro ![filter](../../images/tutorials/update/filter.png) na parte superior esquerda para iniciar o painel de classificação.

![filter-dataflows](../../images/tutorials/update-dataflows/filter-dataflows.png)

O painel de classificação fornece uma lista de todas as fontes disponíveis. Você pode selecionar mais de uma fonte na lista para acessar uma seleção filtrada de fluxos de dados pertencentes a fontes diferentes.

Selecione a fonte com a qual deseja trabalhar para ver uma lista de seus fluxos de dados existentes. Depois de identificar o fluxo de dados que deseja atualizar, selecione as reticências (`...`) ao lado do nome da conta.

![editar-fonte](../../images/tutorials/update-dataflows/edit-source.png)

Um menu suspenso é exibido, fornecendo opções para atualizar o fluxo de dados selecionado. Aqui, você pode optar por atualizar os conjuntos de mapeamento e o agendamento de ingestão de um fluxo de dados. Você também pode selecionar opções para inspecionar o fluxo de dados no painel de monitoramento, bem como desativar ou excluir o fluxo de dados.

Selecione **[!UICONTROL Edit source]** para atualizar o mapeamento.

![edit-dataflow](../../images/tutorials/update-dataflows/edit-dataflow.png)

A etapa [!UICONTROL Add data] é exibida. Selecione o formato de dados apropriado para revisar o conteúdo dos dados selecionados e selecione **[!UICONTROL Next]** para continuar.

![add-data](../../images/tutorials/update-dataflows/add-data.png)

A página [!UICONTROL Mapping] fornece uma interface na qual você pode adicionar e remover conjuntos de mapeamento associados ao conjunto de dados.

>[!TIP]
>
>As atualizações de mapeamento são aplicadas apenas a execuções de fluxo de dados agendadas no futuro.

Selecione **[!UICONTROL Add new mapping]** para adicionar um novo conjunto de mapeamento.

![add-new-mapping](../../images/tutorials/update-dataflows/add-new-mapping.png)

Em seguida, insira o atributo de campo de origem e os valores de campo XDM de destino apropriados para concluir seu conjunto de mapeamento adicional. Selecione **[!UICONTROL Next]** para continuar.

![novo mapeamento adicionado](../../images/tutorials/update-dataflows/new-mapping-added.png)

A etapa [!UICONTROL Scheduling] é exibida, permitindo atualizar o agendamento de assimilação do fluxo de dados e assimilar automaticamente os dados de origem selecionados com os mapeamentos atualizados.

>[!NOTE]
>
>Não é possível atualizar conjuntos de mapeamento para fluxos de dados que foram agendados para assimilação única e a hora de início está no passado.

![programação](../../images/tutorials/update-dataflows/scheduling.png)

Na página [!UICONTROL Dataflow detail], você pode fornecer um nome e uma descrição atualizados para o fluxo de dados, bem como reconfigurar o limite de erro do fluxo de dados.

Depois de fornecer os valores atualizados, selecione **[!UICONTROL Next]**.

![detalhe do fluxo de dados](../../images/tutorials/update-dataflows/dataflow-detail.png)

A etapa **[!UICONTROL Review]** é exibida, permitindo que você revise o fluxo de dados antes de atualizá-lo.

Depois de revisar o fluxo de dados, selecione **[!UICONTROL Finish]** e conceda algum tempo para que o fluxo de dados com os novos conjuntos de mapeamento sejam criados.

![revisão](../../images/tutorials/update-dataflows/review.png)

## Editar programação

Para editar o agendamento de assimilação de um fluxo de dados existente, selecione os elipses (`...`) ao lado de um nome de fluxo de dados e selecione **[!UICONTROL Edit schedule]** no menu suspenso.

![editar programação](../../images/tutorials/update-dataflows/edit-schedule.png)

A caixa de diálogo **[!UICONTROL Edit schedule]** fornece opções para atualizar a frequência de assimilação e a taxa de intervalo do fluxo de dados. Depois de definir os valores de frequência e intervalo atualizados, selecione **[!UICONTROL Save]**.

>[!NOTE]
>
>Não é possível reprogramar um fluxo de dados agendado para uma ingestão única.

![caixa de diálogo agendamento](../../images/tutorials/update-dataflows/schedule-dialog-box.png)

| Agendamento | Descrição |
| ---------- | ----------- |
| Frequência | A frequência com que o fluxo de dados coletará dados. Os valores aceitáveis para o agendamento de frequência de edição de um fluxo de dados já existente incluem: `minute`, `hour`, `day` ou `week`. |
| Intervalo | O intervalo designa o período entre duas execuções consecutivas de fluxo. O valor do intervalo deve ser um número inteiro diferente de zero e deve ser maior ou igual a `15`. |

Após alguns instantes, uma caixa de confirmação será exibida na parte inferior da tela para confirmar uma atualização bem-sucedida.

![confirmação de programação](../../images/tutorials/update-dataflows/schedule-confirm.png)

## Próximas etapas

Ao seguir este tutorial, você usou com sucesso o espaço de trabalho [!UICONTROL Sources] para atualizar o agendamento de assimilação e os conjuntos de mapeamento do seu fluxo de dados.

Para obter etapas sobre como executar essas operações de forma programática usando a API [!DNL Flow Service], consulte o tutorial em [atualizar fluxos de dados usando a API do Serviço de Fluxo](../../tutorials/api/update-dataflows.md).
