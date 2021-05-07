---
keywords: Experience Platform; home; tópicos populares; XDM; sistema XDM; perfil individual XDM; XDM ExperienceEvent; Evento de experiência XDM; evento de experiência; evento de experiência; grupos de campos; grupo de campos; grupo de campos; grupo de campos; evento de experiência; Evento de experiência XDM; ExperienceEvent; evento de experiência; evento de experiência XDM; modelo de dados de experiência; modelo de dados de experiência; modelo de dados; Registro de esquema, Registro de esquema, biblioteca de esquema, Biblioteca de esquema, esquema, dados de registro, série de tempo, série de tempo
solution: Experience Platform
title: Visão geral do sistema XDM
topic-legacy: overview
description: A padronização e a interoperabilidade são conceitos-chave por trás do Adobe Experience Platform. O Experience Data Model (XDM), impulsionado pelo Adobe, é um esforço para padronizar os dados de experiência do cliente e definir esquemas para o gerenciamento da experiência do cliente.
exl-id: 294d5f02-850f-47ea-9333-8b94a0bb291e
translation-type: tm+mt
source-git-commit: b70e693b4ffeda561de4d4c8dd8fd1adeec489f7
workflow-type: tm+mt
source-wordcount: '1694'
ht-degree: 1%

---

# Visão geral do sistema XDM

>[!NOTE]
>
>O termo &quot;mixin&quot; foi atualizado para &quot;grupo de campos&quot; do schema para promover a compreensão. Grupos de campos são conjuntos reutilizáveis de campos para suportar casos de uso de negócios. Essa alteração agora é refletida na API do Registro de Schema, na interface do usuário do Adobe Experience Platform e em toda a documentação da plataforma.

A padronização e a interoperabilidade são conceitos-chave por trás do Adobe Experience Platform. [!DNL Experience Data Model] O (XDM), impulsionado pelo Adobe, é um esforço para padronizar os dados de experiência do cliente e definir esquemas para o gerenciamento da experiência do cliente.

O XDM é uma especificação publicamente documentada projetada para melhorar o poder das experiências digitais. Ele fornece estruturas e definições comuns para qualquer aplicativo usar para se comunicar com os serviços [!DNL Platform]. Ao seguir os padrões XDM, todos os dados de experiência do cliente podem ser incorporados a uma representação comum que pode fornecer insights de uma maneira mais rápida e integrada. Você pode obter informações valiosas das ações do cliente, definir públicos-alvo do cliente por meio de segmentos e expressar atributos do cliente para fins de personalização.

O XDM é a estrutura fundamental que permite que o Adobe Experience Cloud, desenvolvido por [!DNL Experience Platform], forneça a mensagem certa à pessoa certa, no canal certo, no momento certo. A metodologia na qual [!DNL Experience Platform] é criado, o Sistema XDM, opera [!DNL Experience Data Model] esquemas para uso pelos serviços [!DNL Platform].

Este documento fornece uma visão geral da função do Sistema XDM em [!DNL Experience Platform].

## Esquemas XDM

[!DNL Experience Platform]A utiliza esquemas para descrever a estrutura dos dados de forma consistente e reutilizável. Ao definir os dados de forma consistente em todos os sistemas, fica mais fácil manter o significado e, portanto, obter valor dos dados.

Para que os dados possam ser assimilados em [!DNL Platform], um schema deve ser composto para descrever a estrutura dos dados e fornecer restrições ao tipo de dados que pode ser contido em cada campo. Os esquemas consistem em uma classe base e zero ou mais grupos de campos de esquema.

Para obter mais informações sobre o modelo de composição do schema, incluindo princípios de design e práticas recomendadas, consulte as [noções básicas da composição do schema](schema/composition.md).

### [!DNL Schema Registry] e [!DNL Schema Library]

O **[!DNL Schema Registry]** fornece uma interface de usuário e a API RESTful a partir da qual você pode visualizar e gerenciar todos os recursos relacionados ao schema no Adobe Experience Platform **[!DNL Schema Library]**. O [!DNL Schema Library] contém recursos padrão do setor disponibilizados para você pelo Adobe, bem como recursos de [!DNL Experience Platform] parceiros e fornecedores cujos aplicativos você usa. A interface do usuário e a API do Registro de Schema também podem ser usadas para criar e gerenciar novos esquemas e recursos exclusivos de sua organização.

Para obter um guia abrangente das principais operações disponíveis no [!DNL Schema Registry], consulte o [Guia do desenvolvedor do Registro de Schema](api/getting-started.md).

## Comportamentos de dados no Sistema XDM {#data-behaviors}

Os dados destinados ao uso em [!DNL Experience Platform] são agrupados em dois tipos de comportamento:

* **Registrar dados**: Fornece informações sobre os atributos de um assunto. Um assunto pode ser uma organização ou um indivíduo.
* **Dados** das séries cronológicas: Fornece um instantâneo do sistema no momento em que uma ação foi tomada direta ou indiretamente por um titular de registro.

