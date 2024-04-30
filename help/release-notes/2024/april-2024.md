---
title: Notas de versão de abril de 2024 da Adobe Experience Platform
description: As notas de versão de abril de 2024 da Adobe Experience Platform.
source-git-commit: 6ad7d55ca0a544879db9738c0a4ab914fdc363bd
workflow-type: tm+mt
source-wordcount: '1728'
ht-degree: 18%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: quarta-feira, 30 de abril de 2024**

>[!TIP]
>
>Use o [Glossário do Adobe Experience Platform](/help/landing/glossary.md) para conhecer a terminologia usada no Real-time Customer Data Platform e no Adobe Experience Platform. Se você não conseguir encontrar um termo específico que esteja procurando, use as opções de feedback na página para solicitar que novos termos sejam adicionados ao glossário.

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

O Adobe Experience Platform fornece vários painéis por meio dos quais você pode visualizar insights importantes sobre os dados de sua organização, conforme capturados durante instantâneos diários.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Insights B2B do Real-time Customer Data Platform | Explore insights de dados B2B pré-configurados do Real-Time CDP sobre contas e oportunidades para ajudá-lo a entender seus dados e informar suas decisões de negócios. Você também pode criar seus próprios insights usando o Modelo de dados B2B do Real-Time CDP para visualizar e explorar seus dados e salvar suas visualizações personalizadas no painel. |

{style=“table-layout:auto”}

Para obter mais informações sobre painéis, incluindo como conceder permissões de acesso e criar widgets personalizados, comece lendo a [visão geral dos painéis](../../dashboards/home.md).

## Coleção de dados {#data-collection}

A Adobe Experience Platform fornece um conjunto de tecnologias que permitem coletar dados de experiência do cliente do lado do cliente e enviá-los para o Edge Network de Experience Platform, onde podem ser enriquecidos, transformados e distribuídos para destinos Adobe ou não Adobe.

**Recursos novos ou atualizados**

