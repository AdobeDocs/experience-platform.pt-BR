---
title: Tipo de Dados do Endereço Postal
description: Saiba mais sobre o tipo de dados Modelo de dados de experiência de endereço postal (XDM).
exl-id: 92385cd8-60c8-4360-a8e7-e6224e85e4d4
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 42%

---

# Tipo de dados [!UICONTROL Endereço Postal]

[!UICONTROL Endereço Postal] é um tipo de dados padrão do Experience Data Model (XDM) que fornece detalhes de endereço.

![Um diagrama do tipo de dados [!UICONTROL Endereço Postal].](../images/data-types/postal-address.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
|------------------------------------|------------------|-----------|-----------------------------------------------------------------------------------------------|
| [!UICONTROL Principal] | `primary` | booleano | Indicador de endereço principal. Um perfil pode ter apenas um endereço `primary` em um determinado momento. |
| [!UICONTROL Rótulo] | `label` | sequência de caracteres | Nome do endereço de forma livre. |
| [!UICONTROL Rua 1] | `street1` | sequência de caracteres | Informações no nível da rua principal, número do apartamento, número da rua e nome da rua. |
| [!UICONTROL Rua 2] | `street2` | sequência de caracteres | Segunda linha opcional de informações da rua. |
| [!UICONTROL Rua 3] | `street3` | sequência de caracteres | Terceira linha opcional de informações da rua. |
| [!UICONTROL Rua 4] | `street4` | sequência de caracteres | Quarta linha opcional de informações da rua. |
| [!UICONTROL Região] | `region` | sequência de caracteres | A parte da região, cidade ou distrito do endereço. |
| [!UICONTROL caixa do escritório da Post] | `postOfficeBox` | sequência de caracteres | Caixa postal do endereço. |
| [!UICONTROL Country] | `country` | sequência de caracteres | O nome do território administrado pelo governo. Além de ``countryCode``, este é um campo de forma livre que pode ter o nome do país em qualquer idioma. |
| [!UICONTROL Estado] | `state` | sequência de caracteres | O nome do Estado é um campo de forma livre. |
| [!UICONTROL Status] | `status` | sequência de caracteres | Uma indicação quanto à capacidade de usar o endereço. |
| [!UICONTROL Motivo do status] | `statusReason` | sequência de caracteres | Uma descrição do status atual. |
| [!UICONTROL Última data verificada] | `lastVerifiedDate` | sequência de caracteres | A data em que o endereço foi verificado pela última vez como ainda associado à pessoa. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o tipo de dados, consulte o [esquema completo](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/address.schema.json) no repositório XDM público:
