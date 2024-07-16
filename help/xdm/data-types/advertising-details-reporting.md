---
title: Tipo de dados de relatório de detalhes do Advertising
description: Saiba mais sobre o tipo de dados Modelo de dados de experiência (XDM) dos relatórios de detalhes do Advertising.
exl-id: fbca5b2a-a9bd-4f76-a494-d682cb2cbfbc
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 12%

---

# [!UICONTROL Detalhes do Advertising] Tipo de dados de relatório

[!UICONTROL Detalhes do Advertising] Os relatórios são um tipo de dados padrão do Experience Data Model (XDM) que captura os principais atributos relacionados aos anúncios. Inclui informações como ID do anúncio, IDs do anunciante e da campanha, duração, posição em uma sequência, detalhes sobre o reprodutor que renderiza o anúncio e assim por diante. Você pode usar esse tipo de dados para rastrear e analisar vários aspectos do desempenho e engajamento do anúncio, e fornecer insights sobre como os públicos-alvo interagem e respondem a diferentes anúncios.

+++Selecione para exibir um diagrama do tipo de dados Relatórios de detalhes do Advertising.
![Um diagrama do tipo de dados do Relatório de Detalhes do Advertising.](../images/data-types/advertising-details-information.png)
+++

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
|----------------------------------------|-----------------|-----------|-----------------------------------------------------------------------------------------------|
| [!UICONTROL Nome do anúncio] | `friendlyName` | sequência de caracteres | O nome legível do anúncio. Nos relatórios, o &quot;Ad Name&quot; é a classificação e o &quot;Ad Name (variable)&quot; é o eVar. |
| [!UICONTROL ID do anúncio] | `name` | sequência de caracteres | A ID do anúncio. Qualquer combinação de número inteiro e/ou letra. |
| [!UICONTROL Duração Ou Comprimento Do Anúncio] | `length` | inteiro | A duração do anúncio de vídeo em segundos. |
| [!UICONTROL Posição Do Anúncio No Pod (Início Do Anúncio)] | `podPosition` | inteiro | O índice do anúncio dentro do início do anúncio principal, por exemplo, o primeiro anúncio tem índice 0 e o segundo anúncio tem índice 1. |
| [!UICONTROL Nome do player do anúncio] | `playerName` | sequência de caracteres | O nome do player responsável por renderizar o anúncio. |
| [!UICONTROL Anunciante de anúncio] | `advertiser` | sequência de caracteres | A empresa ou marca cujo produto é apresentado no anúncio. |
| [!UICONTROL Campanha publicitária] | `campaignID` | sequência de caracteres | A ID da campanha publicitária. |
| [!UICONTROL Ad Creative ID] | `creativeID` | sequência de caracteres | A ID do criativo do anúncio. |
| [!UICONTROL ID do site de anúncio] | `siteID` | sequência de caracteres | A ID do site do anúncio. |
| [!UICONTROL URL de criação do anúncio] | `creativeURL` | sequência de caracteres | A URL do criativo do anúncio. |
| [!UICONTROL ID de posicionamento do anúncio] | `placementID` | sequência de caracteres | A ID de posicionamento do anúncio. |
| [!UICONTROL Anúncio concluído] | `isCompleted` | booleano | Rastreia se o anúncio foi concluído. |
| [!UICONTROL Anúncio iniciado] | `isStarted` | booleano | Rastreia se o anúncio foi iniciado. |
| [!UICONTROL Tempo de reprodução do anúncio] | `timePlayed` | inteiro | O tempo total, em segundos, gasto com a exibição do anúncio (ou seja, o número de segundos reproduzidos). |

{style="table-layout:auto"}

Para obter mais detalhes sobre o grupo de campos, consulte o [repositório XDM público](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json)
