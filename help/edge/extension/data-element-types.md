---
title: Tipos de elementos de dados na extensão do SDK da Web da Adobe Experience Platform
description: Saiba mais sobre os diferentes tipos de elementos de dados fornecidos pela extensão Adobe Experience Platform Web SDK no Adobe Experience Platform Launch.
exl-id: 3c2c257f-1fbc-4722-8040-61ad19aa533f
translation-type: tm+mt
source-git-commit: 3f7808a08d033c5940d2115006c269b8c4079822
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 47%

---

# Tipos de elementos de dados

Depois de definir seus [tipos de ação](action-types.md) na [extensão Adobe Experience Platform Web SDK](web-sdk-extension.md) para [Adobe Experience Platform Launch](https://experienceleague.adobe.com/docs/launch.html), configure os tipos de elemento de dados.

Esta página descreve os tipos de elementos de dados disponíveis.

## ID de mesclagem de eventos

Quando usado, esse elemento de dados fornece uma ID de mesclagem de eventos. Nenhuma configuração é necessária para esse elemento de dados. O elemento de dados fornecido permanece o mesmo até que o visitante saia da página ou até que o tipo de ação &quot;Redefinir ID de mesclagem de eventos&quot; seja usado.

## Mapa de identidade

O elemento de dados do mapa de identidade permite criar identidades com base em outros elementos de dados ou outros valores especificados. Todas as identidades que você criar deverão estar associadas a um namespace correspondente. Esse elemento de dados fornece uma lista suspensa que mostra todos os namespaces padrão e qualquer um que você criou.

![](./assets/identity-map-data-element.png)

## Objeto XDM {#xdm-object}

Use o formato XDM para enviar dados para o SDK da Web da Adobe Experience Platform. A formatação dos dados é mais fácil com o elemento de dados do objeto XDM. Ao abrir esse elemento de dados pela primeira vez, selecione a sandbox e o esquema corretos da Adobe Experience Platform. Após selecionar o esquema, é possível ver a estrutura do esquema, que pode ser facilmente preenchida.

![](./assets/XDM-object.png)

Observe que quando você abre determinados campos do esquema, como `web.webPageDetails.URL`, alguns itens são coletados automaticamente. Mesmo que vários itens sejam coletados automaticamente, você pode substituir qualquer item, se necessário. Todos os valores podem ser preenchidos manualmente ou usando outros elementos de dados.

>[!NOTE]
>
>Preencha apenas as informações que você está interessado em coletar. Qualquer coisa que não for preenchida é omitida quando os dados forem enviados para as soluções.
