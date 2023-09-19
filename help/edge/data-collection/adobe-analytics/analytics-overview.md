---
title: Utilização do Adobe Analytics com o SDK da Web da plataforma
description: Saiba como enviar dados para a Adobe Analytics com o SDK da Web da Adobe Experience Platform.
keywords: adobe analytics;analytics;dados mapeados;vars mapeadas;
exl-id: b18d1163-9edf-4a9c-b247-cd1aa7dfca50
source-git-commit: 3272db15283d427eb4741708dffeb8141f61d5ff
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 0%

---

# Utilização do Adobe Analytics com o SDK da Web da plataforma

O ADOBE EXPERIENCE PLATFORM [!DNL Web SDK] O pode enviar dados para a Adobe Analytics. Isso funciona traduzindo `xdm` em um formato que o Adobe Analytics possa usar.

## Configuração

A Adobe Analytics seleciona automaticamente os dados que você está enviando se você tiver um conjunto de relatórios mapeado na interface de configuração do cliente. Aqui você pode mapear um ou mais relatórios para uma determinada configuração. Depois que um conjunto de relatórios é mapeado, os dados começam a fluir automaticamente.

## Grupo de campos XDM

Para facilitar a captura das métricas mais comuns do Adobe Analytics, fornecemos um grupo de campos do Analytics que você pode usar. Para obter mais detalhes sobre esse esquema, consulte a documentação do [Grupo de campos de esquema de Extensão completa do Adobe Analytics ExperienceEvent](../../../xdm/field-groups/event/analytics-full-extension.md)

## Dados mapeados automaticamente

O ADOBE EXPERIENCE PLATFORM [!DNL Edge Network] O mapeia automaticamente muitas variáveis XDM. A lista completa dessas variáveis é [aqui](automatically-mapped-vars.md).

## Dados mapeados manualmente

Quaisquer dados que não sejam mapeados automaticamente pelo [!DNL Edge Network] pode ser acessado pelas regras de processamento. Os dados são nivelados usando a notação de pontos e disponibilizados como contextData.

Se você tivesse um esquema com esta aparência.

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

Este é um exemplo de uma regra de processamento que usaria esses dados.

![Interface de regras de processamento](./assets/edge_analytics_processing_rules.png)

>[!NOTE]
>
>Com a coleção Rede de borda, todos os eventos são enviados para o Analytics, bem como para quaisquer outros serviços que você tenha configurado para o seu fluxo de dados. Por exemplo, se o Analytics e o Target estiverem configurados como serviços e você fizer chamadas separadas para personalização e Analytics, ambos os eventos serão enviados para o Analytics e para o Target. Esses eventos serão registrados nos relatórios do Analytics e podem afetar métricas como taxa de rejeição.
