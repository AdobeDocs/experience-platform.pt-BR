---
description: Saiba como atualizar um fluxo de dados de fontes existente na interface do usuário do Experience Platform.
title: Atualizar um fluxo de dados de conexão do Source na interface
exl-id: 0499a2a3-5a22-47b1-ac0e-76a432bd26c0
source-git-commit: c3082a8769f317407197b3fd05b36cfe00b36470
workflow-type: tm+mt
source-wordcount: '766'
ht-degree: 8%

---

# Atualizar fluxos de dados na interface do

Leia este tutorial para obter etapas sobre como atualizar um fluxo de dados existente, incluindo suas configurações de agendamento e mapeamento, usando o espaço de trabalho de origens na interface do usuário do Adobe Experience Platform.

## Introdução

Este tutorial requer um entendimento prático dos seguintes componentes do Experience Platform:

* [Fontes](../../home.md): o Experience Platform permite que os dados sejam assimilados de várias fontes e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.
* [Sandboxes](../../../sandboxes/home.md): o Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

## Atualizar fluxos de dados {#update-dataflows}

>[!CONTEXTUALHELP]
>id="platform_sources_dataflows_daysRemaining"
>title="Expiração do conjunto de dados"
>abstract="Esta coluna indica o número de dias que o conjunto de dados de destino tem antes de expirar automaticamente.<br>Haverá falha em um fluxo de dados se o conjunto de dados de destino expirar. Para evitar falhas em um fluxo de dados, certifique-se de que um conjunto de dados de destino esteja definido para expirar na data correta. Consulte a documentação para saber como atualizar datas de expiração."

Na interface do usuário do Experience Platform, selecione **[!UICONTROL Fontes]** na navegação à esquerda e selecione **[!UICONTROL Fluxos de dados]** no cabeçalho superior.

![O catálogo de fontes com a guia de cabeçalho de fluxos de dados selecionada.](../../images/tutorials/update-dataflows/catalog.png)

>[!TIP]
>
>Você pode classificar e filtrar seus fluxos de dados usando recursos de filtragem. Leia o manual sobre [filtragem de objetos de fontes na interface](./filter.md) para obter mais informações.

A página [!UICONTROL Fluxos de Dados] exibe uma lista de todos os fluxos de dados existentes na sua organização. Localize o fluxo de dados que você deseja atualizar e selecione as reticências (`...`) ao lado dele. Um menu suspenso é exibido, exibindo uma lista de opções que você pode escolher para fazer configurações adicionais ao seu fluxo de dados existente.

Para atualizar seu fluxo de dados, selecione **[!UICONTROL Atualizar fluxo de dados]**.

![O menu suspenso no qual são listadas as opções para atualizar fluxos de dados.](../../images/tutorials/update-dataflows/dropdown_update.png)

Você é levado ao fluxo de trabalho de origens, onde pode prosseguir para atualizar aspectos do fluxo de dados, incluindo seus detalhes na etapa [!UICONTROL Fornecer detalhes do fluxo de dados].

### Atualizar mapeamento {#update-mapping}

>[!NOTE]
>
>O recurso de mapeamento de edição não tem suporte atualmente para as seguintes fontes: Adobe Analytics, Adobe Audience Manager, API HTTP e [!DNL Marketo Engage].

Durante esse processo, também é possível atualizar os conjuntos de mapeamento associados ao fluxo de dados.  A interface de mapeamento exibe o mapeamento existente do fluxo de dados e não um novo conjunto de mapeamentos recomendado. As atualizações de mapeamento são aplicadas apenas a execuções de fluxo de dados agendadas no futuro. Um fluxo de dados agendado para assimilação única não pode ter seus conjuntos de mapeamento atualizados.

Use a interface de mapeamento para modificar os conjuntos de mapeamento aplicados ao seu fluxo de dados. Para obter etapas abrangentes sobre como usar a interface de mapeamento, consulte o [guia da interface de preparação de dados](../../../data-prep/ui/mapping.md) para obter mais informações.

![A etapa de mapeamento do fluxo de trabalho de origens. Use esta etapa para atualizar os mapeamentos associados ao seu fluxo de dados.](../../images/tutorials/update-dataflows/mapping.png)

### Atualizar programação

Depois de atualizar os mapeamentos do fluxo de dados, você pode prosseguir para atualizar a programação de assimilação para assimilar o fluxo de dados com os novos dados de mapeamento. Você só pode atualizar a programação de assimilação de fluxos de dados configurados para assimilação em uma programação recorrente. Não é possível reagendar um fluxo de dados configurado para assimilação única.

Você também pode atualizar a programação de assimilação do fluxo de dados usando a opção de atualização em linha fornecida na página Fluxos de dados.

Na página de fluxos de dados, selecione as reticências (`...`) ao lado do nome do fluxo de dados e selecione **[!UICONTROL Editar programação]** no menu suspenso exibido.

![A etapa de agendamento do fluxo de trabalho de fontes. Use esta etapa para atualizar a programação do fluxo de dados.](../../images/tutorials/update-dataflows/dropdown_edit.png)

A caixa de diálogo **[!UICONTROL Editar agendamento]** fornece opções para atualizar a frequência de assimilação e a taxa de intervalo do fluxo de dados. Depois de definir os valores atualizados de frequência e intervalo, selecione **[!UICONTROL Salvar]**.

![Uma janela pop-up que você pode usar para editar a programação de assimilação do fluxo de dados.](../../images/tutorials/update-dataflows/edit_schedule.png)

### Desativar fluxo de dados

Você pode desativar o fluxo de dados usando o mesmo menu suspenso. Para desabilitar seu fluxo de dados, selecione **[!UICONTROL Desabilitar fluxo de dados]**.

![O menu suspenso com a opção para desabilitar o fluxo de dados.](../../images/tutorials/update-dataflows/dropdown_disable.png)

Em seguida, selecione [!UICONTROL Desativar] na janela pop-up exibida.

![A janela pop-up na qual você deve confirmar que deseja desabilitar seu fluxo de dados.](../../images/tutorials/update-dataflows/disable_dataflow.png)

Se e quando você reativar esse fluxo de dados posteriormente, o Experience Platform agendará automaticamente as execuções de preenchimento retroativo para cobrir o período durante o qual o fluxo de dados foi desativado. Por exemplo, se o fluxo de dados foi configurado para ser executado por hora e foi desativado por 48 horas, ao reativar esse fluxo de dados, o Experience Platform criará 48 execuções de preenchimento retroativo para processar os intervalos perdidos.

## Próximas etapas

Ao seguir este tutorial, você usou com êxito o espaço de trabalho [!UICONTROL Fontes] para atualizar o agendamento de assimilação e os conjuntos de mapeamento do seu fluxo de dados.

Para obter etapas sobre como executar essas operações de forma programática usando a API [!DNL Flow Service], consulte o tutorial em [atualização de fluxos de dados usando a API de Serviço de Fluxo](../../tutorials/api/update-dataflows.md).
