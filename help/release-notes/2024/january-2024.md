---
title: Notas da versão de janeiro de 2024 da Adobe Experience Platform
description: As notas da versão de janeiro de 2024 da Adobe Experience Platform.
exl-id: d4b3c5b2-3adb-41fd-91ad-f4c0f21d2325
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1662'
ht-degree: 34%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: quarta-feira, 30 de janeiro de 2024**

Novos recursos na Adobe Experience Platform:

- [Manuais de casos de uso &#x200B;](#use-case-playbooks)

Atualizações dos recursos existentes no Experience Platform:

- [Controle de acesso baseado em atributos](#abac)
- [Preparação de dados](#data-prep)
- [Painéis](#dashboards)
- [Destinos](#destinations)
- [Serviço de identidade](#identity-service)
- [Real-Time Customer Data Platform](#rtcdp)
- [Perfil do cliente em tempo real](#profile)
- [Serviço de segmentação](#segmentation)
- [Origens](#sources)

## Manuais de casos de uso  {#use-case-playbooks}

A funcionalidade [!UICONTROL Guias de reprodução de casos de uso] agora está disponível para todos os clientes do Real-Time CDP e do Adobe Journey Optimizer. Os [!UICONTROL manuais de casos de uso] foram projetados para ajudar os usuários a superar desafios ao começar com o Real-Time Customer Data Platform ou o Adobe Journey Optimizer. Quando não tiver certeza de onde começar ou como criar os ativos certos para os casos de uso desejados, os manuais de casos de uso fornecem inspiração e criam ativos diferentes para que você teste e importe para ambientes de produção quando estiver pronto.

Para começar a usar os [!UICONTROL manuais de casos de uso], leia as seguintes páginas de documentação:

- Leia a [página de visão geral](/help/use-case-playbooks/playbooks/overview.md) para entender a finalidade, as informações de disponibilidade e obter uma demonstração completa de como os manuais funcionam, da descoberta à criação de instâncias, à importação de ativos gerados em outros ambientes de sandbox.
- Obtenha uma lista de todos os [manuais disponíveis](/help/use-case-playbooks/playbooks/playbooks-list.md), agrupados por produto (Real-Time CDP ou Journey Optimizer)
- Obtenha informações sobre todas as [permissões necessárias](/help/use-case-playbooks/playbooks/get-started.md#grant-your-team-the-required-access-permissions) para usar os manuais e os ativos gerados pelos manuais.
- Entenda a [funcionalidade de reconhecimento de dados](/help/use-case-playbooks/playbooks/data-awareness.md) que permite copiar ativos gerados para outros ambientes de sandbox
- Obtenha [dicas de solução de problemas](/help/use-case-playbooks/playbooks/troubleshooting.md) se você encontrar erros ou dificuldades ao usar os manuais de casos de uso.

## Controle de acesso baseado em atributos {#abac}

O controle de acesso baseado em atributos é um recurso do Adobe Experience Platform que oferece às marcas preocupadas com a privacidade maior flexibilidade para gerenciar o acesso do usuário. É possível atribuir objetos individuais, como campos de esquema e segmentos, a funções de usuário. Esse recurso permite conceder ou revogar o acesso a objetos individuais para usuários específicos da Experience Platform em sua organização.

Por meio do controle de acesso baseado em atributos, os administradores da sua organização podem controlar o acesso dos usuários, dados pessoais confidenciais (SPD), informações de identificação pessoal (PII) e outros tipos personalizados de dados em todos os fluxos de trabalho e recursos da Experience Platform. Admins podem definir funções de usuário que tenham acesso somente a campos e dados específicos que correspondam a esses campos.

**Documentação nova ou atualizada**

| Atualização da documentação | Descrição |
| --- | --- |
| Novos endpoints de API documentados para controle de acesso baseado em atributos | A [documentação de referência da API de controle de acesso](https://developer.adobe.com/experience-platform-apis/references/access-control/) agora inclui funções de API de controle de acesso baseado em atributos, políticas e pontos de extremidade de produto. Esses endpoints podem ser usados para recuperar funções, políticas e produtos relevantes para um usuário em determinados recursos em uma sandbox especificada. |

{style="table-layout:auto"}

Para obter mais informações sobre o controle de acesso baseado em atributos, consulte a [visão geral do controle de acesso baseado em atributos](../../access-control/abac/overview.md). Para obter um guia abrangente sobre o fluxo de trabalho do controle de acesso baseado em atributos, leia o [guia completo do controle de acesso baseado em atributos](../../access-control/abac/end-to-end-guide.md).

## Preparação de dados {#data-prep}

A preparação de dados permite que os engenheiros de dados mapeiem, transformem e validem dados de e para o Experience Data Model (XDM).

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Novas funções do mapeador | <ul><li>`object_to_map`: Use a função `object_to_map` para criar tipos de dados de mapa. Esta função suporta várias sintaxes diferentes. Para obter mais informações, leia o manual sobre [funções para hierarquias - objetos](../../data-prep/functions.md#objects). </li><li>`to_map`: Use a função `to_map` para criar um mapa com determinado nome de campo e pares de valores usando objetos. Para obter mais informações, leia o guia em [funções para hierarquias - mapas](../../data-prep/functions.md#map). </li><li>`array_to_map`: Use a função `array_to_map` para criar um mapa com determinado nome de campo e pares de valores usando matrizes de objetos. Para obter mais informações, leia o guia em [funções para hierarquias - mapas](../../data-prep/functions.md#map). |

{style="table-layout:auto"}

Para obter mais informações sobre Preparo de Dados, leia a [Visão geral do Preparo de Dados](../../data-prep/home.md).

## Painéis {#dashboards}

A Adobe Experience Platform fornece vários painéis para você visualizar insights importantes sobre os dados de sua organização, que são capturados por instantâneos diários.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Exibir SQL | Agora você pode visualizar o SQL por trás de seus Perfis, Públicos, Destinos e insights personalizados com a opção Exibir SQL e, em seguida, executar a consulta sob demanda por meio do Editor de consultas. Acessar o SQL que capacita seus insights da Real-time Customer Data Platform ajuda a entender a lógica por trás da análise de seu modelo de dados. Essa transparência torna os dados da CDP em tempo real da Adobe mais acessíveis, compreensíveis e impactantes para a tomada de decisões.<br>Inspire-se no SQL de mais de 40 insights existentes para criar novas consultas que obtenham insights exclusivos de dados do Experience Platform com base nas necessidades da empresa. O SQL também está disponível para seus [Perfis](../../dashboards/insights/profiles.md), [Públicos-alvo](../../dashboards/insights/audiences.md) e [Destinos](../../dashboards/insights/destinations.md) insights na documentação do Experience League. Esses documentos destacam os casos de uso de negócios que podem ser respondidos com os insights padrão. Para obter mais informações, leia o guia em [exibindo insight SQL](../../dashboards/view-sql.md). |

{style="table-layout:auto"}

Para obter mais informações sobre painéis, incluindo como conceder permissões de acesso e criar widgets personalizados, comece lendo a [visão geral dos painéis](../../dashboards/home.md).

## Destinos {#destinations}

[!DNL Destinations] são integrações pré-construídas com plataformas de destino que permitem a ativação perfeita de dados da Adobe Experience Platform. É possível usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas de email, publicidade direcionada e muitos outros casos de uso.

**Novos destinos** {#new-destinations}

| Destino | Descrição |
| ----------- | ----------- |
| [Conexão pública](../../destinations/catalog/advertising/pubmatic.md) | Use este destino para enviar dados de público à plataforma [!DNL PubMatic Connect]. |

{style="table-layout:auto"}

**Funcionalidades novas ou atualizadas** {#destinations-new-updated-functionality}

| Funcionalidade | Descrição |
| ----------- | ----------- |
| Novo tipo de autenticação de **função presumida** para destinos do Amazon S3 | Use o novo tipo de autenticação de função assumida ao conectar o Experience Platform aos buckets do Amazon S3 se não quiser compartilhar chaves de conta e chaves secretas com o Experience Platform. Leia mais sobre o novo método de autenticação na [seção de autenticação](/help/destinations/catalog/cloud-storage/amazon-s3.md#assumed-role-authentication) da documentação do Amazon S3. |

{style="table-layout:auto"}

Para obter informações mais gerais sobre destinos, consulte a [visão geral de destinos](../../destinations/home.md).

## Serviço de identidade {#identity-service}

O Serviço de identidade da Adobe Experience Platform fornece uma visão abrangente dos clientes e seu comportamento ao unir identidades entre dispositivos e sistemas, permitindo fornecer experiências digitais pessoais de impacto em tempo real.

**Documentação nova ou atualizada**

| Atualização da documentação | Descrição |
| --- | --- |
| Reestruturação da documentação | A documentação do Serviço de identidade foi reestruturada para melhorar a apresentação e a clareza dos conceitos no Serviço de identidade:<ul><li>Visite a [página de visão geral do Serviço de identidade](../../identity-service/home.md) para obter um guia de terminologia expandido, um exemplo de caso de uso detalhando uma jornada típica de cliente, um detalhamento de como o Serviço de identidade vincula as identidades e um resumo da função que o Serviço de identidade desempenha no ecossistema da Experience Platform.</li><li>Leia o guia em [noções básicas sobre a relação entre o Serviço de Identidade e o Perfil de Cliente em Tempo Real](../../identity-service/identity-and-profile.md) para obter um resumo detalhado de como os dois serviços funcionam juntos e as diferenças entre suas finalidades, processos, entradas e saídas.</li><li>Consulte o [Guia de lógica de vinculação do Identity Service](../../identity-service/features/identity-linking-logic.md) para obter explicações e visualizações sobre como o gráfico de identidade se comporta em determinados cenários e carimbos de data e hora.</li></ul> |

{style="table-layout:auto"}

Para saber mais sobre o Serviço de identidade, leia a [visão geral do Serviço de identidade](../../identity-service/home.md).

## Real-Time Customer Data Platform {#rtcdp}

Integrado à Experience Platform, a Real-time Customer Data Platform ([!DNL Real-Time CDP]) ajuda as empresas a unirem dados conhecidos e desconhecidos para ativar perfis de clientes com decisões inteligentes em toda a jornada do cliente. A [!DNL Real-Time CDP] combina várias fontes de dados corporativos para criar perfis de clientes em tempo real. Os segmentos criados a partir desses perfis podem ser enviados para destinos downstream com o fim de oferecer experiências de cliente personalizadas em todos os canais e dispositivos.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Atualizações para a [página inicial do Real-Time CDP](https://experience.adobe.com) | <ul><li>**Widget de Perfis**: agora você pode usar o widget de Perfis para navegar até a página de visão geral de Perfis e exibir as métricas de Perfil da sua organização.</li><li>**Cartão de métricas de perfil**: o cartão Métricas de perfil no painel da home page agora exibe a contagem total de perfis em sua organização, dependendo da respectiva política de mesclagem.</li><li>**Widget de esquemas**: agora você pode usar o widget de esquemas para navegar até o fluxo de trabalho de criação de esquemas na interface do usuário.</li></ul> |

{style="table-layout:auto"}

**Documentação nova ou atualizada**

| Atualização da documentação | Descrição |
| --- | --- |
| Nova página inicial de documentação do Real-Time CDP | Visite a [nova página inicial da documentação do Real-Time CDP](/help/rtcdp/home.md) para obter informações resumidas sobre como começar a usar o produto, medidas de proteção, exemplo de caso de uso e muito mais. |
| Visão geral de casos de uso de exemplo do Real-Time CDP | Visite a [nova página de visão geral de casos de uso de exemplo](/help/rtcdp/use-case-guides/overview.md) para obter uma coleção de casos de uso de exemplo que sua organização pode realizar com a Real-Time CDP. |

{style="table-layout:auto"}

Para saber mais sobre o Real-Time CDP, leia a [visão geral do Real-Time CDP](../../rtcdp/overview.md).

## Perfil do cliente em tempo real {#profile}

A Adobe Experience Platform permite gerar experiências coordenadas, consistentes e relevantes para seus clientes, independentemente de onde ou quando eles interagem com sua marca. Com o Perfil do cliente em tempo real, é possível ter uma visão integral de cada cliente ao combinar dados de vários canais, incluindo online, offline, CRM e de terceiros. O Perfil permite consolidar os dados do cliente em uma visualização unificada, oferecendo uma conta acionável com carimbo de data e hora de cada interação com o cliente.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Melhorias na localização dos cartões de painel padrão do visualizador de perfil | Os cartões de perfil padrão agora terão nomes localizados dinamicamente. Os cartões de perfil personalizados podem continuar tendo nomes personalizados que podem ser editados. |

{style="table-layout:auto"}

Para saber mais sobre o Perfil de cliente em tempo real, leia a [Visão geral do perfil](../../profile/home.md)

## Serviço de segmentação {#segmentation}

O [!DNL Segmentation Service] define um subconjunto específico de perfis descrevendo os critérios que distinguem um grupo de pessoas na sua base de clientes que pode ser direcionado por campanhas de marketing. Os segmentos podem ser baseados em dados de registro (como informações demográficas) ou em eventos de séries temporais que representam interações de clientes com sua marca.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| ------- | ----------- |
| Upload de público gerado externamente | O número máximo de colunas foi aumentado para **25**. |
| Estimativas do Construtor de segmentos | Estimativas e perfis qualificados agora são exibidos na seção de propriedades do público-alvo. Para obter mais informações sobre esta alteração, leia o [Guia da interface do usuário do Construtor de segmentos](../../segmentation/ui/segment-builder.md). |

{style="table-layout:auto"}

Para obter mais informações sobre o [!DNL Segmentation Service], consulte a [Visão geral de segmentação](../../segmentation/home.md).

## Origens {#sources}

A Experience Platform fornece uma API RESTful e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar a sistemas de armazenamento externos e serviços de CRM, definir períodos para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL Oracle NetSuite] fontes | Use as integrações do [!DNL Oracle NetSuite] no catálogo de fontes para trazer dados de suas contas do [[!DNL Oracle NetSuite Activities]](../../sources/tutorials/ui/create/marketing-automation/oracle-netsuite-activities.md) e do [[!DNL Oracle NetSuite Entities]](../../sources/tutorials/ui/create/marketing-automation/oracle-netsuite-entities.md) para a Experience Platform. |
| [!BADGE Beta]{type=Informative} [!DNL Braze Currents] origem | Use a integração do [[!DNL Braze Currents]](../../sources/tutorials/ui/create/marketing-automation/braze.md) no catálogo de fontes para trazer dados da sua conta do [!DNL Braze] para a Experience Platform. |
| Suporte para autenticação de par de chaves para a origem em lote [!DNL Snowflake] | Agora você pode usar a autenticação de par de chaves ao criar uma nova conta do [!DNL Snowflake] para dados em lote. Para obter mais informações, leia o manual sobre [criação de uma [!DNL Snowflake] conta usando a API](../../sources/tutorials/api/create/databases/snowflake.md) ou o manual sobre [criação de uma [!DNL Snowflake] conta usando a interface](../../sources/tutorials/ui/create/databases/snowflake.md). |

{style="table-layout:auto"}

Para saber mais sobre origens, leia a [visão geral de origens](../../sources/home.md).
