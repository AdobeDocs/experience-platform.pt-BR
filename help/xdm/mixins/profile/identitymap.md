---
keywords: Experience Platform, home, tópicos populares, esquema, esquema, XDM, perfil individual, campos, esquemas, esquemas, Esquemas, identityMap, mapa de identidade, mapa de identidade, design de esquema, mapa, mapa, mapa, esquema de união, união
solution: Experience Platform
title: Mistura do Mapa de identidade
topic-legacy: overview
description: Este documento fornece uma visão geral da classe Perfil individual XDM.
exl-id: c9928e85-ef1e-4739-ba1d-80505a9e60c3
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 0%

---

# [!UICONTROL IdentityMap] mistura

>[!NOTE]
>
>Os nomes de várias mixins mudaram. Consulte o documento em [mixin name updates](../name-updates.md) para obter mais informações.

[!UICONTROL IdentityMap] é uma mixin padrão para a  [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md) . O mixin fornece um único campo de mapa, que contém um conjunto de identidades de usuário chaveadas por namespace.

>[!WARNING]
>
>O campo `IdentityMap` é atualizado automaticamente pelo sistema conforme os dados de identidade são assimilados. Para utilizar corretamente este campo para [Real-time Customer Profile](../../../profile/home.md), não tente atualizar manualmente o conteúdo do campo em suas operações de dados.

<img src="../../images/mixins/identitymap.png" width="600" /><br />

Consulte a seção sobre mapas de identidade no [básico da composição do schema](../../schema/composition.md#identityMap) para obter mais informações sobre seu caso de uso.
