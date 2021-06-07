---
keywords: Experience Platform, home, tópicos populares, esquema, Esquema, XDM, ExperienceEvent, campos, esquemas, Esquemas, Design de esquema, grupo de campos, grupo de campos;
solution: Experience Platform
title: Grupo de Campos do Esquema de Detalhes do Comércio
topic-legacy: overview
description: Este documento fornece uma visão geral do grupo de campos Detalhes de comércio .
source-git-commit: b22dce52563d5f3bbd1796c11d7c7b2a49fa6d5f
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 3%

---


# [!UICONTROL Grupo de campos ] de esquema Detalhes do Comércio

>[!NOTE]
>
>Os nomes de vários grupos de campos de esquema foram alterados. Consulte o documento em [atualizações do nome do grupo de campos](../name-updates.md) para obter mais informações.

[!UICONTROL Commerce ] Details é um grupo de campos de esquema padrão para a  [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md), usado para descrever dados de comércio, como informações do produto (SKU, nome, quantidade) e operações padrão do carrinho (ordem, check-out, abandono).

![](../../images/field-groups/commerce-details.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `commerce` | [Comércio](../../data-types/commerce.md) | Um objeto que descreve retornos de produtos, registro em garantia e processos de carrinho/pedido de compras. |
| `productListItems` | Matriz de [Itens da lista de produtos](../../data-types/product-list-item.md) | Uma lista de itens que representa o(s) produto(s) selecionado(s) por um cliente, com opções e preços específicos em um ponto de tempo específico (que pode diferir do registro do produto). |

{style=&quot;table-layout:auto&quot;}

Para obter mais detalhes sobre o grupo de campos, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-commerce.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-commerce.schema.json)
