---
title: Tipo de dados de detalhes de relatórios de mídia
description: Saiba mais sobre o tipo de dados Modelo de dados de experiência (XDM) dos Detalhes de relatórios de mídia.
exl-id: e8bf20a9-9ac0-4339-8200-5d6d9328ce3b
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 1%

---

# [!UICONTROL Detalhes de Relatórios de Mídia] tipo de dados

>[!NOTE]
>
>Os campos da Coleção de mídia capturam dados e os enviam para outros serviços da Adobe para processamento adicional. Os campos de Relatórios de mídia são usados pelos serviços da Adobe para analisar os campos de Coleção de mídia enviados pelos usuários. Esses dados, juntamente com outras métricas específicas do usuário, são calculados e relatados.

[!UICONTROL Detalhes de Relatórios de Mídia] é um tipo de dados padrão do Experience Data Model (XDM) que captura detalhes essenciais sobre eventos de reprodução de mídia. Use o tipo de dados [!UICONTROL Detalhes de Relatórios de Mídia] para capturar detalhes como a posição do indicador de reprodução no conteúdo, identificadores de sessão exclusivos e várias propriedades aninhadas relacionadas à sessão, entre outras. Esse tipo de dados fornece uma visão geral abrangente da experiência de reprodução, que permite o rastreamento e a análise dos padrões de consumo de mídia e dos eventos associados durante as sessões de reprodução.

>[!NOTE]
>
>Os campos mencionados abaixo não são usados diretamente para criar solicitações. Em vez disso, a coleção de campos enviados para o Adobe Experience Platform ou o Adobe Analytics é montada a partir dos dados de solicitação, e as métricas são incorporadas ou processadas pela infraestrutura do servidor. Embora a Experience Platform colete vários tipos de eventos de usuário, os relatórios retornados a você focalizam eventos específicos, como `media.sessionStart`, `media.adStart` e `media.sessionComplete`. Isso significa que, embora você transmita 12 tipos de eventos durante a coleta, seus relatórios só apresentarão detalhamentos baseados nos cinco eventos listados abaixo.

+++Selecione para exibir um diagrama do tipo de dados [!UICONTROL Detalhes de Relatórios de Mídia].
![Um diagrama do tipo de dados [!UICONTROL Detalhes de Relatórios de Mídia].](../images/data-types/media-reporting-details.png)
+++

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
| --------------------- | --------------- | --------- | ----------- |
| [!UICONTROL Detalhes do Advertising] | `advertisingDetails` | [[!UICONTROL advertisingDetails]](./advertising-details-reporting.md) | Os detalhes do Advertising se referem a informações específicas relacionadas a atividades de publicidade durante o evento de experiência. Isso inclui metadados de anúncios, especificações de direcionamento e métricas de desempenho. |
| [!UICONTROL Detalhes do pod do Advertising] | `advertisingPodDetails` | [[!UICONTROL advertisingPodDetails]](./advertising-pod-details-reporting.md) | Detalhes do pod do Advertising contêm informações sobre pods de anúncios no evento de experiência. Ele fornece insights sobre sequência de anúncios, conteúdo e métricas de envolvimento. |
| [!UICONTROL Detalhes do capítulo] | `chapterDetails` | [[!UICONTROL DetalhesDoCapítulo]](./chapter-details-reporting.md) | Detalhes do capítulo captura dados relacionados aos capítulos ou partes segmentadas do conteúdo. Ela fornece informações sobre marcadores de capítulo, linhas do tempo e metadados associados. |
| [!UICONTROL Lista De Estados] | `states` | [[!UICONTROL playerStateData]](./player-state-data-reporting.md) | A propriedade States é uma matriz que captura vários estados durante o evento de experiência. Essa propriedade fornece dados sequenciais sobre reprodução, ações do usuário ou alterações de conteúdo. |
| [!UICONTROL Detalhes de Dados de Qoe] | `qoeDataDetails` | [[!UICONTROL DetalhesDeDadosDeQoe]](./qoe-data-details-reporting.md) | Os Detalhes dos dados de QoE (Qualidade da experiência) capturam métricas relacionadas ao desempenho e dados de experiência do usuário. Ele fornece insights de qualidade, capacidade de resposta e interações do usuário. |
| [!UICONTROL Detalhes da sessão] | `sessionDetails` | [[!UICONTROL DetalhesDaSessão]](./session-details-reporting.md) | Os Detalhes da sessão englobam informações abrangentes associadas ao evento de experiência, oferecendo insights sobre as interações do usuário, duração e dados contextuais pertinentes à sessão de reprodução. |
| [!UICONTROL Os metadados personalizados] | `customMetadata` | [[!UICONTROL customMetadataDetails]](./custom-metadata-details-reporting.md) | Os metadados personalizados contêm metadados adicionais ou definidos pelo usuário associados ao evento de experiência. Esses metadados permitem que dados personalizados ou específicos sejam incluídos no contexto do evento. |
| [!UICONTROL Indicador de reprodução] | `playhead` | inteiro | O indicador de reprodução representa a posição de reprodução atual no conteúdo de mídia. Para conteúdo ao vivo, indica o segundo atual do dia (0 &lt;= indicador de reprodução &lt; 86400). Para conteúdo gravado, ele reflete o segundo atual da duração do conteúdo (0 &lt;= indicador de reprodução &lt; duração do conteúdo). |

{style="table-layout:auto"}
