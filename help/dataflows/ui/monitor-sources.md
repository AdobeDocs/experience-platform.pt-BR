---
keywords: Experience Platform;home;popular topics;monitor accounts;monitor dataflows;dataflows;sources
description: Os conectores de origem na Adobe Experience Platform fornecem a capacidade de assimilar dados de origem externa de forma programada. Este tutorial fornece etapas para a exibição de fluxos de dados existentes na área de trabalho Fontes.
solution: Experience Platform
title: Monitorar fluxos de dados
topic: overview
type: Tutorial
translation-type: tm+mt
source-git-commit: 4d99526a592e173e3b46e1fa2a3f869b1fe5d4f2
workflow-type: tm+mt
source-wordcount: '807'
ht-degree: 1%

---


# Monitorar fluxos de dados para fontes na interface do usuário

Os conectores de origem na Adobe Experience Platform fornecem a capacidade de assimilar dados de origem externa de forma programada. Este tutorial fornece etapas para a exibição de fluxos de dados existentes na área de trabalho [!UICONTROL Fontes] .

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

- [Fontes](../../sources/home.md): [!DNL Experience Platform] permite que os dados sejam ingeridos de várias fontes e, ao mesmo tempo, fornece a você a capacidade de estruturar, rotular e aprimorar os dados recebidos usando [!DNL Platform] serviços.
- [Caixas de proteção](../../sandboxes/home.md): [!DNL Experience Platform] fornece caixas de proteção virtuais que particionam uma única [!DNL Platform] instância em ambientes virtuais separados para ajudar a desenvolver e desenvolver aplicativos de experiência digital.

## Monitorar fluxos de dados

