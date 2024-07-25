---
keywords: Experience Platform;página inicial;tópicos populares;atualizar fluxos de dados;editar programação;;home;popular topics;update dataflows;edit schedule
description: Este tutorial aborda as etapas para atualizar uma programação de fluxo de dados, incluindo a frequência de assimilação e a taxa de intervalo, usando o espaço de trabalho Origens.
solution: Experience Platform
title: Atualizar um fluxo de dados de conexão do Source na interface
type: Tutorial
exl-id: 0499a2a3-5a22-47b1-ac0e-76a432bd26c0
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 9%

---

# Atualizar fluxos de dados na interface do

Este tutorial fornece etapas sobre como atualizar um fluxo de dados existente, incluindo sua programação e mapeamento, usando o espaço de trabalho de origens.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../home.md): o Experience Platform permite que os dados sejam assimilados de várias fontes e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.
* [Sandboxes](../../../sandboxes/home.md): o Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

## Atualizar fluxos de dados {#update-dataflows}

>[!CONTEXTUALHELP]
>id="platform_sources_dataflows_daysRemaining"
>title="Expiração do conjunto de dados"
>abstract="Esta coluna indica o número de dias que o conjunto de dados de destino tem antes de expirar automaticamente.<br>Haverá falha em um fluxo de dados se o conjunto de dados de destino expirar. Para evitar falhas em um fluxo de dados, certifique-se de que um conjunto de dados de destino esteja definido para expirar na data correta. Consulte a documentação para saber como atualizar datas de expiração."

Na interface da Platform, selecione **[!UICONTROL Fontes]** na navegação à esquerda para acessar o espaço de trabalho [!UICONTROL Fontes]. Selecione **[!UICONTROL Fluxos de dados]** no cabeçalho superior para exibir uma lista de fluxos de dados existentes.

![catálogo](../../images/tutorials/update-dataflows/catalog.png)

A página [!UICONTROL Fluxos de Dados] contém uma lista de todos os fluxos de dados existentes, incluindo informações sobre o conjunto de dados de destino, a fonte e o nome da conta correspondentes.

Para classificar pela lista, selecione o ícone de filtro ![filtro](/help/images/icons/filter.png) na parte superior esquerda para usar o painel de classificação.

![fluxos-dados-filtro](../../images/tutorials/update-dataflows/filter-dataflows.png)

O painel de classificação fornece uma lista de todas as fontes disponíveis. Você pode selecionar mais de uma origem na lista para acessar uma seleção filtrada de fluxos de dados pertencentes a origens diferentes.

Selecione a fonte com a qual deseja trabalhar para ver uma lista de fluxos de dados existentes. Depois de identificar o fluxo de dados que deseja atualizar, selecione as reticências (`...`) ao lado do nome do fluxo de dados.

![editar-fonte](../../images/tutorials/update-dataflows/edit-source.png)

Um menu suspenso é exibido, fornecendo opções para atualizar o fluxo de dados selecionado. Aqui, você pode optar por atualizar os conjuntos de mapeamento e a programação de assimilação de um fluxo de dados. Você também pode selecionar opções para inspecionar o fluxo de dados no painel de monitoramento, assinar alertas, bem como desativar ou excluir o fluxo de dados.

Para atualizar as informações do seu fluxo de dados, selecione **[!UICONTROL Atualizar fluxo de dados]**.

![fluxo de dados de atualização](../../images/tutorials/update-dataflows/update-dataflow.png)

### Adicionar dados

A etapa [!UICONTROL Adicionar dados] é exibida. Selecione o formato de dados apropriado para revisar o conteúdo dos dados selecionados e selecione **[!UICONTROL Avançar]** para continuar.

![adicionar-dados](../../images/tutorials/update-dataflows/add-data.png)

### Detalhes do fluxo de dados

Na página [!UICONTROL detalhes do fluxo de dados], você pode fornecer um nome e uma descrição atualizados para o fluxo de dados, bem como reconfigurar o limite de erros do fluxo de dados. Durante essa etapa, você também pode definir ou modificar as configurações de sua assinatura de alertas.

Depois de fornecer os valores atualizados, selecione **[!UICONTROL Avançar]**.

![detalhes do fluxo de dados](../../images/tutorials/update-dataflows/dataflow-detail.png)

### Mapeamento

>[!NOTE]
>
>O recurso de mapeamento de edição não tem suporte atualmente para as seguintes fontes: Adobe Analytics, Adobe Audience Manager, API HTTP e [!DNL Marketo Engage].

A página [!UICONTROL Mapeamento] fornece uma interface em que você pode adicionar e remover conjuntos de mapeamentos associados ao seu fluxo de dados.

A interface de mapeamento exibe o conjunto de mapeamento existente do fluxo de dados e não um novo conjunto de mapeamento recomendado. As atualizações de mapeamento são aplicadas apenas a execuções de fluxo de dados agendadas no futuro. Um fluxo de dados agendado para assimilação única não pode ter seus conjuntos de mapeamento atualizados.

Aqui, você pode usar a interface de mapeamento para modificar os conjuntos de mapeamento aplicados ao seu fluxo de dados. Para obter etapas abrangentes sobre como usar a interface de mapeamento, consulte o [guia da interface de preparação de dados](../../../data-prep/ui/mapping.md) para obter mais informações.

![mapeamento](../../images/tutorials/update-dataflows/mapping.png)

### Agendando

A etapa [!UICONTROL Agendamento] é exibida, permitindo atualizar o agendamento de assimilação do fluxo de dados e assimilar automaticamente os dados de origem selecionados com os mapeamentos atualizados.

>[!NOTE]
>
>Não é possível reagendar um fluxo de dados que foi agendado para assimilação única.

![nova-programação](../../images/tutorials/update-dataflows/new-schedule.png)

Você também pode atualizar a programação de assimilação do fluxo de dados usando a opção de atualização em linha fornecida na página Fluxos de dados.

Na página de fluxos de dados, selecione as reticências (`...`) ao lado do nome do fluxo de dados e selecione **[!UICONTROL Editar programação]** no menu suspenso exibido.

![editar-agendar](../../images/tutorials/update-dataflows/edit-schedule.png)

A caixa de diálogo **[!UICONTROL Editar agendamento]** fornece opções para atualizar a frequência de assimilação e a taxa de intervalo do fluxo de dados. Depois de definir os valores atualizados de frequência e intervalo, selecione **[!UICONTROL Salvar]**.

![pop-up de agendamento](../../images/tutorials/update-dataflows/schedule-pop-up.png)

### Revisar

A etapa **[!UICONTROL Revisão]** é exibida, permitindo que você revise seu fluxo de dados antes que ele seja atualizado.

Depois de revisar o fluxo de dados, selecione **[!UICONTROL Concluir]** e aguarde algum tempo para que o fluxo de dados com os novos conjuntos de mapeamento seja criado.

![avaliação](../../images/tutorials/update-dataflows/review.png)

## Próximas etapas

Ao seguir este tutorial, você usou com êxito o espaço de trabalho [!UICONTROL Fontes] para atualizar o agendamento de assimilação e os conjuntos de mapeamento do seu fluxo de dados.

Para obter etapas sobre como executar essas operações de forma programática usando a API [!DNL Flow Service], consulte o tutorial em [atualização de fluxos de dados usando a API de Serviço de Fluxo](../../tutorials/api/update-dataflows.md).
