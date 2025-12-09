---
keywords: Experience Platform;página inicial;tópicos populares;XDM;Sistema XDM;Perfil individual XDM;Evento de experiência XDM;Evento de experiência XDM;Evento de experiência;Grupos de campos;Grupos de campos;Grupo de campos;Evento de experiência;Evento de experiência XDM;Evento de experiência XDM;Evento de experiência;Evento de experiência;Evento de experiência XDM;Evento de experiência;Modelo de dados de experiência;Modelo de dados de experiência;Modelo de dados;Modelo de dados;Registro de esquemas;Biblioteca de esquemas;esquema;dados de registros;série temporal;série temporal
solution: Experience Platform
title: Visão geral do sistema XDM
description: A padronização e a interoperabilidade são os principais conceitos por trás da Adobe Experience Platform. O Experience Data Model (XDM), orientado pela Adobe, é um esforço para padronizar os dados de experiência do cliente e definir esquemas para o gerenciamento da experiência do cliente.
exl-id: 294d5f02-850f-47ea-9333-8b94a0bb291e
source-git-commit: 491588dab1388755176b5e00f9d8ae3e49b7f856
workflow-type: tm+mt
source-wordcount: '2411'
ht-degree: 3%

---

# Visão geral do sistema XDM

A padronização e a interoperabilidade são os principais conceitos por trás da Adobe Experience Platform. O Experience Data Model (XDM), orientado pela Adobe, é um esforço para padronizar os dados de experiência do cliente e definir esquemas para o gerenciamento da experiência do cliente.

O XDM é uma especificação documentada publicamente projetada para melhorar o potencial das experiências digitais. Ela fornece estruturas e definições comuns que permitem que qualquer aplicativo seja usado para se comunicar com os serviços da Experience Platform. Seguindo os padrões XDM, todos os dados de experiência do cliente podem ser incorporados a uma representação comum que pode fornecer insights de maneira mais rápida e integrada. Você pode obter insights valiosos das ações do cliente, definir públicos-alvo do cliente por meio de segmentos e expressar atributos do cliente para fins de personalização.

O XDM é a estrutura fundamental que permite ao Adobe Experience Cloud, viabilizado pelo Experience Platform, enviar a mensagem certa à pessoa certa, no canal certo, no momento exato. A metodologia na qual o Experience Platform é criado, o Sistema XDM, operacionaliza esquemas do Modelo de dados de experiência para uso pelos serviços da Experience Platform.

Saiba mais sobre a função do Sistema XDM no Experience Platform.

## Esquemas XDM {#xdm-schemas}

A Experience Platform usa esquemas para descrever a estrutura dos dados de forma consistente e reutilizável. Ao definir os dados de forma consistente em todos os sistemas, fica mais fácil manter o significado e, portanto, obter valor dos dados.

Antes que os dados possam ser assimilados na Experience Platform, um esquema deve ser composto para descrever a estrutura dos dados e fornecer restrições ao tipo de dados que podem estar contidos em cada campo. Os esquemas consistem em uma classe base e zero ou mais grupos de campos de esquema.

Para obter mais informações sobre o modelo de composição de esquema, incluindo princípios de design e práticas recomendadas, consulte as [noções básicas da composição de esquema](schema/composition.md).

### Componentes XDM padrão {#Standard-xdm-components}

O XDM fornece uma coleção eficiente de grupos de campos e tipos de dados padrão, que têm como objetivo capturar conceitos e casos de uso comuns em diferentes setores. O Experience Platform permite filtrar esses componentes por setor, permitindo criar esquemas de forma rápida e segura que melhor atendam às necessidades específicas da sua empresa.

Ao construir esquemas na interface do Experience Platform, os grupos de campos listados são mostrados com uma métrica de popularidade. Essa métrica é determinada pela frequência com que outros usuários do Experience Platform usam o grupo de campos em seus esquemas. Quanto maior o número, mais popular será o grupo de campos. Por padrão, os resultados são exibidos de mais popular a menos popular, mantendo você informado sobre as tendências de modelagem de dados do seu setor.

