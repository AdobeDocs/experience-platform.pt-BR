---
keywords: Experience Platform;página inicial;tópicos populares;esquema;Esquema;XDM;perfil individual;campos;esquemas;Esquemas;detalhes de fidelidade;Design de esquema;grupo de campos;Grupo de campos;
solution: Experience Platform
title: Grupo de Campos de Esquema de Detalhes de Fidelidade
description: Saiba mais sobre o grupo de campos de esquema Detalhes de fidelidade.
exl-id: 12c9fef5-4f9e-49b5-894f-f4938bb95c23
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 3%

---

# [!UICONTROL Detalhes de fidelidade] grupo de campos de esquema

>[!NOTE]
>
>Os nomes de vários grupos de campos de esquema foram alterados. Consulte o documento em [atualizações de nome de grupo de campos](../name-updates.md) para obter mais informações.

[!UICONTROL Detalhes de fidelidade] é um grupo de campos de esquema padrão para a [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md). O grupo de campos fornece um único campo de tipo de objeto, `loyalty`, que captura informações relacionadas à associação de uma pessoa em um programa de fidelidade do cliente.

![](../../images/field-groups/loyalty-details.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `pointsExpiration` | Matriz de objetos | Lista quaisquer pontos de fidelidade (ou grupos de pontos de fidelidade) que irão expirar e as datas em que expirarão. Cada item de matriz deve ser um objeto que contenha as duas propriedades a seguir: <ul><li>`pointsExpirationDate`: um datetime ISO 8601 de quando os pontos irão expirar.</li><li>`pointsExpiring`: o saldo de pontos expirando na data de expiração associada.</li></ul> |
| `joinDate` | DateTime | Uma data e hora ISO 8601 de quando a pessoa ingressou no programa de fidelidade. |
| `loyaltyID` | Matriz de cadeias de caracteres | Representa as IDs do programa de fidelidade associadas ao membro do programa de fidelidade. |
| `points` | Duplo | O saldo atual de pontos de fidelidade ou prêmios para o membro de fidelidade. |
| `pointsRedeemed` | Duplo | A quantidade de pontos que o membro de fidelidade aplicou em uma compra ou resgatou de outra forma. |
| `program` | String | O nome do programa de fidelidade no qual a pessoa está inscrita. |
| `status` | String | O status atual da associação de fidelidade da pessoa, como `active`, `disabled` ou `suspended`. |
| `tier` | String | Registra o nível do programa de fidelidade no qual a pessoa está inscrita. |
| `upgradeDate` | String | A data em que o membro de fidelidade foi atualizado para seu nível de camada mais recente. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o grupo de campos, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-loyalty-details.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-loyalty-details.schema.json)
