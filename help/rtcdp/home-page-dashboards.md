---
keywords: visão geral das métricas; visão geral das métricas Rtcdp
title: Home page e Painéis da plataforma de dados do cliente em tempo real
seo-title: Home page e Painéis da plataforma de dados do cliente em tempo real
description: Painéis, Página inicial e experiência de usuário iniciante da Adobe Experience Platform
seo-description: Painéis, Página inicial e experiência de usuário iniciante da Adobe Experience Platform
translation-type: tm+mt
source-git-commit: 00010d38a5d05800aeac9af8505093fee3593b45
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 4%

---


# [!DNL Real-time Customer Data Platform] visão geral das métricas

O home page Real-time Customer Data Platform (CDP em tempo real), que inclui um painel de métricas, é exibido quando você faz logon na CDP em tempo real.

O home page é apenas um dos locais onde os cartões de métrica aparecem. A CDP em tempo real fornece cartões de métricas em toda a sua experiência. Essas métricas informam sobre as audiências de dados, perfis e segmentos no sistema.

![imagem](assets/home.png)

Se não houver dados no sistema quando você fizer logon na CDP em tempo real, o painel no home page não será exibido. Nesse caso, o home page fornece material de aprendizado para uma primeira experiência do usuário. À medida que os dados são coletados — em outras palavras, à medida que <!--sources-->conjuntos de dados, perfis, segmentos e destinos são criados e os dados fluem para o sistema — o painel é atualizado automaticamente para exibir informações sobre esses dados<!-- in metric cards-->.

## Visualização painel home page

<!--The dashboard shows information in several areas. Each category of information displays for the time range shown beneath the data.-->

O painel é dividido em<!-- two areas.-->:

* **O** quadro de líderes fica na parte superior do painel. O quadro de líderes mostra o número de conjuntos de dados, perfis, segmentos e destinos no sistema.

   ![imagem](assets/leaderboard.png)

<!-- * **Metric cards** display beneath the leaderboard. Metric cards show additional information, such as percentages or trends. Metric cards appear as data is collected.
    ![image](assets/home-metrics.jpg)
Some information is shown in different ways on both the leaderboard and metric cards. -->
* **Os** itens recentes listam os cinco conjuntos de dados, fontes, segmentos e destinos mais recentes adicionados ao sistema.

   ![imagem](assets/recent.png)

Métricas adicionais — por exemplo, para perfis e segmentos — estão disponíveis em outras partes da Plataforma de dados do cliente em tempo real.

### Conjuntos de dados

O contador **[!UICONTROL Datasets]** mostra o número de conjuntos de dados no sistema e a quantidade de dados em [!DNL Platform]. Este contador é atualizado quando um conjunto de dados é criado.

Para obter mais informações sobre conjuntos de dados, consulte a [visão geral dos conjuntos de dados](../catalog/datasets/overview.md).

### Perfis

A contagem **[!UICONTROL Perfis]** mostra o número total de pessoas com perfis em [!DNL Real-time Customer Profile]. Ela não inclui fragmentos de perfil. Esta é a sua audiência totalmente endereçável.

Essa contagem usa a [política de mesclagem](profile/merge-policies.md) padrão, conforme definido na configuração da política de mesclagem no Perfil Unificado.

O número de perfis é atualizado uma vez a cada 24 horas.

Para obter mais informações sobre perfis, consulte [Uma visualização unificada do seu cliente em CDP em tempo real](profile/profile-overview.md).

### Segmentos

**[!UICONTROL Os]** segmentos mostram o número total de segmentos criados para a organização. Esse número é atualizado quando novos segmentos são criados.

Para obter mais informações sobre segmentos, consulte [Visão geral do Serviço de Segmentação](segmentation/segmentation-overview.md).

### Destinos

**** Destinos mostra o número total de destinos criados para a organização. Esse número é atualizado quando novos destinos são criados.

Para obter mais informações sobre destinos, consulte [Visão geral de destinos](destinations/overview.md).

<!-- ### Successful profile records

In the leaderboard **[!UICONTROL Successful profile records]** shows the total number of records that have been successfully processed into the profile.

There is also a metric card that shows the percentage of successful records. Select **[!UICONTROL View datasets]** to see more details about the profile records. Hover over the colored area of the graph to see additional details:

![image](assets/home-profilerecords-details.PNG)

The number of successful profile records is updated hourly. 

For more information about profiles, see [A unified view of your customer in Real-time CDP](profile/profile-overview.md).

### Total profile records

The **[!UICONTROL Total profile records]** metric card shows the total number of data records enabled to feed into the profiles, and the percentage that are successful, updated once per day. This does not include all data in the data lake, because some data might not be enabled to feed into the profiles.

 Hover over the colored area of the graph to see additional details about the successful profiles:

![image](assets/home-profile-details.PNG)

Select **[!UICONTROL View profiles]** to see more details about the profile records.

For more information about profiles, see [A unified view of your customer in Real-time CDP](profile/profile-overview.md).

For more information about viewing a specific profile, see [Profile viewer](profile/profile-viewer.md).

### Failed profile records

In the leaderboard, **[!UICONTROL Failed profile records]** counts the number of records that failed to process into the profile.

The **[!UICONTROL Failed profile records]** metric card shows this count, and includes a graphical representation that helps you see how failures have trended during the time shown below the graphic. This chart is updated hourly. Select **[!UICONTROL View datasets]** to see more details about the profile records.

The number of failed profile records is updated hourly. -->

### Conjuntos de dados recentes

O cartão **[!UICONTROL Conjuntos de dados recentes]** mostra os cinco conjuntos de dados mais recentes criados na organização. Esta lista é atualizada quando um novo conjunto de dados é criado.

Selecione um conjunto de dados para visualização dos detalhes desse item ou **[!UICONTROL Visualização all]** para ver a lista de conjuntos de dados. Daí, você pode selecionar uma fonte específica para obter detalhes.

Para obter mais informações sobre conjuntos de dados, consulte a [visão geral dos conjuntos de dados](../catalog/datasets/overview.md).

### Fontes recentes

O cartão de métrica **[!UICONTROL Fontes recentes]** mostra as cinco fontes mais recentes criadas na organização. Essa lista é atualizada quando uma nova fonte é criada.

Selecione uma fonte para visualização dos detalhes desse item ou **[!UICONTROL Visualização all]** para ver a lista das fontes. Daí, você pode selecionar uma fonte específica para obter detalhes.

Para obter mais informações sobre fontes, consulte [Visão geral das fontes](sources/sources-overview.md).

### Segmentos recentes

O cartão de métricas **[!UICONTROL Segmentos recentes]** mostra os cinco segmentos mais recentes criados na organização. Essa lista é atualizada quando um novo segmento é criado.

Selecione um segmento para visualização dos detalhes desse item ou **[!UICONTROL Visualização all]** para ver informações sobre mais segmentos.

Para obter mais informações sobre segmentos, consulte [Visão geral do Serviço de Segmentação](segmentation/segmentation-overview.md).

### Destinos recentes

O cartão de métricas **[!UICONTROL Destinos recentes]** mostra os cinco destinos mais recentes criados na organização. Essa lista é atualizada quando um novo destino é criado.

Selecione um destino para visualização dos detalhes desse item ou **[!UICONTROL Visualização all]** para ver informações sobre mais destinos.

Para obter mais informações sobre destinos, consulte [Visão geral de destinos](destinations/overview.md).
