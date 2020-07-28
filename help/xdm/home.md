---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Sistema do Experience Data Model (XDM)
topic: overview
translation-type: tm+mt
source-git-commit: d04bf35e49488ab7d5e07de91eb77d0d9921b6fa
workflow-type: tm+mt
source-wordcount: '1606'
ht-degree: 0%

---


# Visão geral do sistema XDM

A normalização e a interoperabilidade são conceitos-chave por detrás da Adobe Experience Platform. [!DNL Experience Data Model] (XDM), impulsionado pelo Adobe, é um esforço para padronizar os dados de experiência do cliente e definir schemas para o gerenciamento da experiência do cliente.

A XDM é uma especificação publicamente documentada projetada para melhorar o poder das experiências digitais. Fornece estruturas e definições comuns para qualquer aplicativo a ser usado para se comunicar com [!DNL Platform] serviços. Ao aderir aos padrões XDM, todos os dados de experiência do cliente podem ser incorporados a uma representação comum que pode fornecer insights de uma forma mais rápida e integrada. Você pode obter informações valiosas das ações do cliente, definir audiências do cliente por meio de segmentos e expressar atributos do cliente para fins de personalização.

O XDM é a estrutura fundamental que permite à Adobe Experience Cloud, capacitada por [!DNL Experience Platform], entregar a mensagem certa para a pessoa certa, no canal certo, no momento exato. A metodologia na qual [!DNL Experience Platform] está construído, o Sistema **** XDM, opera [!DNL Experience Data Model] schemas para uso pelos [!DNL Platform] serviços.

Este documento fornece uma visão geral da função do Sistema XDM no [!DNL Experience Platform].

## schemas XDM

[!DNL Experience Platform] usa schemas para descrever a estrutura dos dados de forma consistente e reutilizável. Ao definir os dados de forma consistente em todos os sistemas, torna-se mais fácil manter o significado e, portanto, obter valor dos dados.

Para que os dados possam ser ingeridos, [!DNL Platform]um schema deve ser composto para descrever a estrutura dos dados e fornecer restrições ao tipo de dados que pode ser contido em cada campo. Schemas consistem em uma classe base e zero ou mais combinações.

Para obter mais informações sobre o modelo de composição do schema, incluindo princípios de design e práticas recomendadas, consulte os [fundamentos da composição](schema/composition.md)do schema.

### [!DNL Schema Registry] e [!DNL Schema Library]

O **[!DNL Schema Registry]** fornece uma interface de usuário e uma RESTful API da qual você pode visualização e gerenciar todos os recursos relacionados ao schema no Adobe Experience Platform **[!DNL Schema Library]**. O [!DNL Schema Library] contém recursos padrão do setor disponibilizados pelo Adobe, bem como recursos de [!DNL Experience Platform] parceiros e fornecedores cujos aplicativos você usa. A interface do usuário e a API do Registro do Schema também podem ser usadas para criar e gerenciar novos schemas e recursos exclusivos à sua organização.

Para obter um guia abrangente das principais operações disponíveis no [!DNL Schema Registry], consulte o guia [do desenvolvedor do Registro do](api/getting-started.md)Schema.

## Comportamentos de dados no Sistema XDM {#data-behaviors}

Os dados destinados ao uso em [!DNL Experience Platform] são agrupados em dois tipos de comportamento:

* **Registrar dados**: Fornece informações sobre os atributos de um assunto. Um sujeito pode ser uma organização ou um indivíduo.
* **Dados** das séries cronológicas: Fornece um instantâneo do sistema no momento em que uma ação foi tomada, direta ou indiretamente, por um participante do registro.

Todos os schemas XDM descrevem dados que podem ser classificados como registros ou séries de tempo. O comportamento de dados de um schema é definido pela **classe** schema, que é atribuída a um schema quando ele é criado pela primeira vez. As classes XDM descrevem o menor número de propriedades que um schema deve conter para representar um comportamento de dados específico.

Embora seja possível definir suas próprias classes dentro do [!DNL Schema Registry], recomenda-se que você use as classes preferenciais **[!DNL XDM Individual Profile]** e **[!DNL XDM ExperienceEvent]** para dados de registro e de série de tempo, respectivamente. Essas classes são descritas com mais detalhes abaixo.

### [!DNL XDM Individual Profile]

[!DNL XDM Individual Profile] é uma classe baseada em registros que forma uma representação singular dos atributos de indivíduos identificados e parcialmente identificados. Perfis altamente identificados podem ser usados para comunicações pessoais ou envolvimentos direcionados e podem conter informações pessoais detalhadas, como nome, gênero, data de nascimento, local e informações de contato, incluindo números de telefone e endereços de email.

