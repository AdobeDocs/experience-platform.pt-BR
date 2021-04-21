---
keywords: Experience Platform, home, tópicos populares, esquema, esquema, XDM, campos, esquemas, esquemas, medida, tipo de dados, tipo de dados, tipo de dados;
solution: Experience Platform
title: Tipo de dados da medida
topic-legacy: overview
description: Este documento fornece uma visão geral do tipo de dados Measure Experience Data Model (XDM).
exl-id: 5d6cc15d-63cf-4af5-9ae9-12c886dd6735
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 1%

---

# [!UICONTROL Measure] tipo de dados

[!UICONTROL Measure] é um tipo de dados padrão do Experience Data Model (XDM) que contém um ponto de dados quantificável concreto de uma métrica específica. Uma medida é composta de um identificador exclusivo e um valor.

<img src="../images/data-types/measure.PNG" width="500" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `id` | String | O identificador exclusivo desta medida. Nos casos de coleta de dados que utilizam canais de comunicação com perdas, como aplicativos móveis ou sites com funcionalidade offline nos quais não é possível garantir a transmissão de medidas, essa propriedade contém uma ID exclusiva e gerada pelo cliente da medida tomada. É uma prática recomendada fazer isto suficientemente longo para assegurar a aleatoriedade suficiente. <br><br> Se informações como carimbo de data e hora, ID do dispositivo, IP, endereço MAC ou outros valores potencialmente identificáveis pelo usuário forem incorporadas na geração do  `id`, o resultado deverá ser colocado em hash. Isso garante que nenhuma PII seja codificada no valor, pois o objetivo não é identificar um usuário ou dispositivo, mas a medida específica no tempo. |
| `value` | Duplo | O valor quantificável desta medida. |

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/data/measure.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/data/measure.schema.json)
