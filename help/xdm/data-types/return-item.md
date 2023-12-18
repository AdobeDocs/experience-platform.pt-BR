---
title: Tipo de Dados do Item de Retorno
description: Saiba mais sobre o tipo de dados Modelo de dados de experiência de item de retorno (XDM).
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 6%

---

# [!UICONTROL Retornar item] tipo de dados

[!UICONTROL Retornar item] O é um tipo de dados padrão do Experience Data Model (XDM) que captura detalhes essenciais relacionados ao processo de devolução de um item comprado.

![Um diagrama do tipo de dados Item de Retorno.](../images/data-types/return-item.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
|-----------------------------|------------------------------|-----------|--------------------------------------------------------|
| [!UICONTROL Status de retorno] | `returnStatus` | string | O status do item retornado (por exemplo, Pendente ou Aprovado). |
| [!UICONTROL Motivo da Devolução] | `returnReason` | string | O motivo pelo qual a devolução foi solicitada para o item. |
| [!UICONTROL Condição de Item de Devolução] | `returnItemCondition` | string | A condição do item para o qual a devolução é solicitada. |
| [!UICONTROL Resolução de devolução] | `returnResolution` | string | A resolução ou resultado desejado esperado da devolução (por exemplo, Reembolso ou Troca). |
| [!UICONTROL Quantidade de Devolução Solicitada] | `returnQuantityRequested` | inteiro | A quantidade do item que o comprador solicitou devolver. |
| [!UICONTROL Quantidade de Devolução Autorizada] | `returnQuantityAuthorized` | inteiro | A quantidade do item autorizado a ser devolvido. |
| [!UICONTROL Quantidade de Devolução Recebida] | `returnQuantityReceived` | inteiro | A quantidade de itens devolvidos recebidos. |
| [!UICONTROL Quantidade de Devolução Aprovada] | `returnQuantityApproved` | inteiro | A quantidade do item com uma devolução totalmente concluída e aprovada. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/returnitem.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/returnitem.schema.json)
