---
title: Tipo de dados de impressões
description: Saiba mais sobre o tipo de dados XDM de impressões.
exl-id: 1e758043-a41e-45f7-ae8b-514990d0649e
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 6%

---

# Tipo de dados [!UICONTROL Impressões]

[!UICONTROL Impressões] é um tipo de dados XDM padrão que descreve uma impressão de marketing, que é uma métrica usada para quantificar o número de visualizações ou envolvimentos digitais para um conteúdo, como um anúncio, publicação digital ou página da Web.

![](../images/data-types/impressions.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `ID` | String | Um identificador exclusivo para a impressão. |
| `displays` | Número inteiro | O número de vezes que o item de impressão foi exibido para um cliente. |
| `selected` | Número inteiro | O número de vezes que o item de impressão foi selecionado ou clicado. |
| `type` | String | O tipo de impressão. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o grupo de campos, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/impressions.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/impressions.schema.json)
