---
keywords: Experience Platform;home;popular topics;api;API;XDM;sistema XDM;experimentar modelo de dados;modelo de dados;ui;espaço de trabalho;relacionamento;campo;
solution: Experience Platform
title: Definir campos de relacionamento na interface do usuário
description: Saiba como definir um campo de relacionamento na interface do usuário do Experience Platform.
topic: user guide
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---


# Definir campos de relacionamento na interface do usuário

No Modelo de dados de experiência (XDM), um [schema](../../schema/composition.md#union) é uma visualização unificada de todos os schemas pertencentes à mesma classe que também foram habilitados para [Perfil do cliente em tempo real](../../../profile/home.md). O schema de união é aproveitado pelo Perfil para construir uma representação completa de um cliente a partir de dados de experiência diferentes.

Em alguns casos, você pode estar ingerindo dados que não são necessariamente parte de um perfil, mas que estão relacionados ao perfil. Um exemplo desse tipo de dados seria um campo de &quot;hotel favorito&quot; para um cliente. Como os atributos do hotel favorito de uma pessoa não são atributos da própria pessoa, um hotel é melhor representado por um schema separado com base em uma classe personalizada em vez de [!DNL XDM Individual Profile].

Como os schemas de união são baseados apenas em schemas que compartilham a mesma classe, simplesmente habilitar o schema &quot;Hotéis&quot; para uso no Perfil não incluirá seus campos schema união para [!DNL XDM Individual Profile]. Em vez disso, você deve definir uma relação entre &quot;Hotéis&quot; e outro schema que pertence à união. Isso envolve definir um **campo de relacionamento** em um schema de origem que faz referência à identidade primária de um schema de destino.

Para obter etapas detalhadas sobre como definir uma relação entre dois schemas na interface do usuário do Adobe Experience Platform, consulte o tutorial [relacionamento da interface do usuário](../../tutorials/relationship-ui.md).