---
keywords: Experience Platform;página inicial;tópicos populares;esquema;Esquema;XDM;campos;esquemas;Esquemas;Detalhes da página da Web;tipo de dados;tipo de dados;tipo de dados;página da Web
solution: Experience Platform
title: Tipo de dados do canal de experiência
description: Saiba mais sobre o tipo de dados Experience Data Model (XDM) do canal de experiência.
exl-id: 209654f7-0bde-439a-989c-ce2e41599105
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 4%

---

# [!UICONTROL Canal de experiência] tipo de dados

[!UICONTROL Canal de experiência] é um tipo de dados padrão do Experience Data Model (XDM) que descreve um canal de experiência. Um canal de experiência representa um método ou caminho para o consumo de experiências digitais.

Há vários canais de experiência, cada um com diferentes restrições sobre como o conteúdo é entregue e como a interação com o cliente pode ser observada, e como os dados são coletados. Em um canal, as experiências podem ser entregues a locais específicos. Os locais e tipos de locais que existem em um canal diferem de canal para canal.

![](../images/data-types/experience-channel.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `_id` | String | Uma ID que identifica exclusivamente o canal. Cada canal de experiência específico define uma constante `@id`. |
| `_type` | String | Fornece um rótulo de classificação aproximada para canais com propriedades semelhantes. |
| `contentTypes` | Matriz de cadeias de caracteres | Os tipos de conteúdo que este canal pode oferecer. |
| `locationTypes` | Matriz de cadeias de caracteres | Os tipos de locais (locais virtuais) em que este canal consiste e para os quais pode entregar conteúdo. |
| `mediaAction` | String | Descreve uma ação de mídia de Evento de experiência, se aplicável. |
| `mediaType` | String | Descreve se o tipo de mídia é pago, próprio ou ganho. |
| `metricTypes` | Matriz de cadeias de caracteres | As métricas que podem ser coletadas neste canal. |
| `mode` | String | Como as experiências são entregues neste canal. |
| `typeAtSource` | String | Um nome personalizado para o canal. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/channel.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/channel.schema.json)
