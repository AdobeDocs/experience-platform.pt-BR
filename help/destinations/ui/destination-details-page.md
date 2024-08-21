---
keywords: destinos;destino;página detalhes de destinos;página detalhes de destinos
title: Exibir detalhes do destino
description: A página de detalhes de um destino individual fornece uma visão geral dos detalhes do destino. Os detalhes do destino incluem o nome do destino, a ID, os públicos mapeados para o destino e os controles para editar a ativação e habilitar e desabilitar o fluxo de dados.
exl-id: e44e2b2d-f477-4516-8a47-3e95c2d85223
source-git-commit: 47d0e2a7fae973edfda035d046f66c88d34bf8b2
workflow-type: tm+mt
source-wordcount: '1286'
ht-degree: 0%

---

# Exibir detalhes do destino

## Visão geral {#overview}

Na interface do usuário do Adobe Experience Platform, é possível visualizar e monitorar os atributos e as atividades dos destinos. Esses detalhes incluem o nome e a ID do destino, controles para ativar ou desativar os destinos e muito mais. Os detalhes também incluem métricas para registros de perfis ativados, identidades ativadas, com falha e excluídas, e um histórico de execuções de fluxo de dados.

>[!NOTE]
>
>A página de detalhes dos destinos faz parte do espaço de trabalho [!UICONTROL Destinos] no [!DNL Platform] [!DNL UI]. Consulte a [[!UICONTROL visão geral do espaço de trabalho de Destinos]](./destinations-workspace.md) para obter mais informações.

## Exibir detalhes do destino {#view-details}

Siga as etapas abaixo para exibir mais detalhes sobre um destino existente. Você pode descobrir a ID de destino de um destino, o usuário que criou o destino, quando ele foi criado e outras informações.

