---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;individual profile;fields;schemas;Schemas;loyalty details;Schema design;field group;Field group;
solution: Experience Platform
title: Loyalty Details Schema Field Group
topic-legacy: overview
description: Este documento fornece uma visão geral do grupo de campos Detalhes da Fidelidade .
source-git-commit: afe748d443aad7b6da5b348cd569c9e806e4419b
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 3%

---


# [!UICONTROL Loyalty Details] schema field group

>[!NOTE]
>
>Os nomes de vários grupos de campos de esquema foram alterados. Consulte o documento em [atualizações do nome do grupo de campos](../name-updates.md) para obter mais informações.

[!UICONTROL Loyalty Details] is a standard schema field group for the [[!DNL XDM Individual Profile] class](../../classes/individual-profile.md). O grupo de campos fornece um único campo do tipo de objeto, `loyalty`, que captura informações relacionadas à associação de uma pessoa em um programa de fidelidade do cliente.

![](../../images/field-groups/loyalty-details.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `pointsExpiration` | Matriz de objetos | Lista quaisquer pontos de fidelidade (ou grupos de pontos de fidelidade) que irão expirar e as datas em que expirarão. Cada item de matriz deve ser um objeto que contenha as duas propriedades a seguir: <ul><li>`pointsExpirationDate`: Um datetime ISO 8601 de quando os pontos expirarão.</li><li>`pointsExpiring`: O saldo do ponto que expira a partir da data de expiração associada.</li></ul> |
| `joinDate` | DateTime | An ISO 8601 datetime of when the person joined the loyalty program. |
| `loyaltyID` | Array of strings | Representa as IDs do programa de fidelidade associadas ao membro do programa de fidelidade. |
| `points` | Duplo | O saldo atual de pontos de fidelidade ou prêmios para o membro de fidelidade. |
| `pointsRedeemed` | Duplo | A quantidade de pontos que o membro do programa de fidelidade aplicou a uma compra ou resgatou de outra forma. |
| `program` | String | O nome do programa de fidelidade em que a pessoa está inscrita. |
| `status` | String | O status atual da associação de fidelidade da pessoa, como `active`, `disabled` ou `suspended`. |
| `tier` | String | Captura o nível do programa de fidelidade em que a pessoa está inscrita. |
| `upgradeDate` | String | The date when the loyalty member was upgraded to their most recent tier level. |

{style=&quot;table-layout:auto&quot;}

Para obter mais detalhes sobre o grupo de campos, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-loyalty-details.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-loyalty-details.schema.json)