Faça logon na interface do usuário [do](https://platform.adobe.com) Experience Platform e selecione **[!UICONTROL Fontes]** na navegação à esquerda para acessar a área de trabalho [!UICONTROL Fontes] . Selecione **[!UICONTROL Fluxos de dados]** no cabeçalho superior para visualização de fluxos de dados existentes.

![catálogo-dataflows](../assets/ui/monitor-sources/catalog-dataflows.png)

Uma lista de fluxos de dados existentes é exibida. Nesta página há uma lista de fluxos de dados visualizáveis, incluindo informações sobre sua fonte, nome de usuário, número de fluxos de dados e status.

Consulte a tabela a seguir para obter mais informações sobre status:

| Status | Descrição |
| ------ | ----------- |
| Ativado | O `Enabled` status indica que um fluxo de dados está ativo e está ingerindo dados de acordo com o agendamento fornecido. |
| Desativado | O `Disabled` status indica que um fluxo de dados está inativo e não está ingerindo dados. |
| Processamento | O `Processing` status indica que um fluxo de dados ainda não está ativo. Esse status geralmente é encontrado imediatamente após a criação de um novo fluxo de dados. |
| Erro | O `Error` status indica que o processo de ativação de um fluxo de dados foi interrompido. |

Selecione o ícone de funil na parte superior esquerda para classificar.

![lista de dados](../assets/ui/monitor-sources/dataflows-list.png)

O painel de classificação é exibido. Selecione a fonte que deseja acessar no menu de rolagem e selecione o fluxo de dados na lista à direita. Você também pode selecionar o botão de elipses (`...`) para exibir mais opções disponíveis para o seu fluxo de dados selecionado.

![sort-dataflows](../assets/ui/monitor-sources/dataflows-sort.png)

A página de atividade **[!UICONTROL do]** Dataflow contém detalhes sobre o número de registros ingeridos e os registros falharam, bem como informações sobre o status e o tempo de processamento do dataflow. Selecione o ícone de calendário acima do fluxo de dados para ajustar o intervalo de tempo dos registros de ingestão.

![atividade de fluxo de dados](../assets/ui/monitor-sources/dataflow-activity.png)

O calendário permite que você visualização os diferentes intervalos de tempo para registros ingeridos. Você pode selecionar uma das duas opções predefinidas &quot;[!UICONTROL Últimos 7 dias]&quot; ou &quot;[!UICONTROL Últimos 30 dias]&quot;. Como alternativa, você pode definir um período de tempo personalizado usando o calendário. Selecione seu período de tempo de escolha e selecione **[!UICONTROL Aplicar]** para continuar.

![calendário de fluxo](../assets/ui/monitor-sources/flow-calendar.png)

Por padrão, a atividade **** Dataflow exibe o painel **[!UICONTROL Propriedades]** associado ao fluxo de dados. Selecione a execução de fluxo da lista para ver seus metadados associados, incluindo informações sobre sua ID de execução exclusiva.

Selecione start **[!UICONTROL de execução do]** Dataflow para acessar a visão geral **[!UICONTROL de execução do]** Dataflow.

![run](../assets/ui/monitor-sources/run-metadata.png)

A visão geral **[!UICONTROL da execução do]** Fluxo de dados exibe informações sobre o fluxo de dados, incluindo seus metadados, status de ingestão parcial e limite de erro atribuído. O cabeçalho superior também inclui um resumo de erro. O resumo **[!UICONTROL de]** Erro contém o erro de nível superior específico que mostra em qual etapa o processo de ingestão encontrou um erro.

![visão geral da execução do dataflow](../assets/ui/monitor-sources/dataflow-run-overview.png)

Consulte a tabela a seguir para obter os erros que podem ser vistos no resumo **** Erro.

| Erro | Descrição |
| ---------- | ----------- |
| `CONNECTOR-1001-500` | Erro ao copiar dados de uma fonte. |
| `CONNECTOR-2001-500` | Ocorreu um erro ao processar os dados copiados para [!DNL Platform]. Esse erro pode ser relacionado à análise, validação ou transformação. |

A metade inferior da tela contém informações sobre erros **[!UICONTROL de execução do]** Dataflow. Daqui, você também pode visualização os arquivos assimilados, pré-visualização e fazer download do diagnóstico de erros ou fazer download do manifesto do arquivo.

A seção **[!UICONTROL Dataflow run errors]** exibe o código de erro, o número de registros que falharam e as informações que descrevem o erro.

Selecione Diagnóstico **[!UICONTROL de erro de]** Pré-visualização para ver mais informações sobre o erro de ingestão.

![Erros de execução de fluxo de dados](../assets/ui/monitor-sources/dataflow-run-errors.png)

O painel pré-visualização **[!UICONTROL do diagnóstico]** Error (Erro) é exibido. Essa tela exibe informações específicas sobre a falha de ingestão, incluindo o nome do arquivo, o código de erro, o nome da coluna na qual o erro ocorreu e uma descrição do erro.

Esta seção também inclui uma pré-visualização da coluna que contém o erro.

>[!IMPORTANT]
>
>Para ativar a pré-visualização **[!UICONTROL de diagnóstico de]** erro, é necessário ativar a assimilação **[!UICONTROL parcial]** e o diagnóstico **[!UICONTROL de]** erro ao configurar um fluxo de dados. Isso permitirá que o sistema verifique todos os registros ingeridos durante a execução do fluxo.

![diagnóstico de erro de pré-visualização](../assets/ui/monitor-sources/preview-error-diagnostics.png)

Depois de visualizar os erros, você pode selecionar **[!UICONTROL Download]** no painel de visão geral **[!UICONTROL do]** fluxo de dados para acessar o diagnóstico completo de erros e baixar o manifesto do arquivo. Consulte os documentos sobre diagnósticos [de](../../ingestion/batch-ingestion/partial.md#retrieve-errors) erros e o [download de metadados](../../ingestion/batch-ingestion/partial.md#download-metadata) para obter mais informações.

![diagnóstico de erro de pré-visualização](../assets/ui/monitor-sources/download.png)

Para obter mais informações sobre monitoramento de fluxos de dados e ingestão, consulte o tutorial sobre [monitoramento de fluxos de dados](../../ingestion/quality/monitor-data-ingestion.md)de fluxo contínuo.

## Próximas etapas

Ao seguir este tutorial, você acessou com êxito contas e fluxos de dados existentes na área de trabalho **[!UICONTROL Fontes]** . Os dados recebidos agora podem ser usados por [!DNL Platform] serviços de downstream, como [!DNL Real-time Customer Profile] e [!DNL Data Science Workspace]. Consulte os seguintes documentos para obter mais detalhes:

- [Visão geral do Perfil do cliente em tempo real](../../profile/home.md)
- [Visão geral da Análise do espaço de trabalho da Data Science](../../data-science-workspace/home.md)
