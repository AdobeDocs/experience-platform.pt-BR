---
title: Tipo de dados de informações de detalhes da mídia
description: Saiba mais sobre o tipo de dados Modelo de dados de experiência (XDM) de informações de detalhes de mídia.
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 1%

---

# [!UICONTROL Informações de detalhes de mídia] tipo de dados

[!UICONTROL Informações de detalhes de mídia] O é um tipo de dados padrão do Experience Data Model (XDM) que captura detalhes essenciais sobre eventos de reprodução de mídia. Use o [!UICONTROL Informações de detalhes de mídia] tipo de dados para capturar detalhes como a posição do indicador de reprodução no conteúdo, identificadores de sessão exclusivos e várias propriedades aninhadas relacionadas à sessão, entre outras. Esse tipo de dados fornece uma visão geral abrangente da experiência de reprodução, o que permite o rastreamento e a análise dos padrões de consumo de mídia e dos eventos associados durante as sessões de reprodução.

+++Selecione para exibir um diagrama do [!UICONTROL Informações de detalhes de mídia] tipo de dados.
![Um diagrama do [!UICONTROL Informações de detalhes de mídia] tipo de dados.](../images/data-types/media-details-information.png)
+++

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
| --------------------- | --------------- | --------- | ----------- |
| [!UICONTROL Indicador de reprodução] | `playhead` | inteiro | O indicador de reprodução representa a posição de reprodução atual no conteúdo de mídia. Para conteúdo ao vivo, indica o segundo atual do dia (0 &lt;= indicador de reprodução &lt; 86400). Para conteúdo gravado, ele reflete o segundo atual da duração do conteúdo (0 &lt;= indicador de reprodução &lt; duração do conteúdo). |
| [!UICONTROL ID da sessão de mídia] | `sessionID` | string | A ID de sessão de mídia identifica exclusivamente uma instância de um fluxo de conteúdo durante uma sessão de reprodução individual. Ele serve como um identificador exclusivo para rastrear e gerenciar a experiência de reprodução específica associada a um usuário ou visualizador. |
| [!UICONTROL Detalhes da sessão] | `sessionDetails` | [[!UICONTROL sessionDetails]](./session-details-information.md) | Os Detalhes da sessão englobam informações abrangentes associadas ao evento de experiência, oferecendo insights sobre as interações do usuário, duração e dados contextuais pertinentes à sessão de reprodução. |
| [!UICONTROL Detalhes de publicidade] | `advertisingDetails` | [[!UICONTROL advertisingDetails]](./advertising-details-information.md) | Os Detalhes do anúncio referem-se a informações específicas relacionadas a atividades de publicidade durante o evento de experiência. Isso inclui metadados de anúncios, especificações de direcionamento e métricas de desempenho. |
| [!UICONTROL Detalhes do pod de publicidade] | `advertisingPodDetails` | [[!UICONTROL advertisingPodDetails]](./advertising-pod-details-information.md) | Detalhes do pod de publicidade contêm informações sobre pods de publicidade no evento de experiência. Ele fornece insights sobre sequência de anúncios, conteúdo e métricas de envolvimento. |
| [!UICONTROL Detalhes do capítulo] | `chapterDetails` | [[!UICONTROL chapterDetails]](./chapter-details-information.md) | Detalhes do capítulo captura dados relacionados aos capítulos ou partes segmentadas do conteúdo. Ela fornece informações sobre marcadores de capítulo, linhas do tempo e metadados associados. |
| [!UICONTROL Detalhes do erro] | `errorDetails` | [[!UICONTROL errorDetails]](./error-details-information.md) | Detalhes do erro contêm informações relacionadas aos erros encontrados durante o evento de experiência. Isso inclui códigos de erro, descrições, carimbos de data e hora e dados contextuais relevantes. |
| [!UICONTROL Detalhes dos dados de Qoe] | `qoeDataDetails` | [[!UICONTROL qoeDataDetails]](./qoe-data-details-information.md) | Os Detalhes dos dados de QoE (Qualidade da experiência) capturam métricas relacionadas ao desempenho e dados de experiência do usuário. Ele fornece insights de qualidade, capacidade de resposta e interações do usuário. |
| [!UICONTROL Lista De Início De Estados] | `statesStart` | [[!UICONTROL playerStateData]](./player-state-data-information.md) | Início de estados fornece uma matriz para listar os estados no início do evento de experiência. Ele apresenta dados relacionados à reprodução, ações do usuário ou especificidades do conteúdo. |
| [!UICONTROL Fim Da Lista De Estados] | `statesEnd` | [[!UICONTROL playerStateData]](./player-state-data-information.md) | O fim dos estados fornece uma matriz para listar os estados na conclusão do evento de experiência. Ele contém detalhes sobre os estados finais de reprodução ou status do conteúdo. |
| [!UICONTROL Lista De Estados] | `states` | [[!UICONTROL playerStateData]](./player-state-data-information.md) | A propriedade States é uma matriz que captura vários estados durante o evento de experiência. Essa propriedade fornece dados sequenciais sobre reprodução, ações do usuário ou alterações de conteúdo. |
| [!UICONTROL Os metadados personalizados] | `customMetadata` | [[!UICONTROL customMetadataDetails]](./custom-metadata-details-information.md) | Os metadados personalizados contêm metadados adicionais ou definidos pelo usuário associados ao evento de experiência. Esses metadados permitem que dados personalizados ou específicos sejam incluídos no contexto do evento. |

{style="table-layout:auto"}

Para obter mais informações sobre o grupo de campos, consulte o [repositório XDM público](https://github.com/adobe/xdm/blob/master/components/datatypes/mediadetails.schema.json)
