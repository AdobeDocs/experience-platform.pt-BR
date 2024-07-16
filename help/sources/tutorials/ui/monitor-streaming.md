---
keywords: Experience Platform;página inicial;tópicos populares;monitorar contas;monitorar fluxos de dados;fluxos de dados
description: Os conectores do Source no Adobe Experience Platform fornecem a capacidade de assimilar dados obtidos externamente de forma programada. Este tutorial fornece etapas para monitorar fluxos de dados de transmissão do espaço de trabalho Fontes.
title: Monitorar fluxos de dados para fontes de transmissão na interface
exl-id: b080e398-e71f-40bd-aea1-7ea3ce86b55d
source-git-commit: 647f2780798dcf55a68e156af3318924c352a442
workflow-type: tm+mt
source-wordcount: '1037'
ht-degree: 10%

---

# Monitorar fluxos de dados para fontes de transmissão na interface

Este tutorial aborda as etapas de monitoramento de fluxos de dados para fontes de transmissão usando o espaço de trabalho [!UICONTROL Fontes].

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fluxos de dados](../../../dataflows/home.md): os fluxos de dados são uma representação de trabalhos de dados que movem dados pela Plataforma. Os fluxos de dados são configurados em diferentes serviços, ajudando a mover dados dos conectores de origem para conjuntos de dados de destino, para [!DNL Identity] e [!DNL Profile] e para [!DNL Destinations].
   * [Execuções de fluxo de dados](../../notifications.md): as execuções de fluxo de dados são os trabalhos agendados recorrentes com base na configuração de frequência dos fluxos de dados selecionados.
* [Fontes](../../home.md): o Experience Platform permite que os dados sejam assimilados de várias fontes e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.
* [Sandboxes](../../../sandboxes/home.md): o Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

## Monitorar fluxos de dados para fontes de transmissão

