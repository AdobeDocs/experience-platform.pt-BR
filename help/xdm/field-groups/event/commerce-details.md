---
keywords: Experience Platform;início;tópicos populares;esquema;Esquema;XDM;ExperienceEvent;campos;esquemas;Esquemas;Design de esquema;grupo de campos;grupo de campos;
solution: Experience Platform
title: Grupo de campos de esquema de detalhes de comércio
description: Este documento fornece uma visão geral do grupo de campos de esquema Detalhes do comércio.
exl-id: 36aba186-fadb-4abb-a94f-7e151ff3f744
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 1%

---

# [!UICONTROL Detalhes do comércio] grupo de campos de esquema

>[!NOTE]
>
>Os nomes de vários grupos de campos de esquema foram alterados. Consulte o documento sobre [atualizações do nome do grupo de campos](../name-updates.md) para obter mais informações.

[!UICONTROL Detalhes do comércio] é um grupo de campos de esquema padrão para o [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md), usado para descrever dados de comércio, como informações do produto (SKU, nome, quantidade) e operações padrão do carrinho (pedido, check-out, abandono).

![](../../images/field-groups/commerce-details.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `commerce` | [Commerce](../../data-types/commerce.md) | Um objeto que descreve devoluções de produtos, registro de garantia e carrinho de compras/processos de pedido. |
| `productListItems` | Matriz de [Itens da lista de produtos](../../data-types/product-list-item.md) | Uma lista de itens que representam os produtos selecionados por um cliente, com opções e preços específicos em um momento específico (que pode diferir do registro do produto). |

{style="table-layout:auto"}

Para obter mais detalhes sobre o grupo de campos, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-commerce.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-commerce.schema.json)
