---
keywords: Experience Platform, home, tópicos populares, atualizar fluxos de dados, editar programação
description: Este tutorial aborda as etapas para atualizar uma programação de fluxo de dados, incluindo sua frequência de assimilação e taxa de intervalo, usando a área de trabalho Fontes .
solution: Experience Platform
title: Atualizar o cronograma de fluxo de dados da conexão de origem na interface do usuário
topic: visão geral
type: Tutorial
translation-type: tm+mt
source-git-commit: 31e4b15ad71a0d17278fbdb4d88ff42029cbe655
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 3%

---


# Atualizar fluxos de dados na interface do usuário

Este tutorial aborda as etapas para atualizar uma programação de fluxo de dados, incluindo sua frequência de assimilação e taxa de intervalo, usando o espaço de trabalho [!UICONTROL Sources].

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

- [Fontes](../../home.md): O Experience Platform permite que os dados sejam assimilados de várias fontes, fornecendo a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.
- [Sandboxes](../../../sandboxes/home.md): O Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

## Editar programação

Na interface do usuário da plataforma, selecione **[!UICONTROL Sources]** na navegação à esquerda para acessar o espaço de trabalho [!UICONTROL Sources]. Selecione **[!UICONTROL Dataflows]** no cabeçalho superior para exibir uma lista de fluxos de dados existentes.

![catálogo](../../images/tutorials/update-dataflows/catalog.png)

A página [!UICONTROL Dataflows] contém uma lista de todos os fluxos de dados existentes, incluindo informações sobre o status de execução, a data da última execução e o nome da conta.

Selecione o ícone de filtro ![filter](../../images/tutorials/update/filter.png) na parte superior esquerda para iniciar o painel de classificação.

![filter-dataflows](../../images/tutorials/update-dataflows/filter-dataflows.png)

O painel de classificação fornece uma lista de todas as fontes disponíveis. Você pode selecionar mais de uma fonte na lista para acessar uma seleção filtrada de fluxos de dados pertencentes a fontes diferentes.

Selecione a fonte com a qual deseja trabalhar para ver uma lista de seus fluxos de dados existentes. Depois de identificar o fluxo de dados que deseja reprogramar, selecione as reticências (`...`) ao lado do nome da conta.

![reagendar](../../images/tutorials/update-dataflows/reschedule.png)

Um menu suspenso é exibido, fornecendo opções para **[!UICONTROL Edit schedule]**, **[!UICONTROL Disable dataflow]**, **[!UICONTROL View in monitoring]** e **[!UICONTROL Delete]**. Selecione **[!UICONTROL Edit schedule]** no menu.

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

Ao seguir este tutorial, você usou com sucesso o espaço de trabalho [!UICONTROL Sources] para atualizar o agendamento de assimilação de um fluxo de dados.

Para obter etapas sobre como executar essas operações de forma programática usando a API [!DNL Flow Service], consulte o tutorial em [atualizar fluxos de dados usando a API do Serviço de Fluxo](../../tutorials/api/update-dataflows.md).