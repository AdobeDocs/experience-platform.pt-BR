---
keywords: Experience Platform;página inicial;tópicos populares;controle de acesso;adobe admin console
solution: Experience Platform
title: Visão geral do controle de acesso
description: O controle de acesso do Adobe Experience Platform é fornecido por meio da Adobe Admin Console. Essa funcionalidade aproveita perfis de produto no Admin Console, que vinculam usuários com permissões e sandboxes.
exl-id: 591d59ad-2784-4ae4-a509-23649ce712c9
source-git-commit: 16313e2109152329a427be9f13fcbd6382353797
workflow-type: tm+mt
source-wordcount: '1718'
ht-degree: 1%

---

# Visão geral do controle de acesso

O controle de acesso do Adobe Experience Platform é fornecido por meio da **[!UICONTROL Permissões]** in [Adobe Experience Cloud](https://experience.adobe.com/). Essa funcionalidade aproveita funções e políticas, que vinculam usuários com permissões e sandboxes.

## Hierarquia e fluxo de trabalho do controle de acesso

Para configurar o controle de acesso para o Experience Platform, você deve ter privilégios de administrador de sistema ou de produto para uma organização que tenha um produto Experience Platform. A função mínima que pode conceder ou retirar permissões é um administrador de produto. Outras funções de administrador que podem gerenciar permissões são administradores do sistema (sem restrições). Consulte o artigo da Adobe Help Center sobre [funções administrativas](https://helpx.adobe.com/br/enterprise/using/admin-roles.html) para obter mais informações.

>[!NOTE]
>
>A partir deste ponto, qualquer menção a &quot;administrador&quot; neste documento se refere a um administrador de produto ou superior (conforme descrito acima).

Um workflow de alto nível para obter e atribuir permissões de acesso pode ser resumido da seguinte maneira:

- Após licenciar o Adobe Experience Platform ou um Serviço de aplicativo/aplicativo que use o Experience Platform, um email é enviado ao administrador especificado durante o licenciamento.
- O administrador faz logon no [Adobe Admin Console](#adobe-admin-console) e seleciona **Adobe Experience Platform** na lista de produtos na página visão geral.
- Para conceder acesso ao Experience Platform, é recomendável que o administrador adicione usuários ao perfil de produto padrão: `AEP-Default-All-Users`.
- Nas Permissões do Experience Platform, o administrador pode criar novas funções ou editar as permissões e os usuários de qualquer função existente.
- Ao criar ou editar uma função, o administrador adiciona usuários à função usando o **[!UICONTROL usuários]** e concede permissões a esses usuários (como &quot;[!UICONTROL Ler conjuntos de dados]&quot; ou &quot;[!UICONTROL Gerenciar esquemas]&quot;) editando as permissões da função. Da mesma forma, o administrador pode atribuir acesso a sandboxes usando a mesma opção de edição.
- Quando os usuários fazem logon na interface do usuário do Experience Platform, o acesso aos recursos do Experience Platform é orientado pelas permissões concedidas a eles na etapa anterior. Por exemplo, se um usuário não tiver o [!UICONTROL Exibir conjuntos de dados] permissão, a variável **[!UICONTROL Conjuntos de dados]** no menu lateral não estará visível para esse usuário.

Para obter etapas mais detalhadas sobre como gerenciar o controle de acesso no Experience Platform, consulte [guia do usuário de controle de acesso](./ui/overview.md).

Todas as chamadas para APIs Experience Platform são validadas em relação a permissões e retornarão erros se as permissões apropriadas não forem encontradas no contexto do usuário atual. Na interface do usuário, os elementos serão ocultos ou alterados dependendo das permissões concedidas ao usuário atual.

## Permissões {#platform-permissions}

[!UICONTROL Permissões] O fornece um local central para gerenciar o acesso ao Experience Platform para sua organização. Até [!UICONTROL Permissões], você pode conceder a grupos de usuários permissões de acesso para vários recursos do Experience Platform, como [!UICONTROL Gerenciar conjuntos de dados], [!UICONTROL Exibir conjuntos de dados]ou [!UICONTROL Gerenciar perfis].

### Funções

No [!UICONTROL Funções] , as permissões são atribuídas aos usuários por meio do uso de funções. As funções permitem conceder permissões a um ou vários usuários e também contêm acesso ao escopo das sandboxes atribuídas a eles por meio de funções. Os usuários podem ser atribuídos a uma ou várias funções pertencentes à sua organização.

### Funções padrão

O Experience Platform vem com duas funções padrão pré-configuradas. A tabela a seguir descreve o que é fornecido em cada perfil padrão, incluindo a sandbox à qual eles concedem acesso, bem como as permissões que concedem no escopo dessa sandbox.

| Função | Acesso à sandbox | Permissões |
| --- | --- | --- |
| Acesso total à produção padrão | Produção | Todas as permissões aplicáveis ao Experience Platform, exceto as permissões de Administração de sandbox. |
| Administradores de sandbox | N/D | Fornece acesso somente a permissões de Administração de sandbox. |

## Sandboxes e permissões

As sandboxes de não produção são uma forma de virtualização de dados que permitem isolar dados de outras sandboxes e são normalmente usadas para experimentos de desenvolvimento, testes ou avaliações. As permissões de uma função concedem aos usuários da função acesso aos recursos de Experience Platform nos ambientes de sandbox aos quais eles receberam acesso. Uma licença de Experience Platform padrão concede cinco sandboxes (uma de produção e quatro de não produção). Você pode adicionar pacotes de dez sandboxes de não produção até um máximo de 75 sandboxes no total. Entre em contato com o administrador da organização ou com o representante de vendas da Adobe para obter mais detalhes.

Para obter mais informações sobre sandboxes no Experience Platform, consulte o [visão geral das sandboxes](../sandboxes/home.md).

### Acesso a sandboxes

O acesso a sandboxes é gerenciado por meio de funções. Para obter etapas detalhadas sobre como habilitar o acesso a uma sandbox para uma função, consulte o [guia de funções de controle de acesso baseado em atributo](./abac/ui/roles.md).

É possível conceder aos usuários acesso a uma ou mais sandboxes em uma função. Se um usuário estiver incluído em duas ou mais funções, ele terá acesso a todas as sandboxes incluídas nessas funções.

A permissão &quot;Gerenciamento de sandbox&quot; permite que os usuários gerenciem, visualizem ou redefinam sandboxes.

### Permissões de recurso {#permissions}

O recurso [!UICONTROL Permissões] em uma função exibe as sandboxes e permissões que estão ativas para essa função:

![permissões-visão geral](./images/permissions.png)

As permissões concedidas por meio das permissões de recurso são classificadas por categoria, com algumas permissões que concedem acesso a várias funcionalidades de baixo nível.

A tabela a seguir descreve as permissões disponíveis para Experience Platform na função, com descrições dos recursos de Experience Platform específicos aos quais eles concedem acesso. Para obter etapas detalhadas sobre como adicionar permissões a uma função, consulte o [guia de funções de controle de acesso baseado em atributo](./abac/ui/roles.md).

| Categoria | Permissão | Descrição |
| --- | --- | --- |
| [!DNL Alerts] | [!UICONTROL Exibir histórico de alertas] | Acesso somente leitura para o histórico de alertas. |
| [!DNL Alerts] | [!UICONTROL Resolver alertas] | Acesso para ler, editar e excluir alertas. |
| [!DNL Alerts] | [!UICONTROL Exibir alertas] | Acesso somente leitura para alertas. |
| [!DNL Alerts] | [!UICONTROL Gerenciar alertas] | Acesso para ler, criar, editar e excluir o histórico de alertas. |
| [!DNL Computed Attributes] | [!UICONTROL Exibir atributos computados] | Acesso somente leitura para a guia de atributos calculados, inventário e detalhes. |
| [!DNL Computed Attributes] | [!UICONTROL Gerenciar atributos computados] | Acesso para ler, criar, excluir rascunhos e desativar atributos calculados. |
| [!DNL Data Lifecycle] | [!UICONTROL Exibir ciclo de vida dos dados] | Acesso somente leitura para o ciclo de vida dos dados. |
| [!DNL Data Lifecycle] | [!UICONTROL Gerenciar o ciclo de vida dos dados] | Acesso para ler, criar, editar e excluir o ciclo de vida dos dados. |
| [!DNL Data Modeling] | [!UICONTROL Gerenciar esquemas] | Acesso para ler, criar, editar e excluir esquemas e recursos relacionados. |
| [!DNL Data Modeling] | [!UICONTROL Exibir esquemas] | Acesso somente leitura a esquemas e recursos relacionados. |
| [!DNL Data Modeling] | [!UICONTROL Gerenciar relacionamentos] | Acesso para ler, criar, editar e excluir relacionamentos de esquema. |
| [!DNL Data Modeling] | [!UICONTROL Gerenciar metadados de identidade] | Acesso para ler, criar, editar e excluir metadados de identidade de esquemas. |
| [!DNL Data Management] | [!UICONTROL Gerenciar conjuntos de dados] | Acesso para ler, criar, editar e excluir conjuntos de dados. Acesso somente leitura para esquemas. |
| [!DNL Data Management] | [!UICONTROL Exibir conjuntos de dados] | Acesso somente leitura para conjuntos de dados e esquemas. |
| [!DNL Data Management] | [!UICONTROL Monitoramento de dados] | Acesso somente leitura a conjuntos de dados e fluxos de monitoramento. |
| [!DNL Profile Management] | [!UICONTROL Gerenciar perfis] | Acesso para ler, criar, editar e excluir conjuntos de dados usados para perfis de clientes. Acesso somente leitura aos perfis disponíveis. |
| [!DNL Profile Management] | [!UICONTROL Exibir perfis] | Acesso somente leitura aos perfis disponíveis. |
| [!DNL Profile Management] | [!UICONTROL Gerenciar segmentos] | Acesso para ler, criar, editar e excluir segmentos. |
| [!DNL Profile Management] | [!UICONTROL Exibir segmentos] | Acesso somente leitura aos segmentos disponíveis. |
| [!DNL Profile Management] | [!UICONTROL Gerenciar políticas de mesclagem] | Acesso para ler, criar, editar e excluir políticas de mesclagem. |
| [!DNL Profile Management] | [!UICONTROL Exibir Políticas de Mesclagem] | Acesso somente leitura às políticas de mesclagem disponíveis. |
| [!DNL Profile Management] | [!UICONTROL Importar públicos] | Acesso para ler, criar, editar e excluir públicos importados. |
| [!DNL Profile Management] | [!UICONTROL Exportar público-alvo para segmento] | Capacidade de exportar um segmento de público avaliado para um conjunto de dados. |
| [!DNL Profile Management] | [!UICONTROL Avaliar um segmento para um público-alvo] | Capacidade de gerar perfis para um público-alvo avaliando uma definição de segmento. |
| [!DNL Profile Management] | [!UICONTROL Exibir IA B2B] | Acesso somente leitura às definições e configurações para todos os serviços de IA/ML B2B. |
| [!DNL Profile Management] | [!UICONTROL Gerenciar IA B2B] | Acesso para ler, criar, editar e excluir configurações e configurações para todos os serviços de IA/ML B2B. |
| [!DNL Profile Management] | [!UICONTROL Exibir perfil B2B] | Acesso somente leitura a perfis de entidade B2B (como Conta, Oportunidade e assim por diante), configurações e configurações para todos os serviços de IA/ML B2B e widgets do painel B2B. |
| [!DNL Profile Management] | [!UICONTROL Gerenciar perfil B2B] | Acesso para ler, criar, editar e excluir perfis de entidade B2B (como Conta, Oportunidade e assim por diante). Acesso somente leitura para definições e configurações para todos os serviços de IA/ML B2B e widgets do painel B2B. |
| [!DNL Identity Management] | [!UICONTROL Gerenciar namespaces de identidade] | Acesso para ler, criar, editar e excluir namespaces de identidade. |
| [!DNL Identity Management] | [!UICONTROL Exibir namespaces de identidade] | Acesso somente leitura para namespaces de identidade. |
| [!DNL Identity Management] | [!UICONTROL Exibir gráfico de identidade] | Acesso somente leitura para gráficos de identidade. |
| [!DNL Sandbox Administration] | [!UICONTROL Gerenciar sandboxes] | Acesso para ler, criar, editar e excluir sandboxes. |
| [!DNL Sandbox Administration] | [!UICONTROL Exibir sandboxes] | Acesso somente leitura para sandboxes que pertencem à sua organização. |
| [!DNL Sandbox Administration] | [!UICONTROL Redefinir uma sandbox] | Capacidade de redefinir uma sandbox. |
| [!DNL Destinations] | [!UICONTROL Exibir destinos] | Acesso somente leitura para visualizar os destinos disponíveis na **[!UICONTROL Catálogo]** e destinos autenticados na **[!UICONTROL Procurar]** guia. |
| [!DNL Destinations] | [!UICONTROL Gerenciar destinos] | Acesso para ler, criar e excluir conexões e contas de destino. |
| [!DNL Destinations] | [!UICONTROL Ativar destinos] | Oferece aos usuários a capacidade de ativar segmentos para destinos existentes. Ativa a etapa de mapeamento no fluxo de trabalho de ativação. Essa permissão também exige que o [!UICONTROL Exibir destinos] permissão a ser concedida ao usuário que ativará os dados para destinos. |
| [!DNL Destinations] | [!UICONTROL Ativar segmento sem mapeamento] | Oferece aos usuários a capacidade de ativar segmentos para destinos existentes, sem exibir a [etapa de mapeamento](../destinations/ui/activate-batch-profile-destinations.md#mapping). Os usuários podem adicionar e remover segmentos em workflows de ativação, mas não podem adicionar ou remover atributos ou identidades mapeadas. Essa permissão também exige que o [!UICONTROL Exibir destinos] permissão a ser concedida ao usuário que ativará os dados para destinos. |
| [!DNL Destinations] | [!UICONTROL Gerenciar e ativar destinos do conjunto de dados] | Capacidade de ler, criar, editar e desativar fluxos de exportação do conjunto de dados. Capacidade de também ativar dados para conjuntos de dados ativos que foram criados. Essa permissão também exige que o [!UICONTROL Exibir destinos] permissão a ser concedida ao usuário que ativará os dados para destinos. |
| [!DNL Destinations] | [!UICONTROL Criação de destino] | Capacidade de criar destinos usando [Adobe Experience Platform Destination SDK](../destinations/destination-sdk/overview.md). |
| [!DNL Data Ingestion] | [!UICONTROL Gerenciar fontes] | Acesso para ler, criar, editar e desativar fontes. |
| [!DNL Data Ingestion] | [!UICONTROL Exibir fontes] | Acesso somente leitura a fontes disponíveis na **[!UICONTROL Catálogo]** e fontes autenticadas na **[!UICONTROL Procurar]** guia. |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share Connections] | Acesso para criar, aceitar e recusar handshakes de parceiros para conectar duas organizações e habilitar [!DNL Segment Match] fluxos. |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share] | Acesso para ler, criar, editar e publicar [!DNL Segment Match] Feeds com parceiros ativos. |
| [!DNL Data Science Workspace] | [!UICONTROL Gerenciar o Espaço de trabalho de ciência de dados] | Acesso para ler, criar, editar e excluir no [!DNL Data Science Workspace]. |
| Governança de dados | [!UICONTROL Gerenciar rótulos de uso] | Acesso para ler, criar e excluir rótulos de uso. |
| Governança de dados | [!UICONTROL Gerenciar políticas de uso de dados] | Acesso para ler, criar, editar e excluir políticas de uso de dados. |
| Governança de dados | [!UICONTROL Exibir políticas de uso de dados] | Acesso somente leitura para políticas de uso de dados pertencentes à sua organização. |
| Governança de dados | [!UICONTROL Exibir log de atividades do usuário] | Acesso somente leitura para visualização registrada [logs de auditoria](../landing/governance-privacy-security/audit-logs/overview.md) das atividades da Platform. |
| [!DNL Dashboards] | [!UICONTROL Exibir Painel de Uso da Licença] | Acesso somente leitura para exibir o painel de uso de licença. |
| [!DNL Dashboards] | [!UICONTROL Gerenciar painéis padrão] | Adicione atributos personalizados que ainda não estão no data warehouse. |
| [!DNL Query Service] | [!UICONTROL Gerenciar consultas] | Acesso para ler, criar, editar e excluir consultas SQL estruturadas para dados da Platform. |
| [!DNL Query Service] | [!UICONTROL Gerenciar Integração do Serviço de Consulta] | Acesso para criar, atualizar e excluir credenciais sem expiração para acesso ao Serviço de consulta. |

## Próximas etapas

Ao ler este guia, você foi apresentado aos principais princípios de controle de acesso no Experience Platform. Agora você pode continuar com a [guia do usuário de controle de acesso baseado em atributo](./abac/overview.md) para obter etapas detalhadas sobre como usar o Experience Cloud para criar funções e atribuir permissões para o Experience Platform.