1. Faça logon na [interface do usuário do Experience Platform](https://platform.adobe.com/) e selecione **[!UICONTROL Destinos]** na barra de navegação esquerda. Selecione **[!UICONTROL Procurar]** no cabeçalho superior para exibir seus destinos existentes.

   ![Procurar destinos](../assets/ui/details-page/browse-destinations.png)

2. Selecione o ícone de filtro ![Ícone de filtro](../../images/icons/filter.png) na parte superior esquerda para iniciar o painel de classificação. O painel de classificação fornece uma lista de todos os seus destinos. Você pode selecionar mais de um destino na lista para ver uma seleção filtrada de fluxos de dados associados ao destino selecionado.

   ![Filtrar destinos](../assets/ui/details-page/filter-destinations.png)

3. Selecione a linha do destino para a qual você deseja exibir mais informações. Isso exibe um painel direito com informações sobre o destino, incluindo a ID de destino, o usuário que criou a conexão de destino e outras informações.

   ![ID de destino no painel direito](../assets/ui/details-page/right-rail-info-including-destination-id.png)

4. Como alternativa, você pode exibir outras informações sobre o destino selecionando *o nome do destino* que deseja exibir.

   ![Selecionar destino](../assets/ui/details-page/destination-select.png)

5. A página de detalhes do destino é exibida no painel direito, mostrando os controles disponíveis.

   ![Detalhes do destino](../assets/ui/details-page/destination-details.png)

## Painel direito {#right-rail}

O painel direito exibe as informações básicas sobre o destino selecionado.

![painel direito](../assets/ui/details-page/right-sidebar.png)

A tabela a seguir abrange os controles e os detalhes fornecidos pelo painel direito:

| Item do painel direito | Descrição |
| --- | --- |
| [!UICONTROL Ativar públicos-alvo] | Selecione este controle para editar quais públicos-alvo estão mapeados para o destino, atualizar agendas de exportação ou adicionar e remover atributos e identidades mapeados. Consulte os guias em [ativando dados de público-alvo para destinos de transmissão de público-alvo](./activate-segment-streaming-destinations.md), [ativando dados de público-alvo para destinos baseados em perfil em lote](./activate-batch-profile-destinations.md) e [ativando dados de público para destinos baseados em perfil de transmissão](./activate-streaming-profile-destinations.md) para obter mais informações. |
| [!UICONTROL Excluir] | Permite excluir esse fluxo de dados e desmapeia os públicos-alvo que foram ativados anteriormente, se houver. |
| [!UICONTROL Nome do destino] | Este campo pode ser editado para atualizar o nome do destino. |
| [!UICONTROL Descrição] | Este campo pode ser editado para atualizar ou adicionar uma descrição opcional ao destino. |
| [!UICONTROL Destino] | Representa a plataforma de destino para a qual os públicos-alvo são enviados. Consulte o [catálogo de destinos](../catalog/overview.md) para obter mais informações. |
| [!UICONTROL Status] | Indica se o destino está ativado ou desativado. |
| [!UICONTROL Ações de marketing] | Indica as ações de marketing (casos de uso) que se aplicam a esse destino para fins de governança de dados. |
| [!UICONTROL Categoria] | Indica o tipo de destino. Consulte o [catálogo de destinos](../catalog/overview.md) para obter mais informações. |
| [!UICONTROL Tipo de conexão] | Indica o formulário pelo qual seus públicos-alvo estão sendo enviados para o destino. Os valores possíveis incluem [!UICONTROL Cookie] e [!UICONTROL Baseado em perfil]. |
| [!UICONTROL Frequência] | Indica a frequência com que os públicos-alvo são enviados para o destino. Os valores possíveis incluem [!UICONTROL Streaming] e [!UICONTROL Batch]. |
| [!UICONTROL Identidade] | Representa o namespace de identidade aceito pelo destino, como `GAID`, `IDFA` ou `email`. Para obter mais informações sobre namespaces de identidade aceitos, consulte a [visão geral sobre namespaces de identidade](../../identity-service/features/namespaces.md). |
| [!UICONTROL Criado por] | Indica o usuário que criou esse destino. |
| [!UICONTROL Criado] | Indica a data e hora UTC em que esse destino foi criado. |

{style="table-layout:auto"}

## Alternância [!UICONTROL Habilitado]/[!UICONTROL Desabilitado] {#enabled-disabled-toggle}

Você pode usar a opção **[!UICONTROL Habilitado]/[!UICONTROL Desabilitado]** para iniciar e pausar todas as exportações de dados para o destino.

![Habilitar ou desabilitar a alternância de fluxo de dados](../assets/ui/details-page/enable-disable.png)

## [!UICONTROL Execuções de fluxo de dados] {#dataflow-runs}

A guia [!UICONTROL Execuções de fluxo de dados] fornece dados de métrica sobre as execuções de fluxo de dados para destinos de lote e fluxo. Consulte [Monitorar fluxos de dados](monitor-dataflows.md) para obter detalhes e definições de métricas.

>[!NOTE]
>
>* Atualmente, a funcionalidade de monitoramento de destinos tem suporte para todos os destinos nos destinos do Experience Platform *except* do [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md), [Personalização personalizada](/help/destinations/catalog/personalization/custom-personalization.md) e [Experience Cloud Audiences](/help/destinations/catalog/adobe/experience-cloud-audiences.md).
>* Para os [Amazon Kinesis](/help/destinations/catalog/cloud-storage/amazon-kinesis.md), [Hubs de Eventos do Azure](/help/destinations/catalog/cloud-storage/azure-event-hubs.md) e [destinos da API HTTP](/help/destinations/catalog/streaming/http-destination.md), as métricas relacionadas às identidades excluídas, com falha e ativadas são estimadas. Volumes maiores de dados de ativação levam a uma maior precisão das métricas.

![Exibição de execuções de fluxo de dados](../assets/ui/details-page/dataflow-runs.png)

### Duração das execuções de fluxo de dados {#dataflow-runs-duration}

Há uma diferença na duração exibida das execuções de fluxo de dados entre destinos de transmissão e destinos baseados em arquivo.

### Destinos de transmissão {#streaming}

Embora a **[!UICONTROL Duração do processamento]** indicada para a maioria das execuções de fluxo de dados de streaming seja de aproximadamente quatro horas, como mostrado na imagem abaixo, o tempo de processamento real para qualquer execução de fluxo de dados é muito mais curto. As janelas de execução do fluxo de dados permanecem abertas por mais tempo caso o Experience Platform precise tentar fazer chamadas novamente para o destino e também garantir que ele não perca nenhum dado de chegada tardia na mesma janela de tempo.

![Imagem da página Execuções de fluxo de dados com a coluna Tempo de processamento realçada para um destino de streaming.](/help/destinations/assets/ui/details-page/processing-time-dataflow-run-streaming.png)

Para obter mais informações, leia sobre [o fluxo de dados é executado para destinos de streaming](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-streaming-destinations) na documentação de monitoramento.

### Destinos baseados em arquivo {#file-based}

Para execuções de fluxo de dados para destinos baseados em arquivo, a **[!UICONTROL Duração do processamento]** depende do tamanho dos dados que estão sendo exportados e do carregamento do sistema. Observe também que o fluxo de dados executado para destinos baseados em arquivo é detalhado por público-alvo.

![Imagem da página Execuções de fluxo de dados com a coluna Tempo de processamento realçada para um destino baseado em arquivo.](../assets/ui/details-page/processing-time-dataflow-run-file-based.png)

Para obter mais informações, leia sobre [execuções de fluxo de dados para destinos em lote (baseados em arquivo)](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) na documentação de monitoramento.

## [!UICONTROL Dados de ativação] {#activation-data}

A guia **[!UICONTROL Dados de ativação]** exibe uma lista de públicos que foram mapeados para o destino, incluindo sua data inicial e data final (se aplicável), e outras informações relevantes para a exportação de dados, como tipo de exportação, agendamento e frequência. Para exibir os detalhes sobre um público-alvo específico, selecione o nome na lista.

>[!TIP]
>
>Para exibir e editar detalhes sobre os atributos e identidades mapeados para um destino, selecione **[!UICONTROL Ativar públicos-alvo]** no [painel direito](#right-rail).

>[!BEGINSHADEBOX]

A guia **[!UICONTROL Dados de ativação]** para um destino baseado em arquivo.

![Destino do lote de visualização de dados de ativação](../assets/ui/details-page/activation-data-batch.png)

>[!ENDSHADEBOX]


>[!BEGINSHADEBOX]

A guia **[!UICONTROL Dados de ativação]** para um destino de streaming.

![Destino de transmissão da exibição de dados de ativação](../assets/ui/details-page/activation-data-streaming.png)

>[!ENDSHADEBOX]

### Filtrar públicos ativados {#filter-audiences}

Para filtrar pela lista de públicos ativados para um destino, digite um nome de público na caixa de pesquisa. A lista de públicos-alvo é atualizada automaticamente com os resultados da pesquisa.

![Caixa de pesquisa para filtrar públicos.](../assets/ui/details-page/filter-audiences.png)

### Remover vários públicos-alvo dos fluxos de ativação {#bulk-remove}

Para remover vários públicos-alvo dos fluxos de ativação existentes, selecione os públicos-alvo e, em seguida, selecione **[!UICONTROL Remover públicos-alvo]**.

![Tela de dados de ativação destacando a opção Remover públicos.](../assets/ui/details-page/bulk-remove-audiences.png)

### Exportar vários arquivos sob demanda para destinos em lote {#bulk-export}

Você pode [exportar vários arquivos sob demanda](../ui/export-file-now.md) da página **[!UICONTROL Dados de ativação]**. Para fazer isso, selecione os públicos para os quais deseja exportar arquivos por demanda e selecione o controle **[!UICONTROL Exportar arquivo agora]** para acionar uma exportação única que fornecerá um arquivo para cada público selecionado para o destino do lote.

![Imagem destacando o botão Exportar arquivo agora.](../assets/ui/details-page/bulk-export-file-now.png)

### Editar agendamentos de ativação para vários públicos-alvo exportados para destinos em lote {#bulk-edit-schedule}

Para editar o agendamento de ativação existente de vários públicos-alvo ao mesmo tempo, selecione os públicos-alvo desejados e selecione **[!UICONTROL Editar agendamento]**. Para obter informações detalhadas sobre como definir ou editar um agendamento de exportação, leia a seção [agendar exportação de público-alvo](../ui/activate-batch-profile-destinations.md#scheduling).

![Tela de dados de ativação destacando a opção para editar agendamentos de ativação para vários públicos.](../assets/ui/details-page/bulk-edit-schedule.png)

>[!NOTE]
>
>Para obter detalhes sobre como explorar a página de detalhes de um público-alvo, consulte a [Visão geral do Portal de público-alvo](../../segmentation/ui/audience-portal.md#segment-details).

### Editar nomes de arquivos para vários públicos exportados para destinos em lote {#bulk-edit-file-names}

Para editar os nomes de arquivos exportados de vários públicos-alvo ao mesmo tempo, selecione os públicos-alvo desejados e selecione **[!UICONTROL Editar nome do arquivo]**. Para obter informações detalhadas sobre como definir ou editar um nome de arquivo, leia a seção sobre como [configurar nomes de arquivo](../ui/activate-batch-profile-destinations.md#configure-file-names).

![Tela de dados de ativação destacando a opção para editar nomes de arquivos para vários públicos-alvo.](../assets/ui/details-page/bulk-edit-file-name.png)