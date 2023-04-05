---
keywords: Experience Platform, home, tópicos populares, schema, esquema, XDM, perfil individual, campos, esquemas, esquemas, segmento, segmentMembership, associação de segmento, design de esquema, mapa, Mapa;
solution: Experience Platform
title: Detalhes da associação ao segmento Grupo de campos do esquema
description: Este documento fornece uma visão geral do grupo de campos Detalhes da associação ao segmento .
exl-id: 4d463f3a-2247-4307-8afe-9527e7fd72a7
source-git-commit: 229dd08bc5d5dfab068db3be84ad20d10992fd31
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 2%

---


# [!UICONTROL Detalhes da associação ao segmento] grupo de campos de esquema

>[!NOTE]
>
>Os nomes de vários grupos de campos de esquema foram alterados. Consulte o documento em [atualizações de nome do grupo de campos](../name-updates.md) para obter mais informações.

[!UICONTROL Detalhes da associação ao segmento] é um grupo de campos de esquema padrão para a variável [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md). O grupo de campos fornece um único campo de mapa que captura informações relacionadas à associação de segmentos, incluindo a quais segmentos o indivíduo pertence, a última hora de qualificação e quando a associação é válida até.

>[!WARNING]
>
>Enquanto a variável `segmentMembership` O campo deve ser adicionado manualmente ao esquema do perfil usando esse grupo de campos, e você não deve tentar preencher ou atualizar manualmente esse campo. O sistema atualiza automaticamente os `segmentMembership` são executados mapas para cada perfil, pois os trabalhos de segmentação são executados.

<img src="../../images/data-types/profile-segmentation.png" width="400" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `segmentMembership` | Mapa | Um objeto de mapa que descreve as associações de segmento de cada indivíduo. A estrutura desse objeto é descrita detalhadamente abaixo. |

{style="table-layout:auto"}

Este é um exemplo `segmentMembership` mapa que o sistema preencheu para um perfil específico. As associações de segmento são classificadas por namespace, conforme indicado pelas chaves de nível raiz do objeto. Por sua vez, as chaves individuais em cada namespace representam as IDs dos segmentos dos quais o perfil é membro. Cada objeto de segmento contém vários subcampos que fornecem mais detalhes sobre a associação:

```json
{
  "xdm:segmentMembership": {
    "AAM": {
      "04a81716-43d6-4e7a-a49c-f1d8b3129ba9": {
        "xdm:version": "15",
        "xdm:lastQualificationTime": "2018-04-26T15:52:25+00:00",
        "xdm:validUntil": "2019-04-26T15:52:25+00:00",
        "xdm:status": "realized",
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
| `xdm:version` | A versão do segmento para a qual este perfil se qualificou. |
| `xdm:lastQualificationTime` | Um carimbo de data e hora da última vez que esse perfil se qualificou para o segmento. |
| `xdm:validUntil` | Um carimbo de data e hora de quando a associação de segmento não deve mais ser considerada válida. Para públicos externos, se esse campo não estiver definido, a associação do segmento será retida somente por 30 dias a partir da data de `lastQualificationTime`. |
| `xdm:status` | Campo de string que indica se a associação de segmentos foi realizada como parte da solicitação atual. Os seguintes valores são aceitos: <ul><li>`realized`: O perfil se qualifica para o segmento.</li><li>`exited`: O perfil está saindo do segmento como parte da solicitação atual.</li></ul> |
| `xdm:payload` | Algumas associações de segmento incluem uma carga que descreve valores adicionais diretamente relacionados à associação. Somente uma carga de um determinado tipo pode ser fornecida para cada associação. `xdm:payloadType` indica o tipo de carga (`boolean`, `number`, `propensity`ou `string`), enquanto sua propriedade irmão fornece o valor para o tipo de carga útil. |

{style="table-layout:auto"}

>[!NOTE]
>
>Qualquer associação de segmento que esteja no `exited` por mais de 30 dias, com base no `lastQualificationTime`, estará sujeita a exclusão.

Para obter mais detalhes sobre o grupo de campos, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.schema.json)