| Tipo | Recurso | Descrição |
| --- | --- | --- |
| Insights | [!DNL Acxiom] Insights de visitante anônimo | Descubra de onde os visitantes do seu site vêm com a [!DNL Acxiom's] Insights do visitante. Ao utilizar a tecnologia de pesquisa geográfica de IP, identificamos a localização de navegadores anônimos. Uma vez identificada, uma pesquisa rápida em nosso banco de dados organizado produz insights adicionais que são enviados de volta ao navegador. Para criadores de conteúdo, isso significa uma oportunidade de ouro para adaptar seu conteúdo para corresponder a esses pontos de dados, fornecendo uma experiência mais personalizada e envolvente para os visitantes, mesmo que eles tenham começado como estranhos. |
| Sequências de dados | [Detecção de bot Edge Network](../../datastreams/bot-detection.md) | O tráfego proveniente de entidades não humanas, como programas automatizados, web scrapers, spiders e scanners com script, pode dificultar a identificação de eventos que ocorrem de visitantes humanos. Esse tipo de tráfego pode afetar negativamente métricas comerciais importantes, resultando em relatórios de tráfego incorretos. <br>A detecção de bot permite identificar eventos gerados pelo [SDK da Web](../../web-sdk/home.md), [SDK móvel](https://developer.adobe.com/client-sdks/home/) e [[!DNL Server API]](../../server-api/overview.md) como sendo gerado por aranhas e bots conhecidos. Ao configurar a detecção de bot para seus fluxos de dados, você pode identificar endereços IP, intervalos de IP e cabeçalhos de solicitação específicos que gostaria de classificar como eventos de bot. <br> A identificação do tráfego de bot pode fornecer uma medida mais precisa da atividade do usuário no seu site ou aplicativo móvel. |
| SDK móvel | Versão principal | Novas versões principais do SDK móvel foram lançadas para as seguintes plataformas: iOS Mobile Core 5.x e extensões compatíveis do iOS, Android Mobile Core 3.x e extensões compatíveis do Android, React Native Core 6.x e extensões compatíveis do React Native, Flutter Core 4.x e extensões compatíveis do Flutter. Essas versões fornecem vários novos recursos e melhorias, incluindo suporte no Android SDK para Jetpack Compose, suporte para experiências baseadas em código Adobe Journey Optimizer e disponibilidade geral da extensão do Adobe Journey Optimizer Messaging para Flutter. Para obter notas de versão mais detalhadas, consulte [Notas de versão do SDK móvel](https://developer.adobe.com/client-sdks/home/release-notes/). |
| SDK móvel | Privacidade | Devido à atualização da política do Apple, a partir de 1 de maio de 2024, os desenvolvedores deverão implementar novos recursos de privacidade para enviar para o App Store. Todos os clientes do Adobe que usam o SDK móvel precisarão atualizar para a versão 5.x do SDK se quiserem receber a aprovação da App Store após 1º de maio. |
| SDK do Roku | SDK do Roku | A primeira versão principal do SDK do Roku foi lançada com suporte para mídia de transmissão para o Edge Network da plataforma. |
| Tags e encaminhamento de eventos | Orientação no produto | Experience Platform [Tags](../../tags/home.md) e [Encaminhamento de evento](../../tags/ui/event-forwarding/overview.md) ofereça uma nova variedade de experiências que podem ajudá-lo a começar rapidamente e a obter um tempo de retorno rápido. Essas experiências incluem novas telas de integração, tutoriais no produto e dicas de ferramentas. <br>![O encaminhamento de eventos com a orientação no produto está destacado.](../2024/assets/april/event-forwarding.png "O Editor de esquemas com os campos Type e Map value type realçados."){width="100" zoomable="yes"}<br> |
| Web SDK | Adoção simplificada do SDK da Web para clientes do Audience Manager | Agora, várias atualizações de SDK da Web simplificam a adoção do SDK da Web sem usar o Experience Data Model (XDM) para soluções de Experience Cloud, como o Audience Manager, o Analytics e o Target. Saiba mais sobre a adoção do SDK da Web do Audience Manager nos seguintes guias: <ul><li><a href="https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/migrate-to-web-sdk/dil-extension-to-web-sdk">Atualize sua biblioteca de coleção de dados para o Audience Manager da extensão de tag Audience Manager para a extensão de tag do SDK da Web</li><li><a href="https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/migrate-to-web-sdk/appmeasurement-to-web-sdk">Atualize sua biblioteca de coleção de dados para o Audience Manager da biblioteca JavaScript do AppMeasurement para a biblioteca JavaScript do SDK da Web</li></ul> |

{style="table-layout:auto"}

<!--| Web SDK | [Streaming Media Collection support in Web SDK](../../web-sdk/commands/configure/streamingmedia.md) | You can now use Experience Platform Web SDK to collect data related to media sessions on your website. The collected data can include information about media playbacks, pauses, completions, and other related events. Once collected, you can send this data to Adobe Experience Platform and/or Adobe Analytics, to generate reports. This feature provides a comprehensive solution for tracking and understanding media consumption behavior on your website. <br>See the [Web SDK](../../web-sdk/commands/configure/streamingmedia.md) documentation to learn how to configure the `streamingMedia` component. <br>See the guide on [migrating your Analytics for Streaming Media implementation from Media JS to Web SDK](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/edge-recommended/media-edge-sdk/edge-web-sdk) for more details.|-->

Para saber mais sobre coleções de dados, leia o [visão geral da coleção de dados](../../collection/home.md).

## Destinos {#destinations}

[!DNL Destinations] são integrações pré-construídas com plataformas de destino que permitem a ativação perfeita de dados da Adobe Experience Platform. É possível usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas de email, publicidade direcionada e muitos outros casos de uso.

**Funcionalidades novas ou atualizadas** {#destinations-new-updated-functionality}

| Funcionalidade | Descrição |
| ----------- | ----------- |
| `isRequired` parâmetro agora disponível para campos de dados aninhados do cliente no Destination SDK | Ao configurar um destino no Destination SDK, agora é possível [defina campos de dados aninhados do cliente conforme necessário](/help/destinations/destination-sdk/functionality/destination-configuration/customer-data-fields.md#nested-fields). Dessa forma, os usuários que configuram seu destino não podem continuar com o fluxo de ativação até que selecionem um valor para esse campo. |

{style="table-layout:auto"}

Para obter informações mais gerais sobre destinos, consulte a [visão geral de destinos](../../destinations/home.md).

<!--| [!BADGE Beta]{type=Informative} Remove multiple audiences and datasets from activation flows | You can now select and remove multiple audiences and datasets from destination activation flows. See the [destination details](../../destinations/ui/destination-details-page.md#bulk-remove) and [dataset export](../../destinations/ui/export-datasets.md) documentation for more details. |-->

## Serviço de identidade {#identity-service}

Use o Serviço de identidade da Adobe Experience Platform para criar uma visualização abrangente dos clientes e seus comportamentos, unindo identidades em dispositivos e sistemas, permitindo que você forneça experiências digitais pessoais e de impacto em tempo real.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Substituição do `/orgs/{ORG}/` endpoints na API | Os seguintes endpoints no [[!DNL Identity Service] API](https://developer.adobe.com/experience-platform-apis/references/identity-service/) foram descontinuadas:<ul><li>`https://platform.adobe.io/data/core/idnamespace/orgs/{ORG}/identities`</li><li>`https://platform.adobe.io/data/core/idnamespace/orgs/{ORG}/identities/{ID}`</li></ul> Você pode usar o `/idnamespace/identities` e a variável `/idnamespace/identities/{ID}` pontos de acesso para realizar as mesmas tarefas e recuperar todos os namespaces em uma organização ou um namespace específico em uma organização. |

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

O Query Service permite usar SQL padrão para consultar dados no [!DNL Data Lake] da Adobe Experience Platform. Você pode associar qualquer conjunto de dados da [!DNL Data Lake] e capture os resultados da consulta como um novo conjunto de dados para usar em relatórios, no Data Science Workspace ou para assimilação no Perfil do cliente em tempo real.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Quarentena de consulta | Isole automaticamente as execuções de consulta com falha para evitar interrupções e manter o desempenho consistente. |
| Cancelar consulta | Assuma o controle da execução de consultas e melhore sua produtividade cancelando consultas de longa execução. |
| Alertas de consulta agendada | Mantenha-se informado com notificações proativas enquanto agenda consultas, garantindo um gerenciamento de tarefas eficiente e oportuno. Você pode assinar alertas ao criar uma consulta ou usar as ações em linha para consultas agendadas existentes. |
| Navegação de consulta programada aprimorada | Navegue facilmente entre modelos de consulta e execuções programadas para aumentar a produtividade. |
| Saída de consulta estendida | Acesse até 500 linhas de resultados de query no console para uma análise mais profunda dos dados. |
| Encerramento do Editor de Consulta Herdada | A partir de 30 de abril de 2024, o Editor de consultas aprimorado se tornou o editor padrão para todos os usuários. O editor herdado será descontinuado em 30 de maio de 2024 e não estará mais disponível para uso. |

{style=“table-layout:auto”}

Para obter mais informações sobre o Query Service, acesse a [Visão geral do Query Service](../../query-service/home.md).

## Sandboxes {#sandboxes}

O Adobe Experience Platform foi criado para enriquecer aplicativos de experiência digital em escala global. As empresas geralmente executam vários aplicativos de experiência digital em paralelo e precisam atender ao desenvolvimento, ao teste e à implantação desses aplicativos enquanto garantem a conformidade operacional. Para atender a essa necessidade, o Experience Platform fornece sandboxes que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| [Ferramentas de sandbox](../../sandboxes/ui/sandbox-tooling.md) | Use as ferramentas de sandbox para [exportar](../../sandboxes/ui/sandbox-tooling.md#export-entire-sandbox) todos os tipos de objetos compatíveis em um pacote de sandbox completo e, em seguida, [importar](../../sandboxes/ui/sandbox-tooling.md#import-entire-sandbox) o pacote em várias sandboxes para replicar configurações de objetos. |

{style="table-layout:auto"}

Para obter mais informações sobre sandboxes, leia a [visão geral das sandboxes](../../sandboxes/home.md).

## Serviço de segmentação {#segmentation}

O [!DNL Segmentation Service] permite segmentar dados relacionados a indivíduos (como clientes, prospectos, usuários ou organizações) que estão armazenados na [!DNL Experience Platform] em públicos-alvo. Você pode criar públicos-alvo por meio de definições de segmento ou outras fontes a partir dos dados do [!DNL Real-Time Customer Profile]. Esses públicos-alvo são configurados e mantidos de forma centralizada na [!DNL Platform] e podem ser acessados a qualquer momento usando as soluções da Adobe.

**Recurso atualizado**

| Recurso | Descrição |
| ------- | ----------- |
| Estados do ciclo de vida do público | Os estados do ciclo de vida do público-alvo foram simplificados para simplificar o gerenciamento do ciclo de vida. Para saber mais sobre esses estados do ciclo de vida, leia o [Perguntas frequentes sobre o serviço de segmentação](../../segmentation/faq.md#lifecycle-states). |

{style="table-layout:auto"}

Para obter mais informações sobre o [!DNL Segmentation Service], consulte a [Visão geral de segmentação](../../segmentation/home.md).

## Origens {#sources}

A Experience Platform fornece uma API RESTful e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar a sistemas de armazenamento externos e serviços de CRM, definir períodos para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

Use fontes no Experience Platform para assimilar dados de um aplicativo Adobe ou de uma fonte de dados de terceiros.

**Novas fontes**

| Novas fontes | Descrição |
| --- | --- |
| [!BADGE Beta]{type=Informativo} [!DNL PathFactory] | Use o [[!DNL PathFactory] origem](../../sources/tutorials/ui/create/marketing-automation/pathfactory.md) para integrar os dados de visitante, sessão e exibição de página do [!DNL PathFactory] para Experience Platform. Leia o [[!DNL PathFactory] visão geral](../../sources/connectors/marketing-automation/pathfactory.md) para obter informações sobre como começar. |
| [!DNL Teradata Vantage] | Use o [[!DNL Teradata Vantage] origem](../../sources/tutorials/ui/create/databases/teradata-vantage.md) para assimilar dados de ambientes híbridos de várias nuvens no Experience Platform. Leia o [[!DNL Teradata Vantage] visão geral](../../sources/connectors/databases/teradata-vantage.md) para obter informações sobre como começar. |

{style="table-layout:auto"}

**Recursos novos e atualizados**

| Recurso | Descrição |
| --- | --- |
| Atualizações em endereços IP para lista de permissões no VA7 | Os seguintes endereços IP foram adicionados à lista de endereços IP para adicionar à sua lista de permissões para VA7 (América do Norte): <ul><li>`20.98.198.224/29`</li><li>`20.119.28.57/32`</li><li>`20.232.89.104/29`</li><li>`20.98.195.172/32`</li><li>`172.210.218.144/28`</li></ul> Para obter uma lista abrangente de endereços IP para adicionar à lista de permissões, leia o [Documento de lista de permissões do endereço IP](../../sources/ip-address-allow-list.md). |
| Suporte para novos tipos de autenticação com o [!DNL Azure Event Hubs] origem | Agora você pode conectar seu [!DNL Event Hubs] origem para Experience Platform usando [!DNL Azure Active Directory Authentication] ou [!DNL Scoped Azure Active Directory Authentication]. Leia o guia em [conectando [!DNL Event Hubs] para Experience Platform](../../sources/tutorials/ui/create/cloud-storage/eventhub.md) para obter mais informações. |
| Atualizações para [!DNL Data Landing Zone] recuperação de credencial | Agora, você pode usar o painel direito no espaço de trabalho de origens para recuperar o [!DNL Data Landing Zone] credenciais. Agora você também pode usar o painel direito para atualizar suas credenciais. Leia o [[!DNL Data Landing Zone] Guia da interface do usuário](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md) para obter mais informações. |

{style="table-layout:auto"}

<!--| Enhanced filtering and navigation in the sources UI workspace | Use the enhanced filtering, search, and inline action tools in the sources UI workspace to streamline your workflow. <ul><li>Use filtering and search capabilities to navigate your way through sources accounts and dataflows in your organization.</li><li>Use inline actions to modify configuration settings applied to your dataflows and improve organizational workflows. You can use inline actions to apply tags, set up alerts, or create ingestion jobs on demand.</li></ul> For more information, read the guide on [filtering sources objects in the UI](../../sources/tutorials/ui/filter.md).|-->

Para obter mais informações sobre fontes, leia a [visão geral das origens](../../sources/home.md).
