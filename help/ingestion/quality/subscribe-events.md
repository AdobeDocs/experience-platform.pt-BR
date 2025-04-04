---
keywords: Experience Platform;página inicial;tópicos populares;notificações de assimilação de dados;notificações;assinar eventos;status de assimilação de dados eventos;eventos de status;assinar;notificações de status;
solution: Experience Platform
title: Notificações de assimilação de dados
description: Para auxiliar no monitoramento do processo de assimilação, o Adobe Experience Platform permite assinar um conjunto de eventos publicados por cada etapa do processo, notificando você sobre o status dos dados assimilados e sobre possíveis falhas.
exl-id: fd34e1ab-f6f6-44f0-88ee-7020e9322c39
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 1%

---

# Notificações de assimilação de dados

O processo de assimilação de dados na Adobe Experience Platform é composto por várias etapas. Depois de identificar os arquivos de dados que precisam ser assimilados no [!DNL Experience Platform], o processo de assimilação começa e cada etapa ocorre consecutivamente até que os dados sejam assimilados com êxito ou falhem. O processo de assimilação pode ser iniciado usando a [API de assimilação em lote do Adobe Experience Platform](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/) ou a interface de usuário [!DNL Experience Platform].

Os dados carregados em [!DNL Experience Platform] devem passar por várias etapas para atingir seu destino, o [!DNL Data Lake] ou o armazenamento de dados [!DNL Real-Time Customer Profile]. Cada etapa envolve processar os dados, validá-los e armazená-los antes de passá-los para a próxima etapa. Dependendo da quantidade de dados que está sendo assimilada, esse processo pode se tornar demorado e há sempre uma chance de falha do processo devido a erros de validação, semântica ou processamento. No caso de uma falha, os problemas de dados precisam ser corrigidos e, em seguida, todo o processo de assimilação deve ser reiniciado usando os arquivos de dados corrigidos.

Para auxiliar no monitoramento do processo de assimilação, o [!DNL Experience Platform] permite assinar um conjunto de eventos publicados por cada etapa do processo, notificando você sobre o status dos dados assimilados e sobre possíveis falhas.

## Registrar um webhook para notificações de assimilação de dados

Para receber notificações de assimilação de dados, você deve usar o [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) para registrar um webhook na integração do Experience Platform.

Siga o tutorial em [assinatura de [!DNL Adobe I/O Event] notificações](../../observability/alerts/subscribe.md) para obter etapas detalhadas sobre como fazer isso.

>[!IMPORTANT]
>
>Durante o processo de assinatura, selecione **[!UICONTROL Notificações da plataforma]** como provedor de eventos e selecione a assinatura de eventos **[!UICONTROL Notificação de assimilação de dados]** quando solicitado.

## Receber notificações de assimilação de dados

Depois de registrar seu webhook com êxito e os novos dados tiverem sido assimilados, você poderá começar a receber notificações de evento. Esses eventos podem ser exibidos usando o próprio webhook ou selecionando a guia **[!UICONTROL Rastreamento de depuração]** na visão geral de registro de eventos do seu projeto no Adobe Developer Console.

O JSON a seguir é um exemplo de uma carga de notificação que seria enviada para o seu webhook no caso de falha de um evento de assimilação em lote:

```json
{
  "event_id": "93a5b11a-b0e6-4b29-ad82-81b1499cb4f2",
  "event": {
    "xdm:ingestionId": "01EGK8H8HF9JGFKNDCABHGA24G",
    "xdm:customerIngestionId": "01EGK8H8HF9JGFKNDCABHGA24G",
    "xdm:imsOrg": "{ORG_ID}",
    "xdm:completed": 1598374341560,
    "xdm:datasetId": "5e55b556c2ae4418a8446037",
    "xdm:eventCode": "ing_load_failure",
    "xdm:sandboxName": "prod",
    "sentTime": "1598374341595",
    "processStartTime": 1598374342614,
    "transformedTime": 1598374342621,
    "header": {
      "_adobeio": {
        "imsOrgId": "{ORG_ID}",
        "providerMetadata": "aep_observability_catalog_events",
        "eventCode": "platform_event"
      }
    }
  }
}
```

| Propriedade | Descrição |
| --- | --- |
| `event_id` | Uma ID exclusiva gerada pelo sistema para a notificação. |
| `event` | Um objeto que contém os detalhes do evento que acionou a notificação. |
| `event.xdm:datasetId` | A ID do conjunto de dados ao qual o evento de assimilação se aplica. |
| `event.xdm:eventCode` | Um código de status indicando o tipo de evento que foi acionado para o conjunto de dados. Consulte o [apêndice](#event-codes) para obter valores específicos e suas definições. |

Para exibir o esquema completo para notificações de eventos, consulte o [repositório público do GitHub](https://github.com/adobe/xdm/blob/master/schemas/notifications/ingestion.schema.json).

## Próximas etapas

Depois de registrar [!DNL Experience Platform] notificações ao seu projeto, você poderá exibir os eventos recebidos na [!UICONTROL Visão geral do projeto]. Consulte o manual sobre [Adobe I/O Events de rastreamento](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/support/tracing.md) para obter instruções detalhadas sobre como rastrear seus eventos.

## Apêndice

A seção a seguir contém informações adicionais sobre a interpretação das cargas de notificação de assimilação de dados.

### Eventos de notificação de status disponíveis {#event-codes}

A tabela a seguir lista as notificações de status de assimilação de dados disponíveis nas quais você pode se inscrever.

| Código do evento | Serviço Experience Platform | Status | Descrição do evento |
| --- | ---------------- | ------ | ----------------- |
| `ing_load_success` | [!DNL Data Ingestion] | success | Um lote foi assimilado com êxito em um conjunto de dados no [!DNL Data Lake]. |
| `ing_load_failure` | [!DNL Data Ingestion] | falha | Falha ao assimilar um lote em um conjunto de dados no [!DNL Data Lake]. |
| `ps_load_success` | [!DNL Real-Time Customer Profile] | success | Um lote foi assimilado com êxito no repositório de dados [!DNL Profile]. |
| `ps_load_failure` | [!DNL Real-Time Customer Profile] | falha | Falha ao assimilar um lote no repositório de dados [!DNL Profile]. |
| `ig_load_success` | [!DNL Identity Service] | success | Os dados foram carregados com sucesso no gráfico de identidade. |
| `ig_load_failure` | [!DNL Identity Service] | falha | Falha ao carregar dados no gráfico de identidade. |

>[!NOTE]
>
>Há apenas um tópico de evento fornecido para todas as notificações de assimilação de dados. Para distinguir entre status diferentes, o código do evento pode ser usado.
