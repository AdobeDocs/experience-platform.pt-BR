---
keywords: Experience Platform;home;popular topics;monitor accounts;monitor dataflows;data flows
description: Os conectores de origem na Adobe Experience Platform fornecem a capacidade de assimilar dados de origem externa de forma programada. Este tutorial fornece etapas para a exibição de contas e fluxos de dados existentes na área de trabalho Fontes.
solution: Experience Platform
title: Monitorar contas e fluxos de dados
topic: overview
translation-type: tm+mt
source-git-commit: a93b3a1980ca0f1d3a32257a923eb7ffc8896fd5
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 0%

---


# Monitorar contas e fluxos de dados na interface do usuário

Os conectores de origem na Adobe Experience Platform fornecem a capacidade de assimilar dados de origem externa de forma programada. Este tutorial fornece etapas para a exibição de contas e fluxos de dados existentes na área de trabalho [!UICONTROL Fontes] .

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

- [[!DNL Experience Data Model] (XDM) Sistema](../../../xdm/home.md): A estrutura padronizada pela qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   - [Noções básicas da composição](../../../xdm/schema/composition.md)do schema: Saiba mais sobre os elementos básicos dos schemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   - [Tutorial](../../../xdm/tutorials/create-schema-ui.md)do Editor de schemas: Saiba como criar schemas personalizados usando a interface do editor de Schemas.
- [[!DNL Perfil do cliente em tempo real]](../../../profile/home.md): Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

## Monitorar contas

