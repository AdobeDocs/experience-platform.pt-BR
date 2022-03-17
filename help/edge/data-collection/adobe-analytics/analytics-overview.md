---
title: Uso do Adobe Analytics com o SDK da Web da plataforma
description: Saiba como enviar dados para o Adobe Analytics com o SDK da Web da Adobe Experience Platform.
keywords: adobe analytics;analytics;mapped data;mapped vars;
exl-id: b18d1163-9edf-4a9c-b247-cd1aa7dfca50
source-git-commit: 921a3a32ee5f2daa04512a3f2c68935667ab3875
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 6%

---

# Uso do Adobe Analytics com o SDK da Web da plataforma

A Adobe Experience Platform [!DNL Web SDK] O pode enviar dados para o Adobe Analytics. Isso funciona traduzindo `xdm` em um formato que o Adobe Analytics pode usar.

## Configuração

Adobe Analytics automatically picks up the data you are sending if you have a report suite mapped in the Customer Config UI. Here you can map one or more reportings to a given config. Depois que um conjunto de relatórios é mapeado, os dados começam a fluir automaticamente.

## Grupo de campos XDM

To make it easier to capture the most common Adobe Analytics metrics, we provide an Analytics field group that you can use. For more details on this schema, see the documenation for the [Adobe Analytics ExperienceEvent Full Extension schema field group](../../../xdm/field-groups/event/analytics-full-extension.md)

## Dados mapeados automaticamente

The Adobe Experience Platform [!DNL Edge Network] automatically maps many XDM variables. A lista completa dessas variáveis está listada [here](automatically-mapped-vars.md).

## Manually mapped data

Todos os dados coletados pela rede de borda podem ser acessados pelas regras de processamento. The data is flattened using dot notation and available as contextData.

If you had a schema that looked like this.

```javascript
{
  key:value,
  object:{
    key1:value1,
    key2:value2
  },
  array:[
    "v0",
    "v1",
    "v2"
  ],
  arrayofobjects:[
    {
      obj1key:objval0
    },
    {
      obj2key:objval1
    }
  ]
}
```

Em seguida, essas seriam as chaves de dados de contexto disponíveis para você.

```javascript
a.x.key //value
a.x.object.key1 //value1
a.x.object.key2 //value2
a.x.array.0 //v0
a.x.array.1 //v1
a.x.array.2 //v2
a.x.arrayofobjects.0.obj1key //objval0
a.x.arrayofobjects.1.obj2key //objval1
```

Este é um exemplo de regra de processamento que usaria esses dados.

![Interface das regras de processamento](./assets/edge_analytics_processing_rules.png)
