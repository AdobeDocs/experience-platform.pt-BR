---
keywords: Experience Platform, home, tópicos populares, esquema, esquema, XDM, campos, esquemas, esquemas, esquemas, detalhes da página da Web, tipo de dados, tipo de dados, tipo de dados, página da Web
solution: Experience Platform
title: Tipo de dados de informações da Web
topic-legacy: overview
description: Este documento fornece uma visão geral das informações da Web do tipo de dados do Experience Data Model (XDM).
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 2%

---

# [!UICONTROL Tipo de ] dados de informações da Web

[!UICONTROL As ] informações da Web são um tipo de dados padrão do Experience Data Model (XDM) que descreve as informações gravadas por um Evento de experiência específico para o canal da World Wide Web, incluindo a página da Web, o referenciador e/ou o link relacionado à interação na página.

![](../images/data-types/web-information.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `webInteraction` | [[!UICONTROL Interação da Web]](./web-interaction.md) | Descreve os detalhes sobre o link da Web ou URL que corresponde à interação. |
| `webPageDetails` | [[!UICONTROL Detalhes da página da Web]](./webpage-details.md) | Descreve os detalhes sobre a página da Web em que a interação da Web ocorreu. |
| `webReferrer` | [!UICONTROL Objeto] | Descreve o referenciador de uma interação da Web, que é o URL de onde um visitante veio imediatamente antes do registro da interação da Web atual. Contém as seguintes subpropriedades: <ul><li>`URL`: O URL do referenciador.</li><li>`type`: O tipo de referenciador.</li></ul> |

{style=&quot;table-layout:auto&quot;}

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/webinfo.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/webinfo.schema.json)
