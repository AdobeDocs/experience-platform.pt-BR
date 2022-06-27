---
keywords: visão geral das métricas; visão geral das métricas do rtcdp
title: Página inicial e painéis do Real-time Customer Data Platform
description: Painéis, Página inicial e experiência de usuário iniciante da Adobe Experience Platform
exl-id: ced5b69c-5bb5-4e06-9cb4-938e36e6e5cc
source-git-commit: ad0d38cbd249642d582a807c5679065827f57717
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 2%

---

# [!DNL Real-time Customer Data Platform] página inicial e painéis

A página inicial da Real-time Customer Data Platform (CDP em tempo real), que inclui um painel de métricas, é exibida ao fazer logon na CDP em tempo real.

A página inicial é apenas um dos locais onde os cartões de métrica são exibidos. A CDP em tempo real fornece cartões de métrica em toda a sua experiência. Essas métricas informam sobre os dados, o perfil e os públicos do segmento no sistema.

![imagem](assets/home.png)

Se não houver dados no sistema quando você fizer logon na CDP em tempo real, o painel na página inicial não será exibido. Nesse caso, a página inicial fornece material de aprendizagem para uma primeira experiência do usuário. Conforme os dados são coletados, em outras palavras, como <!--sources-->conjuntos de dados, perfis, segmentos e destinos são criados e fluxos de dados no sistema — o painel é atualizado automaticamente para exibir informações sobre esses dados<!-- in metric cards-->.

## Exibição do painel da página inicial

<!--The dashboard shows information in several areas. Each category of information displays for the time range shown beneath the data.-->

O painel é dividido em<!-- two areas.-->:

* **O Quadro de Liderança** fica na parte superior do painel. O painel de líderes mostra o número de conjuntos de dados, perfis, segmentos e destinos no sistema.

   ![imagem](assets/leaderboard.png)

<!-- * **Metric cards** display beneath the leaderboard. Metric cards show additional information, such as percentages or trends. Metric cards appear as data is collected.
    ![image](assets/home-metrics.jpg)
Some information is shown in different ways on both the leaderboard and metric cards. -->
* **Itens recentes** lista os cinco conjuntos de dados, fontes, segmentos e destinos mais recentes adicionados ao sistema.

   ![imagem](assets/recent.png)

Métricas adicionais, por exemplo, para perfis e segmentos, estão disponíveis em outras partes do Real-time Customer Data Platform.

### Conjuntos de dados

O **[!UICONTROL Conjuntos de dados]** O contador mostra o número de conjuntos de dados no sistema e a quantidade de dados em [!DNL Platform]. Esse contador é atualizado quando um conjunto de dados é criado.

Para obter mais informações sobre conjuntos de dados, consulte o [visão geral dos conjuntos de dados](../catalog/datasets/overview.md).

### Perfis

O **[!UICONTROL Perfis]** contagem mostra o número total de pessoas com perfis na [!DNL Real-time Customer Profile]. Ela não inclui fragmentos de perfil. Esse é seu público-alvo totalmente endereçável.

Essa contagem usa o padrão [política de mesclagem](profile/merge-policies.md) conforme definido na configuração da política de mesclagem no Perfil unificado.

O número de perfis é atualizado uma vez a cada 24 horas.

Para obter mais informações sobre perfis, consulte [Uma visão unificada do cliente na CDP em tempo real](profile/profile-overview.md).

### Segmentos

**[!UICONTROL Segmentos]** mostra o número total de segmentos criados para a organização. Esse número é atualizado quando novos segmentos são criados.

Para obter mais informações sobre segmentos, consulte [Visão geral do serviço de segmentação](segmentation/segmentation-overview.md).

### Destinos

**[!UICONTROL Destinos]** mostra o número total de destinos criados para a organização. Esse número é atualizado quando novos destinos são criados.

Para obter mais informações sobre destinos, consulte [Visão geral dos destinos](destinations/overview.md).

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

O **[!UICONTROL Conjuntos de dados recentes]** cartão mostra os cinco conjuntos de dados mais recentes criados na organização. Essa lista é atualizada quando um novo conjunto de dados é criado.

Selecione um conjunto de dados para ver os detalhes desse item, ou **[!UICONTROL Exibir tudo]** para ver a lista de conjuntos de dados. A partir daí, é possível selecionar uma fonte específica para obter detalhes.

Para obter mais informações sobre conjuntos de dados, consulte o [visão geral dos conjuntos de dados](../catalog/datasets/overview.md).

### Fontes recentes

O **[!UICONTROL Fontes recentes]** cartão de métrica mostra as cinco fontes mais recentes criadas na organização. Essa lista é atualizada quando uma nova fonte é criada.

Selecione uma fonte para exibir os detalhes desse item, ou **[!UICONTROL Exibir tudo]** para ver a lista de fontes. A partir daí, é possível selecionar uma fonte específica para obter detalhes.

Para obter mais informações sobre fontes, consulte [Visão geral das fontes](sources/sources-overview.md).

### Segmentos recentes

O **[!UICONTROL Segmentos recentes]** cartão de métrica mostra os cinco segmentos mais recentes criados na organização. Essa lista é atualizada quando um novo segmento é criado.

Selecione um segmento para ver os detalhes do item, ou **[!UICONTROL Exibir tudo]** para ver informações sobre mais segmentos.

Para obter mais informações sobre segmentos, consulte [Visão geral do serviço de segmentação](segmentation/segmentation-overview.md).

### Destinos recentes

O **[!UICONTROL Destinos recentes]** cartão de métrica mostra os cinco destinos mais recentes criados na organização. Essa lista é atualizada quando um novo destino é criado.

Selecione um destino para ver os detalhes para esse item, ou **[!UICONTROL Exibir tudo]** para ver informações sobre mais destinos.

Para obter mais informações sobre destinos, consulte [Visão geral dos destinos](destinations/overview.md).
