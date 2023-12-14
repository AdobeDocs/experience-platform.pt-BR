---
keywords: Experience Platform;página inicial;tópicos populares;esquema;Esquema;XDM;perfil individual;campos;esquemas;Esquemas;identityMap;mapa de identidade;mapa de identidade;Design de esquema;mapa;Mapa;esquema de união;união
title: Grupo de campos de esquema do IdentityMap
description: Este documento fornece uma visão geral da classe Perfil individual XDM.
exl-id: c9928e85-ef1e-4739-ba1d-80505a9e60c3
source-git-commit: 43b3b79a4d24fd92c7afbf9ca9c83b0cbf80e2c2
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---

# [!UICONTROL IdentityMap] grupo de campos de esquema

>[!NOTE]
>
>Os nomes de vários grupos de campos de esquema foram alterados. Consulte o documento sobre [atualizações do nome do grupo de campos](../name-updates.md) para obter mais informações.

[!UICONTROL IdentityMap] é um grupo de campos de esquema padrão para o [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md). O grupo de campos fornece um único campo de mapa, que contém um conjunto de identidades de usuário digitadas por namespace.

![Um diagrama do [!UICONTROL IdentityMap] grupo de campos de esquema](../../images/field-groups/identitymap.png)

Consulte a seção sobre mapas de identidade na [noções básicas da composição do esquema](../../schema/composition.md#identityMap) para obter mais informações sobre o caso de uso, incluindo benefícios e desvantagens.

**exemplo**

```JSON
{
    "identityMap":{
        "ECID":[
            {
                "id":"83238819066235616291057085344313877718",
                "authenticatedState":"ambiguous",
                "primary":true
            }
        ]
    }
}
```

Para obter mais informações sobre o grupo de campos, consulte o [esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/identitymap.schema.json) no repositório XDM público.
