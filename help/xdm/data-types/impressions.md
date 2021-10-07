---
title: Tipo de dados de impressões
description: Este documento fornece uma visão geral do tipo de dados XDM de impressões.
source-git-commit: 7fc16546176d196582a3cdfcee51f799eeef9788
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 6%

---

#  Tipo de dados de impressão

 Impressão é um tipo de dados XDM padrão que descreve uma impressão de marketing, que é uma métrica usada para quantificar o número de visualizações ou envolvimentos digitais para um conteúdo, como um anúncio, postagem digital ou página da Web.

![](../images/data-types/impressions.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `ID` | String | Uma ID exclusiva para a impressão. |
| `displays` | Número inteiro | O número de vezes em que o item de impressão foi exibido a um cliente. |
| `selected` | Número inteiro | O número de vezes que o item de impressão foi selecionado ou clicado. |
| `type` | String | O tipo de impressão. |

{style=&quot;table-layout:auto&quot;}

Para obter mais detalhes sobre o grupo de campos, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/impressions.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/impressions.schema.json)
