---
keywords: Experience Platform;início;tópicos populares;esquema;Esquema;XDM;campos;esquemas;Esquemas;dispositivo;tipo de dados;tipo de dados;tipo de dados;
solution: Experience Platform
title: Tipo de dados do dispositivo
description: Saiba mais sobre o tipo de dados XDM do dispositivo.
exl-id: 049a2ca1-6bc3-4b9c-832a-77102e8a0ed2
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 17%

---

# Tipo de dados [!UICONTROL Dispositivo]

[!UICONTROL Dispositivo] é um tipo de dados XDM padrão que descreve um dispositivo identificado. Um dispositivo é um aplicativo ou instância do navegador que pode ser rastreado entre as sessões, normalmente por cookies.

![](../images/data-types/device.png){width=450}

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `colorDepth` | Número inteiro | O número de cores que a tela pode representar. |
| `manufacturer` | String | O nome da organização que possui o design e a criação do dispositivo. |
| `model` | String | O nome do modelo do dispositivo. Esse é o nome comum, legível ou de marketing do dispositivo. Por exemplo, o &quot;iPhone 6S&quot; é um modelo específico de celular. |
| `modelNumber` | String | A designação do número do modelo único atribuída pelo fabricante para este dispositivo. Os números de modelo não são versões, mas identificadores exclusivos que identificam uma configuração de modelo específica. |
| `screenHeight` | Número inteiro | O número de pixels verticais da tela ativa do dispositivo na orientação padrão. |
| `screenOrientation` | String | A orientação atual da tela. Os valores aceitos incluem `portrait` e `landscape`. |
| `screenWidth` | String | O número de pixels horizontais da tela ativa do dispositivo na orientação padrão. |
| `type` | String | O tipo de dispositivo sendo rastreado. Os valores aceitos incluem: <ul><li>`mobile`</li><li>`tablet`</li><li>`desktop`</li><li>`ereader`</li><li>`gaming`</li><li>`television`</li><li>`settop`</li><li>`mediaplayer`</li><li>`computers`</li><li>`tv screens`</li></ul> |
| `typeID` | String | Um identificador do dispositivo. Pode ser um identificador do DeviceAtlas ou de outro serviço que identifica o hardware que está sendo usado. |
| `typeIDService` | String | O namespace do serviço usado para identificar o tipo de dispositivo. Consulte o [apêndice](#typeIDService) para obter detalhes sobre valores aceitos. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o grupo de campos, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/device.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/device.schema.json)

## Apêndice

A seção a seguir contém informações adicionais sobre o tipo de dados [!UICONTROL Dispositivo].

## Valores aceitos para typeIDService {#typeIDService}

A tabela a seguir descreve os valores aceitos para `typeIDService` e seus significados associados:

| Valor | Descrição |
| --- | --- |
| `https://ns.adobe.com/xdm/external/deviceatlas` | O dispositivo foi identificado usando o DeviceAtlas. |
| `https://ns.adobe.com/xdm/external/adobecampaign` | O dispositivo foi identificado usando Adobe Campaign. |
