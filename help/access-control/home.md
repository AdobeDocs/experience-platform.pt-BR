---
keywords: Experience Platform, home, tópicos populares, controle de acesso, console de administração da adobe
solution: Experience Platform
topic-legacy: overview
title: Visão geral do controle de acesso
description: O controle de acesso do Adobe Experience Platform é fornecido por meio da Adobe Admin Console. Essa funcionalidade utiliza perfis de produto no Admin Console, que vinculam usuários com permissões e sandboxes.
exl-id: 591d59ad-2784-4ae4-a509-23649ce712c9
source-git-commit: 36aaccddeb207e22a22d5124ec8592ac8dddf8bc
workflow-type: tm+mt
source-wordcount: '1307'
ht-degree: 2%

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
- Ao criar ou editar um perfil de produto, o administrador adiciona usuários ao perfil usando a guia **[!UICONTROL users]** e concede permissões a esses usuários (como &quot;[!UICONTROL Ler conjuntos de dados]&quot; ou &quot;[!UICONTROL Gerenciar esquemas]&quot;) acessando a guia **[!UICONTROL permissions]**. Da mesma forma, o administrador pode atribuir acesso às sandboxes usando a mesma guia de permissões.
- Quando os usuários fazem logon na interface do usuário [!DNL Experience Platform], o acesso aos recursos [!DNL Platform] é controlado pelas permissões que foram concedidas a eles na Etapa 2. Por exemplo, se um usuário não tiver a permissão &quot;[!UICONTROL Exibir Conjuntos de Dados]&quot;, a guia **[!UICONTROL Conjuntos de Dados]** no menu lateral não estará visível para esse usuário.

Para obter etapas mais detalhadas sobre como gerenciar o controle de acesso em [!DNL Experience Platform], consulte o [guia do usuário de controle de acesso](./ui/overview.md).

Todas as chamadas para [!DNL Experience Platform] APIs são validadas para permissões e retornarão erros se as permissões apropriadas não forem encontradas no contexto de usuário atual. Na interface do usuário, os elementos serão ocultos ou alterados, dependendo das permissões concedidas ao usuário atual.

## Adobe Admin Console

