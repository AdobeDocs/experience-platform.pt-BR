---
keywords: Experience Platform;início;tópicos populares;esquema;Esquema;XDM;campos;esquemas;Esquemas;medida;tipo de dados;tipo de dados;tipo de dados;
solution: Experience Platform
title: Tipo de Dados de Medida
description: Este documento fornece uma visão geral do tipo de dados Measure Experience Data Model (XDM).
exl-id: 5d6cc15d-63cf-4af5-9ae9-12c886dd6735
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 1%

---

# [!UICONTROL Medir] tipo de dados

[!UICONTROL Medir] é um tipo de dados padrão do Experience Data Model (XDM) que contém um ponto de dados quantificável concreto de uma métrica específica. Uma medida é composta de um identificador exclusivo e um valor.

<img src="../images/data-types/measure.PNG" width="500" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `id` | String | O identificador exclusivo desta medida. No caso de recolha de dados através de canais de comunicação com perdas, como aplicações móveis ou sítios Web com funcionalidade offline, em que a transmissão de medidas não pode ser assegurada, esta propriedade contém uma ID única gerada pelo cliente da medida tomada. A prática recomendada é tornar isso suficientemente longo para garantir um grau suficiente de aleatoriedade. <br><br> Se informações como carimbo de data e hora, ID do dispositivo, IP, endereço MAC ou outros valores potencialmente identificáveis pelo usuário forem incorporadas na geração do `id`, o resultado deve ser transformado em hash. Isso garante que nenhuma PII seja codificada no valor, pois o objetivo não é identificar um usuário ou dispositivo, mas a medida específica no tempo. |
| `value` | Duplo | O valor quantificável dessa medida. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/data/measure.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/data/measure.schema.json)
