---
keywords: Experience Platform;página inicial;tópicos populares;controle de acesso;adobe admin console
solution: Experience Platform
title: Visão geral do controle de acesso
description: O controle de acesso do Adobe Experience Platform é fornecido por meio da Adobe Admin Console. Essa funcionalidade aproveita perfis de produto no Admin Console, que vinculam usuários com permissões e sandboxes.
exl-id: 591d59ad-2784-4ae4-a509-23649ce712c9
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '3818'
ht-degree: 0%

---

# Visão geral do controle de acesso

O controle de acesso do Adobe Experience Platform é fornecido através das **[!UICONTROL Permissões]** no [Adobe Experience Cloud](https://experience.adobe.com/). Essa funcionalidade aproveita funções e políticas, que vinculam usuários com permissões e sandboxes.

## Hierarquia e fluxo de trabalho do controle de acesso

Para configurar o controle de acesso para o Experience Platform, você deve ter privilégios de administrador do sistema ou do produto para uma organização que tenha um produto da Experience Platform. A função mínima que pode conceder ou retirar permissões é um administrador de produto. Outras funções de administrador que podem gerenciar permissões são administradores do sistema (sem restrições). Consulte o artigo da Central de ajuda da Adobe em [funções administrativas](https://helpx.adobe.com/br/enterprise/using/admin-roles.html) para obter mais informações.

>[!NOTE]
>
>A partir deste ponto, qualquer menção a &quot;administrador&quot; neste documento se refere a um administrador de produto ou superior (conforme descrito acima).

Um workflow de alto nível para obter e atribuir permissões de acesso pode ser resumido da seguinte maneira:

- Após o licenciamento do Adobe Experience Platform ou de um Aplicativo/Serviço de Aplicativo que usa o Experience Platform, um email é enviado ao administrador especificado durante o licenciamento.
- O administrador faz logon no [Adobe Admin Console](#adobe-admin-console) e seleciona **Adobe Experience Platform** da lista de produtos na página de visão geral.
- Para conceder acesso ao Experience Platform, é recomendável que o administrador adicione usuários ao perfil de produto padrão: `AEP-Default-All-Users`.
- Nas Permissões do Experience Platform, o administrador pode criar novas funções ou editar as permissões e os usuários de qualquer função existente.
- Ao criar ou editar uma função, o administrador adiciona usuários à função usando a guia **[!UICONTROL usuários]** e concede permissões a esses usuários (como &quot;[!UICONTROL Ler Conjuntos de Dados]&quot; ou &quot;[!UICONTROL Gerenciar Esquemas]&quot;) ao editar as permissões da função. Da mesma forma, o administrador pode atribuir acesso a sandboxes usando a mesma opção de edição.
- Quando os usuários fazem logon na interface do usuário do Experience Platform, o acesso aos recursos do Experience Platform é orientado pelas permissões concedidas a eles na etapa anterior. Por exemplo, se um usuário não tiver a permissão [!UICONTROL Exibir conjuntos de dados], a guia **[!UICONTROL Conjuntos de dados]** no menu lateral não estará visível para esse usuário.

Para obter etapas mais detalhadas sobre como gerenciar o controle de acesso no Experience Platform, consulte o [guia do usuário de controle de acesso](./ui/overview.md).

Todas as chamadas para APIs do Experience Platform são validadas em relação a permissões e retornarão erros se as permissões apropriadas não forem encontradas no contexto do usuário atual. Na interface do usuário, os elementos serão ocultos ou alterados dependendo das permissões concedidas ao usuário atual.

## Permissões {#platform-permissions}

As [!UICONTROL Permissões] fornecem um local central para gerenciar o acesso à Experience Platform para sua organização. Através das [!UICONTROL Permissões], você pode conceder a grupos de usuários permissões de acesso para vários recursos do Experience Platform, como [!UICONTROL Gerenciar conjuntos de dados], [!UICONTROL Exibir conjuntos de dados] ou [!UICONTROL Gerenciar perfis].

### Funções

Na seção [!UICONTROL Funções], permissões são atribuídas a usuários por meio do uso de funções. As funções permitem conceder permissões a um ou vários usuários e também contêm acesso ao escopo das sandboxes atribuídas a eles por meio de funções. Os usuários podem ser atribuídos a uma ou várias funções pertencentes à sua organização.

### Funções padrão

O Experience Platform vem com duas funções padrão pré-configuradas. A tabela a seguir descreve o que é fornecido em cada perfil padrão, incluindo a sandbox à qual eles concedem acesso, bem como as permissões que concedem no escopo dessa sandbox.

| Função | Acesso à sandbox | Permissões |
| --- | --- | --- |
| Acesso total à produção padrão | Prod | Todas as permissões aplicáveis ao Experience Platform, exceto as permissões de Administração de sandbox. |
| Administradores de sandbox | N/D | Fornece acesso à sandbox `Prod` e às permissões de Administração de sandbox. |

## Sandboxes e permissões

As sandboxes de não produção são uma forma de virtualização de dados que permitem isolar dados de outras sandboxes e são normalmente usadas para experimentos de desenvolvimento, testes ou avaliações. As permissões de uma função concedem aos usuários da função acesso aos recursos do Experience Platform nos ambientes de sandbox aos quais eles receberam acesso. Uma licença padrão do Experience Platform concede cinco sandboxes (uma de produção e quatro de não produção). Você pode adicionar pacotes de dez sandboxes de não produção até um máximo de 75 sandboxes no total. Entre em contato com o administrador da organização ou com o representante de vendas da Adobe para obter mais detalhes.

Para obter mais informações sobre sandboxes na Experience Platform, consulte a [visão geral das sandboxes](../sandboxes/home.md).

### Acesso a sandboxes

O acesso a sandboxes é gerenciado por meio de funções. Para obter etapas detalhadas sobre como habilitar o acesso a uma sandbox para uma função, consulte o [guia de funções de controle de acesso baseado em atributo](./abac/ui/roles.md).

É possível conceder aos usuários acesso a uma ou mais sandboxes em uma função. Se um usuário estiver incluído em duas ou mais funções, ele terá acesso a todas as sandboxes incluídas nessas funções.

A permissão &quot;Gerenciamento de sandbox&quot; permite que os usuários gerenciem, visualizem ou redefinam sandboxes.

### Permissões de recurso {#permissions}

As permissões de recursos concedem acesso a recursos específicos do Experience Platform. Os recursos são divididos em categorias que contêm um conjunto de permissões relevantes, que podem ser atribuídas individualmente a funções.

Em [!UICONTROL Permissões], o espaço de trabalho de recursos de uma função exibe as sandboxes e as permissões que estão ativas para essa função:

![Um espaço de trabalho de recursos da função com uma lista de categorias e permissões selecionadas.](./images/permissions.png)

A tabela a seguir descreve as categorias de recursos disponíveis para o Experience Platform e aplicativos gerenciados por meio de Permissões:

| Categoria | Descrição |
| --- | --- |
| [!DNL Adobe Mix Modeler] | Configurar, gerenciar e exibir permissões para [!DNL Adobe Mix Modeler]. |
| [!DNL AI Assistant] | Configurar permissões para [!DNL AI Assistant]. |
| [!DNL Alerts] | Configure, gerencie e visualize permissões para alertas e histórico de alertas. |
| [!DNL B2B Account Lists] | Configure permissões de gerenciamento, visualização e publicação para listas de contas B2B, incluindo ações como adicionar, remover, importar e excluir contas de listas de contas. |
| [!DNL B2B Admin Configurations] | Configure permissões de gerenciamento e visualização para configurações do administrador B2B, incluindo conexões de gerenciamento de ativos digitais, repositórios de ativos e eventos. |
| [!DNL B2B Assets] | Configure permissões de gerenciamento e visualização para ativos B2B, incluindo emails, SMS, páginas de aterrissagem, fragmentos, modelos e imagens. |
| [!DNL B2B Buying Groups] | Configure permissões de gerenciamento e visualização para grupos de compra B2B, incluindo recursos como interesses de solução, modelos de funções e status do grupo de compra. |
| [!DNL B2B Channel Configurations] | Configure permissões de gerenciamento e visualização para configurações de canal B2B, incluindo configurações como limites de comunicação, credenciais da API e configurações de segurança. |
| [!DNL B2B Dashboards] | Configure permissões de exibição para painéis B2B, incluindo recursos como envolvimento de conta, estágios de grupo de compra, contas de surging e cobertura de contato. |
| [!DNL B2B Journeys] | Configure permissões de gerenciamento, visualização e publicação para jornadas B2B, incluindo recursos como ações de conta e pessoa, ouvintes de eventos e caminhos divididos. |
| [!DNL Campaigns] | Configure permissões de gerenciamento, publicação e visualização para campanhas no Journey Optimizer. |
| [!DNL Channel Configurations] | Configure recursos de gerenciamento, visualização e exportação de configurações de canal, como subdomínios, pools de IP, predefinições de mensagem, registros PTR, listas de supressão, configurações de página de aterrissagem, configurações de SMS e roteamento de arquivos. |
| [!DNL Collaborations] | Configure permissões de gerenciamento e visualização para os recursos do Real-time Customer Data Profile Collaboration. |
| [!DNL Computed Attributes] | Configure as permissões de gerenciamento e visualização para rascunhar ou publicar atributos computados. |
| [!DNL Customer Managed Keys] | Configure permissões de gerenciamento para chaves gerenciadas pelo cliente. |
| [!DNL Dashboards] | Configure permissões de gerenciamento e visualização para painéis padrão, personalizados e licenciados. |
| [!DNL Data Collection] | Configurar permissões de gerenciamento e visualização para sequências de dados. |
| [!DNL Data Governance] | Configure, gerencie, aplique e visualize permissões para recursos de Governança de dados, como rótulos, políticas e logs de atividades. |
| [!DNL Data Ingestion] | Configure permissões de gerenciamento e visualização para recursos de assimilação de dados, como fontes e compartilhamento de público-alvo. |
| [!DNL Data Lifecycle] | Configure permissões de gerenciamento e visualização para recursos de higiene de dados. |
| [!DNL Data Management] | Configure permissões de gerenciamento e visualização para recursos de gerenciamento de dados, como conjuntos de dados e monitoramento de conjuntos de dados e fluxos. |
| [!DNL Data Modeling] | Configure permissões de gerenciamento e visualização para recursos de modelagem de dados, como esquemas, relacionamentos e metadados de identidade. |
| [!DNL Data Science Workspace] | Configurar permissões de gerenciamento para [!DNL Data Science Workspace]. |
| [!DNL Decision Management] | Configure permissões de gerenciamento e visualização para decisões, ofertas e recursos de estratégia de classificação na gestão de decisões. |
| [!DNL Destinations] | Configure permissões de gerenciamento e visualização para destinos, incluindo recursos como ativação e criação com o Destinations SDK. |
| [!DNL Federated Data] | Configure permissões de gerenciamento e exibição para recursos de dados federados. |
| [!DNL Identity Management] | Configure permissões de gerenciamento e visualização para recursos do Serviço de identidade, como namespaces de identidade e o gráfico de identidade. |
| [!DNL Intelligent Service] | Configure permissões de gerenciamento e visualização para a IA de atribuição e a IA do cliente no serviço inteligente. |
| [!DNL IP Warmup Configurations] | Configure e visualize permissões para planos de aquecimento de IP e visualize permissões para visualizar relatórios de aquecimento de IP. |
| [!DNL Journey Optimizer Library] | Configure permissões de gerenciamento para itens de biblioteca no Adobe Journey Optimizer. |
| [!DNL Journey Optimizer Rules] | Configure permissões de gerenciamento e visualização para regras de frequência no Adobe Journey Optimizer. |
| [!DNL Journeys] | Configure permissões de gerenciamento, publicação e exibição para o jornada, incluindo recursos como relatórios do jornada, eventos, fontes de dados e ações. |
| [!DNL Messages] | Configure permissões de gerenciamento, publicação e visualização de mensagens, incluindo recursos como pré-visualização e teste de mensagens. |
| [!DNL Privacy Service] | Configure permissões de gerenciamento e visualização para recursos do Privacy Service. |
| [!DNL Profile Management] | Configure permissões de gerenciamento, visualização, exportação e avaliação para recursos do serviço de perfil, como públicos, perfis e políticas de mesclagem. |
| [!DNL Prospects] | Configure permissões de gerenciamento e visualização para esquemas, perfis e públicos-alvo de clientes potenciais, incluindo recursos como a exibição da opção de cliente potencial. |
| [!DNL Query Service] | Configure permissões de gerenciamento para recursos de serviço de consulta, como consultas SQL estruturadas e de credencial sem expiração. |
| [!DNL Reports] | Configurar permissões de exibição para relatórios de canal. |
| [!DNL Sandbox Administration] | Configure permissões de gerenciamento, visualização e redefinição ao administrar sandboxes. |
| [!DNL Traits Configuration] | Configure e visualize características por meio da interface do usuário de atributos computados. |
| [!DNL Translation Services] | Configure permissões de gerenciamento e visualização para serviços de tradução para projetos, tarefas, revisões, internas, configurações e provedores. |

A tabela a seguir descreve as permissões disponíveis para o Experience Platform na função, com descrições dos recursos específicos do Experience Platform aos quais eles concedem acesso. Para obter etapas detalhadas sobre como adicionar permissões a uma função, consulte o [guia de funções de controle de acesso baseado em atributo](./abac/ui/roles.md).

| Categoria | Permissão | Descrição |
| --- | --- | --- |
| [!DNL Adobe Mix Modeler] | [!UICONTROL Gerenciar dados harmonizados do Adobe Mix Modeler] | A capacidade de visualizar e modificar dados harmonizados. |
| [!DNL Adobe Mix Modeler] | [!UICONTROL Exibir Dados Harmonizados do Adobe Mix Modeler] | Acesso somente leitura a dados harmonizados. |
| [!DNL Adobe Mix Modeler] | [!UICONTROL Gerenciar configurações de modelos do Adobe Mix Modeler] | A capacidade de exibir e modificar configurações de modelos. |
| [!DNL Adobe Mix Modeler] | [!UICONTROL Exibir Configurações De Modelos Do Adobe Mix Modeler] | Acesso somente leitura a configurações de modelos. |
| [!DNL Adobe Mix Modeler] | [!UICONTROL Gerenciar configurações de planos de modelos do Adobe Mix Modeler] | A capacidade de exibir e modificar configurações de planos. |
| [!DNL Adobe Mix Modeler] | [!UICONTROL Exibir Configurações De Planos De Modelos Do Adobe Mix Modeler] | Acesso somente leitura a configurações de planos. |
| [!DNL AI Assistant] | [!UICONTROL Habilitar o Assistente de IA] | Capacidade de fazer as perguntas de [[!DNL [AI assistant]]](../ai-assistant/access.md). |
| [!DNL AI Assistant] | [!UICONTROL Exibir Insights Operacionais] | Acesso para obter respostas a consultas de [insights operacionais](../ai-assistant/home.md##operational-insights). |
| [!DNL AI Assistant] | [!UICONTROL Gerar conteúdo] | Habilitar usuários a gerar conteúdo usando o [!DNL AI Assistant]. |
| [!DNL AI Assistant] | [!UICONTROL Gerenciar Kit de Marcas] | Habilitar usuários a criar diretrizes de marca usando o [!DNL AI Assistant]. |
| [!DNL Alerts] | [!UICONTROL Exibir Histórico de Alertas] | Acesso somente leitura para o histórico de alertas. |
| [!DNL Alerts] | [!UICONTROL Resolver alertas] | Acesso para ler, editar e excluir alertas. |
| [!DNL Alerts] | [!UICONTROL Exibir Alertas] | Acesso somente leitura para alertas. |
| [!DNL Alerts] | [!UICONTROL Gerenciar alertas] | Acesso para ler, criar, editar e excluir alertas. |
| [!DNL B2B Account Lists] | [!UICONTROL Gerenciar listas de contas B2B] | Capacidade de exibir e acessar **[!UICONTROL Listas de contas]** na navegação à esquerda. Os usuários com acesso a **[!UICONTROL Listas de Contas]** devem ter acesso a todas as funções CRUD de Listas de Contas: `/accounts-list`. |
| [!DNL B2B Admin Configurations] | [!UICONTROL Gerenciar configurações do administrador B2B] | Capacidade de exibir e acessar **[!UICONTROL Configurações do administrador B2B]** na navegação à esquerda. Os usuários com acesso às **[!UICONTROL Configurações de Administrador B2B]** devem ter acesso a todas as funções CRUD de Credenciais de API de SMS: `/admin-configs`. |
| [!DNL B2B Assets] | [!UICONTROL Gerenciar Assets B2B] | Capacidade de exibir e acessar o **[!UICONTROL Assets]** na navegação à esquerda. Os usuários com acesso ao **[!UICONTROL Assets]** devem ter acesso a todas as funções CRUD do Assets: `/assets-listing`. |
| [!DNL B2B Assets] | [!UICONTROL Gerenciar Modelos B2B] | Capacidade de exibir e acessar **[!UICONTROL Modelos]** na navegação à esquerda. Os usuários com acesso a **[!UICONTROL Modelos]** devem ter acesso a todas as funções CRUD de Modelos: `/b2b-content-templates`. |
| [!DNL B2B Assets] | [!UICONTROL Gerenciar fragmentos B2B] | Capacidade de exibir e acessar **[!UICONTROL Fragmentos]** na navegação à esquerda. Os usuários com acesso a **[!UICONTROL Fragmentos]** devem ter acesso a todas as funções CRUD de fragmentos: `/fragments`. |
| [!DNL B2B Buying Groups] | [!UICONTROL Gerenciar Grupos De Compras B2B] | Capacidade de exibir e acessar **[!UICONTROL Grupos de Compras]** na navegação à esquerda. Os usuários com acesso a **[!UICONTROL Grupos de Compra]** devem ter acesso a todas as funções CRUD de Grupos de Compra: `/buying-groups`. |
| [!DNL B2B Dashboards] | [!UICONTROL Gerenciar Painéis de Envolvimento B2B] | Capacidade de exibir e acessar o **[!UICONTROL Painel]** na navegação à esquerda. Os usuários com acesso a **[!UICONTROL Painéis]** devem ter acesso a todas as funções CRUD de Painéis: `/insights-dashboard`. |
| [!DNL B2B Channel Configurations] | [!UICONTROL Gerenciar configurações de canais B2B] | Capacidade de exibir e acessar **[!UICONTROL Canais]** na navegação à esquerda. Os usuários com acesso a **[!UICONTROL Canais]** devem ter acesso a todas as funções de CRUD de canais: `/channels-config`. |
| [!DNL B2B Journeys] | [!UICONTROL Gerenciar Jornadas da Conta B2B] | Capacidade de exibir e acessar **[!UICONTROL Jornadas da conta]** na navegação à esquerda. Os usuários com acesso a **[!UICONTROL Jornadas de Conta]** devem ter acesso a todas as funções CRUD de Jornadas de Conta: `/account-journeys`. |
| [!DNL Campaigns] | [!UICONTROL Gerenciar Campanhas] | Acesso para ler, criar, editar e excluir campanhas. |
| [!DNL Campaigns] | [!UICONTROL Aprovar e publicar campanhas] | A capacidade de aprovar e publicar campanhas. |
| [!DNL Campaigns] | [!UICONTROL Publicar Campanhas] | Capacidade de publicar campanhas. |
| [!DNL Campaigns] | [!UICONTROL Exibir Campanhas] | Acesso somente leitura às campanhas. |
| [!DNL Campaigns] | [!UICONTROL Exibir Relatório de Campanhas] | Acesso somente leitura aos relatórios da campanha. |
| [!DNL Channel Configurations] | [!UICONTROL Exibir Configurações Gerais das Mensagens] | Acesso somente leitura a configurações gerais de mensagens. |
| [!DNL Channel Configurations] | [!UICONTROL Gerenciar Delegações De Subdomínios] | Acesso para ler, criar, editar e excluir delegações de subdomínio. |
| [!DNL Channel Configurations] | [!UICONTROL Gerenciar Pools de IPs] | Acesso para ler, criar e editar pools de IP. |
| [!DNL Channel Configurations] | [!UICONTROL Configurações Gerais para Gerenciar Mensagens] | Acesso para ler, criar, editar e excluir configurações gerais de mensagens. |
| [!DNL Channel Configurations] | [!UICONTROL Gerenciar predefinições de mensagens] | Acesso para ler, criar, editar e excluir predefinições de mensagens. |
| [!DNL Channel Configurations] | [!UICONTROL Exibir Predefinições De Mensagens] | Acesso somente leitura a predefinições de mensagens. |
| [!DNL Channel Configurations] | [!UICONTROL Gerenciar Registros PTR] | Acesso para ler e editar registros PTR. |
| [!DNL Channel Configurations] | [!UICONTROL Exibir Registros PTR] | Acesso somente leitura a registros PTR. |
| [!DNL Channel Configurations] | [!UICONTROL Gerenciar supressão] | Acesso para ler, criar, editar e excluir regras de supressão. |
| [!DNL Channel Configurations] | [!UICONTROL Exibir Lista de Supressão] | Acesso somente leitura à lista de supressão. |
| [!DNL Channel Configurations] | [!UICONTROL Exportar Lista de Supressão] | Acesso para exportar a lista de supressão como um arquivo CSV. |
| [!DNL Channel Configurations] | [!UICONTROL Gerenciar Configurações Da Página De Aterrissagem] | Acesso para ler, criar, editar e excluir configurações de página de aterrissagem. |
| [!DNL Channel Configurations] | [!UICONTROL Gerenciar configurações de SMS] | Acesso para ler, criar, editar e excluir configurações de SMS. |
| [!DNL Channel Configurations] | [!UICONTROL Gerenciar Subdomínios de SMS] | Acesso para ler, criar, editar e excluir subdomínios de SMS. |
| [!DNL Channel Configurations] | [!UICONTROL Gerenciar Roteamento de Arquivos] | Acesso para ler, criar, editar e excluir roteamentos de arquivos. |
| [!DNL Channel Configurations] | [!UICONTROL Exibir Roteamento de Arquivos] | Acesso somente leitura a roteamentos de arquivos. |
| [!DNL Channel Configurations] | [!UICONTROL Gerenciar lista de propagação] | A capacidade de criar e editar a Seedlist. |
| [!DNL Channel Configurations] | [!UICONTROL Gerenciar Configurações de Idioma] | A capacidade de criar e editar as configurações de idioma. |
| [!DNL Channel Configurations] | [!UICONTROL Gerenciar Subdomínios da Web] | A capacidade de criar e editar subdomínios da Web do CJM. |
| [!DNL Channel Configurations] | [!UICONTROL Gerenciar credenciais de push] | A capacidade de criar, editar e excluir credenciais de push. |
| [!DNL Collaborations] | [!UICONTROL Gerenciar instâncias do Collaboration] | Exibir, criar, atualizar e excluir as instâncias de colaboração de uma organização. Descubra as instâncias de colaboração de outras organizações. |
| [!DNL Collaborations] | [!UICONTROL Ler instâncias do Collaboration] | Leia as instâncias de colaboração de uma organização e descubra as instâncias de colaboração de outras organizações. |
| [!DNL Collaborations] | [!UICONTROL Gerenciar convites de conexão] | Exibir, criar e excluir convites de conexão iniciados por sua organização. Aceitar e recusar convite de conexão iniciado por outras organizações. |
| [!DNL Collaborations] | [!UICONTROL Ler convites de conexão] | Acesso somente leitura a convites de conexão. |
| [!DNL Collaborations] | [!UICONTROL Gerenciar Conexões do Collaboration] | Um anunciante pode exibir, criar e atualizar configurações, bem como enviar e excluir conexões. Um editor pode exibir, aceitar ou recusar conexões. |
| [!DNL Collaborations] | [!UICONTROL Ler Conexões do Collaboration] | Acesso somente leitura a conexões. |
| [!DNL Collaborations] | [!UICONTROL Gerenciar dados de público-alvo] | Integre e descubra públicos-alvo. Atualize públicos-alvo públicos, privados e personalizados e gerencie configurações de metadados do Audience Inventory. |
| [!DNL Collaborations] | [!UICONTROL Ler dados de público-alvo] | Leia e descubra públicos-alvo. |
| [!DNL Collaborations] | [!UICONTROL Gerenciar Dados de Medição] | Integrar, atualizar e excluir dados de medição. |
| [!DNL Collaborations] | [!UICONTROL Ler dados de medição] | Acesso somente leitura aos dados de medição. |
| [!DNL Collaborations] | [!UICONTROL Gerenciar Projetos] | Exiba, crie, atualize e exclua projetos para qualquer uma das atividades de descoberta, compartilhamento, ativação e medição. |
| [!DNL Collaborations] | [!UICONTROL Ler projetos] | Visualize projetos para qualquer uma das atividades de descoberta, compartilhamento, ativação e medição. |
| [!DNL Collaborations] | [!UICONTROL Ler atividades do usuário] | Acesso somente leitura às atividades do usuário. |
| [!DNL Collaborations] | [!UICONTROL Exportar atividades do usuário] | Exportar atividades do usuário. |
| [!DNL Collaborations] | [!UICONTROL Ler Monitoramento de Crédito da Collaboration] | Monitoramento de crédito no nível da organização e da instância. |
| [!DNL Computed Attributes] | [!UICONTROL Exibir atributos computados] | Acesso somente leitura para a guia de atributos calculados, inventário e detalhes. |
| [!DNL Computed Attributes] | [!UICONTROL Gerenciar atributos computados] | Acesso para ler, criar, excluir rascunhos e desativar atributos calculados. |
| [!DNL Customer Managed Keys] | [!UICONTROL Gerenciar Chaves Gerenciadas pelo Cliente] | Acesso para exibir e configurar chaves gerenciadas pelo cliente. |
| [!DNL Dashboards] | [!UICONTROL Exibir Painel de Uso de Licenças] | Acesso somente leitura para exibir o painel de uso de licença. |
| [!DNL Dashboards] | [!UICONTROL Gerenciar Painéis Padrão] | Adicione atributos personalizados que ainda não estão no data warehouse. |
| [!DNL Dashboards] | [!UICONTROL Exibir Painéis Padrão] | Acesso somente leitura para exibir o painel de uso de licença. |
| [!DNL Dashboards] | [!UICONTROL Gerenciar Painéis Personalizados] | Acesso para criar ou editar um painel. |
| [!DNL Dashboards] | [!UICONTROL Exibir Painéis Personalizados] | Acesso somente leitura a painéis definidos pelo usuário. |
| [!DNL Dashboards] | [!UICONTROL Gerenciar Agendamentos de Relatórios] | Capacidade de criar agendamentos. |
| [!DNL Data Collection] | [!UICONTROL Gerenciar Datastreams] | Acesso para ler, criar e editar fluxos de dados. |
| [!DNL Data Collection] | [!UICONTROL Exibir Datastreams] | Acesso somente leitura a sequências de dados. |
| [!DNL Data Governance] | [!UICONTROL Gerenciar rótulos de uso] | Acesso para ler, criar e excluir rótulos de uso. |
| [!DNL Data Governance] | [!UICONTROL Gerenciar Políticas de Uso de Dados] | Acesso para ler, criar, editar e excluir políticas de uso de dados. |
| [!DNL Data Governance] | [!UICONTROL Exibir Políticas de Uso de Dados] | Acesso somente leitura para políticas de uso de dados pertencentes à sua organização. |
| [!DNL Data Governance] | [!UICONTROL Exibir Log de Atividades do Usuário] | Acesso somente leitura para exibir [logs de auditoria](../landing/governance-privacy-security/audit-logs/overview.md) registrados de atividades do Experience Platform. |
| [!DNL Data Governance] | [!UICONTROL Exibir Console de Privacidade] | Acesso somente leitura aos consoles de privacidade. |
| [!DNL Data Ingestion] | [!UICONTROL Gerenciar fontes] | Acesso para ler, criar, editar e desativar fontes. |
| [!DNL Data Ingestion] | [!UICONTROL Exibir fontes] | Acesso somente leitura a fontes disponíveis na guia **[!UICONTROL Catálogo]** e fontes autenticadas na guia **[!UICONTROL Procurar]**. |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share Connections] | Acesse para criar, aceitar e recusar o compartilhamento de parceiros para conectar duas organizações e habilitar os fluxos do [!DNL Segment Match]. |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share] | Acesso para ler, criar, editar e publicar feeds do [!DNL Segment Match] com parceiros ativos. |
| [!DNL Data Lifecycle] | [!UICONTROL Exibir Ciclo de Vida dos Dados] | Acesso somente leitura para o ciclo de vida dos dados. |
| [!DNL Data Lifecycle] | [!UICONTROL Gerenciar Ciclo de Vida dos Dados] | Acesso para ler, criar, editar e excluir o ciclo de vida dos dados. |
| [!DNL Data Modeling] | [!UICONTROL Gerenciar esquemas] | Acesso para ler, criar, editar e excluir esquemas e recursos relacionados. |
| [!DNL Data Modeling] | [!UICONTROL Exibir Esquemas] | Acesso somente leitura a esquemas e recursos relacionados. |
| [!DNL Data Modeling] | [!UICONTROL Gerenciar Relações] | Acesso para ler, criar, editar e excluir relacionamentos de esquema. |
| [!DNL Data Modeling] | [!UICONTROL Gerenciar metadados de identidade] | Acesso para ler, criar, editar e excluir metadados de identidade de esquemas. |
| [!DNL Data Management] | [!UICONTROL Gerenciar conjuntos de dados] | Acesso para ler, criar, editar e excluir conjuntos de dados. Acesso somente leitura para esquemas. |
| [!DNL Data Management] | [!UICONTROL Exibir Conjuntos de Dados] | Acesso somente leitura para conjuntos de dados e esquemas. |
| [!DNL Data Management] | [!UICONTROL Monitoramento de dados] | Acesso somente leitura a conjuntos de dados e fluxos de monitoramento. |
| [!DNL Data Science Workspace] | [!UICONTROL Gerenciar o Data Science Workspace] | Acesso para ler, criar, editar e excluir em [!DNL Data Science Workspace]. |
| [!DNL Decision Management] | [!UICONTROL Gerenciar decisão de experiência] | Capacidade de gerenciar entidades de decisão de experiência. |
| [!DNL Decision Management] | [!UICONTROL Exibir decisão de experiência] | Acesso somente leitura a entidades do Experience Decisioning. |
| [!DNL Decision Management] | [!UICONTROL Gerenciar Decisões] | Acesso para ler, criar, editar e excluir entidades de decisão. |
| [!DNL Decisions Management] | [!UICONTROL Exibir Decisões] | Acesso somente leitura a entidades de decisão. |
| [!DNL Decision Management] | [!UICONTROL Gerenciar Ofertas] | Acesso para ler, criar, editar e excluir todas as ofertas e componentes. Acesso somente leitura a decisões e coleções. |
| [!DNL Decsion Management] | [!UICONTROL Gerenciar Estratégias De Classificação] | Acesso para ler, criar, editar e excluir relatórios personalizados e usar recursos de ação. |
| [!DNL Destinations] | [!UICONTROL Exibir Destinos] | Acesso somente leitura para exibir os destinos disponíveis na guia **[!UICONTROL Catálogo]** e destinos autenticados na guia **[!UICONTROL Procurar]**. |
| [!DNL Destinations] | [!UICONTROL Gerenciar destinos] | Acesso para ler, criar e excluir conexões de destino e contas de destino. |
| [!DNL Destinations] | [!UICONTROL Ativar Destinos] | Capacidade de ativar dados para destinos ativos que foram criados. Esta permissão também requer que [!UICONTROL Exibir Destinos] ou [!UICONTROL Gerenciar Destinos] sejam concedidos ao usuário que ativará os destinos. |
| [!DNL Destinations] | [!UICONTROL Ativar segmento sem mapeamento] | A capacidade de ativar públicos para destinos existentes, sem exibir a [etapa de mapeamento](../destinations/ui/activate-batch-profile-destinations.md#mapping). Os usuários podem adicionar e remover públicos-alvo em workflows de ativação, mas não podem adicionar ou remover atributos ou identidades mapeadas. Esta permissão também requer que a permissão [!UICONTROL Exibir Destinos] seja concedida ao usuário que ativará os dados para destinos. |
| [!DNL Destinations] | [!UICONTROL Gerenciar e ativar destinos do conjunto de dados] | Capacidade de ler, criar, editar e desativar fluxos de exportação do conjunto de dados. Capacidade de também ativar dados para conjuntos de dados ativos que foram criados. Esta permissão também requer que a permissão [!UICONTROL Exibir Destinos] seja concedida ao usuário que ativará os dados para destinos. |
| [!DNL Destinations] | [!UICONTROL Criação de Destino] | Capacidade de criar destinos usando o [Adobe Experience Platform Destination SDK](../destinations/destination-sdk/overview.md). |
| [!DNL Federated Data] | [!UICONTROL Gerenciar Dados Federados] | A capacidade de acessar todos os recursos de dados federados, como criar esquemas, modelos e composições. |
| [!DNL Identity Management] | [!UICONTROL Gerenciar Namespaces de Identidade] | Acesso para ler, criar, editar e excluir namespaces de identidade. |
| [!DNL Identity Management] | [!UICONTROL Exibir Namespaces De Identidade] | Acesso somente leitura para namespaces de identidade. |
| [!DNL Identity Management] | [!UICONTROL Exibir Gráfico De Identidade] | Acesso somente leitura para gráficos de identidade. |
| [!DNL Identity Management] | [!UICONTROL Gerenciar Configurações de Identidade] | Acesso para ler, criar e editar configurações de identidade. |
| [!DNL Identity Management] | [!UICONTROL Exibir Configurações De Identidade] | Acesso somente leitura às configurações de identidade. |
| [!DNL Intelligent Services] | [!UICONTROL Exibir IA de atribuição] | Acesso somente leitura para configurações e insights da IA de atribuição. |
| [!DNL Intelligent Services] | [!UICONTROL Gerenciar IA de atribuição] | Acesso para ler, criar, editar e excluir modelos de IA de atribuição. |
| [!DNL Intelligent Services] | [!UICONTROL Exibir IA do cliente] | Acesso para ler ou visualizar os modelos de IA do cliente. |
| [!DNL Intelligent Services] | [!UICONTROL Gerenciar a IA do cliente] | Acesso para criar, atualizar, excluir, ativar ou desativar modelos de IA do cliente. |
| [!DNL IP Warmup Configurations] | [!UICONTROL Exibir Planos de Warmup de IP] | Acesso somente leitura a planos de aquecimento de IP. |
| [!DNL IP Warmup Configurations] | [!UICONTROL Gerenciar Planos de Warmup de IP] | A capacidade de gerenciar planos de aquecimento de IP. |
| [!DNL IP Warmup Configurations] | [!UICONTROL Exibir Relatórios de Desvio de IP] | Acesso somente leitura a relatórios de aquecimento de IP. |
| [!DNL Journeys] | [!UICONTROL Gerenciar Jornadas] | Acesso para ler, criar, editar e excluir jornadas. |
| [!DNL Journeys] | [!UICONTROL Exibir Jornadas] | Acesso somente leitura a jornadas. |
| [!DNL Journeys] | [!UICONTROL Exibir Relatório de Jornadas] | Acesso somente leitura ao relatório do jornada. |
| [!DNL Journeys] | [!UICONTROL Gerenciar Eventos, Fontes de Dados e Ações do Jornada] | Acesso para ler, criar, editar e excluir eventos, fontes de dados ou ações. |
| [!DNL Journeys] | [!UICONTROL Exibir Eventos, Fontes de Dados e Ações do Jornada] | Acesso somente leitura a eventos, fontes de dados ou ações. |
| [!DNL Journeys] | [!UICONTROL Aprovar e publicar Jornadas] | Capacidade de aprovar e publicar jornadas quando uma política é aplicada. |
| [!DNL Journeys] | [!UICONTROL Publicar Jornadas] | Capacidade de publicar jornadas. |
| [!DNL Journey Optimizer Library] | [!UICONTROL Gerenciar itens de biblioteca] | A capacidade de adicionar e excluir expressões salvas. |
| [!DNL Journey Optimizer Library] | [!UICONTROL Publicar fragmentos] | A capacidade de publicar fragmentos de conteúdo. |
| [!DNL Journey Optimizer Library] | [!UICONTROL Simular Conteúdo] | Acesso à opção de conteúdo simular para visualização e prova. |
| [!DNL Journey Optimizer Rules] | [!UICONTROL Exibir Regras de Frequência] | Acesso somente leitura às regras de frequência. |
| [!DNL Journey Optimizer Rules] | [!UICONTROL Gerenciar Regras de Frequência] | Acesso para ler, criar, editar ou excluir regras de frequência. |
| [!DNL Messages] | [!UICONTROL Gerenciar Mensagens] | Acesso para ler, criar, editar e excluir mensagens. |
| [!DNL Messages] | [!UICONTROL Exibir Mensagens] | Acesso somente leitura a mensagens. |
| [!DNL Messages] | [!UICONTROL Exibir Relatório de Mensagens] | Acesso para ler e editar relatórios de mensagens. |
| [!DNL Messages] | [!UICONTROL Publicar Mensagens] | Capacidade de publicar mensagens. |
| [!DNL Messages] | [!UICONTROL Gerenciar Pré-visualização e Teste de Mensagens] | Capacidade de aprovar e publicar mensagens quando uma política é aplicada. |
| [!DNL Privacy Service] | [!UICONTROL Gerenciar Privacy Service] | Acesso a workflows de privacidade de leitura e gravação. |
| [!DNL Privacy Service] | [!UICONTROL Exibir Privacy Service] | Acesso somente leitura a workflows de privacidade. |
| [!DNL Profile Management] | [!UICONTROL Gerenciar perfis] | Acesso para ler, criar, editar e excluir conjuntos de dados usados para perfis de clientes. Acesso somente leitura aos perfis disponíveis. |
| [!DNL Profile Management] | [!UICONTROL Exibir Perfis] | Acesso somente leitura aos perfis disponíveis. |
| [!DNL Profile Management] | [!UICONTROL Gerenciar segmentos] | Acesso para ler, criar, editar e excluir públicos. |
| [!DNL Profile Management] | [!UICONTROL Exibir Segmentos] | Acesso somente leitura aos públicos-alvo disponíveis. |
| [!DNL Profile Management] | [!UICONTROL Gerenciar Políticas de Mesclagem] | Acesso para ler, criar, editar e excluir políticas de mesclagem. |
| [!DNL Profile Management] | [!UICONTROL Exibir Políticas de Mesclagem] | Acesso somente leitura às políticas de mesclagem disponíveis. |
| [!DNL Profile Management] | [!UICONTROL Importar públicos-alvo] | Capacidade de usar o fluxo de trabalho de upload do CSV para importar novos públicos. |
| [!DNL Profile Management] | [!UICONTROL Exportar segmento de público-alvo] | Capacidade de exportar um público avaliado para um conjunto de dados. |
| [!DNL Profile Management] | [!UICONTROL Avaliar um segmento para um público-alvo] | Capacidade de gerar perfis para um público-alvo avaliando uma definição de segmento. |
| [!DNL Profile Management] | [!UICONTROL Exibir IA B2B] | Acesso somente leitura às definições e configurações para todos os serviços de IA/ML B2B. |
| [!DNL Profile Management] | [!UICONTROL Gerenciar IA B2B] | Acesso para ler, criar, editar e excluir configurações e configurações para todos os serviços de IA/ML B2B. |
| [!DNL Profile Management] | [!UICONTROL Exibir Perfil B2B] | Acesso somente leitura a perfis de entidade B2B (como Conta, Oportunidade e assim por diante), configurações e configurações para todos os serviços de IA/ML B2B e widgets do painel B2B. |
| [!DNL Profile Management] | [!UICONTROL Gerenciar Perfil B2B] | Acesso para ler, criar, editar e excluir perfis de entidade B2B (como Conta, Oportunidade e assim por diante). Acesso somente leitura para definições e configurações para todos os serviços de IA/ML B2B e widgets do painel B2B. |
| [!DNL Profile Management] | [!UICONTROL Gerenciar Lookalikes] | Capacidade de criar ou excluir públicos-alvo semelhantes. |
| [!DNL Profile Management] | [!UICONTROL Exibir Experiência B2B] | Capacidade de exibir perfis e atributos B2B. |
| [!DNL Profile Management] | [!UICONTROL Exibir Configurações de Perfil] | Acesso somente leitura a todas as configurações do perfil. |
| [!DNL Profile Management] | [!UICONTROL Gerenciar Configurações de Perfil] | Acesso para ler e editar todas as configurações de perfil. |
| [!DNL Prospects] | [!UICONTROL Exibir Clientes Potenciais] | Acesso somente leitura a esquemas, perfis, públicos-alvo e a opção de prospecto. |
| [!DNL Prospects] | [!UICONTROL Gerenciar clientes potenciais] | Capacidade de criar e gerenciar esquemas, perfis e públicos-alvo de clientes potenciais. Acesso somente leitura à opção de cliente potencial. |
| [!DNL Query Service] | [!UICONTROL Gerenciar consultas] | Acesso para ler, criar, editar e excluir consultas SQL estruturadas para dados do Experience Platform. |
| [!DNL Query Service] | [!UICONTROL Gerenciar Integração do Serviço de Consulta] | Acesso para criar, atualizar e excluir credenciais sem expiração para acesso ao Serviço de consulta. |
| [!DNL Query Service] | [!UICONTROL Gerenciar Sessões de Consulta] | Capacidade de remover sessões existentes. |
| [!DNL Query Service] | [!UICONTROL Gerenciar Lista de permissões] | Capacidade de gerenciar restrições de IP para sua organização. |
| [!DNL Reports] | [!UICONTROL Exibir Relatórios de Canal] | A capacidade de exibir e modificar relatórios de canal. |
| [!DNL Sandbox Administration] | [!UICONTROL Gerenciar Sandboxes] | Acesso para ler, criar, editar e excluir sandboxes. |
| [!DNL Sandbox Administration] | [!UICONTROL Exibir Sandboxes] | Acesso somente leitura para sandboxes que pertencem à sua organização. |
| [!DNL Sandbox Administration] | [!UICONTROL Redefinir uma Sandbox] | Capacidade de redefinir uma sandbox. |
| [!DNL Sandbox Administration] | [!UICONTROL Gerenciar Pacotes] | Acesso para criar, importar ou exportar pacotes. |
| [!DNL Sandbox Administration] | [!UICONTROL Compartilhar Pacotes] | Acesso para compartilhar pacotes em diferentes organizações. |
| [!DNL Traits Configurations] | [!UICONTROL Exibir características] | Acesso somente leitura para características. |
| [!DNL Traits Configurations] | [!UICONTROL Gerenciar características] | Acesso para gerenciar características. |
| [!DNL Translation Service] | [!UICONTROL Gerenciar projetos de tradução] | A capacidade de gerenciar projetos de tradução. |
| [!DNL Translation Service] | [!UICONTROL Exibir Projetos De Tradução] | Acesso somente leitura a projetos de tradução. |
| [!DNL Translation Service] | [!UICONTROL Gerenciar tarefas de tradução] | A capacidade de gerenciar tarefas de tradução. |
| [!DNL Translation Service] | [!UICONTROL Exibir Tarefas de Tradução] | Acesso somente leitura a tarefas de tradução. |
| [!DNL Translation Service] | [!UICONTROL Gerenciar revisões de tradução] | A capacidade de gerenciar revisões de tradução. |
| [!DNL Translation Service] | [!UICONTROL Exibir Revisões de Tradução] | Acesso somente leitura a revisões de tradução. |
| [!DNL Translation Service] | [!UICONTROL Gerenciar tradução internamente] | A capacidade de gerenciar a tradução internamente. |
| [!DNL Translation Service] | [!UICONTROL Exibir tradução internamente] | Acesso somente leitura à tradução interna. |
| [!DNL Translation Service] | [!UICONTROL Gerenciar configurações de tradução] | A capacidade de os administradores gerenciarem configurações de tradução. |
| [!DNL Translation Service] | [!UICONTROL Gerenciar provedores de tradução] | A capacidade de gerenciar provedores de tradução. |

## Próximas etapas

Ao ler este guia, você foi apresentado aos principais princípios de controle de acesso no Experience Platform. Agora você pode continuar com o [guia do usuário de controle de acesso baseado em atributos](./abac/overview.md) para obter etapas detalhadas sobre como usar o Experience Cloud para criar funções e atribuir permissões para o Experience Platform.