![A coluna de popularidade da caixa de diálogo [!UICONTROL Add field group].](./images/overview/popularity.png)

### [!DNL Schema Library] {#schema-library}

O Experience Platform fornece uma interface de usuário e uma API RESTful a partir das quais você pode exibir e gerenciar todos os recursos relacionados ao esquema no Experience Platform **[!DNL Schema Library]**. O [!DNL Schema Library] contém componentes XDM padrão disponibilizados a você pela Adobe, bem como recursos de parceiros e fornecedores da Experience Platform cujos aplicativos você usa.

Você também pode criar e gerenciar novos esquemas e recursos que sejam exclusivos para sua organização usando o [!DNL Schema Registry API] ou o espaço de trabalho [!UICONTROL Schemas] na interface de usuário do Experience Platform.

Para obter mais informações sobre como gerenciar e interagir com schemas no Experience Platform, consulte a seguinte documentação:

* [Guia da interface do XDM](./ui/overview.md)
* [Guia da API do registro de esquema](./api/overview.md)

## Comportamentos de dados no sistema XDM {#data-behaviors}

>[!CONTEXTUALHELP]
>id="platform_schemas_behavior"
>title="Comportamentos de dados"
>abstract="Os dados destinados ao uso na Experience Platform são agrupados em três tipos de comportamento: registro, série de tempo e ad hoc. Os esquemas de registro fornecem informações sobre os atributos de um assunto, enquanto os esquemas de séries de tempo capturam um instantâneo do sistema no momento em que uma ação foi tomada. Os esquemas ad hoc capturam campos que são namespaces usados somente por um único conjunto de dados. Consulte a documentação para obter mais informações sobre comportamentos de dados na Experience Platform."

Os dados destinados ao uso no Experience Platform são agrupados em três tipos de comportamento:

* **Registro**: fornece informações sobre os atributos de um assunto. Um assunto pode ser uma organização ou um indivíduo.
* **Série temporal**: fornece um instantâneo do sistema no momento em que uma ação foi tomada direta ou indiretamente por um assunto de registro.
* **Ad-hoc**: captura campos com namespace para uso somente por um único conjunto de dados. Esquemas ad-hoc são usados em vários workflows de assimilação de dados para o Experience Platform, incluindo a assimilação de arquivos CSV e a criação de determinados tipos de conexões de origem.

Todos os esquemas XDM descrevem dados que podem ser categorizados como registro ou série de tempo. O comportamento dos dados de um schema é definido pela classe do schema, que é atribuída a um schema quando ele é criado pela primeira vez. As classes XDM descrevem o menor número de propriedades que um esquema deve conter para representar um comportamento de dados específico.

Embora você possa definir suas próprias classes no [!DNL Schema Registry], é recomendável usar as classes padrão **[!UICONTROL XDM Individual Profile]** e **[!UICONTROL XDM ExperienceEvent]** para dados de registro e série temporal, respectivamente. Essas classes são descritas mais detalhadamente abaixo.

>[!NOTE]
>
>Não há classes padrão baseadas no comportamento ad-hoc. Esquemas ad-hoc são gerados automaticamente pelos processos Experience Platform que os utilizam, mas também podem ser [criados manualmente usando a API do Registro de Esquemas](./tutorials/ad-hoc.md).

### [!UICONTROL XDM Individual Profile] {#xdm-individual-profile}

[!UICONTROL XDM Individual Profile] é uma classe baseada em registros que forma uma representação singular dos atributos de indivíduos identificados e parcialmente identificados. Os perfis altamente identificados podem ser usados para comunicações pessoais ou engajamentos direcionados. Perfis altamente identificados podem conter informações pessoais detalhadas, como nome, sexo, data de nascimento, local e informações de contato, incluindo números de telefone e endereços de email.

