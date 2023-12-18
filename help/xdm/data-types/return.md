---
title: Tipo de dados de retorno
description: Saiba mais sobre o tipo de dados Return Experience Data Model (XDM).
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 6%

---

# [!UICONTROL Retornar] tipo de dados

[!UICONTROL Retornar] é um tipo de dados padrão do Experience Data Model (XDM) que captura as informações essenciais relacionadas a uma Autorização de devolução de produto (RMA).

![Um diagrama do tipo de dados Return.](../images/data-types/return.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
|----------------------------------|----------------------|-----------|--------------------------------------------------|
| [!UICONTROL ID de devolução] | `returnID` | string | O identificador exclusivo desta ADM. |
| [!UICONTROL Status de retorno] | `returnStatus` | string | O status atual da RMA (por exemplo, Pendente ou Fechada). |
| [!UICONTROL ID de compra do pedido] | `purchaseID` | string | O identificador exclusivo da ordem/compra à qual a RMA pertence. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/return.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/return.schema.json)

