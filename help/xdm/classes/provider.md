---
title: Classe do Provedor
description: Este documento fornece uma visão geral da classe Provedor no Experience Data Model (XDM).
source-git-commit: cf39f943e27cd11b0eabbc344774fa12482a8f92
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 4%

---

# [!UICONTROL Provedor] classe

No Experience Data Model (XDM), a variável [!UICONTROL Provedor] captura o conjunto mínimo de propriedades que definem uma entidade de negócios provedor (como um provedor de saúde ou um provedor de seguros).

![Estrutura de classes](../images/classes/provider.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `providerName` | [[!UICONTROL Nome da pessoa]](../data-types/person-name.md) | O nome do provedor. |
| `_id` | [!UICONTROL String] | Um identificador de string exclusivo gerado pelo sistema para o registro. Este campo é usado para rastrear a exclusividade de um registro individual, evitar a duplicação de dados e buscar esse registro em serviços downstream.<br><br>Como esse campo é gerado pelo sistema, ele não recebe um valor explícito durante a assimilação de dados. No entanto, ainda é possível optar por fornecer seus próprios valores de ID exclusivos. |
| `providerId` | [!UICONTROL String] | Um identificador exclusivo para o provedor. |

{style=&quot;table-layout:auto&quot;}

A classe pode ser estendida com a variável [[!UICONTROL Provedor de saúde] grupo de campos](../field-groups/provider/healthcare-provider.md) descrever mais detalhes sobre um prestador de cuidados de saúde.
