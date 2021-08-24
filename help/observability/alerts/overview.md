---
keywords: Experience Platform, home, tópicos populares, intervalo de datas
title: Visão geral dos alertas
description: Saiba mais sobre alertas no Adobe Experience Platform, incluindo a estrutura de como as regras de alerta são definidas.
source-git-commit: 5fabf5fa12f0a117a50bf694dea5118e5ea03500
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 3%

---


# Visão geral dos alertas

O Adobe Experience Platform permite assinar alertas baseados em eventos sobre atividades do Adobe Experience Platform. Os alertas reduzem ou eliminam a necessidade de pesquisar a [[!DNL Observability Insights] API](../api/overview.md) para verificar se uma tarefa foi concluída, se um determinado marco em um workflow foi atingido ou se ocorreram erros.

Quando um determinado conjunto de condições em suas operações da plataforma é atingido (como um possível problema quando o sistema viola um limite), a Platform pode enviar mensagens de alerta para qualquer usuário em sua organização que tenha se inscrito nelas. Essas mensagens podem se repetir em um intervalo de tempo predefinido até que o alerta seja resolvido.

Este documento fornece uma visão geral dos alertas no Adobe Experience Platform, incluindo a estrutura de como as regras de alerta são definidas.

## Alertas únicos vs. alertas repetitivos

Os alertas da plataforma podem ser enviados uma vez ou podem se repetir em um intervalo predefinido até que sejam resolvidos. Os casos de uso de cada uma dessas opções devem diferir das seguintes maneiras:

| Alerta único | Alerta de repetição |
| --- | --- |
| Não indica necessariamente um problema. | Indica um estado potencialmente indesejável. |
| Não se repete. | Pode se repetir se a condição anômala persistir. |
| São exemplos:<ul><li>A assimilação de dados foi concluída com êxito.</li><li>Uma execução de consulta foi concluída.</li><li>Os dados foram excluídos.</li></ul> | São exemplos:<ul><li>A duração da assimilação excede o contrato de nível de serviço (SLA).</li><li>A ingestão diária não ocorreu nas últimas 24 horas.</li><li>A taxa de erro do processador de fluxo está acima do limite configurado.</li><li>O número total de perfis está excedendo o direito.</li></ul> |

{style=&quot;table-layout:auto&quot;}

## Anatomia de um alerta

Um alerta pode ser detalhado nos seguintes componentes:

| Componente | Descrição |
| --- | --- |
| **Métrica** | Uma Observabilidade [métrica](../api/metrics.md#available-metrics) cujo valor aciona o alerta, como o número de eventos de ingestão em lote com falha (`timeseries.ingestion.dataset.batchfailed.count`). |
| **Condição** | Uma condição relacionada à métrica que aciona o alerta se ela for resolvida para true, como uma métrica de contagem que excede um determinado número. Essa condição pode ser associada a uma janela de tempo predefinida. |
| **Window** | (Opcional) A condição de um alerta pode ser restrita a uma janela de tempo predefinida. Por exemplo, um alerta pode ser acionado dependendo do número de lotes com falha nos últimos cinco minutos. |
| **Ação** | Quando um alerta é acionado, uma ação é executada. Especificamente, as mensagens são enviadas aos recipients aplicáveis por meio de um canal de delivery, como um webhook pré-configurado ou a interface do usuário do Experience Platform. |
| **Frequência** | (Opcional) Um alerta pode ser configurado para repetir sua ação em um intervalo definido, se a condição permanecer verdadeira ou não for resolvida. |

{style=&quot;table-layout:auto&quot;}

## Receber e gerenciar alertas

Os alertas podem ser recebidos e gerenciados por meio de dois canais:

* [Adobe I/O Events](#events)
* [Interface do usuário da plataforma](#ui)

### Eventos de E/S {#events}

Os alertas podem ser enviados para um webhook configurado para facilitar a automação eficiente do monitoramento de atividades. Para receber alertas via webhook, você deve registrar seu webhook para receber alertas da Platform no Console do desenvolvedor do Adobe. Consulte o guia em [assinar notificações de Adobe I/O Event](./subscribe.md) para obter etapas específicas.

### Interface do usuário da plataforma {#ui}

Para trabalhar com alertas na interface do usuário da plataforma, você deve ter as seguintes permissões de controle de acesso ativadas por meio do Adobe Admin Console:

| Permissão | Descrição |
| --- | --- |
| Visualizar alertas | Permite exibir mensagens de alerta recebidas. |
| Visualizar histórico de alertas* | Permite que você visualize um histórico de alertas recebidos por meio da guia [!UICONTROL Alerts]. |
| Gerenciar alertas* | Permite ativar e desativar regras de alerta por meio da guia [!UICONTROL Alerts]. |
| Resolver alertas* | Permite resolver alertas acionados por meio da guia [!UICONTROL Alerts] . |

{style=&quot;table-layout:auto&quot;}

**Para acessar a guia [!UICONTROL Alerts], você também deve receber a permissão Exibir Alertas em combinação com uma das outras permissões.*

>[!NOTE]
>
>Para obter mais informações sobre como gerenciar permissões no Platform, consulte a [documentação de controle de acesso](../../access-control/ui/overview.md).

Com a permissão Visualizar alertas , é possível visualizar os alertas recebidos selecionando o ícone de sino (![Ícone de sino](../images/alerts/overview/icon.png)) no canto superior direito.

![](../images/alerts/overview/ui.png)

Além disso, a guia [!UICONTROL Alerts] na interface do usuário permite que usuários individuais se inscrevam em tipos de alertas específicos e permite que administradores habilitem ou desabilitem completamente as regras de alertas. Consulte o [guia da interface do usuário](./ui.md) para obter mais informações sobre como gerenciar alertas.

## Próximas etapas

Ao ler este documento, você foi introduzido nos alertas da plataforma e sua função no ecossistema da plataforma. Consulte a documentação do processo vinculada a esta visão geral para saber como receber e gerenciar alertas.