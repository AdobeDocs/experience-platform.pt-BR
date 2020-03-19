---
title: Página inicial da plataforma de dados do cliente em tempo real e painéis
seo-title: Página inicial da plataforma de dados do cliente em tempo real e painéis
description: Painéis, Página inicial e Experiência do usuário iniciante da Adobe Experience Platform
seo-description: Painéis, Página inicial e Experiência do usuário iniciante da Adobe Experience Platform
translation-type: tm+mt
source-git-commit: 6c8d0757d7e7568b1976823d9c52221374e67cbb

---


# Visão geral das métricas da Plataforma de dados do cliente em tempo real

A página inicial da Plataforma de dados do cliente em tempo real (CDP em tempo real) da Adobe, que inclui um painel de métricas, é exibida quando você faz logon na CDP em tempo real.

A página inicial é apenas um dos locais onde os cartões de métricas são exibidos. A CDP em tempo real fornece cartões de métricas em toda a sua experiência. Essas métricas informam sobre os dados, o perfil e os públicos do segmento no sistema.

![image](assets/home2.jpg)

Se não houver dados no sistema quando você fizer logon na CDP em tempo real, o painel na página inicial não será exibido. Nesse caso, a página inicial fornece material de aprendizado para uma primeira experiência do usuário. À medida que os dados são coletados — em outras palavras, à medida que <!--sources-->os conjuntos de dados, perfis, segmentos e destinos são criados e os dados fluem para o sistema — o painel é atualizado automaticamente para exibir informações sobre esses dados<!-- in metric cards-->.

## Exibição do painel da página inicial

<!--The dashboard shows information in several areas. Each category of information displays for the time range shown beneath the data.-->

O painel é dividido em<!-- two areas.-->:

* **O quadro de líderes** fica na parte superior do painel. O quadro de líderes mostra o número de conjuntos de dados, perfis, segmentos e destinos no sistema.

   ![image](assets/home-leaderboard2.jpg)

<!-- * **Metric cards** display beneath the leaderboard. Metric cards show additional information, such as percentages or trends. Metric cards appear as data is collected.
    ![image](assets/home-metrics.jpg)
Some information is shown in different ways on both the leaderboard and metric cards. -->
* **Itens** recentes listam os cinco conjuntos de dados, fontes, segmentos e destinos mais recentes adicionados ao sistema.

   ![image](assets/home-recent.jpg)

Métricas adicionais — por exemplo, para perfis e segmentos — estão disponíveis em outras partes da Plataforma de dados do cliente em tempo real.

### Conjuntos de dados

O contador **[!UICONTROL de conjuntos]** de dados mostra o número de conjuntos de dados no sistema e a quantidade de dados na Plataforma. Este contador é atualizado quando um conjunto de dados é criado.

Para obter mais informações sobre conjuntos de dados, consulte [Ingressar dados na Adobe Experience Platform](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html#!api-specification/markdown/narrative/tutorials/data_ingestion_tutorial/data_ingestion_tutorial.md).

### Perfis

A contagem de **[!UICONTROL Perfis]** mostra o número total de pessoas com perfis no Perfil do cliente em tempo real. Não inclui fragmentos de perfil. Este é o seu público-alvo totalmente endereçável.

Essa contagem usa a política [de](profile/merge-policies.md) mesclagem padrão definida na configuração da política de mesclagem no Perfil Unificado.

O número de perfis é atualizado uma vez a cada 24 horas.

Para obter mais informações sobre perfis, consulte [Uma visão unificada do cliente em CDP](profile/profile-overview.md)em tempo real.

### Segmentos

**[!UICONTROL Segmentos]** mostra o número total de segmentos criados para a organização. Esse número é atualizado quando novos segmentos são criados.

Para obter mais informações sobre segmentos, consulte Visão geral [do Serviço de](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/segmentation/segmentation-overview.md)segmentação.

### Destinos

**[!UICONTROL Destinos]** mostra o número total de destinos criados para a organização. Esse número é atualizado quando novos destinos são criados.

Para obter mais informações sobre destinos, consulte Visão geral [sobre](destinations/destinations-overview.md)Destinos.

<!-- ### Successful profile records

In the leaderboard **[!UICONTROL Successful profile records]** shows the total number of records that have been successfully processed into the profile.

There is also a metric card that shows the percentage of successful records. Click **[!UICONTROL View datasets]** to see more details about the profile records. Hover over the colored area of the graph to see additional details:

![image](assets/home-profilerecords-details.PNG)

The number of successful profile records is updated hourly. 

For more information about profiles, see [A unified view of your customer in Real-time CDP](profile/profile-overview.md).

### Total profile records

The **[!UICONTROL Total profile records]** metric card shows the total number of data records enabled to feed into the profiles, and the percentage that are successful, updated once per day. This does not include all data in the data lake, because some data might not be enabled to feed into the profiles.

 Hover over the colored area of the graph to see additional details about the successful profiles:

![image](assets/home-profile-details.PNG)

Click **[!UICONTROL View profiles]** to see more details about the profile records.

For more information about profiles, see [A unified view of your customer in Real-time CDP](profile/profile-overview.md).

For more information about viewing a specific profile, see [Profile viewer](profile/profile-viewer.md).

### Failed profile records

In the leaderboard, **[!UICONTROL Failed profile records]** counts the number of records that failed to process into the profile.

The **[!UICONTROL Failed profile records]** metric card shows this count, and includes a graphical representation that helps you see how failures have trended during the time shown below the graphic. This chart is updated hourly. Click **[!UICONTROL View datasets]** to see more details about the profile records.

The number of failed profile records is updated hourly. -->

### Conjuntos de dados recentes

O cartão de conjuntos de dados **** recentes mostra os cinco conjuntos de dados mais recentes criados na organização. Essa lista é atualizada quando um novo conjunto de dados é criado.

Clique em um conjunto de dados para exibir os detalhes desse item ou **[!UICONTROL Visualize todos]** para ver a lista de conjuntos de dados. Daí, você pode clicar em uma fonte específica para obter detalhes.

Para obter mais informações sobre conjuntos de dados, consulte [Ingressar dados na Adobe Experience Platform](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html#!api-specification/markdown/narrative/tutorials/data_ingestion_tutorial/data_ingestion_tutorial.md).

### Fontes recentes

O cartão de métricas de fontes **** recentes mostra as cinco fontes mais recentes criadas na organização. Essa lista é atualizada quando uma nova fonte é criada.

Clique em uma fonte para exibir os detalhes desse item ou **[!UICONTROL Visualize tudo]** para ver a lista de fontes. Daí, você pode clicar em uma fonte específica para obter detalhes.

Para obter mais informações sobre fontes, consulte Visão geral [das](sources/sources-overview.md)fontes.

### Segmentos recentes

O cartão de métricas de segmentos **** recentes mostra os cinco segmentos mais recentes criados na organização. Essa lista é atualizada quando um novo segmento é criado.

Clique em um segmento para exibir os detalhes desse item ou **[!UICONTROL Visualize todos]** para ver informações sobre mais segmentos.

Para obter mais informações sobre segmentos, consulte Visão geral [do Serviço de](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/segmentation/segmentation-overview.md)segmentação.

### Destinos recentes

O cartão de métricas de destinos **** recentes mostra os cinco destinos mais recentes criados na organização. Essa lista é atualizada quando um novo destino é criado.

Clique em um destino para exibir os detalhes desse item ou **[!UICONTROL Visualize todos]** para ver informações sobre mais destinos.

Para obter mais informações sobre destinos, consulte Visão geral [sobre](destinations/destinations-overview.md)Destinos.
