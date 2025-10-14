---
title: Notas de versão de abril de 2024 da Adobe Experience Platform
description: As notas de versão de abril de 2024 da Adobe Experience Platform.
exl-id: 86d72fd8-a464-4715-abc9-4177236e423c
source-git-commit: 7f3459f678c74ead1d733304702309522dd0018b
workflow-type: tm+mt
source-wordcount: '1896'
ht-degree: 21%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: quarta-feira, 30 de abril de 2024**

>[!TIP]
>
>Use o [glossário do Adobe Experience Platform](/help/landing/glossary.md) para se familiarizar com a terminologia usada no Real-Time Customer Data Platform e no Adobe Experience Platform. Se você não conseguir encontrar um termo específico que esteja procurando, use as opções de feedback na página para solicitar que novos termos sejam adicionados ao glossário.

Atualizações dos recursos existentes no Experience Platform:

- [Painéis](#dashboards)
- [Coleção de dados](#data-collection)
- [Destinos](#destinations)
- [Serviço de identidade](#identity-service)
- [Monitoramento](#monitoring)
- [Query Service](#query-service)
- [Sandboxes](#sandboxes)
- [Serviço de segmentação](#segmentation)
- [Origens](#sources)

## Painéis {#dashboards}

A Adobe Experience Platform fornece vários painéis para você visualizar insights importantes sobre os dados de sua organização, que são capturados por instantâneos diários.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Insights B2B do Real-Time Customer Data Platform | Explore insights de dados B2B pré-configurados do [Real-Time CDP sobre contas e oportunidades](../../dashboards/insights/account-profiles.md) para ajudá-lo a entender seus dados e informar suas decisões comerciais. Você também pode [criar seus próprios insights usando o Modelo de Dados B2B do Real-Time CDP](../../dashboards/data-models/cdp-insights-data-model-b2c.md) para visualizar e explorar seus dados e salvar suas visualizações personalizadas em seu painel. |

{style="table-layout:auto"}

Para obter mais informações sobre painéis, incluindo como conceder permissões de acesso e criar widgets personalizados, comece lendo a [visão geral dos painéis](../../dashboards/home.md).

## Coleção de dados {#data-collection}

O Adobe Experience Platform fornece um conjunto de tecnologias que permitem coletar dados de experiência do cliente do lado do cliente e enviá-los para o Experience Platform Edge Network, onde podem ser enriquecidos, transformados e distribuídos para destinos da Adobe ou que não sejam da Adobe.

**Recursos novos ou atualizados**

| Tipo | Recurso | Descrição |
| --- | --- | --- |
| Extensões | Extensão de [!DNL Acxiom Anonymous Visitor Insights] Tags | Descubra de onde vêm os visitantes do seu site com o [!DNL Acxiom's Visitor Insights]. Utilizando a tecnologia de pesquisa geográfica de IP, a Acxiom pode identificar a localização de navegadores anônimos. Uma vez identificada, uma pesquisa em seu banco de dados organizado produz insights adicionais que são enviados de volta para o navegador. Assim, os criadores de conteúdo podem adaptar seu conteúdo para corresponder a esses pontos de dados, fornecendo uma experiência mais personalizada e envolvente para os visitantes, mesmo que eles tenham começado como estranhos. |
| Sequência de dados | [Detecção de bot do Edge Network](../../datastreams/bot-detection.md) | O tráfego proveniente de entidades não humanas, como programas automatizados, web scrapers, spiders e scanners com script, pode dificultar a identificação de eventos que ocorrem de visitantes humanos. Esse tipo de tráfego pode afetar negativamente métricas comerciais importantes, resultando em relatórios de tráfego incorretos. A <br>Detecção de bot permite identificar eventos gerados pelo [Web SDK](../../web-sdk/home.md), [SDK Móvel](https://developer.adobe.com/client-sdks/home/) e [[!DNL Edge Network API]](https://developer.adobe.com/data-collection-apis/docs/getting-started/) como sendo gerados por spiders e bots conhecidos. Ao configurar a detecção de bot para seus fluxos de dados, você pode identificar endereços IP, intervalos de IP e cabeçalhos de solicitação específicos que gostaria de classificar como eventos de bot. <br> A identificação do tráfego de bot pode fornecer uma medida mais precisa da atividade do usuário no seu site ou aplicativo móvel. |
| SDK móvel | Versão principal | Novas versões principais do Mobile SDK foram lançadas para as seguintes plataformas: iOS Mobile Core 5.x e extensões compatíveis do iOS, Android Mobile Core 3.x e extensões compatíveis do Android, React Native Core 6.x e extensões compatíveis do React Native, Flutter Core 4.x e extensões compatíveis do Flutter. Essa versão oferece vários novos recursos e aprimoramentos, incluindo suporte no Android SDK para Jetpack Compose, suporte para experiências baseadas em código do Adobe Journey Optimizer e disponibilidade geral da extensão de Mensagens do Adobe Journey Optimizer para Flutter. Para obter notas de versão mais detalhadas, consulte as [Notas de versão do Mobile SDK](https://developer.adobe.com/client-sdks/home/release-notes/). |
| SDK móvel | Privacidade | Devido à atualização da política do Apple, a partir de 1 de maio de 2024, os desenvolvedores deverão implementar novos recursos de privacidade para enviar para o App Store. Todos os clientes do Adobe que usam o Mobile SDK precisarão atualizar para a versão 5.x do SDK se quiserem receber a aprovação do App Store após 1º de maio. |
| Roku SDK | Roku SDK | A primeira versão principal do Roku SDK foi lançada com suporte para mídia de transmissão para o Experience Platform Edge Network. |
| Tags e encaminhamento de eventos | Orientação no produto | As [Marcas](../../tags/home.md) e o [Encaminhamento de Eventos](../../tags/ui/event-forwarding/overview.md) da Experience Platform oferecem um novo intervalo de experiências que pode ajudá-lo a começar rapidamente e obter um tempo de retorno rápido. Essas experiências incluem novas telas de integração, tutoriais no produto e dicas de ferramentas. <br>![Encaminhamento de eventos com a orientação no produto destacada.](../2024/assets/april/event-forwarding.png "O Editor de esquemas com os campos de tipo de valor Tipo e Mapa realçados."){width="100" zoomable="yes"}<br> |
| Web SDK | Adoção simplificada do Web SDK para clientes do Audience Manager | Agora, várias atualizações do Web SDK simplificam a adoção do Web SDK sem usar o Experience Data Model (XDM) para soluções da Experience Cloud, como o Audience Manager, o Analytics e o Target. Saiba mais sobre a adoção do Audience Manager Web SDK nos seguintes guias: <ul><li><a href="https://experienceleague.adobe.com/pt-br/docs/audience-manager/user-guide/migrate-to-web-sdk/dil-extension-to-web-sdk">Atualize a biblioteca de coleção de dados para o Audience Manager a partir da extensão de marca Audience Manager para a extensão de marca Web SDK</li><li><a href="https://experienceleague.adobe.com/pt-br/docs/audience-manager/user-guide/migrate-to-web-sdk/appmeasurement-to-web-sdk">Atualize a biblioteca de coleção de dados do Audience Manager da biblioteca JavaScript do AppMeasurement para a biblioteca JavaScript do Web SDK</li></ul> |

{style="table-layout:auto"}

<!--| Web SDK | [Streaming Media Collection support in Web SDK](../../web-sdk/commands/configure/streamingmedia.md) | You can now use Experience Platform Web SDK to collect data related to media sessions on your website. The collected data can include information about media playbacks, pauses, completions, and other related events. Once collected, you can send this data to Adobe Experience Platform and/or Adobe Analytics, to generate reports. This feature provides a comprehensive solution for tracking and understanding media consumption behavior on your website. <br>See the [Web SDK](../../web-sdk/commands/configure/streamingmedia.md) documentation to learn how to configure the `streamingMedia` component. <br>See the guide on [migrating your Analytics for Streaming Media implementation from Media JS to Web SDK](https://experienceleague.adobe.com/pt-br/docs/media-analytics/using/implementation/edge-recommended/media-edge-sdk/edge-web-sdk) for more details.|-->

Para saber mais sobre coleções de dados, leia a [visão geral da coleção de dados](../../collection/home.md).

## Destinos {#destinations}

[!DNL Destinations] são integrações pré-construídas com plataformas de destino que permitem a ativação perfeita de dados da Adobe Experience Platform. É possível usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas de email, publicidade direcionada e muitos outros casos de uso.

**Funcionalidade nova ou atualizada** {#destinations-new-updated-functionality}

| Funcionalidade | Descrição |
| ----------- | ----------- |
| Parâmetro `isRequired` agora disponível para campos de dados aninhados do cliente no Destination SDK | Ao configurar um destino no Destination SDK, agora você pode [definir campos de dados aninhados do cliente conforme necessário](/help/destinations/destination-sdk/functionality/destination-configuration/customer-data-fields.md#nested-fields). Dessa forma, os usuários que configuram seu destino não podem continuar com o fluxo de ativação até que selecionem um valor para esse campo. |
| A segmentação do Edge não é mais um requisito obrigatório ao configurar um destino do Adobe Target com o Web SDK | Anteriormente, ao configurar um [destino do Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) com o Web SDK, a sequência de dados tinha que ser habilitada para personalização e segmentação de borda. O requisito de que a sequência de dados seja habilitada para a segmentação de borda [&#x200B; agora foi removido](/help/destinations/ui/activate-edge-personalization-destinations.md#configure-datastream). Observe que esse padrão de integração permite que você se beneficie de um subconjunto de casos de uso de personalização ao usar o Adobe Target com o Real-Time CDP. Leia mais sobre os [casos de uso habilitados pelo tipo de integração](/help/destinations/catalog/personalization/adobe-target-connection.md#supported-use-cases). |
| [!BADGE Beta]{type=Informative} Remova vários públicos-alvo e conjuntos de dados dos fluxos de ativação | Agora é possível selecionar e remover vários públicos-alvo e conjuntos de dados dos fluxos de ativação de destino. Consulte a documentação dos [detalhes do destino](../../destinations/ui/destination-details-page.md#bulk-remove) e da [exportação de conjunto de dados](../../destinations/ui/export-datasets.md) para obter mais detalhes. |

{style="table-layout:auto"}

Para obter informações mais gerais sobre destinos, consulte a [visão geral de destinos](../../destinations/home.md).

## Serviço de identidade {#identity-service}

Use o Serviço de identidade da Adobe Experience Platform para criar uma visão abrangente dos clientes e seus comportamentos pela união de identidades entre dispositivos e sistemas, permitindo fornecer experiências digitais pessoais e impactantes em tempo real.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Substituição dos pontos de extremidade `/orgs/{ORG}/` na API | Os seguintes pontos de extremidade na [[!DNL Identity Service] API](https://developer.adobe.com/experience-platform-apis/references/identity-service/) foram descontinuados:<ul><li>`https://platform.adobe.io/data/core/idnamespace/orgs/{ORG}/identities`</li><li>`https://platform.adobe.io/data/core/idnamespace/orgs/{ORG}/identities/{ID}`</li></ul> Você pode usar os pontos de extremidade `/idnamespace/identities` e `/idnamespace/identities/{ID}` para realizar as mesmas tarefas e recuperar todos os namespaces em uma organização ou um namespace específico em uma organização. |

{style="table-layout:auto"}

Para obter mais informações sobre o Serviço de identidade, leia a [Visão geral do serviço de identidade](../../identity-service/home.md).

## Monitoramento {#monitoring}

Use o painel de monitoramento na interface do usuário do Experience Platform para monitorar a jornada de dados de Fontes, Serviço de identidade, Perfil do cliente em tempo real, Públicos-alvo e Destinos.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Monitorar expansão do painel | Agora você pode usar o painel de monitoramento para diferentes tipos de dados com base no caso de uso de negócios. Use o painel de monitoramento para monitorar atividades de tipos de dados de pessoas, contas e clientes potenciais em fontes, públicos e destinos. |

{style="table-layout:auto"}

Para obter mais informações, leia o guia em [usando o painel de monitoramento](../../dataflows/ui/monitor.md).

## Query Service {#query-service}

O Query Service permite usar SQL padrão para consultar dados no [!DNL Data Lake] da Adobe Experience Platform. Você pode ingressar em qualquer conjunto de dados do [!DNL Data Lake] e capturar os resultados da consulta como um novo conjunto de dados para usar em relatórios, no Data Science Workspace ou para assimilação no Perfil do cliente em tempo real.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Quarentena de consultas | Isole automaticamente as execuções de consulta com falha para evitar interrupções e manter o desempenho consistente. Consulte a documentação da [quarentena de consulta](../../query-service/ui/query-schedules.md#quarantine) para obter mais informações. |
| Cancelar consulta | Assuma o controle da execução da consulta e melhore sua produtividade cancelando consultas de longa execução.Consulte a documentação de [cancelar consulta](../../query-service/ui/user-guide.md#cancel-query) para obter mais informações. |
| Alertas de consulta agendada | Mantenha-se informado com notificações proativas enquanto agenda consultas, garantindo um gerenciamento de tarefas eficiente e oportuno. Você pode [assinar alertas ao criar uma consulta](../../query-service/ui/query-schedules.md#alerts-for-query-status) ou usar as ações embutidas para consultas agendadas existentes. Consulte a documentação [assinar alertas com ações embutidas](../../query-service/ui/monitor-queries.md#alert-subscription) para obter mais informações. |
| Navegação de consulta programada aprimorada | Navegue facilmente entre modelos de consulta e execuções programadas para aumentar a produtividade. Consulte a documentação em [exibindo execuções de consulta agendadas](../../query-service/ui/query-schedules.md#scheduled-query-runs) para obter mais informações. |
| Saída de consulta estendida | Acesse até 500 linhas de resultados de consulta no console para uma análise mais profunda de seus dados. Consulte a documentação de [contagem de resultados](../../query-service/ui/user-guide.md#result-count) para obter mais informações. |
| Encerramento do Editor de Consulta Herdada | A partir de 30 de abril de 2024, o Editor de consultas aprimorado se tornou o editor padrão para todos os usuários. O editor herdado será descontinuado em 24 de maio de 2024 e não estará mais disponível para uso. Consulte o [Guia do usuário do Editor de Consulta](../../query-service/ui/user-guide.md) para obter mais informações. |

{style="table-layout:auto"}

Para obter mais informações sobre o Query Service, acesse a [Visão geral do Query Service](../../query-service/home.md).

## Sandboxes {#sandboxes}

O Adobe Experience Platform foi criado para enriquecer aplicativos de experiência digital em escala global. As empresas geralmente executam vários aplicativos de experiência digital em paralelo e precisam atender ao desenvolvimento, ao teste e à implantação desses aplicativos enquanto garantem a conformidade operacional. Para atender a essa necessidade, a Experience Platform fornece sandboxes que particionam uma única instância do Experience Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| [Ferramentas de sandbox](../../sandboxes/ui/sandbox-tooling.md) | Use a ferramenta de sandbox para [exportar](../../sandboxes/ui/sandbox-tooling.md#export-entire-sandbox) todos os tipos de objetos com suporte para um pacote de sandbox completo e [importar](../../sandboxes/ui/sandbox-tooling.md#import-entire-sandbox) o pacote em várias sandboxes para replicar configurações de objeto. |

{style="table-layout:auto"}

Para obter mais informações sobre sandboxes, leia a [visão geral das sandboxes](../../sandboxes/home.md).

## Serviço de segmentação {#segmentation}

O [!DNL Segmentation Service] permite segmentar dados relacionados a indivíduos (como clientes, prospectos, usuários ou organizações) que estão armazenados na [!DNL Experience Platform] em públicos-alvo. Você pode criar públicos-alvo por meio de definições de segmento ou outras fontes a partir dos dados do [!DNL Real-Time Customer Profile]. Esses públicos-alvo são configurados e mantidos de forma centralizada na [!DNL Experience Platform] e podem ser acessados a qualquer momento usando as soluções da Adobe.

**Recurso atualizado**

| Recurso | Descrição |
| ------- | ----------- |
| Estados do ciclo de vida do público | Os estados do ciclo de vida do público-alvo foram simplificados para simplificar o gerenciamento do ciclo de vida. Para saber mais sobre esses estados de ciclo de vida, leia as [Perguntas frequentes sobre o Serviço de Segmentação](../../segmentation/faq.md#lifecycle-states). |

{style="table-layout:auto"}

Para obter mais informações sobre o [!DNL Segmentation Service], consulte a [Visão geral de segmentação](../../segmentation/home.md).

## Origens {#sources}

A Experience Platform fornece uma API RESTful e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar a sistemas de armazenamento externos e serviços de CRM, definir períodos para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

Use fontes na Experience Platform para assimilar dados de um aplicativo da Adobe ou de uma fonte de dados de terceiros.

**Novas fontes**

| Novas fontes | Descrição |
| --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL PathFactory] | Use a [[!DNL PathFactory] origem](../../sources/tutorials/ui/create/marketing-automation/pathfactory.md) para integrar os dados de visitante, sessão e exibição de página de [!DNL PathFactory] à Experience Platform. Leia a [[!DNL PathFactory] visão geral](../../sources/connectors/marketing-automation/pathfactory.md) para obter informações sobre como começar. |
| [!DNL Teradata Vantage] | Use a [[!DNL Teradata Vantage] origem](../../sources/tutorials/ui/create/databases/teradata-vantage.md) para assimilar dados de ambientes híbridos de várias nuvens para a Experience Platform. Leia a [[!DNL Teradata Vantage] visão geral](../../sources/connectors/databases/teradata-vantage.md) para obter informações sobre como começar. |

{style="table-layout:auto"}

**Recursos novos e atualizados**

| Recurso | Descrição |
| --- | --- |
| Atualizações em endereços IP para lista de permissões no VA7 | Os seguintes endereços IP foram adicionados à lista de endereços IP para adicionar à sua lista de permissões para VA7 (América do Norte): <ul><li>`20.98.198.224/29`</li><li>`20.119.28.57/32`</li><li>`20.232.89.104/29`</li><li>`20.98.195.172/32`</li><li>`172.210.218.144/28`</li></ul> Para obter uma lista abrangente dos endereços IP a serem adicionados à sua lista de permissões, leia o [documento de lista de permissões de Endereço IP](../../sources/ip-address-allow-list.md). |
| Suporte para novos tipos de autenticação com a origem [!DNL Azure Event Hubs] | Agora você pode conectar sua origem [!DNL Event Hubs] ao Experience Platform usando [!DNL Azure Active Directory Authentication] ou [!DNL Scoped Azure Active Directory Authentication]. Leia o manual sobre [conexão [!DNL Event Hubs] ao Experience Platform](../../sources/tutorials/ui/create/cloud-storage/eventhub.md) para obter mais informações. |
| Atualizações para recuperação de credencial [!DNL Data Landing Zone] | Agora você pode usar o painel direito no espaço de trabalho de origens para recuperar suas credenciais do [!DNL Data Landing Zone]. Agora você também pode usar o painel direito para atualizar suas credenciais. Leia o [[!DNL Data Landing Zone] guia da interface](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md) para obter mais informações. |

{style="table-layout:auto"}

<!--| Enhanced filtering and navigation in the sources UI workspace | Use the enhanced filtering, search, and inline action tools in the sources UI workspace to streamline your workflow. <ul><li>Use filtering and search capabilities to navigate your way through sources accounts and dataflows in your organization.</li><li>Use inline actions to modify configuration settings applied to your dataflows and improve organizational workflows. You can use inline actions to apply tags, set up alerts, or create ingestion jobs on demand.</li></ul> For more information, read the guide on [filtering sources objects in the UI](../../sources/tutorials/ui/filter.md).|-->

Para obter mais informações sobre fontes, leia a [visão geral das fontes](../../sources/home.md).
