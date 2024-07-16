---
title: Tipo de Dados do Item de Retorno
description: Saiba mais sobre o tipo de dados Modelo de dados de experiência de item de retorno (XDM).
exl-id: e703d65b-a133-484e-96d6-6b1f50fc1e48
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 7%

---

# Tipo de dados [!UICONTROL Retornar Item]

[!UICONTROL Retornar Item] é um tipo de dados padrão do Experience Data Model (XDM) que captura detalhes essenciais relacionados ao processo de devolução de um item comprado.

![Um diagrama do tipo de dados Item de Retorno.](../images/data-types/return-item.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
|-----------------------------|------------------------------|-----------|--------------------------------------------------------|
| [!UICONTROL Retornar Status] | `returnStatus` | sequência de caracteres | O status do item retornado (por exemplo, Pendente ou Aprovado). |
| [!UICONTROL Motivo da Devolução] | `returnReason` | sequência de caracteres | O motivo pelo qual a devolução foi solicitada para o item. |
| [!UICONTROL Condição de Item de Retorno] | `returnItemCondition` | sequência de caracteres | A condição do item para o qual a devolução é solicitada. |
| [!UICONTROL Resolução de Retorno] | `returnResolution` | sequência de caracteres | A resolução ou resultado desejado esperado da devolução (por exemplo, Reembolso ou Troca). |
| [!UICONTROL Quantidade de Devolução Solicitada] | `returnQuantityRequested` | inteiro | A quantidade do item que o comprador solicitou devolver. |
| [!UICONTROL Quantidade de Devolução Autorizada] | `returnQuantityAuthorized` | inteiro | A quantidade do item autorizado a ser devolvido. |
| [!UICONTROL Quantidade de Devolução Recebida] | `returnQuantityReceived` | inteiro | A quantidade de itens devolvidos recebidos. |
| [!UICONTROL Quantidade de Devoluções Aprovada] | `returnQuantityApproved` | inteiro | A quantidade do item com uma devolução totalmente concluída e aprovada. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/returnitem.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/returnitem.schema.json)
