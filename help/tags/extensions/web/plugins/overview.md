---
title: Visão geral da extensão comum do Analytics
description: Saiba mais sobre a extensão de tag do Common Analytics no Adobe Experience Platform.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 66%

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

Nesta ação, você pode selecionar cada plug-in que deseja incluir na implementação e salvar as alterações. Selecione quantas vezes você pretende usar durante a implementação. Links para a documentação sobre como usar cada plug-in e uma breve descrição são fornecidos na visão geral dos [Plug-ins do Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/impl-plugins.html?lang=pt-BR).

### Inicializar plug-in

Essas ações inicializam o plug-in específico que você pretende usar individualmente. Para inicializar todos os plug-ins que você pretende usar em sua propriedade, basta adicionar a ação correspondente à regra e salvá-la. Embora haja um pouco mais de esforço envolvido na configuração da extensão dessa forma, ela oferece um código mais eficiente. Portanto, a Adobe recomenda essa abordagem.

## Elementos de dados da extensão de plug-ins comuns do Analytics

Esta seção descreve os elementos de dados disponíveis na extensão de plug-ins comuns do Analytics.

### getGeoCoordinates

Permite que os usuários aproveitem a interface nativa da coleta de dados no Adobe Experience Platform para configurar o plug-in getGeoCoordinates.

### getNewRepeat

Permite que os usuários aproveitem a interface nativa da coleta de dados para configurar o plug-in getNewRepeat.

### getPageName

Permite que os usuários aproveitem a interface nativa da coleta de dados para configurar o plug-in getPageName.

### getResponsiveLayout

Permite que os usuários aproveitem a interface nativa da coleta de dados para configurar o plug-in getResponsiveLayout.

### getTimeParting

Permite que os usuários aproveitem a interface nativa da coleta de dados para configurar o plug-in getTimeParting.

### getTimeSinceLastVisit

Permite que os usuários aproveitem a interface nativa da coleta de dados para configurar o plug-in getTimeSinceLastVisit.

### getVisitDuration

Permite que os usuários aproveitem a interface nativa da coleta de dados para configurar o plug-in getVisitDuration.

### getVisitNum

Permite que os usuários aproveitem a interface nativa da coleta de dados para configurar o plug-in getVisitNum .
