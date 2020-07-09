---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Sistema do Experience Data Model (XDM)
topic: overview
translation-type: tm+mt
source-git-commit: 8ea3b09f86fe11ce7043f22c56ff9756b909e716
workflow-type: tm+mt
source-wordcount: '1777'
ht-degree: 0%

---


# Visão geral do sistema XDM

A normalização e a interoperabilidade são conceitos-chave por detrás da Adobe Experience Platform. O Experience Data Model (XDM), desenvolvido pela Adobe, é um esforço para padronizar os dados de experiência do cliente e definir schemas para o gerenciamento da experiência do cliente.

A XDM é uma especificação publicamente documentada projetada para melhorar o poder das experiências digitais. Fornece estruturas e definições comuns para qualquer aplicativo a ser usado para se comunicar com os serviços da Platform. Ao aderir aos padrões XDM, todos os dados de experiência do cliente podem ser incorporados a uma representação comum que pode fornecer insights de uma forma mais rápida e integrada. Você pode obter informações valiosas das ações do cliente, definir audiências do cliente por meio de segmentos e expressar atributos do cliente para fins de personalização.

O XDM é a estrutura fundamental que permite à Adobe Experience Cloud, capacitada pela Experience Platform, entregar a mensagem certa para a pessoa certa, no canal certo, no momento certo. A metodologia na qual o Experience Platform é criado, o Sistema **** XDM, opera schemas do Modelo de Dados da Experiência para uso pelos serviços da Platform.

Este documento fornece uma visão geral da função do Sistema XDM no Experience Platform.

## schemas XDM

O Experience Platform usa schemas para descrever a estrutura dos dados de forma consistente e reutilizável. Ao definir os dados de forma consistente em todos os sistemas, torna-se mais fácil manter o significado e, portanto, obter valor dos dados.

Para que os dados possam ser ingeridos no Platform, um schema deve ser composto para descrever a estrutura dos dados e fornecer restrições ao tipo de dados que pode ser contido em cada campo. Schemas consistem em uma classe base e zero ou mais combinações.

Para obter mais informações sobre o modelo de composição do schema, incluindo princípios de design e práticas recomendadas, consulte os [fundamentos da composição](schema/composition.md)do schema.

### Registro do Schema e biblioteca do Schema

O Registro **do** Schema fornece uma interface de usuário e uma RESTful API da qual você pode visualização e gerenciar todos os recursos relacionados ao schema na Biblioteca **do** Schema. A Biblioteca de Schemas contém recursos padrão do setor disponibilizados pela Adobe, bem como recursos de parceiros e fornecedores de Experience Platform cujos aplicativos você usa. A interface do usuário e a API do Registro do Schema também podem ser usadas para criar e gerenciar novos schemas e recursos exclusivos à sua organização.

Para obter um guia abrangente das principais operações disponíveis no Registro do Schema, consulte o guia [do desenvolvedor do Registro do](api/getting-started.md)Schema.

## Comportamentos de dados no Sistema XDM {#data-behaviors}

Os dados destinados ao uso no Experience Platform são agrupados em dois tipos de comportamento:

* **Registrar dados**: Fornece informações sobre os atributos de um assunto. Um sujeito pode ser uma organização ou um indivíduo.
* **Dados** das séries cronológicas: Fornece um instantâneo do sistema no momento em que uma ação foi tomada, direta ou indiretamente, por um participante do registro.

Todos os schemas XDM descrevem dados que podem ser classificados como registros ou séries de tempo. O comportamento de dados de um schema é definido pela **classe** schema, que é atribuída a um schema quando ele é criado pela primeira vez. As classes XDM descrevem o menor número de propriedades que um schema deve conter para representar um comportamento de dados específico.

Embora seja possível definir suas próprias classes no Registro do Schema, recomenda-se que você use as classes preferenciais Perfil **individual** XDM e **XDM ExperienceEvent** para dados de registro e série de tempo, respectivamente. Essas classes são descritas com mais detalhes abaixo.

### Perfil individual XDM

O Perfil XDM Individual é uma classe baseada em registros que forma uma representação singular dos atributos de indivíduos identificados e parcialmente identificados. Perfis altamente identificados podem ser usados para comunicações pessoais ou envolvimentos direcionados e podem conter informações pessoais detalhadas, como nome, gênero, data de nascimento, local e informações de contato, incluindo números de telefone e endereços de email.