Na interface da Platform, selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar o espaço de trabalho [!UICONTROL Fontes]. A tela [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conta.

Para exibir fluxos de dados existentes para fontes de transmissão, selecione **[!UICONTROL Fluxos de Dados]** no cabeçalho superior.

![catálogo](../../images/tutorials/monitor-streaming/catalog.png)

A página [!UICONTROL Fluxos de Dados] contém uma lista de todos os fluxos de dados existentes em sua organização, incluindo informações sobre seus dados de origem, nome da conta e status de execução do fluxo de dados.

Selecione o nome do fluxo de dados que deseja exibir.

![fluxos de dados](../../images/tutorials/monitor-streaming/dataflows.png)

A tabela a seguir contém mais informações sobre os status de execução do fluxo de dados:

| Status | Descrição |
| ------ | ----------- |
| Concluído | O status `Completed` indica que todos os registros da execução de fluxo de dados correspondente foram processados dentro do período de uma hora. Um status `Completed` ainda pode conter erros em execuções de fluxo de dados. |
| Sucesso | O status `Success` indica que todos os registros da execução de fluxo de dados correspondente foram processados dentro do período de uma hora e que não foram encontrados erros durante a execução do fluxo de dados. |
| Processamento | O status `Processing` indica que um fluxo de dados ainda não está ativo. Esse status geralmente é encontrado imediatamente após a criação de um novo fluxo de dados. |
| Erro | O status `Error` indica que o processo de ativação de um fluxo de dados foi interrompido. |
| Nenhuma execução | O status `No runs` indica que o fluxo de dados foi criado, mas nenhuma execução de fluxo de dados foi iniciada. |

A página [!UICONTROL Atividade do Fluxo de Dados] exibe informações específicas sobre o fluxo de dados de transmissão. O banner superior contém o número cumulativo de registros assimilados e falhas nos registros para todas as execuções de fluxo de dados de transmissão no intervalo de datas selecionado.

![atividade-fluxo-dados](../../images/tutorials/monitor-streaming/dataflow-activity.png)

Por padrão, os dados exibidos contêm taxas de assimilação dos últimos sete dias. Selecione **[!UICONTROL Últimos 7 dias]** para ajustar o intervalo de tempo dos registros exibidos.

Uma janela pop-up de calendário é exibida, fornecendo opções para intervalos de tempo de assimilação alternativos. Você pode configurar o intervalo de tempo de execução do fluxo de dados para exibir as execuções de fluxo dos sete dias anteriores ou dos últimos 30 dias. Como alternativa, configure o calendário interativo para definir um intervalo de tempo personalizado de sua escolha. Quando terminar, selecione **[!UICONTROL Aplicar]**.

![calendário](../../images/tutorials/monitor-streaming/calendar.png)

A metade inferior da página exibe informações sobre o número de registros recebidos, assimilados e com falha por execução de fluxo. Cada execução de fluxo é registrada em uma janela de hora em hora.

![execução do fluxo de dados](../../images/tutorials/monitor-streaming/dataflow-run.png)

### Métricas de execução de fluxo de dados {#dataflow-run-metrics}

>[!CONTEXTUALHELP]
>id="platform_sources_dataflow_records_received"
>title="Registros recebidos"
>abstract="A métrica Registros recebidos indica a contagem total de registros recebidos no fluxo de dados."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_dataflow_records_ingested"
>title="Registros assimilados"
>abstract="A métrica Registros assimilados indica a contagem total de registros assimilados no data lake."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_dataflow_records_failed"
>title="Registros com falha"
>abstract="A métrica Registros com falha indica a contagem total de registros que não foram assimilados no data lake devido a erros nos dados."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_dataflow_records_warnings"
>title="Registros com avisos"
>abstract="Os Registros com avisos indicam a contagem total de registros assimilados com avisos de transformação do mapeador. Todos os erros de transformação do mapeador são relatados como avisos e linhas que são parcialmente assimiladas são consideradas bem-sucedidas com um aviso"
>text="Learn more in documentation"

Cada execução de fluxo de dados individual mostra os seguintes detalhes:

* **[!UICONTROL Início da execução do fluxo de dados]**: a hora em que a execução do fluxo de dados começou.
* **[!UICONTROL Tempo de processamento]**: o tempo necessário para o processamento do fluxo de dados.
* **[!UICONTROL Registros Recebidos]**: o número total de registros recebidos no fluxo de dados de um conector de origem.
* **[!UICONTROL Registros Assimilados]**: A contagem total de registros assimilados em [!DNL Data Lake].
* **[!UICONTROL Registros com Avisos]**: a contagem total de registros com avisos que foram assimilados. Todos os erros de transformação do mapeador são relatados como avisos, e as linhas parcialmente assimiladas são rotuladas como `success` com um aviso. **Observação**: o suporte para assimilar registros com avisos está disponível somente para fontes de streaming.
* **[!UICONTROL Registros com Falha]**: o número de registros que não foram assimilados em [!DNL Data Lake] devido a erros nos dados.
* **[!UICONTROL Taxa de assimilação]**: a taxa de sucesso dos registros assimilados em [!DNL Data Lake]. Esta métrica é aplicável quando a [!UICONTROL Assimilação parcial] está habilitada.
* **[!UICONTROL Status]**: representa o estado em que o fluxo de dados está: [!UICONTROL Concluído] ou [!UICONTROL Processando]. [!UICONTROL Concluído] significa que todos os registros para a execução do fluxo de dados correspondente foram processados dentro do período de uma hora. [!UICONTROL Processando] significa que a execução do fluxo de dados ainda não foi concluída.

A página [!UICONTROL Visão geral da execução do fluxo de dados] contém informações adicionais sobre o fluxo de dados, como a ID de execução do fluxo de dados correspondente, o conjunto de dados de destino e a ID da organização.

Uma execução de fluxo com erros também contém o painel [!UICONTROL Erros de execução de fluxo de dados], que exibe o erro específico que levou à falha da execução, bem como a contagem total de registros que falharam.

![visão geral-execução-fluxo-dados](../../images/tutorials/monitor-streaming/dataflow-run-overview.png)

### Exibir registros com avisos {#warnings}

[!UICONTROL Registros com avisos] exibe uma lista de avisos de transformação do mapeador que ocorreram durante a execução do fluxo. As linhas parcialmente assimiladas são consideradas bem-sucedidas e são anexadas com avisos se algum erro de transformação do mapeador for encontrado.

Por padrão, todos os erros de transformação do mapeador são considerados como avisos, exceto se forem qualquer um dos seguintes:

* Erros de sintaxe
* Referências a atributos que não existem
* Uma incompatibilidade de tipos de dados XDM

Para exibir o diagnóstico de erro, selecione **[!UICONTROL Visualizar diagnóstico de erro]**.

![registros-com-avisos](../../images/tutorials/monitor-streaming/records-with-warnings.png)

A janela [!UICONTROL Visualização do diagnóstico de erro] permite visualizar até 100 erros e/ou avisos relacionados à execução do fluxo de dados. Aqui, você também pode baixar o manifesto de falha de assimilação para obter mais informações, usando a API [!DNL Data Access].

![diagnóstico](../../images/tutorials/monitor-streaming/diagnostics.png)

## Próximas etapas

Ao seguir este tutorial, você usou com êxito o espaço de trabalho [!UICONTROL Fontes] para monitorar seus fluxos de dados de transmissão e identificar os erros que levaram a qualquer falha nos fluxos de dados. Consulte os seguintes documentos para obter mais informações:

* [Visão geral das fontes](../../home.md)
* [Visão geral dos fluxos de dados](../../../dataflows/home.md)
