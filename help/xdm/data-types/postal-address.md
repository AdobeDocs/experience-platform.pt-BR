---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;address;xdm:address;datatype;data-type;data type;
solution: Experience Platform
title: Tipo de dados do endereço postal
topic: overview
description: Este documento fornece uma visão geral do tipo de dados XDM de Endereço Postal.
translation-type: tm+mt
source-git-commit: 6a7967ac9e652c7e73fd713e89a9079287cf0ae5
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 0%

---


# [!UICONTROL Tipo de dados do endereço] postal

[!UICONTROL O endereço] postal é um tipo de dados XDM padrão que descreve os detalhes de um endereço de correspondência.

<img src="../images/data-types/postal-address.png" width="450" /><br />

| Propriedade | Descrição |
| --- | --- |
| `city` | O nome da cidade. |
| `country` | O nome do território administrado pelo governo. Este é um campo de forma livre que pode ter o nome do país em qualquer idioma. |
| `countryCode` | O código <a href="https://datahub.io/core/country-list">ISO 3166-1 alfa-2</a> de dois caracteres para o país. |
| `createdByBatchID` | A ID do arquivo de lote ingerido que criou o registro de endereço. |
| `dmaID` | A investigação sobre os meios de comunicação social Nielsen designou a área de mercado. |
| `label` | Um nome de forma livre para o endereço. |
| `lastVerifiedDate` | A data em que o endereço foi verificado pela última vez como ainda associado à pessoa. |
| `modifiedByBatchID` | A ID do arquivo de lote ingerido que modificou o registro pela última vez. |
| `msaID` | A área metropolitana de estatística dos Estados Unidos onde ocorreu a observação. |
| `postOfficeBox` | A caixa postal do endereço. |
| `postalCode` | O código postal da localização. Os códigos postais não estão disponíveis para todos os países. Em alguns países, este código só contém uma parte do código postal. |
| `primary` | Um valor booliano que indica se este é o endereço principal do indivíduo. Um perfil pode ter apenas um `primary` endereço em um determinado momento. |
| `region` | A região, o condado ou a parte do distrito do endereço. |
| `repositoryCreatedBy` | A ID do usuário que criou o registro. |
| `repositoryLastModifiedBy` | A ID do usuário que modificou o registro pela última vez. |
| `stateProvince` | A parte do estado ou província da observação. O formato segue a norma [ISO 3166-2 (país e subdivisão)](http://www.unece.org/cefact/locode/subdivisions.html) . |
| `status` | Indica se o endereço pode ser usado no momento. |
| `statusReason` | Uma descrição do atual `status`. |
| `street1` - `street4` | Esses quatro campos devem conter informações primárias de nível de rua, número do apartamento, número da rua e nome da rua. `street2` são `street4` opcionais. |

Para obter mais detalhes sobre o tipo de dados de endereço postal, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/address.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/address.schema.json)