Perfis menos identificados podem consistir apenas em sinais comportamentais anônimos, como cookies do navegador. Nesse caso, os dados esparsos do perfil são usados para criar uma base de informações na qual os interesses e as preferências do perfil anônimo são agrupados e armazenados. Esses identificadores podem se tornar mais detalhados ao longo do tempo, à medida que o assunto se inscreve para notificações, assinaturas, compras e assim por diante. Esse aumento nos atributos do perfil pode eventualmente resultar em um assunto identificado e permitir um grau mais alto de envolvimento direcionado.

À medida que o perfil continua a crescer, ele se torna um repositório robusto de informações pessoais, informações de identificação, detalhes de contato e preferências de comunicação de um indivíduo.

Consulte o [[!UICONTROL XDM Individual Profile] guia de referência](./classes/individual-profile.md) para obter mais informações sobre a estrutura e caso de uso dos campos fornecidos pela classe.

### [!UICONTROL XDM ExperienceEvent] {#xdm-experience-event}

XDM ExperienceEvent é uma classe baseada em séries de tempo usada para capturar o estado do sistema quando um evento (ou conjunto de eventos) ocorreu, incluindo o momento e a identidade do assunto envolvido. Eventos de experiência são registros fatuais imutáveis do que ocorreu naquele momento, representando o que aconteceu sem agregação ou interpretação. Eles são essenciais para a análise de domínio de tempo, pois podem ser usados para analisar alterações que ocorrem em uma determinada janela de tempo e para comparar entre várias janelas de tempo para rastrear tendências.

Os Eventos de experiência podem ser explícitos ou implícitos. Eventos explícitos são ações humanas diretamente observáveis que ocorrem durante um ponto em uma jornada. Eventos implícitos são eventos que são gerados sem uma ação humana direta, mas ainda se relacionam com um indivíduo. Exemplos de eventos implícitos podem incluir o envio agendado de boletins informativos por email ou a tensão da bateria que atinge um determinado limite.

Embora nem todos os eventos sejam facilmente categorizados em todas as fontes de dados, é extremamente valioso harmonizar eventos semelhantes em tipos semelhantes, quando possível, para processamento.

![Um infográfico da Jornada do cliente visualizado com eventos de experiência ao longo do tempo.](images/overview/experience-event-journey.png)

Consulte o [[!UICONTROL XDM ExperienceEvent] guia de referência](./classes/experienceevent.md) para obter mais informações sobre a estrutura e caso de uso dos campos fornecidos pela classe.

## Esquemas XDM e serviços da Experience Platform {#schemas-and-platform-services}

O Experience Platform é independente de esquema, o que significa que qualquer esquema que esteja em conformidade com o padrão XDM é disponibilizado para os serviços da Experience Platform. As maneiras como diferentes serviços da Experience Platform usam esquemas são descritas com mais detalhes abaixo.

### Serviço de catálogo, assimilação de dados e data lake {#ingestion-catalog-and-storage}

O Serviço de catálogo é o sistema de registro de ativos do Experience Platform e seus esquemas relacionados. O catálogo não contém os arquivos ou diretórios de dados reais, mas contém os metadados e as descrições desses arquivos e diretórios.

Os dados do catálogo são armazenados no data lake, um armazenamento de dados altamente granular que contém todos os dados gerenciados pela Experience Platform, independentemente da origem ou do formato de arquivo.

Para começar a assimilar dados na Experience Platform, você pode usar o Serviço de catálogo para criar um conjunto de dados. O conjunto de dados faz referência a um esquema XDM que descreve a estrutura dos dados que serão assimilados. Se um conjunto de dados for criado sem um esquema, a Experience Platform deriva um &quot;esquema observado&quot; ao inspecionar o tipo e o conteúdo dos campos de dados assimilados. Os conjuntos de dados são rastreados no Serviço de catálogo e armazenados no lago de dados ao lado dos esquemas e esquemas observados nos quais se baseiam.

Consulte a [Visão geral do Serviço de Catálogo](../catalog/home.md) para obter mais informações. Consulte a [Visão geral da assimilação de dados](../ingestion/home.md) para obter mais informações sobre a assimilação de dados do Adobe Experience Platform.

