---
keywords: visão geral de métricas; visão geral de métricas do rtcdp
title: Página inicial e painéis do Real-time Customer Data Platform
description: Entenda vários painéis, a página inicial e a experiência de usuários iniciantes na Adobe Real-Time CDP.
feature: Dashboards, Get Started
exl-id: ced5b69c-5bb5-4e06-9cb4-938e36e6e5cc
source-git-commit: 2704184446f7945c744e7e2d2a8c3cda3fc12527
workflow-type: tm+mt
source-wordcount: '919'
ht-degree: 6%

---

# [!DNL Real-Time Customer Data Platform] home page

A página inicial do Adobe Real-time Customer Data Platform (Real-Time CDP) é a primeira página exibida após o logon no Real-Time CDP.

A página inicial do Real-Time CDP inclui um widget de introdução que permite acessar rapidamente vários recursos diferentes e uma seção de métricas que exibe informações atualizadas sobre os dados na organização.

Este documento fornece uma visão geral da página inicial da Real-Time CDP e do painel de métricas.

![A página inicial da Interface do usuário da plataforma.](assets/platform-home/home.png)

## Widget de introdução

A variável [!UICONTROL Introdução ao Perfil de cliente em tempo real] O widget está dividido em quatro seções:

* **Assimilar dados na plataforma**: este widget direciona você para o catálogo de códigos-fonte. Use o catálogo de fontes para selecionar uma fonte e assimilar seus dados no Experience Platform. Selecionar **[Configurar fontes]** para navegar até o catálogo de origens. Para obter mais informações, leia a [visão geral das origens](../sources/home.md).
* **Estruturas de dados do modelo**: este widget direciona você para a visão geral dos esquemas. Use a visão geral de esquemas para procurar esquemas existentes ou criar um blueprint que descreva a estrutura de seus dados. Selecionar **[!UICONTROL Criar esquema]** para navegar até a interface de criação do esquema. Para obter mais informações, leia a [visão geral de esquemas](../xdm/home.md).
* **Criar públicos-alvo**: esse widget direciona você para o Construtor de segmentos na interface do usuário. Use o Construtor de segmentos para interagir com elementos de dados do Perfil e definir os critérios para a definição do segmento. Selecionar **[!UICONTROL Criar público]** para navegar até o Construtor de segmentos. Para obter mais informações, leia a [Visão geral do serviço de segmentação](../segmentation/home.md).
* **Enviar dados para destinos**: esse widget direciona você para o catálogo de destinos. Use o catálogo de destinos para selecionar um destino ao qual você possa se conectar e enviar públicos-alvo. Selecionar **[!UICONTROL Configurar destinos]** para navegar até o catálogo de destinos. Para obter mais informações, leia a [visão geral dos destinos](../destinations/home.md).

![A página inicial da Interface do usuário do Platform que exibe o widget de introdução](assets/platform-home/getting-started-widget.png)

## Painel de métricas {#metrics-dashboard}

>[!CONTEXTUALHELP]
>id="platform_home_metrics_totalProfiles"
>title="Contagem total de perfis"
>abstract="O número total de perfis que a organização possui na Experience Platform. Essa contagem se baseia na política de mesclagem da organização e não inclui fragmentos de perfil. O número de perfis é atualizado a cada 24 horas."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/ui/user-guide.html?lang=pt-BR#profile-count" text="Saiba mais na documentação"

O painel de métricas exibe informações atualizadas sobre seus dados de Experience Platform. O painel é dividido em duas seções:

### O quadro de classificação

O quadro de classificação mostra o número total atual de esquemas, conjuntos de dados, perfis e públicos-alvo na organização, bem como a data de atualização mais recente.

![A seção de quadro de classificação na página inicial da interface do usuário da plataforma.](assets/platform-home/leaderboard.png)

