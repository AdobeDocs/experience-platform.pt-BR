---
title: Notas de versão da Adobe Experience Platform de agosto de 2022
description: As notas de versão de agosto de 2022 para o Adobe Experience Platform.
source-git-commit: b8513fa214ea74eec6809796cc194466e05cbb21
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 6%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 24 de agosto de 2022**

Atualizações dos recursos existentes na Adobe Experience Platform:

- [Preparação de dados](#data-prep)
- [Fontes](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] O permite que os engenheiros de dados mapeiem, transformem e validem dados de e para o Experience Data Model (XDM).

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Suporte para assimilar registros com avisos | A Preparação de dados agora localiza avisos (erros não críticos) nos campos e permitirá que o restante da linha seja assimilado. Todos os erros de transformação do mapeador agora são relatados como avisos e linhas que são parcialmente assimiladas são consideradas bem-sucedidas, com um aviso.  Também há suporte para monitoramento em registros com avisos e detalhes de diagnóstico. A assimilação parcial de registros com avisos está atualmente disponível apenas para dados de transmissão. Revise a documentação em [assimilação de registros com avisos](../../sources/tutorials/ui/monitor-streaming.md) para obter mais informações. |

{style=&quot;table-layout:auto&quot;}

Para saber mais sobre [!DNL Data Prep], consulte o [[!DNL Data Prep] visão geral](../../data-prep/home.md).

## Fontes {#sources}

A Adobe Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, permitir estruturar, rotular e aprimorar esses dados usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

O Experience Platform fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e se conectar a sistemas de armazenamento externos e serviços CRM, definir horários para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Disponibilidade geral de fontes de autoatendimento (SDK em lote) | Desenvolva, teste e integre sua fonte de dados baseada em REST API para assimilar dados em lote no Experience Platform usando as especificações de origem fáceis de configurar. Com o SDK de fontes, é possível: <ul><li>Configure uma nova fonte para o catálogo de Experience Platform.</li><li>Defina as especificações para a sua fonte, incluindo informações relacionadas aos tipos de autenticação suportados, programação e como os dados de recursos são buscados.</li><li>Crie uma documentação voltada para o usuário para sua nova fonte.</li></ul> Para obter mais informações, leia a documentação em [Fontes de autoatendimento (SDK em lote)](../../sources/sources-sdk/overview.md). |
| Disponibilidade geral [!DNL Google BigQuery] source | Use o [!DNL Google BigQuery] fonte para assimilar dados da sua [!DNL Google BigQuery] data warehouse para Experience Platform. Para obter mais informações, leia a documentação sobre o [[!DNL Google BigQuery] source](../../sources/connectors/databases/bigquery.md). |
| [!DNL Teradata Vantage] fonte (Beta) | Use o [!DNL Teradata Vantage] origem para assimilar dados de ambientes híbridos de várias nuvens para o Experience Platform. Para obter mais informações, leia a documentação sobre o [[!DNL Teradata Vantage] source](../../sources/connectors/databases/teradata-vantage.md). |
| Suporte entre regiões para origem do Adobe Analytics | Agora é possível assimilar conjuntos de relatórios de qualquer região (Estados Unidos, Reino Unido ou Cingapura). Os conjuntos de relatórios devem ser mapeados para a mesma organização da instância Sandbox do Experience Platform na qual a conexão de origem está sendo criada. Para obter mais informações, leia o guia sobre [criação de uma conexão de origem do Adobe Analytics na interface do usuário](../../sources/tutorials/ui/create/adobe-applications/analytics.md). |
| Suporte a API para assimilação sob demanda | Use a assimilação sob demanda para criar execuções de fluxo ad hoc para um determinado fluxo de dados com o [!DNL Flow Service] API. As execuções de fluxo criadas devem ser definidas para assimilação única. Para obter mais informações, leia o guia sobre [criação de uma execução de fluxo para assimilação sob demanda usando a API](../../sources/tutorials/api/on-demand-ingestion.md) para obter mais informações. |

{style=&quot;table-layout:auto&quot;}

Para saber mais sobre fontes, consulte o [visão geral das fontes](../../sources/home.md).
