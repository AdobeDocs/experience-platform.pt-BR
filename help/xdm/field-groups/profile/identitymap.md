---
keywords: Experience Platform;página inicial;tópicos populares;esquema;Esquema;XDM;perfil individual;campos;esquemas;Esquemas;identityMap;identity map;Identity map;Schema design;map;Map;union schema;union
title: Grupo de campos de esquema do IdentityMap
description: Saiba mais sobre a classe Perfil individual XDM.
exl-id: c9928e85-ef1e-4739-ba1d-80505a9e60c3
source-git-commit: cfa3e5c6811f148376a2d2012f5687be6fad2299
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---

# Grupo de campos de esquema [!UICONTROL IdentityMap]

>[!NOTE]
>
>Os nomes de vários grupos de campos de esquema foram alterados. Consulte o documento em [atualizações de nome de grupo de campos](../name-updates.md) para obter mais informações.

[!UICONTROL IdentityMap] é um grupo de campos de esquema padrão para a [[!UICONTROL classe XDM ExperienceEvent]](../../classes/experienceevent.md) e um grupo de campos compatível para a [[!UICONTROL classe XDM Individual Profile]](../../classes/individual-profile.md). O grupo de campos fornece um único campo de mapa, que contém um conjunto de identidades de usuário digitadas por namespace.

![Um diagrama do [!UICONTROL IdentityMap] grupo de campos de esquema](../../images/field-groups/identitymap.png)

Consulte a seção sobre mapas de identidade nas [noções básicas da composição de esquema](../../schema/composition.md#identityMap) para obter mais informações sobre o caso de uso, incluindo seus benefícios e desvantagens.

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

Para obter mais detalhes sobre o grupo de campos, consulte o [esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/identitymap.schema.json) no repositório XDM público.
