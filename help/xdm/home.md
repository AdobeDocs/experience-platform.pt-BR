---
keywords: Experience Platform;home;popular topics;XDM;sistema XDM individual;perfil XDM ExperienceEvent;Evento XDM Experience;experienceEvent;experience evento;Mixins;mixin;Mixin;Experience evento;XDM Experience Evento;XDM Experience ExperienceEvent;experienceEvent;experienceEvent;XDM Experience ExperienceEvent;experience data model;Experience data model;Experience data model;Experience Data Model;modelo;Modelo;Modelo de dados;Registro do schema;Registro do Schema;Biblioteca de schema;Biblioteca de Schema;schema;registro de dados;série de tempo;série de tempo;modelo;Modelo de dados;Registro de ;Registro de ;Biblioteca de ;Biblioteca de;de registros de dados;série de tempo;série de tempo
solution: Experience Platform
title: Visão geral do sistema XDM
topic: overview
description: 'A normalização e a interoperabilidade são conceitos-chave por trás da Adobe Experience Platform. O Experience Data Model (XDM), desenvolvido pela Adobe, é um esforço para padronizar os dados de experiência do cliente e definir schemas para o gerenciamento da experiência do cliente. '
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '1642'
ht-degree: 2%

---


# Visão geral do sistema XDM

A normalização e a interoperabilidade são conceitos-chave por trás da Adobe Experience Platform. [!DNL Experience Data Model] (XDM), impulsionado pelo Adobe, é um esforço para padronizar os dados de experiência do cliente e definir schemas para o gerenciamento da experiência do cliente.

A XDM é uma especificação publicamente documentada projetada para melhorar o poder das experiências digitais. Fornece estruturas e definições comuns para qualquer aplicativo a ser usado para se comunicar com os serviços [!DNL Platform]. Ao aderir aos padrões XDM, todos os dados de experiência do cliente podem ser incorporados a uma representação comum que pode fornecer insights de uma forma mais rápida e integrada. Você pode obter informações valiosas das ações do cliente, definir audiências do cliente por meio de segmentos e expressar atributos do cliente para fins de personalização.

O XDM é a estrutura fundamental que permite à Adobe Experience Cloud, capacitada por [!DNL Experience Platform], entregar a mensagem certa para a pessoa certa, no canal certo, no momento exato. A metodologia na qual [!DNL Experience Platform] é criado, o Sistema XDM, opera schemas [!DNL Experience Data Model] para uso pelos serviços [!DNL Platform].

Este documento fornece uma visão geral da função do Sistema XDM em [!DNL Experience Platform].

## Schemas XDM

[!DNL Experience Platform]A utiliza esquemas para descrever a estrutura dos dados de forma consistente e reutilizável. Ao definir os dados de forma consistente em todos os sistemas, fica mais fácil manter o significado e, portanto, obter valor dos dados.

Para que os dados possam ser ingeridos em [!DNL Platform], um schema deve ser composto para descrever a estrutura dos dados e fornecer restrições ao tipo de dados que pode ser contido em cada campo. Schemas consistem em uma classe base e zero ou mais combinações.

Para obter mais informações sobre o modelo de composição do schema, incluindo princípios de design e práticas recomendadas, consulte as [noções básicas de composição do schema](schema/composition.md).

### [!DNL Schema Registry] e [!DNL Schema Library]

O **[!DNL Schema Registry]** fornece uma interface de usuário e uma RESTful API da qual você pode visualização e gerenciar todos os recursos relacionados ao schema no Adobe Experience Platform **[!DNL Schema Library]**. O [!DNL Schema Library] contém recursos padrão do setor disponibilizados para você pelo Adobe, bem como recursos de [!DNL Experience Platform] parceiros e fornecedores cujos aplicativos você usa. A interface do usuário e a API do Registro do Schema também podem ser usadas para criar e gerenciar novos schemas e recursos exclusivos à sua organização.

Para obter um guia abrangente das principais operações disponíveis em [!DNL Schema Registry], consulte o [Guia do desenvolvedor do Registro de Schemas](api/getting-started.md).

## Comportamentos de dados no Sistema XDM {#data-behaviors}

Os dados destinados ao uso em [!DNL Experience Platform] são agrupados em dois tipos de comportamento:

* **Registrar dados**: Fornece informações sobre os atributos de um assunto. Um sujeito pode ser uma organização ou um indivíduo.
* **Dados** das séries cronológicas: Fornece um instantâneo do sistema no momento em que uma ação foi tomada, direta ou indiretamente, por um participante do registro.

Todos os schemas XDM descrevem dados que podem ser classificados como registros ou séries de tempo. O comportamento de dados de um schema é definido pela classe do schema, que é atribuída a um schema quando ele é criado pela primeira vez. As classes XDM descrevem o menor número de propriedades que um schema deve conter para representar um comportamento de dados específico.

