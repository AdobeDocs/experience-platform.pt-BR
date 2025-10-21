---
keywords: Experience Platform;página inicial;tópicos populares
solution: Experience Platform
title: Glossário do Adobe Experience Platform
description: Um glossário de termos importantes na Experience Platform.
exl-id: 00eae5f5-7dfa-45ac-aff9-9e1769a3a53a
source-git-commit: b960e67789acaeb27a0a39db933a2bbb7d84f4d5
workflow-type: tm+mt
source-wordcount: '8170'
ht-degree: 0%

---

# Glossário do Adobe Experience Platform {#adobe-experience-platform-glossary}

## A

**Controle de acesso**: o controle de acesso baseado em função permite que os administradores atribuam acesso e permissões aos usuários do Experience Platform. As permissões incluem a capacidade de visualizar e/ou usar recursos do Experience Platform, como criar sandboxes, definir esquemas e gerenciar conjuntos de dados.

**ID da chave de acesso**: uma ID da chave de acesso é um identificador exclusivo associado a uma chave de acesso secreta do [!DNL Amazon] S3. A ID da chave de acesso e a chave de acesso secreta são usadas juntas para assinar as solicitações do [!DNL Amazon Web Services] (AWS).

**Ação**: no contexto de marcas, uma ação é um tipo específico de componente de regra que define o que deve acontecer depois que um evento ocorrer e as condições forem avaliadas e passadas.

**Ativar**: Ativar é a ação executada por um usuário para mapear um segmento ou perfis para um destino como [!DNL Oracle Eloqua], [!DNL Google] ou [!DNL Salesforce Marketing Cloud].

**Atividade**: em [!DNL Offer Decisioning], uma atividade contém a lógica que informa a seleção de uma oferta.

**Administrador**: um ou mais indivíduos em sua organização que podem configurar e personalizar permissões para o Experience Platform no Adobe Admin Console.

**Adobe Admin Console**: a Adobe Admin Console fornece um local central para gerenciar os direitos e o acesso aos produtos da Adobe para sua organização. Por meio do console, os administradores podem conceder a grupos de usuários permissões de acesso para vários recursos do Experience Platform, como &quot;Gerenciar conjuntos de dados&quot;, &quot;Exibir conjuntos de dados&quot; ou &quot;Gerenciar perfis&quot;.

**Adobe Experience Platform**: a Adobe Experience Platform padroniza dados e conteúdo em toda a empresa, acionando perfis de consumidor em tempo real, permitindo a ciência de dados e acelerando a velocidade do conteúdo para impulsionar a personalização da experiência na jornada do cliente.

**Serviço de consulta do Adobe Experience Platform**: permite que os analistas de dados consultem eventos e perfis para uso em análise e aprendizado de máquina. Com o Serviço de consulta, os cientistas e analistas de dados podem obter todos os seus conjuntos de dados armazenados no Experience Platform (incluindo dados comportamentais, ponto de venda (POS), gerenciamento de relacionamento com o cliente (CRM) e muito mais) e consultar esses conjuntos de dados para responder perguntas específicas sobre os dados.

**Serviço de segmentação do Adobe Experience Platform**: permite criar segmentos e gerar públicos a partir dos dados do Perfil do cliente em tempo real. Esses públicos-alvo podem ser exportados para seus próprios conjuntos de dados no Data Lake.

**Serviços inteligentes da Adobe**: serviços inteligentes como IA de atribuição e IA do cliente são modelos de aprendizado de máquina e inteligência artificial criados com propósitos específicos e que exigem a execução e operação da Experience Platform.

**Adobe I/O**: o Adobe I/O faz parte do Experience Platform e fornece acesso a tudo o que os desenvolvedores precisam para integrar, estender e personalizar o Experience Platform, incluindo APIs, eventos, console do desenvolvedor e ferramentas úteis.

**Adobe Sensei**: o Adobe Sensei é a estrutura de inteligência que habilita o Experience Platform. Ele também fornece um conjunto de serviços de IA que capacita as marcas a melhorar sua capacidade de fornecer experiências do cliente personalizadas e em tempo real.

**Compartimento do Amazon S3**: [!DNL Amazon S3] os compartimentos são os contêineres fundamentais para dados armazenados no ecossistema [!DNL Amazon]. Os buckets contêm objetos. Cada objeto é armazenado e recuperado usando uma chave exclusiva atribuída pelo desenvolvedor.

**Conector S3 do Amazon**: o conector S3 do [!DNL Amazon] permite que os clientes da Experience Platform se conectem e acessem com segurança seus dados S3 do [!DNL Amazon].