perfis menos identificados podem consistir apenas em sinais comportamentais anônimos, como cookies de navegador. Nesse caso, os dados de perfil esparsos são usados para criar uma base de informações na qual os interesses e preferências do perfil anônimo são coletados e armazenados. Esses identificadores podem se tornar mais detalhados ao longo do tempo, à medida que o assunto se inscreve para receber notificações, subscrições, compras e assim por diante. Este aumento nos atributos do perfil pode eventualmente resultar em um assunto identificado e permitir um maior grau de envolvimento direcionado.

À medida que o perfil do consumidor continua crescendo, ele se torna um repositório robusto de informações pessoais, informações de identificação, detalhes de contato e preferências de comunicação de um indivíduo.

### XDM ExperienceEvent

O XDM ExperienceEvent é uma classe baseada em série de tempo usada para capturar o estado do sistema quando um evento (ou conjunto de eventos) ocorreu, incluindo o ponto no tempo e a identidade do assunto envolvido. Os Eventos de experiência são registros de fato do que ocorreu, portanto eles são imutáveis e representam o que aconteceu sem agregação ou interpretação. Eles são essenciais para análises de domínio de tempo, pois podem ser usados para analisar alterações que ocorrem em uma determinada janela de tempo e para comparar entre várias janelas de tempo para rastrear tendências.

Os Eventos de experiência podem ser explícitos ou implícitos. eventos explícitos são ações humanas diretamente observáveis que ocorrem durante um ponto de uma jornada. eventos implícitos são eventos que são criados sem uma ação humana direta, mas que ainda se relacionam com um indivíduo. Exemplos de eventos implícitos podem incluir o envio agendado de boletins informativos por email ou voltagem da bateria atingindo um determinado limite.

Embora nem todos os eventos sejam facilmente categorizados em todas as fontes de dados, é extremamente importante harmonizar eventos semelhantes em tipos semelhantes, sempre que possível, para processamento.

![Jornada do cliente ExperienceEvent](images/overview/experience-event-journey.png)

## schemas XDM e serviços de Experience Platform

Experience Platform é um agnóstico do schema, o que significa que qualquer schema que esteja em conformidade com o padrão XDM está disponível para uso pelos serviços da Platform. As formas pelas quais os diferentes serviços da Platform usam schemas são descritas abaixo com mais detalhes.

### Serviço de catálogo, ingestão de dados e lago de dados

O serviço de catálogo é o sistema de registro dos ativos Experience Platform e de seus schemas relacionados. Catálogo não são os arquivos ou diretórios reais que contêm dados, mas ele armazena os metadados e as descrições desses arquivos e diretórios.

Os dados do catálogo são armazenados no Data Lake, um armazenamento de dados altamente granular contendo todos os dados gerenciados pela Platform, independentemente da origem ou do formato de arquivo.

Para começar a assimilar dados no Experience Platform, um conjunto de dados é criado usando o serviço de catálogo. O conjunto de dados faz referência a um schema XDM que descreve a estrutura dos dados a serem assimilados. Se um conjunto de dados for criado sem um schema, o Experience Platform derivará um &quot;schema observado&quot; inspecionando o tipo e o conteúdo dos campos de dados assimilados. Os conjuntos de dados são rastreados no Catálogo e armazenados no Data Lake ao lado dos schemas e dos schemas observados nos quais se baseiam.

Para obter mais informações sobre Catálogo, consulte a visão geral [do Serviço de](../catalog/home.md)Catálogo. Para obter mais informações sobre a ingestão de dados de Adobe Experience Platform, consulte a visão geral [da ingestão de](../ingestion/home.md)dados.

### Serviço de Query

O Serviço de Query de Adobe Experience Platform permite que você use SQL padrão para dados de Experience Platform de query para suportar muitos casos de uso diferentes.

Após a composição de um schema e a criação de um conjunto de dados que faz referência a esse schema, os dados são assimilados e armazenados no Data Lake. Usando o Serviço de Query, você pode associar qualquer conjunto de dados no Data Lake e capturar os resultados do query como um novo conjunto de dados para uso em relatórios, aprendizado de máquina ou para ingestão no Perfil de cliente em tempo real.

Para saber mais sobre o Serviço de Query, consulte a introdução [do Serviço de](../query-service/home.md)Query.

### Perfil do cliente em tempo real

