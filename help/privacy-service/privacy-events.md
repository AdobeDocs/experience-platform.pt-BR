---
keywords: Experience Platform;home;populares tópicos
solution: Experience Platform
title: Inscrever-se em Eventos Privacy Service
topic: privacy events
description: Saiba como assinar eventos de Privacy Service usando um webhook pré-configurado.
translation-type: tm+mt
source-git-commit: 2b919a3b6cbbd59521874cfd2d11e20de3077740
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 1%

---


# Assine [!DNL Privacy Service Events]

[!DNL Privacy Service Events] são mensagens fornecidas pela Adobe Experience Platform  [!DNL Privacy Service], que aproveitam Eventos Adobe I/O enviados para um webhook configurado para facilitar a automação eficiente de solicitações de trabalhos. Eles reduzem ou eliminam a necessidade de pesquisar a API [!DNL Privacy Service] para verificar se um trabalho foi concluído ou se um determinado marco em um fluxo de trabalho foi atingido.

Existem atualmente quatro tipos de notificações relacionadas ao ciclo de vida da solicitação de trabalho de privacidade:

| Tipo | Descrição |
| --- | --- |
| Tarefa concluída | Todos os aplicativos [!DNL Experience Cloud] reportaram e o status geral ou global do trabalho foi marcado como concluído. |
| Erro de trabalho | Um ou mais aplicativos relataram um erro ao processar a solicitação. |
| Produto concluído | Uma das aplicações associadas a esta tarefa concluiu o seu trabalho. |
| Erro do produto | Um dos aplicativos relatou um erro ao processar a solicitação. |

Este documento fornece etapas para configurar um registro de evento para notificações [!DNL Privacy Service] e como interpretar as cargas de notificação.

## Introdução

Consulte a documentação de Privacy Service antes de iniciar este tutorial:

* [Visão geral do Privacy Service](./home.md)
* [Guia do desenvolvedor da API Privacy Service](./api/getting-started.md)

## Registrar um webhook em [!DNL Privacy Service Events]

Para receber [!DNL Privacy Service Events], você deve usar o Console do desenvolvedor do Adobe para registrar um webhook em sua integração [!DNL Privacy Service].

Siga o tutorial em [inscrevendo-se em [!DNL I/O Event] notifications](../observability/notifications/subscribe.md) para obter etapas detalhadas sobre como fazer isso. Certifique-se de escolher **[!UICONTROL Eventos de Privacy Service]** como provedor de eventos para acessar os eventos listados acima.

## Receber notificações [!DNL Privacy Service Event]

Depois que você tiver registrado com êxito seu webhook e os trabalhos de privacidade tiverem sido executados, você poderá start recebendo notificações de evento. Esses eventos podem ser visualizados usando o próprio webhook ou selecionando a guia **[!UICONTROL Rastreamento de depuração]** na visão geral de registro de eventos do seu projeto no Console do desenvolvedor do Adobe.

![](images/privacy-events/debug-tracing.png)

O JSON a seguir é um exemplo de uma carga de notificação [!DNL Privacy Service Event] que seria enviada ao seu webhook quando um dos aplicativos associados a um trabalho de privacidade tiver concluído seu trabalho:

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
| `type` | O tipo de notificação que está sendo enviada, dando contexto às informações fornecidas em `data`. Os valores potenciais incluem: <ul><li>`com.adobe.platform.gdpr.jobcomplete`</li><li>`com.adobe.platform.gdpr.joberror`</li><li>`com.adobe.platform.gdpr.productcomplete`</li><li>`com.adobe.platform.gdpr.producterror`</li></ul> |
| `time` | Um carimbo de data e hora de quando o evento ocorreu. |
| `data.value` | Contém informações adicionais sobre o que acionou a notificação: <ul><li>`jobId`: A ID do trabalho de privacidade que acionou a notificação.</li><li>`message`: Uma mensagem relacionada ao status específico da tarefa. Para notificações `productcomplete` ou `producterror`, esse campo indica o aplicativo Experience Cloud em questão.</li></ul> |

## Próximas etapas

Este documento abordou como registrar Eventos Privacy Service a um webhook configurado e como interpretar as cargas de notificação. Para saber como rastrear trabalhos de privacidade usando a interface do usuário, consulte o [guia do usuário do Privacy Service](./ui/user-guide.md).