Embora seja possível definir suas próprias classes dentro de [!DNL Schema Registry], recomenda-se que você use as classes preferenciais **[!DNL XDM Individual Profile]** e **[!DNL XDM ExperienceEvent]** para dados de registro e de série de tempo, respectivamente. Essas classes são descritas com mais detalhes abaixo.

### [!DNL XDM Individual Profile] {#xdm-individual-profile}

[!DNL XDM Individual Profile] é uma classe baseada em registros que forma uma representação singular dos atributos de indivíduos identificados e parcialmente identificados. Perfis altamente identificados podem ser usados para comunicações pessoais ou envolvimentos direcionados e podem conter informações pessoais detalhadas, como nome, gênero, data de nascimento, local e informações de contato, incluindo números de telefone e endereços de email.

Perfis menos identificados podem consistir apenas em sinais comportamentais anônimos, como cookies de navegador. Nesse caso, os dados de perfil esparsos são usados para criar uma base de informações na qual os interesses e preferências do perfil anônimo são coletados e armazenados. Esses identificadores podem se tornar mais detalhados ao longo do tempo, à medida que o assunto se inscreve para receber notificações, subscrições, compras e assim por diante. Este aumento nos atributos do perfil pode eventualmente resultar em um assunto identificado e permitir um maior grau de envolvimento direcionado.

À medida que o perfil do consumidor continua crescendo, ele se torna um repositório robusto de informações pessoais, informações de identificação, detalhes de contato e preferências de comunicação de um indivíduo.

### [!DNL XDM ExperienceEvent] {#xdm-experience-event}

O XDM ExperienceEvent é uma classe baseada em série de tempo usada para capturar o estado do sistema quando um evento (ou conjunto de eventos) ocorreu, incluindo o ponto no tempo e a identidade do assunto envolvido. Os Eventos de experiência são registros de fato do que ocorreu, portanto eles são imutáveis e representam o que aconteceu sem agregação ou interpretação. Eles são essenciais para análises de domínio de tempo, pois podem ser usados para analisar alterações que ocorrem em uma determinada janela de tempo e para comparar entre várias janelas de tempo para rastrear tendências.

Os Eventos de experiência podem ser explícitos ou implícitos. Eventos explícitos são ações humanas diretamente observáveis que ocorrem durante um ponto de uma jornada. Eventos implícitos são eventos que são criados sem uma ação humana direta, mas que ainda se relacionam com um indivíduo. Exemplos de eventos implícitos podem incluir o envio agendado de boletins informativos por email ou voltagem da bateria atingindo um determinado limite.

Embora nem todos os eventos sejam facilmente categorizados em todas as fontes de dados, é extremamente importante harmonizar eventos semelhantes em tipos semelhantes, sempre que possível, para processamento.

![Jornada do cliente ExperienceEvent](images/overview/experience-event-journey.png)

## Schemas XDM e serviços [!DNL Experience Platform]

[!DNL Experience Platform] é agnóstico do schema, o que significa que qualquer schema que esteja em conformidade com o padrão XDM está disponível para uso pelos  [!DNL Platform] serviços. As maneiras pelas quais diferentes [!DNL Platform] serviços usam schemas são descritas abaixo com mais detalhes.

### [!DNL Catalog Service], [!DNL Data Ingestion] &amp; [!DNL Data Lake]

[!DNL Catalog Service] é o sistema de registro dos  [!DNL Experience Platform] ativos e dos respectivos schemas. [!DNL Catalog] não são os arquivos ou diretórios reais que contêm dados, mas sim os metadados e as descrições desses arquivos e diretórios.

[!DNL Catalog] os dados são armazenados no,  [!DNL Data Lake]um armazenamento de dados altamente granular contendo todos os dados gerenciados por  [!DNL Platform], independentemente da origem ou do formato de arquivo.

Para começar a assimilar dados em [!DNL Experience Platform], um conjunto de dados é criado usando [!DNL Catalog Service]. O conjunto de dados faz referência a um schema XDM que descreve a estrutura dos dados a serem assimilados. Se um conjunto de dados for criado sem um schema, [!DNL Experience Platform] derivará um &quot;schema observado&quot; inspecionando o tipo e o conteúdo dos campos de dados assimilados. Os conjuntos de dados são rastreados em [!DNL Catalog] e armazenados em [!DNL Data Lake] ao lado dos schemas e dos schemas observados nos quais se baseiam.

Para obter mais informações sobre [!DNL Catalog], consulte a [visão geral do serviço de catálogo](../catalog/home.md). Para obter mais informações sobre a ingestão de dados da Adobe Experience Platform, consulte a [visão geral da ingestão de dados](../ingestion/home.md).

### [!DNL Query Service]

