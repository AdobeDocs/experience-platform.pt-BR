---
title: Classe do provedor
description: Saiba mais sobre a classe Provedor no Experience Data Model (XDM).
exl-id: acb9b8a3-f911-49c5-9d2a-3a0d6aeebef9
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 4%

---

# [!UICONTROL Provedor] classe

No Experience Data Model (XDM), a variável [!UICONTROL Provedor] a classe captura o conjunto mínimo de propriedades que definem uma entidade comercial do provedor (como um provedor de assistência médica ou de seguro).

![Estrutura de classe](../images/classes/provider.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `providerName` | [[!UICONTROL Nome da pessoa]](../data-types/person-name.md) | O nome do provedor. |
| `_id` | [!UICONTROL String] | Um identificador de sequência de caracteres exclusivo gerado pelo sistema para o registro. Este campo é usado para rastrear a exclusividade de um registro individual, impedir a duplicação de dados e pesquisar esse registro nos serviços downstream.<br><br>Como esse campo é gerado pelo sistema, ele não recebe um valor explícito durante a assimilação de dados. No entanto, você ainda pode optar por fornecer seus próprios valores de ID exclusivos, se desejar. |
| `providerId` | [!UICONTROL String] | Um identificador exclusivo do provedor. |

{style="table-layout:auto"}

A classe pode ser estendida com a variável [[!UICONTROL Provedor de assistência médica] grupo de campos](../field-groups/provider/healthcare-provider.md) para descrever mais detalhes sobre um prestador de cuidados de saúde.
