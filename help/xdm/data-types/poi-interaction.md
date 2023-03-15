---
keywords: Experience Platform;página inicial;tópicos populares;esquema;Esquema;XDM;campos;esquemas;Esquemas;poi;interação;ponto de interesse;ponto de interesse;tipo de dados;tipo de dados;tipo de dados;
solution: Experience Platform
title: Tipo de dados da interação do ponto de interesse
description: Este documento fornece uma visão geral do tipo de dados XDM da interação com o Ponto de interesse.
exl-id: 398f56d9-1802-458d-b565-4096beb5b014
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 2%

---

# [!UICONTROL Interação com o ponto de interesse] tipo de dados

[!UICONTROL Interação com o ponto de interesse] é um tipo de dados XDM padrão que descreve o dispositivo sem fio que comunica informações de identidade para aplicativos móveis à medida que os dispositivos móveis ficam ao alcance.

<img src="../images/data-types/poi-interaction.png" width="400" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `poiDetail` | [[!UICONTROL Detalhes do ponto de interesse]](./poi-details.md) | Descreve os detalhes do POI que causou o evento. |
| `poiEntries` | Objeto | Descreve o número de vezes que uma pessoa inseriu o POI. Contém duas propriedades: <ul><li>`id`: um identificador exclusivo para a medida.</li><li>`value`: o valor quantificável da medida.</li></ul> |
| `poiExits` | Objeto | Descreve o número de vezes que uma pessoa saiu do POI. Contém duas propriedades: <ul><li>`id`: um identificador exclusivo para a medida.</li><li>`value`: o valor quantificável da medida.</li></ul> |

{style="table-layout:auto"}

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/poi-interaction.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/poi-interaction.schema.json)
