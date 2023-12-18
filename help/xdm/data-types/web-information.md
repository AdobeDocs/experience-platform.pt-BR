---
keywords: Experience Platform;página inicial;tópicos populares;esquema;Esquema;XDM;campos;esquemas;Esquemas;Detalhes da página da Web;tipo de dados;tipo de dados;tipo de dados;página da Web
solution: Experience Platform
title: Tipo de Dados de Informações da Web
description: Saiba mais sobre o tipo de dados do Experience Data Model (XDM) para informações da Web.
exl-id: bfb00835-5908-4baf-af2a-6d845710e340
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 2%

---

# [!UICONTROL Informações da Web] tipo de dados

[!UICONTROL Informações da Web] é um tipo de dados padrão do Experience Data Model (XDM) que descreve as informações registradas por meio de um Evento de experiência específico do canal da World Wide Web, incluindo a página da Web, o referenciador e/ou o link relacionado à interação na página.

![](../images/data-types/web-information.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `webInteraction` | [[!UICONTROL Interação na Web]](./web-interaction.md) | Descreve os detalhes sobre o link da Web ou o URL que corresponde à interação. |
| `webPageDetails` | [[!UICONTROL Detalhes da página da Web]](./webpage-details.md) | Descreve os detalhes sobre a página da Web em que ocorreu a interação da Web. |
| `webReferrer` | [!UICONTROL Objeto] | Descreve o referenciador de uma interação da web, que é o URL de onde um visitante veio imediatamente antes de a interação da web atual ser registrada. Contém as seguintes subpropriedades: <ul><li>`URL`: o URL do referenciador.</li><li>`type`: o tipo de referenciador.</li></ul> |

{style="table-layout:auto"}

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/webinfo.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/webinfo.schema.json)
