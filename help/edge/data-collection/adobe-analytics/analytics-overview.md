---
title: Uso do Adobe Analytics com o SDK da Web da plataforma
description: Saiba como enviar dados para o Adobe Analytics com o SDK da Web da Adobe Experience Platform.
keywords: adobe analytics; analytics; dados mapeados; vars mapeadas;
exl-id: b18d1163-9edf-4a9c-b247-cd1aa7dfca50
source-git-commit: f627c1f6c917e74e0a366ce0611a1fa6bd0e3c3d
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Uso do Adobe Analytics com o SDK da Web da plataforma

A Adobe Experience Platform [!DNL Web SDK] O pode enviar dados para o Adobe Analytics. Isso funciona traduzindo `xdm` em um formato que o Adobe Analytics pode usar.

## Configuração

A Adobe Analytics coleta automaticamente os dados que você está enviando se você tem um conjunto de relatórios mapeado na interface do usuário de configuração do cliente. Aqui você pode mapear um ou mais relatórios para uma determinada configuração. Depois que um conjunto de relatórios é mapeado, os dados começam a fluir automaticamente.

## Grupo de campos XDM

Para facilitar a captura das métricas mais comuns do Adobe Analytics, fornecemos um grupo de campos do Analytics que pode ser usado. Para obter mais detalhes sobre esse schema, consulte a documentação do [Grupo de campos do esquema Extensão completa do Adobe Analytics ExperienceEvent](../../../xdm/field-groups/event/analytics-full-extension.md)

## Dados mapeados automaticamente

A Adobe Experience Platform [!DNL Edge Network] O mapeia automaticamente muitas variáveis XDM. A lista completa dessas variáveis está listada [here](automatically-mapped-vars.md).

## Dados mapeados manualmente

Todos os dados não mapeados automaticamente pela rede de borda podem ser acessados por meio de regras de processamento. Os dados são nivelados usando a notação de pontos e estão disponíveis como contextData.

Se você tivesse um esquema que se parecesse com este.

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
