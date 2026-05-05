---
title: Notas de versão da Adobe Experience Platform de abril de 2026
description: As notas de versão de abril de 2026 para Adobe Experience Platform.
exl-id: 47070fcf-b585-43f4-b43b-0d62c18f0693
source-git-commit: 9ebf498257378f4c5002276a84f104cf2d337601
workflow-type: tm+mt
source-wordcount: '1580'
ht-degree: 15%

---

# Notas de versão da Adobe Experience Platform

>[!TIP]
>
>Consulte a documentação a seguir para obter as notas de versão de outros aplicativos da Adobe Experience Platform:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/releases/latest)
>- [Composição de público-alvo federado](https://experienceleague.adobe.com/pt-br/docs/federated-audience-composition/using/release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/pt-br/docs/real-time-cdp-collaboration/using/latest)

**Data de lançamento: 28 de abril de 2026**

Novos recursos e atualizações dos recursos existentes no Adobe Experience Platform:

- [Coleção de dados](#data-collection)
- [Destinos](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Serviço de consultas](#query-service)
- [Real-Time CDP](#rtcdp)
- [Sandboxes](#sandboxes)
- [Fontes](#sources)

## Coleção de dados {#data-collection}

A Adobe Experience Platform fornece um conjunto de tecnologias que permitem coletar dados da experiência do cliente e enviá-los à Rede de borda da Adobe Experience Platform, onde eles podem ser enriquecidos, transformados e distribuídos para destinos da Adobe ou de outras empresas.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Exibir detalhes da compilação | Agora você pode acessar Builds e criar detalhes de uma Biblioteca ou de um Ambiente para visualizar o build ativo no momento e inspecionar o conteúdo (extensões, elementos de dados e regras). Para obter mais informações, consulte a [Visão geral das compilações](../../tags/ui/publishing/builds.md#build-details). |

{style="table-layout:auto"}

Para obter mais informações, leia a [Visão geral da coleção de dados](../../tags/home.md).

## Destinos {#destinations}

[!DNL Destinations] são integrações pré-criadas com plataformas de destino. Use destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas por email, publicidade direcionada e muitos outros casos de uso.

**Destinos novos ou atualizados**

| Destino | Descrição |
| --- | --- |
| [!BADGE Beta]{type=Informative} [Correspondência de Cliente de Anúncios da Microsoft](../../destinations/catalog/advertising/microsoft-ads-customer-match.md) | Combinar clientes por endereço de email e reengajar com eles em todo o [!DNL Microsoft Advertising Network], incluindo anúncios de Pesquisa e Público-alvo. Vincule sua conta do [!DNL Microsoft Advertising] à Real-Time CDP para automatizar a criação e o gerenciamento de listas de correspondência de clientes diretamente da Experience Platform. Para obter acesso, entre em contato com seu gerente de conta da Adobe. |
| [!BADGE Beta]{type=Informative} [Reddit Custom Audience](../../destinations/catalog/advertising/reddit-custom-audience.md) | Enviar audiências do Experience Platform para [!DNL Reddit Ads]. Conecte sua conta do [!DNL Reddit], mapeie identidades e ative públicos para alcançar as pessoas que exploram ativamente seus interesses no [!DNL Reddit]. |
| [Amazon Ads v2](../../destinations/catalog/advertising/amazon-ads-v2.md) | Use o cartão [!DNL Amazon Ads v2] para todas as novas conexões [!DNL Amazon Ads]. O [!DNL Amazon Ads v2] se conecta ao [!DNL Ads Data Manager], que fornece suporte para tipos de identidade expandidos, campos relacionados a endereços e compartilhamento de dados entre produtos [!DNL Amazon Ads], melhorando o direcionamento e as taxas de correspondência de público-alvo. O conector [!DNL Amazon Ads] existente no catálogo foi renomeado para [(Herdado) [!DNL Amazon Ads]](../../destinations/catalog/advertising/amazon-ads.md). Se você tiver uma conexão existente herdada, ela continuará a funcionar sem as alterações necessárias. |
| [[!DNL Rokt]](../../destinations/catalog/advertising/rokt.md) | Use o [!DNL Rokt] para conectar os públicos da Experience Platform à tomada de decisões em tempo real orientada por IA, melhorando o desempenho da campanha por meio de direcionamento, supressão e personalização mais precisos. |
| [Conexão de público-alvo da Acxiom](../../destinations/catalog/advertising/acxiom-audience-connection.md) | O destino [!DNL Acxiom Audience Connection] agora está disponível. Use-o para aprimorar públicos-alvo com tecnologia [!DNL Acxiom's Real ID] e ativá-los para [!DNL Altice], [!DNL Ampersand], [!DNL Comcast], [!DNL Cox], [!DNL Facebook], [!DNL Amazon], [!DNL Pinterest], [!DNL Vizio], [!DNL LG Ads], [!DNL Spectrum] e [!DNL Viant]. |
| [Conexão de público-alvo da Acxiom Real ID](../../destinations/catalog/advertising/acxiom-real-id-audience-connection.md) | O destino [!DNL Acxiom Real ID Audience Connection] agora está disponível. Use-o para ativar públicos usando [!DNL Acxiom's Real ID] como chave de correspondência entre [!DNL Altice], [!DNL Ampersand], [!DNL Comcast], [!DNL Cox], [!DNL Facebook], [!DNL Amazon], [!DNL Pinterest], [!DNL Vizio], [!DNL LG Ads], [!DNL Spectrum] e [!DNL Viant]. |

{style="table-layout:auto"}

**Correções e melhorias**

| Corrigir | Descrição |
| --- | --- |
| Nova coluna `TS` para destinos [Snowflake Streaming](../../destinations/catalog/warehouses/snowflake.md) | O destino [Snowflake Streaming](../../destinations/catalog/warehouses/snowflake.md) agora inclui uma coluna de carimbo de data/hora `TS` na tabela compartilhada, mostrando quando cada linha foi atualizada pela última vez. Esta atualização estará sendo lançada até o final de abril. |
| Suporte de monitoramento para destinos do [Personalization](../../destinations/catalog/personalization/custom-personalization.md) personalizado | A página [execuções de fluxo de dados](../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-streaming-destinations) agora mostra métricas para destinos do [Personalization personalizado](../../destinations/catalog/personalization/custom-personalization.md). Anteriormente, essas métricas não estavam disponíveis para esse tipo de destino. Use-os para verificar se os públicos-alvo estão sendo ativados conforme esperado e para diagnosticar problemas. <br> ![O fluxo de dados executa as métricas exibidas para um destino Personalization personalizado, mostrando identidades ativadas, excluídas e com falha.](./assets/april/dataflow-run-custom-personalization.png "O fluxo de dados executa métricas para destinos Personalization Personalizados."){zoomable="yes"} |
| Contagens de perfis na etapa de revisão do fluxo de trabalho de ativação | A etapa de revisão do fluxo de trabalho de ativação agora mostra as contagens de perfil para públicos-alvo que já estão ativados. As contagens de perfil também são mostradas para [destinos de streaming](../../destinations/ui/activate-segment-streaming-destinations.md), não apenas [destinos em lote](../../destinations/ui/activate-batch-profile-destinations.md). <br> ![As contagens de perfil exibidas na etapa de revisão do fluxo de trabalho de ativação para públicos-alvo já ativados e de transmissão.](./assets/april/profile-count-review.png "Contagens de perfis na etapa de revisão do fluxo de trabalho de ativação."){zoomable="yes"} |
| Visibilidade de expiração de token [!DNL Pinterest] | O destino [[!DNL Pinterest]](../../destinations/catalog/advertising/pinterest.md) agora exibe a data de expiração do token para que você possa ver quando a reautenticação é necessária. [!DNL Pinterest] tokens expiram a cada 30 dias. Quando um token expira, as exportações de dados param de funcionar. Para evitar interrupções, [atualize suas credenciais de autenticação](../../destinations/catalog/advertising/pinterest.md#refresh-authentication-credentials) antes que o token expire. |
| Exportar arquivo agora desativado para agendamentos expirados | Quando o cronograma do seu público-alvo expira, o **[!UICONTROL Export file now]** é desabilitado antes de você tentar usá-lo, e uma dica de ferramenta explica o motivo. Anteriormente, selecionar a ação resultava em um erro. <br> ![A ação Exportar arquivo agora está desabilitada com uma dica de ferramenta explicando por que a ação não está disponível.](./assets/april/export-file-now-disabled.png "Ação Exportar arquivo agora desabilitada."){zoomable="yes"} |
| Correção da visibilidade da coluna no fluxo de trabalho de ativação | Correção de um problema em que a alteração de colunas visíveis em uma tabela afetava incorretamente outras tabelas no fluxo de trabalho de ativação. |

{style="table-layout:auto"}

Para obter mais informações, leia a [Visão geral dos Destinos](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

O XDM é uma especificação de código aberto que fornece estruturas e definições comuns (esquemas) para dados trazidos para o Experience Platform. Ao aderir aos padrões do XDM, todos os dados de experiência do cliente podem ser incorporados em uma representação comum para fornecer insights de maneira mais rápida e integrada. Você pode obter insights valiosos sobre ações de clientes, definir públicos-alvo por meio de segmentos e usar atributos de clientes para fins de personalização.

| Recurso | Descrição |
| --- | --- |
| Aprimoramentos No Uso E Na Detecção De Grupos De Campo | Visualize quais esquemas usam um grupo de campos e acesse metadados, como classes compatíveis, atributos obrigatórios e rótulos de governança diretamente na interface do usuário. Você também pode filtrar grupos de campos por compatibilidade de classe e tags do setor para descobrir recursos relevantes e avaliar o impacto com mais eficiência antes de fazer alterações. Consulte o [Guia de exploração de grupos de campos](../../xdm/ui/explore.md#explore-field-groups.md) para obter mais detalhes. |

Para obter mais informações, leia a [visão geral do XDM](../../xdm/home.md).

## Serviço de consultas {#query-service}

Use o Serviço de Consulta para consultar dados no Adobe Experience Platform [!DNL Data Lake] com SQL padrão. Associe-se a qualquer conjunto de dados do [!DNL Data Lake] e capture os resultados da consulta como um novo conjunto de dados para usar em relatórios, no Data Science Workspace ou na assimilação no Perfil do Cliente em Tempo Real.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Gerenciamento de Sessão do Serviço de Consulta | Exiba e encerre sessões ativas do Serviço de Consulta da guia [!UICONTROL Admin] para monitorar o uso e a capacidade de sessão ociosa livre. Isso ajuda os administradores a manter fluxos de trabalho confiáveis do Data Distiller, recuperando a capacidade de sessões inativas. Consulte o [Guia de sessões de Gerenciar Serviço de Consulta](../../query-service/ui/session-management.md) para obter mais detalhes. |

{style="table-layout:auto"}

Para obter mais informações, leia a [Visão geral do Serviço de consulta](../../query-service/home.md).

## Real-Time CDP {#rtcdp}

O Real-Time CDP fornece perfis de clientes unificados e acionáveis ao assimilar, processar e ativar dados em vários canais em tempo real. Com o Real-Time CDP, as organizações podem conectar fontes de dados existentes, criar e ativar públicos-alvo avançados e garantir a ativação em conformidade com a privacidade nos destinos, tudo isso no Experience Platform. Isso permite que profissionais de marketing, analistas e equipes de TI ofereçam experiências oportunas e altamente personalizadas para seus clientes por meio de campanhas de marketing ininterruptas em vários canais.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Real-Time CDP MCP (Beta) | Use o [Real-Time CDP MCP](../../rtcdp/rtcdp-mcp.md) para trazer o Real-Time CDP para agentes de IA e clientes compatíveis com MCP, permitindo que você interaja com as ferramentas do Real-Time CDP diretamente por meio da sua experiência LLM nativa. Ao conectar um cliente compatível com MCP (como Claude, ChatGPT, Claude Code, Codex, Cursor ou VS Code) ao endpoint fornecido pelo representante da Adobe, é possível usar a linguagem natural para inspecionar públicos, configuração de destino e histórico de execução de ativação, sem gravar chamadas de API REST do Experience Platform ou navegar em vários workflows da interface do usuário. Depois de concluir um logon no Adobe com base em navegador, você terá acesso somente leitura a ferramentas que incluem: <ul><li>Pesquisar públicos existentes</li><li>Visualizar associação de público-alvo</li><li>Listar Tipos de Destino</li><li>Listar Contas Configuradas</li><li>Listar destinos configurados</li><li>Listar Conexões Do Source</li><li>Listar Conexões de Destino</li><li>Inspecionar execuções de ativação</li></ul>. Cada solicitação requer parâmetros `imsOrgId` e `sandboxName` para garantir que as ações tenham escopo para sua organização e sandbox. **Observação**: não há suporte para operações de gravação nesta versão do Beta. |

{style="table-layout:auto"}

Para obter mais informações, leia a [visão geral do Real-Time CDP](../../rtcdp/home.md).

## Sandboxes {#sandboxes}

O Adobe Experience Platform foi criado para enriquecer aplicativos de experiência digital em escala global. As empresas geralmente executam vários aplicativos de experiência digital em paralelo e precisam atender ao desenvolvimento, ao teste e à implantação desses aplicativos enquanto garantem a conformidade operacional.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Cópia Expressa | Use a Cópia Expressa para copiar objetos para uma sandbox de destino em uma única ação da [Interface do Usuário de Ferramentas da Sandbox](/help/sandboxes/ui/sandbox-tooling.md#express-copy). Os objetos dependentes são detectados automaticamente e criados na sandbox de destino ou reutilizados quando já existem. |

{style="table-layout:auto"}

Para obter mais informações, leia a [visão geral das sandboxes](../../sandboxes/home.md).

## Fontes {#sources}

A Experience Platform fornece uma API RESTful e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar a sistemas de armazenamento externos e serviços de CRM, definir períodos para execuções de ingestão e gerenciar a taxa de transferência de ingestão de dados.

**Fontes novas ou atualizadas**

| Fonte | Descrição |
| --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL Talon.One] | A [[!DNL Talon.One] origem](../../sources/connectors/loyalty/talon-one.md) do Experience Platform agora está disponível nos modos de lote e de streaming. Use o [[!DNL Talon.One Batch Source Connector]](../../sources/tutorials/ui/create/loyalty/talon-one-batch.md) para assimilar periodicamente sessões fechadas e transações históricas de fidelidade e a origem [[!DNL Talon.One Streaming Events]](../../sources/tutorials/ui/create/loyalty/talon-one-streaming.md) para trazer eventos [!DNL Talon.One] para a Experience Platform em tempo quase real. Juntos, eles facilitam o carregamento e a ativação dos dados de fidelidade do [!DNL Talon.One] na Real-Time CDP, Adobe Journey Optimizer e Offer Decisioning. |
| Suporte à filtragem em nível de linha para [!DNL Salesforce] usando SOQL | Agora é possível aplicar [!DNL Salesforce] filtros SOQL (Object Query Language) diretamente em [!DNL Salesforce] conexões de origem, permitindo restringir os dados em nível de linha antes que sejam assimilados na Experience Platform. Use o recurso para: <ul><li>Definir as condições de estilo WHERE-clause do SOQL em objetos do Salesforce (por exemplo, somente leads com Email != nulo ou oportunidades em estágios específicos)</li><li>Limite a assimilação somente às linhas que atendem aos seus critérios, reduzindo a movimentação de dados, o armazenamento e o processamento downstream desnecessários</li><li>Alinhe mais a assimilação do Experience Platform com suas regras de acesso e conformidade de dados do CRM, controlando quais registros são trazidos para o Experience Platform na origem</li></ul>. Para obter mais informações, leia o manual sobre a [filtragem em nível de linha para fontes](../../sources/tutorials/api/filter.md). |

{style="table-layout:auto"}

Para obter mais informações, leia a [visão geral de fontes](../../sources/home.md).

<!--

| Data Distiller Accelerators | Run and schedule Adobe-managed, parameterized SQL templates in the Query Service UI to perform common analyses without writing SQL. This helps you standardize analytics workflows and reuse trusted query logic across your organization. See the [Data Distiller accelerators guide](../../query-service/ui/accelerators.md) for more details. |

| [!DNL Delta Sharing] | You can use the [!DNL Delta Sharing] source to bring Delta tables into Experience Platform through a secure, open data‑sharing protocol. After you configure a [!DNL Delta Sharing] connection and select the shares and tables you want to ingest, Platform automatically brings that data into your datasets so you can use it for analysis, segmentation, and activation. |
| [!DNL Meta Ads] (Beta) | You can use the [!DNL Meta Ads] source connector (Beta) in the Sources workspace to authenticate to [!DNL Meta], select your ad accounts, and schedule ingestion of [!DNL Meta Ads] campaign and performance data into Experience Platform datasets. |

| Automatic dataflow disabling | Sources ingestion dataflows that fail continuously for 30 days are automatically disabled, helping to surface unhealthy dataflows and reduce repeated failed runs. |

-->
