---
title: Notas da versão de janeiro de 2022 da Adobe Experience Platform
description: As notas da versão de janeiro de 2022 da Adobe Experience Platform.
exl-id: 734ce1b3-e270-4c37-958c-88bcc39fbf20
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1344'
ht-degree: 20%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: quinta-feira, 26 de janeiro de 2022**

Atualizações dos recursos já existentes na Adobe Experience Platform:

- [Alertas](#alerts)
- [[!DNL Dashboards]](#dashboards)
- [[!DNL Data Prep]](#data-prep)
- [[!DNL Destinations]](#destinations)
- [Query Service](#query-service)
- [Sandboxes](#sandboxes)
- [Serviço de segmentação](#segmentation)
- [Origens](#sources)

## Alertas {#alerts}

O Experience Platform permite assinar alertas baseados em eventos para várias atividades do Experience Platform. Você pode assinar diferentes regras de alerta por meio da guia [!UICONTROL Alertas] na interface do usuário do Experience Platform e pode optar por receber mensagens de alerta na própria interface ou por meio de notificações por email.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Novas regras de alerta | Várias novas regras de alerta agora estão disponíveis para fluxos de trabalho relacionados à assimilação de dados, identidades, perfis, segmentação e ativação. Consulte a visão geral em [regras de alerta](../../observability/alerts/rules.md) para obter a lista atualizada dos tipos de alerta. |
| Alertas em contexto para fluxos de dados de origens | Agora você pode se inscrever para receber mensagens de alerta sobre o status dos fluxos de dados durante o fluxo de trabalho de assimilação. Para obter mais informações, consulte o manual sobre [assinatura de alertas de fontes na interface](../../sources/tutorials/ui/alerts.md). |

Para obter mais informações sobre alertas no Experience Platform, consulte a [visão geral dos alertas](../../observability/alerts/overview.md).

## [!DNL Dashboards] {#dashboards}

A Adobe Experience Platform fornece vários painéis para você visualizar insights importantes sobre os dados de sua organização, que são capturados por instantâneos diários.

| Recurso | Descrição |
| --- | --- |
| Legendas inteligentes | Um algoritmo de aprendizado de máquina fornece automaticamente insights sobre seus dados de perfil e público-alvo e ilustra padrões e tendências ao longo de um período de 30 a 90 dias ou 12 meses. As legendas incluem informações sobre <ul><li>Forma geral e estatísticas</li><li>Tendências e alterações bruscas</li><li>Padrões sazonais</li><li>Anomalias inesperadas</li></ul> Mais informações podem ser encontradas na documentação dos [painéis de perfis](../../dashboards/guides/profiles.md#profiles-count-trend) e [painéis de segmentos](../../dashboards/guides/audiences.md#audience-size-trend). |
| Inventário de painéis | Acesse os relatórios pré-configurados de painéis de perfil, segmentos e destinos, incluindo qualquer integração instalada, como o Power BI, em um local centralizado. Para obter mais informações, consulte a [[!DNL Dashboards] documentação do inventário](../../dashboards/inventory.md). |
| Modelos de relatório do Power BI | Crie, personalize ou estenda métricas dos modelos de dados de relatório de perfil, segmentos e destino usando novos gráficos do Power BI. O fluxo de trabalho de instalação automatizada permite compartilhar seus insights de marketing em toda a organização no ambiente do Power BI. Para obter mais informações, consulte a [documentação do modelo de relatório do Power BI](../../dashboards/integrations/power-bi.md). |

Para obter mais informações sobre [!DNL Dashboards], consulte a [[!DNL Dashboards] visão geral](../../dashboards/home.md).

## [!DNL Data Prep] {#data-prep}

O [!DNL Data Prep] permite que os engenheiros de dados mapeiem, transformem e validem dados de e para o Experience Data Model (XDM).

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Experiência de mapeamento consolidada | A nova interface de mapeamento na interface do Experience Platform fornece uma experiência de mapeamento consistente para aproveitar as recomendações de mapeamento inteligentes, configurar regras de mapeamento manualmente e depurar quaisquer erros que ocorram em seus conjuntos de mapeamento. Para obter mais informações, consulte o [[!DNL Data Prep] guia da interface](../../data-prep/ui/mapping.md). |

Para obter mais informações sobre [!DNL Data Prep], consulte a [[!DNL Data Prep] visão geral](../../data-prep/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] são integrações pré-construídas com plataformas de destino que permitem a ativação perfeita de dados da Adobe Experience Platform. É possível usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas de email, publicidade direcionada e muitos outros casos de uso.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| ----------- | ----------- |
| Personalização de mesma página e próxima página | O [recurso de personalização de mesma página e próxima página](../../destinations/ui/activate-edge-personalization-destinations.md) fornece uma exibição compartilhada e direcionável dos usuários para aplicativos na Edge Network, para fins de consistência entre canais de marketing e clientes. Essa personalização é possível por meio da [conexão do Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) e da [conexão de personalização personalizada](../../destinations/catalog/personalization/custom-personalization.md). Para configurar suas campanhas de personalização de mesma página ou próxima página, consulte o [tutorial dedicado](../../destinations/ui/activate-edge-personalization-destinations.md). |
| Monitoramento de destino em lote e métricas em nível de segmento | A funcionalidade de monitoramento de destino agora é expandida dos destinos de transmissão para também incluir destinos em lote e métricas no nível de segmento para seus fluxos de dados de ativação. Para obter mais informações, leia o [painel de destinos do monitoramento](/help/dataflows/ui/monitor-destinations.md#monitoring-destinations-dashboard), o [painel de trabalhos do segmento de monitoramento](/help/dataflows/ui/monitor-destinations.md#monitoring-segment-jobs-dashboard) e a [exibição no nível do segmento](/help/dataflows/ui/monitor-destinations.md#segment-level-view). |
| Programar edição na interface do usuário para fluxos de dados de ativação em lote existentes | Esta versão apresenta a opção de editar a programação dos fluxos de dados de ativação existentes para destinos em lote. Para obter mais informações, leia [ativar dados de perfil para destinos de perfil em lote](/help/destinations/ui/activate-batch-profile-destinations.md). |
| Aprimoramentos no destino do Marketo | Os clientes da Experience Platform que usam o Marketo Engage podem maximizar seu banco de dados do Marketo com a nova capacidade de enviar registros de novas pessoas para o Marketo Engage a partir do Experience Platform por meio do [conector de destino do Marketo](/help/destinations/catalog/adobe/marketo-engage.md). <br> Ao enviar segmentos de público-alvo do Experience Platform para o Marketo Engage, as pessoas dentro do segmento que ainda não existe no banco de dados do Marketo Engage podem ser adicionadas automaticamente a ele. Para obter mais informações, leia [Enviar um segmento do Adobe Experience Platform para uma lista estática do Marketo](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-platform-segment-to-a-marketo-static-list.html?lang=pt-BR) (a etapa 9 do tutorial indica como enviar registros de novas pessoas para o Marketo). |

**Novos destinos**

| Destino | Descrição |
| ----------- | ----------- |
| [conexão com o Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) | O Adobe Target é um aplicativo que fornece personalização e experimentação em tempo real e alimentadas por IA em todas as interações de entrada de clientes em sites, aplicativos móveis e muito mais. O Adobe Target é uma conexão de personalização no Adobe Experience Platform. |
| [Conexão de personalização personalizada](../../destinations/catalog/personalization/custom-personalization.md) | Essa conexão de personalização fornece uma maneira de recuperar informações de segmento do Adobe Experience Platform para plataformas de personalização externas, sistemas de gerenciamento de conteúdo, servidores de anúncios e outros aplicativos que estão sendo executados nos sites do cliente. |

Para obter informações mais gerais sobre destinos, consulte a [visão geral de destinos](../../destinations/home.md).

## Query Service {#query-service}

[!DNL Query Service] permite que você use o SQL padrão para consultar dados no Adobe Experience Platform [!DNL Data Lake]. Você pode ingressar em qualquer conjunto de dados do [!DNL Data Lake] e capturar os resultados da consulta como um novo conjunto de dados para usar em relatórios, no Data Science Workspace ou para assimilação no Perfil do cliente em tempo real.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Bloqueio anônimo | A construção anônima de bloco SQL permite dividir trabalhos de preparação de dados em larga escala no Serviço de Consulta em tarefas menores e, em seguida, reutilizá-los e executá-los em sequência para carregamento de dados incrementais. Para obter mais informações, consulte as [consultas de exemplo para a documentação de blocos anônimos](../../query-service/key-concepts/anonymous-block.md). |
| Organização do conjunto de dados | Fornece uma estrutura de dados coerente e lógica para organizar seus ativos de dados para uso com o Serviço de consulta à medida que a quantidade de ativos de dados na sandbox cresce. Para obter mais informações, consulte a [documentação sobre a organização de ativos de dados](../../query-service/best-practices/organize-data-assets.md). |

Para obter mais informações sobre [!DNL Query Service], consulte a [[!DNL Query Service] visão geral](../../query-service/home.md).

## Sandboxes {#sandboxes}

O Adobe Experience Platform foi criado para enriquecer aplicativos de experiência digital em escala global. As empresas geralmente executam vários aplicativos de experiência digital em paralelo e precisam atender ao desenvolvimento, ao teste e à implantação desses aplicativos enquanto garantem a conformidade operacional. Para atender a essa necessidade, a Experience Platform fornece sandboxes que particionam uma única instância do Experience Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Aprimoramentos na interface do usuário de sandboxes | Agora, o indicador da sandbox está integrado no cabeçalho para todos os aplicativos de interface do usuário do Experience Platform. O indicador da sandbox exibe o nome, a região e o tipo da sandbox e também permite acessar um menu suspenso para alternar entre sandboxes. Para obter mais informações, consulte o [guia da interface do usuário da sandbox](../../sandboxes/ui/user-guide.md). |

Para obter mais informações sobre sandboxes, consulte a [visão geral das sandboxes](../../sandboxes/home.md).

## Serviço de segmentação {#segmentation}

O [!DNL Segmentation Service] define um subconjunto específico de perfis descrevendo os critérios que distinguem um grupo de pessoas na sua base de clientes que pode ser direcionado por campanhas de marketing. Os segmentos podem ser baseados em dados de registro (como informações demográficas) ou em eventos de séries temporais que representam interações de clientes com sua marca.

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Correspondência de segmentos | A Correspondência de segmentos é um serviço de colaboração de dados que permite que dois ou mais usuários do Experience Platform troquem dados, com base em identificadores comuns, de maneira segura, controlada e compatível com a privacidade. A correspondência de segmentos usa padrões de privacidade da Experience Platform e identificadores pessoais, como emails com hash, números de telefone com hash e identificadores de dispositivos, como IDFAs e GAIDs. Para obter mais informações, consulte a [Visão geral da Correspondência de Segmentos](../../segmentation/ui/segment-match/overview.md). |

Para obter mais informações sobre o [!DNL Segmentation Service], consulte a [Visão geral de segmentação](../../segmentation/home.md).

## Origens {#sources}

O Adobe Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, estruturar, rotular e aprimorar esses dados usando os serviços da Experience Platform. É possível assimilar dados de várias origens, como aplicativos da Adobe, do armazenamento na nuvem, um software de terceiros e do seu sistema de CRM.

A Experience Platform fornece uma API RESTful e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar a sistemas de armazenamento externos e serviços de CRM, definir períodos para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

| Recurso | Descrição |
| --- | --- |
| Origens do Beta migrando para o GA | As seguintes fontes foram promovidas de beta para GA: <ul><li>[[!DNL Snowflake]](../../sources/connectors/databases/snowflake.md)</li><li>[[!DNL Veeva CRM]](../../sources/connectors/crm/veeva.md)</li></ul> |
| [!DNL Event Hubs] aprimoramentos na origem | A origem [!DNL Event Hubs] agora dá suporte ao tipo de autenticação de chave SAS não raiz para conectar e criar conexão de origem. Para obter mais informações, consulte a [[!DNL Event Hubs] visão geral](../../sources/connectors/cloud-storage/eventhub.md). |
| [!DNL SFTP] aprimoramentos na origem | A origem [!DNL SFTP] agora permite estabelecer um número definido de um máximo de conexões simultâneas que um fluxo de dados pode usar para se conectar ao servidor SFTP. Para obter mais informações, consulte a [[!DNL SFTP] visão geral](../../sources/connectors/cloud-storage/sftp.md). |
