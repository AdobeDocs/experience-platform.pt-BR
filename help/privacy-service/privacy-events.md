---
keywords: Experience Platform;página inicial;tópicos populares
solution: Experience Platform
title: Inscrever-se em eventos Privacy Service
description: Saiba como se inscrever em eventos Privacy Service usando um webhook pré-configurado.
exl-id: 9bd34313-3042-46e7-b670-7a330654b178
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 2%

---

# Assinar [!DNL Privacy Service Events]

[!DNL Privacy Service Events] são mensagens fornecidas pelo Adobe Experience Platform [!DNL Privacy Service], que aproveita os Adobe I/O Events enviados para um webhook configurado para facilitar a automação eficiente da solicitação de trabalho. Eles reduzem ou eliminam a necessidade de sondar a API [!DNL Privacy Service] para verificar se um trabalho foi concluído ou se uma determinada etapa em um fluxo de trabalho foi atingida.

Atualmente, existem quatro tipos de notificações relacionadas ao ciclo de vida da solicitação de acesso a dados pessoais:

| Tipo | Descrição |
| --- | --- |
| Trabalho concluído | Todos os aplicativos [!DNL Experience Cloud] foram reportados de volta e o status geral ou global do trabalho foi marcado como concluído. |
| Erro de tarefa | Um ou mais aplicativos relataram um erro ao processar a solicitação. |
| Produto completo | Um dos aplicativos associados a este trabalho concluiu seu trabalho. |
| Erro de produto | Um dos aplicativos relatou um erro ao processar a solicitação. |

Este documento fornece etapas para configurar um registro de evento para [!DNL Privacy Service] notificações e como interpretar cargas de notificação.

## Introdução

Consulte a documentação do Privacy Service a seguir antes de iniciar este tutorial:

* [Visão geral do Privacy Service](./home.md)
* [Guia da API do Privacy Service](./api/overview.md)

## Registrar um webhook em [!DNL Privacy Service Events]

Para receber [!DNL Privacy Service Events], você deve usar o Adobe Developer Console para registrar um webhook na integração do [!DNL Privacy Service].

Siga o tutorial em [assinatura de notificações do [!DNL I/O Event]](../observability/alerts/subscribe.md) para obter etapas detalhadas sobre como fazer isso. Escolha **[!UICONTROL Privacy Service Events]** como seu provedor de eventos para acessar os eventos listados acima.

## Receber [!DNL Privacy Service Event] notificações

Depois de registrar com êxito o webhook e os trabalhos de privacidade serem executados, você poderá começar a receber notificações de evento. Esses eventos podem ser exibidos usando o próprio webhook ou selecionando a guia **[!UICONTROL Rastreamento de depuração]** na visão geral de registro de eventos do seu projeto no Adobe Developer Console.

![](images/privacy-events/debug-tracing.png)

O JSON a seguir é um exemplo de uma carga de notificação [!DNL Privacy Service Event] que será enviada para o seu webhook quando um dos aplicativos associados a um trabalho de privacidade tiver concluído o trabalho:

```json
{
  "id":"b472e249-368b-4706-90f3-1d774713f827",
  "event_id":"b116f797-e50b-432e-9c65-189106a34820",
  "specversion":"0.2",
  "type":"com.adobe.platform.gdpr.productcomplete",
  "source":"https://ns.adobe.com/platform/gdpr",
  "time":"Wed Oct 23 18:52:32 GMT 2019",
  "data":{
    "imsOrg":"{ORG_ID}",
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
| `type` | O tipo de notificação que está sendo enviada, fornecendo contexto às informações fornecidas em `data`. Os valores potenciais incluem: <ul><li>`com.adobe.platform.gdpr.jobcomplete`</li><li>`com.adobe.platform.gdpr.joberror`</li><li>`com.adobe.platform.gdpr.productcomplete`</li><li>`com.adobe.platform.gdpr.producterror`</li></ul> |
| `time` | Um carimbo de data e hora de quando o evento ocorreu. |
| `data.value` | Contém informações adicionais sobre o que acionou a notificação: <ul><li>`jobId`: a ID do trabalho de privacidade que disparou a notificação.</li><li>`message`: uma mensagem relacionada ao status específico do trabalho. Para `productcomplete` ou `producterror` notificações, este campo indica o aplicativo Experience Cloud em questão.</li></ul> |

## Próximas etapas

Este documento abordou como registrar eventos Privacy Service em um webhook configurado e como interpretar cargas de notificação. Para saber como rastrear processos de privacidade usando a interface do usuário, consulte o [guia do usuário do Privacy Service](./ui/user-guide.md).
