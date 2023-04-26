---
keywords: visão geral das métricas; visão geral das métricas do rtcdp
title: Página inicial e painéis do Real-time Customer Data Platform
description: Painéis, Página inicial e experiência de usuário iniciante da Adobe Experience Platform
exl-id: ced5b69c-5bb5-4e06-9cb4-938e36e6e5cc
source-git-commit: 8ea657e379248616d3140bc0a7b0c25a918bc857
workflow-type: tm+mt
source-wordcount: '802'
ht-degree: 1%

---

# [!DNL Real-Time Customer Data Platform] página inicial

A página inicial do Adobe Real-time Customer Data Platform (Real-Time CDP) é a primeira página exibida após fazer logon no Real-Time CDP.

A página inicial do Real-Time CDP inclui um widget de introdução que permite acessar rapidamente vários recursos diferentes e uma seção de métricas que exibe informações atualizadas sobre dados em sua organização.

Este documento fornece uma visão geral da página inicial do Real-Time CDP e do painel de métricas.

![A página inicial da interface do usuário da plataforma.](assets/platform-home/home.png)

## Dispositivo de introdução

O [!UICONTROL Introdução ao perfil do cliente em tempo real] o widget é dividido em quatro seções:

* **Assimilar dados na plataforma**: Este widget direciona você ao catálogo de fontes. Use o catálogo de fontes para selecionar uma fonte e assimilar seus dados no Experience Platform. Para obter mais informações, leia a [visão geral das fontes](../sources/home.md)
* **Estruturas de dados do modelo**: Este widget direciona você à visão geral dos schemas. Use a visão geral dos esquemas para procurar esquemas existentes ou criar blocos de construção que descrevam a estrutura de seus dados. Para obter mais informações, leia a [visão geral dos schemas](../xdm/home.md).
* **Segmentar públicos**: Este widget direciona você ao [!DNL Segment Builder] na interface do usuário do . Use o [!DNL Segment Builder] para interagir com os elementos de dados do perfil e definir regras para seus segmentos. Para obter mais informações, leia a [Visão geral do serviço de segmentação](../segmentation/home.md).
* **Enviar dados para destinos**: Este widget direciona você ao catálogo de destinos. Use o catálogo de destinos para selecionar um destino ao qual você pode se conectar e enviar segmentos. Para obter mais informações, leia a [visão geral dos destinos](../destinations/home.md)

![A página inicial da interface do usuário da plataforma que exibe o widget de introdução](assets/platform-home/getting-started-widget.png)

## Painel de métricas

O painel de métricas exibe informações atualizadas sobre seus dados de Experience Platform. O painel é dividido em duas seções:

### O Quadro de Liderança

O Quadro de líderes mostra o número total atual de esquemas, conjuntos de dados, perfis e segmentos em sua organização, bem como a data de atualização mais recente.

![A seção do quadro de líderes na página inicial da interface do usuário da plataforma.](assets/platform-home/leaderboard.png)

* **Total de schemas**: O **Total de esquemas** O contador exibe o número de esquemas no sistema. Esse contador é atualizado quando um schema é criado. Para obter mais informações, leia a [visão geral dos schemas](../xdm/home.md).
* **Total de conjuntos de dados**: O **Total de conjuntos de dados** O contador mostra o número de conjuntos de dados no sistema e a quantidade de dados em [!DNL Platform]. Esse contador é atualizado quando um conjunto de dados é criado. Para obter mais informações sobre conjuntos de dados, leia a [visão geral dos conjuntos de dados](../catalog/datasets/overview.md).
* **Total de perfis**: O **Perfis** contagem mostra o número total de pessoas com perfis na [!DNL Real-Time Customer Profile]. Ela não inclui fragmentos de perfil. Esse é seu público-alvo totalmente endereçável. Essa contagem usa o padrão [política de mesclagem](profile/merge-policies.md) conforme definido na configuração da política de mesclagem no Perfil unificado. O número de perfis é atualizado uma vez a cada 24 horas. Para obter mais informações sobre perfis, leia a [Visão geral do perfil do cliente em tempo real](../profile/home.md).
* **Total de segmentos**: **Segmentos** mostra o número total de segmentos criados para a organização. Esse número é atualizado quando novos segmentos são criados. Para obter mais informações sobre segmentos, leia a [Visão geral do serviço de segmentação](../segmentation/home.md).

