---
keywords: editar ativação, editar destino, editar destino
title: Editar fluxos de dados de ativação
type: Tutorial
description: Siga as etapas deste artigo para editar um fluxo de dados de ativação existente no Adobe Experience Platform.
exl-id: 0d79fbff-bfde-4109-8353-c7530e9719fb
source-git-commit: ec87cb1c8755f52233a5725aa3bb0c80a135d60c
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Editar fluxos de dados de ativação {#edit-activation-flows}

No Adobe Experience Platform, você pode configurar vários componentes de fluxos de dados de ativação existentes para destinos, como:

* [Habilitar ou desabilitar](#enable-disable-dataflows) fluxos de dados de ativação
* [Adicionar mais públicos-alvo](#add-audiences) aos fluxos de dados de ativação
* [Editar atributos e identidades mapeadas](#edit-mapped-attributes)
* [Editar o agendamento de ativação e a frequência de exportação](#edit-schedule-frequency)
* [Adicionar conjuntos de dados adicionais](#add-datasets) ao fluxo de trabalho de ativação
* [Editar ações de marketing](#edit-marketing-actions) para seus fluxos de dados de ativação
* [Aplicar rótulos de acesso](#apply-access-labels) aos dados exportados
* [Editar nomes e descrições](#edit-names-descriptions) para seus fluxos de dados de ativação

## Procurar fluxos de dados de ativação {#browse-activation-dataflows}

Siga as etapas abaixo para procurar seus fluxos de dados de ativação existentes e identificar aquele que deseja editar.

1. Faça logon na [Interface do usuário do Experience Platform](https://platform.adobe.com/) e selecione **[!UICONTROL Destinos]** na barra de navegação esquerda. Selecione **[!UICONTROL Procurar]** no cabeçalho superior para exibir seus fluxos de dados de destino existentes.

   ![Procurar destinos](../assets/ui/edit-activation/browse-destinations.png)

2. Selecione o ícone de filtro ![Ícone de filtro](../../images/icons/filter.png) na parte superior esquerda para iniciar o painel de classificação. O painel de classificação fornece uma lista de todos os seus destinos. Você pode selecionar mais de um destino na lista para ver uma seleção filtrada de fluxos de dados associados ao destino selecionado.

   ![Filtrar destinos](../assets/ui/edit-activation/filter-destinations.png)

3. Selecione o nome do fluxo de dados de destino que deseja editar.

   ![Selecionar destino](../assets/ui/edit-activation/destination-select.png)

4. A página **[!UICONTROL Execuções do fluxo de dados]** para o destino é exibida, mostrando seus controles disponíveis. Dependendo do tipo de destino, é possível executar várias operações de fluxo de dados. Consulte as próximas seções para cada operação de fluxo de dados compatível.

## Habilitar ou desabilitar fluxos de dados de ativação {#enable-disable-dataflows}

Use a opção **[!UICONTROL Habilitado]/[!UICONTROL Desabilitado]** para iniciar ou pausar todas as exportações de dados para o destino.

![Imagem da interface do Experience Platform mostrando a alternância de execução do fluxo de dados Habilitado/Desabilitado.](../assets/ui/edit-activation/enable-toggle.png)

## Adicionar públicos-alvo a um fluxo de dados de ativação {#add-audiences}

Selecione **[!UICONTROL Ativar públicos-alvo]** no painel direito para alterar quais públicos-alvo serão enviados para o destino. Essa ação leva você ao fluxo de trabalho de ativação.

![Imagem da interface do usuário do Experience Platform mostrando a opção de execução do fluxo de dados Ativar públicos-alvo.](../assets/ui/edit-activation/activate-audiences.png)

Na etapa **[!UICONTROL Selecionar públicos-alvo]** do fluxo de trabalho de ativação, você pode remover públicos-alvo existentes ou adicionar novos públicos-alvo ao fluxo de trabalho de ativação.

O fluxo de trabalho de ativação é ligeiramente diferente dependendo do tipo de destino. Para obter mais informações sobre os workflows de ativação para cada tipo de destino, leia os guias a seguir:

* [Ativar públicos para destinos de streaming](./activate-segment-streaming-destinations.md) (por exemplo, Facebook ou Twitter);
* [Ativar públicos para destinos de exportação de perfil em lote](./activate-batch-profile-destinations.md) (por exemplo, Amazon S3 ou Oracle Eloqua);
* [Ative públicos para destinos de exportação de perfil de streaming](./activate-streaming-profile-destinations.md) (por exemplo, API HTTP ou Amazon Kinesis).

## Editar o agendamento de ativação e a frequência de exportação {#edit-schedule-frequency}

Selecione **[!UICONTROL Ativar públicos-alvo]** no painel direito. Essa ação leva você ao fluxo de trabalho de ativação.

![Imagem da interface do usuário do Experience Platform mostrando a opção de execução do fluxo de dados Ativar públicos-alvo.](../assets/ui/edit-activation/activate-audiences.png)

Selecione a etapa **[!UICONTROL Agendamento]** no fluxo de trabalho de ativação para editar o agendamento de ativação e a frequência de exportação para seu fluxo de dados. Essa etapa permite configurar com que frequência os dados são exportados para o destino.

Na etapa **[!UICONTROL Agendamento]** do fluxo de trabalho de ativação, é possível:
* Ajuste a frequência da exportação.
* Defina ou modifique as datas de início e término do fluxo de dados de ativação e muito mais.

As operações de programação que você pode executar variam um pouco, dependendo do tipo de destino. Para obter mais informações sobre os workflows de ativação para cada tipo de destino, leia os guias a seguir:

* [Ativar públicos para destinos de streaming](./activate-segment-streaming-destinations.md) (por exemplo, Facebook ou Twitter);
* [Ativar públicos para destinos de exportação de perfil em lote](./activate-batch-profile-destinations.md) (por exemplo, Amazon S3 ou Oracle Eloqua);
* [Ative públicos para destinos de exportação de perfil de streaming](./activate-streaming-profile-destinations.md) (por exemplo, API HTTP ou Amazon Kinesis).

## Editar atributos e identidades mapeadas {#edit-mapped-attributes}

Selecione **[!UICONTROL Ativar públicos-alvo]** no painel direito. Essa ação leva você ao fluxo de trabalho de ativação.

![Imagem da interface do usuário do Experience Platform mostrando a opção de execução do fluxo de dados Ativar públicos-alvo.](../assets/ui/edit-activation/activate-audiences.png)

Selecione a etapa **[!UICONTROL Mapping]** do fluxo de trabalho de ativação para editar os atributos e as identidades mapeadas para o fluxo de dados de ativação. Isso permite ajustar quais atributos de perfil e identidades devem ser exportados para o destino.

Na etapa **[!UICONTROL Mapeamento]** do fluxo de trabalho de ativação, é possível:

* Adicione novos atributos ou identidades ao mapeamento.
* Remova atributos ou identidades existentes do mapeamento.
* Ajuste a ordem dos mapeamentos para definir a ordem das colunas nos arquivos exportados.

O fluxo de trabalho de ativação é ligeiramente diferente dependendo do tipo de destino. Para obter mais informações sobre os workflows de ativação para cada tipo de destino, leia os guias a seguir:

* [Ativar públicos para destinos de streaming](./activate-segment-streaming-destinations.md) (por exemplo, Facebook ou Twitter);
* [Ativar públicos para destinos de exportação de perfil em lote](./activate-batch-profile-destinations.md) (por exemplo, Amazon S3 ou Oracle Eloqua);
* [Ative públicos para destinos de exportação de perfil de streaming](./activate-streaming-profile-destinations.md) (por exemplo, API HTTP ou Amazon Kinesis).

## Adicionar conjuntos de dados a um fluxo de dados de ativação {#add-datasets}

Selecione **[!UICONTROL Exportar conjuntos de dados]** no painel direito para selecionar conjuntos de dados adicionais para exportar para o seu destino. Essa opção direciona você ao [fluxo de trabalho de exportação do conjunto de dados](export-datasets.md).

>[!NOTE]
>
>Esta opção só é visível para [destinos que oferecem suporte à exportação do conjunto de dados](export-datasets.md#supported-destinations).

![Imagem da interface do Experience Platform mostrando a opção de execução do fluxo de dados Exportar conjuntos de dados.](../assets/ui/edit-activation/export-datasets.png)

## [!BADGE Beta]{type=Informative} Editar ações de marketing {#edit-marketing-actions}

>[!NOTE]
>
>Este recurso está atualmente em **beta**. Para solicitar acesso, entre em contato com o representante da Adobe.

Você pode adicionar ou remover ações de marketing configuradas ao se conectar inicialmente ao destino.

Selecione **[!UICONTROL Editar ações de marketing]** no painel direito para abrir a tela de seleção de ações de marketing.

![Imagem da interface do Experience Platform mostrando a opção de edição de ações de marketing.](../assets/ui/edit-activation/edit-marketing-actions.png)

Selecione as ações de marketing aplicáveis e selecione **[!UICONTROL Salvar]** para aplicar as alterações.

![Imagem da interface do Experience Platform mostrando a tela editar ações de marketing.](../assets/ui/edit-activation/edit-marketing-actions-screen.png)


## Aplicar rótulos de acesso {#apply-access-labels}

Selecione **[!UICONTROL Aplicar rótulos de acesso]** para editar os rótulos de uso de dados dos dados exportados. Consulte a [documentação de rótulos de uso de dados](../../data-governance/labels/overview.md) para saber mais.

![Imagem da interface do Experience Platform mostrando a opção de execução do fluxo de dados Exportar conjuntos de dados.](../assets/ui/edit-activation/apply-access-labels.png)

## Editar nomes e descrições do fluxo de dados de ativação {#edit-names-descriptions}

Para editar o nome e a descrição do fluxo de dados de ativação, use os campos **[!UICONTROL Nome do destino]** e **[!UICONTROL Descrição]**.

![Detalhes do destino](../assets/ui/edit-activation/edit-destination-name-description.png)

## Próximas etapas {#next-steps}

Ao seguir este tutorial, você usou com êxito o espaço de trabalho **[!UICONTROL destinos]** para atualizar fluxos de dados de destino existentes.

Para obter mais informações sobre destinos, consulte a [visão geral sobre destinos](../catalog/overview.md).
