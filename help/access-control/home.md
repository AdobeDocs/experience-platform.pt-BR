---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Visão geral do Controle de acesso
topic: overview
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '1177'
ht-degree: 4%

---


# Visão geral do Controle de acesso

O Controle de acesso for Experience Platform é fornecido por meio do [Adobe Admin Console](https://adminconsole.adobe.com). Essa funcionalidade aproveita perfis de produtos no Admin Console, que vinculam usuários com permissões e caixas de proteção.

## Hierarquia de Controles de acesso e fluxo de trabalho

Para configurar o controle de acesso para o Experience Platform, você deve ter privilégios de administrador para uma organização que tenha uma integração de produto Experience Platform. A função mínima que concede ou retira permissões é um administrador **de perfil de** produto. Outras funções de administrador que podem gerenciar permissões são administradores **de** produtos (podem gerenciar todos os perfis em um produto) e administradores **de** sistema (sem restrições). Consulte o artigo da Central de ajuda da Adobe sobre funções [](https://helpx.adobe.com/enterprise/using/admin-roles.html) administrativas para obter mais informações.

>[!NOTE]
>
>A partir desse ponto, quaisquer menções de &quot;administrador&quot; neste documento se referem a um administrador do perfil do produto ou a uma versão superior (conforme descrito acima).

Um fluxo de trabalho de alto nível para obter e atribuir permissões de acesso pode ser resumido da seguinte forma:

- Após a inscrição no Adobe Experience Platform, um email é enviado para o administrador especificado no formulário de inscrição.
- O administrador faz logon no [Adobe Admin Console](#adobe-admin-console) e seleciona **Adobe Experience Platform** na lista de produtos na página de visão geral.
- O administrador pode visualização os perfis [de](#product-profiles) produtos padrão ou criar novos perfis de produtos do cliente, conforme necessário.
- O administrador pode editar as permissões e os usuários de qualquer perfil de produto existente.
- Ao criar ou editar um perfil de produto, o administrador adiciona usuários ao perfil usando a guia **usuários** e concede permissões a esses usuários (como &quot;Ler conjuntos de dados&quot; ou &quot;Gerenciar Schemas&quot;) acessando a guia **permissões** . Da mesma forma, o administrador pode atribuir acesso a caixas de proteção usando a mesma guia de permissões.
- Quando os usuários fazem logon na interface do usuário do Experience Platform, seu acesso aos recursos do Platform é determinado pelas permissões que lhes foram concedidas na Etapa 2. Por exemplo, se um usuário não tiver a permissão &quot;Conjuntos de dados de Visualização&quot;, a guia *Conjuntos* de dados no menu lateral não estará visível para esse usuário.

Para obter etapas mais detalhadas sobre como gerenciar o controle de acesso, consulte o guia [do usuário do](./ui/overview.md)controle de acesso.

Todas as chamadas para APIs de Experience Platform são validadas para permissões e retornarão erros se as permissões apropriadas não forem encontradas no contexto do usuário atual. Na interface do usuário, os elementos serão omitidos ou alterados, dependendo das permissões concedidas ao usuário atual.

## Adobe Admin Console

A Adobe Admin Console fornece um local central para gerenciar os direitos e o acesso dos produtos da Adobe para sua organização. Por meio do console, você pode conceder a grupos de usuários permissões de acesso para vários recursos do Platform, como &quot;Gerenciar conjuntos de dados&quot;, &quot;Conjuntos de dados de Visualização&quot; ou &quot;Gerenciar Perfis&quot;.

### perfis de produtos

No Admin Console, as permissões são atribuídas aos usuários por meio do uso de perfis **de** produtos. Os perfis de produtos permitem que você conceda permissões a um ou vários usuários e também contêm seu acesso ao escopo das caixas de proteção que lhes são atribuídas por meio de perfis de produtos. Os usuários podem ser atribuídos a um ou vários perfis de produtos pertencentes à sua organização.

### perfis de produtos padrão

O Experience Platform vem com dois perfis de produto padrão pré-configurados. A tabela a seguir descreve o que é fornecido em cada perfil padrão, incluindo a caixa de proteção à qual eles concedem acesso, bem como as permissões que eles concedem dentro do escopo dessa caixa de proteção.

| Perfil de produto | Acesso à caixa de proteção | Permissões |
| --- | --- | --- |
| Produção padrão - Todos os acessos | Produção | Todas as permissões aplicáveis ao Experience Platform, exceto as permissões de Administração da caixa de proteção. |
| Administração padrão de sandbox | N/D | Fornece acesso somente às permissões de Administração da caixa de proteção. |

## Caixas de proteção e permissões

O Experience Platform fornece acesso a uma caixa de proteção de produção e permite criar **caixas de proteção** de não produção. As caixas de proteção de não-produção são uma forma de virtualização de dados que permite isolar dados de outras caixas de proteção e geralmente são usadas para experimentos de desenvolvimento, testes ou testes. As **permissões** de um perfil de produto concedem aos usuários do perfil acesso aos recursos do Platform dentro dos ambientes da caixa de proteção aos quais eles receberam acesso.

Para obter mais informações sobre caixas de proteção no Experience Platform, consulte a visão geral [das](../sandboxes/home.md)caixas de proteção.

### Acesso a caixas de proteção

O acesso às caixas de proteção é gerenciado por meio de perfis de produtos. Para obter etapas detalhadas sobre como ativar o acesso a uma caixa de proteção para um perfil de produto, consulte o guia [do usuário do](./ui/overview.md)controle de acesso.

Os usuários podem receber acesso a uma ou mais caixas de proteção em um perfil de produto. Se um usuário estiver incluído em dois ou mais perfis de produtos, ele terá acesso a todas as caixas de proteção incluídas nesses perfis.

A permissão &quot;Gerenciamento de sandbox&quot; permite que os usuários gerenciem, visualizações ou redefinam caixas de proteção.

### Permissões

A guia **Permissões** em um perfil de produto exibe as caixas de proteção e as permissões que estão ativas para esse perfil:

![](./images/permissions-overview.png)

As permissões que são concedidas por meio do Admin Console são classificadas por categoria, com algumas permissões concedendo acesso a várias funcionalidades de baixo nível.

A tabela a seguir descreve as permissões disponíveis para o Experience Platform no Admin Console, com descrições dos recursos específicos do Platform aos quais eles concedem acesso. Para obter etapas detalhadas sobre como adicionar permissões a um perfil de produto, consulte o guia [do usuário do](./ui/overview.md)controle de acesso.

| Categoria | Permissão | Descrição |
| --- | --- | --- |
| Modelagem de dados | Gerenciar Schemas | Acesso para ler, criar, editar e excluir schemas e recursos relacionados. |
| Modelagem de dados | Visualizar esquemas | Acesso somente leitura a schemas e recursos relacionados. |
| Gestão de Dados | Gerenciar conjuntos de dados | Acesso para ler, criar, editar e excluir conjuntos de dados. Acesso somente leitura para schemas. |
| Gestão de Dados | Visualizar conjuntos de dados | Acesso somente leitura para conjuntos de dados e schemas. |
| Gestão de Dados | Monitoramento de dados | Acesso somente leitura a conjuntos de dados e fluxos de monitoramento. |
| Gerenciamento de Perfis | Gerenciar Perfis | Acesso para ler, criar, editar e excluir conjuntos de dados usados para perfis do cliente. Acesso somente leitura aos perfis disponíveis. |
| Gerenciamento de Perfis | Perfis Visualizações | Acesso somente leitura aos perfis disponíveis. |
| Gerenciamento de Perfis | Exportar Audiência para segmento | Capacidade de exportar um segmento de audiência avaliado para um conjunto de dados. |
| Identidades | Gerenciar namespaces de identidade | Acesso para ler, criar, editar e excluir namespaces de identidade. |
| Identidades | Namespaces de identidade de Visualização | Acesso somente leitura para namespaces de identidade. |
| Administração de sandbox | Gerenciar caixas de proteção | Acesso para ler, criar, editar e excluir caixas de proteção. |
| Administração de sandbox | Visualizar sandboxes | Acesso somente leitura para caixas de proteção pertencentes à sua organização. |
| Administração de sandbox | Redefinir uma caixa de proteção | Capacidade de reiniciar uma caixa de proteção. |
| Destinos | Gerenciar destinos | Acesso para ler, criar, editar e desativar destinos.* |
| Destinos | Destinos da Visualização | Acesso somente leitura para destinos disponíveis na guia *Catálogo* e destinos autenticados na guia *Procurar* .* |
| Destinos | Ativar destinos | Capacidade de ativar dados para destinos ativos que foram criados. Essa permissão requer que &quot;Destinos de Visualização&quot; ou &quot;Gerenciar destinos&quot; sejam concedidos ao usuário que ativará os destinos.* |
| Ingestão de dados | Gerenciar fontes | Acesso para ler, criar, editar e desativar fontes. |
| Ingestão de dados | Fontes de Visualização | Acesso somente leitura a fontes disponíveis na guia *Catálogo* e fontes autenticadas na guia *Procurar* . |
| Área de trabalho da ciência de dados | Gerenciar a área de trabalho da análise de dados | Acesso para ler, criar, editar e excluir na Data Science Workspace. |

_(*) Esta permissão exige provisões para os Dados do cliente em tempo real na Platform. Para obter mais informações sobre a CDP em tempo real, comece lendo a visão geral[da CDP em tempo](https://docs.adobe.com/content/help/pt-BR/experience-platform/rtcdp/overview.html)real._

## Próximas etapas

Ao ler este guia, o senhor foi apresentado aos principais princípios do controle de acesso. Agora você pode continuar com o guia [do usuário do](./ui/overview.md) controle de acesso para obter etapas detalhadas sobre como usar o Admin Console para criar perfis de produtos e atribuir permissões ao Platform.