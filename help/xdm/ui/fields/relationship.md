---
keywords: Experience Platform;página inicial;tópicos populares;api;API;XDM;sistema XDM;modelo de dados de experiência;modelo de dados;interface;espaço de trabalho;relacionamento;campo;
solution: Experience Platform
title: Definir campos de relacionamento na interface
description: Saiba como definir um campo de relacionamento na interface do usuário do Experience Platform.
exl-id: 8a6be545-0edb-4b9c-b164-e44a7a5f54f5
source-git-commit: 7021725e011a1e1d95195c6c7318ecb5afe05ac6
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---

# Definir campos de relacionamento na interface

No Experience Data Model (XDM), um [esquema de união](../../schema/composition.md#union) é uma exibição unificada de todos os esquemas pertencentes à mesma classe que também foram habilitados para o [Perfil de cliente em tempo real](../../../profile/home.md). O esquema de união é aproveitado pelo Perfil para construir uma representação completa de um cliente a partir de dados de experiência diferentes.

Em alguns casos, você pode estar assimilando dados que não são necessariamente parte de um perfil, mas ainda assim estão relacionados ao perfil. Um exemplo desse tipo de dado seria um campo de &quot;hotel favorito&quot; para um cliente. Como os atributos do hotel favorito de uma pessoa não são atributos da própria pessoa, um hotel é melhor representado por um esquema separado baseado em uma classe personalizada em vez de [!DNL XDM Individual Profile].

Como os esquemas de união são baseados apenas em esquemas que compartilham a mesma classe, simplesmente habilitar o esquema &quot;Hotéis&quot; para uso em Perfil não incluirá seu esquema de união de campos para [!DNL XDM Individual Profile]. Em vez disso, você deve definir uma relação entre &quot;Hotels&quot; e outro schema pertencente ao sindicato. Isso envolve a definição de um **campo de relacionamento** em um esquema de origem que faz referência à identidade primária de um esquema de referência.

Para obter etapas detalhadas sobre como definir uma relação entre dois esquemas na interface do usuário do Adobe Experience Platform, consulte o [tutorial sobre interface do usuário de relacionamento](../../tutorials/relationship-ui.md).
