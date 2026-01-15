---
keywords: Experience Platform;página inicial;tópicos populares;intervalo de datas
title: Visão geral de alertas
description: Saiba mais sobre os alertas na Adobe Experience Platform, incluindo a estrutura de como as regras de alerta são definidas.
feature: Alerts
exl-id: c38a93c6-1618-4ef9-8f94-41c7ab4af43c
source-git-commit: f33bcf982216d25e514992d5ebf978b5535abd77
workflow-type: tm+mt
source-wordcount: '791'
ht-degree: 12%

---

# Visão geral de alertas

>[!NOTE]
>
>Como os alertas são compatíveis com sandboxes de produção e desenvolvimento, você pode assiná-los em qualquer sandbox. Quando uma sandbox é redefinida, todos os alertas de assinatura também são redefinidos e, quando uma sandbox é excluída, todos os alertas de assinatura são excluídos.

A Adobe Experience Platform permite que você se inscreva para receber alertas baseados em eventos relacionados às atividades da Adobe Experience Platform. Os alertas reduzem ou eliminam a necessidade de pesquisar a [[!DNL Observability Insights] API](../api/overview.md) para verificar se um trabalho foi concluído, se um determinado marco em um fluxo de trabalho foi atingido ou se ocorreu algum erro.

Quando um determinado conjunto de condições em suas operações do Experience Platform é atingido (como um problema em potencial quando o sistema ultrapassa um limite), o Experience Platform pode enviar mensagens de alerta para qualquer usuário em sua organização que se inscreveu neles. Essas mensagens podem se repetir em um intervalo predefinido até que o alerta seja resolvido.

Este documento fornece uma visão geral dos alertas no Adobe Experience Platform, incluindo a estrutura de como as regras de alerta são definidas.

## Alertas únicos vs. alertas repetidos

Os alertas do Experience Platform podem ser enviados uma vez ou repetidos em um intervalo predefinido até serem resolvidos. Os casos de uso de cada uma dessas opções devem diferir das seguintes maneiras:

| Alerta único | Alerta repetitivo |
| --- | --- |
| Não indica necessariamente um problema. | Indica um estado potencialmente indesejável. |
| Não se repete. | Pode se repetir se a condição anômala persistir. |
| São exemplos:<ul><li>A assimilação de dados foi concluída com sucesso.</li><li>Uma execução de consulta foi concluída.</li><li>Os dados foram excluídos.</li></ul> | São exemplos:<ul><li>A duração da assimilação excede o contrato de nível de serviço (SLA).</li><li>A ingestão diária não ocorreu nas últimas 24 horas.</li><li>A taxa de erro do processador de fluxo está acima do limite configurado.</li></ul> |

{style="table-layout:auto"}

## Anatomia de um alerta

Um alerta pode ser dividido nos seguintes componentes:

| Componente | Descrição |
| --- | --- |
| **Métrica** | Uma [métrica](../api/metrics.md#available-metrics) de Observability cujo valor aciona o alerta, como o número de eventos de assimilação em lote com falha (`timeseries.ingestion.dataset.batchfailed.count`). |
| **Condição** | Uma condição relacionada à métrica que aciona o alerta se for resolvido como verdadeiro, como uma métrica de contagem que excede um determinado número. Essa condição pode ser associada a uma janela de tempo predefinida. |
| **Janela** | (Opcional) A condição de um alerta pode ser restrita a uma janela de tempo predefinida. Por exemplo, um alerta pode ser disparado dependendo do número de lotes com falha nos últimos cinco minutos. |
| **Ação** | Quando um alerta é acionado, uma ação é executada. Especificamente, as mensagens são enviadas aos recipients aplicáveis por meio de um canal de delivery, como um webhook pré-configurado ou a interface do usuário do Experience Platform. |
| **Frequência** | (Opcional) Um alerta pode ser configurado para repetir sua ação em um intervalo definido se sua condição permanecer verdadeira ou não for resolvida. |

{style="table-layout:auto"}

## Receber e gerenciar alertas

Os alertas podem ser recebidos e gerenciados por meio de dois canais:

* [Adobe I/O Events](#events)
* [Interface do usuário do Experience Platform](#ui)

### Eventos de E/S {#events}

Os alertas podem ser enviados a um webhook configurado para facilitar a automação eficiente do monitoramento de atividades. Para receber alertas via webhook, você deve registrar o webhook para alertas do Experience Platform no Adobe Developer Console. Consulte o manual sobre [assinatura de notificações de eventos do Adobe I/O](./subscribe.md) para obter as etapas específicas.

### Interface do usuário do Experience Platform {#ui}

A interface do usuário do Experience Platform permite visualizar alertas recebidos e gerenciar regras de alerta. O vídeo a seguir fornece uma introdução a esses recursos.

>[!VIDEO](https://video.tv.adobe.com/v/336218?quality=12&learn=on)

Para trabalhar com alertas na interface do usuário do Experience Platform, você deve ter as seguintes permissões de controle de acesso ativadas por meio do Adobe Admin Console:

| Permissão | Descrição |
| --- | --- |
| Exibir alertas | Permite exibir as mensagens de alerta recebidas. |
| Exibir histórico de alertas* | Permite exibir um histórico de alertas recebidos por meio da guia [!UICONTROL Alerts]. |
| Gerenciar alertas* | Permite ativar e desativar as regras de alerta por meio da guia [!UICONTROL Alerts]. |
| Resolver alertas* | Permite resolver alertas acionados por meio da guia [!UICONTROL Alerts]. |

{style="table-layout:auto"}

**Para acessar a guia [!UICONTROL Alerts], você também deve receber a permissão Exibir Alertas em combinação com uma das outras permissões.*

>[!NOTE]
>
>Para obter mais informações sobre como gerenciar permissões no Experience Platform, consulte a [documentação de controle de acesso](../../access-control/ui/overview.md).

Com a permissão Exibir Alertas, você pode exibir alertas recebidos selecionando o ícone de sino (![Ícone de sino](/help/images/icons/bell.png)) no canto superior direito.

![](../images/alerts/overview/ui.png)

>[!NOTE]
>
> Selecione um alerta para navegar para um painel relacionado e obter informações mais detalhadas sobre por que o alerta foi acionado.

Além disso, a guia [!UICONTROL Alerts] na interface do usuário permite que usuários individuais assinem tipos de alertas específicos e que administradores habilitem ou desabilitem regras de alertas completamente. Consulte o [guia da interface](./ui.md) para obter mais informações sobre como gerenciar alertas.

## Próximas etapas

Ao ler este documento, você foi apresentado aos alertas do Experience Platform e sua função no ecossistema da Experience Platform. Consulte a documentação do processo vinculada a esta visão geral para saber como receber e gerenciar alertas.
