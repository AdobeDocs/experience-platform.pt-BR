---
title: Envio de dados para o Adobe Analytics
seo-title: Envio de dados para o Adobe Analytics com o SDK da Web da Adobe Experience Platform
description: Saiba como enviar dados para o Adobe Analytics com o Experience Platform Web SDK
seo-description: Saiba como enviar dados para o Adobe Analytics com o Experience Platform Web SDK
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# (Beta) Envio de dados para o Adobe Analytics

>[!IMPORTANT]
>
>O SDK da Web da plataforma Adobe Experience está atualmente em beta e não está disponível para todos os usuários. A documentação e a funcionalidade estão sujeitas a alterações.

O SDK da Web da plataforma Adobe Experience pode enviar dados para o Adobe Analytics. Isso funciona se traduzindo `xdm` em um formato que o Adobe Analytics pode usar.

## Configuração

O Adobe Analytics coleta automaticamente os dados que você está enviando caso tenha um conjunto de relatórios mapeado na interface do usuário de configuração do cliente. Aqui você pode mapear um ou mais relatórios para uma determinada configuração. Depois que um conjunto de relatórios é mapeado, os dados começam a fluir automaticamente.

## Dados mapeados automaticamente

A Adobe Experience Platform Edge Network mapeia automaticamente muitas variáveis XDM. A lista completa de variáveis mapeadas automaticamente é listada [aqui](../analytics/automatically-mapped-vars.md).

## Dados mapeados manualmente

Todos os dados coletados pela rede de borda podem ser acessados pelas regras de processamento. Os dados são nivelados usando a notação de pontos e estão disponíveis como contextData.

Se você tivesse um esquema que se parecesse com este.

```javascript
{
  key:value,
  object:{
    key1:value1,
    key2:value2
  },
  array:[
    v1,
    v2,
    v3
  ],
  arrayofobjects:[
    {
      obj1key:objval1
    },
    {
      obj2key:objval2
    }
  ]
}
```

Essas seriam as chaves de dados de contexto disponíveis para você.

```javascript
a.x.key //value
a.x.object.key1 //value1
a.x.object.key2 //value2
a.x.array[0] //v1
a.x.array[1] //v2
a.x.array[3] //v3
a.x.arrayofobjects[1].obj1key //objval1
a.x.arrayofobjects[2].obj2key //objval2
```

Este é um exemplo de uma regra de processamento que usaria esses dados.

![Interface das regras de processamento](../../../assets/edge_analytics_processing_rules.png)
