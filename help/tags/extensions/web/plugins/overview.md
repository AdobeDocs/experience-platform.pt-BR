---
title: Visão geral da extensão comum do Analytics
description: Saiba mais sobre a extensão comum de tags do Analytics na Adobe Experience Platform.
exl-id: 9eeb4589-df90-4356-b927-b2c29c32370b
source-git-commit: 77313baabee10e21845fa79763c7ade4e479e080
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 86%

---

# Visão geral da extensão de plug-ins comuns do Analytics

>[!NOTE]
>
>A Adobe Experience Platform Launch foi reformulada como um conjunto de tecnologias de coleta de dados no Adobe Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

Use esta referência para obter informações sobre como configurar a extensão de plug-ins comuns do Analytics e as opções disponíveis ao usá-la para aumentar a Extensão [!DNL Adobe Analytics].

## Configurar a extensão de plug-ins comuns do Analytics

Esta seção fornece uma referência para as opções disponíveis ao configurar a extensão de plug-ins comuns do Analytics.

>[!IMPORTANT]
>
>A extensão de plug-ins comuns do Analytics aumenta a extensão [!DNL Adobe Analytics]. É necessário ter a extensão [!DNL Adobe Analytics] instalada na propriedade para que ela funcione. Além disso, você deve tornar o rastreador globalmente acessível na extensão [!DNL Adobe Analytics].

Nenhuma configuração adicional é necessária no nível da extensão.

## Adicionar plug-ins à extensão [!DNL Adobe Analytics]

Para usar os plug-ins fornecidos nesta extensão, primeiro você deve inicializar os plug-ins que pretende usar em sua própria regra.

1. Crie uma nova regra.
1. Adicione o evento Principal - Biblioteca carregada (topo da página).
1. Use qualquer um dos métodos de inicialização abaixo.

## Tipos de ação da extensão de plug-ins comuns do Analytics

Esta seção descreve os tipos de ação disponíveis na extensão de plug-ins comuns do Analytics.

A extensão de plug-ins comuns do Analytics fornece as seguintes ações:

* [Inicializar](#initialize)
* [Inicializar plug-in](#initialize-plugin)

### Inicializar

>[!IMPORTANT]
>
>Embora essa ação seja mais fácil de implementar, a Adobe Consulting não recomenda usar essa ação, pois ela aumenta o peso do plug-in.

Nesta ação, você pode selecionar cada plug-in que deseja incluir na implementação e salvar as alterações. Selecione quantas vezes você pretende usar durante a implementação.

### Inicializar plug-in

Essas ações inicializam o plug-in específico que você pretende usar individualmente. Para inicializar todos os plug-ins que você pretende usar em sua propriedade, basta adicionar a ação correspondente à regra e salvá-la. Embora haja um pouco mais de esforço envolvido na configuração da extensão dessa forma, ela oferece um código mais eficiente. Portanto, a Adobe recomenda essa abordagem.

## Elementos de dados da extensão de plug-ins comuns do Analytics

Os seguintes elementos de dados estão disponíveis na extensão de plug-ins comuns do Analytics, que aproveita os recursos de tags para configurar e configurar os plug-ins correspondentes no Analytics:

* `getGeoCoordinates`
* `getNewRepeat`
* `getPageName`
* `getResponsiveLayout`
* `getTimeParting`
* `getTimeSinceLastVisit`
* `getVisitDuration`
* `getVisitNum`

>[!NOTE]
>
>Para obter mais informações sobre os plug-ins acima, consulte o [Documentação do Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/impl-plugins.html?lang=pt-BR).
