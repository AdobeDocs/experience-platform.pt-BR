---
keywords: Experience Platform;página inicial;tópicos populares;esquema;Esquema;XDM;perfil individual;campos;esquemas;Esquemas;identityMap;mapa de identidade;mapa de identidade;Design de esquema;mapa;Mapa;esquema de união;união
title: Grupo de campos de esquema do IdentityMap
description: Saiba mais sobre a classe Perfil individual XDM.
exl-id: c9928e85-ef1e-4739-ba1d-80505a9e60c3
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 0%

---

# Grupo de campos de esquema [!UICONTROL IdentityMap]

>[!NOTE]
>
>Os nomes de vários grupos de campos de esquema foram alterados. Consulte o documento em [atualizações de nome de grupo de campos](../name-updates.md) para obter mais informações.

[!UICONTROL IdentityMap] é um grupo de campos de esquema padrão para a [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md). O grupo de campos fornece um único campo de mapa, que contém um conjunto de identidades de usuário digitadas por namespace.

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
