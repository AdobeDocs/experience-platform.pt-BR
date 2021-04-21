---
keywords: Experience Platform, home, tópicos populares, controle de acesso, console de administração da adobe
solution: Experience Platform
topic-legacy: overview
title: Visão geral do controle de acesso
description: O controle de acesso do Adobe Experience Platform é fornecido por meio da Adobe Admin Console. Essa funcionalidade utiliza perfis de produto no Admin Console, que vinculam usuários com permissões e sandboxes.
exl-id: 591d59ad-2784-4ae4-a509-23649ce712c9
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1181'
ht-degree: 1%

---

# Visão geral do controle de acesso

O controle de acesso para [!DNL Experience Platform] é fornecido por meio do [Adobe Admin Console](https://adminconsole.adobe.com). Essa funcionalidade utiliza perfis de produto no [!DNL Admin Console], que vincula usuários com permissões e sandboxes.

## Hierarquia e fluxo de trabalho do controle de acesso

Para configurar o controle de acesso para [!DNL Experience Platform], você deve ter privilégios de administrador para uma organização que tenha uma integração de produto [!DNL Experience Platform]. A função mínima que concede ou retira permissões é um administrador de perfil de produto. Outras funções de administrador que podem gerenciar permissões são administradores de produtos (podem gerenciar todos os perfis em um produto) e administradores de sistema (sem restrições). Consulte o artigo do Adobe Help Center sobre [funções administrativas](https://helpx.adobe.com/enterprise/using/admin-roles.html) para obter mais informações.

>[!NOTE]
>
>A partir deste ponto, qualquer menção de &quot;administrador&quot; neste documento se refere a um administrador de perfil de produto ou a uma referência superior (como descrito acima).

Um fluxo de trabalho de alto nível para obter e atribuir permissões de acesso pode ser resumido da seguinte maneira:

- Depois de licenciar o Adobe Experience Platform ou um Aplicativo/Serviço de Aplicativo que usa o Experience Platform, um email é enviado ao administrador especificado durante o licenciamento.
- O administrador faz logon no [Adobe Admin Console](#adobe-admin-console) e seleciona **Adobe Experience Platform** da lista de produtos na página de visão geral.
- O administrador pode visualizar os [perfis de produto](#product-profiles) padrão ou criar novos perfis de produto do cliente, conforme necessário.
- O administrador pode editar as permissões e os usuários para qualquer perfil de produto existente.
- Ao criar ou editar um perfil de produto, o administrador adiciona usuários ao perfil usando a guia **[!UICONTROL users]** e concede permissões a esses usuários (como &quot;[!UICONTROL Read Datasets]&quot; ou &quot;[!UICONTROL Manage Schemas]&quot;) acessando a guia **[!UICONTROL permissions]**. Da mesma forma, o administrador pode atribuir acesso às sandboxes usando a mesma guia de permissões.
- Quando os usuários fazem logon na interface do usuário [!DNL Experience Platform], o acesso aos recursos [!DNL Platform] é controlado pelas permissões que foram concedidas a eles na Etapa 2. Por exemplo, se um usuário não tiver a permissão &quot;[!UICONTROL View Datasets]&quot;, a guia **[!UICONTROL Datasets]** no menu lateral não estará visível para esse usuário.

Para obter etapas mais detalhadas sobre como gerenciar o controle de acesso em [!DNL Experience Platform], consulte o [guia do usuário de controle de acesso](./ui/overview.md).

Todas as chamadas para [!DNL Experience Platform] APIs são validadas para permissões e retornarão erros se as permissões apropriadas não forem encontradas no contexto de usuário atual. Na interface do usuário, os elementos serão ocultos ou alterados, dependendo das permissões concedidas ao usuário atual.

## Adobe Admin Console

A Adobe Admin Console fornece um local central para gerenciar direitos de produto e acesso do Adobe para sua organização. Por meio do console, você pode conceder a grupos de usuários permissões de acesso para vários recursos [!DNL Platform], como &quot;[!UICONTROL Manage Datasets]&quot;, &quot;[!UICONTROL View Datasets]&quot; ou &quot;[!UICONTROL Manage Profiles]&quot;.

### Perfis de produto

No [!DNL Admin Console], as permissões são atribuídas aos usuários por meio do uso de perfis de produto. Os perfis de produtos permitem conceder permissões a um ou vários usuários e também contêm seu acesso ao escopo das sandboxes atribuídas a eles por meio de perfis de produtos. Os usuários podem ser atribuídos a um ou vários perfis de produto pertencentes à sua organização.

### Perfis de produto padrão

[!DNL Experience Platform] O vem com dois perfis de produto padrão pré-configurados. A tabela a seguir descreve o que é fornecido em cada perfil padrão, incluindo a sandbox à qual ele concede acesso, bem como as permissões que concede dentro do escopo dessa sandbox.

| Perfil de produto | Acesso à sandbox | Permissões |
| --- | --- | --- |
| Produção padrão todo acesso | Produção | Todas as permissões aplicáveis a [!DNL Experience Platform], exceto as permissões de Administração de sandbox. |
| Administradores do Sandbox | N/D | Fornece acesso somente às permissões de Administração de sandbox. |

## Sandboxes e permissões

As sandboxes de não-produção são uma forma de virtualização de dados que permite isolar dados de outras sandboxes e geralmente são usadas para experimentos de desenvolvimento, testes ou testes. As permissões de um perfil de produto dão aos usuários do perfil acesso aos recursos [!DNL Platform] nos ambientes do sandbox aos quais eles receberam acesso. Uma licença padrão do Experience Platform concede cinco sandboxes (uma produção e quatro não produção). É possível adicionar pacotes de dez sandboxes de não produção até um máximo de 75 sandboxes no total. Entre em contato com o administrador de organização IMS ou o representante de vendas de Adobe para obter mais detalhes.

Para obter mais informações sobre sandboxes em [!DNL Experience Platform], consulte a [visão geral das sandboxes](../sandboxes/home.md).

### Acesso a sandboxes

O acesso a sandboxes é gerenciado por meio de perfis de produtos. Para obter etapas detalhadas sobre como habilitar o acesso a uma sandbox para um perfil de produto, consulte o [guia do usuário de controle de acesso](./ui/overview.md).

Os usuários podem receber acesso a uma ou mais sandboxes em um perfil de produto. Se um usuário estiver incluído em dois ou mais perfis de produto, ele terá acesso a todas as sandboxes incluídas nesses perfis.

A permissão &quot;Gerenciamento de sandbox&quot; permite que os usuários gerenciem, visualizem ou redefinam sandboxes.

### Permissões

A guia de permissões em um perfil de produto exibe as sandboxes e as permissões ativas para esse perfil:

![permissões-visão geral](./images/permissions-overview.png)

As permissões concedidas por meio do [!DNL Admin Console] são classificadas por categoria, com algumas permissões concedendo acesso a várias funcionalidades de baixo nível.

A tabela a seguir descreve as permissões disponíveis para [!DNL Experience Platform] no [!DNL Admin Console], com descrições dos recursos específicos [!DNL Platform] aos quais eles concedem acesso. Para obter etapas detalhadas sobre como adicionar permissões a um perfil de produto, consulte o [guia do usuário de controle de acesso](./ui/overview.md).

| Categoria | Permissão | Descrição |
| --- | --- | --- |
| [!DNL Data Modeling] | [!UICONTROL Manage Schemas] | Acesso para ler, criar, editar e excluir esquemas e recursos relacionados. |
| [!DNL Data Modeling] | [!UICONTROL View Schemas] | Acesso somente leitura a schemas e recursos relacionados. |
| [!DNL Data Modeling] | [!UICONTROL Manage Relationships] | Acesso para ler, criar, editar e excluir relacionamentos de esquema. |
| [!DNL Data Modeling] | [!UICONTROL Manage Identity Metadata] | Acesso para ler, criar, editar e excluir metadados de identidade de esquemas. |
| [!DNL Data Management] | [!UICONTROL Manage Datasets] | Acesso para ler, criar, editar e excluir conjuntos de dados. Acesso somente leitura para schemas. |
| [!DNL Data Management] | [!UICONTROL View Datasets] | Acesso somente leitura para conjuntos de dados e esquemas. |
| [!DNL Data Management] | [!UICONTROL Data Monitoring] | Acesso somente leitura a conjuntos de dados e fluxos de monitoramento. |
| [!DNL Profile Management] | [!UICONTROL Manage Profiles] | Acesso para ler, criar, editar e excluir conjuntos de dados usados para perfis do cliente. Acesso somente leitura a perfis disponíveis. |
| [!DNL Profile Management] | [!UICONTROL View Profiles] | Acesso somente leitura a perfis disponíveis. |
| [!DNL Profile Management] | [!UICONTROL Manage Segments] | Acesso para ler, criar, editar e excluir segmentos. |
| [!DNL Profile Management] | [!UICONTROL View Segments] | Acesso somente leitura aos segmentos disponíveis. |
| [!DNL Profile Management] | [!UICONTROL Manage Merge Policies] | Acesso para ler, criar, editar e excluir políticas de mesclagem. |
| [!DNL Profile Management] | [!UICONTROL View Merge Policies] | Acesso somente leitura às políticas de mesclagem disponíveis. |
| [!DNL Profile Management] | [!UICONTROL Export Audience for Segment] | Capacidade de exportar um segmento de público-alvo avaliado para um conjunto de dados. |
| [!DNL Profile Management] | [!UICONTROL Evaluate a Segment to an Audience] | Capacidade de gerar perfis para um público-alvo avaliando uma definição de segmento. |
| [!DNL Identities] | [!UICONTROL Manage Identity Namespaces] | Acesso para ler, criar, editar e excluir namespaces de identidade. |
| [!DNL Identities] | [!UICONTROL View Identity Namespaces] | Acesso somente leitura para namespaces de identidade. |
| [!DNL Sandbox Administration] | [!UICONTROL Manage Sandboxes] | Acesso para ler, criar, editar e excluir sandboxes. |
| [!DNL Sandbox Administration] | [!UICONTROL View Sandboxes] | Acesso somente leitura para sandboxes pertencentes à sua organização. |
| [!DNL Sandbox Administration] | [!UICONTROL Reset a Sandbox] | Capacidade de redefinir uma sandbox. |
| [!DNL Destinations] | [!UICONTROL Manage Destinations] | Acesso para ler, criar, editar e desativar destinos. |
| [!DNL Destinations] | [!UICONTROL View Destinations] | Acesso somente leitura a destinos disponíveis na guia **[!UICONTROL Catalog]** e destinos autenticados na guia **[!UICONTROL Browse]**. |
| [!DNL Destinations] | [!UICONTROL Activate Destinations] | Capacidade de ativar dados para destinos ativos que foram criados. Essa permissão requer que &quot;Exibir destinos&quot; ou &quot;Gerenciar [!UICONTROL Destinations”]&quot; sejam concedidas ao usuário que ativará destinos. |
| [!DNL Data Ingestion] | [!UICONTROL Manage Sources] | Acesso para ler, criar, editar e desativar fontes. |
| [!DNL Data Ingestion] | [!UICONTROL View Sources] | Acesso somente leitura a fontes disponíveis na guia **[!UICONTROL Catalog]** e fontes autenticadas na guia **[!UICONTROL Browse]**. |
| [!DNL Data Science Workspace] | [!UICONTROL Manage Data Science Workspace] | Acesso para ler, criar, editar e excluir em [!DNL Data Science Workspace]. |
| [!DNL Data Governance] | [!UICONTROL Apply Data Usage Labels] | Acesso para ler, criar e excluir rótulos de uso. |
| [!DNL Data Governance] | [!UICONTROL Manage Data Usage Policies] | Acesso para ler, criar, editar e excluir políticas de uso de dados. |
| [!DNL Data Governance] | [!UICONTROL View Data Usage Policies] | Acesso somente leitura para políticas de uso de dados pertencentes à sua organização. |
| [!DNL Query Service] | [!UICONTROL Manage Queries] | Acesso para ler, criar, editar e excluir consultas SQL estruturadas para dados da plataforma. |

## Próximas etapas

Ao ler este guia, você foi apresentado aos principais princípios do controle de acesso em [!DNL Experience Platform]. Agora você pode continuar para o [guia do usuário de controle de acesso](./ui/overview.md) para obter etapas detalhadas sobre como usar o [!DNL Admin Console] para criar perfis de produto e atribuir permissões para [!DNL Platform].
