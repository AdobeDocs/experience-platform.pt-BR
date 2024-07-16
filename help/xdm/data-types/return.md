---
title: Tipo de dados de retorno
description: Saiba mais sobre o tipo de dados Return Experience Data Model (XDM).
exl-id: 1fd99a25-547f-49e7-8980-dda7db2ebb8a
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 8%

---

# [!UICONTROL Retornar] tipo de dados

[!UICONTROL Retornar] é um tipo de dados padrão do Experience Data Model (XDM) que captura as informações essenciais relacionadas a uma Autorização de devolução de produto (RMA).

![Um diagrama do tipo de dados Return.](../images/data-types/return.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
|----------------------------------|----------------------|-----------|--------------------------------------------------|
| [!UICONTROL ID de Retorno] | `returnID` | sequência de caracteres | O identificador exclusivo desta ADM. |
| [!UICONTROL Retornar Status] | `returnStatus` | sequência de caracteres | O status atual da RMA (por exemplo, Pendente ou Fechada). |
| [!UICONTROL ID de Compra da Ordem] | `purchaseID` | sequência de caracteres | O identificador exclusivo da ordem/compra à qual a RMA pertence. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/return.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/return.schema.json)
