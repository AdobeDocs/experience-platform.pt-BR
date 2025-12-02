---
keywords: Experience Platform;página inicial;tópicos populares;assimilação de dados;dados assimilados;streaming;visão geral;assimilação de streaming;latência;latência de streaming;
solution: Experience Platform
title: Visão geral da assimilação de fluxo
description: A assimilação de streaming para o Adobe Experience Platform fornece aos usuários um método para enviar dados de dispositivos cliente e do lado do servidor para o Experience Platform em tempo real.
exl-id: 851f15fd-7ac5-4a9f-934d-6b907057da87
source-git-commit: ea693cb4bb732c829d9a477cbd3dcb209da524f3
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 3%

---

# Visão geral da ingestão de streaming

A assimilação de streaming para o Adobe Experience Platform fornece aos usuários um método para enviar dados de dispositivos cliente e do lado do servidor para o [!DNL Experience Platform] em tempo real.

## O que você pode fazer com a assimilação por transmissão?

O Adobe Experience Platform permite gerar experiências coordenadas, consistentes e relevantes, gerando um [!DNL Real-Time Customer Profile] para cada cliente individual. A assimilação de streaming desempenha uma função importante na criação desses perfis, permitindo que você entregue dados do [!DNL Profile] no [!DNL Data Lake] com a menor latência possível.

O vídeo a seguir foi projetado para ajudar a entender a assimilação de streaming e descreve os conceitos acima.

>[!VIDEO](https://video.tv.adobe.com/v/31683?captions=por_br&quality=12&learn=on)

### Registros de perfil de fluxo e [!DNL ExperienceEvents]

Com a assimilação por transmissão, os usuários podem transmitir registros de perfil e [!DNL ExperienceEvents] para [!DNL Experience Platform] em segundos para ajudar a impulsionar a personalização em tempo real. Todos os dados enviados para as APIs de assimilação de streaming são automaticamente mantidos no [!DNL Data Lake].

Leia o [guia de criação de conexão de streaming](../tutorials/create-streaming-connection.md) para obter mais informações.

### Transmitir para conjuntos de dados

Depois de ter certeza de que seus dados estão limpos, você poderá habilitar seus conjuntos de dados para [!DNL Real-Time Customer Profile] e [!DNL Identity Service].

Para obter mais informações sobre como habilitar um conjunto de dados para [!DNL Profile] e [!DNL Identity Service], leia o [guia de configuração de um conjunto de dados](/help/profile/tutorials/dataset-configuration.md).

## Qual é a latência esperada para a assimilação por transmissão no Experience Platform?

>[!IMPORTANT]
>
>As garantias para assimilação por transmissão estão vinculadas ao direito de uso total de licença que corresponde a toda a organização. Além disso, o uso de dados em sandboxes de desenvolvimento é limitado a 10% do total de perfis. Para obter mais informações sobre direitos de uso de licença, leia o [guia de práticas recomendadas de gerenciamento de dados](/help/landing/license-usage-and-guardrails/data-management-best-practices.md). Para saber como definir limites para sua taxa de transferência de streaming, leia a [Visão geral da capacidade](../../landing/license-usage-and-guardrails/capacity.md).

| Destino | Latência esperada |
| --------- | ---------------- |
| Perfil do cliente em tempo real | &lt; 15 minutos no percentil 95 |
| Data lake | &lt; 60 minutos |

## Orientação de solicitação por segundos (RPS) sobre assimilação de streaming

A tabela abaixo exibe orientações sobre os limites de solicitação por segundos para assimilação de streaming.

| Limite de RPS | Notas |
| --- | --- |
| 1000 solicitações por segundo | Eles podem conter várias mensagens ao usar o ponto de extremidade `/collection/batch`. |
| 10000 mensagens individuais por segundo | As mensagens podem ser agrupadas em menos solicitações reais ao usar o ponto de extremidade `/collection/`. |

>[!IMPORTANT]
>
>O limite imposto torna-se de **60 solicitações por minuto** ao usar a validação síncrona como pretendido para fins de depuração.

## Extensão da Adobe Experience Platform

Você pode usar a extensão Adobe Experience Platform para criar uma nova conexão de transmissão. A extensão [!DNL Experience Platform] fornece ações para enviar sinais formatados em [!DNL Experience Data Model] (XDM) para assimilação em tempo real para [!DNL Experience Platform]. Visite a documentação da [Extensão do Experience Platform](/help/tags/extensions/client/web-sdk/overview.md) para obter mais informações.
