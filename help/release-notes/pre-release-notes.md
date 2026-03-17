---
title: Notas de pré-lançamento do Experience Platform
description: Uma visualização das notas de versão mais recentes do Adobe Experience Platform.
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: efa50881315d986940f7cb3afcbfcc30ef67c3a7
workflow-type: tm+mt
source-wordcount: '1411'
ht-degree: 14%

---

# Notas de pré-lançamento do Adobe Experience Platform

>[!IMPORTANT]
>
>Este documento é uma **visualização** das notas de versão do mês atual. Os itens da versão estão sujeitos a alterações e podem ser adicionados ou removidos na versão final.

>[!TIP]
>
>Consulte a documentação a seguir para obter as notas de versão de outros aplicativos da Adobe Experience Platform:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/releases/latest)
>- [Composição de público-alvo federado](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/en/docs/real-time-cdp-collaboration/using/latest)

**Data de lançamento: março de 2026**

Novos recursos e atualizações dos recursos existentes no Adobe Experience Platform:

- [Gerenciamento avançado do ciclo de vida de dados](#advanced-data-lifecycle-management)
- [Agent Orchestrator](#agent-orchestrator)
- [Destinos](#destinations)
- [Serviço de consultas](#query-service)
- [Perfil do cliente em tempo real](#profile)
- [Executar e operar](#run-and-operate)
- [Serviço de segmentação](#segmentation-service)
- [Fontes](#sources)

## Gerenciamento avançado do ciclo de vida de dados {#advanced-data-lifecycle-management}

O Experience Platform fornece um conjunto de recursos de higiene de dados que permitem gerenciar os dados armazenados por meio de exclusões programáticas de registros e conjuntos de dados do consumidor. Usando o espaço de trabalho Ciclo de vida dos dados na interface do usuário ou por meio de chamadas para a API de higiene de dados, você pode gerenciar com eficiência seus armazenamentos de dados. Use esses recursos para garantir que as informações sejam usadas conforme esperado, sejam atualizadas quando dados incorretos precisarem de correção e sejam excluídas quando as políticas organizacionais considerarem necessário.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Exclusão de registro de vários conjuntos de dados e somente perfil (somente API) | Você pode enviar uma única ID de conjunto de dados, uma lista separada por vírgulas de IDs de conjunto de dados ou o literal `ALL` em `datasetId` para excluir identidades em um, em vários ou em todos os conjuntos de dados. Você também pode limitar a exclusão aos serviços de perfil definindo `targetServices` como `["identity","profile","ajo"]`, o que deixa o datalake inalterado. Consulte o [guia de Registrar Ordens de Serviço de Exclusão](../hygiene/api/workorder.md) para obter mais detalhes. |

{style="table-layout:auto"}

Para obter mais informações, leia a [visão geral avançada do gerenciamento do ciclo de vida dos dados](../hygiene/home.md).

## Agent Orchestrator {#agent-orchestrator}

O Agent Orchestrator permite criar e implantar agentes alimentados por IA que podem automatizar fluxos de trabalho e interagir com clientes em vários canais.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Adobe Marketing Agent para [!DNL Microsoft 365 Copilot] | O Adobe Marketing Agent para [!DNL Microsoft 365 Copilot] é seu agente incorporado que traz a inteligência de marketing da Adobe diretamente para as ferramentas do dia a dia, como [!DNL Teams], [!DNL Word], [!DNL PowerPoint] e outros aplicativos do [!DNL Microsoft 365]. Você pode usar esse agente para obter insights de campanha confiáveis dos aplicativos da Adobe enquanto planeja campanhas, revisa públicos ou colabora com colegas, responde a perguntas de clientes e toma decisões com base em dados sem sair do fluxo de trabalho do [!DNL Microsoft 365]. |

{style="table-layout:auto"}

Para obter mais informações, consulte a [documentação do Agent Orchestrator](https://experienceleague.adobe.com/pt-br/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator).

## Destinos {#destinations}

[!DNL Destinations] são integrações pré-criadas com plataformas de destino que permitem a ativação contínua de dados do Experience Platform. É possível usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas de email, publicidade direcionada e muitos outros casos de uso.

**Destinos novos ou atualizados**

| Destino | Descrição |
| --- | --- |
| Suporte a várias regiões para [Snowflake Streaming](../destinations/catalog/warehouses/snowflake.md) | O conector de transmissão Snowflake agora está disponível para clientes fora da região US VA7. Use o seletor suspenso de região para selecionar em qual região do Snowflake sua conta está. A documentação foi atualizada com a estrutura de dados esperada para as tabelas de transmissão do Snowflake. |
| Seletor de região [Snowflake Streaming](../destinations/catalog/warehouses/snowflake.md) e [Snowflake Batch](../destinations/catalog/warehouses/snowflake-batch.md) | Agora é possível encontrar sua região mais facilmente com a nova lista suspensa pesquisável, que combina pesquisa e lista suspensa em um controle. |
| Exportar metadados de público-alvo para [Destinos do Lote Snowflake](../destinations/catalog/warehouses/snowflake-batch.md) | Os arquivos exportados para esse destino agora incluem metadados de público-alvo. A nova estrutura da tabela se aplica a todas as novas conexões de destino configuradas dali em diante. A estrutura da tabela antiga será mantida por mais três meses antes de ser descontinuada. |
| [!DNL Adobe Advertising Cloud DSP] conexão | A nova conexão do Adobe Advertising DSP oferece a mesma funcionalidade da conexão herdada, além de suporte para identidades adicionais. |
| Suporte a público-alvo externo para [o CRM da Trade Desk](../destinations/catalog/advertising/tradedesk-emails.md), [Critério](../destinations/catalog/advertising/criteo.md) e [Pinterest](../destinations/catalog/advertising/pinterest.md) | Agora é possível ativar públicos-alvo além dos segmentos do Serviço de segmentação para o Trade Desk CRM, Critério e Pinterest, incluindo públicos-alvo de upload personalizados (importados do CSV), públicos-alvo semelhantes, públicos-alvo federados e públicos-alvo criados em outros aplicativos da Experience Platform, como o Adobe Journey Optimizer. Consulte a seção [públicos-alvo suportados](../destinations/catalog/advertising/criteo.md#supported-audiences) na página do catálogo de cada destino para obter detalhes. |
| Filtragem de público-alvo no fluxo de trabalho de ativação | Agora é possível encontrar e filtrar públicos-alvo na etapa **[!UICONTROL Select audiences]** com a mesma experiência da página Públicos-alvo; por exemplo, você pode filtrar por origem de público-alvo para encontrar facilmente o público-alvo que está procurando. |
| Aumento do limite de públicos-alvo de upload personalizado | Agora você pode ativar até 20 públicos-alvo de upload personalizados por instância de destino. Anteriormente, esse limite era de 10. |
| [Exportar arquivo agora](../destinations/ui/export-file-now.md) e [suporte à API de ativação ad hoc](../destinations/api/ad-hoc-activation-api.md) para públicos externos | Agora você pode usar o Export file now (UI) e a API de ativação ad-hoc com públicos externos (como upload personalizado, semelhante, federado e públicos de outros aplicativos da Experience Platform) ao ativar para destinos baseados em arquivo em lote. |
| Destinos da API HTTP com OAuth 2 e mTLS | Agora é possível criar e autenticar destinos da API HTTP que usam o OAuth 2 quando o endpoint de autenticação requer TLS mútuo (mTLS). A recuperação de token durante a configuração do destino agora oferece suporte a mTLS. |
| Destino da conta ZoomInfo | Agora você pode enviar públicos-alvo da conta para ZoomInfo do Real-Time Customer Data Platform (B2B). |

{style="table-layout:auto"}

**Correções e melhorias**

| Correção | Descrição |
| --- | --- |
| Validação da ID da conta de [Streaming do Snowflake](../destinations/catalog/warehouses/snowflake.md) | Um validador de expressão regular foi adicionado à etapa ID da conta. Ao inserir sua ID, ela agora é validada para garantir que a ID da organização e a ID da conta estejam no formato correto (separadas por um ponto). |
| hash do número de telefone do conector [TikTok](../destinations/catalog/social/tiktok.md) | Correção de um problema em que uma configuração incorreta no cartão de destino significava que as identidades destacadas de números de telefone não eram ativadas para o TikTok. |

{style="table-layout:auto"}

Para obter mais informações, leia a [Visão geral dos Destinos](../destinations/home.md).

## Perfil do cliente em tempo real {#profile}

A Adobe Experience Platform permite gerar experiências coordenadas, consistentes e relevantes para seus clientes, independentemente de onde ou quando eles interagem com sua marca. Com o Perfil do cliente em tempo real, você pode ter uma visualização integral de cada cliente individual, combinando dados de vários canais, inclusive dados online, offline, de CRM e de terceiros.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Seletor de tempo de eventos do perfil | Agora você pode definir uma janela de tempo na guia de eventos do perfil para exibir e analisar eventos dentro desse intervalo. Você pode definir a janela de tempo para até 30 dias. Por padrão, ele mostra eventos das últimas 48 horas. |

{style="table-layout:auto"}

Para obter mais informações, leia a [Visão geral do Perfil do cliente em tempo real](../profile/home.md).

## Serviço de consultas {#query-service}

O Serviço de consultas permite usar SQL padrão para consultar dados no [!DNL Data Lake] da Adobe Experience Platform. Você pode ingressar em qualquer conjunto de dados do [!DNL Data Lake] e capturar os resultados da consulta como um novo conjunto de dados para usar em relatórios, no Data Science Workspace ou para assimilação no Perfil do cliente em tempo real.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Data Distiller Accelerators | Agora você pode escolher um acelerador na guia Aceleradores, inserir os parâmetros necessários e executar ou agendar o SQL gerado sem gravá-lo sozinho; clonar qualquer acelerador em um modelo personalizado para editar. |

{style="table-layout:auto"}

Para obter mais informações, leia a [Visão geral do Serviço de consulta](../query-service/home.md).

## Executar e operar {#run-and-operate}

Inspecione, solucione problemas e otimize suas implementações do Experience Platform com as ferramentas Executar e Operar. Obtenha visibilidade sobre ativações programadas em lote, identifique problemas de configuração e melhore a confiabilidade do sistema.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| [Calendários de Trabalho](../run-and-operate/job-schedules.md) disponibilidade geral | O [!DNL Job Schedules] fornece uma exibição unificada de todos os trabalhos agendados de processamento em lote em seu pipeline de dados, desde a assimilação até a ativação de destino. Inspecione o status da execução, identifique conflitos de agendamento e diagnostique problemas de configuração antes que eles afetem as operações de negócios. |
| Verificações de integridade disponibilidade geral | Configurações insatisfatórias de esquema e identidade levam a problemas significativos de downstream, incluindo criação incorreta de perfis, falha na qualificação de segmentos e ativação imprecisa. <br>As verificações de integridade alteram sua abordagem da solução de problemas reativa para a manutenção proativa e preventiva. As verificações de integridade são verificações sempre ativas de seus esquemas e identidades usados em sua sandbox e fornecem um resumo dos problemas que você pode usar para explorar e solucionar problemas. |

{style="table-layout:auto"}

Para obter mais informações, leia a [Visão geral de Execução e Operação](../run-and-operate/overview.md), [Inspecionar agendas de trabalho](../run-and-operate/job-schedules.md) e o [guia da Interface do Usuário da Plataforma](../landing/ui-guide.md).

## Serviço de segmentação {#segmentation}

O Experience Platform permite criar segmentos de público-alvo com base nos dados do cliente e o gerenciamento do ciclo de vida completo desses públicos-alvo.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Origem da assimilação no Audience Builder | Agora é possível ver se cada atributo vem de um lote, transmissão ou fonte de borda dentro do Audience Builder para evitar a criação de públicos de transmissão inválidos ou ineficientes. |
| Mostrar apenas campos com dados no Construtor de público-alvo da conta | Agora é possível filtrar para mostrar somente atributos que contêm dados ao criar públicos-alvo da conta. |

{style="table-layout:auto"}

Para obter mais informações, leia a [Visão geral dos públicos-alvo](../segmentation/home.md).

## Fontes {#sources}

A Experience Platform fornece uma API RESTful e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar a sistemas de armazenamento externos e serviços de CRM, definir períodos para execuções de ingestão e gerenciar a taxa de transferência de ingestão de dados.

**Fontes novas ou atualizadas**

| Fonte | Descrição |
| --- | --- |
| Suporte aprimorado para a captura de dados do Change | Agora você pode usar o Change Data Capture com as fontes [!DNL Marketo Engage], [!DNL Microsoft Dynamics] e [!DNL Salesforce CRM]. |

{style="table-layout:auto"}

Para obter mais informações, leia a [visão geral de fontes](../sources/home.md).

<!--

| [!DNL Deltashare] | The new [!DNL Deltashare] source lets you securely bring live, shared datasets from your partners or internal lakehouse environments directly into Adobe's applications without copying or manually uploading files. You connect to a [!DNL Deltashare] endpoint, choose the tables you need, and you can then use that governed, up-to-date data alongside your existing profiles and insights, so you spend less time on data wrangling and more time activating and analyzing it in your marketing workflows. |
| [!DNL Kobie] | The new [!DNL Kobie] source connector lets you directly ingest rich loyalty data from [!DNL Kobie] into Adobe's applications, so you can activate it alongside your existing customer profiles and insights. You connect your [!DNL Kobie] environment, configure the data objects you want to bring in (such as member status, transactions, and engagement), and then you can use that up-to-date loyalty information to build audiences, personalize experiences, and measure performance without juggling separate systems. |
| [!DNL Talon.One] | The new Talon.One source lets you seamlessly bring promotion and incentive data from Talon.One into Adobe's applications, so you can use it alongside your existing customer profiles and behavioral data. You connect your Talon.One account, select the entities and events you want to ingest (such as campaigns, coupons, and redemptions), and then you can use that real-time promotion context to build smarter audiences, personalize offers, and better understand which incentives are driving performance—without managing separate, disconnected systems. |

-->

<!--

| Data Engineering Agent | The following new and updated skills are available in the Data Engineering Agent:<br><br><ul><li><strong>Data onboarding:</strong> Follow step-by-step workflows and example prompts to connect sources, check data quality, enrich data semantically, and ingest data for B2C and B2B flows, with expected outputs and troubleshooting guidance in the docs.</li><li><strong>Data quality and validation:</strong> Validate data fields and datasets using two new skills (DataField and DataSet).</li><li><strong>Data collection:</strong> Get in-context guidance for complex Data Collection configurations and use conversational insights to explore lineage, dependencies, and relationships across your data collection objects.</li></ul> |

-->