---
title: Classe do pagador
description: Este documento fornece uma visão geral da classe Payer no Experience Data Model (XDM).
source-git-commit: 3937963ceee8502b0669a3f007fd38ecf2824e9b
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 5%

---

# [!UICONTROL Pagador] classe

No Experience Data Model (XDM), a variável [!UICONTROL Pagador] A classe captura o conjunto mínimo de propriedades que definem uma entidade de negócios pagador que coleta dados pertencentes a companhias de seguros (como seguro de saúde).

![Estrutura de classes](../images/classes/payer.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `_id` | [!UICONTROL String] | Um identificador de string exclusivo gerado pelo sistema para o registro. Este campo é usado para rastrear a exclusividade de um registro individual, evitar a duplicação de dados e buscar esse registro em serviços downstream.<br><br>Como esse campo é gerado pelo sistema, ele não recebe um valor explícito durante a assimilação de dados. No entanto, ainda é possível optar por fornecer seus próprios valores de ID exclusivos. |
| `payerId` | [!UICONTROL String] | Um identificador exclusivo para o ordenante. |
| `payerName` | [!UICONTROL String] | O nome do pagador. |

{style=&quot;table-layout:auto&quot;}
