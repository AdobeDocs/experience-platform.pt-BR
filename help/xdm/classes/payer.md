---
title: Classe do pagador
description: Saiba mais sobre a classe Payer no Experience Data Model (XDM).
exl-id: 8d3e0a6d-41eb-4ffe-81dd-c7b7d532a531
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 5%

---

# Classe [!UICONTROL Payer]

No Experience Data Model (XDM), a classe [!UICONTROL Payer] captura o conjunto mínimo de propriedades que definem uma entidade de negócios do pagador que coleta dados relativos às empresas de seguros (como seguro de saúde).

![Estrutura de classe](../images/classes/payer.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `_id` | [!UICONTROL String] | Um identificador de sequência de caracteres exclusivo gerado pelo sistema para o registro. Este campo é usado para rastrear a exclusividade de um registro individual, impedir a duplicação de dados e pesquisar esse registro nos serviços downstream.<br><br>Como este campo é gerado pelo sistema, ele não receberá um valor explícito durante a assimilação de dados. No entanto, você ainda pode optar por fornecer seus próprios valores de ID exclusivos, se desejar. |
| `payerId` | [!UICONTROL String] | Um identificador exclusivo do pagador. |
| `payerName` | [!UICONTROL String] | O nome do pagador. |

{style="table-layout:auto"}
