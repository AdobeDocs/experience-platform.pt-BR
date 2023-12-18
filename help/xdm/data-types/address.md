---
title: Tipo de Dados do Endereço Postal
description: Saiba mais sobre o tipo de dados Modelo de dados de experiência de endereço postal (XDM).
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 9%

---

# [!UICONTROL Endereço postal] tipo de dados

[!UICONTROL Endereço postal] é um tipo de dados padrão do Experience Data Model (XDM) que fornece detalhes de endereço.

![Um diagrama do [!UICONTROL Endereço postal] tipo de dados.](../images/data-types/postal-address.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
|------------------------------------|------------------|-----------|-----------------------------------------------------------------------------------------------|
| [!UICONTROL Principal] | `primary` | booleano | Indicador de endereço principal. Um perfil pode ter apenas um `primary` em um determinado momento. |
| [!UICONTROL Rótulo] | `label` | string | Nome do endereço de forma livre. |
| [!UICONTROL Folha 1] | `street1` | string | Informações no nível da rua principal, número do apartamento, número da rua e nome da rua. |
| [!UICONTROL Folha 2] | `street2` | string | Segunda linha opcional de informações da rua. |
| [!UICONTROL Folha 3] | `street3` | string | Terceira linha opcional de informações da rua. |
| [!UICONTROL Folha 4] | `street4` | string | Quarta linha opcional de informações da rua. |
| [!UICONTROL Região] | `region` | string | A parte da região, cidade ou distrito do endereço. |
| [!UICONTROL Caixa de correio] | `postOfficeBox` | string | Caixa postal do endereço. |
| [!UICONTROL Country] | `country` | string | O nome do território administrado pelo governo. Exceto ``countryCode``, este é um campo de formato livre que pode ter o nome do país em qualquer idioma. |
| [!UICONTROL Estado] | `state` | string | O nome do Estado. Este é um campo de forma livre. |
| [!UICONTROL Status] | `status` | string | Uma indicação quanto à capacidade de usar o endereço. |
| [!UICONTROL Motivo do status] | `statusReason` | string | Uma descrição do status atual. |
| [!UICONTROL Última data verificada] | `lastVerifiedDate` | string | A data em que o endereço foi verificado pela última vez como ainda associado à pessoa. |

{style="table-layout:auto"}

Para obter mais informações sobre o tipo de dados, consulte a [esquema completo](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/address.schema.json) no repositório XDM público:
