---
title: Notas de versão da Adobe Experience Platform de setembro de 2024
description: As notas de versão de setembro de 2024 da Adobe Experience Platform.
exl-id: e5b40712-2a54-4c6f-a4a1-2f078305da59
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2202'
ht-degree: 20%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 24 de setembro de 2024**

Atualizações dos recursos e da documentação existentes no Adobe Experience Platform:

- [Alertas](#alerts)
- [Painéis](#dashboards)
- [Preparação de dados](#data-prep)
- [Destinos](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Serviço de identidade](#identity-service)
- [Query Service](#query-service)
- [Serviço de segmentação](#segmentation-service)
- [Origens](#sources)

## Alertas {#alerts}

O Experience Platform permite assinar alertas baseados em eventos para várias atividades do Experience Platform. Você pode assinar diferentes regras de alerta por meio da guia [!UICONTROL Alertas] na interface do usuário do Experience Platform e pode optar por receber mensagens de alerta na própria interface ou por meio de notificações por email.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Suporte para sandbox de desenvolvimento | Agora você pode [assinar alertas](../../observability/alerts/ui.md) em sandboxes de produção e desenvolvimento, permitindo um monitoramento perfeito em todos os ambientes. |
| Modelos de email | [Alertas de email](../../observability/alerts/ui.md) agora incluem informações detalhadas de ativos, garantindo que você tenha todos os detalhes importantes à disposição. |
| Personalização aprimorada | Agora você pode configurar [limites de alerta](../../observability/alerts/ui.md#alert-threshold), oferecendo maior flexibilidade para ajustar os alertas às suas necessidades específicas para os seguintes tipos de alerta:<br><ul><li>Atraso na tarefa do segmento</li><li>Atraso na exportação do segmento</li><li>Atraso na execução do fluxo de destino</li><li>Atraso na execução do fluxo do serviço de identidade</li><li>Atraso na execução do fluxo de perfil</li><li>Atraso na execução do fluxo de fontes</li><li>Atraso da execução da consulta</li><li>Taxa de Ignorar Ativação Excedida</li><li>Taxa de erro de assimilação de origens excedida</ul> |
| Alertas expandidos | Alertas de informações de eventos de auditoria agora estão disponíveis para assinatura para as [seguintes regras de alerta](../../observability/alerts/rules.md):<br><ul><li>Criação de público</li><li>Atualização de público</li><li>Exclusão de público</li><li>Criação do conjunto de dados</li><li>Atualização do conjunto de dados</li><li>Exclusão do conjunto de dados</li><li>Criação de esquema</li><li>Atualização de esquema</li><li>Exclusão de esquema. |

{style="table-layout:auto"}

Para obter mais informações sobre alertas, leia a [[!DNL Observability Insights] visão geral](../../observability/home.md).

## Painéis {#dashboards}

O Experience Platform fornece vários painéis por meio dos quais você pode visualizar insights importantes sobre os dados de sua organização, conforme capturados durante instantâneos diários.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| ------- | ----------- |
| Tabela de Complementos de Uso de Licença | Obtenha visibilidade granular sobre o uso de licenças e gerencie seus recursos do Experience Platform com tabelas dedicadas para os principais produtos e complementos. Rastreie e analise as principais métricas de cada produto principal com exibições de drill-through no nível da sandbox. As métricas complementares se integram perfeitamente às métricas dos produtos principais, oferecendo uma visualização abrangente do uso. A visibilidade aprimorada ajuda a otimizar o gerenciamento de licenças e alinhar recursos às necessidades organizacionais. Consulte o [[!UICONTROL guia do painel de Uso da licença]](../../dashboards/guides/license-usage.md#overview-tab) para obter mais detalhes. |
| Query Pro Mode - Atualizações de Filtro Global | Melhore a análise com o novo filtro de datas do Modo Query Pro. Refine insights com parâmetros de data dinâmicos em suas consultas SQL e filtre dados por intervalos de tempo específicos. Escolha intervalos de datas predefinidos ou personalizados com uma interface intuitiva, mantendo os painéis relevantes para todos os usuários. Simplifique os fluxos de trabalho, mantenha a precisão e tome decisões oportunas. Leia o [guia sobre criação de filtros de data](../../dashboards/sql-insights-query-pro-mode/filters/global-filter.md) para obter mais informações. |
| Modos de Consulta Pro - Drill-Throughs | Descubra insights mais profundos com o recurso de detalhamento do modo Query Pro e navegue facilmente de gráficos de alto nível para painéis detalhados. Use esse recurso para mover facilmente de resumos para análises detalhadas e explorar tendências, comportamentos de clientes e KPIs. As passagens automáticas de filtros e as passagens de vários níveis mantêm os dados consistentes, garantindo uma exploração tranquila. Simplifique os fluxos de trabalho, mantenha o contexto e acelere as decisões. Leia o [guia passo a passo sobre como criar detalhamentos](../../dashboards/sql-insights-query-pro-mode/drill-through.md) para obter mais informações. |
| Modo Query Pro - Atributos de Tabela Avançados | Use os atributos de tabela avançados do Modo Query Pro para simplificar a visualização de dados, melhorar a eficiência do fluxo de trabalho e melhorar a clareza dos dados. Adicione classificação automática, redimensionamento e paginação às tabelas diretamente dos painéis personalizados. Classifique as colunas para priorizar os dados principais, redimensionar para facilitar a leitura e navegar por grandes conjuntos de dados sem interrupção sem modificar as consultas SQL. Leia o guia &#39;[Exibir Mais](../../dashboards/sql-insights-query-pro-mode/view-more.md)&#39; para saber como integrar esses recursos e elevar seus insights de dados. |
| Volume de dados total | A métrica &quot;Riqueza média de perfil&quot; foi substituída pela métrica &quot;Volume total de dados&quot;. Volume de dados total refere-se à quantidade total de dados disponíveis que podem ser usados com o Perfil do cliente em tempo real para fluxos de trabalho de envolvimento e personalização. Mais detalhes sobre esta alteração podem ser encontrados no [Guia do Volume de Dados Total](../../landing/license-usage-and-guardrails/total-data-volume.md). |

{style="table-layout:auto"}

Para obter mais informações sobre painéis, incluindo como conceder permissões de acesso e criar widgets personalizados, comece lendo a [visão geral dos painéis](../../dashboards/home.md).

## Preparação de dados {#data-prep}

Use o preparo de dados para mapear, transformar e validar dados de e para o Experience Data Model (XDM).

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| [!BADGE Beta]{type=Informative} Novas funções de Preparação de Dados para uso em Destinos | Agora você pode usar as seguintes funções de matriz para casos de uso de Destinos:<ul><li>`array_to_string`</li><li>`filterArray`</li><li>`transformArray`</li><li>`flattenArray`</li></ul> Para obter mais informações, leia o [guia de funções de preparação de dados](../../data-prep/functions.md#arrays). |

{style="table-layout:auto"}

Para obter mais informações sobre Preparo de Dados, leia a [Visão geral do Preparo de Dados](../../data-prep/home.md).

## Destinos {#destinations}

**Atualizado em: 30 de setembro de 2024**

[!DNL Destinations] são integrações pré-construídas com plataformas de destino que permitem a ativação perfeita de dados da Adobe Experience Platform. É possível usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas de email, publicidade direcionada e muitos outros casos de uso.

**Destinos novos ou atualizados** {#new-updated-destinations}

| Destino | Descrição |
| --- | --- |
| [Anúncios do Amazon](/help/destinations/catalog/advertising/amazon-ads.md) | A versão de setembro de 2024 adiciona a opção de mapeamento para exportar o parâmetro `countryCode` para o Amazon Ads. Use o `countryCode` na [etapa de mapeamento](/help/destinations/catalog/advertising/amazon-ads.md#map) para melhorar suas taxas de correspondência de identidade com a Amazon. |
| Demandbase [[!BADGE B2B]{type=Informative}](/help/destinations/catalog/advertising/demandbase.md) | Use esse destino para ativar os públicos-alvo da conta para os casos de uso do Account-Based Marketing (ABM). Anuncie para personas e funções relevantes em suas contas do target por meio do Demand Side Platform B2B (DSP) da DemandBase. As contas do Target também podem ser enriquecidas com dados de terceiros do Demandbase para outros casos de uso downstream em marketing e vendas. |

{style="table-layout:auto"}

**Funcionalidades novas ou atualizadas** {#destinations-new-updated-functionality}

| Recurso | Descrição |
| --- | --- |
| Aprimoramentos na [exportação do conjunto de dados](/help/destinations/ui/export-datasets.md) | A versão de setembro de 2024 do Experience Platform inclui várias melhorias nos recursos de exportação do conjunto de dados para oferecer melhor suporte a vários casos de uso de saída de dados. Esses aprimoramentos de recursos incluem: <ul><li>Novas opções de configuração da pasta de dados, incluindo a opção de adicionar e remover subpastas.</li><li>Novas opções de exportação, incluindo exportação de arquivo completo (uma vez) e a capacidade de especificar datas de término</li><li>Observação: a Adobe também está introduzindo uma data de término padrão de 1º de maio de 2025 para todos os fluxos de dados de exportação de conjunto de dados criados antes da versão de setembro. Para qualquer um desses fluxos de dados, os clientes precisarão atualizar manualmente a data final no fluxo de dados antes da data final, caso contrário, as exportações serão interrompidas nessa data.</li></ul> <br> ![Imagem da interface do usuário do Experience Platform destacando a opção Editar agendamento e pastas na etapa de agendamento.](../2024/assets/september/edit-schedule-folders.png "Opção Editar agendamento e pastas na etapa de agendamento."){width="250" align="center" zoomable="yes"} |

{style="table-layout:auto"}

Para obter mais informações, leia a [visão geral de destinos](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

O XDM é uma especificação de código aberto que fornece estruturas e definições comuns (esquemas) para dados inseridos na Adobe Experience Platform. Ao aderir aos padrões do XDM, todos os dados de experiência do cliente podem ser incorporados em uma representação comum para fornecer insights de maneira mais rápida e integrada. Você pode obter insights valiosos sobre ações de clientes, definir públicos-alvo por meio de segmentos e usar atributos de clientes para fins de personalização.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Melhorias no Editor de esquemas | Assuma o controle dos relacionamentos do esquema com um workflow de relacionamento atualizado no Editor de esquemas. Atualize ou remova facilmente os relacionamentos existentes diretamente da interface do usuário do Experience Platform, tornando o gerenciamento de esquemas mais simples e intuitivo. Ajuste esquemas de referência e renomeie os relacionamentos com confiança, garantindo uma integridade de dados contínua na segmentação e em outros processos importantes. Para saber mais sobre como gerenciar com eficiência suas relações de esquema, consulte os guias em [definindo campos de relação na interface](../../xdm/tutorials/relationship-ui.md#create-a-relationship-field-group) e para [relações B2B](../../xdm/tutorials/relationship-b2b.md#edit-a-b2b-schema-relationship). |

{style="table-layout:auto"}

Para obter mais informações sobre o XDM, leia a [Visão geral do sistema XDM](../../xdm/home.md).

## Serviço de identidade {#identity-service}

Use o Serviço de identidade da Adobe Experience Platform para criar uma visão abrangente dos clientes e seus comportamentos pela união de identidades entre dispositivos e sistemas, permitindo fornecer experiências digitais pessoais e impactantes em tempo real.

**Recurso atualizado**

| Recurso | Descrição |
| --- | --- |
| Disponibilidade limitada das regras de vinculação do gráfico de identidade | As regras de vinculação do gráfico de identidade são um conjunto de ferramentas no Serviço de identidade que você pode usar para garantir uma personalização precisa para seus usuários. <ul><li>Agora você pode usar o [algoritmo de otimização de identidade](../../identity-service/identity-graph-linking-rules/identity-optimization-algorithm.md) para garantir que um gráfico de identidade seja representativo de uma única pessoa e, portanto, impeça a mesclagem indesejada de identidades no Perfil do cliente em tempo real.</li><li>Configure as [prioridades de namespace](../../identity-service/identity-graph-linking-rules/namespace-priority.md) para definir a importância dos respectivos namespaces e influenciar como seus perfis são formados e segmentados.</li><li>Use a ferramenta de simulação de gráficos [&#x200B; na interface do usuário &#x200B;](../../identity-service/identity-graph-linking-rules/graph-simulation.md) para simular gráficos de identidade com configurações variadas.</li><li>Use a [interface de configurações de identidade](../../identity-service/identity-graph-linking-rules/identity-settings-ui.md) para designar seu namespace exclusivo e estabelecer prioridades para todos os namespaces em sua organização.</li><li>Consulte o [painel de identidade](../../identity-service/identity-graph-linking-rules/implementation-guide.md#validate-your-graphs) para obter as métricas e tendências relacionadas aos dados do gráfico.</li></ul> Para experimentar as regras de vinculação de gráficos de identidade, entre em contato com a equipe de conta da Adobe para obter acesso às sandboxes de desenvolvimento. |

**Documentação atualizada**

| Recurso | Descrição |
| --- | --- |
| Guia de solução de problemas para regras de vinculação de gráficos de identidade | Leia o novo [guia de solução de problemas para regras de vinculação de gráficos de identidade](../../identity-service/identity-graph-linking-rules/troubleshooting.md) para abordagens e soluções de depuração que você pode realizar para resolver problemas comuns que poderá encontrar ao trabalhar com regras de vinculação de gráficos de identidade. |
| Perguntas frequentes sobre regras de vinculação do gráfico de identidade | Leia as novas [Perguntas frequentes sobre regras de vinculação de gráficos de identidade](../../identity-service/identity-graph-linking-rules/troubleshooting.md#frequently-asked-questions) para obter uma lista de respostas às perguntas frequentes sobre a prioridade de namespace, o algoritmo de otimização de identidade e outras facetas das regras de vinculação de gráficos de identidade. |

{style="table-layout:auto"}

Para obter mais informações sobre o Serviço de identidade, leia a [Visão geral do serviço de identidade](../../identity-service/home.md).

## Query Service {#query-service}

O Query Service permite usar SQL padrão para consultar dados no [!DNL data lake] da Adobe Experience Platform. É possível unir qualquer conjunto de dados do data lake e capturar os resultados de consultas como um novo conjunto de dados para usar em relatórios, no espaço de trabalho de ciência de dados ou para assimilação no perfil do cliente em tempo real.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Públicos-alvo de dados do Distiller | Crie, gerencie e ative facilmente os públicos com a extensão de público-alvo SQL no Data Distiller da Experience Platform. Defina segmentos de público-alvo com comandos SQL diretamente do data lake, ignorando a necessidade de dados brutos em perfis. Refine as estratégias de direcionamento e sincronize automaticamente os públicos-alvo com destinos baseados em arquivos usando essa abordagem flexível e orientada por dados. Simplifique os fluxos de trabalho, otimize o gerenciamento do público-alvo e libere todo o potencial dos dados. Leia o [guia sobre como usar a extensão de público-alvo do SQL](../../query-service/data-distiller-audiences/overview.md) para elevar suas estratégias de público-alvo. |
| Estatísticas do Data Distiller - Hipercubos | Otimize a análise de big data com Hipercubos. Lidar com cálculos complexos — como contagens distintas e análise multidimensional — sem reprocessar dados históricos. Atualize dados de maneira incremental, simplifique os fluxos de trabalho e reduza o tempo de processamento, mantendo a precisão e a eficiência. Obtenha insights mais rápidos, escaláveis e econômicos que transformam a tomada de decisões. Explore o [guia sobre o uso de Hipercubos](../../query-service/hypercubes/overview.md) para desbloquear a análise avançada. |
| Navegador de objetos do Editor de consultas | Aumente a eficiência da consulta com o novo Navegador de objetos no Editor de consultas. Pesquise, filtre e acesse conjuntos de dados rapidamente para gravar e refinar consultas mais rapidamente. Com atualizações de esquema em tempo real e metadados de tabela instantâneos, você pode simplificar fluxos de trabalho, reduzir o tempo de navegação e aprimorar sua experiência de consulta. Libere o potencial de seus dados e otimize a análise. Leia o [guia sobre como usar o Pesquisador de Objetos](../../query-service/ui/user-guide.md#object-browser) para obter mais informações. |
| Computar horas | Obtenha controle sobre o uso de recursos com a métrica Horas de computação visível recentemente para consultas programadas. Visualize as Horas de computação no nível de execução da consulta para monitorar e otimizar o uso de recursos para consultas em lote CTAS/ITAS. Rastreie horas iniciais, status de conclusão e tempo de computação para cada execução de consulta. Ajuste o desempenho e reduza custos facilmente. Leia o [guia sobre Horas de Computação](../../query-service/ui/query-schedules.md#compute-hours-at-job-level) para obter informações sobre como maximizar a eficiência da sua consulta. |

{style="table-layout:auto"}

Para saber mais sobre o Serviço de consulta, leia a [Visão geral do Serviço de consulta](../../query-service/home.md).

## Serviço de segmentação {#segmentation-service}

O [!DNL Segmentation Service] define um subconjunto específico de perfis descrevendo os critérios que distinguem um grupo de pessoas na sua base de clientes que pode ser direcionado por campanhas de marketing. Os segmentos podem ser baseados em dados de registro (como informações demográficas) ou em eventos de séries temporais que representam interações de clientes com sua marca.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| ------- | ----------- |
| Atualização dos critérios de segmentação de transmissão | A partir da versão de setembro de 2024, os critérios para que seus públicos-alvo se qualifiquem para segmentação de transmissão foram atualizados. Mais informações sobre essas alterações podem ser encontradas na [atualização dos critérios de qualificação de segmentação de streaming](../../segmentation/eligibility-criteria-update.md). |
| Implementação da Pesquisa unificada | O comportamento de pesquisa no Construtor de segmentos agora usa a Pesquisa unificada. Isso permite uma experiência mais robusta ao gerenciar e pesquisar públicos para reutilização para associação de segmento. Para obter mais informações sobre esta alteração, leia o [guia do Construtor de segmentos](../../segmentation/ui/segment-builder.md#rule-builder-canvas). |

{style="table-layout:auto"}

Para obter mais informações sobre [!DNL Segmentation Service], leia a [Visão geral da segmentação](../../segmentation/home.md).

## Origens {#sources}

A Experience Platform fornece uma API RESTful e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar a sistemas de armazenamento externos e serviços de CRM, definir períodos para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

Use fontes na Experience Platform para assimilar dados de um aplicativo da Adobe ou de uma fonte de dados de terceiros.

**Recurso atualizado**

| Recurso | Descrição |
| --- | --- |
| [!BADGE Beta]{type=Informative} Suporte para assimilação de dados criptografados na interface | Agora é possível assimilar dados criptografados de uma origem em lote de armazenamento na nuvem usando o espaço de trabalho de origens na interface do usuário do Experience Platform. Leia o tutorial sobre [assimilação de dados criptografados na interface](../../sources/tutorials/ui/encryped-ingestion.md) para obter mais informações. |
| Disponibilidade Geral da origem [!DNL Snowflake Streaming] | A origem [!DNL Snowflake Streaming] agora está na disponibilidade geral. Use esta fonte para transmitir dados da sua conta do [!DNL Snowflake] para a Experience Platform. Leia a [[!DNL Snowflake Streaming] visão geral](../../sources/connectors/databases/snowflake-streaming.md)para obter mais informações. |
| Suporte para autenticação de conta de serviço em [!DNL Google BigQuery] | Agora você pode conectar sua conta do [!DNL Google BigQuery] à Experience Platform usando a autenticação de conta de serviço. Leia a [[!DNL Google BigQuery] visão geral](../../sources/connectors/databases/bigquery.md#generate-your-google-bigquery-credentials) para obter mais informações. <br> ![Imagem da interface do usuário do Experience Platform destacando a opção Editar agendamento e pastas na etapa de agendamento.](../2024/assets/september/service_auth.png "Autenticação de serviço para o Google BigQuery."){width="250" align="center" zoomable="yes"} |
| Suporte para ignorar a pré-visualização de dados de amostra | Agora é possível optar por ignorar a visualização de dados ao criar uma conexão de origem com as seguintes origens: <ul><li>[[!DNL Google BigQuery]](../../sources/tutorials/ui/create/databases/bigquery.md#skip-preview-of-sample-data)</li><li>[[!DNL Salesforce]](../../sources/tutorials/ui/create/crm/salesforce.md#skip-preview-of-sample-data)</li><li>[[!DNL Snowflake]](../../sources/tutorials/ui/create/databases/snowflake.md#skip-preview-of-sample-data)</li></ul> Você pode ignorar a visualização de dados para contornar um tempo limite que pode ocorrer ao assimilar dados de lotes grandes. Isso pode impedir a validação automática dos campos calculados e obrigatórios. Se optar por ignorar a visualização de dados, talvez seja necessário validar manualmente os campos calculados e obrigatórios durante o mapeamento. |
| Suporte para desabilitar o agrupamento em [!DNL SFTP] | Agora você pode definir uma configuração que permita desabilitar o agrupamento na origem [!DNL SFTP]. Leia a [[!DNL SFTP] visão geral](../../sources/connectors/cloud-storage/sftp.md) para obter mais informações. |

{style="table-layout:auto"}

Para obter mais informações, leia a [visão geral de fontes](../../sources/home.md).
