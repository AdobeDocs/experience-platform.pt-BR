---
title: Notas de versão da Adobe Experience Platform
description: As notas de versão mais recentes do Adobe Experience Platform.
source-git-commit: 74e2ebd324265744702a385dbaca2ac4a10ea1f7
workflow-type: tm+mt
source-wordcount: '959'
ht-degree: 6%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 26 de janeiro de 2022**

Atualizações dos recursos existentes na Adobe Experience Platform:

- [Alertas](#alerts)
- [[!DNL Data Prep]](#data-prep)
- [[!DNL Dashboards]](#dashboards)
- [Serviço de query](#query-service)
- [Sandboxes](#sandboxes)
- [Serviço de segmentação](#segmentation)
- [Fontes](#sources)

## Alertas {#alerts}

O Experience Platform permite assinar alertas baseados em eventos para várias atividades da plataforma. É possível assinar diferentes regras de alerta por meio do [!UICONTROL Alertas] na interface do usuário da plataforma e pode optar por receber mensagens de alerta na própria interface do usuário ou por meio de notificações por email.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Novas regras de alerta | Várias novas regras de alerta estão disponíveis para fluxos de trabalho relacionados à assimilação de dados, identidades, perfis, segmentação e ativação. Consulte a visão geral em [regras de alerta](../../observability/alerts/rules.md) para obter a lista atualizada de tipos de alertas. |
| Alertas no contexto para fluxos de dados de fontes | Agora você pode se inscrever para receber mensagens de alerta sobre o status dos seus fluxos de dados durante o fluxo de trabalho de assimilação. Para obter mais informações, consulte o guia sobre [inscrição em alertas de origens na interface do usuário](../../sources/tutorials/ui/alerts.md). |

Para obter mais informações sobre alertas na Platform, consulte [visão geral dos alertas](../../observability/alerts/overview.md).

## [!DNL Dashboards] {#dashboards}

O Adobe Experience Platform fornece vários painéis através dos quais você pode visualizar insights importantes sobre os dados de sua organização, conforme capturados durante os instantâneos diários.

| Recurso | Descrição |
| --- | --- |
| Legendas inteligentes | Um algoritmo de aprendizado de máquina fornece automaticamente insights sobre seu perfil e dados de público-alvo e ilustra padrões e tendências em um período de 30 a 90 dias ou 12 meses. As legendas incluem informações sobre <ul><li>Forma e estatísticas gerais</li><li>Tendências e alterações abruptas</li><li>Padrões sazonais</li><li>Anomalias inesperadas</li></ul> Mais informações podem ser encontradas no [painéis de perfis](../../dashboards/guides/profiles.md#profiles-count-trend) e [painéis de segmentos](../../dashboards/guides/segments.md#audience-size-trend) documentação. |
| Inventário de painéis | Acesse os relatórios pré-configurados de painéis de perfil, segmentos e destinos, incluindo quaisquer integrações instaladas, como Power BI, em um local centralizado. Para obter mais informações, consulte o [[!DNL Dashboards] visão geral](../../dashboards/home.md). |
| Modelos de relatório do Power BI | Crie, personalize ou estenda métricas do perfil, segmentos e modelos de dados de relatório de destino usando novos gráficos do Power BI. O fluxo de trabalho de instalação automatizada permite compartilhar seus insights de marketing em sua organização a partir do ambiente Power BI. Para obter mais informações, consulte o [[!DNL Dashboards] visão geral](../../dashboards/home.md). |

Para obter mais informações sobre [!DNL Dashboards]consulte o [[!DNL Dashboards] visão geral](../../dashboards/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] O permite que os engenheiros de dados mapeiem, transformem e validem dados de e para o Experience Data Model (XDM).

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Experiência de mapeamento consolidado | A nova interface de mapeamento na interface do usuário da plataforma fornece uma experiência de mapeamento consistente para aproveitar as recomendações de mapeamento inteligente, configurar manualmente as regras de mapeamento e depurar todos os erros que ocorrerem nos conjuntos de mapeamento. Para obter mais informações, consulte o [[!DNL Data Prep] Guia da interface do usuário](../../data-prep/ui/mapping.md). |

Para obter mais informações sobre [!DNL Data Prep]consulte o [[!DNL Data Prep] visão geral](../../data-prep/home.md).

## Serviço de query {#query-service}

[!DNL Query Service] permite usar o SQL padrão para consultar dados no Adobe Experience Platform [!DNL Data Lake]. É possível unir qualquer conjunto de dados da [!DNL Data Lake] e capture os resultados do query como um novo conjunto de dados para usar nos relatórios, no Data Science Workspace ou para assimilação no Perfil do cliente em tempo real.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Bloco Anônimo | A construção SQL de bloco anônimo permite dividir tarefas de preparação de dados em grande escala no Serviço de Consulta em tarefas menores, reutilizá-las e executá-las em sequência para carregamento de dados incrementais. Para obter mais informações, consulte o [Visão geral do Serviço de query](../../query-service/home.md). |
| Organização do conjunto de dados | Fornece uma estrutura de dados lógica e coerente para organizar seus ativos de dados para uso com o Serviço de query, à medida que a quantidade de ativos de dados na sandbox cresce. Para obter mais informações, consulte o [Visão geral do Serviço de query](../../query-service/home.md). |

Para obter mais informações sobre [!DNL Query Service]consulte o [[!DNL Query Service] visão geral](../../query-service/home.md).

## Sandboxes {#sandboxes}

O Adobe Experience Platform foi criado para enriquecer os aplicativos de experiência digital em escala global. Geralmente, as empresas executam vários aplicativos de experiência digital em paralelo e precisam atender ao desenvolvimento, teste e implantação desses aplicativos, além de garantir a conformidade operacional. Para atender a essa necessidade, o Experience Platform fornece sandboxes que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Aprimoramentos da interface do usuário de sandboxes | O indicador sandbox agora é integrado no cabeçalho para todos os aplicativos da interface do usuário da plataforma. O indicador sandbox exibe o nome, a região e o tipo da sandbox e também permite acessar um menu suspenso para alternar entre sandboxes. Para obter mais informações, consulte o [guia da interface do usuário da sandbox](../../sandboxes/ui/user-guide.md). |

Para obter mais informações sobre sandboxes, consulte o [visão geral das sandboxes](../../sandboxes/home.md).

## Serviço de segmentação {#segmentation}

[!DNL Segmentation Service] O define um subconjunto específico de perfis ao descrever os critérios que distinguem um grupo comercializável de pessoas dentro da base do cliente. Os segmentos podem se basear em dados de registro (como informações demográficas) ou em eventos de séries cronológicas que representem as interações do cliente com sua marca.

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Correspondência de segmentos | Correspondência de segmentos é um serviço de colaboração de dados que permite que dois ou mais usuários da plataforma troquem dados, com base em identificadores comuns, de forma segura, regida e compatível com a privacidade. A Correspondência de segmentos usa padrões de privacidade da plataforma e identificadores pessoais, como emails com hash, números de telefone com hash e identificadores de dispositivo, como IDFAs e GAIDs. Para obter mais informações, consulte o [Visão geral da Correspondência de segmento](../../segmentation/ui/segment-match/overview.md). |

Para obter mais informações sobre [!DNL Segmentation Service]consulte o [Visão geral da segmentação](../../segmentation/home.md).

## Fontes {#sources}

A Adobe Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, permitir estruturar, rotular e aprimorar esses dados usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

O Experience Platform fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e se conectar a sistemas de armazenamento externos e serviços CRM, definir horários para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

| Recurso | Descrição |
| --- | --- |
| Fontes beta movendo-se para GA | As seguintes fontes foram promovidas de beta para GA: <ul><li>[[!DNL Snowflake]](../../sources/connectors/databases/snowflake.md)</li><li>[[!DNL Veeva CRM]](../../sources/connectors/crm/veeva.md)</li></ul> |
| [!DNL Event Hubs] melhorias na fonte | O [!DNL Event Hubs] A fonte agora oferece suporte ao tipo de autenticação de chave SAS não raiz para conexão e criação de conexão de origem. Para obter mais informações, consulte o [[!DNL Event Hubs] visão geral](../../sources/connectors/cloud-storage/eventhub.md). |
| [!DNL SFTP] melhorias na fonte | O [!DNL SFTP] A fonte agora permite estabelecer um número definido de um número máximo de conexões simultâneas que um fluxo de dados pode usar para se conectar ao servidor SFTP. Para obter mais informações, consulte o [[!DNL SFTP] visão geral](../../sources/connectors/cloud-storage/sftp.md). |