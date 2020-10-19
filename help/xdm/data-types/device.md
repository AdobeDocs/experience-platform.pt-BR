---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;device;datatype;data-type;data type;
solution: Experience Platform
title: Tipo de dados do dispositivo
topic: overview
description: Este documento fornece uma visão geral do tipo de dados do Device XDM.
translation-type: tm+mt
source-git-commit: f5bddb39c16eb25e85297f56e331d3aa51510eb9
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 4%

---


# [!UICONTROL Tipo de dados do dispositivo]

[!UICONTROL O dispositivo] é um tipo de dados XDM padrão que descreve um dispositivo identificado. Um dispositivo é uma instância de aplicativo ou navegador rastreável em sessões, normalmente por cookies.

<img src="../images/data-types/device.png" width="450" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `colorDepth` | Número inteiro | O número de cores que a exibição pode representar. |
| `manufacturer` | String | O nome da organização proprietária do design e da criação do dispositivo. |
| `model` | String | O nome do modelo para o dispositivo. Este é o nome comum, legível por humanos ou de marketing do dispositivo. Por exemplo, o &quot;iPhone 6S&quot; é um modelo específico de telefone celular. |
| `modelNumber` | String | A designação exclusiva do número do modelo atribuída pelo fabricante a este dispositivo. Os números de modelo não são versões, mas identificadores exclusivos que identificam uma configuração de modelo específica. |
| `screenHeight` | Número inteiro | O número de pixels verticais da exibição ativa do dispositivo na orientação padrão. |
| `screenOrientation` | String | A orientação atual da tela. Os valores aceitos incluem `portrait` e `landscape`. |
| `screenWidth` | String | O número de pixels horizontais da exibição ativa do dispositivo na orientação padrão. |
| `type` | String | O tipo de dispositivo que está sendo rastreado. Os valores aceitos incluem: <ul><li>`mobile`</li><li>`tablet`</li><li>`desktop`</li><li>`ereader`</li><li>`gaming`</li><li>`television`</li><li>`settop`</li><li>`mediaplayer`</li><li>`computers`</li><li>`tv screens`</li></ul> |
| `typeID` | String | Um identificador para o dispositivo. Este pode ser um identificador do DeviceAtlas ou de outro serviço que identifica o hardware que está sendo usado. |
| `typeIDService` | String | A namespace do serviço usado para identificar o tipo de dispositivo. Consulte o [apêndice](#typeIDService) para obter detalhes sobre os valores aceitos. |

Para obter mais detalhes sobre a mistura, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/device.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/device.schema.json)

## Apêndice

A seção a seguir contém informações adicionais sobre o tipo de dados do [!UICONTROL Dispositivo] .

## Valores aceitos para typeIDService {#typeIDService}

A tabela a seguir descreve os valores aceitos para `typeIDService` e seus significados associados:

| Valor | Descrição |
| --- | --- |
| `https://ns.adobe.com/xdm/external/deviceatlas` | O dispositivo foi identificado usando o DeviceAtlas. |
| `https://ns.adobe.com/xdm/external/adobecampaign` | O dispositivo foi identificado usando o Adobe Campaign. |