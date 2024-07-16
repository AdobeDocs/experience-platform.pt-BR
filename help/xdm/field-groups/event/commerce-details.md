---
keywords: Experience Platform;início;tópicos populares;esquema;Esquema;XDM;ExperienceEvent;campos;esquemas;Esquemas;Design de esquema;grupo de campos;grupo de campos;
solution: Experience Platform
title: Grupo de campos de esquema de detalhes do Commerce
description: Saiba mais sobre o grupo de campos de esquema Detalhes do Commerce.
exl-id: 36aba186-fadb-4abb-a94f-7e151ff3f744
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 3%

---

# [!UICONTROL Detalhes do Commerce] grupo de campos de esquema

>[!NOTE]
>
>Os nomes de vários grupos de campos de esquema foram alterados. Consulte o documento em [atualizações de nome de grupo de campos](../name-updates.md) para obter mais informações.

[!UICONTROL Detalhes do Commerce] é um grupo de campos de esquema padrão para a [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md), usado para descrever dados de comércio, como informações do produto (SKU, nome, quantidade) e operações padrão do carrinho (pedido, check-out, abandono).

![](../../images/field-groups/commerce-details.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `commerce` | [Comércio](../../data-types/commerce.md) | Um objeto que descreve devoluções de produtos, registro de garantia e carrinho de compras/processos de pedido. |
| `productListItems` | Matriz de [itens da lista de produtos](../../data-types/product-list-item.md) | Uma lista de itens que representam os produtos selecionados por um cliente, com opções e preços específicos em um momento específico (que pode diferir do registro do produto). |

{style="table-layout:auto"}

Para obter mais detalhes sobre o grupo de campos, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-commerce.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-commerce.schema.json)
