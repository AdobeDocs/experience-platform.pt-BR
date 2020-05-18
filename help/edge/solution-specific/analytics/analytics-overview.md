---
title: Envio de dados para o Adobe Analytics
seo-title: Envio de dados para o Adobe Analytics com o SDK da Web da Adobe Experience Platform
description: Saiba como enviar dados para o Adobe Analytics com o Experience Platform Web SDK
seo-description: Saiba como enviar dados para o Adobe Analytics com o Experience Platform Web SDK
translation-type: tm+mt
source-git-commit: 890004b54cb4daf08f188147ed5c97d56e4055fb
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---


# Envio de dados para o Adobe Analytics

O SDK da Web da plataforma Adobe Experience pode enviar dados para o Adobe Analytics. Isso funciona se traduzindo `xdm` em um formato que o Adobe Analytics pode usar.

## Configurar

O Adobe Analytics coleta automaticamente os dados que você está enviando caso tenha um conjunto de relatórios mapeado na interface do usuário de configuração do cliente. Aqui você pode mapear um ou mais relatórios para uma determinada configuração. Depois que um conjunto de relatórios é mapeado, os dados começam a fluir automaticamente.

## Dados mapeados automaticamente

A Adobe Experience Platform Edge Network mapeia automaticamente muitas variáveis XDM. A lista completa de variáveis mapeadas automaticamente é listada [aqui](../analytics/automatically-mapped-vars.md).

## Dados mapeados manualmente

Todos os dados coletados pela rede de borda podem ser acessados pelas regras de processamento. Os dados são nivelados usando a notação de pontos e estão disponíveis como contextData.

Se você tivesse uma schema parecida com esta.

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

Essas seriam as chaves de dados de contexto disponíveis para você.

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

![Interface das regras de processamento](../../../assets/edge_analytics_processing_rules.png)
