---
solution: Real-Time Customer Data Platform
title: Trabalhar com clientes MCP (Beta)
description: Saiba como conectar o Adobe Real-Time CDP a clientes MCP usando o servidor MCP
feature: Integrations
topic: Content Management, Artificial Intelligence
badge: label="Beta" type="Informative"
role: User, Developer
level: Beginner, Intermediate
hide: true
hidefromtoc: true
exl-id: 48dba0d2-7df9-4d76-bc87-5af49a8a40cc
source-git-commit: 8a9dd740bb210ef125bca65a8358bb6b51f6d28f
workflow-type: tm+mt
source-wordcount: '2379'
ht-degree: 0%

---

# Trabalhar com clientes MCP (Beta) {#rtcdp-mcp}

Você pode usar a integração do Adobe Real-Time CDP MCP para consultar públicos, destinos e integridade da ativação usando prompts em linguagem simples, sem gravar chamadas de API ou navegar nas telas dos produtos. Esta página explica como a integração funciona, o que você pode fazer com ela e como começar.

>[!AVAILABILITY]
>
>O servidor MCP do Real-Time CDP é distribuído como um **servidor de transporte HTTP remoto** que os usuários instalam e configuram em clientes MCP e plataformas de aplicativos compatíveis (por exemplo, Claude, ChatGPT, Claude Code, Codex, Cursor ou Código VS). A autenticação é tratada por meio de um **fluxo de logon baseado em navegador** — quando o cliente se conecta ao servidor pela primeira vez, ele abre o navegador padrão para que você possa entrar com as credenciais da Adobe e autorizar o acesso. Entre em contato com o representante da Adobe para acessar este programa da Beta.

## Beta, segurança e avisos legais {#mcp-notices}

**aviso sobre a documentação do Beta:** esta documentação abrange um recurso do Beta e não constitui a documentação final. O conteúdo descrito aqui está relacionado a uma versão do Beta e está sujeito a alterações até sua disponibilização geral. A Adobe não faz declarações sobre a integridade ou a precisão desta documentação.

Ao usar o Adobe Real-Time CDP MCP Server (Beta) (&quot;Beta&quot;), você reconhece que o Beta é fornecido **&quot;no estado em que se encontra&quot; sem garantias de qualquer tipo**. A Adobe não tem nenhuma obrigação de manter, corrigir, atualizar, alterar, modificar ou oferecer suporte à Beta. É recomendável ter cuidado e não depender de forma alguma do funcionamento ou desempenho correto desse Beta e/ou dos materiais que o acompanham. O Beta é considerado Informações confidenciais da Adobe. Qualquer &quot;Feedback&quot; (informação sobre o Beta incluindo, mas não se limitando a, problemas ou defeitos encontrados durante o uso do Beta, sugestões, melhorias e recomendações) fornecido por Você ao Adobe é atribuído ao Adobe, incluindo todos os direitos, cargos e interesses no e no Feedback.

>[!WARNING]
>
>O protocolo de contexto de modelo (MCP) é um padrão de código aberto emergente e pode apresentar riscos de segurança ou confiabilidade. As integrações do servidor Adobe MCP e a documentação relacionada são fornecidas &quot;no estado em que se encontram&quot;, sem garantias de nenhum tipo.
>
>Conectar clientes ou servidores MCP a produtos da Adobe é uma configuração selecionada pelo cliente. Os clientes são responsáveis por avaliar a segurança e a adequação de qualquer integração de MCP. O Adobe não é responsável por problemas resultantes de configuração incorreta, uso incorreto do MCP, vulnerabilidades em implementações de terceiros ou ações não intencionais executadas por meio de fluxos de trabalho habilitados para MCP.
>
>Para reduzir os riscos, a Adobe incentiva o teste de integrações em um ambiente de sandbox antes do uso produtivo e a análise e validação cuidadosas de todas as ações e respostas iniciadas pelo MCP antes de confirmar ou confiar nelas.

## Qual é o protocolo de contexto do modelo? {#mcp-overview}

