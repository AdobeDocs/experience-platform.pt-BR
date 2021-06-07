---
keywords: Experience Platform, home, tópicos populares, esquema, esquema, XDM, perfil individual, campos, esquemas, esquemas, detalhes de fidelidade, design de esquema, grupo de campos, grupo de campos;
solution: Experience Platform
title: Grupo de Campos do Esquema Detalhes da Fidelidade
topic-legacy: overview
description: Este documento fornece uma visão geral do grupo de campos Detalhes da Fidelidade .
source-git-commit: fe49560a69c4c02835f00e4ebc0a5b9dc88eae90
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 3%

---


# [!UICONTROL Grupo de campos ] Detalhes da Fidelidade do schema

>[!NOTE]
>
>Os nomes de vários grupos de campos de esquema foram alterados. Consulte o documento em [atualizações do nome do grupo de campos](../name-updates.md) para obter mais informações.

[!UICONTROL Fidelidade ] Detalha um grupo de campos de esquema padrão para a  [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md). O grupo de campos fornece um único campo do tipo de objeto, `loyalty`, que captura informações relacionadas à associação de uma pessoa em um programa de fidelidade do cliente.

![](../../images/field-groups/loyalty-details.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `pointsExpiration` | Matriz de objetos | Lista quaisquer pontos de fidelidade (ou grupos de pontos de fidelidade) que irão expirar e as datas em que expirarão. Cada item de matriz deve ser um objeto que contenha as duas propriedades a seguir: <ul><li>`pointsExpirationDate`: Um datetime ISO 8601 de quando os pontos expirarão.</li><li>`pointsExpiring`: O saldo do ponto que expira a partir da data de expiração associada.</li></ul> |
| `joinDate` | DateTime | Um datetime ISO 8601 de quando a pessoa ingressou no programa de fidelidade. |
| `loyaltyID` | Matriz de cadeias de caracteres | Representa as IDs do programa de fidelidade associadas ao membro do programa de fidelidade. |
| `points` | Duplo | O saldo atual de pontos de fidelidade ou prêmios para o membro de fidelidade. |
| `pointsRedeemed` | Duplo | A quantidade de pontos que o membro do programa de fidelidade aplicou a uma compra ou resgatou de outra forma. |
| `program` | String | O nome do programa de fidelidade em que a pessoa está inscrita. |
| `status` | String | O status atual da associação de fidelidade da pessoa, como `active`, `disabled` ou `suspended`. |
| `tier` | String | Captura o nível do programa de fidelidade em que a pessoa está inscrita. |
| `upgradeDate` | String | A data em que o membro de fidelidade foi atualizado para seu nível de camada mais recente. |

{style=&quot;table-layout:auto&quot;}

Para obter mais detalhes sobre o grupo de campos, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-loyalty-details.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-loyalty-details.schema.json)
