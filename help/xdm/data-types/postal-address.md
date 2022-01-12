---
keywords: Experience Platform, home, tópicos populares, esquema, esquema, XDM, campos, esquemas, esquemas, endereço, xdm:endereço, tipo de dados, tipo de dados, tipo de dados;
solution: Experience Platform
title: Tipo de dados do endereço postal
topic-legacy: overview
description: Este documento fornece uma visão geral do tipo de dados XDM de Endereço Postal.
exl-id: 94457fe5-80bc-4822-9f6c-48f77d56c89b
source-git-commit: dc81da58594fac4ce304f9d030f2106f0c3de271
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 1%

---

# [!UICONTROL Endereço postal] tipo de dados

[!UICONTROL Endereço postal] é um tipo de dados XDM padrão que descreve os detalhes de um endereço de correspondência.

<img src="../images/data-types/postal-address.png" width="450" /><br />

| Propriedade | Descrição |
| --- | --- |
| `city` | O nome da cidade. |
| `country` | O nome do território administrado pelo governo. Este é um campo de forma livre que pode ter o nome do país em qualquer idioma. |
| `countryCode` | Os dois caracteres <a href="https://datahub.io/core/country-list">ISO 3166-1 alfa-2</a> código do país. |
| `createdByBatchID` | A ID do arquivo de lote assimilado que criou o registro de endereço. |
| `dmaID` | A pesquisa de mídia da Nielsen designou área de mercado. |
| `label` | Um nome de forma livre para o endereço. |
| `lastVerifiedDate` | A data em que o endereço foi verificado pela última vez como ainda associado à pessoa. |
| `modifiedByBatchID` | A ID do arquivo de lote assimilado que modificou o registro pela última vez. |
| `msaID` | A área estatística metropolitana dos Estados Unidos onde ocorreu a observação. |
| `postOfficeBox` | A caixa postal do endereço. |
| `postalCode` | O código postal da localização. Os códigos postais não estão disponíveis para todos os países. Em alguns países, apenas fará parte do código postal. |
| `primary` | Um valor booleano que indica se esse é o endereço principal do indivíduo. Um perfil pode ter apenas um `primary` endereço em um determinado momento. |
| `region` | A região, município ou porção do distrito do endereço. |
| `repositoryCreatedBy` | A ID do usuário que criou o registro. |
| `repositoryLastModifiedBy` | A ID do usuário que modificou o registro pela última vez. |
| `stateProvince` | O estado ou parte de província da observação. O formato segue o [ISO 3166-2 (país e subdivisão)](https://www.unece.org/cefact/locode/subdivisions.html) padrão. |
| `status` | Indica se o endereço pode ser usado no momento. |
| `statusReason` | Uma descrição do atual `status`. |
| `street1` - `street4` | Esses quatro campos devem conter informações primárias sobre o nível da rua, número do apartamento, número da rua e nome da rua. `street2` para `street4` são opcionais. |

{style=&quot;table-layout:auto&quot;}

Para obter mais detalhes sobre o tipo de dados de endereço postal, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/address.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/address.schema.json)