As equipes de marketing, dados e experiência do cliente dependem cada vez mais de aplicativos baseados em bate-papo e ferramentas de desenvolvedor — como Anthropic Claude, OpenAI ChatGPT, Cursor e Microsoft Copilot Studio — para simplificar seu trabalho diário. Esses aplicativos oferecem suporte ao **Protocolo de Contexto de Modelo (MCP)**, um padrão aberto que permite que os aplicativos exponham ferramentas de back-end a grandes modelos de idioma (LLMs) de maneira uniforme.

O Real-Time CDP agora fornece um servidor MCP que exibe operações de público-alvo, destino e ativação diretamente dentro de qualquer aplicativo compatível com MCP. Com a integração do Real-Time CDP MCP, diferentes personalidades podem colaborar em torno da mesma segmentação e dados de ativação — sem gravar consultas nas APIs REST do Adobe Experience Platform ou navegar por várias telas de interface do usuário. Os clientes podem descrever a intenção por conversação e permitir que o LLM chame as ferramentas de MCP apropriadas.

## Principais recursos {#mcp-capabilities}

O servidor MCP do Real-Time CDP permite inspecionar, resumir e solucionar problemas de públicos-alvo e destinos diretamente do assistente de IA. Todas as operações são **somente leitura** — as superfícies do servidor MCP recuperam APIs como respostas em linguagem simples para que você possa:

* **Obter visibilidade instantânea do público-alvo** — Pergunte sobre definições de público-alvo, estado do ciclo de vida e namespace em linguagem simples sem navegar pelos menus ou extrair relatórios manualmente.
* **Estime o tamanho do público antes da ativação** — Visualize as contagens de associação e os intervalos de confiança para uma consulta de segmento do PQL ou SDD antes de confirmar a criação de um público.
* **Auditoria de seu portfólio de ativação** — Revise os destinos configurados, os fluxos de dados que os alimentam e as conexões de origem/destino por trás de cada fluxo — sem analisar o JSON ou pular nas telas dos produtos.
* **Problemas de ativação de ponto com antecedência** — O destino de superfície falhou ou está em andamento no momento que você pergunta, para que sua equipe possa agir rápido.
* **Colaborar com dados em tempo real** — Profissionais de marketing, engenheiros de dados e partes interessadas podem consultar os mesmos dados em tempo real do Real-Time CDP por meio do assistente de IA, facilitando o alinhamento, a decisão e a movimentação.

## Ferramentas disponíveis {#mcp-tools}

A disponibilidade das ferramentas está mudando rapidamente à medida que ativamos novas ferramentas. Entre em contato com seu representante da Adobe para obter uma lista das ferramentas mais recentes disponíveis.

>[!NOTE]
>
>Todas as ferramentas são **somente leitura**. As operações de gravação (criação, atualização ou exclusão de públicos, destinos ou fluxos de dados) não são compatíveis com a versão atual do Beta.

## Casos de uso {#mcp-use-cases}

Os seguintes exemplos mostram como interagir com o servidor MCP [!DNL Adobe Real-Time CDP] usando linguagem natural:

