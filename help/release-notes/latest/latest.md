---
title: Notas de versão da Adobe Experience Platform
description: As notas de versão mais recentes do Adobe Experience Platform.
source-git-commit: 021a0833941f250475786bb8629542c50229b238
workflow-type: tm+mt
source-wordcount: '921'
ht-degree: 7%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 26 de outubro de 2022**

Novos recursos no Adobe Experience Platform:

- [Chaves gerenciadas pelo cliente](#cmk)

Atualizações dos recursos existentes na Adobe Experience Platform:

- [Coleta de dados](#data-collection)
- [Destinos](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Serviço de query](#query-service)
- [Fontes](#sources)

## Chaves gerenciadas pelo cliente {#cmk}

Todos os dados armazenados no Adobe Experience Platform são criptografados em repouso usando chaves de nível de sistema. Se você estiver usando um aplicativo criado na plataforma, poderá optar por usar suas próprias chaves de criptografia, fornecendo maior controle sobre a segurança dos dados.

Consulte a visão geral em [chaves gerenciadas pelo cliente](../../landing/governance-privacy-security/customer-managed-keys.md) para obter detalhes sobre o recurso.

## Coleta de dados {#data-collection}

A Adobe Experience Platform fornece um conjunto de tecnologias que permitem coletar dados de experiência do cliente e enviá-los para a Adobe Experience Platform Edge Network, onde podem ser enriquecidos, transformados e distribuídos para destinos Adobe ou não-Adobe.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Tratamento de dados confidenciais para conjuntos de dados | Os datastreams agora usam várias tecnologias da plataforma para lidar adequadamente com dados confidenciais, conforme empregado por regulamentos, como o Health Insurance Portability and Accountability Act (HIPAA). Consulte a seção sobre [tratamento de dados confidenciais em fluxos de dados](../../edge/datastreams/overview.md#sensitive) para obter mais informações. |
| [!DNL Splunk] extensão para encaminhamento de eventos | Agora é possível enviar dados para o [!DNL Splunk] usando um [encaminhamento de eventos](../../tags/ui/event-forwarding/overview.md) extensão. Consulte a [[!DNL Splunk] visão geral da extensão](../../tags/extensions/web/splunk/overview.md) para obter mais informações. |
| [!DNL Zendesk] extensão para encaminhamento de eventos | Agora é possível enviar dados para o [!DNL Zendesk] usando um [encaminhamento de eventos](../../tags/ui/event-forwarding/overview.md) extensão. Consulte a [[!DNL Zendesk] visão geral da extensão](../../tags/extensions/web/zendesk/overview.md) para obter mais informações. |

{style=&quot;table-layout:auto&quot;}

## [!DNL Destinations] {#destinations}

[!DNL Destinations] são integrações pré-criadas com plataformas de destino que permitem a ativação contínua de dados do Adobe Experience Platform. Você pode usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas por email, anúncios direcionados e muitos outros casos de uso.

**Destinos novos ou atualizados**

| Destino | Descrição |
| ----------- | ----------- |
| [[!DNL Line]](../../destinations/catalog/mobile-engagement/line.md) | O Line é uma plataforma de comunicação popular que conecta pessoas, serviços e informações e cresceu de um aplicativo de chat em um hub para atividades de entretenimento, sociais e diárias. |
| [[!DNL Microsoft Dynamics 365]](../../destinations/catalog/crm/microsoft-dynamics-365.md) | O Microsoft Dynamics 365 é uma plataforma de aplicativos de negócios baseada em nuvem que combina o Enterprise Resource Planning (ERP) e o Customer Relationship Management (CRM), juntamente com aplicativos de produtividade e ferramentas de IA, para proporcionar operações completas e mais controladas, melhorar o potencial de crescimento e reduzir os custos. |

{style=&quot;table-layout:auto&quot;}

**Documentação nova ou atualizada**

| Documentação | Descrição |
| ----------- | ----------- |
| [Medidas de proteção de destinos](../../destinations/guardrails.md) | Esta página fornece limites de uso e taxa padrão em relação ao comportamento de ativação. |

Para obter informações mais gerais sobre destinos, consulte [visão geral dos destinos](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

O XDM é uma especificação de código aberto que fornece estruturas e definições comuns (esquemas) para dados trazidos para o Adobe Experience Platform. Ao seguir os padrões XDM, todos os dados de experiência do cliente podem ser incorporados em uma representação comum para fornecer insights de uma maneira mais rápida e integrada. Você pode obter informações valiosas das ações do cliente, definir públicos-alvo do cliente por meio de segmentos e usar atributos do cliente para fins de personalização.

**Componentes XDM atualizados**

| Tipo de componente | Nome | Descrição |
| --- | --- | --- |
| Tipo de dados | [[!UICONTROL Informações de detalhes da sessão]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | Atualização do `authorized` de um tipo booleano a uma string. `season` e `episode` foram alteradas de números inteiros para sequências. |
| Tipo de dados | [[!UICONTROL Informações de detalhes de publicidade]](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json) | `name` foi renomeado para `friendlyName`e `ID` foi renomeado para `name`. |
| Tipo de dados | [[!UICONTROL Informações de detalhes do erro]](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json) | A `ID` foi renomeada como `name`.  |

{style=&quot;table-layout:auto&quot;}

Para obter mais informações sobre o XDM na Platform, consulte o [Visão geral do sistema XDM](../../xdm/home.md).

## Serviço de query {#query-service}

O Serviço de Consulta permite que você use o SQL padrão para consultar dados no Adobe Experience Platform [!DNL Data Lake]. É possível unir qualquer conjunto de dados da [!DNL Data Lake] e capture os resultados do query como um novo conjunto de dados para usar nos relatórios, no Data Science Workspace ou para assimilação no Perfil do cliente em tempo real.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Modelo de dados de insights de relatórios acelerados de query | Como parte da SKU do Data Distiller, o armazenamento acelerado de query permite reduzir o tempo e o poder de processamento necessários para obter insights críticos de seus dados. Com a loja acelerada de query, você pode criar um modelo de dados personalizado e/ou estender em modelos de dados existentes do Adobe Real-time Customer Data Platform para melhorar seus insights de relatórios e suas visualizações. Consulte a [documento de insights de relatórios de armazenamento acelerado de query](https://experienceleague.adobe.com/docs/experience-platform/query/query-accelerated-store/reporting-insights-data-model.html) para saber mais sobre esse recurso. |

{style=&quot;table-layout:auto&quot;}

Para obter mais informações sobre Serviços de query, consulte [Visão geral do Serviço de query](../../query-service/home.md).
Novos recursos no Adobe Experience Platform:

## Fontes {#sources}

A Adobe Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, permitir estruturar, rotular e aprimorar esses dados usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

O Experience Platform fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e se conectar a sistemas de armazenamento externos e serviços CRM, definir horários para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- | 
| Disponibilidade beta da origem do Adobe Workfront | Use o [Origem do Adobe Workfront](../../sources/connectors/adobe-applications/workfront.md) para trazer seus dados do Workfront para o Experience Platform e executar casos de uso, como combinar seus registros de trabalho com dados de terceiros, aplicar análises históricas e de séries de tempo em registros de trabalho e consultar dados de trabalho usando o SQL padrão. Para obter mais informações, leia o guia sobre [criação de uma conexão de origem do Workfront na interface do usuário](../../sources/tutorials/ui/create/adobe-applications/workfront.md). |
| Disponibilidade beta da origem da nuvem do Oracle Service | Use a fonte da nuvem do Oracle Service para assimilar dados da sua conta da Oracle Service Cloud para o Experience Platform. Para obter mais informações, leia a documentação sobre o [Origem da nuvem do Oracle Service](../../sources/connectors/customer-success/oracle-service-cloud.md). |

Para saber mais sobre fontes, leia a [visão geral das fontes](../../sources/home.md).