Todos os esquemas XDM descrevem dados que podem ser categorizados como registro ou série de tempo. O comportamento de dados de um schema é definido pela classe do schema, que é atribuída a um schema quando ele é criado pela primeira vez. As classes XDM descrevem o menor número de propriedades que um schema deve conter para representar um comportamento de dados específico.

Embora seja possível definir suas próprias classes no [!DNL Schema Registry], é recomendável usar as classes preferidas **[!DNL XDM Individual Profile]** e **[!DNL XDM ExperienceEvent]** para dados de registro e de série de tempo, respectivamente. Essas classes são descritas com mais detalhes abaixo.

### [!DNL XDM Individual Profile] {#xdm-individual-profile}

[!DNL XDM Individual Profile] é uma classe baseada em registros que forma uma representação singular dos atributos de indivíduos identificados e parcialmente identificados. Os perfis altamente identificados podem ser usados para comunicações pessoais ou participações direcionadas e podem conter informações pessoais detalhadas, como nome, gênero, data de nascimento, local e informações de contato, incluindo números de telefone e endereços de email.

Os perfis menos identificados podem consistir apenas de sinais comportamentais anônimos, como cookies do navegador. Nesse caso, os dados de perfil esparsos são usados para criar uma base de informações na qual os interesses e as preferências do perfil anônimo são coletados e armazenados. Esses identificadores podem se tornar mais detalhados ao longo do tempo, à medida que o assunto se inscreve para notificações, assinaturas, compras e assim por diante. Esse aumento nos atributos do perfil pode eventualmente resultar em um assunto identificado e permitir um grau mais alto de envolvimento direcionado.

À medida que um perfil do consumidor continua a crescer, ele se torna um repositório robusto de informações pessoais, informações de identificação, detalhes de contato e preferências de comunicação de um indivíduo.

### [!DNL XDM ExperienceEvent] {#xdm-experience-event}

O XDM ExperienceEvent é uma classe baseada em séries de tempo usada para capturar o estado do sistema quando um evento (ou conjunto de eventos) ocorreu, incluindo o ponto no tempo e a identidade do assunto envolvido. Os Eventos de experiência são registros de fatos do que aconteceu, portanto, são imutáveis e representam o que aconteceu sem agregação ou interpretação. Elas são essenciais para a análise de domínio de tempo, pois podem ser usadas para analisar alterações que ocorrem em uma determinada janela de tempo e para comparar entre várias janelas de tempo para rastrear tendências.

Os Eventos de experiência podem ser explícitos ou implícitos. Acontecimentos explícitos são ações humanas diretamente observáveis que ocorrem durante um ponto de uma jornada. Acontecimentos implícitos são acontecimentos que são levantados sem uma ação humana direta, mas que ainda estão relacionados com um indivíduo. Exemplos de eventos implícitos podem incluir o envio agendado de informativos por email ou voltagem da bateria atingindo um determinado limite.

Embora nem todos os eventos sejam facilmente categorizados em todas as fontes de dados, é extremamente valioso harmonizar eventos semelhantes em tipos semelhantes, sempre que possível, para processamento.

![Jornada do cliente ExperienceEvent](images/overview/experience-event-journey.png)

## Esquemas e serviços XDM [!DNL Experience Platform]

[!DNL Experience Platform] é independente de esquema, o que significa que qualquer esquema que esteja em conformidade com o padrão XDM está disponível para uso pelos  [!DNL Platform] serviços. As maneiras pelas quais diferentes serviços [!DNL Platform] usam esquemas são descritas mais detalhadamente abaixo.

### [!DNL Catalog Service], [!DNL Data Ingestion] &amp; [!DNL Data Lake]

[!DNL Catalog Service] é o sistema de registro de  [!DNL Experience Platform] ativos e seus esquemas relacionados. [!DNL Catalog] não são os arquivos ou diretórios reais que contêm dados, mas sim os metadados e as descrições desses arquivos e diretórios.

[!DNL Catalog] Os dados são armazenados no  [!DNL Data Lake], um armazenamento de dados altamente granular que contém todos os dados gerenciados pelo  [!DNL Platform], independentemente da origem ou do formato de arquivo.

Para começar a assimilar dados em [!DNL Experience Platform], um conjunto de dados é criado usando [!DNL Catalog Service]. O conjunto de dados faz referência a um esquema XDM que descreve a estrutura dos dados a serem assimilados. Se um conjunto de dados for criado sem um esquema, [!DNL Experience Platform] derivará um &quot;schema observado&quot; ao inspecionar o tipo e o conteúdo dos campos de dados assimilados. Os conjuntos de dados são rastreados em [!DNL Catalog] e armazenados no [!DNL Data Lake] ao lado dos schemas e dos schemas observados em que se baseiam.

Para obter mais informações sobre [!DNL Catalog], consulte a [Visão geral do Serviço de Catálogo](../catalog/home.md). Para obter mais informações sobre a Ingestão de dados do Adobe Experience Platform, consulte a [Visão geral da Ingestão de dados](../ingestion/home.md).

