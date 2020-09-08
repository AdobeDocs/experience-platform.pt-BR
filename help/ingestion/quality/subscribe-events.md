---
keywords: Experience Platform;home;popular topics;data ingestion notifications;notifications;subscribe events;data ingestion status events;status events;subscribe;status notifications;
solution: Experience Platform
title: Assinar eventos de ingestão de dados
topic: overview
translation-type: tm+mt
source-git-commit: 80a1694f11cd2f38347989731ab7c56c2c198090
workflow-type: tm+mt
source-wordcount: '621'
ht-degree: 1%

---


# Notificações de ingestão de dados

O processo de assimilação de dados no Adobe Experience Platform é composto de várias etapas. Depois que você identificar os arquivos de dados que precisam ser ingeridos, o processo de ingestão será iniciado e cada etapa ocorrerá consecutivamente até que os dados sejam ingeridos com êxito ou falhem. [!DNL Platform] O processo de ingestão pode ser iniciado usando a API [de ingestão de dados da](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml) Adobe Experience Platform ou a interface do [!DNL Experience Platform] usuário.

Os dados carregados em [!DNL Platform] devem passar por várias etapas para chegar ao destino, ao local [!DNL Data Lake] ou ao [!DNL Real-time Customer Profile] armazenamento de dados. Cada etapa envolve o processamento dos dados, a validação dos dados e o armazenamento dos dados antes de passá-los para a próxima etapa. Dependendo da quantidade de dados que está sendo ingerida, isso pode se tornar um processo demorado e sempre há uma chance de o processo falhar devido a erros de validação, semântica ou processamento. No evento de uma falha, os problemas de dados precisam ser corrigidos e todo o processo de ingestão deve ser reiniciado usando os arquivos de dados corrigidos.

Para auxiliar no monitoramento do processo de ingestão, [!DNL Experience Platform] torna possível assinar um conjunto de eventos publicados em cada etapa do processo, notificando o status dos dados ingeridos e de possíveis falhas.

## Registrar um webhook para notificações de ingestão de dados

Para receber notificações de ingestão de dados, você deve usar o Console [do desenvolvedor do](https://www.adobe.com/go/devs_console_ui) Adobe para registrar um webhook na integração do Experience Platform.

Siga o tutorial sobre como [assinar [!DNL Adobe I/O Event] as notificações](../../observability/notifications/subscribe.md) para obter etapas detalhadas sobre como fazer isso.

>[!IMPORTANT]
>
>Durante o processo de subscrição, selecione Notificações **[!UICONTROL da]** plataforma como o provedor do evento e selecione a subscrição de evento de notificação **[!UICONTROL de ingestão de]** dados quando solicitado.

## Receber notificações de ingestão de dados

Depois que você tiver registrado com êxito seu webhook e novos dados tiverem sido ingeridos, você poderá receber notificações de evento. Esses eventos podem ser visualizados usando o próprio webhook ou selecionando a guia Rastreamento **[!UICONTROL de]** depuração na visão geral de registro de eventos do seu projeto no Console do desenvolvedor do Adobe.

O seguinte JSON é um exemplo de uma carga de notificação que seria enviada para o seu webhook no caso de um evento de ingestão em lote com falha:

```json
{
  "event_id": "93a5b11a-b0e6-4b29-ad82-81b1499cb4f2",
  "event": {
    "xdm:ingestionId": "01EGK8H8HF9JGFKNDCABHGA24G",
    "xdm:customerIngestionId": "01EGK8H8HF9JGFKNDCABHGA24G",
    "xdm:imsOrg": "{IMS_ORG}",
    "xdm:completed": 1598374341560,
    "xdm:datasetId": "5e55b556c2ae4418a8446037",
    "xdm:eventCode": "ing_load_failure",
    "xdm:sandboxName": "prod",
    "sentTime": "1598374341595",
    "processStartTime": 1598374342614,
    "transformedTime": 1598374342621,
    "header": {
      "_adobeio": {
        "imsOrgId": "{IMS_ORG}",
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
| `event.xdm:datasetId` | A ID do conjunto de dados ao qual o evento de ingestão se aplica. |
| `event.xdm:eventCode` | Um código de status que indica o tipo de evento que foi acionado para o conjunto de dados. Consulte o [apêndice](#event-codes) para obter valores específicos e suas definições. |

Para visualização do schema completo para notificações de eventos, consulte o repositório [GitHub](https://github.com/adobe/xdm/blob/master/schemas/notifications/ingestion.schema.json)público.

## Próximas etapas

Depois de registrar [!DNL Platform] notificações para o seu projeto, você poderá visualização eventos recebidos da visão geral [!UICONTROL do]projeto. Consulte o guia sobre o [rastreamento de Eventos](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/support/tracing.md) de E/S de Adobe para obter instruções detalhadas sobre como rastrear seus eventos.

## Apêndice

A seção a seguir contém informações adicionais sobre a interpretação de cargas de notificação de ingestão de dados.

### Eventos de notificação de status disponíveis {#event-codes}

A tabela a seguir lista as notificações de status de ingestão de dados disponíveis que podem ser assinadas.

| Código do evento | Serviço de plataforma | Status | Descrição do Evento |
| --- | ---------------- | ------ | ----------------- |
| `ing_load_success` | [!DNL Data Ingestion] | success | Um lote foi assimilado com êxito em um conjunto de dados dentro do [!DNL Data Lake]. |
| `ing_load_failure` | [!DNL Data Ingestion] | falha | Falha ao assimilar um lote em um conjunto de dados dentro do [!DNL Data Lake]. |
| `ps_load_success` | [!DNL Real-time Customer Profile] | success | Um lote foi ingerido com êxito no repositório de [!DNL Profile] dados. |
| `ps_load_failure` | [!DNL Real-time Customer Profile] | falha | Falha ao assimilar um lote no repositório de [!DNL Profile] dados. |
| `ig_load_success` | [!DNL Identity Service] | success | Os dados foram carregados com êxito no gráfico de identidade. |
| `ig_load_failure` | [!DNL Identity Service] | falha | Falha ao carregar os dados no gráfico de identidade. |

>[!NOTE]
>
>Há apenas um tópico de evento fornecido para todas as notificações de ingestão de dados. Para distinguir entre diferentes status, é possível usar o código do evento.