| Meta | Exemplo de prompt |
| --- | --- |
| **Descoberta do catálogo de destino** | &quot;O TikTok está disponível como destino na minha sandbox?&quot; / &quot;Para quais tipos de destino já tenho contas configuradas?&quot; |
| **Inventário de destino por tipo** | &quot;Listar todos os meus destinos do Amazon S3.&quot; / &quot;Tenho algum destino de exportação de conjunto de dados configurado?&quot; |
| **Auditoria de configuração de destino** | &quot;Em qual bucket meu destino `Loyalty S3 Export` está gravando?&quot; / &quot;Mostrar o caminho de destino e o formato de arquivo do fluxo de dados [ID].&quot; |
| **Integridade da conta** | &quot;Quais das minhas contas de destino têm credenciais expiradas?&quot; / &quot;Alguma conta do Pinterest ou do Facebook está em um estado de erro?&quot; |
| **Integridade da ativação — últimas 24 horas** | &quot;Listar todos os destinos com uma execução com falha nas últimas 24 horas.&quot; / &quot;Meu destino de exportação do conjunto de dados enviou dados nas últimas 24 horas?&quot; |
| **Histórico de ativação por destino** | &quot;`Weekly Loyalty Export` exportou alguma coisa nos últimos 30 dias?&quot; / &quot;Mostrar o histórico completo de execução do destino {NAME}.&quot; |
| **Análise de falha** | &quot;Qual é o motivo de falha mais comum em meus destinos baseados em arquivo esta semana?&quot; / &quot;Execuções com falha recentes do grupo por tipo de erro.&quot; |
| **Descoberta e filtragem de público-alvo** | &quot;Liste cada público com base em CSV na sandbox `marketing-prod`.&quot; / &quot;Quais públicos-alvo têm uma ID de público-alvo externa definida?&quot; |
| **Auditoria de dimensionamento de público-alvo** | &quot;Mostre-me todos os públicos-alvo com tamanho 0.&quot; / &quot;Quais públicos-alvo são maiores que 1.000 perfis?&quot; |
| **Auditoria de expiração de público-alvo** | &quot;Quais destinos têm públicos-alvo cuja data final já passou?&quot; / &quot;Listar públicos-alvo agendados para expirar nos próximos 7 dias.&quot; |
| **Espaço de ativação de público-alvo** | &quot;Quais destinos têm mais de 10 públicos-alvo ativados para eles?&quot; / &quot;Qual público-alvo é ativado para a maioria dos destinos?&quot; |
| **Cross-filter: audience × ativation** | &quot;Mostre-me públicos-alvo com tamanho superior a 1.000 ativados em pelo menos 2 destinos.&quot; / &quot;Públicos-alvo grandes que são ativados apenas para um único destino.&quot; |
| **Visualização da associação do público-alvo** | &quot;Visualize o tamanho da associação para o público-alvo `High-Value Loyalty Members`.&quot; / &quot;Estime o tamanho desta consulta PQL antes de salvá-la: {EXPRESSION}.&quot; |

## Pré-requisitos {#mcp-prerequisites}

Antes de conectar o servidor MCP do Real-Time CDP ao seu cliente MCP, verifique o seguinte:

* Você tem uma licença ativa do Real-Time CDP.
* Você tem acesso a um cliente compatível que pode se conectar a um servidor MCP remoto ou a um aplicativo MCP personalizado, como Claude, ChatGPT, Claude Code, Codex, Cursor ou VS Code.
* Você tem a ID da organização e o nome da sandbox que deseja consultar.
* Você tem as permissões necessárias no Adobe Experience Platform para exibir públicos, destinos e entidades de serviço de fluxo.

## Conectar o servidor MCP do Real-Time CDP {#mcp-connect}

>[!NOTE]
>
>Essa integração está no Beta. Os menus do cliente, os requisitos de plano e os controles administrativos podem variar de acordo com o aplicativo e a versão.

Antes de começar, verifique se você tem o seguinte:

* A URL do ponto de extremidade do servidor MCP: `Available to Beta customers through your Adobe representative`.
* Confirmação de que seu usuário do Adobe tem acesso à organização e à sandbox da Experience Platform de destino.

O servidor MCP do Real-Time CDP é um **servidor MCP HTTP remoto**. Em todos os clientes, a configuração segue o mesmo padrão:

1. Adicione o URL do servidor.
2. Salve ou habilite a conexão.
3. Conclua o **logon do Adobe baseado em navegador** na primeira vez que o cliente chamar uma ferramenta.
4. Forneça `imsOrgId` e `sandboxName` com cada solicitação.

### Instalar em clientes baseados em interface do usuário {#mcp-connect-ui}

#### Claude

Para `claude.ai` e Claude Desktop, adicione o servidor MCP do Real-Time CDP como um **conector personalizado** usando o ponto de extremidade fornecido pelo representante da Adobe. Em planos Claude individuais, adicione-o em **Personalizar > Conectores**. Em planos Team e Enterprise, um proprietário pode precisar adicioná-lo primeiro em **Configurações da organização > Conectores**, após o qual cada usuário o conecta em suas próprias configurações Claude. Depois de configurado, habilite o conector em uma conversa e conclua o logon do navegador do Adobe na primeira utilização.

#### ChatGPT

No ChatGPT, adicione o servidor MCP do Real-Time CDP como um **aplicativo/conector personalizado** usando o ponto de extremidade fornecido pelo representante da Adobe. Dependendo do seu plano ChatGPT, isso pode exigir **Modo de desenvolvedor** e aprovação do administrador do espaço de trabalho. Depois que o aplicativo/conector for criado ou habilitado, conecte-o a partir de **Configurações > Aplicativos** ou **Configurações > Aplicativos e Conectores** e, em seguida, autentique por meio do logon no navegador Adobe quando solicitado.

