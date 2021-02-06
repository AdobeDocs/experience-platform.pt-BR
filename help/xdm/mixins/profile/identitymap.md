---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;perfil individual;campos;schemas;Schemas;identityMap;identity map;Identity map;Schema design;map;Map;união schema;união
solution: Experience Platform
title: Mixin do IdentityMap
topic: overview
description: Este documento fornece uma visão geral da classe de Perfil individual XDM.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---


# [!UICONTROL mixin ] IdentityMapin

>[!NOTE]
>
>Os nomes de várias misturas mudaram. Consulte o documento em [mixin name updates](../name-updates.md) para obter mais informações.

 IdentityMapis é uma combinação padrão para a  [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md). O mixin fornece um único campo de mapa, que contém um conjunto de identidades de usuário digitadas pela namespace.

>[!WARNING]
>
>O campo `IdentityMap` é atualizado automaticamente pelo sistema à medida que os dados de identidade são assimilados. Para utilizar adequadamente este campo para [Perfil do cliente em tempo real](../../../profile/home.md), não tente atualizar manualmente o conteúdo do campo em suas operações de dados.

<img src="../../images/mixins/identitymap.png" width="600" /><br />

Consulte a seção sobre mapas de identidade nos [fundamentos da composição do schema](../../schema/composition.md#identityMap) para obter mais informações sobre o caso de uso.