A Adobe Experience Platform [!DNL Query Service] permite que você use SQL padrão para dados de query [!DNL Experience Platform] para suportar muitos casos de uso diferentes.

Depois que um schema é composto e um conjunto de dados é criado que faz referência a esse schema, os dados são assimilados e armazenados em [!DNL Data Lake]. Usando [!DNL Query Service], você pode ingressar em qualquer conjunto de dados em [!DNL Data Lake] e capturar os resultados do query como um novo conjunto de dados para uso em relatórios, aprendizado de máquina ou para ingestão em [!DNL Real-time Customer Profile].

Para saber mais sobre [!DNL Query Service], consulte [Introdução ao serviço de Query](../query-service/home.md).

### [!DNL Real-time Customer Profile]

O Perfil do cliente em tempo real oferece um perfil centralizado para o gerenciamento de experiências direcionado e personalizado. Cada perfil contém dados agregados em todos os sistemas, bem como contas acionáveis com carimbos de data e hora de eventos que envolvam o indivíduo que ocorreram em qualquer um dos sistemas que você usa com [!DNL Experience Platform].

[!DNL Real-time Customer Profile] consome dados formatados em schemas com base nas  [!DNL XDM Individual Profile] ou  [!DNL XDM ExperienceEvent] classes e responde a query com base nesses dados. [!DNL Profile] não suporta o uso de schemas com base em outras classes.

[!DNL Profile] mantém uma instância de cada perfil do cliente, unindo dados para formar uma &quot;única fonte de verdade&quot; para o indivíduo. Esses dados unificados são representados usando o que é conhecido como &quot;visualização de união&quot;. Uma visualização união agregação os campos de todos os schemas que implementam a mesma classe em um único schema.  Ao compor um schema usando a interface do usuário ou a API, você pode ativar o schema para uso com [!DNL Real-time Customer Profile] e marcá-lo para inclusão na visualização da união. O schema marcado participará da definição do schema que está sendo alimentado para [!DNL Profile].

Como os dados [!DNL XDM Individual Profile] e [!DNL XDM ExperienceEvent] são assimilados e gerenciados por [!DNL Catalog], aciona [!DNL Real-time Customer Profile] para começar a assimilar dados que foram habilitados para uso. Quanto mais interações e detalhes forem ingeridos, mais robustos serão os perfis individuais.

[!DNL XDM Individual Profile] os dados ajudam a informar e capacitar ações em qualquer integração de canal ou solução de Adobe e, quando combinados a um histórico avançado de dados comportamentais e de interação, esses dados são usados para potencializar o aprendizado de máquinas. A API [!DNL Real-time Customer Profile] também pode ser usada para aprimorar a funcionalidade de soluções de terceiros, CRMs e soluções proprietárias.

Consulte [Visão geral do Perfil do cliente em tempo real](../profile/home.md) para obter mais informações.

### [!DNL Data Science Workspace]

A Adobe Experience Platform [!DNL Data Science Workspace] usa o aprendizado da máquina e a inteligência artificial para obter insights dos dados armazenados em [!DNL Experience Platform]. [!DNL Data Science Workspace] permite que os cientistas de dados construam receitas com base no XDM Individual  [!DNL Profile] e  [!DNL XDM ExperienceEvent] dados sobre clientes e suas atividades, facilitando previsões como a propensão de compra e ofertas recomendadas que o indivíduo provavelmente apreciará e usará.

Com [!DNL Data Science Workspace], os cientistas de dados podem criar facilmente APIs de serviços inteligentes acionadas pelo aprendizado de máquina. Esses serviços funcionam com outras soluções de Adobe, incluindo Adobe Target e Adobe Analytics Cloud, para ajudar a automatizar experiências digitais personalizadas e direcionadas.

Para obter mais informações sobre como usar [!DNL Experience Platform] dados para fornecer insights, consulte a [visão geral da Data Science Workspace](../data-science-workspace/home.md).

## Próximos passos e recursos adicionais

Agora que você melhor entende o papel dos schemas em [!DNL Experience Platform], você está pronto para start compondo o seu próprio. Para continuar complementando seu aprendizado, leia a documentação sugerida e assista ao vídeo abaixo.

Para aprender os princípios de design e as práticas recomendadas para a composição de schemas a serem usados com [!DNL Experience Platform], comece lendo as [noções básicas de composição de schemas](schema/composition.md). Para obter instruções passo a passo sobre como criar um schema, consulte os tutoriais sobre como criar um schema [usando a API](tutorials/create-schema-api.md) ou [usando a interface do usuário](tutorials/create-schema-ui.md).

Para reforçar sua compreensão de [!DNL XDM System] em [!DNL Experience Platform], assista ao seguinte vídeo:

>[!VIDEO](https://video.tv.adobe.com/v/27105?quality=12&learn=on)

