---
keywords: Experience Platform;página inicial;tópicos populares;Adobe Experience Platform;guia do usuário;guia da interface do usuário;guia da interface do usuário da plataforma;introdução à plataforma;painel;
solution: Experience Platform
title: Visão geral da interface do Experience Platform
description: Adobe Experience Platform
exl-id: 47f9a3fb-731d-4ade-8069-faaa18f224dc
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1795'
ht-degree: 1%

---

# Guia da interface do usuário do Adobe Experience Platform

Este guia serve como uma introdução ao uso da interface do usuário (UI) do Adobe Experience Platform, explicando para que os vários componentes são usados e fornecendo links para mais informações.

Para saber mais sobre o Adobe Experience Platform, leia a [visão geral do Experience Platform](home.md).

## Tela inicial

Depois de fazer logon no Adobe Experience Platform, você estará na página [!UICONTROL Página inicial], que é composta pelas seções [painel de métricas](#metrics), [dados recentes](#recent-data) e [aprendizado recomendado](#recommended-learning).

![](images/user-guide/homepage.png)

### Métricas

O painel de métricas fornece cartões que fornecem informações sobre conjuntos de dados, perfis, segmentos e destinos em sua organização.

![](images/user-guide/homepage-dashboard.png)

A seção **[!UICONTROL Conjuntos de Dados]** mostra o número de conjuntos de dados na organização. Esse número é atualizado quando um novo conjunto de dados é criado. Mais informações sobre conjuntos de dados podem ser encontradas na [visão geral sobre conjuntos de dados](../catalog/datasets/overview.md).

A seção **[!UICONTROL Perfis]** mostra o número total de pessoas com perfis em sua organização, excluindo fragmentos de perfil. Esse número total de pessoas representa o público-alvo endereçável total e é atualizado uma vez a cada 24 horas. Mais informações sobre perfis podem ser encontradas na [Visão geral do Perfil do cliente em tempo real](../profile/home.md).

A seção **[!UICONTROL Segmentos]** mostra o número total de segmentos criados em sua organização. Esse número é atualizado quando um novo segmento é criado. Mais informações sobre segmentos podem ser encontradas na [Visão geral do Serviço de segmentação](../segmentation/home.md).

A seção **[!UICONTROL Destinos]** mostra o número total de destinos criados para a organização. Esse número é atualizado quando um novo destino é criado. Mais informações sobre destinos podem ser encontradas na [visão geral sobre destinos](../destinations/home.md).

### Dados recentes

O painel de dados recentes fornece informações sobre conjuntos de dados, fontes, segmentos e destinos criados recentemente.

![](images/user-guide/homepage-recent.png)

A seção **[!UICONTROL Conjuntos de dados recentes]** lista os cinco conjuntos de dados criados mais recentemente na organização. Essa lista é atualizada sempre que um novo conjunto de dados é criado. Você pode selecionar um conjunto de dados na lista para exibir mais informações sobre o conjunto de dados especificado ou selecionar **[!UICONTROL Exibir todos]** para ver uma lista de todos os conjuntos de dados criados. Mais informações sobre conjuntos de dados podem ser encontradas na [visão geral sobre conjuntos de dados](../catalog/datasets/overview.md).

A seção **[!UICONTROL Fontes recentes]** lista os cinco conectores de origem criados mais recentemente na organização. Essa lista é atualizada sempre que um novo conector de origem é criado. Você pode selecionar uma conexão de origem na lista para exibir mais informações sobre o conector especificado ou selecionar **[!UICONTROL Exibir tudo]** para ver uma lista de todas as conexões de origem criadas. Mais informações sobre origens podem ser encontradas na [visão geral das origens](../sources/home.md).

A seção **[!UICONTROL Segmentos recentes]** lista as cinco definições de segmento criadas mais recentemente na organização. Essa lista é atualizada sempre que uma nova definição de segmento é criada. Você pode selecionar uma definição de segmento na lista para ver mais informações sobre a definição de segmento especificada ou selecionar **[!UICONTROL Exibir todos]** para ver uma lista de todas as definições de segmento criadas. Mais informações sobre segmentos podem ser encontradas na [Visão geral do Serviço de segmentação](../segmentation/home.md).

A seção **[!UICONTROL Destinos recentes]** lista os cinco destinos criados mais recentemente na organização. Essa lista é atualizada sempre que um novo destino é criado. Você pode selecionar um destino na lista para ver mais informações sobre o destino especificado ou selecionar **[!UICONTROL Exibir todos]** para ver uma lista de todos os destinos criados. Mais informações sobre destinos podem ser encontradas na [visão geral sobre destinos](../destinations/home.md).

### Aprendizado recomendado

A seção **[!UICONTROL Aprendizado recomendado]** fornece links para documentações úteis para começar a usar o Adobe Experience Platform.

![](images/user-guide/homepage-recommended.png)

## Barra de navegação superior

A barra de navegação superior na interface do usuário da Platform exibe a organização na qual você está conectado no momento e fornece vários controles importantes.

No lado esquerdo da barra de navegação, há o logotipo do Adobe Experience Platform. A seleção desse logotipo a qualquer momento o traz de volta à tela inicial da interface do usuário da plataforma.

![](./images/user-guide/homepage-top-nav-bar.png)

### Seletor de organização

O primeiro item no lado direito da barra de navegação superior é o **Seletor de organização**.

![](./images/user-guide/homepage-ims-org-switcher.png)

Selecionar o alternador abre um menu suspenso de organizações às quais você tem acesso, se houver alguma disponível. Para alternar para outra organização, selecione uma opção listada.

### Alternar aplicativos

O próximo item no lado direito da navegação superior é o **alternador de aplicativos**, representado pelo ícone ![alternador de aplicativos](./images/user-guide/app-switcher-icon.png). Ao selecionar esse ícone, você pode alternar entre aplicativos Adobe aos quais sua organização tem acesso, como Experience Platform, Analytics, Assets e outros.

### Ajuda

À direita do alternador de aplicativos está o **menu Ajuda e Suporte**, representado pelo ícone ![ponto de interrogação/ajuda](./images/user-guide/help-icon.png). Ao selecionar esse ícone, um menu pop-over é exibido contendo vários recursos de ajuda e suporte. A guia **[!UICONTROL Ajuda]** mostra uma lista de documentações relevantes para a página em que você está no momento. A guia **[!UICONTROL Suporte]** permite criar um tíquete de suporte com a equipe de suporte do Adobe. A guia **[!UICONTROL Feedback]** permite enviar comentários sobre a Platform para o Adobe.

![](images/user-guide/homepage-help-clicked.png)

### Notificações e anúncios

Na **seção de notificações**, que é representada pelo ícone ![sino/Notificações e Anúncios](images/user-guide/notification-icon.png). A guia **[!UICONTROL Notificações]** mostra informações importantes sobre o produto e outras atualizações relevantes, enquanto a guia **[!UICONTROL Avisos]** mostra informações sobre a manutenção do serviço.

### Perfil de usuário

O item final na barra de navegação superior são as **configurações do usuário**, representadas pelo ícone ![configurações do usuário/Perfil do usuário](images/user-guide/profile-icon.png). Selecione este ícone para editar suas preferências ou sair.

Você pode alternar entre o tema claro e escuro da interface da Platform com o switch localizado logo abaixo do seu nome e email. Selecione o tema de sua preferência.

![](images/theme.png)

### Sandboxes

Imediatamente abaixo da barra de navegação superior está a barra de sandbox. Esta barra mostra qual sandbox você está usando atualmente para a Platform. Mais informações sobre sandboxes podem ser encontradas na [visão geral das sandboxes](../sandboxes/home.md).

## Navegação à esquerda {#left-nav}

A navegação no lado esquerdo da tela lista todos os diferentes serviços compatíveis com a interface do usuário da Platform.

Clique no ícone do menu para mostrar ou ocultar o painel de navegação esquerdo.

![](images/user-guide/hidemenu.png)

Você pode bloquear a navegação na posição aberta clicando novamente depois de mostrar o painel.

>[!IMPORTANT]
>
>A barra de navegação esquerda mostra apenas os recursos que você pode acessar. Em versões anteriores do Adobe Experience Platform, itens indisponíveis eram desativados. Se você achar que deve ter acesso a uma seção que não aparece, entre em contato com o administrador do sistema.

![](images/user-guide/homepage-left.png)

A seção **[!UICONTROL Página inicial]** permite retornar à página inicial da interface do usuário da plataforma.

A seção **[!UICONTROL Fluxos de trabalho]** mostra uma lista de fluxos de trabalho de várias etapas para executar operações na Plataforma. Mais informações sobre fluxos de trabalho podem ser encontradas na [visão geral sobre fluxos de trabalho](./workflows.md).

### [!UICONTROL Conexões]

A seção **[!UICONTROL Fontes]** permite criar, atualizar e excluir conexões de origem, permitindo assimilar dados de fontes externas na Platform. Mais informações sobre origens podem ser encontradas na [visão geral das origens](../sources/home.md).

A seção **[!UICONTROL Destinos]** permite criar, atualizar e excluir destinos, permitindo exportar dados da Platform para vários destinos externos. Mais informações sobre destinos podem ser encontradas na [visão geral sobre destinos](../destinations/home.md).

### [!UICONTROL Cliente]

A seção **[!UICONTROL Perfis]** permite procurar perfis de clientes, exibir métricas de perfil, criar e gerenciar políticas de mesclagem e exibir esquemas de união. Para saber mais sobre como usar a seção [!UICONTROL Perfis], leia o [[!DNL Profile] guia do usuário](../profile/ui/user-guide.md). Mais informações sobre o Perfil do cliente em tempo real podem ser encontradas na [Visão geral do Perfil do cliente em tempo real](../profile/home.md).

A seção **[!UICONTROL Audiences]** permite criar e gerenciar definições de segmento. Para saber mais sobre como usar a seção [!UICONTROL Públicos-alvo], leia o [guia do usuário de segmentação](../segmentation/ui/overview.md). Mais informações sobre o Serviço de segmentação podem ser encontradas na [visão geral do Serviço de segmentação](../segmentation/home.md).

A seção **[!UICONTROL Identidades]** permite criar e gerenciar namespaces de identidade. Para obter mais informações sobre a seção [!UICONTROL Identidades], incluindo informações sobre namespaces de identidade e como usar identidades na interface da Platform, consulte a [visão geral sobre namespaces de identidade](../identity-service/features/namespaces.md).

### [!UICONTROL Privacidade]

A seção **[!UICONTROL Políticas]** permite criar e gerenciar políticas de uso de dados. Para saber mais sobre como usar a seção Políticas, leia o [guia do usuário de políticas de uso de dados](../data-governance/policies/user-guide.md). Mais informações sobre políticas de uso de dados podem ser encontradas na [visão geral das políticas de uso de dados](../data-governance/policies/overview.md).

A seção **[!UICONTROL Solicitações]** permite criar e gerenciar solicitações de privacidade. Incluir na lista de permissões Observe que você deve ser atualizado para ter acesso à interface do usuário do Privacy Service. Para saber mais sobre como usar a seção Solicitações, leia o [guia do usuário do Privacy Service](../privacy-service/ui/user-guide.md). Mais informações sobre o Privacy Service podem ser encontradas na [visão geral do Privacy Service](../privacy-service/home.md).

### [!UICONTROL Ciência de dados]

A seção **[!UICONTROL Notebooks]** fornece acesso ao JupyterLab, um ambiente de desenvolvimento interativo que permite explorar, analisar e modelar seus dados. Para saber mais sobre como usar a seção Notebooks, leia o [guia do usuário do JupyterLab](../data-science-workspace/jupyterlab/overview.md). Mais informações sobre o Data Science Workspace podem ser encontradas na [visão geral do Data Science Workspace](../data-science-workspace/home.md)

A seção **[!UICONTROL Modelos]** permite usar o aprendizado de máquina e a inteligência artificial para criar, desenvolver, treinar e ajustar modelos e fazer previsões. Mais informações sobre a seção Modelos podem ser encontradas no tutorial sobre [treinamento e avaliação de um modelo](../data-science-workspace/models-recipes/train-evaluate-model-ui.md).

A seção **[!UICONTROL Serviços]** permite gerenciar os modelos publicados para treinamento e pontuação agendados ou usar os Serviços inteligentes do Adobe, um conjunto de serviços de IA que fornecem experiências do cliente personalizadas e em tempo real. Mais informações sobre a seção Serviços podem ser encontradas no [tutorial Publicação de um Modelo como um Serviço](../data-science-workspace/models-recipes/publish-model-service-ui.md).

### [!UICONTROL Gerenciamento de dados]

A seção **[!UICONTROL Esquemas]** permite criar e gerenciar esquemas do Experience Data Model (XDM). Para saber mais sobre esquemas, leia o tutorial sobre [criação de um esquema](../xdm/tutorials/create-schema-ui.md). Mais informações sobre o XDM podem ser encontradas na [visão geral do Sistema XDM](../xdm/home.md).

A seção **[!UICONTROL Datasets]** permite criar e gerenciar conjuntos de dados. Mais informações sobre conjuntos de dados podem ser encontradas no [guia do usuário dos conjuntos de dados](../catalog/datasets/user-guide.md).

A seção **[!UICONTROL Consultas]** permite criar e gerenciar consultas, registrar consultas SQL feitas pelo Serviço de Consulta da Adobe Experience Platform e exibir suas credenciais do [!DNL PostgreSQL]. Mais informações sobre consultas podem ser encontradas no [guia do usuário do Serviço de Consulta](../query-service/ui/overview.md).

A seção **[!UICONTROL Monitoramento]** permite monitorar a assimilação de lote e streaming. Mais informações sobre monitoramento podem ser encontradas no [guia do usuário de assimilação de dados de monitoramento](../ingestion/quality/monitor-data-ingestion.md).

### [!UICONTROL Decisão]

O Adobe Journey Optimizer é um serviço de aplicativos criado sobre o Experience Platform. Ele permite usar tecnologias de decisão avançadas para fornecer a melhor oferta e experiência aos seus clientes em todos os pontos de contato na hora certa. Para saber mais sobre o Journey Optimizer, incluindo como trabalhar com [!UICONTROL Ofertas] e [!UICONTROL Atividades], visite a [documentação do Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer.html?lang=pt-BR).

### [!UICONTROL Administração]

A interface do usuário (UI) da Platform fornece um painel por meio do qual você pode visualizar informações importantes sobre o uso de licença da organização, conforme capturadas durante um instantâneo diário. Acesse este painel selecionando **[!UICONTROL Uso da licença]** na navegação. Para saber mais sobre o painel de uso de licença, visite o [guia do painel de uso de licença](./license-usage-and-guardrails/license-usage-dashboard.md).

>[!IMPORTANT]
>
>No momento, a funcionalidade do painel de uso de licença está em alfa e não está disponível para todos os usuários. A documentação e a funcionalidade estão sujeitas a alterações.

## Próximas etapas

Após a leitura deste guia, você foi apresentado à página inicial e aos principais elementos de navegação da interface do usuário da Platform. Para obter informações mais detalhadas sobre como trabalhar na interface do usuário, consulte a documentação de cada serviço individual do Platform. Links para esta documentação são fornecidos na seção [navegação à esquerda](#left-nav), localizada anteriormente neste documento.
