---
keywords: Experience Platform, home, tópicos populares, Adobe Experience Platform, guia do usuário, guia da interface do usuário, guia da interface da plataforma, introdução à plataforma, painel;
solution: Experience Platform
title: Visão geral da interface do usuário do Experience Platform
topic-legacy: ui guide
description: Adobe Experience Platform
exl-id: 47f9a3fb-731d-4ade-8069-faaa18f224dc
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1695'
ht-degree: 3%

---

# Guia da interface do usuário do Adobe Experience Platform

Este guia serve como uma introdução ao uso da interface do usuário do Adobe Experience Platform (UI), explicando para que os vários componentes são usados e fornecendo links para mais documentação para obter mais informações.

Para saber mais sobre o Adobe Experience Platform, leia a [Experience Platform overview](home.md).

## Tela inicial

Depois de fazer logon no Adobe Experience Platform, você está na página [!UICONTROL Home], que é composta pelas seções [painel de métricas](#metrics), [dados recentes](#recent-data) e [aprendizagem recomendada](#recommended-learning).

![](images/user-guide/homepage.png)

### Métricas

O painel de métricas fornece cartões que fornecem informações sobre conjuntos de dados, perfis, segmentos e destinos em sua organização.

![](images/user-guide/homepage-dashboard.png)

A seção **[!UICONTROL Datasets]** mostra o número de conjuntos de dados na organização IMS. Esse número é atualizado quando um novo conjunto de dados é criado. Mais informações sobre conjuntos de dados podem ser encontradas na [visão geral dos conjuntos de dados](../catalog/datasets/overview.md).

A seção **[!UICONTROL Profiles]** mostra o número total de pessoas com perfis em sua Organização IMS, excluindo fragmentos de perfil. Esse número total de pessoas representa o público-alvo total endereçável e é atualizado uma vez a cada 24 horas. Mais informações sobre perfis podem ser encontradas na [Visão geral do Perfil do cliente em tempo real](../profile/home.md).

A seção **[!UICONTROL Segments]** mostra o número total de segmentos criados na Organização IMS. Esse número é atualizado quando um novo segmento é criado. Mais informações sobre segmentos podem ser encontradas na [Visão geral do Serviço de segmentação](../segmentation/home.md).

A seção **[!UICONTROL Destinations]** mostra o número total de destinos criados para a Organização IMS. Esse número é atualizado quando um novo destino é criado. Mais informações sobre destinos podem ser encontradas na [visão geral de destinos](../destinations/home.md).

### Dados recentes

O painel de dados recente fornece informações sobre conjuntos de dados, fontes, segmentos e destinos criados recentemente.

![](images/user-guide/homepage-recent.png)

A seção **[!UICONTROL Recent datasets]** lista os cinco conjuntos de dados criados mais recentemente na organização IMS. Essa lista é atualizada sempre que um novo conjunto de dados é criado. Você pode selecionar um conjunto de dados na lista para exibir mais informações sobre o conjunto de dados especificado ou selecionar **[!UICONTROL View all]** para ver uma lista de todos os conjuntos de dados criados. Mais informações sobre conjuntos de dados podem ser encontradas na [visão geral dos conjuntos de dados](../catalog/datasets/overview.md).

A seção **[!UICONTROL Recent sources]** lista os cinco conectores de origem criados mais recentemente na organização IMS. Essa lista é atualizada sempre que um novo conector de origem é criado. Você pode selecionar uma conexão de origem na lista para exibir mais informações sobre o conector especificado ou selecionar **[!UICONTROL View all]** para ver uma lista de todas as conexões de origem criadas. Mais informações sobre fontes podem ser encontradas na [visão geral das fontes](../sources/home.md).

A seção **[!UICONTROL Recent segments]** lista as cinco definições de segmento criadas mais recentemente na Organização IMS. Essa lista é atualizada sempre que uma nova definição de segmento é criada. Você pode selecionar uma definição de segmento na lista para exibir mais informações sobre a definição de segmento especificada ou selecionar **[!UICONTROL View all]** para ver uma lista de todas as definições de segmento criadas. Mais informações sobre segmentos podem ser encontradas na [Visão geral do Serviço de segmentação](../segmentation/home.md).

A seção **[!UICONTROL Recent destinations]** lista os cinco destinos criados mais recentemente na organização IMS. Essa lista é atualizada sempre que um novo destino é criado. Você pode selecionar um destino na lista para exibir mais informações sobre o destino especificado ou selecionar **[!UICONTROL View all]** para ver uma lista de todos os destinos criados. Mais informações sobre destinos podem ser encontradas na [visão geral de destinos](../destinations/home.md).

### Aprendizagem recomendada

A seção **[!UICONTROL Recommended learning]** fornece links para a documentação útil para começar a usar o Adobe Experience Platform.

![](images/user-guide/homepage-recommended.png)

## Barra de navegação superior

A barra de navegação superior na interface do usuário da plataforma exibe a Organização IMS na qual você está conectado no momento e fornece vários controles importantes.

No lado esquerdo da barra de navegação, há o logotipo do Adobe Experience Platform. A seleção dessa opção a qualquer momento o retornará à tela inicial da interface do usuário da plataforma.

![](./images/user-guide/homepage-top-nav-bar.png)

### Seletor da Organização IMS

O primeiro item no lado direito da barra de navegação superior é o **IMS Organization switcher**.

![](./images/user-guide/homepage-ims-org.png)

Selecionar o alternador abre um menu suspenso de Organizações IMS às quais você tem acesso, se houver algum disponível. Selecione uma opção listada para mudar para essa Organização IMS.

![](./images/user-guide/homepage-ims-org-switcher.png)

### Aplicativos de switch

O próximo item no lado direito da navegação superior é o **application switcher**, representado pelo ícone ![application switcher](./images/user-guide/app-switcher-icon.png). Ao selecionar esse ícone, você pode alternar entre aplicativos do Adobe aos quais a sua Organização IMS tem acesso, como Experience Platform, Analytics, Assets e Launch.

### Ajuda

À direita do alternador de aplicativos, há o **menu de ajuda e suporte**, que é representado pelo ícone ![ponto de interrogação/ajuda](./images/user-guide/help-icon.png). Ao selecionar esse ícone, um menu pop-up é exibido, contendo vários recursos de ajuda e suporte. A guia **[!UICONTROL Help]** mostra uma lista de documentação relevante para a página em que você está no momento. A guia **[!UICONTROL Support]** permite criar um tíquete de suporte com a equipe de suporte do Adobe. A guia **[!UICONTROL Feedback]** permite enviar feedback sobre a Platform para o Adobe.

![](images/user-guide/homepage-help-clicked.png)

### Notificações e anúncios

Na seção **notifications**, que é representada pelo ícone ![bell/Notifications and Announces](images/user-guide/notification-icon.png). A guia **[!UICONTROL Notifications]** mostra informações importantes sobre o produto e outras atualizações relevantes, enquanto a guia **[!UICONTROL Announcements]** mostra informações sobre a manutenção do serviço.

### Perfil de usuário

O item final na barra de navegação superior é o **user settings**, que é representado pelo ícone ![user settings/User Profile](images/user-guide/profile-icon.png). Selecione esse ícone para editar suas preferências ou sair.

### Sandboxes

Imediatamente abaixo da barra de navegação superior está a barra de sandbox. Esta barra mostra qual sandbox você está usando atualmente para a plataforma. Mais informações sobre sandboxes podem ser encontradas na [sandboxes overview](../sandboxes/home.md).

## Navegação à esquerda {#left-nav}

A navegação no lado esquerdo da tela lista todos os diferentes serviços compatíveis com a interface do usuário da plataforma.

>[!IMPORTANT]
>
>Algumas das seções na barra de navegação esquerda podem não aparecer ou estar esmaecidas. Isso ocorre porque você não tem acesso a esses recursos. Se você acha que deve ter acesso a essas seções, entre em contato com o administrador do sistema.

![](images/user-guide/homepage-left.png)

A seção **[!UICONTROL Home]** permite retornar à página inicial da interface do usuário da plataforma.

A seção **[!UICONTROL Workflows]** mostra uma lista de fluxos de trabalho de várias etapas para executar operações no Platform. Mais informações sobre workflows podem ser encontradas na [visão geral dos workflows](./workflows.md).

### [!UICONTROL Connections]

A seção **[!UICONTROL Sources]** permite criar, atualizar e excluir conexões de origem, permitindo assimilar dados de fontes externas na Plataforma. Mais informações sobre fontes podem ser encontradas na [visão geral das fontes](../sources/home.md).

A seção **[!UICONTROL Destinations]** permite criar, atualizar e excluir destinos, permitindo exportar dados da Platform para muitos destinos externos. Mais informações sobre destinos podem ser encontradas na [visão geral de destinos](../destinations/home.md).

### [!UICONTROL Customer]

A seção **[!UICONTROL Profiles]** permite navegar pelos perfis do cliente, visualizar métricas de perfil, criar e gerenciar políticas de mesclagem e visualizar esquemas de união. Para saber mais sobre como usar a seção [!UICONTROL Profiles], leia o [[!DNL Profile] guia do usuário](../profile/ui/user-guide.md). Mais informações sobre o Perfil do cliente em tempo real podem ser encontradas na [Visão geral do perfil do cliente em tempo real](../profile/home.md).

A seção **[!UICONTROL Segments]** permite criar e gerenciar definições de segmento. Para saber mais sobre como usar a seção [!UICONTROL Segments], leia o [guia do usuário de segmentação](../segmentation/ui/overview.md). Mais informações sobre o Serviço de segmentação podem ser encontradas na [Visão geral do Serviço de segmentação](../segmentation/home.md).

A seção **[!UICONTROL Identities]** permite criar e gerenciar namespaces de identidade. Para obter mais informações sobre a seção [!UICONTROL Identities], incluindo informações sobre namespaces de identidade e como usar identidades na interface do usuário da plataforma, consulte a [visão geral do namespace de identidade](../identity-service/namespaces.md).

### [!UICONTROL Privacy]

A seção **[!UICONTROL Policies]** permite criar e gerenciar políticas de uso de dados. Para saber mais sobre como usar a seção Políticas , leia o [guia do usuário das políticas de uso de dados](../data-governance/policies/user-guide.md). Mais informações sobre as políticas de uso de dados podem ser encontradas na [visão geral das políticas de uso de dados](../data-governance/policies/overview.md).

A seção **[!UICONTROL Requests]** permite criar e gerenciar solicitações de privacidade. Observe que você deve ser incluir na lista de permissões para ter acesso à interface do usuário do Privacy Service. Para saber mais sobre como usar a seção Solicitações, leia o [guia do usuário do Privacy Service](../privacy-service/ui/user-guide.md). Mais informações sobre o Privacy Service podem ser encontradas na [Privacy Service overview](../privacy-service/home.md).

### [!UICONTROL Data Science]

A seção **[!UICONTROL Notebooks]** fornece acesso ao JupyterLab, um ambiente de desenvolvimento interativo que permite explorar, analisar e modelar seus dados. Para saber mais sobre como usar a seção Notebooks , leia o [Guia do usuário do JupyterLab](../data-science-workspace/jupyterlab/overview.md). Mais informações sobre o Data Science Workspace podem ser encontradas na [Visão geral do Data Science Workspace](../data-science-workspace/home.md)

A seção **[!UICONTROL Models]** permite que você aproveite o aprendizado de máquina e a inteligência artificial para criar, desenvolver, treinar e ajustar modelos para fazer previsões. Mais informações sobre a seção Modelos podem ser encontradas no tutorial em [treinamento e avaliar um modelo](../data-science-workspace/models-recipes/train-evaluate-model-ui.md).

A seção **[!UICONTROL Services]** permite gerenciar seus modelos publicados para pontuação de treinamento programado ou aproveitar os Serviços inteligentes Adobe, um conjunto de serviços de IA que fornecem experiências personalizadas em tempo real para os clientes. Mais informações sobre a seção Serviços podem ser encontradas no [Tutorial Publicação de um modelo como um serviço](../data-science-workspace/models-recipes/publish-model-service-ui.md).

### [!UICONTROL Data management]

A seção **[!UICONTROL Schemas]** permite criar e gerenciar esquemas do Experience Data Model (XDM). Para saber mais sobre schemas, leia o tutorial em [criar um schema](../xdm/tutorials/create-schema-ui.md). Mais informações sobre o XDM podem ser encontradas na [Visão geral do sistema XDM](../xdm/home.md).

A seção **[!UICONTROL Datasets]** permite criar e gerenciar conjuntos de dados. Mais informações sobre conjuntos de dados podem ser encontradas no [guia do usuário dos conjuntos de dados](../catalog/datasets/user-guide.md).

A seção **[!UICONTROL Queries]** permite criar e gerenciar consultas, registrar consultas SQL realizadas pelo Adobe Experience Platform Query Service e exibir suas credenciais PostgreSQL. Mais informações sobre consultas podem ser encontradas no [Guia do usuário do Serviço de Consulta](../query-service/ui/overview.md).

A seção **[!UICONTROL Monitoring]** permite monitorar a assimilação em lote e streaming. Mais informações sobre o monitoramento podem ser encontradas no [guia do usuário de assimilação de dados de monitoramento](../ingestion/quality/monitor-data-ingestion.md).

### [!UICONTROL Decisioning]

O Offer Decisioning é um serviço de aplicativos integrado à Adobe Experience Platform. Ele permite usar a Experience Platform para oferecer a melhor oferta e experiência aos clientes em todos os pontos de contato na hora certa. Para saber mais sobre o Offer Decisioning, incluindo trabalhar com [!UICONTROL Offers] e [!UICONTROL Activities], visite a [documentação do Offer Decisioning](https://experienceleague.adobe.com/docs/offer-decisioning.html).

### [!UICONTROL Administration]

A interface do usuário da Platform (UI) fornece um painel através do qual você pode visualizar informações importantes sobre o uso de licenças da organização, conforme capturado durante um instantâneo diário. Isso pode ser acessado selecionando **[!UICONTROL License usage]** na navegação. Para saber mais sobre o painel de uso da licença, visite o [guia do painel de uso da licença](license-usage-dashboard.md).

>[!IMPORTANT]
>
>A funcionalidade do painel de uso de licença está atualmente em alfa e não está disponível para todos os usuários. A documentação e a funcionalidade estão sujeitas a alterações.

## Próximas etapas

Ao ler este guia, você foi apresentado agora à página inicial e aos principais elementos de navegação da interface do usuário da plataforma. Para obter informações mais detalhadas sobre como trabalhar na interface do usuário, consulte a documentação de cada serviço individual da Platform. Os links para esta documentação são fornecidos na seção [navegação à esquerda](#left-nav) encontrada anteriormente neste documento.