### Data Mirror e esquemas relacionais {#relational-schemas}

>[!AVAILABILITY]
>
>O Data Mirror e esquemas relacionais estão disponíveis para os **titulares de licença de campanhas orquestradas** da Adobe Journey Optimizer. Eles também estão disponíveis como uma **versão limitada** para usuários do Customer Journey Analytics, dependendo da sua licença e da ativação de recursos. Entre em contato com o representante da Adobe para obter acesso.

O Data Mirror é um recurso do Adobe Experience Platform que permite a sincronização avançada do banco de dados usando esquemas relacionais. Para obter uma visão geral completa dos recursos e casos de uso do Data Mirror, consulte a [visão geral do Data Mirror](./data-mirror/overview.md).

O Data Mirror opera por meio de esquemas relacionais, que são projetados para padrões de dados estruturados e de estilo relacional. Eles impõem chaves primárias, aceitam identificadores de versão e definem relações esquema a esquema usando chaves primárias e estrangeiras. Diferentemente dos esquemas XDM padrão, eles não exigem classes ou grupos de campos e são otimizados para alterar os fluxos de trabalho de assimilação de captura de dados.

Para obter detalhes sobre como definir relações esquema a esquema, consulte a [documentação do endpoint de descritores](./api/descriptors.md).

Use o Data Mirror quando precisar:

* Sincronizar alterações de dados de sistemas externos, como Snowflake, Databricks ou BigQuery
* Preservar as relações do banco de dados e impor a integridade dos dados durante a assimilação
* Suporte à análise avançada e à orquestração de jornadas
* Habilitar o controle preciso de alterações com substituições e exclusões

Para criar um esquema relacional, selecione **[!UICONTROL Relational]** ao criar um esquema. Esquemas relacionais não usam classes ou grupos de campos. Em vez disso, defina a estrutura manualmente ou faça upload de um arquivo DDL. Esquemas relacionais exigem uma chave primária, um identificador de versão e, se aplicável, campos de identificador de carimbo de data e hora. Em seguida, você pode configurar campos adicionais e definir relações com outros esquemas.

>[!NOTE]
>
>As colunas de controle usadas durante a assimilação (como `_change_request_type` para fluxos de trabalho de captura de dados de alteração) são lidas no momento da assimilação e não são armazenadas no esquema nem mapeadas para campos XDM. Os esquemas relacionais estão disponíveis com direitos apropriados do Experience Platform e ativação de recursos.

Para obter as etapas detalhadas e as orientações para o caso de uso, consulte:

