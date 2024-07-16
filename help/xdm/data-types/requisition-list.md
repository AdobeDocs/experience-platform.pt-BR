---
title: Tipo de Dados da Lista de Requisições
description: Saiba mais sobre o tipo de dados Modelo de Dados de Experiência da Lista de Requisições (XDM).
exl-id: cbea6b08-9d4d-4cbe-b0c5-506bccc6df67
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 7%

---

# Tipo de dados [!UICONTROL Lista de Requisições]

[!UICONTROL Lista de Requisições] é um tipo de dados padrão do Experience Data Model (XDM) que descreve uma coleção de itens com curadoria para compras. Use o tipo de dados [!UICONTROL Lista de Requisições] para identificar e descrever listas de requisições.

![Um diagrama do tipo de dados [!UICONTROL Lista de Requisições].](../images/data-types/requisition-list.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
|---------------------------|-------------------|-----------|--------------------------------------------------|
| [!UICONTROL ID da Lista de Requisições] | `ID` | sequência de caracteres | O identificador exclusivo da lista de requisições. |
| [!UICONTROL Nome da Lista de Requisições] | `name` | sequência de caracteres | O nome da lista de requisições especificada pelo cliente. |
| [!UICONTROL Descrição da Lista de Requisições] | `description` | sequência de caracteres | Uma descrição da lista de requisições especificada pelo cliente. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/requisitionlist.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/requisitionlist.schema.json)