#### Cursor

No Cursor, adicione o servidor MCP do Real-Time CDP como um servidor MCP remoto usando o endpoint fornecido pelo representante da Adobe. Abra **Configurações > MCP**, adicione um novo servidor e cole a URL do ponto de extremidade. Depois de adicionado, habilite o servidor para o seu espaço de trabalho selecionando **conectar** para autenticar através do navegador.

#### Outros clientes com base na interface do usuário

Para clientes como o Código VS ou outros aplicativos Web e de desktop com suporte a MCP remoto, adicione o servidor MCP do Real-Time CDP como um servidor HTTP **remoto** usando o ponto de extremidade fornecido pelo representante da Adobe. Se o cliente suportar cabeçalhos opcionais ou tokens de portador, deixe-os vazios, a menos que a Adobe especificamente instrua o contrário; a autenticação é tratada por meio do fluxo de logon do Adobe com base em navegador na primeira utilização.

### Instalar em clientes técnicos {#mcp-connect-technical}

#### código Claude

Adicione o servidor do terminal:

```bash
claude mcp add --transport http rtcdp <endpoint provided by your Adobe representative>
```

Em seguida, inicie o Claude Code e execute:

```text
/mcp
```

Selecione o servidor `rtcdp` e conclua o fluxo de logon do Adobe em seu navegador. Se você já tiver adicionado o servidor em `claude.ai`, ele também poderá aparecer automaticamente no Código Claude quando ambos estiverem usando a mesma conta.

#### Codex

Adicione o servidor do terminal:

```bash
codex mcp add rtcdp --url <endpoint provided by your Adobe representative>
```

Autentique o servidor:

```bash
codex mcp login rtcdp
```

Verifique a configuração:

```bash
codex mcp list
```

Você também pode adicionar o servidor diretamente a `~/.codex/config.toml`:

```toml
[mcp_servers.rtcdp]
url = "<endpoint provided by your Adobe representative>"
```

### Parâmetros de solicitação obrigatórios {#mcp-connect-params}

Cada chamada de ferramenta requer dois parâmetros que determinam o escopo da solicitação:

* `imsOrgId` — sua ID de organização, mapeada para o cabeçalho `x-gw-ims-org-id` nas chamadas downstream de API do Experience Platform.
* `sandboxName` — o nome da sandbox do Experience Platform, mapeado para o cabeçalho `x-sandbox-name`.

## Limitações conhecidas (Beta) {#mcp-limitations}

As seguintes limitações se aplicam à versão atual do Beta do servidor MCP [!DNL Adobe Real-Time CDP]:

| Limitação | Descrição | Solução alternativa |
| --- | --- | --- |
| **Superfície somente leitura** | O servidor MCP expõe apenas APIs de recuperação. Não é possível criar, atualizar, ativar ou excluir públicos, destinos ou fluxos de dados. | Use a interface do usuário do Real-Time CDP ou as APIs REST do AEP para operações de gravação. |
| **Nenhuma métrica de envolvimento ou entrega** | O servidor MCP não retorna estatísticas de delivery downstream, engajamento ou métricas de conversão das plataformas de destino. | Use os relatórios da própria plataforma de destino, o Customer Journey Analytics MCP ou o Adobe Analytics MCP para dados de engajamento e conversão. |
| **A consulta de segmento deve ser criada externamente** | `Preview Audience Membership` requer uma expressão PQL ou SDD válida como entrada; o servidor MCP não compõe a consulta para você. | Crie a expressão PQL/SDD na interface do usuário do Construtor de segmentos ou por meio da API do serviço de segmentação e cole no prompt do MCP. |
| **Paginação via tokens de continuação** | As ferramentas de lista retornam resultados paginados. A enumeração completa em sandboxes muito grandes requer o encadeamento de chamadas `continuationToken`. | Restrinja as consultas usando filtros (nome, estado, especificação de conexão, intervalo de tempo) em vez de enumerar a lista completa. |
| **A filtragem de execução de ativação é baseada apenas no tempo** | O `Inspect Activation Runs` oferece suporte à filtragem por status e carimbo de data/hora de conclusão (ms UTC de época), mas não diretamente por tipo de erro ou plataforma de destino. | O filtro por `flowId` primeiro (obtido de `List Configured Destinations`) para escopo é executado para um destino específico. |
| **Configuração de região necessária** | As chamadas de ferramenta falharão com HTTP 403 &quot;User region is missing&quot; se o gateway MCP não estiver configurado para a região do usuário. | Entre em contato com seu representante da Adobe para confirmar se o gateway está configurado para sua região antes da primeira utilização. |

