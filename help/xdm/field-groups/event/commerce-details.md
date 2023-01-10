---
keywords: Experience Platform, home, tópicos populares, esquema, Esquema, XDM, ExperienceEvent, campos, esquemas, Esquemas, Design de esquema, grupo de campos, grupo de campos;
solution: Experience Platform
title: Grupo de Campos do Esquema de Detalhes do Comércio
description: Este documento fornece uma visão geral do grupo de campos Detalhes de comércio .
exl-id: 36aba186-fadb-4abb-a94f-7e151ff3f744
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 3%

---

# [!UICONTROL Detalhes de comércio] grupo de campos de esquema

>[!NOTE]
>
>Os nomes de vários grupos de campos de esquema foram alterados. Consulte o documento em [atualizações de nome do grupo de campos](../name-updates.md) para obter mais informações.

[!UICONTROL Detalhes de comércio] é um grupo de campos de esquema padrão para a variável [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md), usado para descrever dados de comércio, como informações do produto (SKU, nome, quantidade) e operações padrão do carrinho (pedido, check-out, abandono).

![](../../images/field-groups/commerce-details.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `commerce` | [Commerce](../../data-types/commerce.md) | Um objeto que descreve retornos de produtos, registro em garantia e processos de carrinho/pedido de compras. |
| `productListItems` | Matriz de [Itens da lista de produtos](../../data-types/product-list-item.md) | Uma lista de itens que representa o(s) produto(s) selecionado(s) por um cliente, com opções e preços específicos em um ponto de tempo específico (que pode diferir do registro do produto). |

{style=&quot;table-layout:auto&quot;}

Para obter mais detalhes sobre o grupo de campos, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-commerce.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-commerce.schema.json)
