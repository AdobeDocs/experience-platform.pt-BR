---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;individual profile;fields;schemas;Schemas;segment;segmentMembership;segment membership;Schema design;map;Map;
solution: Experience Platform
title: Mistura de segmentação de perfis
topic: overview
description: Este documento fornece uma visão geral da classe de Perfil individual XDM.
translation-type: tm+mt
source-git-commit: 53575488c08f73a65a7f1cc5f803f9ead707ae48
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 1%

---


# [!UICONTROL Mistura de segmentação] de perfis

[!UICONTROL A segmentação] do perfil é uma mistura padrão para a [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md). O mixin fornece um único campo de mapa que captura informações relacionadas à associação de segmentos, incluindo a quais segmentos o indivíduo pertence, a última hora de qualificação e quando a associação é válida até.

>[!WARNING]
>
>Embora o `segmentMembership` campo deva ser adicionado manualmente ao schema do perfil usando essa combinação, você não deve tentar preencher ou atualizar manualmente esse campo. O sistema atualiza automaticamente o `segmentMembership` mapa de cada perfil à medida que os trabalhos de segmentação são executados.

<img src="../../images/data-types/profile-segmentation.png" width="400" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `segmentMembership` | Mapa | Um objeto de mapa que descreve as associações de segmento do indivíduo. A estrutura desse objeto é descrita em detalhes abaixo. |

A seguir está um exemplo de `segmentMembership` mapa que o sistema preencheu para um determinado perfil. As associações de segmentos são classificadas por namespace, conforme indicado pelas chaves de nível raiz do objeto. Por sua vez, as chaves individuais em cada namespace representam as IDs dos segmentos dos quais o perfil é membro. Cada objeto de segmento contém vários subcampos que fornecem mais detalhes sobre a associação:

```json
{
  "xdm:segmentMembership": {
    "AAM": {
      "04a81716-43d6-4e7a-a49c-f1d8b3129ba9": {
        "xdm:version": "15",
        "xdm:lastQualificationTime": "2018-04-26T15:52:25+00:00",
        "xdm:validUntil": "2019-04-26T15:52:25+00:00",
        "xdm:status": "existing",
        "xdm:payload": {
          "xdm:payloadBooleanValue": true,
          "xdm:payloadType": "boolean"
        }
      },
      "53cba6b2-a23b-454a-8069-fc41308f1c0f": {
        "xdm:version": "3",
        "xdm:lastQualificationTime": "2018-04-26T15:52:25+00:00",
        "xdm:validUntil": "2018-04-27T15:52:25+00:00",
        "xdm:status": "realized",
        "xdm:payload": {
          "xdm:payloadPropensityValue": 0.5,
          "xdm:payloadType": "propensity"
        }
      }
    },
    "Email": {
      "abcd@adobe.com": {
        "xdm:version": "1",
        "xdm:lastQualificationTime": "2017-09-26T15:52:25+00:00",
        "xdm:validUntil": "2017-12-26T15:52:25+00:00",
        "xdm:status": "exited"
      }
    }
  }
}
```

| Propriedade | Descrição |
| --- | --- |
| `xdm:version` | A versão do segmento para a qual esse perfil se qualificou. |
| `xdm:lastQualificationTime` | Um carimbo de data e hora da última vez que este perfil se qualificou para o segmento. |
| `xdm:validUntil` | Um carimbo de data e hora em que a associação de segmento não deve mais ser considerada válida. |
| `xdm:status` | Indica se a associação de segmento foi realizada como parte da solicitação atual. Os seguintes valores são aceitos: <ul><li>`existing`: O perfil já fazia parte do segmento antes da solicitação e continua mantendo sua associação.</li><li>`realized`: O perfil está inserindo o segmento como parte da solicitação atual.</li><li>`exited`: O perfil está saindo do segmento como parte da solicitação atual.</li></ul> |
| `xdm:payload` | Algumas associações de segmentos incluem uma carga que descreve valores adicionais diretamente relacionados à associação. Somente uma carga de um determinado tipo pode ser fornecida para cada associação. `xdm:payloadType` indica o tipo de carga (`boolean`, `number`, `propensity`ou `string`), enquanto sua propriedade irmão fornece o valor para o tipo de carga. |

Para obter mais detalhes sobre a mistura, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-personal-details.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-personal-details.schema.json)
