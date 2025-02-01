---
keywords: Experience Platform;página inicial;tópicos populares;esquema;Esquema;XDM;campos;esquemas;Esquemas;endereço;xdm:endereço;tipo de dados;tipo de dados;tipo de dados;
solution: Experience Platform
title: Tipo de Dados do Endereço Postal
description: Saiba mais sobre o tipo de dados XDM do endereço postal.
exl-id: 94457fe5-80bc-4822-9f6c-48f77d56c89b
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 23%

---

# Tipo de dados [!UICONTROL Endereço postal]

[!UICONTROL Endereço postal] é um tipo de dados XDM padrão que descreve os detalhes de um endereço para correspondência.

![](../images/data-types/postal-address.png){width=450}

| Propriedade | Descrição |
| --- | --- |
| `city` | O nome da cidade. |
| `country` | O nome do território administrado pelo governo. Este é um campo de formato livre que pode ter o nome do país em qualquer idioma. |
| `countryCode` | O código <a href="https://datahub.io/core/country-list">ISO 3166-1 alpha-2</a> de dois caracteres para o país. |
| `createdByBatchID` | A ID do arquivo de lote assimilado que criou o registro de endereço. |
| `dmaID` | A área de mercado designada de pesquisa de mídia da Nielsen. |
| `label` | Um nome de formato livre para o endereço. |
| `lastVerifiedDate` | A data em que o endereço foi verificado pela última vez como ainda associado à pessoa. |
| `modifiedByBatchID` | A ID do arquivo de lote assimilado que modificou o registro pela última vez. |
| `msaID` | A área estatística metropolitana dos Estados Unidos onde ocorreu a observação. |
| `postOfficeBox` | A caixa postal do endereço. |
| `postalCode` | O código postal do local. Os códigos postais não estão disponíveis para todos os países. Em alguns países, conterá apenas parte do código postal. |
| `primary` | Um valor booleano que indica se este é o endereço principal do indivíduo. Um perfil pode ter apenas um endereço `primary` em um determinado momento. |
| `region` | A parte da região, cidade ou distrito do endereço. |
| `repositoryCreatedBy` | A ID do usuário que criou o registro. |
| `repositoryLastModifiedBy` | A ID do usuário que modificou o registro pela última vez. |
| `stateProvince` | A parte do estado ou província da observação. O formato segue o padrão [ISO 3166-2 (país e subdivisão)](https://www.unece.org/cefact/locode/subdivisions.html). |
| `status` | Indica se o endereço pode ser usado no momento. |
| `statusReason` | Uma descrição do `status` atual. |
| `street1` - `street4` | Esses quatro campos devem conter informações no nível da rua principal, número do apartamento, número da rua e nome da rua. `street2` a `street4` são opcionais. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o tipo de dados do endereço postal, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/address.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/address.schema.json)