**APA**: o [[!DNL Australia Privacy Act (Privacy Act)]](https://www.oaic.gov.au/privacy/the-privacy-act) promove e protege a privacidade dos indivíduos e regula como as agências e organizações governamentais australianas lidam com informações pessoais. O [!DNL Privacy Act] inclui princípios que se aplicam a organizações do setor privado. Por exemplo, as pessoas têm o direito de entender por que as informações pessoais estão sendo coletadas e como serão usadas, a capacidade de acessar, apagar seus dados e corrigir informações pessoais.

**Anexar estratégia de salvamento**: a estratégia de salvamento &quot;anexar&quot; é uma opção usada ao especificar dados de terceiros para assimilar por meio de uma conexão e anexar novos dados ou linhas ao final do conjunto de dados. As linhas assimiladas anteriormente permanecem inalteradas e somente as linhas criadas desde a última execução agendada são assimiladas no Experience Platform. As linhas alteradas no sistema de origem permanecem inalteradas no Experience Platform.

**Matriz**: as matrizes são usadas para elementos ordenados com o mesmo tipo de dados.

**Inteligência artificial**: a inteligência artificial é uma teoria e um desenvolvimento de sistemas de computador capazes de executar tarefas que normalmente exigem inteligência humana, como percepção visual, reconhecimento de fala, tomada de decisões e tradução entre idiomas.

**Atributos**: atributos são características especificadas que representam um perfil.

**Mesclagem de atributos**: ao definir uma política de mesclagem usando a API de perfil de cliente em tempo real, o objeto `attributeMerge` indica a maneira pela qual a política de mesclagem priorizará os atributos de perfil em caso de conflitos de dados. É equivalente a selecionar um [!UICONTROL Merge method] ao definir uma política de mesclagem na interface do usuário do Experience Platform.

**IA de atribuição**: [!DNL Attribution AI] é um Serviço inteligente fornecido pela Adobe Sensei que fornece recursos de atribuição de vários canais algorítmicos por todo o ciclo de vida do cliente.

**Público-alvo**: um público-alvo é o conjunto de perfis resultante que atende aos critérios de uma definição de segmento.

**Tamanho do público-alvo**: um tamanho de público-alvo é o número total de perfis que atendem aos critérios de uma definição de segmento e se qualificam para associação de público-alvo.

**Instantâneo de público-alvo**: um instantâneo de público-alvo captura todos os perfis que se qualificam para os critérios de segmento no momento da segmentação.

## B

**Preenchimento retroativo**: para fontes agendadas, a opção de preenchimento retroativo habilita a assimilação de dados históricos.

**Período de preenchimento retroativo**: o período de preenchimento retroativo é uma opção para definir a duração da assimilação de dados históricos de terceiros por meio de uma conexão de origem. Selecionar um período de preenchimento retroativo de &quot;para sempre&quot; assimilará todo o histórico dos dados de origem para o Experience Platform.

**Lote**: um lote é um conjunto de dados coletados durante um período e processados juntos como uma única unidade. Os conjuntos de dados são compostos de vários lotes.

**ID do Lote**: uma ID do lote é um identificador gerado pela Adobe para um lote de dados.

**Assimilação em lote**: a assimilação em lote permite assimilar dados na Experience Platform como arquivos em lote. Lotes são unidades de dados que consistem em um ou mais arquivos que serão assimilados como uma única unidade.

**Segmentação em lote**: a segmentação em lote é uma alternativa a um processo de seleção de dados em andamento e move todos os dados de perfil de uma só vez pelas definições de segmento para produzir públicos correspondentes. Depois de criado, esse segmento é salvo e armazenado para que possa ser exportado para uso.

**Compilação**: no contexto de marcas, uma compilação é um arquivo ou conjunto de arquivos que contém todas as configurações e códigos necessários para executar a lógica comercial contida em uma biblioteca, permitindo que você implante essa biblioteca no seu site ou aplicativo móvel.

**Ferramentas de Business Intelligence**: as ferramentas de Business Intelligence (BI) estão integradas principalmente com o [!DNL Experience Platform Query Service]. As ferramentas de BI são tipos de software de aplicativos que coletam e processam grandes quantidades de dados não estruturados de sistemas internos e externos.

## C

**Limite**: em [!DNL Offer Decisioning], o limite (também conhecido como limite de frequência) é usado nas regras de decisão para definir quantas vezes uma oferta é apresentada. Há dois tipos de limites: quantas vezes uma oferta pode ser proposta através do público-alvo combinado (chamado de &quot;Limite global&quot;) e quantas vezes uma oferta pode ser proposta ao mesmo usuário final (chamado de &quot;Limite de perfil&quot;).

**Catálogo**: no contexto de fontes e destinos, um catálogo é uma galeria com conexões disponíveis para aplicativos da Adobe e tecnologias de terceiros. Não confundir com [!DNL Catalog Service].

**[!DNL Catalog Service]**: [!DNL Catalog Service] (às vezes chamado de [!DNL Catalog]) é o sistema de registro para localização e linhagem de dados no Adobe Experience Platform. Embora todos os dados assimilados na Experience Platform sejam armazenados no data lake como arquivos e diretórios, o [!DNL Catalog] retém os metadados e a descrição desses arquivos e diretórios para fins de pesquisa, monitoramento e governança de dados.

**CCPA**: o [[!DNL California Consumer Privacy Act (CCPA)]](https://oag.ca.gov/privacy/ccpa) aprimora os direitos de privacidade e a proteção do consumidor para os moradores da Califórnia, Estados Unidos. A CCPA oferece novos direitos de privacidade de dados aos moradores da Califórnia, incluindo o direito de acessar e excluir seus dados pessoais, de saber se seus dados pessoais são vendidos ou divulgados (e para quem) e o direito de recusar a venda de seus dados a terceiros.

**Classe**: no Experience Data Model (XDM), uma classe define o menor conjunto de campos usados para criar um esquema e define o comportamento base do objeto comercial que o esquema representa.

**Cliente**: um cliente é uma ferramenta ou aplicativo externo que se conecta a [!DNL Query Service] por meio do protocolo [!DNL PostgreSQL] ou da API HTTP.

**Coleção**: em [!DNL Offer Decisioning], as coleções são subconjuntos de ofertas com base em condições predefinidas por um profissional de marketing, como a categoria da oferta.

**Combinar com ação de marketing de PII**: uma ação de marketing que combina informações de identificação pessoal (PII) com dados anônimos. Os contratos para dados obtidos de redes de publicidade, servidores de publicidade e provedores de dados de terceiros geralmente incluem proibições contratuais específicas sobre o uso desses dados com dados diretamente identificáveis.

**Interface de linha de comando**: uma interface de linha de comando é uma ferramenta baseada em texto que pode ser usada para conexão com [!DNL Query Service] para execução de consulta bruta.

**Composição**: uma composição é um agrupamento de componentes que se formam juntos para compor o esquema.

**Condição**: no contexto de marcas, uma condição é um componente de regra que avalia uma instrução lógica que deve retornar `true` ou `false`. Todas as condições devem ser avaliadas como `true` e todas as condições de exceção devem ser avaliadas como `false` antes que qualquer ação na regra seja executada.

**Console**: em [!DNL Query Service], o console fornece informações sobre o status e a operação de uma consulta. O console exibe o status da conexão com [!DNL Query Service], operações de consulta sendo executadas e mensagens de erro resultantes dessas consultas.

**Rótulos de contrato (&quot;C&quot;)**: os rótulos de uso de dados de contrato (&quot;C&quot;) são usados para categorizar dados que contêm obrigações contratuais ou estão relacionados às políticas de governança de dados da sua organização.

**CPRA**: o [[!DNL California Consumer Privacy Rights Act (CPRA)]](https://cppa.ca.gov/regulations/consumer_privacy_act.html) expande e corrige partes do [!DNL California Consumer Privacy Act (CCPA)]. O [!DNL CPRA] estabelece uma nova linha de base para a privacidade de dados do consumidor na Califórnia, aumentando os direitos do consumidor e expandindo o tipo de dados abrangidos por uma definição mais ampla de informações pessoais confidenciais. Além disso, o [!DNL CPRA] estabeleceu a California Privacy Protection Agency, uma nova agência dedicada à implementação e aplicação de regras de privacidade de dados.

**Rótulo de contrato C1**: um rótulo de uso de dados de contrato `C1` especifica que os dados só podem ser exportados do Adobe Experience Cloud de forma agregada sem incluir identificadores individuais ou de dispositivo. Por exemplo, dados originados de redes sociais.

Rótulo de contrato **C2**: um rótulo de uso de dados de contrato `C2` especifica dados que não podem ser exportados para terceiros. Alguns provedores de dados têm termos em seus contratos que proíbem a exportação de dados de onde foram originalmente coletados. Por exemplo, os contratos de redes sociais geralmente restringem a transferência de dados recebidos deles. C2 é mais restritivo que C1, que requer apenas agregação e dados anônimos.

**Rótulo do contrato C3**: um rótulo de uso de dados do contrato `C3` especifica dados que não podem ser combinados ou usados com informações diretamente identificáveis. Alguns provedores de dados têm termos em seus contratos que proíbem a combinação ou o uso desses dados com informações diretamente identificáveis. Por exemplo, os contratos para dados obtidos a partir de redes de publicidade, servidores de publicidade e fornecedores de dados de terceiros incluem frequentemente proibições contratuais específicas sobre a utilização de dados diretamente identificáveis.

**Rótulo do contrato C4**: um rótulo de uso de dados do contrato `C4` especifica que os dados não podem ser usados para direcionar anúncios ou conteúdo, no site ou entre sites. C4 é o rótulo mais restritivo, pois abrange os rótulos C5, C6 e C7.

**Rótulo de contrato C5**: um rótulo de uso de dados de contrato `C5` especifica que os dados não podem ser usados para direcionamento entre sites de conteúdo ou anúncios baseados em interesses. O direcionamento baseado em interesses, ou personalização, ocorre se as três condições a seguir forem atendidas: os dados coletados no site são usados para tirar conclusões sobre o interesse de um usuário; são usados em outro contexto, como em outro site ou aplicativo; e são usados para selecionar qual conteúdo ou anúncios são veiculados com base nessas conclusões.

**Rótulo de contrato C6**: um rótulo de uso de dados de contrato `C6` especifica que os dados não podem ser usados para direcionamento de anúncios no site. O direcionamento de anúncios no site inclui a seleção e a entrega de anúncios nos sites ou aplicativos da organização, ou para medir a entrega e a eficácia desses anúncios. Isso inclui o uso de dados coletados anteriormente no site sobre o interesse dos usuários em selecionar anúncios, dados de processo sobre quais anúncios foram mostrados, quando e onde foram mostrados e se os usuários tomaram alguma ação relacionada ao anúncio, como selecionar um anúncio ou fazer uma compra.

**Rótulo de contrato C7**: um rótulo de uso de dados de contrato `C7` especifica que os dados não podem ser usados para direcionamento de conteúdo no site. O direcionamento de conteúdo no site inclui a seleção e a entrega de conteúdo nos sites ou aplicativos da organização, ou para medir a entrega e a eficácia desse conteúdo. Isso inclui informações coletadas anteriormente sobre o interesse dos usuários em selecionar o conteúdo, o processamento de dados sobre qual conteúdo foi mostrado, com que frequência ou por quanto tempo ele foi exibido, quando e onde foi exibido e se os usuários executaram ações relacionadas ao conteúdo, incluindo, por exemplo, a seleção de conteúdo.

**Rótulo do contrato C8**: um rótulo de uso de dados do contrato `C8` especifica que os dados não podem ser usados para medição dos sites ou aplicativos de sua organização. Isso não inclui direcionamento com base em interesses, que é a coleta de informações sobre o uso desse serviço para personalizar subsequentemente o conteúdo e/ou a publicidade em outros contextos.

**Rótulo de contrato C9**: um rótulo de uso de dados de contrato `C9` especifica que os dados não podem ser usados em fluxos de trabalho de ciência de dados. Alguns contratos incluem proibições explícitas sobre dados usados para ciência de dados. Às vezes, esses termos são redigidos em termos que proíbem o uso de dados para inteligência artificial (IA), aprendizado de máquina (ML) ou modelagem.

**Rótulo de contrato C10**: um rótulo de uso de dados de contrato `C10` especifica que os dados não podem ser usados para ativação de identidade compilada. Algumas políticas de uso de dados restringem o uso de dados de identidade compilados para personalização. O rótulo `C10` é aplicado automaticamente a segmentos se suas políticas de mesclagem usarem a opção &quot;gráfico privado&quot;.

**Coluna Data de Criação**: a seleção de uma coluna Data de Criação é uma opção ao especificar dados de terceiros por meio de uma conexão de origem. Quando a estratégia anexar salvar for selecionada e o esquema de conjunto de dados contiver vários campos de data, você deverá escolher no esquema disponível para especificar uma coluna de chave Data de criação. A opção Data de criação não está disponível quando a estratégia de salvamento de substituição é selecionada.

**Criar Tabela como Seleção**: Criar Tabela como Seleção (CTAS) é um comando SQL que, quando executado como parte de uma consulta SQL completa e válida, instruirá [!DNL Query Service] a manter os resultados da consulta em um conjunto de dados. Você pode criar um novo conjunto de resultados, substituir resultados anteriores ou anexar a resultados anteriores.

**Dados entre sites**: dados entre sites são a combinação de dados de vários sites, incluindo uma combinação de dados internos e externos ou uma combinação de dados de várias fontes externas.

**Ação de marketing para direcionamento entre sites**: uma ação de marketing que usa dados para direcionamento de anúncios entre sites. A combinação de dados de vários sites, incluindo uma combinação de dados internos e externos ou uma combinação de dados de várias fontes externas, é chamada de dados entre sites. Normalmente, os dados entre sites são coletados e processados para deduzir os interesses dos clientes.

**Namespace de identidade personalizado**: os namespaces de identidade personalizados podem ser criados por sua organização para representar identidades para uma organização ou caso comercial específico.

**Rótulos personalizados**: rótulos de uso de dados personalizados permitem criar e aplicar rótulos específicos a campos de dados que atendem a necessidades comerciais específicas.

**IA do cliente**: a IA do cliente é um Serviço inteligente fornecido pela Adobe Sensei que enriquece os perfis do cliente com propensões baseadas em IA e capacita os esforços de segmentação e direcionamento do cliente.

## D

**Diariamente**: no contexto de exportações de arquivos agendadas, agenda as exportações de arquivos completas ou incrementais uma vez por dia, todos os dias, da data de início até a data de término na hora especificada pelo usuário.

**Dicionário de dados**: no contexto de marcas, um dicionário de dados (também conhecido como mapa de dados) é um conjunto de elementos de dados definidos em uma propriedade.

**Elemento de dados**: no contexto de marcas, um elemento de dados é um ponteiro usado em regras e extensões para apontar para dados específicos existentes no dispositivo cliente.

**Assimilação de dados**: a assimilação de dados é o processo de adicionar dados de uma origem à Experience Platform. Os dados podem ser assimilados na Experience Platform de várias maneiras, incluindo transmissão, lotes ou adicionados por meio de conectores de origem.

**Camada de dados**: no contexto de marcas, uma camada de dados é uma estrutura de dados que existe no dispositivo cliente e que contém metadados sobre o contexto em que uma página ou tela é exibida.

**Governança de dados**: a governança de dados abrange as estratégias e tecnologias usadas para garantir que os dados estejam em conformidade com as regulamentações e as políticas organizacionais com relação ao uso de dados.

**Parceiros de integração de dados**: os parceiros de integração de dados simplificam e automatizam o carregamento e a transformação de grandes volumes de dados de mais de 200 fontes para a Experience Platform sem gravar o código.

**Rótulos do conjunto de dados**: os rótulos de uso de dados podem ser adicionados aos conjuntos de dados. Todos os campos nesse conjunto de dados herdarão os rótulos dele.

**Data Science Workspace**: [!DNL Data Science Workspace] no Experience Platform permite que os clientes criem modelos de aprendizado de máquina utilizando dados em aplicativos da Experience Platform e Adobe para criar segmentos inteligentes, gerar insights e fornecer previsões, permitindo que você aprimore significativamente as experiências digitais do usuário final.

**Fonte de dados**: uma fonte de dados é uma origem de dados designada pelo usuário. Exemplos de uma fonte de dados são um aplicativo móvel, eventos de perfil e/ou experiência, eventos de perfil de site ou um CRM.

**Administrador de dados**: um administrador de dados é a pessoa responsável pelo gerenciamento, supervisão e aplicação dos ativos de dados de uma organização. Um administrador de dados também garante que as políticas de governança de dados sejam protegidas e mantidas para estar em conformidade com as regulamentações governamentais e as políticas organizacionais.

**Fluxo de dados**: um fluxo de dados é um conjunto de mensagens que compartilham o mesmo esquema e são enviadas pela mesma fonte.

**Tipo de dados**: um tipo de dados é um recurso XDM reutilizável que define um campo de tipo de objeto que contém várias propriedades em uma representação hierárquica.

**Rótulos de uso de dados**: os rótulos de uso de dados permitem que você categorize dados que refletem considerações relacionadas à privacidade e às condições contratuais para estar em conformidade com os regulamentos e as políticas corporativas. Os rótulos de uso de dados adicionados a um conjunto de dados são herdados ou aplicados a todos os campos nesse conjunto de dados. Os rótulos de uso de dados também podem ser aplicados diretamente aos campos.

**Fluxo de dados**: um fluxo de dados é um pipeline virtual de dados que flui para o Experience Platform a partir de uma origem e para destinos.

**Execução de fluxo de dados**: uma execução de fluxo de dados é um fluxo de dados que chega ao Experience Platform com base em um agendamento especificado pelo usuário.

**Conjunto de dados**: um conjunto de dados é uma construção de armazenamento e gerenciamento para uma coleção de dados, normalmente uma tabela, que contém um esquema (colunas) e campos (linhas).

**ID do conjunto de dados**: um identificador gerado pela Adobe para um conjunto de dados assimilado.

**Saída do conjunto de dados**: a saída do conjunto de dados fornece um mecanismo para determinar o que a opção &quot;Criar Tabela como Seleção&quot; será usada para uma execução [!DNL Query Service] específica.

**Chave de desduplicação**: uma chave primária definida pelo usuário que determina a identidade pela qual os usuários desejam que seus perfis sejam desduplicados.&#x200B;

**Coluna delta**: uma coluna delta permite selecionar um campo de dados de origem para representar um carimbo de data/hora para assimilação incremental.

**Estratégia de salvamento delta**: a estratégia de salvamento delta é uma opção para assimilar dados de terceiros por meio de uma conexão de origem. A opção permite que o usuário especifique se linhas novas ou alteradas de dados de origem são assimiladas na Experience Platform. Novas linhas são adicionadas ao final do conjunto de dados e as linhas alteradas são atualizadas no conjunto de dados no Experience Platform.

**Descritor**: no Experience Data Model (XDM), um descritor é um conjunto adicional de metadados relacionados ao esquema que descreve um comportamento específico para um campo. Os descritores podem ser usados pelo Experience Platform para entender o comportamento do esquema desejado, como a relação entre dois esquemas.

**Destino**: um destino é um termo geral para qualquer ponto de extremidade, como um aplicativo do Adobe, uma plataforma de publicidade, um serviço de armazenamento na nuvem ou um serviço de marketing, em que um público-alvo é ativado e entregue.

**Categoria de destino**: uma categoria de destino é um agrupamento de destinos que têm características semelhantes.

**Catálogo de destino**: um catálogo de destino é uma lista de destinos disponíveis no Experience Platform.

**Regras de chamada direta**: no contexto de marcas, uma regra de chamada direta é uma regra que é executada quando é chamada diretamente da página, ignorando a detecção de eventos e os sistemas de pesquisa.

**Nome de exibição**: no Experience Data Model (XDM), um nome de exibição é um nome amigável para um campo que é mostrado na interface do usuário.

## E

**Oferta elegível**: uma oferta elegível pode ser oferecida de forma consistente a um perfil, pois atende às restrições definidas upstream.

**Regras de qualificação**: em [!DNL Offer Decisioning], as regras de qualificação são aplicadas a um perfil relacionado a restrições de calendário, agendamento e limite.

**Ação de marketing para direcionamento por email**: uma ação de marketing que usa dados em campanhas de direcionamento por email.

**Código de inserção**: no contexto de marcas, o código de inserção é uma marca de script colocada na HTML em um site ou ambiente. O código incorporado instrui o navegador onde a build deve ser recuperada.

**Enumeração**: uma enumeração (enum) é um campo XDM restrito a um conjunto de valores predefinidos.

**Ambiente**: no contexto de marcas, um ambiente é um conjunto de instruções de implantação que especifica a entrega do host e o formato de arquivo de uma compilação. Uma biblioteca deve estar emparelhada a um ambiente para que possa ser criada.

**Diagnóstico de erro**: o diagnóstico de erro habilita a geração de mensagens de erro detalhadas para lotes assimilados. O limite de erro permite configurar a porcentagem de erros aceitáveis antes que um lote falhe.

**Evento**: no contexto de marcas, um evento é um tipo específico de componente de regra, que é um disparador que ocorre em um dispositivo cliente para iniciar a execução de uma regra.

**Entidades de evento**: no contexto de modelagem de dados, as entidades de evento representam conceitos relacionados às ações que um cliente pode realizar, aos eventos do sistema ou a qualquer outro conceito em que você queira rastrear as alterações ao longo do tempo. As entidades que se enquadram nessa categoria devem ser representadas por esquemas baseados na classe [!DNL XDM ExperienceEvent].

**Eventos**: eventos são os dados de comportamento associados a um perfil.

O **Experience Data Model (XDM)** [!DNL Experience Data Model] (XDM) é uma estrutura de código aberto que usa esquemas padrão para unificar dados a serem usados com aplicativos do Experience Platform e do Adobe Experience Cloud. O XDM padroniza como os dados são estruturados e acelera e simplifica o processo de obtenção de insights de grandes quantidades de dados.

**Experimento**: um experimento é o processo de criação de um modelo treinado ao treinar a instância com uma parte de amostra dos dados de produção em tempo real. Isso é diferente de um modelo treinado que é testado em relação a um conjunto de dados de teste de validação. Isso também é diferente do conceito de um experimento em algumas estruturas de aprendizado de máquina onde ele realmente significa um projeto de modelagem de amostra.

**Evento de experiência**: um evento de experiência representa um instantâneo do sistema quando ocorre uma interação ou um evento relacionado a uma experiência do cliente. Eventos de experiência são registros de fatos imutáveis do que ocorreu e representam o que aconteceu sem agregação ou interpretação. No Experience Data Model (XDM), esse conceito é capturado pela classe [!DNL XDM ExperienceEvent].

**Exportar arquivo completo**: um arquivo de exportação contendo um instantâneo completo de todas as qualificações de perfil para o segmento selecionado.

**Exportar arquivos incrementais**: uma série de arquivos exportados em que o primeiro arquivo é um instantâneo completo de todas as qualificações de perfil do segmento selecionado, e os arquivos subsequentes são qualificações de perfil incrementais desde a exportação anterior.

**Extensão**: no contexto de marcas, uma extensão é um pacote de funcionalidades adicionado a uma propriedade de marca. Uma extensão geralmente foca em uma solução de marketing ou análise específica e fornece as ferramentas necessárias para implantar essa tecnologia em um ambiente cliente.

**Pacote de extensão**: no contexto de marcas, um pacote de extensão é um arquivo ZIP criado e carregado por um desenvolvedor de extensão que fornece tudo o que é necessário para que os usuários de marcas instalem a extensão dentro de suas propriedades. Um pacote de extensão contém um manifesto que especifica informações sobre a extensão, a HTML/JavaScript necessária para os usuários finais configurarem o comportamento da extensão de tag e o JavaScript executável entregue ao ambiente do cliente (se necessário).

## F

**Ofertas substitutas**: uma oferta substituta é a oferta padrão exibida quando um usuário final não está qualificado para nenhuma das ofertas da coleção usada.

**Mapeamento de recursos**: o mapeamento de recursos refere-se ao processo de mapeamento de recursos de dados para recursos de entrada e destino exigidos por um modelo de aprendizado de máquina.

**Campo**: um campo é o elemento de nível mais baixo de um conjunto de dados, conforme definido pelo esquema XDM do conjunto de dados. Cada campo tem um nome para fins de referência e um tipo para indicar o tipo de dados que ele contém. Os tipos de campo podem incluir (mas não estão limitados a) número inteiro, número, string, booleano e objeto.

**Grupo de campos**: consulte &quot;Grupo de campos de esquema&quot;.

**Rótulos de campos**: os rótulos de campos são rótulos de governança de dados herdados de um conjunto de dados ou aplicados diretamente a um campo.

**Nome do campo**: um nome de campo é usado para fazer referência ao valor de um campo em consultas e serviços downstream.

**Frequência**: Em [!DNL Query Service], a frequência determina a frequência com que uma consulta agendada recorrente será executada.

## G

**Geofence**: uma geofence é um limite geográfico virtual, definido pela tecnologia GPS ou RFID, que permite que o software acione uma resposta quando um dispositivo móvel entra ou sai de uma determinada área.

**GDPR (Regulamento Geral sobre a Proteção de Dados)**: o Regulamento Geral sobre a Proteção de Dados (GDPR) é uma estrutura legal que define diretrizes para a coleta e o processamento de informações pessoais de indivíduos na União Europeia (UE). O RGPD estabelece os princípios para a gestão de dados e os direitos do indivíduo e abrange todas as empresas que lidam com os dados de cidadãos da UE.

**Medidas de proteção**: as medidas de proteção são limites que fornecem orientação para o uso de dados e do sistema, otimização de desempenho e prevenção de erros ou resultados inesperados no Adobe Experience Platform. As garantias podem se referir ao uso ou consumo de dados e processamento em relação aos seus direitos de licenciamento.

## H

**HIPAA**: o [[!DNL Health Insurance Portability and Accountability Act (HIPAA)]](https://www.hhs.gov/hipaa/index.html) é uma lei federal dos Estados Unidos criada para melhorar a eficiência da saúde, melhorar a portabilidade do seguro de saúde e proteger a privacidade dos pacientes e dos membros do plano de saúde. De acordo com a HIPAA, os indivíduos têm o direito de acessar e alterar suas informações e obter cópias de seus registros médicos ou informações de saúde. As entidades cobertas e os parceiros comerciais das entidades cobertas devem seguir as normas da HIPAA.

**Host**: no contexto de marcas, um host especifica o local, o domínio e as credenciais de usuário necessárias para o sistema entregar uma compilação.

**Por hora**: no contexto de exportações de arquivos agendadas, agenda as exportações de arquivos incrementais a cada 3, 6, 8 ou 12 horas.

## I

**Identidade**: uma identidade é um identificador que representa exclusivamente um cliente individual, como uma ID de cookie, ID de dispositivo ou ID de email.

**Campos de identidade**: campos de identidade são campos XDM usados para unir informações sobre clientes individuais provenientes de várias fontes de dados. Uma única identidade principal deve ser definida para que o esquema seja ativado para uso no Perfil do cliente em tempo real.

**Rótulos de identidade (&quot;I&quot;)**: os rótulos de uso de dados de identidade (&quot;I&quot;) são usados para categorizar dados que podem identificar ou contatar uma pessoa específica.

**Gráfico de identidade**: um gráfico de identidade é um mapa de relacionamentos entre identidades compiladas e vinculadas que existem para um cliente individual. Cada gráfico de identidade é atualizado em tempo quase real com a atividade do cliente. A estrutura comum das relações de identidade em seus dados é representada pelo [!UICONTROL Private Graph], que serve como blueprint estrutural para cada gráfico de identidade individual.

**Namespace de identidade**: um namespace de identidade define o contexto de um identificador, como um endereço de email ou uma ID de CRM.

**Serviço de Identidade**: [!DNL Experience Platform Identity Service] habilita a criação e o gerenciamento de tipos de identidade, permitindo que você vincule as identidades do cliente em dispositivos e canais. A capacidade do serviço de vincular identidades permite que o Perfil do cliente em tempo real forneça uma representação completa de cada cliente individual.

**Compilação de identidade**: a compilação de identidade é o processo de identificar fragmentos de dados e uni-los para formar um registro de perfil completo.

**Símbolo de identidade**: um símbolo de identidade é uma abreviação de um namespace de identidade que pode ser usado como referência em APIs.

**Valor de identidade**: um valor de identidade, combinado com um namespace de identidade, é um identificador que representa uma pessoa, organização ou ativo exclusivo. Ao corresponder os dados de registro em fragmentos de perfil, o namespace e o valor de identidade devem corresponder.

Rótulo de uso de dados **I1**: o rótulo de uso de dados `I1` é usado para classificar dados que podem identificar ou contatar diretamente uma pessoa específica em vez de um dispositivo.

Rótulo de uso de dados **I2**: o rótulo de uso de dados `I2` é usado para classificar dados que podem ser usados em combinação com outros dados para identificar ou contatar indiretamente uma pessoa específica.

**Organização IMS**: uma Organização IMS (às vezes chamada de Organização IMS) é o nome usado para identificar uma empresa ou um grupo específico em uma empresa nos produtos da Adobe. Os administradores podem configurar e gerenciar o acesso e as permissões de recursos para usuários de uma organização.

**Assimilação**: consulte a assimilação de dados.

**Agendamento de assimilação**: um agendamento de assimilação fornece opções baseadas em tempo ao assimilar de uma origem para a Experience Platform.

**Recurso de entrada**: um recurso de entrada é especificado no mapeamento de recursos e é usado por um modelo de aprendizado de máquina para fazer previsões.

**[!DNL Intelligent Services]**: [!DNL Intelligent Services] como [!DNL Attribution AI] e [!DNL Customer AI] são modelos de aprendizado de máquina e inteligência artificial que exigem o Experience Platform (ou aplicativos criados com base no Experience Platform, como o Adobe Real-Time Customer Data Platform) para serem executados e operados.

**Direcionamento ou personalização baseado em interesses**: o direcionamento baseado em interesses, também conhecido como personalização, ocorrerá se as três condições a seguir forem atendidas:

1. Os dados coletados no site são usados para deduzir o interesse de um usuário.
1. Os dados são usados em outro contexto, como em outro site ou aplicativo (externo).
1. Os dados são usados para selecionar qual conteúdo ou quais anúncios são veiculados com base nessas inferências.

## J

**[!DNL JupyterLab]**: uma interface de código aberto baseada na Web para o Projeto [!DNL Jupyter] que está integrada à interface do usuário do Experience Platform.

**[!DNL Jupyter Notebook]**: Integrado ao JupyterLab, o Jupyter Notebooks permite realizar limpeza e transformação de dados, simulação numérica, modelagem estatística, visualização de dados, aprendizado de máquina e muito mais em seus dados do Experience Platform em uma variedade de linguagens como Python, Scala e PySpark.

## K

## L

**LGPD**: O [[!DNL Lei Geral de Proteção de Dados (LGPD)]](https://gdpr.eu/gdpr-vs-lgpd/) visa regular o tratamento de dados pessoais de todos os indivíduos ou pessoas singulares no Brasil. A LGPD dá aos cidadãos brasileiros o direito de acessar e apagar seus dados pessoais, de saber se seus dados pessoais são vendidos ou divulgados (e para quem), e o direito de recusar a venda de seus dados a terceiros.

**Biblioteca**: no contexto de marcas, uma biblioteca é um conjunto de lógicas de negócios que contém instruções sobre como a biblioteca de marcas deve se comportar no dispositivo cliente.

**Entidades de pesquisa**: no contexto de modelagem de dados, as entidades de pesquisa representam conceitos que podem se relacionar a uma pessoa individual, mas não podem ser usadas diretamente para identificá-la. As entidades que se enquadram nessa categoria devem ser representadas por esquemas baseados em classes personalizadas do Experience Data Model (XDM) e vinculadas a uma entidade de perfil por meio de um [relacionamento de esquema](../xdm/tutorials/relationship-ui.md).

## M

**Aprendizado de máquina (ML)**: o aprendizado de máquina é o campo de estudo que permite que os computadores aprendam sem serem explicitamente programados.

**Modelo de aprendizado de máquina**: um modelo de aprendizado de máquina é uma instância de uma fórmula de aprendizado de máquina treinada com dados históricos e configurações a serem resolvidos para um caso de uso comercial. Na Adobe Experience Platform Data Science Workspace, os modelos de aprendizado de máquina são chamados de receitas.

**Atributo obrigatório**: uma caixa de seleção habilitada pelo usuário que garante que todos os registros de perfil contenham o atributo selecionado. Por exemplo: todos os perfis exportados contêm um endereço de email.

**Mapeamento**: o mapeamento de dados é o processo de mapear campos de dados de origem para campos de destino relacionados em um destino.

**Ação de marketing**: na estrutura de governança de dados, uma ação de marketing (também conhecida como caso de uso de marketing) é uma ação que um consumidor de dados do Experience Platform toma, para a qual é necessário verificar se há violações das políticas de uso de dados.

**Método de mesclagem**: ao definir uma política de mesclagem usando a interface do usuário do Experience Platform, o método de mesclagem especifica como os fragmentos de dados devem ser priorizados quando ocorre um conflito. Ao usar a API de perfil do cliente em tempo real para definir uma política de mesclagem, o método de mesclagem é determinado usando o objeto `attributeMerge`.

**Política de mesclagem**: as políticas de mesclagem são regras que a Experience Platform usa para determinar como os fragmentos de dados do cliente de várias fontes serão combinados para criar um perfil individual. Quando ocorre um conflito de dados, a política de mesclagem determina quais dados devem ser priorizados para inclusão no perfil.

**MHMDAa**: o [[!DNL Washington My Health My Data Act]](https://app.leg.wa.gov/RCW/default.aspx?cite=19.373&full=true) aprimora os direitos de privacidade dos consumidores em relação aos seus dados de saúde. Ela exige a divulgação, o consentimento do consumidor e os direitos de exclusão dos dados de saúde, e proíbe a venda de dados de saúde sem autorização. Além disso, a lei torna ilegal o uso de geofencing em instalações de saúde.

**Mixin**: consulte &quot;Grupo de campos de esquema&quot;.

**Módulo**: no contexto de marcas, um módulo é um trecho de JavaScript executável fornecido por uma extensão, que executa ações em um ambiente cliente sem precisar criar uma regra.

**MODPA**: o [!DNL Maryland Online Data Privacy Act] (MODPA) de 2024 concede aos residentes de Maryland direitos incluindo acesso, correção, exclusão e portabilidade de dados. Os residentes podem recusar a publicidade direcionada, a venda de dados pessoais e a definição de perfis. Os controladores devem fornecer os avisos de privacidade e realizar avaliações de proteção de dados para processamento de alto risco. O MODPA se destaca pela proibição de geofencing em torno de instalações de saúde mental ou reprodutiva. A lei se aplica a entidades que processam dados de mais de 35 mil consumidores, ou àquelas que processam dados de mais de 10 mil consumidores e obtêm mais de 20% de sua receita com a venda desses dados. É aplicado pelo Procurador Geral de Maryland.

## N

**[!DNL New Zealand Privacy Act]**: O [[!DNL New Zealand Privacy Act]](https://www.privacy.org.nz/privacy-act-2020/privacy-principles/) controla como as agências podem coletar, usar, divulgar, armazenar e dar acesso às informações pessoais de cidadãos e organizações da Nova Zelândia. Em 2020, a versão mais recente da lei introduziu atualizações significativas nessas leis de privacidade, incluindo novas infrações, aumento das multas, notificações obrigatórias por violações de dados e aumento dos poderes do Comissário para a Privacidade.

**Sandbox de não produção**: sandboxes de não produção são sandboxes que normalmente são usadas para experimentos de desenvolvimento, testes ou avaliações. Diferentemente das sandboxes de produção, as sandboxes de não produção podem ser redefinidas e excluídas.

**[!DNL Notebooks]**: [!DNL Notebooks] foram criados usando [!DNL Jupyter Notebook] e podem ser executados para executar a análise de dados.

## O

**Oferta**: uma oferta é uma mensagem de marketing que contém uma proposta de negócios ou de vendas para um (potencial) cliente. As ofertas geralmente têm regras específicas que determinam quem está qualificado para vê-las ou recebê-las.

**[!DNL Offer Decisioning]**: [!DNL Offer Decisioning] permite que profissionais de marketing gerenciem regras e modelos treinados de propostas de ofertas ao interagirem com usuários finais com base em dados coletados em canais e aplicativos.

**Biblioteca de ofertas**: a biblioteca de ofertas é uma biblioteca central usada para gerenciar ofertas personalizadas e substitutas, regras de decisão e atividades.

**Ação de marketing para personalização no site**: uma ação de marketing que usa dados para a personalização de conteúdo no site. A personalização no site inclui todos os dados usados para deduzir os interesses dos usuários e é usada para selecionar qual conteúdo ou quais anúncios são veiculados com base nessas deduções.

**Ação de marketing para direcionamento no site**: uma ação de marketing que usa dados para anúncios no site, incluindo a seleção e a entrega de anúncios nos sites ou aplicativos da organização, ou para medir a entrega e a eficácia desses anúncios.

**Uma vez**: no contexto de exportações de arquivos agendadas, agenda uma exportação de arquivos completa, sob demanda e única.

**Substituir estratégia de salvamento**: a estratégia de salvamento &quot;Substituir&quot; é uma opção para assimilar dados de terceiros por meio de uma conexão, na qual você pode especificar se os dados assimilados serão substituídos em um agendamento especificado.

## P

**Assimilação parcial**: a assimilação parcial permite a assimilação de registros válidos de dados em lote dentro de um limite de erro especificado. O diagnóstico de erro para registros com falha pode ser baixado ou acessado na visão geral de execução do fluxo de dados [!UICONTROL Monitoring] ou [!UICONTROL Sources].

**Arquivos Parquet**: um arquivo Parquet é um formato de arquivo de armazenamento em colunas com estruturas de dados aninhadas complexas. Os arquivos Parquet são necessários para adicionar dados a fim de preencher um conjunto de dados de esquema.

**PDPA**: o [[!DNL Personal Data Protection Act (PDPA)]](https://www.pdpc.gov.sg/Overview-of-PDPA/The-Legislation/Personal-Data-Protection-Act) foi introduzido para proteger os proprietários de dados tailandeses da coleta, uso ou divulgação ilegais de seus dados pessoais. Inspirado pelo GDPR da União Europeia, o regulamento concede aos cidadãos tailandeses o direito de solicitar acesso ou a exclusão de seus dados pessoais armazenados.

**Ofertas personalizadas**: uma oferta personalizada é uma mensagem de marketing personalizável baseada em regras de elegibilidade e restrições.

**PIPA** (Coreia do Sul): o [[!DNL Personal Information Protection Act] (PIPA)](https://elaw.klri.re.kr/eng_service/lawView.do?hseq=53044&lang=ENG) regula o processamento e a proteção de dados pessoais para residentes da Coreia do Sul. O PIPA concede direitos para ser informado, acessar, obter cópias e solicitar correção, exclusão ou suspensão do processamento. Os controladores de informações pessoais devem especificar os objetivos de coleta, processar os dados legalmente na extensão mínima necessária e garantir a precisão dos dados. A PIPA também criou a Comissão de Proteção de Informações Pessoais para investigar e aplicar as regulamentações de proteção de dados pessoais.

**Posicionamentos**: um posicionamento é o local e/ou contexto em que uma oferta é exibida para o usuário final.

**Espaço de trabalho de políticas**: um espaço de trabalho na interface do usuário do Experience Platform que permite aos administradores de dados exibir e gerenciar rótulos e políticas de uso de dados para sua organização.

**Política**: uma política de uso de dados é uma regra que especifica ações de marketing restritas com base na aplicação de rótulos de uso aplicados aos dados do Experience Platform.

**Imposição de política**: permite que você imponha políticas de uso de dados com ações de marketing aplicadas para impedir operações de dados que constituam violações de política em uma organização.

**Chave primária**: uma chave primária é uma designação em um esquema para identificar exclusivamente todos os registros.

**Prioridade**: em [!DNL Offer Decisioning], a prioridade é usada para classificar ofertas que atendam a todas as restrições, como qualificação, calendário e limite.

**Gráfico de identidade privada**: o gráfico de identidade privada (às vezes chamado de gráfico privado) é um mapa privado das relações entre identidades compiladas e vinculadas, que é criado com base nos dados primários e é visível apenas pela sua organização. Existe apenas um gráfico privado para cada organização e ele serve como blueprint estrutural para os gráficos de identidade individuais gerados para cada cliente que interage com sua marca.

**Perfil de produto**: os perfis de produto permitem que os administradores concedam ao usuário acesso a todos ou a um subconjunto de serviços associados ao Experience Platform.

**Sandbox de produção**: uma sandbox de produção é uma sandbox destinada para uso em seu ambiente de produção. Diferentemente das sandboxes de não produção, as sandboxes de produção não podem ser redefinidas ou excluídas.

**Perfil**: para não ser confundido com o Perfil de Cliente em Tempo Real como um serviço, um perfil é uma representação completa de um cliente individual, construído a partir de dados de série temporal e registro mesclados de várias fontes.

**Acesso ao perfil**: o ponto de extremidade `/entities` da API de Perfil do Cliente em Tempo Real permite que você acesse dados de registro e eventos de série temporal no repositório de dados do Perfil. Consulte também: Entidades de perfil

**Dados do perfil**: os dados do perfil se referem a quaisquer dados localizados no repositório de dados do Perfil.

**Armazenamento de dados do perfil**: o Armazenamento de dados do perfil (às vezes chamado de Armazenamento de perfil) é um sistema de armazenamento de dados separado do data lake, usado pelo Perfil do cliente em tempo real para criar e armazenar perfis.

**Entidades de perfil**: as entidades de perfil representam atributos relacionados a uma pessoa individual, geralmente um cliente. As entidades que se enquadram nessa categoria devem ser representadas por esquemas baseados na classe [!DNL XDM Individual Profile]. Consulte também: Acesso ao perfil

**Exportação de perfil**: a exportação [!DNL Profile] é um dos dois tipos de destinos no Experience Platform. A exportação do [!DNL Profile] gera um arquivo contendo perfis e atributos, e usa dados PII brutos com email para integrar-se a plataformas de marketing e automação de email.

**Fragmento de perfil**: um fragmento de perfil são as informações de perfil de apenas uma identidade da lista de identidades existentes para um determinado cliente.

**ID de Perfil**: uma ID de perfil é um identificador gerado automaticamente associado a um tipo de identidade e representa um perfil.

**Propriedade**: no contexto de marcas, uma propriedade é um contêiner de tudo o que é necessário para implantar um conjunto de marcas.

## Q

**Consulta**: consultas são solicitações de dados de tabelas de banco de dados.

**Editor de Consultas**: o Editor de Consultas é uma ferramenta para gravar, validar e enviar instruções SQL em [!DNL Query Service].

## R

**Real-Time Customer Data Platform**: o Adobe Real-Time Customer Data Platform (Real-Time CDP) reúne dados conhecidos e desconhecidos do cliente para criar perfis confiáveis do cliente com integração simplificada, segmentação inteligente e ativação em tempo real na jornada digital do cliente.

**Perfil do cliente em tempo real**: o Perfil do cliente em tempo real (às vezes chamado de Perfil) fornece uma visão holística de cada cliente individual ao combinar dados de vários canais, incluindo online, offline, CRM e de terceiros. O Perfil permite consolidar os dados do cliente em perfis individuais, oferecendo contas acionáveis com carimbo de data e hora para cada interação com o cliente.

**Receita**: uma fórmula é o termo da Adobe para uma especificação de modelo e é um contêiner de nível superior que representa processos de aprendizado de máquina específicos, algoritmos de IA, lógica de processamento e parâmetros de configuração necessários para criar e executar um modelo treinado e, portanto, ajudar a resolver problemas comerciais específicos.

**Registro**: um registro são dados que persistem como linhas em um conjunto de dados.

**Dados de registro**: fornece informações sobre os atributos de um assunto. Um assunto pode ser uma organização ou um indivíduo.

**Recorrência**: em [!DNL Query Service], uma recorrência define se uma consulta está agendada para ser executada apenas uma vez ou de forma recorrente.

**Representação**: em [!DNL Offer Decisioning], uma representação é a informação usada por um canal para exibir uma oferta, como localização ou idioma.

**Recurso**: no contexto de marcas, um recurso é um termo genérico que se refere às opções que o usuário da marca pode configurar no ambiente cliente, incluindo extensões, elementos de dados e regras.

**Controle de acesso baseado em função**: o controle de acesso baseado em função permite que os administradores atribuam acesso e permissões aos usuários do Experience Platform. As permissões incluem a capacidade de visualizar e/ou usar recursos do Experience Platform, como criar sandboxes, definir esquemas e gerenciar conjuntos de dados.

**Regra**: no contexto de marcas, uma regra é uma coleção de componentes que definem um conjunto específico de eventos, condições e ações que devem ser agrupados logicamente.

**Componente de regra**: no contexto de marcas, os componentes de regra são os eventos, as condições e as ações que compõem uma regra.

**Tempo de execução**: o tempo de execução especifica um ambiente de tempo de execução para uma fórmula de aprendizado de máquina. Os tempos de execução de [!DNL Python], R, [!DNL Spark], PySpark e Tensorflow permitem que você insira uma URL para uma imagem do Docker de uma origem de fórmula.

## S

**Dados de amostra**: os dados de amostra são uma visualização de um arquivo de dados, normalmente as primeiras 100 linhas, que fornece a um cientista de dados ou engenheiro uma ideia de qual esquema ou dados estão no arquivo de dados.

**Sandbox**: uma sandbox é uma construção virtual que particiona uma única instância do Experience Platform em um ambiente virtual separado, a fim de ajudar a desenvolver aplicativos de experiência digital.

**Redefinição da sandbox**: uma redefinição da sandbox exclui todos os dados, incluindo dados, perfis e segmentos em uma sandbox. As redefinições de sandbox podem afetar dados conectados a destinos internos ou externos.

**Alternador de sandbox**: o controle do alternador de sandbox no Experience Platform permite que os usuários naveguem entre sandboxes às quais têm acesso. Alternar uma sandbox alterará todo o conteúdo e poderá alterar o acesso aos recursos com base em permissões.

**Agendamento**: um agendamento é uma especificação definida pelo usuário sobre a frequência ou a cadência da assimilação de dados de uma fonte de dados de terceiros para o Adobe Experience Platform.

**Pontuação**: a pontuação é o processo de gerar insights dos dados usando um modelo treinado.

**Esquema**: um esquema é um conjunto de regras que representam e validam a estrutura e o formato dos dados. Um esquema é composto de uma classe e grupos de campos opcionais e é usado para criar conjuntos de dados e fluxos de dados. Um esquema pode incluir atributos comportamentais, carimbos de data e hora, identidades, definições de atributos, relacionamentos e muito mais.

**Grupo de campos de esquema**: no Experience Data Model (XDM), um grupo de campos de esquema permite que os usuários estendam campos reutilizáveis para definir um ou mais atributos destinados a serem incluídos em um esquema.

**Biblioteca de Esquemas**: a Biblioteca de Esquemas contém recursos XDM padrão do setor disponibilizados pela Adobe, bem como recursos personalizados definidos pela sua organização.

**Registro de Esquema**: o Registro de Esquema fornece uma interface de usuário e uma API RESTful usadas para exibir e gerenciar todos os recursos relacionados ao esquema na Biblioteca de Esquemas.

**Chave de acesso secreta**: uma chave de acesso secreta é uma chave S3 [!DNL Amazon] usada em conjunto com a ID da chave de acesso para assinar solicitações AWS.

**Segmento**: um segmento é um conjunto de regras que incluem atributos e dados de evento que qualificam vários perfis para se tornarem uma audiência.

**Construtor de segmentos**: [!DNL Segment Builder] é um ambiente de desenvolvimento visual usado para criar definições de segmentos. Ele serve como um componente comum de todos os aplicativos que usam o Serviço de segmentação da Experience Platform.

**Definição de segmento**: uma definição de segmento é o conjunto de regras usado para descrever as principais características ou comportamento de um público-alvo. Depois de conceitualizadas, as regras descritas em uma definição de segmento são usadas para determinar os membros do público-alvo qualificados para um segmento.

**Método de avaliação de segmento**: há dois métodos de avaliação de segmento: programado e sob demanda. A avaliação agendada permite um agendamento recorrente para executar um trabalho de exportação em um momento específico, enquanto a avaliação sob demanda envolve a criação de um trabalho de segmento para criar o público-alvo imediatamente.

**Exportação de segmentos**: a exportação de segmentos é um dos dois tipos de destinos no Experience Platform. Com a exportação de segmentos, é possível enviar os perfis qualificados e mapeados para o destino. Usa IDs de segmento e usuário e dados com pseudônimos e geralmente se integra a redes sociais e outras plataformas de mídia digital de destino.

**ID de segmento**: uma ID de segmento é um identificador gerado automaticamente associado a um segmento.

**Associação de segmento**: a associação de segmento exibe de quais segmentos um perfil faz parte no momento.

**Regras de segmento**: as regras de segmento definem as condições que determinam se um perfil se qualifica para um segmento.

**Segmentação**: a segmentação é o processo de dividir um grande grupo de clientes, clientes potenciais ou consumidores em grupos menores que compartilham atributos semelhantes e responderão de forma semelhante a estratégias de marketing específicas.

**Sensei ML Framework**: o Sensei ML Framework é uma estrutura de aprendizado de máquina unificada (ML) que aproveita os dados do Experience Platform para capacitar cientistas de dados a desenvolver serviços de inteligência orientados por aprendizado de máquina de maneira mais rápida, escalável e reutilizável.

**Rótulos sensíveis (&quot;S&quot;)**: os rótulos sensíveis (&quot;S&quot;) são usados para categorizar dados considerados confidenciais, como diferentes tipos de dados comportamentais ou geográficos que você deseja marcar como confidenciais.

**Serviços**: uma estrutura eficiente para operacionalizar serviços de IA e ML aproveitando os Serviços Inteligentes da Adobe. Os serviços proporcionam experiências personalizadas e em tempo real aos clientes ou operacionalizam serviços inteligentes personalizados.

**Ação de marketing de personalização de identidade única**: uma ação de marketing que usa dados para personalização de conteúdo no site. A personalização no local são quaisquer dados usados para deduzir os interesses dos usuários e são usados para selecionar qual conteúdo ou quais anúncios são veiculados com base nessas deduções.

Rótulo de uso de dados **S1**: um rótulo de uso de dados `S1` é usado para classificar dados que especificam latitude e longitude que podem ser usados para determinar a localização precisa de um dispositivo.

Rótulo de uso de dados **S2**: um rótulo de uso de dados `S2` é usado para classificar dados que podem ser usados para determinar uma área de cerca geográfica amplamente definida.

**Source**: uma origem é um termo geral para qualquer conector de entrada no Experience Platform. Consulte também: Conector do Source

**Atributo Source**: um atributo de origem é um campo no conjunto de dados de origem. Os atributos do Source são mapeados para campos de esquema de destino.

**Catálogo do Source**: o catálogo de origem é a lista de conectores de origem disponíveis no Experience Platform.

**Categoria do Source**: uma categoria de origem é um agrupamento de origens que têm características semelhantes.

**Conector do Source**: os conectores do Source (também conhecidos como fontes) ajudam os usuários a assimilar dados facilmente de várias fontes, permitindo a estruturação, a rotulagem e o aprimoramento de dados usando os serviços da Experience Platform. Os dados podem ser assimilados de várias fontes, como armazenamento baseado em nuvem, software de terceiros e sistemas de CRM.

**Conexão de streaming**: uma conexão de streaming é um ponto de extremidade exclusivo fornecido pela Adobe e vinculado à sua organização para transmitir dados para a Experience Platform.

**Namespace de identidade padrão**: os namespaces de identidade padrão são namespaces de identidade predefinidos fornecidos pela Adobe, que representam soluções padrão do setor normalmente usadas para identificar clientes.

**Assimilação por streaming**: a assimilação por streaming permite enviar dados de dispositivos no lado do cliente e do servidor para a Experience Platform em tempo real.

**Segmentação de transmissão**: a segmentação de transmissão é um processo de seleção de dados em andamento que atualiza os segmentos em resposta à atividade do usuário. Depois que um segmento é criado e salvo, a definição do segmento é aplicada em relação aos dados recebidos para [!DNL Real-Time Customer Profile]. As adições e remoções de segmentos são processadas regularmente, garantindo que o público-alvo permaneça relevante.

**Exibição do Sistema**: a Exibição do Sistema é uma representação visual de conjuntos de dados de origem que fluem através de [!DNL Real-Time Customer Profile] para destinos.

## T

**Tags**: na Adobe Experience Platform, as tags fornecem ferramentas para implantar, unificar e gerenciar integrações de análises, marketing e anúncios necessárias para potencializar experiências de cliente relevantes em todos os dispositivos cliente.

**Recursos de destino**: no mapeamento de recursos, um recurso de destino é o recurso previsto por um modelo.

**Dados de série temporal**: os dados de série temporal fornecem um instantâneo do sistema no momento em que uma ação foi tomada direta ou indiretamente por um titular de registro.

**Modelo treinado**: um modelo treinado representa a saída executável de um processo de treinamento de modelo, no qual um conjunto de dados de treinamento foi aplicado à instância do modelo. Um modelo treinado manterá uma referência a qualquer serviço da Web inteligente criado a partir dele. Um modelo treinado é adequado para pontuar e criar um serviço web inteligente.

**Token**: um token é um tipo de segurança de autenticação de dois fatores que pode ser usado para autorizar o uso de serviços de computador com [!DNL Query Service].

## U

**UCPA**: O [[!DNL Utah Consumer Privacy Act]](https://le.utah.gov/~2022/bills/static/SB0227.html) cria o direito para um consumidor saber quais dados pessoais uma empresa coleta, como a empresa usa seus dados pessoais e se a empresa vende seus dados pessoais. Os consumidores podem exigir que a empresa exclua ou pare de vender seus dados pessoais.

**Esquema de união**: um esquema de união é uma consolidação de esquemas que compartilham a mesma classe e foram habilitados para [!DNL Real-Time Customer Profile]. Vários esquemas de união podem existir para uma organização, mas só pode haver um esquema de união por classe.

## V

**VCDPA**: o [[!DNL Virginia Consumer Data Protection Act (VCDPA)]](https://lis.virginia.gov/cgi-bin/legp604.exe?212+sum+HB2307) fornece novos direitos de privacidade de dados a residentes da Virgínia (&quot;Consumidores&quot;), incluindo o direito de acessar, excluir e corrigir dados pessoais. Os consumidores também têm o direito de recusar a venda de dados pessoais, recusar a definição de perfis com base em dados pessoais e o processamento de fins de publicidade pessoal.

## W

## X

**XDM**: consulte Experience Data Model (XDM).

**Evento de decisão XDM**: o Evento de decisão XDM é uma classe baseada em série temporal usada para capturar observações sobre o resultado e o contexto de uma atividade de decisão. Isso inclui informações sobre como a decisão foi tomada, quando ocorreu, quais opções foram propostas (e escolhidas) e qual estado contextual existia que influenciou a decisão ou poderia ser observado durante o processo de decisão.

**XDM ExperienceEvent**: XDM ExperienceEvent é uma classe baseada em séries de tempo usada para capturar o estado do sistema quando um evento (ou conjunto de eventos) ocorreu, incluindo o momento e a identidade do assunto envolvido. Consulte também: Evento de experiência

**Perfil Individual XDM**: XDM [!DNL Individual Profile] é uma classe baseada em registros que forma uma representação singular dos atributos de assuntos identificados e parcialmente identificados. Os perfis altamente identificados podem ser usados para comunicações pessoais ou compromissos direcionados e podem conter informações pessoais detalhadas, como nome, sexo, data de nascimento, local e informações de contato, incluindo números de telefone e endereços de email.

**Sistema XDM**: o Sistema XDM representa a estrutura que operacionaliza esquemas XDM para uso em serviços downstream do Experience Platform.

## Y

## Z