O Perfil do cliente em tempo real oferece um perfil centralizado para o gerenciamento de experiências direcionado e personalizado. Cada perfil contém dados agregados em todos os sistemas, bem como contas acionáveis com carimbos de data e hora de eventos que envolvam o indivíduo que ocorreram em qualquer um dos sistemas que você usa com o Experience Platform.

O Perfil Cliente em tempo real consome dados formatados em schema com base nas classes XDM Individual Perfil ou XDM ExperienceEvent, e responde aos query com base nesses dados. O Perfil não suporta o uso de schemas com base em outras classes.

O Perfil mantém uma instância de cada perfil do cliente, unindo dados para formar uma &quot;única fonte de verdade&quot; para o indivíduo. Esses dados unificados são representados usando o que é conhecido como &quot;visualização de união&quot;. Uma visualização união agregação os campos de todos os schemas que implementam a mesma classe em um único schema.  Ao compor um schema usando a interface do usuário ou a API, você pode ativar o schema para uso com o Perfil do cliente em tempo real e marcá-lo para inclusão na visualização da união. O schema marcado participará da definição do schema que será alimentado ao Perfil.

Como os dados do Perfil individual XDM e do ExperienceEvent XDM são assimilados e gerenciados pelo Catálogo, ele aciona o Perfil do cliente em tempo real para começar a assimilar dados que foram habilitados para seu uso. Quanto mais interações e detalhes forem ingeridos, mais robustos serão os perfis individuais.

Os dados do Perfil individual XDM ajudam a informar e capacitar ações em qualquer integração de canal ou solução da Adobe e, quando combinados a um histórico avançado de dados comportamentais e de interação, esses dados são usados para potencializar o aprendizado da máquina. A API Perfil do cliente em tempo real também pode ser usada para aprimorar a funcionalidade de soluções de terceiros, CRMs e soluções proprietárias.

Consulte a visão geral [do Perfil do cliente em tempo](../profile/home.md) real para obter mais informações.

### Área de trabalho da ciência de dados

A Adobe Experience Platform Data Science Workspace usa o aprendizado de máquina e a inteligência artificial para obter insights dos dados armazenados no Experience Platform. A Data Science Workspace permite que os cientistas de dados construam receitas com base nos dados XDM Individual Perfil e XDM ExperienceEvent sobre clientes e suas atividades, facilitando previsões como propensão de compra e ofertas recomendadas que o indivíduo provavelmente apreciará e usará.

Com a Data Science Workspace, os cientistas de dados podem criar facilmente APIs de serviços inteligentes, capacitadas pelo aprendizado de máquina. Esses serviços funcionam com outras soluções da Adobe, incluindo a Adobe Target e a Adobe Analytics Cloud, para ajudar a automatizar experiências digitais personalizadas e direcionadas.

Para obter mais informações sobre como usar dados de Experience Platform para fornecer insights, consulte a visão geral [da](../data-science-workspace/home.md)Data Science Workspace.

### Serviço de tomada de decisão

O Serviço de tomada de decisão oferece a capacidade de configurar decisões personalizadas de ofertas em aplicativos integrados à Platform. As Ofertas podem ser recomendações de produtos, componentes de conteúdo para uma experiência da Web, scripts de conversação e ações a serem realizadas.

O Serviço de tomada de decisão aproveita os dados do Perfil do cliente em tempo real e, portanto, só é compatível com conjuntos de dados baseados em schemas que implementam o Perfil individual XDM ou a classe ExperienceEvent XDM.

Consulte a visão geral [do serviço de](../decisioning-service/home.md) decisão para obter mais informações.

## Próximos passos e recursos adicionais

Agora que você entende melhor o papel dos schema, você está pronto para start compondo o seu próprio. Para continuar complementando seu aprendizado, leia a documentação sugerida e assista ao vídeo abaixo.

Para aprender os princípios de design e as práticas recomendadas para a composição de schema, comece lendo as [noções básicas da composição](schema/composition.md)do schema. Para obter instruções passo a passo sobre como criar um schema, consulte os tutoriais sobre como criar um schema [usando a API](tutorials/create-schema-api.md) ou [usando a interface](tutorials/create-schema-ui.md)do usuário.

Para reforçar a compreensão do sistema XDM no Experience Platform, assista ao seguinte vídeo:

>[!VIDEO](https://video.tv.adobe.com/v/27105?quality=12&learn=on)