Faça logon no [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar a área de trabalho **[!UICONTROL Fontes]** . A tela **[!UICONTROL Catálogo]** exibe várias fontes com as quais você pode criar contas e fluxos de dados. Cada fonte mostra o número de contas e fluxos de dados existentes associados a elas.

Selecione **[!UICONTROL Contas]** no cabeçalho superior para visualização contas existentes.

![catálogo](../../images/tutorials/monitor/catalog-accounts.png)

As páginas **[!UICONTROL Contas]** são exibidas. Nesta página há uma lista de contas visualizáveis, incluindo informações sobre a origem, o nome de usuário, o número de fluxos de dados e a data de criação.

Selecione o ícone de funil na parte superior esquerda para abrir a janela de classificação.

![account](../../images/tutorials/monitor/accounts-list.png)

O painel de classificação permite acessar contas de uma fonte específica. Selecione a fonte com a qual deseja trabalhar e selecione a conta na lista à direita.

![selecionar contas](../../images/tutorials/monitor/accounts-sort.png)

Na página **[!UICONTROL Contas]** , é possível visualização de uma lista de fluxos de dados ou conjuntos de dados de públicos alvos existentes associados à conta acessada.

![fluxo de dados](../../images/tutorials/monitor/dataflows.png)

## Monitorar fluxos de dados

Os fluxos de dados podem ser acessados diretamente da página **[!UICONTROL Catálogo]** sem exibir **[!UICONTROL Contas]**. Selecione **[!UICONTROL Fluxos de dados]** no cabeçalho superior para visualização de uma lista de fluxos de dados existentes.

![catálogo-dataflows](../../images/tutorials/monitor/catalog-dataflows.png)

Uma lista de fluxos de dados existentes é exibida. Nesta página há uma lista de fluxos de dados visualizáveis, incluindo informações sobre sua fonte, nome de usuário, número de fluxos de dados e status. Selecione o ícone de funil na parte superior esquerda para classificar.

![lista de dados](../../images/tutorials/monitor/dataflows-list.png)

O painel de classificação é exibido. Selecione a fonte que deseja acessar no menu de rolagem e selecione o fluxo de dados na lista à direita.

![sort-dataflows](../../images/tutorials/monitor/dataflows-sort.png)

A página de atividade **[!UICONTROL do]** Dataflow contém detalhes sobre o número de registros ingeridos e os registros falharam, bem como informações sobre o status e o tempo de processamento do dataflow. Selecione o ícone de calendário acima do fluxo de dados para ajustar o intervalo de tempo dos registros de ingestão.

![atividade de fluxo de dados](../../images/tutorials/monitor/dataflow-activity.png)

O calendário permite que você visualização os diferentes intervalos de tempo para registros ingeridos. Você pode selecionar uma das duas opções predefinidas **[!UICONTROL Últimos 7 dias]** ou **[!UICONTROL Últimos 30 dias]**. Como alternativa, você pode definir um período de tempo personalizado usando o calendário. Selecione seu período de tempo de escolha e selecione **[!UICONTROL Aplicar]** para continuar.

![calendário de fluxo](../../images/tutorials/monitor/flow-calendar.png)

Por padrão, a atividade **** Dataflow exibe o painel **[!UICONTROL Propriedades]** associado ao fluxo de dados. Selecione a execução de fluxo da lista para ver seus metadados associados, incluindo informações sobre sua ID de execução exclusiva.

Selecione start **[!UICONTROL de execução do]** Dataflow para acessar a visão geral **[!UICONTROL de execução do]** Dataflow.

![run](../../images/tutorials/monitor/run-metadata.png)

A visão geral **[!UICONTROL da execução do]** Fluxo de dados exibe informações sobre o fluxo de dados, incluindo seus metadados, o status da ingestão **[!UICONTROL parcial e o limite]** de **** Erro atribuído. O cabeçalho superior também inclui um resumo **[!UICONTROL de]** Erro. O resumo **[!UICONTROL de]** Erro contém o erro de nível superior específico que mostra em qual etapa o processo de ingestão encontrou um erro.

![visão geral da execução do dataflow](../../images/tutorials/monitor/dataflow-run-overview.png)

Consulte a tabela a seguir para obter os códigos de erro que podem ser vistos no resumo **** Erro.

| Código de erro | Mensagem de erro |
| ---------- | ----------- |
| `CONNECTOR-1001-500` | &quot;Ocorreu um problema com a atividade de cópia.&quot; |
| `CONNECTOR-2001-500` | &quot;Ocorreu um problema ao copiar da fonte Experience Platform para o conjunto de dados.&quot; |
| `CONNECTOR-3001-500` | &quot;Ocorreu um problema com o provedor de fluxo ao criar o lote usando a API de assimilação em massa.&quot; |

A metade inferior da tela contém informações sobre erros **[!UICONTROL de execução do]** Dataflow. Daqui, você também pode visualização os arquivos assimilados, pré-visualização e fazer download do diagnóstico de erros ou fazer download do manifesto do arquivo.

A seção **[!UICONTROL Dataflow run errors]** exibe o código **[!UICONTROL de]** erro, o número de registros que falharam e as informações que descrevem o erro.

Selecione Diagnóstico **[!UICONTROL de erro de]** Pré-visualização para ver mais informações sobre o erro de ingestão.

![Erros de execução de fluxo de dados](../../images/tutorials/monitor/dataflow-run-errors.png)

O painel pré-visualização **[!UICONTROL do diagnóstico]** Error (Erro) é exibido. Essa tela exibe informações específicas sobre a falha de ingestão, incluindo o nome **[!UICONTROL do]** arquivo, o código **[!UICONTROL de]** erro, o nome da coluna na qual o erro ocorreu e uma descrição do erro.

Esta seção também inclui uma pré-visualização da coluna que contém o erro.

>[!IMPORTANT]
>
>Para ativar a pré-visualização **[!UICONTROL de diagnóstico de]** erro, é necessário ativar a assimilação **[!UICONTROL parcial]** e o diagnóstico **[!UICONTROL de]** erro ao configurar um fluxo de dados. Isso permitirá que o sistema verifique todos os registros ingeridos durante a execução do fluxo.

![diagnóstico de erro de pré-visualização](../../images/tutorials/monitor/preview-error-diagnostics.png)

Depois de visualizar os erros, você pode selecionar **[!UICONTROL Download]** no painel de visão geral **[!UICONTROL do]** fluxo de dados para acessar o diagnóstico completo de erros e baixar o manifesto do arquivo. Consulte os documentos sobre diagnósticos [de](../../../ingestion/batch-ingestion/partial.md#retrieve-errors) erros e o [download de metadados](../../../ingestion/batch-ingestion/partial.md#download-metadata) para obter mais informações.

![diagnóstico de erro de pré-visualização](../../images/tutorials/monitor/download.png)

Para obter mais informações sobre monitoramento de fluxos de dados e ingestão, consulte o tutorial sobre [monitoramento de fluxos de dados](../../../ingestion/quality/monitor-data-flows.md)de fluxo contínuo.

## Próximas etapas

Ao seguir este tutorial, você acessou com êxito contas e fluxos de dados existentes na área de trabalho **[!UICONTROL Fontes]** . Os dados recebidos agora podem ser usados por [!DNL Platform] serviços de downstream, como [!DNL Real-time Customer Profile] e [!DNL Data Science Workspace]. Consulte os seguintes documentos para obter mais detalhes:

- [Visão geral do Perfil do cliente em tempo real](../../../profile/home.md)
- [Visão geral da Análise do espaço de trabalho da Data Science](../../../data-science-workspace/home.md)
