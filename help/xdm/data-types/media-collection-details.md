---
title: Tipo de dados de detalhes da coleção de mídia
description: Saiba mais sobre o tipo de dados Modelo de dados de experiência (XDM) de Detalhes da coleção de mídia.
exl-id: 1faf60f7-6afb-4ce2-b50d-967776a57715
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 1%

---

# Tipo de dados [!UICONTROL Detalhes da Coleção de Mídia]

[!UICONTROL Detalhes da coleção de mídia] é um tipo de dados padrão do Experience Data Model (XDM) que captura detalhes essenciais sobre eventos de reprodução de mídia. Use o tipo de dados [!UICONTROL Detalhes da coleção de mídia] para capturar detalhes como a posição do indicador de reprodução no conteúdo, identificadores de sessão exclusivos e várias propriedades aninhadas relacionadas à sessão, entre outras. Esse tipo de dados fornece uma visão geral abrangente da experiência de reprodução, que permite o rastreamento e a análise dos padrões de consumo de mídia e dos eventos associados durante as sessões de reprodução.

>[!NOTE]
>
>Os campos da Coleção de mídia capturam dados e os enviam para outros serviços da Adobe para processamento adicional. Os campos de Relatórios de mídia são usados pelos serviços da Adobe para analisar os campos de Coleção de mídia enviados pelos usuários. Esses dados, juntamente com outras métricas específicas do usuário, são calculados e relatados.

+++Selecione para exibir um diagrama do tipo de dados [!UICONTROL Detalhes da coleção de mídia].
![Um diagrama do tipo de dados [!UICONTROL Informações detalhadas sobre a Coleção de Mídia].](../images/data-types/media-collection-details.png)
+++

| Nome de exibição | Propriedade | Eventos necessários para | Tipo de dados | Descrição |
| ------------------------------------ | ----------------------- | ---------------------------------------------------------- | --------- | ----------- |
| [!UICONTROL Detalhes do Advertising] | `advertisingDetails` | `adStart` | [[!UICONTROL advertisingDetails] - Coleção](./advertising-details-collection.md) | Os detalhes do Advertising se referem a informações específicas relacionadas a atividades de publicidade durante o evento de experiência. Isso inclui metadados de anúncios, especificações de direcionamento e métricas de desempenho. |
| [!UICONTROL Detalhes do pod do Advertising] | `advertisingPodDetails` | `adBreakStart` | [[!UICONTROL advertisingPodDetails] - Coleção](./advertising-pod-details-collection.md) | Detalhes do pod do Advertising contêm informações sobre pods de anúncios no evento de experiência. Ele fornece insights sobre sequência de anúncios, conteúdo e métricas de envolvimento. |
| [!UICONTROL Detalhes do capítulo] | `chapterDetails` | `chapterStart` | [[!UICONTROL chapterDetails] - Collection](./chapter-details-collection.md) | Detalhes do capítulo captura dados relacionados aos capítulos ou partes segmentadas do conteúdo. Ela fornece informações sobre marcadores de capítulo, linhas do tempo e metadados associados. |
| [!UICONTROL Detalhes do erro] | `errorDetails` | `error` | [[!UICONTROL DetalhesDoErro] - Coleção](./error-details-collection.md) | Detalhes do erro contêm informações relacionadas aos erros encontrados durante o evento de experiência. Isso inclui códigos de erro, descrições, carimbos de data e hora e dados contextuais relevantes. |
| [!UICONTROL Fim Da Lista De Estados] | `statesEnd` | Usado em `statesUpdate` | [[!UICONTROL statesEnd] - Coleção](./list-of-states-end-collection.md) | O fim dos estados fornece uma matriz para listar os estados na conclusão do evento de experiência. Ele contém detalhes sobre os estados finais de reprodução ou status do conteúdo. |
| [!UICONTROL Início Da Lista De Estados] | `statesStart` | Usado em `statesUpdate` | [[!UICONTROL statesStart] - Coleção](./list-of-states-start-collection.md) | Início de estados fornece uma matriz para listar os estados no início do evento de experiência. Ele apresenta dados relacionados à reprodução, ações do usuário ou especificidades do conteúdo. |
| [!UICONTROL Detalhes de Dados de Qoe] | `qoeDataDetails` | Opcional para todos | [[!UICONTROL qoeDataDetails] - Coleção](./qoe-data-details-collection.md) | Os Detalhes dos dados de QoE (Qualidade da experiência) capturam métricas relacionadas ao desempenho e dados de experiência do usuário. Ele fornece insights de qualidade, capacidade de resposta e interações do usuário. |
| [!UICONTROL Detalhes da sessão] | `sessionDetails` | `sessionStart` | [[!UICONTROL sessionDetails] - Coleção](./session-details-collection.md) | Os Detalhes da sessão englobam informações abrangentes associadas ao evento de experiência, oferecendo insights sobre as interações do usuário, duração e dados contextuais pertinentes à sessão de reprodução. |
| [!UICONTROL Os metadados personalizados] | `customMetadata` | Opcional para `sessionStart`, `adStart`, `sessionStart` | [[!UICONTROL customMetadataDetails] - Coleção](./custom-metadata-details-collection.md) | Os metadados personalizados contêm metadados adicionais ou definidos pelo usuário associados ao evento de experiência. Esses metadados permitem que dados personalizados ou específicos sejam incluídos no contexto do evento. |
| [!UICONTROL ID da Sessão de Mídia] | `sessionID` | Todos os eventos **exceto** `sessionStart` e conteúdo baixado. | sequência de caracteres | A ID de sessão de mídia identifica exclusivamente uma instância de um fluxo de conteúdo durante uma sessão de reprodução individual. Ele serve como um identificador exclusivo para rastrear e gerenciar a experiência de reprodução específica associada a um usuário ou visualizador.<br><em>Observação:<em>`sessionId` é enviado em todos os eventos, exceto para `sessionStart` e para todos os eventos baixados. |
| [!UICONTROL Indicador de reprodução] | `playhead` | Todos os eventos | inteiro | O indicador de reprodução representa a posição de reprodução atual no conteúdo de mídia. Para conteúdo ao vivo, indica o segundo atual do dia (0 &lt;= indicador de reprodução &lt; 86400). Para conteúdo gravado, ele reflete o segundo atual da duração do conteúdo (0 &lt;= indicador de reprodução &lt; duração do conteúdo). |

{style="table-layout:auto"}