perfis menos identificados podem consistir apenas em sinais comportamentais anônimos, como cookies de navegador. Nesse caso, os dados de perfil esparsos são usados para criar uma base de informações na qual os interesses e preferências do perfil anônimo são coletados e armazenados. Esses identificadores podem se tornar mais detalhados ao longo do tempo, à medida que o assunto se inscreve para receber notificações, subscrições, compras e assim por diante. Este aumento nos atributos do perfil pode eventualmente resultar em um assunto identificado e permitir um maior grau de envolvimento direcionado.

À medida que o perfil do consumidor continua crescendo, ele se torna um repositório robusto de informações pessoais, informações de identificação, detalhes de contato e preferências de comunicação de um indivíduo.

### [!DNL XDM ExperienceEvent]

O XDM ExperienceEvent é uma classe baseada em série de tempo usada para capturar o estado do sistema quando um evento (ou conjunto de eventos) ocorreu, incluindo o ponto no tempo e a identidade do assunto envolvido. Os Eventos de experiência são registros de fato do que ocorreu, portanto eles são imutáveis e representam o que aconteceu sem agregação ou interpretação. Eles são essenciais para análises de domínio de tempo, pois podem ser usados para analisar alterações que ocorrem em uma determinada janela de tempo e para comparar entre várias janelas de tempo para rastrear tendências.

Os Eventos de experiência podem ser explícitos ou implícitos. eventos explícitos são ações humanas diretamente observáveis que ocorrem durante um ponto de uma jornada. eventos implícitos são eventos que são criados sem uma ação humana direta, mas que ainda se relacionam com um indivíduo. Exemplos de eventos implícitos podem incluir o envio agendado de boletins informativos por email ou voltagem da bateria atingindo um determinado limite.

Embora nem todos os eventos sejam facilmente categorizados em todas as fontes de dados, é extremamente importante harmonizar eventos semelhantes em tipos semelhantes, sempre que possível, para processamento.

![Jornada do cliente ExperienceEvent](images/overview/experience-event-journey.png)

## schemas e [!DNL Experience Platform] serviços XDM

[!DNL Experience Platform] é agnóstico do schema, o que significa que qualquer schema que esteja em conformidade com o padrão XDM está disponível para uso pelos [!DNL Platform] serviços. As formas como diferentes [!DNL Platform] serviços usam schemas são descritas abaixo com mais detalhes.

### [!DNL Catalog Service], [!DNL Data Ingestion] &amp; [!DNL Data Lake]

[!DNL Catalog Service] é o sistema de registro dos [!DNL Experience Platform] ativos e dos respectivos schemas. [!DNL Catalog] não são os arquivos ou diretórios reais que contêm dados, mas sim os metadados e as descrições desses arquivos e diretórios.

[!DNL Catalog] os dados são armazenados no, [!DNL Data Lake]um armazenamento de dados altamente granular contendo todos os dados gerenciados por [!DNL Platform], independentemente da origem ou do formato de arquivo.

Para começar a assimilar dados no [!DNL Experience Platform], um conjunto de dados é criado usando [!DNL Catalog Service]. O conjunto de dados faz referência a um schema XDM que descreve a estrutura dos dados a serem assimilados. Se um conjunto de dados for criado sem um schema, [!DNL Experience Platform] será derivado de um &quot;schema observado&quot; inspecionando o tipo e o conteúdo dos campos de dados assimilados. Os conjuntos de dados são então rastreados [!DNL Catalog] e armazenados no [!DNL Data Lake] lado dos schemas e dos schemas observados nos quais eles se baseiam.

Para obter mais informações sobre [!DNL Catalog], consulte a visão geral [do Serviço de](../catalog/home.md)catálogo. Para obter mais informações sobre a ingestão de dados de Adobe Experience Platform, consulte a visão geral [da ingestão de](../ingestion/home.md)dados.

### [!DNL Query Service]

O Adobe Experience Platform [!DNL Query Service] permite usar SQL padrão para dados de query [!DNL Experience Platform] para suportar muitos casos de uso diferentes.

Após a composição de um schema e a criação de um conjunto de dados que faz referência a esse schema, os dados são assimilados e armazenados no [!DNL Data Lake]. Usando [!DNL Query Service], você pode ingressar em qualquer conjunto de dados no [!DNL Data Lake] e capturar os resultados do query como um novo conjunto de dados para uso em relatórios, aprendizado de máquina ou para ingestão no [!DNL Real-time Customer Profile].

Para saber mais sobre [!DNL Query Service], consulte a introdução [do Serviço de](../query-service/home.md)Query.

### [!DNL Real-time Customer Profile]

