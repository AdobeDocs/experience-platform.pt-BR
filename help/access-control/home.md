---
keywords: Experience Platform;home;popular topics;access control;adobe admin console
solution: Experience Platform
topic: overview
title: Visão geral do controle de acesso
description: O controle de acesso para Adobe Experience Platform é fornecido através do Adobe Admin Console. Essa funcionalidade aproveita perfis de produtos no Admin Console, que vinculam usuários com permissões e caixas de proteção.
translation-type: tm+mt
source-git-commit: 397f08efa276f7885e099a0a8d9dc6d23fe0e8cc
workflow-type: tm+mt
source-wordcount: '1162'
ht-degree: 3%

---


# Visão geral do controle de acesso

O controle de acesso for [!DNL Experience Platform] é fornecido pelo [Adobe Admin Console](https://adminconsole.adobe.com). Essa funcionalidade aproveita perfis de produtos no, [!DNL Admin Console]que vinculam usuários com permissões e caixas de proteção.

## Hierarquia de controles de acesso e fluxo de trabalho

Para configurar o controle de acesso para [!DNL Experience Platform], você deve ter privilégios de administrador para uma organização que tenha uma integração de [!DNL Experience Platform] produto. A função mínima que concede ou retira permissões é um administrador **[!UICONTROL de perfil de]** produto. Outras funções de administrador que podem gerenciar permissões são administradores **[!UICONTROL de]** produtos (podem gerenciar todos os perfis em um produto) e administradores **[!UICONTROL de]** sistema (sem restrições). Consulte o artigo da Adobe Help Center sobre funções [](https://helpx.adobe.com/enterprise/using/admin-roles.html) administrativas para obter mais informações.

>[!NOTE]
>
>A partir desse ponto, quaisquer menções de &quot;administrador&quot; neste documento se referem a um administrador do perfil do produto ou a uma versão superior (conforme descrito acima).

Um fluxo de trabalho de alto nível para obter e atribuir permissões de acesso pode ser resumido da seguinte forma:

- Depois de licenciar a Adobe Experience Platform ou um serviço de aplicativos/aplicativos que usa o Experience Platform, um email é enviado ao administrador especificado durante o licenciamento.
- O administrador faz logon no [Adobe Admin Console](#adobe-admin-console) e seleciona **Adobe Experience Platform** na lista de produtos na página de visão geral.
- O administrador pode visualização os perfis [de](#product-profiles) produtos padrão ou criar novos perfis de produtos do cliente, conforme necessário.
- O administrador pode editar as permissões e os usuários de qualquer perfil de produto existente.
- Ao criar ou editar um perfil de produto, o administrador adiciona usuários ao perfil usando a guia **[!UICONTROL usuários]** e concede permissões a esses usuários (como &quot;[!UICONTROL Ler conjuntos]de dados&quot; ou &quot;[!UICONTROL Gerenciar Schemas]&quot;) acessando a guia **[!UICONTROL permissões]** . Da mesma forma, o administrador pode atribuir acesso a caixas de proteção usando a mesma guia de permissões.
- Quando os usuários fazem logon na interface do [!DNL Experience Platform] [!DNL Platform] usuário, seu acesso aos recursos é determinado pelas permissões que lhes foram concedidas na Etapa 2. Por exemplo, se um usuário não tiver a permissão &quot;[!UICONTROL Visualização Datasets]&quot;, a guia **[!UICONTROL Datasets]** no menu lateral não estará visível para esse usuário.

Para obter etapas mais detalhadas sobre como gerenciar o controle de acesso em [!DNL Experience Platform], consulte o guia [do usuário do](./ui/overview.md)controle de acesso.

Todas as chamadas para [!DNL Experience Platform] APIs são validadas para obter permissões e retornarão erros se as permissões apropriadas não forem encontradas no contexto do usuário atual. Na interface do usuário, os elementos serão omitidos ou alterados, dependendo das permissões concedidas ao usuário atual.

## Adobe Admin Console

A Adobe Admin Console fornece um local central para gerenciar os direitos e o acesso de produtos do Adobe para sua organização. Por meio do console, você pode conceder a grupos de usuários permissões de acesso para vários [!DNL Platform] recursos, como &quot;[!UICONTROL Gerenciar conjuntos]de dados&quot;, &quot;Conjuntos[!UICONTROL de dados de]Visualização&quot; ou &quot;[!UICONTROL Gerenciar Perfis]&quot;.

### Perfis de produtos

No [!DNL Admin Console], as permissões são atribuídas aos usuários por meio do uso de perfis **[!UICONTROL de]** produtos. Os perfis de produtos permitem que você conceda permissões a um ou vários usuários e também contêm seu acesso ao escopo das caixas de proteção que lhes são atribuídas por meio de perfis de produtos. Os usuários podem ser atribuídos a um ou vários perfis de produtos pertencentes à sua organização.

### Perfis de produtos padrão

[!DNL Experience Platform] vem com dois perfis de produto padrão pré-configurados. A tabela a seguir descreve o que é fornecido em cada perfil padrão, incluindo a caixa de proteção à qual eles concedem acesso, bem como as permissões que eles concedem dentro do escopo dessa caixa de proteção.

| Perfil de produto | Acesso à caixa de proteção | Permissões |
| --- | --- | --- |
| Produção padrão - Todos os acessos | Produção | Todas as permissões se aplicam a [!DNL Experience Platform], exceto as permissões de Administração da caixa de proteção. |
| Administração padrão de sandbox | N/D | Fornece acesso somente às permissões de Administração da caixa de proteção. |

## Caixas de proteção e permissões

As caixas de proteção de não-produção são uma forma de virtualização de dados que permite isolar dados de outras caixas de proteção e geralmente são usadas para experimentos de desenvolvimento, testes ou testes. As **[!UICONTROL permissões]** [!DNL Platform] de um perfil de produto concedem aos usuários do perfil acesso aos recursos dentro dos ambientes da caixa de proteção aos quais eles receberam acesso. Uma licença padrão de Experience Platform concede cinco caixas de proteção (uma produção e quatro não-produção). Você pode adicionar pacotes de dez caixas de proteção de não produção até um máximo de 75 caixas de proteção no total. Entre em contato com seu administrador de organização IMS ou seu representante de vendas de Adobe para obter mais detalhes.

Para obter mais informações sobre caixas de proteção em [!DNL Experience Platform], consulte a visão geral [das](../sandboxes/home.md)caixas de proteção.

### Acesso a caixas de proteção

O acesso às caixas de proteção é gerenciado por meio de perfis de produtos. Para obter etapas detalhadas sobre como ativar o acesso a uma caixa de proteção para um perfil de produto, consulte o guia [do usuário do](./ui/overview.md)controle de acesso.

Os usuários podem receber acesso a uma ou mais caixas de proteção em um perfil de produto. Se um usuário estiver incluído em dois ou mais perfis de produtos, ele terá acesso a todas as caixas de proteção incluídas nesses perfis.

A permissão &quot;Gerenciamento de sandbox&quot; permite que os usuários gerenciem, visualizações ou redefinam caixas de proteção.

### Permissões

A guia **Permissões** em um perfil de produto exibe as caixas de proteção e as permissões que estão ativas para esse perfil:

![](./images/permissions-overview.png)

As permissões que são concedidas por meio do [!DNL Admin Console] são classificadas por categoria, com algumas permissões concedendo acesso a várias funcionalidades de baixo nível.

A tabela a seguir descreve as permissões disponíveis [!DNL Experience Platform] no [!DNL Admin Console], com descrições dos [!DNL Platform] recursos específicos aos quais eles concedem acesso. Para obter etapas detalhadas sobre como adicionar permissões a um perfil de produto, consulte o guia [do usuário do](./ui/overview.md)controle de acesso.

| Categoria | Permissão | Descrição |
| --- | --- | --- |
| [!DNL Data Modeling] | [!UICONTROL Gerenciar Schemas] | Acesso para ler, criar, editar e excluir schemas e recursos relacionados. |
| [!DNL Data Modeling] | [!UICONTROL Visualizar esquemas] | Acesso somente leitura a schemas e recursos relacionados. |
| [!DNL Data Management] | [!UICONTROL Gerenciar conjuntos de dados] | Acesso para ler, criar, editar e excluir conjuntos de dados. Acesso somente leitura para schemas. |
| [!DNL Data Management] | [!UICONTROL Visualizar conjuntos de dados] | Acesso somente leitura para conjuntos de dados e schemas. |
| [!DNL Data Management] | [!UICONTROL Monitoramento de dados] | Acesso somente leitura a conjuntos de dados e fluxos de monitoramento. |
| [!DNL Profile Management] | [!UICONTROL Gerenciar Perfis] | Acesso para ler, criar, editar e excluir conjuntos de dados usados para perfis do cliente. Acesso somente leitura aos perfis disponíveis. |
| [!DNL Profile Management] | [!UICONTROL Perfis visualizações] | Acesso somente leitura aos perfis disponíveis. |
| [!DNL Profile Management] | [!UICONTROL Exportar Audiência para segmento] | Capacidade de exportar um segmento de audiência avaliado para um conjunto de dados. |
| [!DNL Identities] | [!UICONTROL Gerenciar namespaces de identidade] | Acesso para ler, criar, editar e excluir namespaces de identidade. |
| [!DNL Identities] | [!UICONTROL Namespaces de identidade de visualização] | Acesso somente leitura para namespaces de identidade. |
| [!DNL Sandbox Administration] | [!UICONTROL Gerenciar caixas de proteção] | Acesso para ler, criar, editar e excluir caixas de proteção. |
| [!DNL Sandbox Administration] | [!UICONTROL Visualizar sandboxes] | Acesso somente leitura para caixas de proteção pertencentes à sua organização. |
| [!DNL Sandbox Administration] | [!UICONTROL Redefinir uma caixa de proteção] | Capacidade de reiniciar uma caixa de proteção. |
| [!DNL Destinations] | [!UICONTROL Gerenciar destinos] | Acesso para ler, criar, editar e desativar destinos.* |
| [!DNL Destinations] | [!UICONTROL Destinos da visualização] | Acesso somente leitura para destinos disponíveis na guia **[!UICONTROL Catálogo]** e destinos autenticados na guia **[!UICONTROL Procurar]** .* |
| [!DNL Destinations] | [!UICONTROL Ativar destinos] | Capacidade de ativar dados para destinos ativos que foram criados. Esta permissão requer que &quot;Destinos de Visualização&quot; ou &quot;Gerenciar [!UICONTROL destinos&quot;] sejam concedidos ao usuário que ativará os destinos.* |
| [!DNL Data Ingestion] | [!UICONTROL Gerenciar fontes] | Acesso para ler, criar, editar e desativar fontes. |
| [!DNL Data Ingestion] | [!UICONTROL Fontes de visualização] | Acesso somente leitura a fontes disponíveis na guia **[!UICONTROL Catálogo]** e fontes autenticadas na guia **[!UICONTROL Procurar]** . |
| [!DNL Data Science Workspace] | [!UICONTROL Gerenciar a área de trabalho da análise de dados] | Acesso para ler, criar, editar e excluir em [!DNL Data Science Workspace]. |

_(*) Esta permissão exige disposições para[!DNL Real-time Customer Data Platform]. Para obter mais informações sobre a CDP em tempo real, comece lendo a visão geral[da CDP em tempo](https://docs.adobe.com/content/help/pt-BR/experience-platform/rtcdp/overview.html)real._

## Próximas etapas

Ao ler este guia, o senhor foi apresentado aos principais princípios do controle de acesso em [!DNL Experience Platform]. Agora você pode continuar com o guia [do usuário do](./ui/overview.md) controle de acesso para obter etapas detalhadas sobre como usar o [!DNL Admin Console] para criar perfis de produtos e atribuir permissões para [!DNL Platform].