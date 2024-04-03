---
title: Tipo de Dados de Coleta de Detalhes de Dados de QoE (Qualidade da Experiência)
description: Saiba mais sobre o tipo de dados QoE (Quality of Experience) Coleção de dados Tipo de dados Modelo de dados de experiência (XDM).
source-git-commit: e1c94635b691c68de6154d19e974bfdf2e250923
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 5%

---

# Tipo de dados Coleta de detalhes de dados da QoE (Qualidade da experiência)

[!UICONTROL Detalhes de dados de QoE] A coleção é um tipo de dados padrão do Experience Data Model (XDM) que fornece métricas detalhadas relacionadas à qualidade da experiência (QoE) durante a reprodução da mídia. Use o [!UICONTROL Detalhes de dados de QoE] Tipo de dados de coleção para capturar detalhes como informações de taxa de bits, taxas de quadros, eventos de buffering, quadros soltos, etc. Os campos de coleção de mídia capturam dados e os enviam para outros serviços da Adobe para processamento adicional. Esse tipo de dados permite a análise da qualidade da reprodução, permitindo insights sobre o desempenho da transmissão, experiência do usuário e possíveis problemas encontrados durante as sessões de reprodução.

+++Selecione para exibir o tipo de dados Detalhes do QoE.
![Um diagrama do tipo de dados Coleta de detalhes de dados de QoE (Qualidade da experiência).](../images/data-types/qoe-data-details-collection.png)
+++

>[!NOTE]
>
>Cada nome de exibição contém um link para informações adicionais sobre os parâmetros de áudio e vídeo. As páginas vinculadas contêm detalhes sobre os dados de anúncios de vídeo coletados pelo Adobe, valores de implementação, parâmetros de rede, relatórios e considerações importantes.

| Nome de exibição | Propriedade | Tipo de dados | Obrigatório | Descrição |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------|-----------|-----------|---------------------------------------------------------------------------------------|
| [[!UICONTROL Taxa de bits]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#average-bitrate) | `bitrate` | inteiro | Não | O valor da taxa de bits (em kbps). |
| [[!UICONTROL Queda de quadros]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#dropped-frames) | `droppedFrames` | inteiro | Não | A contagem total de quadros perdidos durante a reprodução. |
| [[!UICONTROL Quadros por segundo]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#frames-per-second) | `framesPerSecond` | inteiro | Não | A taxa de quadros do fluxo atual (em quadros por segundo). |
| [[!UICONTROL Hora de início]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#time-to-start-1) | `timeToStart` | inteiro | Não | Duração (em segundos) entre o carregamento e o início do vídeo. |

{style="table-layout:auto"}
