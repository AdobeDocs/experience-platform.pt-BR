---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;campos;schemas;medição;datatype;data-type;data type;Schema;home;popular topics;;XDM;fields;details;measurement;datatype;data-type;data type;data type;
solution: Experience Platform
title: Tipo de dados de medida
topic: overview
description: Este documento fornece uma visão geral do tipo de dados do Modelo de Dados de Experiência de Medida (XDM).
translation-type: tm+mt
source-git-commit: d282ea5526a05b28c6a82470eabf23e44d1fb420
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 1%

---


# [!UICONTROL Tipo ] de dados de medida

 Medida é um tipo de dados padrão do Modelo de Dados de Experiência (XDM) que contém um ponto de dados quantificável concreto de uma métrica específica. Uma medida é composta de um identificador exclusivo e um valor.

<img src="../images/data-types/measure.PNG" width="500" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `id` | String | O identificador exclusivo desta medida. Nos casos de coleta de dados que usam canais de comunicação com perdas, como aplicativos móveis ou sites com funcionalidade offline nos quais não é possível garantir a transmissão de medidas, essa propriedade contém uma ID exclusiva e gerada pelo cliente da medida tomada. É a melhor prática fazer com que isto seja suficientemente longo para garantir uma aleatoriedade suficiente. <br><br> Se informações como carimbo de data e hora, ID do dispositivo, IP, endereço MAC ou outros valores potencialmente identificáveis pelo usuário forem incorporadas na geração do  `id`, o resultado deverá ser obtido com hash. Isso garante que nenhuma PII seja codificada no valor, já que o objetivo não é identificar um usuário ou dispositivo, mas a medida específica no tempo. |
| `value` | Duplo | O valor quantificável desta medida. |

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/data/measure.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/data/measure.schema.json)