## Perguntas frequentes {#mcp-faq}

+++Quais clientes MCP são compatíveis?

O servidor MCP do Real-Time CDP funciona com clientes compatíveis que podem se conectar a servidores MCP remotos ou aplicativos MCP personalizados — incluindo Claude, ChatGPT, Claude Code, Codex, Cursor e VS Code. O fluxo de configuração depende do cliente: os clientes baseados em interface do usuário normalmente adicionam o servidor a partir das configurações, enquanto os clientes técnicos, como Claude Code e Codex, podem adicioná-lo a partir da linha de comando ou dos arquivos de configuração.
+++

+++Como funciona a autenticação?

A autenticação é tratada por meio de um **logon baseado em navegador**. Quando o cliente MCP chama uma ferramenta pela primeira vez, ele abre o navegador padrão para uma página de logon do Adobe. Depois de autenticar e autorizar o cliente, a sessão é estabelecida e as chamadas de ferramenta subsequentes o reutilizam. Nenhuma chave de API ou credenciais de longa duração precisam ser armazenadas na configuração do cliente.
+++

+++Quais objetos do Real-Time CDP posso acessar via MCP?

Você pode acessar públicos, tipos de destino, contas de destino configuradas, fluxos de dados de destino, conexões de origem e de destino e histórico de execuções de ativação. As operações são somente leitura (recuperar APIs); as operações de gravação não são compatíveis com a versão atual.
+++

+++Preciso de acesso de desenvolvedor para usar o servidor MCP do Real-Time CDP?

Não. O servidor MCP foi projetado para personas técnicas e de marketing. Os profissionais de marketing podem interagir com ele usando prompts de linguagem natural em qualquer cliente MCP compatível, enquanto os engenheiros de dados e desenvolvedores podem usá-lo nas ferramentas de desenvolvedor que oferecem suporte ao MCP.
+++

+++Meus dados são enviados ao provedor do cliente MCP?

Quando você envia um prompt, o cliente MCP pode enviar o contexto relevante (incluindo dados do Real-Time CDP retornados pelo servidor MCP) ao seu modelo para processamento. Analise as políticas de privacidade e manuseio de dados do seu provedor de cliente MCP antes de se conectar aos dados de produção.
+++

+++Quais permissões são necessárias no Real-Time CDP?

Você precisa de, no mínimo, **Permissões de exibição** para os objetos que deseja consultar — públicos-alvo, destinos e entidades de serviço de fluxo. Nenhuma permissão de gravação é necessária porque o servidor MCP executa somente operações de leitura. Entre em contato com o administrador do [!DNL Adobe Experience Platform] se não tiver certeza sobre o seu nível de acesso atual.
+++

+++Posso usar o servidor MCP em ambientes de sandbox?

Sim. Cada chamada de ferramenta requer um parâmetro `sandboxName`, de modo que o servidor MCP sempre respeita a configuração da sandbox [!DNL Adobe Experience Platform]. Você pode consultar qualquer sandbox à qual tenha acesso especificando o nome na solicitação.
+++

+++Qual é a diferença entre Visualizar associação de público-alvo e Pesquisar públicos-alvo existentes?

`Search Existing Audiences` retorna públicos que já foram criados e salvos na sandbox. `Preview Audience Membership` pega uma expressão de segmento bruta de PQL ou SDD e retorna uma estimativa de tamanho para ela — útil para dimensionar uma consulta *antes* de salvá-la como uma audiência.
+++

+++Posso consultar públicos da conta, bem como públicos do perfil?

Sim. `Search Existing Audiences` e `Preview Audience Membership` dão suporte a um parâmetro de tipo de entidade. Os públicos do perfil podem ser expressos em PQL ou SDD; os públicos da conta sempre usam a sintaxe SDD (relacional).
+++
