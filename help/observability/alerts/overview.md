---
keywords: Experience Platform;página inicial;tópicos populares;intervalo de datas
title: Visão geral de alertas
description: Saiba mais sobre os alertas na Adobe Experience Platform, incluindo a estrutura de como as regras de alerta são definidas.
feature: Alerts
exl-id: c38a93c6-1618-4ef9-8f94-41c7ab4af43c
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 3%

---

# Visão geral de alertas

>[!NOTE]
>
>Alertas não são aceitos em sandboxes de não produção. Para assinar alertas, você deve garantir que esteja usando uma sandbox de produção.

O Adobe Experience Platform permite assinar alertas baseados em eventos relacionados a atividades do Adobe Experience Platform. Os alertas reduzem ou eliminam a necessidade de sondar os [[!DNL Observability Insights] API](../api/overview.md) para verificar se um trabalho foi concluído, se uma determinada etapa em um fluxo de trabalho foi atingida ou se ocorreram erros.

Quando um determinado conjunto de condições em suas operações do Platform é atingido (como um problema em potencial quando o sistema ultrapassa um limite), o Platform pode enviar mensagens de alerta a qualquer usuário em sua organização que se inscreveu neles. Essas mensagens podem se repetir em um intervalo predefinido até que o alerta seja resolvido.

Este documento fornece uma visão geral dos alertas no Adobe Experience Platform, incluindo a estrutura de como as regras de alerta são definidas.

## Alertas únicos vs. alertas repetitivos

Os alertas da plataforma podem ser enviados uma vez ou repetidos em um intervalo predefinido até serem resolvidos. Os casos de uso de cada uma dessas opções devem diferir das seguintes maneiras:

| Alerta único | Alerta repetitivo |
| --- | --- |
| Não indica necessariamente um problema. | Indica um estado potencialmente indesejável. |
| Não se repete. | Pode se repetir se a condição anômala persistir. |
| São exemplos:<ul><li>A assimilação de dados foi concluída com sucesso.</li><li>Uma execução de consulta foi concluída.</li><li>Os dados foram excluídos.</li></ul> | São exemplos:<ul><li>A duração da assimilação excede o contrato de nível de serviço (SLA).</li><li>A ingestão diária não ocorreu nas últimas 24 horas.</li><li>A taxa de erro do processador de fluxo está acima do limite configurado.</li><li>O número total de perfis excede os direitos.</li></ul> |

{style="table-layout:auto"}

## Anatomia de um alerta

Um alerta pode ser dividido nos seguintes componentes:

| Componente | Descrição |
| --- | --- |
| **Métrica** | Uma capacidade de observação [métrica](../api/metrics.md#available-metrics) cujo valor aciona o alerta, como o número de eventos de assimilação de lote com falha (`timeseries.ingestion.dataset.batchfailed.count`). |
| **Condição** | Uma condição relacionada à métrica que aciona o alerta se for resolvido como verdadeiro, como uma métrica de contagem que excede um determinado número. Essa condição pode ser associada a uma janela de tempo predefinida. |
| **Janela** | (Opcional) A condição de um alerta pode ser restrita a uma janela de tempo predefinida. Por exemplo, um alerta pode ser disparado dependendo do número de lotes com falha nos últimos cinco minutos. |
| **Ação** | Quando um alerta é acionado, uma ação é executada. Especificamente, as mensagens são enviadas aos recipients aplicáveis por meio de um canal de delivery, como um webhook pré-configurado ou a interface do usuário do Experience Platform. |
| **Frequência** | (Opcional) Um alerta pode ser configurado para repetir sua ação em um intervalo definido se sua condição permanecer verdadeira ou não for resolvida. |

{style="table-layout:auto"}

## Receber e gerenciar alertas

Os alertas podem ser recebidos e gerenciados por meio de dois canais:

* [Eventos Adobe I/O](#events)
* [Interface do Platform](#ui)

### Eventos de E/S {#events}

Os alertas podem ser enviados para um webhook configurado para facilitar a automação eficiente do monitoramento de atividades. Para receber alertas via webhook, você deve registrar o webhook para alertas da Platform no Console do Adobe Developer. Consulte o guia sobre [assinatura de notificações de Adobe I/O Event](./subscribe.md) para obter etapas específicas.

### Interface do Platform {#ui}

A interface do usuário da Platform permite visualizar alertas recebidos e gerenciar regras de alerta. O vídeo a seguir fornece uma introdução a esses recursos.

>[!VIDEO](https://video.tv.adobe.com/v/336218?quality=12&learn=on)

Para trabalhar com alertas na interface do Platform, você deve ter as seguintes permissões de controle de acesso ativadas pelo Adobe Admin Console:

| Permissão | Descrição |
| --- | --- |
| Exibir alertas | Permite exibir as mensagens de alerta recebidas. |
| Exibir histórico de alertas* | Permite visualizar um histórico de alertas recebidos por meio da [!UICONTROL Alertas] guia. |
| Gerenciar alertas* | Permite ativar e desativar as regras de alerta por meio da [!UICONTROL Alertas] guia. |
| Resolver alertas* | Permite resolver alertas acionados por meio da [!UICONTROL Alertas] guia. |

{style="table-layout:auto"}

**Para acessar o [!UICONTROL Alertas] , você também deve receber a permissão Exibir alertas em combinação com uma das outras permissões.*

>[!NOTE]
>
>Para obter mais informações sobre como gerenciar permissões na Platform, consulte a [documentação de controle de acesso](../../access-control/ui/overview.md).

Com a permissão Exibir alertas, é possível exibir os alertas recebidos selecionando o ícone de sino (![Ícone de Campainha](../images/alerts/overview/icon.png)) no canto superior direito.

![](../images/alerts/overview/ui.png)

>[!NOTE]
>
> Selecione um alerta para navegar para um painel relacionado e obter informações mais detalhadas sobre por que o alerta foi acionado.

Além disso, a [!UICONTROL Alertas] A guia na interface do permite que usuários individuais assinem tipos de alertas específicos e que os administradores ativem ou desativem as regras de alerta completamente. Consulte a [Guia da interface do usuário](./ui.md) para obter mais informações sobre o gerenciamento de alertas.

## Próximas etapas

Ao ler este documento, você foi apresentado aos alertas da Plataforma e sua função no ecossistema da Plataforma. Consulte a documentação do processo vinculada a esta visão geral para saber como receber e gerenciar alertas.