* **Total de esquemas**: A variável **Total de esquemas** O contador exibe o número de schemas no sistema. Esse contador é atualizado quando um esquema é criado. Para obter mais informações, leia a [visão geral de esquemas](../xdm/home.md).
* **Total de conjuntos de dados**: A variável **Total de conjuntos de dados** o contador mostra o número de conjuntos de dados no sistema e a quantidade de dados no Experience Platform. Esse contador é atualizado quando um conjunto de dados é criado. Para obter mais informações sobre conjuntos de dados, leia a [visão geral dos conjuntos de dados](../catalog/datasets/overview.md).
* **Total de perfis**: A variável **Perfis** contagem mostra o número total de perfis que sua organização tem no Experience Platform. Ela não inclui fragmentos de perfil. Este é o seu público endereçável total. Essa contagem usa o padrão [política de mesclagem](profile/merge-policies.md) conforme definido na configuração da política de mesclagem no Perfil do cliente em tempo real. O número de perfis é atualizado uma vez a cada 24 horas. Selecionar **[!UICONTROL Perfis]** para navegar até a página Visão geral de perfis e visualizar todas as suas Métricas de perfil. Para obter mais informações sobre perfis, leia a [Visão geral do Perfil do cliente em tempo real](../profile/home.md).
* **Total de públicos**: A variável **Total de públicos** contador mostra o número total de públicos-alvo criados para sua organização. Esse número é atualizado quando novos públicos-alvo são criados. Para obter mais informações sobre públicos-alvo, leia a [Visão geral do serviço de segmentação](../segmentation/home.md).

### Itens recentes

Itens recentes lista as alterações mais recentes em sua organização. No exemplo abaixo, as alterações mais recentes pertencem a conjuntos de dados, fontes, públicos-alvo e destinos.

![A seção de itens recentes na página inicial da interface do usuário da plataforma.](assets/platform-home/recent-items.png)

* **Conjuntos de dados recentes**: A variável **[!UICONTROL Conjuntos de dados recentes]** mostra os cinco conjuntos de dados mais recentes criados na organização. Essa lista é atualizada quando um novo conjunto de dados é criado. Selecione um conjunto de dados para exibir os detalhes desse item ou selecione **[!UICONTROL Exibir todos]** para obter uma lista de conjuntos de dados. A partir daí, você pode selecionar uma origem específica para obter detalhes. Para obter mais informações sobre conjuntos de dados, consulte a [visão geral dos conjuntos de dados](../catalog/datasets/overview.md).
* **Origens recentes**: A variável **[!UICONTROL Origens recentes]** o cartão de métrica mostra as cinco fontes mais recentes criadas na organização. Essa lista é atualizada quando uma nova origem é criada. Selecione uma origem para exibir os detalhes desse item ou selecione **[!UICONTROL Exibir todos]** para obter uma lista de fontes. A partir daí, você pode selecionar uma origem específica para obter detalhes. Para obter mais informações sobre origens, consulte [Visão geral das fontes](../sources/home.md).
* **Públicos recentes**: A variável **[!UICONTROL Públicos recentes]** o cartão de métrica mostra os cinco públicos-alvo mais recentes criados na organização. Essa lista é atualizada quando um novo público-alvo é criado. Selecione um público-alvo para exibir os detalhes desse item ou selecione **[!UICONTROL Exibir todos]** para obter uma lista de públicos-alvo. Para obter mais informações sobre públicos-alvo, consulte [Visão geral do serviço de segmentação](../segmentation/home.md).
* **Destinos recentes**: A variável **[!UICONTROL Destinos recentes]** o cartão de métrica mostra os cinco destinos mais recentes criados na organização. Essa lista é atualizada quando um novo destino é criado. Selecione um destino para exibir os detalhes desse item ou selecione **[!UICONTROL Exibir todos]** para obter uma lista de destinos. Para obter mais informações, leia a [visão geral dos destinos](../destinations/home.md).

## Recursos

Por fim, o widget recursos fornece recursos adicionais de documentação que você pode consultar. As melhorias incluem:

![A seção de recursos na página inicial da interface do usuário da plataforma.](assets/platform-home/resources.png)

* [Noções básicas sobre esquemas](../xdm/schema/composition.md)
* [Conectando fontes](../sources/home.md)
* [Como preencher seu Perfil de cliente em tempo real](../profile/home.md)
* [Conectar destinos](../destinations/home.md)
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