### [!DNL Query Service]

O Adobe Experience Platform [!DNL Query Service] permite usar o SQL padrão para consultar dados [!DNL Experience Platform] para suportar muitos casos de uso diferentes.

Depois que um esquema é composto e um conjunto de dados que faz referência a ele, os dados são assimilados e armazenados no [!DNL Data Lake]. Usando [!DNL Query Service], você pode ingressar em qualquer conjunto de dados no [!DNL Data Lake] e capturar os resultados da consulta como um novo conjunto de dados para uso em relatórios, aprendizado de máquina ou para assimilação em [!DNL Real-time Customer Profile].

Para saber mais sobre [!DNL Query Service], consulte a [Introdução ao Serviço de Consulta](../query-service/home.md).

### [!DNL Real-time Customer Profile]

O Perfil do cliente em tempo real oferece um perfil de consumidor centralizado para gerenciamento de experiência direcionado e personalizado. Cada perfil contém dados agregados em todos os sistemas, bem como contas acionáveis com carimbos de data e hora de eventos que envolvem o indivíduo que ocorreram em qualquer um dos sistemas usados com [!DNL Experience Platform].

[!DNL Real-time Customer Profile] O consome dados formatados em esquema com base nas  [!DNL XDM Individual Profile] classes  [!DNL XDM ExperienceEvent] ou e responde a consultas com base nesses dados. [!DNL Profile] não suporta o uso de schemas com base em outras classes.

[!DNL Profile] O mantém uma instância de cada perfil de cliente, mesclando dados para formar uma &quot;única fonte de verdade&quot; para o indivíduo. Esses dados unificados são representados usando o que é conhecido como &quot;exibição de união&quot;. Uma exibição de união agrega os campos de todos os esquemas que implementam a mesma classe em um único schema.  Ao compor um esquema usando a interface do usuário ou a API, você pode habilitar o esquema para usar com [!DNL Real-time Customer Profile] e marcá-lo para inclusão na exibição de união. O schema marcado participará da definição do schema que está sendo alimentado a [!DNL Profile].

Como os dados [!DNL XDM Individual Profile] e [!DNL XDM ExperienceEvent] são assimilados e gerenciados por [!DNL Catalog], aciona [!DNL Real-time Customer Profile] para começar a assimilar dados que foram habilitados para uso. Quanto mais interações e detalhes forem assimilados, mais robustos serão os perfis individuais.

[!DNL XDM Individual Profile] Os dados do ajudam a informar e potencializar ações em qualquer integração de canal ou solução de Adobe e, quando emparelhados a um histórico avançado de dados comportamentais e de interação, esses dados são usados para potencializar o aprendizado de máquina. A API [!DNL Real-time Customer Profile] também pode ser usada para enriquecer a funcionalidade de soluções de terceiros, CRMs e soluções proprietárias.

Consulte a [Visão geral do perfil do cliente em tempo real](../profile/home.md) para obter mais informações.

### [!DNL Data Science Workspace]

O Adobe Experience Platform [!DNL Data Science Workspace] usa o aprendizado de máquina e a inteligência artificial para obter insights dos dados armazenados em [!DNL Experience Platform]. [!DNL Data Science Workspace] O permite que os cientistas de dados criem receitas com base no XDM Individual  [!DNL Profile] e  [!DNL XDM ExperienceEvent] dados sobre os clientes e suas atividades, facilitando previsões, como comprar propensão e ofertas recomendadas que o indivíduo provavelmente apreciará e usará.

Com [!DNL Data Science Workspace], os cientistas de dados podem criar facilmente APIs de serviços inteligentes capacitadas pelo aprendizado de máquina. Esses serviços trabalham com outras soluções Adobe, incluindo Adobe Target e Adobe Analytics Cloud, para ajudar você a automatizar experiências digitais personalizadas e direcionadas.

Para obter mais informações sobre como usar [!DNL Experience Platform] dados para potencializar insights, consulte a [Visão geral do Data Science Workspace](../data-science-workspace/home.md).

## Próximas etapas e recursos adicionais

Agora que você entende melhor a função dos schemas em [!DNL Experience Platform], está pronto para começar a compor os seus próprios. Para continuar complementando seu aprendizado, comece lendo a documentação sugerida e assista ao vídeo abaixo.

Para saber mais sobre os princípios de design e as práticas recomendadas para compor schemas a serem usados com [!DNL Experience Platform], comece lendo as [noções básicas da composição do schema](schema/composition.md). Para obter instruções passo a passo sobre como criar um schema, consulte os tutoriais sobre como criar um schema [usando a API](tutorials/create-schema-api.md) ou [usando a interface do usuário](tutorials/create-schema-ui.md).

Para reforçar sua compreensão de [!DNL XDM System] em [!DNL Experience Platform], assista ao vídeo a seguir:

>[!VIDEO](https://video.tv.adobe.com/v/27105?quality=12&learn=on)
