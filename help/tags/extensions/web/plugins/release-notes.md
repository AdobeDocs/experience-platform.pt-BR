---
title: Notas de versão da Extensão de plug-ins comuns do Analytics
description: As notas de versão mais recentes para a extensão de tag de plug-ins comuns do Analytics no Adobe Experience Platform.
source-git-commit: 5f810ada57eeb12a56de603d974a091b888dc9d2
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 94%

---

# Notas de versão da extensão de plug-ins comuns do Analytics

## 20 de maio de 2021

### Extensão de plug-ins comuns do Analytics 3.0.5

#### Correções de erros

* Correção de um problema em que getTimeParting não era inicializado corretamente ao ser usada a ação de inicialização genérica

## 26 de março de 2021

### Extensão de plug-ins comuns do Analytics 3.0.4

#### Correções de erros

* Correção de um problema em que getPageLoadTime estava definindo variáveis incorretamente no objeto da janela
* Correção de um problema em que getQueryParam retornava indefinido em vez de &quot;&quot; se o queryParam não estivesse presente na sequência de consulta
* Correção de um problema em que os números de versão incorretos eram exibidos na ação de inicialização

## 19 de março de 2021

### Extensão de plug-ins comuns do Analytics 3.0.2

#### Recursos

* Todos os plug-ins foram atualizados para incluir automaticamente informações de versão como dados de contexto
* Adição do plug-in getPercentPageViewed
* Adição de elementos de dados para os seguintes plug-ins
   * getGeoCoordinates
   * getNewRepeat
   * getPageName
   * getResponsiveLayout
   * getTimeParting
   * getTimeSinceLastVisit
   * getVisitDuration
   * getVisitNum
* Estilos atualizados

## 9 de abril de 2020

### Extensão de plug-ins comuns do Analytics 2.2.0

#### Correções de erros

* Texto fixo em visualizações de extensão

#### Recursos

* Atualização da documentação na ação de inicialização

## 5 de dezembro de 2019

### Extensão de plug-ins comuns do Analytics 2.1.1

#### Correções de erros

* Correção de um problema que impedia a compatibilidade com versões 2.0.X
* Correção de um problema no qual os links apontavam para a documentação errada
* Correção de um problema em que `getTimeSinceLastVisit` aparecia duas vezes na ação de inicialização

## 15 de novembro de 2019

### Extensão de plug-ins comuns do Analytics 2.1.0

#### Correções de erros

* Reintrodução de ações individuais de plug-in para oferecer compatibilidade com versões anteriores
* Correção de um problema com o `cleanStr` plug-in
* Correção de um problema com o `getResponsiveLayout` plug-in
* Correção de um problema com o `getPageName` plug-in

#### Recursos

* Atualização de versão para `getTimeParting`
* Atualização de versão para `numberSuite`
* Atualização de versão para `getNewRepeat`
* Atualização da documentação de todos os plug-ins

## 30 de outubro de 2019

### Extensão de plug-ins comuns do Analytics 2.0.3

#### Correções de erros

* Correção de um problema em que os links de documentação estavam com falha

## 11 de outubro de 2019

### Extensão de plug-ins comuns do Analytics 2.0.2

#### Recursos

* Foram adicionados 15 plug-ins à extensão
* Uma nova ação de inicialização foi criada para oferecer suporte e facilitar a implementação

## 11 de julho de 2019

### Extensão de plug-ins comuns do Analytics 1.0.4

#### Recursos

* Extensão lançada com sete plug-ins
* Ações individuais para inicializar cada plug-in
