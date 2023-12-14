---
title: Tipo de Dados de Detalhes de Dados de QoE (Qualidade da Experiência)
description: Saiba mais sobre o tipo de dados QoE (Qualidade da experiência) Informações Tipo de dados Modelo de dados da experiência (XDM).
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 5%

---

# Detalhes de dados de QoE (Qualidade da experiência) Tipo de dados Informações

[!UICONTROL Informações detalhadas de dados de QoE] O é um tipo de dados padrão do Experience Data Model (XDM) que fornece métricas detalhadas relacionadas à qualidade da experiência (QoE) durante a reprodução da mídia. Use o [!UICONTROL Informações detalhadas de dados de QoE] tipo de dados para capturar detalhes como informações de taxa de bits, taxas de quadros, eventos de buffer, quadros soltos, etc. Esse tipo de dados permite a análise da qualidade da reprodução, permitindo insights sobre o desempenho da transmissão, experiência do usuário e possíveis problemas encontrados durante as sessões de reprodução.

+++Selecione para exibir o tipo de dados Informações detalhadas sobre QoE.
![Um diagrama do tipo de dados QoE (Quality of Experience) Data Details Information.](../images/data-types/qoe-data-details-information.png)
+++

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
|----------------------------------------|----------------------------|-----------|--------------------------------------------------------------------------------------------------|
| [!UICONTROL Classificação da taxa média de bits] | `bitrateAverageBucket` | string | A taxa média de bits (em kbps) categorizada em intervalos predefinidos em intervalos de 100 kbps. |
| [!UICONTROL Taxa de bits] | `bitrate` | inteiro | O valor da taxa de bits (em kbps). |
| [!UICONTROL Taxa média de bits] | `bitrateAverage` | number | A taxa média de bits (em kbps, número inteiro). Calculado como uma média ponderada de valores de taxa de bits. |
| [!UICONTROL Fluxos impactados pela alteração da taxa de bits] | `hasBitrateChangeImpactedStreams` | booleano | Indica se os fluxos foram afetados pelas alterações da taxa de bits durante a reprodução. |
| [!UICONTROL Alterações na taxa de bits] | `bitrateChangeCount` | inteiro | A contagem total de alterações da taxa de bits durante a reprodução. |
| [!UICONTROL Fluxos impactados por quedas de quadros] | `hasDroppedFrameImpactedStreams` | booleano | Indica se os fluxos foram afetados pelos quadros ignorados durante a reprodução. |
| [!UICONTROL Queda de quadros] | `droppedFrames` | inteiro | A contagem total de quadros perdidos durante a reprodução. |
| [!UICONTROL Quedas antes de começar] | `isDroppedBeforeStart` | booleano | Indica se os usuários saíram do vídeo antes de seu início, independentemente dos anúncios. |
| [!UICONTROL Quadros por segundo] | `framesPerSecond` | inteiro | A taxa de quadros do fluxo atual (em quadros por segundo). |
| [!UICONTROL Hora de início] | `timeToStart` | inteiro | Duração (em segundos) entre o carregamento e o início do vídeo. |
| [!UICONTROL Fluxos impactados pelo buffer] | `hasBufferImpactedStreams` | booleano | Indica se os fluxos foram afetados pelo buffer durante a reprodução. |
| [!UICONTROL Eventos de buffer] | `bufferCount` | inteiro | A contagem de estados de buffer diferentes durante a reprodução. |
| [!UICONTROL Duração total do buffer] | `bufferTime` | inteiro | Tempo total (em segundos) gasto com buffering durante a reprodução. |
| [!UICONTROL Fluxos impactados por erros] | `hasErrorImpactedStreams` | booleano | Indica se os fluxos apresentaram erros durante a reprodução. |
| [!UICONTROL Erros] | `errorCount` | inteiro | A contagem total de erros que ocorreram durante a reprodução. |
| [!UICONTROL Interrupção de fluxos afetados] | `hasStallImpactedStreams` | booleano | Indica se os fluxos tiveram paralisação durante a reprodução. |
| [!UICONTROL Paralisação de eventos] | `stallCount` | inteiro | A contagem de eventos de paralisação durante a reprodução. |
| [!UICONTROL Duração total da paralisação] | `stallTime` | inteiro | O tempo total (em segundos) que a reprodução ficou paralisada durante a reprodução. |
| [!UICONTROL IDs de erro do Player SDK] | `playerSdkErrors` | matriz de strings | IDs de erro exclusivas geradas pelo SDK do reprodutor durante a reprodução. |
| [!UICONTROL IDs de erro externo] | `externalErrors` | matriz de strings | IDs de erro exclusivas de fontes externas, por exemplo, erros de CDN. |
| [!UICONTROL IDs de erro do SDK do Media] | `mediaSdkErrors` | matriz de strings | IDs de erro exclusivas geradas pelo SDK do Media durante a reprodução. |

{style="table-layout:auto"}

Para obter mais informações sobre o grupo de campos, consulte o [repositório XDM público](https://github.com/adobe/xdm/blob/master/components/datatypes/qoedatadetails.schema.json).

