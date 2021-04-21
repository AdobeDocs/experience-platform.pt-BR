---
keywords: Experience Platform; home; tópicos populares; api; API; XDM; sistema XDM; modelo de dados de experiência; modelo de dados; ui; espaço de trabalho; relacionamento; campo;
solution: Experience Platform
title: Definir campos de relacionamento na interface do usuário
description: Saiba como definir um campo de relacionamento na interface do usuário do Experience Platform.
topic-legacy: user guide
exl-id: 8a6be545-0edb-4b9c-b164-e44a7a5f54f5
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---

# Definir campos de relacionamento na interface do usuário

No Experience Data Model (XDM), um [schema de união](../../schema/composition.md#union) é uma exibição unificada de todos os esquemas pertencentes à mesma classe que também foram habilitados para [Perfil do cliente em tempo real](../../../profile/home.md). O schema de união é aproveitado pelo Perfil para construir uma representação completa de um cliente a partir de dados de experiência diferentes.

Em alguns casos, você pode estar assimilando dados que não são necessariamente parte de um perfil, mas que ainda estão relacionados ao perfil. Um exemplo desse tipo de dados seria um campo de &quot;hotel favorito&quot; para um cliente. Como os atributos do hotel favorito de uma pessoa não são atributos da própria pessoa, um hotel é melhor representado por um schema separado baseado em uma classe personalizada em vez de [!DNL XDM Individual Profile].

Como os schemas de união são baseados apenas em schemas que compartilham a mesma classe, simplesmente habilitar o schema &quot;Hotéis&quot; para uso no Perfil não incluirá seu schema de união de campos para [!DNL XDM Individual Profile]. Em vez disso, você deve definir uma relação entre &quot;Hotéis&quot; e outro schema pertencente à união. Isso envolve definir um **campo de relacionamento** em um schema de origem que faz referência à identidade primária de um schema de destino.

Para obter etapas detalhadas sobre como definir uma relação entre dois schemas na interface do usuário do Adobe Experience Platform, consulte o [tutorial da interface do usuário de relacionamento](../../tutorials/relationship-ui.md).