### Itens recentes

Os itens recentes listam as alterações mais recentes em sua organização. No exemplo abaixo, as alterações mais recentes pertencem a conjuntos de dados, fontes, segmentos e destinos.

![A seção de itens recentes na página inicial da interface do usuário da plataforma.](assets/platform-home/recent-items.png)

* **Conjuntos de dados recentes**: O **[!UICONTROL Conjuntos de dados recentes]** cartão mostra os cinco conjuntos de dados mais recentes criados na organização. Essa lista é atualizada quando um novo conjunto de dados é criado. Selecione um conjunto de dados para ver os detalhes para esse item ou selecione **[!UICONTROL Exibir tudo]** para obter uma lista de conjuntos de dados. A partir daí, é possível selecionar uma fonte específica para obter detalhes. Para obter mais informações sobre conjuntos de dados, consulte o [visão geral dos conjuntos de dados](../catalog/datasets/overview.md).
* **Fontes recentes**: O **[!UICONTROL Fontes recentes]** cartão de métrica mostra as cinco fontes mais recentes criadas na organização. Essa lista é atualizada quando uma nova fonte é criada. Selecione uma fonte para exibir os detalhes do item ou selecione **[!UICONTROL Exibir tudo]** para obter uma lista de fontes. A partir daí, é possível selecionar uma fonte específica para obter detalhes. Para obter mais informações sobre fontes, consulte [Visão geral das fontes](../sources/home.md).
* **Segmentos recentes**: O **[!UICONTROL Segmentos recentes]** cartão de métrica mostra os cinco segmentos mais recentes criados na organização. Essa lista é atualizada quando um novo segmento é criado. Selecione um segmento para ver os detalhes do item ou selecione **[!UICONTROL Exibir tudo]** para obter uma lista de segmentos. Para obter mais informações sobre segmentos, consulte [Visão geral do serviço de segmentação](../segmentation/home.md).
* **Destinos recentes**: O **[!UICONTROL Destinos recentes]** cartão de métrica mostra os cinco destinos mais recentes criados na organização. Essa lista é atualizada quando um novo destino é criado. Selecione um destino para ver os detalhes do item ou selecione **[!UICONTROL Exibir tudo]** para obter uma lista de destinos. Para obter mais informações, leia a [visão geral dos destinos](../destinations/home.md).

## Recursos

Por fim, o widget de recursos fornece recursos de documentação adicionais que você pode consultar. As melhorias incluem:

![A seção recursos na página inicial da interface do usuário da plataforma.](assets/platform-home/resources.png)

* [Noções básicas sobre schemas](../xdm/schema/composition.md)
* [Conectando fontes](../sources/home.md)
* [Como preencher o perfil do cliente em tempo real](../profile/home.md)
* [Conexão de destinos](../destinations/home.md)
* [Gerenciar acesso](../access-control/abac/overview.md)

<!-- ### Successful profile records

In the leaderboard **[!UICONTROL Successful profile records]** shows the total number of records that have been successfully processed into the profile.

There is also a metric card that shows the percentage of successful records. Select **[!UICONTROL View datasets]** to see more details about the profile records. Hover over the colored area of the graph to see additional details:

![image](assets/home-profilerecords-details.PNG)

The number of successful profile records is updated hourly. 

For more information about profiles, see [A unified view of your customer in Real-Time CDP](profile/profile-overview.md).

### Total profile records

The **[!UICONTROL Total profile records]** metric card shows the total number of data records enabled to feed into the profiles, and the percentage that are successful, updated once per day. This does not include all data in the data lake, because some data might not be enabled to feed into the profiles.

 Hover over the colored area of the graph to see additional details about the successful profiles:

![image](assets/home-profile-details.PNG)

Select **[!UICONTROL View profiles]** to see more details about the profile records.

For more information about profiles, see [A unified view of your customer in Real-Time CDP](profile/profile-overview.md).

For more information about viewing a specific profile, see [Profile viewer](profile/profile-viewer.md).

### Failed profile records

In the leaderboard, **[!UICONTROL Failed profile records]** counts the number of records that failed to process into the profile.

The **[!UICONTROL Failed profile records]** metric card shows this count, and includes a graphical representation that helps you see how failures have trended during the time shown below the graphic. This chart is updated hourly. Select **[!UICONTROL View datasets]** to see more details about the profile records.

The number of failed profile records is updated hourly. -->