* [Visão geral do Data Mirror](./data-mirror/overview.md) - Recursos, casos de uso e planejamento de implementação
* [Referência técnica de esquema relacional](./schema/relational.md) - Especificações técnicas e restrições
* [Tutorial de interface do usuário](./ui/resources/schemas.md#create-relational-schema)
* [Tutorial de API](./api/schemas.md#create-relational-schema)
* [Documentação do descritor (identificador)](./api/descriptors.md#relationship-descriptor)
* [Habilitar captura de dados de alteração](../sources/tutorials/api/change-data-capture.md)

### Serviço de consultas {#query-service}

Você pode usar o SQL padrão para consultar dados do Experience Platform e oferecer suporte a vários casos de uso diferentes com o Serviço de consulta da Adobe Experience Platform.

Depois que um esquema é composto e um conjunto de dados que faz referência a ele, os dados são assimilados e armazenados no data lake. Em seguida, você pode usar o Serviço de consulta para ingressar em qualquer conjunto de dados no data lake e capturar os resultados da consulta como um novo conjunto de dados para usar em relatórios, aprendizado de máquina ou assimilação no Perfil do cliente em tempo real.

Consulte a [Visão geral do Serviço de consulta](../query-service/home.md) para obter mais informações sobre o serviço.

### Perfil do cliente em tempo real {#real-time-customer-profile}

O Perfil do cliente em tempo real fornece um perfil do cliente centralizado para gerenciamento de experiência direcionado e personalizado. Cada perfil contém dados agregados em todos os sistemas e inclui contas acionáveis com carimbo de data e hora de eventos que envolvem o assunto do perfil. Esses eventos podem ter ocorrido em qualquer um dos sistemas usados com o Experience Platform.

O Perfil de Cliente em Tempo Real consome dados formatados por esquema baseados nas classes [!UICONTROL XDM Individual Profile] e [!UICONTROL XDM ExperienceEvent] e responde a consultas baseadas nesses dados.

O sistema mantém uma instância de cada perfil de cliente, mesclando dados para formar uma &quot;única fonte da verdade&quot; para o indivíduo. Esses dados unificados são representados usando o que é conhecido como &quot;esquema de união&quot; (às vezes chamado de &quot;visualização de união&quot;). Um esquema de união agrega os campos de todos os esquemas que implementam a mesma classe em um único esquema. Ao compor um esquema usando a interface ou a API do, você pode ativar o esquema para uso com o Perfil do cliente em tempo real e marcá-lo para inclusão na união. O esquema marcado participará da definição do esquema que está sendo alimentado para o Perfil.

Como os dados de [!UICONTROL XDM Individual Profile] e [!UICONTROL XDM ExperienceEvent] são assimilados no data lake, o Perfil do cliente em tempo real assimila todos os dados que foram habilitados para seu uso. Quanto mais interações e detalhes forem assimilados, mais robustos os perfis individuais se tornarão.

Os dados do [!UICONTROL XDM Individual Profile] ajudam a informar e capacitar ações em qualquer canal ou integração de produtos da Adobe. Quando combinados com um histórico avançado de dados comportamentais e de interação, esses dados podem ser usados para potencializar o aprendizado de máquina. A API do Perfil do cliente em tempo real também pode ser usada para enriquecer a funcionalidade de soluções de terceiros, CRMs e soluções proprietárias.

Consulte a [Visão geral do Perfil do cliente em tempo real](../profile/home.md) para obter mais informações.

### Espaço de trabalho do Data Science {#data-science-workspace}

>[!NOTE]
>
>O Data Science Workspace não está mais disponível para compra. Esta documentação destina-se aos clientes existentes com direitos anteriores ao Data Science Workspace.

O Adobe Experience Platform Data Science Workspace usa aprendizagem de máquina e inteligência artificial para obter insights de dados armazenados no Experience Platform. O Data Science Workspace permite que cientistas de dados criem receitas com base em dados do [!UICONTROL XDM Individual Profile] e do [!UICONTROL XDM ExperienceEvent] sobre clientes e suas atividades. Essas receitas facilitam previsões, como propensão de compra e ofertas recomendadas que o indivíduo provavelmente apreciará e usará.

Com o Data Science Workspace, os cientistas de dados podem criar facilmente APIs de serviço inteligentes alimentadas pelo aprendizado de máquina. Esses serviços trabalham com outras soluções da Adobe, incluindo o Adobe Target e o Adobe Analytics Cloud, para ajudar você a automatizar experiências digitais personalizadas e direcionadas.

Para obter mais informações sobre como usar dados do Experience Platform para potencializar insights, consulte a [visão geral do Data Science Workspace](../data-science-workspace/home.md).

## Próximas etapas e recursos adicionais

Agora que você entende melhor a função dos esquemas em todo o Experience Platform, você está pronto para começar a compor os seus próprios.

Para saber mais sobre os princípios de design e as práticas recomendadas para compor esquemas a serem usados com o Experience Platform, comece lendo as [noções básicas da composição de esquema](schema/composition.md). Para obter instruções passo a passo sobre como criar um esquema, consulte os tutoriais em criação de um esquema [usando a API](tutorials/create-schema-api.md) ou [usando a interface do usuário](tutorials/create-schema-ui.md).

Para reforçar sua compreensão do [!DNL XDM System] no Experience Platform, assista ao vídeo a seguir:

>[!VIDEO](https://video.tv.adobe.com/v/27105?quality=12&learn=on)
