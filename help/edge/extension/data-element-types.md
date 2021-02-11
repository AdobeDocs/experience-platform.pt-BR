---
title: Tipos de elemento de dados de extensão do SDK da Web da plataforma
description: Tipos de elemento de dados de extensão do Adobe Experience Platform Web SDK no Adobe Experience Platform Launch
translation-type: tm+mt
source-git-commit: 473cc1f7617f1d65cdb70ff0e758178ea0174f00
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Tipos de elementos de dados

Depois de definir seus [tipos de ação](action-types.md) na [extensão do Adobe Experience Platform Web SDK](web-sdk-extension.md) para [Adobe Experience Platform Launch](https://experienceleague.adobe.com/docs/launch.html), configure os tipos de elementos de dados.

Esta página descreve os tipos de elementos de dados disponíveis.

## ID de mesclagem de eventos

Quando usado, esse elemento de dados fornece uma ID de mesclagem de eventos. Nenhuma configuração é necessária para esse elemento de dados. O elemento de dados fornecido permanece o mesmo até que o visitante saia da página ou até que o tipo de ação &quot;Redefinir ID de mesclagem de eventos&quot; seja usado.

## Mapa de identidade

O elemento de dados do mapa de identidade permite criar identidades com base em outros elementos de dados ou outros valores especificados. Todas as identidades que você criar deverão estar associadas a um namespace correspondente. Esse elemento de dados fornece uma lista suspensa que mostra todos os namespaces padrão, bem como todos os que você criou.

![](./assets/identity-map-data-element.png)

## Objeto XDM

Todos os dados enviados para o SDK da Web da Adobe Experience Platform devem estar no formato XDM. A formatação dos dados é mais fácil com o elemento de dados do objeto XDM. Ao abrir esse elemento de dados pela primeira vez, selecione a sandbox e o esquema corretos da Adobe Experience Platform. Depois de selecionar o esquema, você verá a estrutura dele, que pode ser facilmente preenchida.

![](./assets/XDM-object.png)

Observe que quando você abre determinados campos do esquema, como `web.webPageDetails.URL`, alguns itens são coletados automaticamente. Embora vários itens sejam coletados automaticamente, você tem a opção de substituir qualquer item, se necessário. Todos os valores podem ser preenchidos manualmente ou usando outros elementos de dados.

>[!NOTE]
>
>Basta preencher as informações que você está interessado em coletar. Tudo o que não for preenchido será omitido quando os dados forem enviados para as soluções.
