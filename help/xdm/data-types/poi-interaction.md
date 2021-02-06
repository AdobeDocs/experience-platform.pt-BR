---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;campos;schemas;Schemas;poi;interação;ponto de interesse;tipo de dados;tipo de dados;tipo de dados;;home;popular topics;;social;social;data topics;data-type;data type;data type;
solution: Experience Platform
title: Tipo de Dados de Interação de Ponto de Interesse
topic: overview
description: Este documento fornece uma visão geral do tipo de dados XDM de interação de ponto de interesse.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 1%

---


# [!UICONTROL Tipo de dados de interação de ponto de interesse ] 

[!UICONTROL A ] interação de ponto de interesse é um tipo de dados XDM padrão que descreve o dispositivo sem fio que comunica as informações de identidade para aplicativos móveis quando os dispositivos móveis estão dentro da faixa de alcance.

<img src="../images/data-types/poi-interaction.png" width="400" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `poiDetail` | [[!UICONTROL Detalhes do ponto de interesse]](./poi-details.md) | Descreve os detalhes do POI que causou o evento. |
| `poiEntries` | Objeto | Descreve o número de vezes que uma pessoa entrou no POI. Contém duas propriedades: <ul><li>`id`: Um identificador exclusivo da medida.</li><li>`value`: O valor quantificável da medida.</li></ul> |
| `poiExits` | Objeto | Descreve o número de vezes que uma pessoa saiu do POI. Contém duas propriedades: <ul><li>`id`: Um identificador exclusivo da medida.</li><li>`value`: O valor quantificável da medida.</li></ul> |

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-interaction.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-interaction.schema.json)