A Adobe Admin Console fornece um local central para gerenciar direitos de produto e acesso do Adobe para sua organização. Por meio do console, você pode conceder a grupos de usuários permissões de acesso para vários recursos [!DNL Platform], como &quot;[!UICONTROL Gerenciar conjuntos de dados]&quot;, &quot;[!UICONTROL Exibir conjuntos de dados]&quot; ou &quot;[!UICONTROL Gerenciar perfis]&quot;.

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
| [!DNL Data Modeling] | [!UICONTROL Gerenciar esquemas] | Acesso para ler, criar, editar e excluir esquemas e recursos relacionados. |
| [!DNL Data Modeling] | [!UICONTROL Visualizar esquemas] | Acesso somente leitura a schemas e recursos relacionados. |
| [!DNL Data Modeling] | [!UICONTROL Gerenciar Relacionamentos] | Acesso para ler, criar, editar e excluir relacionamentos de esquema. |
| [!DNL Data Modeling] | [!UICONTROL Gerenciar metadados de identidade] | Acesso para ler, criar, editar e excluir metadados de identidade de esquemas. |
| [!DNL Data Management] | [!UICONTROL Gerenciar conjuntos de dados] | Acesso para ler, criar, editar e excluir conjuntos de dados. Acesso somente leitura para schemas. |
| [!DNL Data Management] | [!UICONTROL Visualizar conjuntos de dados] | Acesso somente leitura para conjuntos de dados e esquemas. |
| [!DNL Data Management] | [!UICONTROL Monitoramento de dados] | Acesso somente leitura a conjuntos de dados e fluxos de monitoramento. |
| [!DNL Profile Management] | [!UICONTROL Gerenciar perfis] | Acesso para ler, criar, editar e excluir conjuntos de dados usados para perfis do cliente. Acesso somente leitura a perfis disponíveis. |
| [!DNL Profile Management] | [!UICONTROL Exibir perfis] | Acesso somente leitura a perfis disponíveis. |
| [!DNL Profile Management] | [!UICONTROL Gerenciar segmentos] | Acesso para ler, criar, editar e excluir segmentos. |
| [!DNL Profile Management] | [!UICONTROL Exibir segmentos] | Acesso somente leitura aos segmentos disponíveis. |
| [!DNL Profile Management] | [!UICONTROL Gerenciar políticas de mesclagem] | Acesso para ler, criar, editar e excluir políticas de mesclagem. |
| [!DNL Profile Management] | [!UICONTROL Exibir Políticas de Mesclagem] | Acesso somente leitura às políticas de mesclagem disponíveis. |
| [!DNL Profile Management] | [!UICONTROL Exportar público-alvo para segmento] | Capacidade de exportar um segmento de público-alvo avaliado para um conjunto de dados. |
| [!DNL Profile Management] | [!UICONTROL Avaliar um segmento para um público-alvo] | Capacidade de gerar perfis para um público-alvo avaliando uma definição de segmento. |
| [!DNL Identities] | [!UICONTROL Gerenciar namespaces de identidade] | Acesso para ler, criar, editar e excluir namespaces de identidade. |
| [!DNL Identities] | [!UICONTROL Exibir namespaces de identidade] | Acesso somente leitura para namespaces de identidade. |
| [!DNL Sandbox Administration] | [!UICONTROL Gerenciar sandboxes] | Acesso para ler, criar, editar e excluir sandboxes. |
| [!DNL Sandbox Administration] | [!UICONTROL Visualizar sandboxes] | Acesso somente leitura para sandboxes pertencentes à sua organização. |
| [!DNL Sandbox Administration] | [!UICONTROL Redefinir uma sandbox] | Capacidade de redefinir uma sandbox. |
| [!DNL Destinations] | [!UICONTROL Gerenciar destinos] | Acesso para ler, criar, editar e desativar destinos. |
| [!DNL Destinations] | [!UICONTROL Exibir destinos] | Acesso somente leitura aos destinos disponíveis na guia **[!UICONTROL Catálogo]** e destinos autenticados na guia **[!UICONTROL Procurar]**. |
| [!DNL Destinations] | [!UICONTROL Ativar destinos] | Capacidade de ativar dados para destinos ativos que foram criados. Essa permissão requer que &quot;Exibir destinos&quot; ou &quot;Gerenciar [!UICONTROL Destinos&quot;] seja concedida ao usuário que ativará destinos. |
| [!DNL Data Ingestion] | [!UICONTROL Gerenciar fontes] | Acesso para ler, criar, editar e desativar fontes. |
| [!DNL Data Ingestion] | [!UICONTROL Exibir fontes] | Acesso somente leitura a fontes disponíveis na guia **[!UICONTROL Catálogo]** e fontes autenticadas na guia **[!UICONTROL Procurar]**. |
| [!DNL Data Science Workspace] | [!UICONTROL Gerenciar o Data Science Workspace] | Acesso para ler, criar, editar e excluir em [!DNL Data Science Workspace]. |
| [!DNL Data Governance] | [!UICONTROL Aplicar rótulos de uso de dados] | Acesso para ler, criar e excluir rótulos de uso. |
| [!DNL Data Governance] | [!UICONTROL Gerenciar políticas de uso de dados] | Acesso para ler, criar, editar e excluir políticas de uso de dados. |
| [!DNL Data Governance] | [!UICONTROL Exibir políticas de uso de dados] | Acesso somente leitura para políticas de uso de dados pertencentes à sua organização. |
| [!DNL Dashboards] | [!UICONTROL Exibir painel de uso de licença] | Acesso somente leitura para exibir o painel de uso da licença. |
| [!DNL Dashboards] | [!UICONTROL Gerenciar painéis padrão] | Adicione atributos personalizados que ainda não estão no data warehouse. |
| [!DNL Query Service] | [!UICONTROL Gerenciar Consultas] | Acesso para ler, criar, editar e excluir consultas SQL estruturadas para dados da plataforma. |

## Próximas etapas

Ao ler este guia, você foi apresentado aos principais princípios do controle de acesso em [!DNL Experience Platform]. Agora você pode continuar para o [guia do usuário de controle de acesso](./ui/overview.md) para obter etapas detalhadas sobre como usar o [!DNL Admin Console] para criar perfis de produto e atribuir permissões para [!DNL Platform].
