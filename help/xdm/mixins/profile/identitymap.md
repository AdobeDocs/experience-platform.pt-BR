---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;individual profile;fields;schemas;Schemas;identityMap;identity map;Identity map;Schema design;map;Map;union schema;union
solution: Experience Platform
title: Mistura IdentityMap
topic: overview
description: Este documento fornece uma visão geral da classe de Perfil individual XDM.
translation-type: tm+mt
source-git-commit: f9d8021643e72e3fbb5315b54a19815dcdaaa702
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---


# [!UICONTROL Mistura IdentityMap]

>[!NOTE]
>
>Os nomes de várias misturas mudaram. Consulte o documento sobre atualizações [de nome de](../name-updates.md) mixin para obter mais informações.

[!UICONTROL O IdentityMap] é uma combinação padrão para a [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md). O mixin fornece um único campo de mapa, que contém um conjunto de identidades de usuário digitadas pela namespace.

>[!WARNING]
>
>O `IdentityMap` campo é atualizado automaticamente pelo sistema à medida que os dados de identidade são assimilados. Para utilizar corretamente este campo para o Perfil [Cliente em tempo](../../../profile/home.md)real, não tente atualizar manualmente o conteúdo do campo em suas operações de dados.

<img src="../../images/mixins/identitymap.png" width="600" /><br />

Consulte a seção sobre mapas de identidade nos [fundamentos da composição](../../schema/composition.md#identityMap) do schema para obter mais informações sobre o caso de uso.