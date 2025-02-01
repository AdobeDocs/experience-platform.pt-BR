---
keywords: Experience Platform;início;tópicos populares;esquema;Esquema;XDM;campos;esquemas;Esquemas;contexto de local;placeContext;tipo de dados;tipo de dados;tipo de dados;
solution: Experience Platform
title: Tipo de Dados de Contexto do Local
description: Saiba mais sobre o tipo de dados XDM de contexto do local.
exl-id: d7cf7366-0136-49ee-84d2-ec663db66eb4
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 3%

---

# Tipo de dados [!UICONTROL Inserir contexto]

[!UICONTROL Inserir contexto] é um tipo de dados XDM padrão que descreve o local de um evento observado, incluindo informações de ponto de interesse e coordenadas geográficas.

![](../images/data-types/place-context.png){width=500}

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `POIinteraction` | [[!UICONTROL Interação com o ponto de interesse]](./poi-interaction.md) | Descreve detalhes sobre a interação do ponto de interesse (POI). |
| `activePOIs` | Matriz de [[!UICONTROL detalhes do ponto de interesse]](./poi-details.md) | Descreve os POIs que causaram o evento. |
| `geo` | [[!UICONTROL Geografia]](./geo.md) | Descreve a localização geográfica onde a experiência foi entregue. |
| `localTime` | DateTime | Um carimbo de data/hora no formato [RFC 3339](https://tools.ietf.org/html/rfc3339), indicando a hora local usando com um deslocamento de fuso horário declarado. O padrão de formatação é `yyyy-MM-dd'T'HH:mm:ssXXX` (por exemplo, `2001-07-04T12:08:56-07:00`). |
| `localTimezoneOffset` | Número inteiro | O deslocamento do fuso horário local atual em minutos do UTC para o valor `localTime`. Isso deve incluir o deslocamento de horário de verão atual, se aplicável. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.schema.json)
