---
keywords: Experience Platform, home, tópicos populares, esquema, esquema, XDM, campos, esquemas, esquemas, dispositivo, tipo de dados, tipo de dados, tipo de dados;
solution: Experience Platform
title: Tipo de dados do dispositivo
topic-legacy: overview
description: Este documento fornece uma visão geral do tipo de dados do Device XDM.
exl-id: 049a2ca1-6bc3-4b9c-832a-77102e8a0ed2
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 4%

---

# [!UICONTROL Device] tipo de dados

[!UICONTROL Device] é um tipo de dados XDM padrão que descreve um dispositivo identificado. Um dispositivo é uma instância de aplicativo ou navegador que pode ser rastreada nas sessões, normalmente por cookies.

<img src="../images/data-types/device.png" width="450" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `colorDepth` | Número inteiro | O número de cores que a exibição pode representar. |
| `manufacturer` | String | O nome da organização proprietária do design e da criação do dispositivo. |
| `model` | String | O nome do modelo do dispositivo. Este é o nome comum, legível por humanos ou de marketing do dispositivo. Por exemplo, o &quot;iPhone 6S&quot; é um modelo específico de telefone celular. |
| `modelNumber` | String | A designação do número de modelo único atribuída pelo fabricante para este dispositivo. Os números de modelo não são versões, mas identificadores exclusivos que identificam uma configuração de modelo específica. |
| `screenHeight` | Número inteiro | O número de pixels verticais da exibição ativa do dispositivo na orientação padrão. |
| `screenOrientation` | String | A orientação atual da tela. Os valores aceitos incluem `portrait` e `landscape`. |
| `screenWidth` | String | O número de pixels horizontais da exibição ativa do dispositivo na orientação padrão. |
| `type` | String | O tipo de dispositivo que está sendo rastreado. Os valores aceitos incluem: <ul><li>`mobile`</li><li>`tablet`</li><li>`desktop`</li><li>`ereader`</li><li>`gaming`</li><li>`television`</li><li>`settop`</li><li>`mediaplayer`</li><li>`computers`</li><li>`tv screens`</li></ul> |
| `typeID` | String | Um identificador para o dispositivo. Pode ser um identificador do DeviceAtlas ou outro serviço que identifique o hardware que está sendo usado. |
| `typeIDService` | String | O namespace do serviço usado para identificar o tipo de dispositivo. Consulte o [apêndice](#typeIDService) para obter detalhes sobre os valores aceitos. |

Para obter mais detalhes sobre o mixin, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/device.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/device.schema.json)

## Apêndice

A seção a seguir contém informações adicionais sobre o tipo de dados [!UICONTROL Device] .

## Valores aceitos para typeIDService {#typeIDService}

A tabela a seguir descreve os valores aceitos para `typeIDService` e seus significados associados:

| Valor | Descrição |
| --- | --- |
| `https://ns.adobe.com/xdm/external/deviceatlas` | O dispositivo foi identificado usando DeviceAtlas. |
| `https://ns.adobe.com/xdm/external/adobecampaign` | O dispositivo foi identificado usando o Adobe Campaign. |
