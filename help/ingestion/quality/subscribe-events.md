---
keywords: Experience Platform, home, tópicos populares, notificações de assimilação de dados, notificações, eventos de assinatura, eventos de status de assimilação de dados, eventos de status, assinar, notificações de status;
solution: Experience Platform
title: Notificações de assimilação de dados
topic-legacy: overview
description: Para auxiliar no monitoramento do processo de ingestão, a Adobe Experience Platform possibilita a assinatura de um conjunto de eventos publicados por cada etapa do processo, notificando o status dos dados assimilados e quaisquer possíveis falhas.
exl-id: fd34e1ab-f6f6-44f0-88ee-7020e9322c39
source-git-commit: a455134a45137b171636d6525ce9124bc95f4335
workflow-type: tm+mt
source-wordcount: '681'
ht-degree: 1%

---

# Notificações de assimilação de dados

O processo de assimilação de dados no Adobe Experience Platform é composto por várias etapas. Depois de identificar os arquivos de dados que precisam ser assimilados em [!DNL Platform], o processo de assimilação é iniciado e cada etapa ocorre consecutivamente até que os dados sejam assimilados com êxito ou falhem. O processo de assimilação pode ser iniciado usando a [API de assimilação de dados do Adobe Experience Platform](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml) ou a interface do usuário [!DNL Experience Platform].

Os dados carregados em [!DNL Platform] devem passar por várias etapas para alcançar seu destino, o armazenamento de dados [!DNL Data Lake] ou [!DNL Real-time Customer Profile]. Cada etapa envolve processar os dados, validar os dados e armazenar os dados antes de passá-los para a próxima etapa. Dependendo da quantidade de dados assimilados, esse processo pode se tornar um processo demorado e sempre há uma chance de o processo falhar devido a erros de validação, semântica ou processamento. Em caso de falha, os problemas de dados precisam ser corrigidos e todo o processo de assimilação deve ser reiniciado usando os arquivos de dados corrigidos.

Para auxiliar no monitoramento do processo de assimilação, [!DNL Experience Platform] possibilita a assinatura de um conjunto de eventos publicados por cada etapa do processo, notificando o status dos dados assimilados e de possíveis falhas.

## Registrar um webhook para notificações de assimilação de dados

Para receber notificações de assimilação de dados, você deve usar [Console do desenvolvedor do Adobe](https://www.adobe.com/go/devs_console_ui) para registrar um webhook na integração do Experience Platform.

Siga o tutorial em [assinar [!DNL Adobe I/O Event] notificações](../../observability/alerts/subscribe.md) para obter etapas detalhadas sobre como fazer isso.

>[!IMPORTANT]
>
>Durante o processo de assinatura, selecione **[!UICONTROL Platform notifications]** como o provedor de eventos e selecione a assinatura de evento **[!UICONTROL Data ingestion notification]** quando solicitado.

## Receber notificações de assimilação de dados

Depois de registrar o webhook com êxito e os novos dados terem sido assimilados, você pode começar a receber notificações de eventos. Esses eventos podem ser exibidos usando o próprio webhook ou selecionando a guia **[!UICONTROL Debug Tracing]** na visão geral de registro de eventos do seu projeto no Console do desenvolvedor do Adobe.

O JSON a seguir é um exemplo de carga de notificação que seria enviada para o seu webhook no caso de um evento de ingestão em lote com falha:

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
| `event.xdm:datasetId` | A ID do conjunto de dados ao qual o evento de assimilação se aplica. |
| `event.xdm:eventCode` | Um código de status que indica o tipo de evento que foi acionado para o conjunto de dados. Consulte o [apêndice](#event-codes) para obter valores específicos e suas definições. |

Para visualizar o esquema completo das notificações de eventos, consulte o [repositório público do GitHub](https://github.com/adobe/xdm/blob/master/schemas/notifications/ingestion.schema.json).

## Próximas etapas

Depois de registrar as notificações [!DNL Platform] no seu projeto, você poderá visualizar os eventos recebidos da [!UICONTROL Visão geral do projeto]. Consulte o guia em [Rastreando eventos Adobe I/O](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/support/tracing.md) para obter instruções detalhadas sobre como rastrear seus eventos.

## Apêndice

A seção a seguir contém informações adicionais sobre a interpretação de cargas de notificação de assimilação de dados.

### Eventos de notificação de status disponíveis {#event-codes}

A tabela a seguir lista as notificações de status da assimilação de dados disponíveis que podem ser assinadas.

| Código do evento | Serviço de plataforma | Status | Descrição do evento |
| --- | ---------------- | ------ | ----------------- |
| `ing_load_success` | [!DNL Data Ingestion] | success | Um lote foi assimilado com êxito em um conjunto de dados dentro do [!DNL Data Lake]. |
| `ing_load_failure` | [!DNL Data Ingestion] | falha | Um lote não pôde ser assimilado em um conjunto de dados dentro do [!DNL Data Lake]. |
| `ps_load_success` | [!DNL Real-time Customer Profile] | success | Um lote foi assimilado com êxito no armazenamento de dados [!DNL Profile]. |
| `ps_load_failure` | [!DNL Real-time Customer Profile] | falha | Um lote não pôde ser assimilado no armazenamento de dados [!DNL Profile]. |
| `ig_load_success` | [!DNL Identity Service] | success | Os dados foram carregados com êxito no gráfico de identidade. |
| `ig_load_failure` | [!DNL Identity Service] | falha | Falha ao carregar dados no gráfico de identidade. |

>[!NOTE]
>
>Há apenas um tópico de evento fornecido para todas as notificações de assimilação de dados. Para distinguir entre diferentes status, o código do evento pode ser usado.