O Perfil do cliente em tempo real oferece um perfil centralizado para o gerenciamento de experiências direcionado e personalizado. Cada perfil contém dados agregados em todos os sistemas, bem como contas acionáveis com carimbos de data e hora de eventos que envolvam o indivíduo que ocorreram em qualquer um dos sistemas usados com [!DNL Experience Platform].

[!DNL Real-time Customer Profile] consome dados formatados em schemas com base nas classes [!DNL XDM Individual Profile] ou [!DNL XDM ExperienceEvent] , e responde a query com base nesses dados. [!DNL Profile] não suporta o uso de schemas com base em outras classes.

[!DNL Profile] mantém uma instância de cada perfil do cliente, unindo dados para formar uma &quot;única fonte de verdade&quot; para o indivíduo. Esses dados unificados são representados usando o que é conhecido como &quot;visualização de união&quot;. Uma visualização união agregação os campos de todos os schemas que implementam a mesma classe em um único schema.  Ao compor um schema usando a interface do usuário ou a API, você pode ativar o schema para uso com [!DNL Real-time Customer Profile] e marcá-lo para inclusão na visualização da união. O schema marcado participará da definição do schema que será alimentado [!DNL Profile].

À medida que [!DNL XDM Individual Profile] e [!DNL XDM ExperienceEvent] os dados são assimilados e gerenciados por [!DNL Catalog], eles acionam [!DNL Real-time Customer Profile] a assimilação de dados que foram ativados para seu uso. Quanto mais interações e detalhes forem ingeridos, mais robustos serão os perfis individuais.

[!DNL XDM Individual Profile] os dados ajudam a informar e capacitar ações em qualquer integração de canal ou solução de Adobe e, quando combinados a um histórico avançado de dados comportamentais e de interação, esses dados são usados para potencializar o aprendizado de máquinas. A [!DNL Real-time Customer Profile] API também pode ser usada para aprimorar a funcionalidade de soluções de terceiros, CRMs e soluções proprietárias.

Consulte a visão geral [do Perfil do cliente em tempo](../profile/home.md) real para obter mais informações.

### [!DNL Data Science Workspace]

O Adobe Experience Platform [!DNL Data Science Workspace] usa o aprendizado de máquina e a inteligência artificial para obter insights dos dados armazenados no [!DNL Experience Platform]. [!DNL Data Science Workspace] permite que os cientistas de dados construam receitas com base no XDM Individual [!DNL Profile] e [!DNL XDM ExperienceEvent] dados sobre clientes e suas atividades, facilitando previsões como a propensão de compra e ofertas recomendadas que o indivíduo provavelmente apreciará e usará.

Com [!DNL Data Science Workspace]isso, os cientistas de dados podem criar facilmente APIs de serviços inteligentes, capacitadas pelo aprendizado de máquinas. Esses serviços funcionam com outras soluções de Adobe, inclusive o Adobe Target e o Adobe Analytics Cloud, para ajudar você a automatizar experiências digitais personalizadas e direcionadas.

Para obter mais informações sobre como usar [!DNL Experience Platform] dados para fornecer insights, consulte a visão geral [da](../data-science-workspace/home.md)Data Science Workspace.

### [!DNL Decisioning Service]

[!DNL Decisioning Service] fornece a capacidade de configurar decisões personalizadas de oferta em aplicativos [!DNL Platform]integrados. As Ofertas podem ser recomendações de produtos, componentes de conteúdo para uma experiência da Web, scripts de conversação e ações a serem realizadas.

[!DNL Decisioning Service] aproveita [!DNL Real-time Customer Profile] os dados e, portanto, só é compatível com conjuntos de dados baseados em schemas que implementam a [!DNL XDM Individual Profile] classe ou [!DNL XDM ExperienceEvent] .

Consulte a visão geral [do serviço de](../decisioning-service/home.md) decisão para obter mais informações.

## Próximos passos e recursos adicionais

Agora que você entende melhor o papel dos schemas ao longo do tempo [!DNL Experience Platform], você está pronto para start compondo o seu próprio. Para continuar complementando seu aprendizado, leia a documentação sugerida e assista ao vídeo abaixo.

Para aprender os princípios de design e as práticas recomendadas para a composição de schemas a serem usados, comece por ler os [!DNL Experience Platform]fundamentos da composição [](schema/composition.md)do schema. Para obter instruções passo a passo sobre como criar um schema, consulte os tutoriais sobre como criar um schema [usando a API](tutorials/create-schema-api.md) ou [usando a interface](tutorials/create-schema-ui.md)do usuário.

Para reforçar sua compreensão do [!DNL XDM System] em [!DNL Experience Platform], assista ao seguinte vídeo:

>[!VIDEO](https://video.tv.adobe.com/v/27105?quality=12&learn=on)

