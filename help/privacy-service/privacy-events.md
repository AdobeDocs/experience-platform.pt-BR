---
keywords: Experience Platform, home, tópicos populares
solution: Experience Platform
title: Inscrever-se em eventos do Privacy Service
topic-legacy: privacy events
description: Saiba como assinar eventos do Privacy Service usando um webhook pré-configurado.
exl-id: 9bd34313-3042-46e7-b670-7a330654b178
source-git-commit: 82dea48c732b3ddea957511c22f90bbd032ed9b7
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 1%

---

# Inscrever-se em [!DNL Privacy Service Events]

[!DNL Privacy Service Events] são mensagens fornecidas pelo Adobe Experience Platform [!DNL Privacy Service], que aproveita os Adobe I/O Events enviados para um webhook configurado para facilitar a automação eficiente de solicitações de trabalhos. Eles reduzem ou eliminam a necessidade de pesquisar a variável [!DNL Privacy Service] API para verificar se uma tarefa foi concluída ou se um determinado marco em um fluxo de trabalho foi atingido.

No momento, há quatro tipos de notificações relacionadas ao ciclo de vida da solicitação de trabalho de privacidade:

| Tipo | Descrição |
| --- | --- |
| Tarefa concluída | Todos [!DNL Experience Cloud] os aplicativos foram relatados e o status geral ou global do trabalho foi marcado como concluído. |
| Erro de Trabalho | Um ou mais aplicativos relataram um erro ao processar a solicitação. |
| Produto concluído | Uma das aplicações associadas a esta tarefa concluiu o seu trabalho. |
| Erro do produto | Um dos aplicativos relatou um erro ao processar a solicitação. |

Este documento fornece etapas para configurar um registro de evento para [!DNL Privacy Service] notificações e como interpretar cargas de notificação.

## Introdução

Revise a seguinte documentação do Privacy Service antes de iniciar este tutorial:

* [Visão geral do Privacy Service](./home.md)
* [Guia da API do Privacy Service](./api/overview.md)

## Registre um webhook para [!DNL Privacy Service Events]

Para receber [!DNL Privacy Service Events], você deve usar o Console do desenvolvedor do Adobe para registrar um webhook em seu [!DNL Privacy Service] integração.

Siga o tutorial em [assinando com [!DNL I/O Event] notificações](../observability/alerts/subscribe.md) para obter etapas detalhadas sobre como fazer isso. Certifique-se de escolher **[!UICONTROL Privacy Service Events]** como seu provedor de eventos para acessar os eventos listados acima.

## Receber [!DNL Privacy Service Event] notificações

Depois de registrar com êxito seu webhook e os trabalhos de privacidade tiverem sido executados, você poderá começar a receber notificações de eventos. Esses eventos podem ser exibidos usando o próprio webhook ou selecionando o **[!UICONTROL Rastreamento de depuração]** na visão geral de registro de eventos do seu projeto no Console do desenvolvedor do Adobe.

![](images/privacy-events/debug-tracing.png)

O JSON a seguir é um exemplo de um [!DNL Privacy Service Event] carga de notificação que seria enviada para o seu webhook quando um dos aplicativos associados a um trabalho de privacidade tiver concluído seu trabalho:

```json
{
  "id":"b472e249-368b-4706-90f3-1d774713f827",
  "event_id":"b116f797-e50b-432e-9c65-189106a34820",
  "specversion":"0.2",
  "type":"com.adobe.platform.gdpr.productcomplete",
  "source":"https://ns.adobe.com/platform/gdpr",
  "time":"Wed Oct 23 18:52:32 GMT 2019",
  "data":{
    "imsOrg":"{IMS_ORG}",
    "value":{
      "jobId":"6f0f2b62-88a7-4515-ba05-432d9a7021c5",
      "message":"analytics.access.complete"
    }
  }
}
```

| Propriedade | Descrição |
| --- | --- |
| `id` | Uma ID exclusiva gerada pelo sistema para a notificação. |
| `type` | O tipo de notificação a ser enviada, contextualizando as informações fornecidas nos termos do `data`. Os valores potenciais incluem: <ul><li>`com.adobe.platform.gdpr.jobcomplete`</li><li>`com.adobe.platform.gdpr.joberror`</li><li>`com.adobe.platform.gdpr.productcomplete`</li><li>`com.adobe.platform.gdpr.producterror`</li></ul> |
| `time` | Um carimbo de data e hora de quando o evento ocorreu. |
| `data.value` | Contém informações adicionais sobre o que acionou a notificação: <ul><li>`jobId`: A ID do trabalho de privacidade que acionou a notificação.</li><li>`message`: Uma mensagem sobre o status específico da tarefa. Para `productcomplete` ou `producterror` notificações, este campo indica o aplicativo Experience Cloud em questão.</li></ul> |

## Próximas etapas

Este documento cobriu como registrar eventos do Privacy Service em um webhook configurado e como interpretar cargas de notificação. Para saber como rastrear tarefas de privacidade usando a interface do usuário, consulte o [Guia do usuário do Privacy Service](./ui/user-guide.md).
