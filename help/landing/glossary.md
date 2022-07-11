---
keywords: Experience Platform, home, tópicos populares
solution: Experience Platform
title: Glossário do Adobe Experience Platform
topic-legacy: getting started
description: Um glossário de terminologia importante na Experience Platform.
exl-id: 00eae5f5-7dfa-45ac-aff9-9e1769a3a53a
source-git-commit: c0f01efa224bffb5b435e2f247e793edfbc576b9
workflow-type: tm+mt
source-wordcount: '7428'
ht-degree: 0%

---

# Glossário da Adobe Experience Platform {#adobe-experience-platform-glossary}

## A

**Controle de acesso**: O controle de acesso baseado em funções permite que os administradores atribuam acesso e permissões aos usuários do Experience Platform. As permissões incluem a capacidade de exibir e/ou usar recursos do Experience Platform, como criar sandboxes, definir esquemas e gerenciar conjuntos de dados.

**ID da chave de acesso**: Uma ID de chave de acesso é um identificador exclusivo associado a um [!DNL Amazon] Chave de acesso secreta S3. A ID da chave de acesso e a chave de acesso secreta são usadas em conjunto para assinar [!DNL Amazon Web Services] Solicitações do (AWS).

**Ação**: No contexto de tags, uma ação é um tipo específico de componente de regra que define o que deve ocorrer depois que um evento ocorre e as condições são avaliadas e passadas.

**Ativar**: Ativar é a ação realizada por um usuário para mapear um segmento ou perfis para um destino, como [!DNL Oracle Eloqua], [!DNL Google]ou [!DNL Salesforce Marketing Cloud].

**Atividade**: Em [!DNL Offer Decisioning], uma atividade contém a lógica que informa a seleção de uma oferta.

**Administrador**: Um ou mais indivíduos em sua organização que podem configurar e personalizar permissões do Experience Platform no Adobe Admin Console.

**Adobe Admin Console**: A Adobe Admin Console fornece um local central para gerenciar direitos de produto e acesso do Adobe para sua organização. Por meio do console, os administradores podem conceder a grupos de usuários permissões de acesso para vários recursos da plataforma, como &quot;Gerenciar conjuntos de dados&quot;, &quot;Visualizar conjuntos de dados&quot; ou &quot;Gerenciar perfis&quot;.

**Adobe Experience Platform**: A Adobe Experience Platform padroniza dados e conteúdo em toda a empresa, acionando perfis de clientes em tempo real, permitindo a ciência de dados e acelerando a velocidade do conteúdo para impulsionar a personalização da experiência na jornada do cliente.

**Serviço de query Adobe Experience Platform**: Permite que analistas de dados consultem eventos e perfis para uso em análises e aprendizado de máquina. Com o Serviço de query, cientistas e analistas de dados podem obter todos os seus conjuntos de dados armazenados no Experience Platform (incluindo dados comportamentais, bem como ponto de venda (POS), gerenciamento de relacionamento com o cliente (CRM) e muito mais) e consultar esses conjuntos de dados para responder perguntas específicas sobre os dados.

**Serviço de segmentação do Adobe Experience Platform**: Permite a criação de segmentos e a geração de públicos-alvo a partir dos dados do Perfil do cliente em tempo real. Esses públicos-alvo podem ser exportados para seus próprios conjuntos de dados no Data Lake.

**Serviços inteligentes do Adobe**: Serviços inteligentes, como Attribution AI e Customer AI, são modelos baseados em inteligência artificial, de aprendizado de máquina, criados especificamente e que exigem Experience Platform para ser executado e operado.

**Adobe I/O**: O Adobe I/O faz parte do Experience Platform e fornece acesso a tudo que os desenvolvedores precisam para integrar, estender e personalizar a Plataforma, incluindo APIs, eventos, console do desenvolvedor e ferramentas úteis.

**Adobe Sensei**: Adobe Sensei é a estrutura de inteligência que alimenta o Experience Platform. Ele também fornece um conjunto de serviços de IA que capacita as marcas a aprimorar sua capacidade de fornecer experiências personalizadas em tempo real para os clientes.

**Bucket do Amazon S3**: [!DNL Amazon S3] os buckets são os contêineres fundamentais para os dados armazenados no [!DNL Amazon] ecosistema. Os bucket contêm objetos, cada objeto é armazenado e recuperado usando uma chave exclusiva atribuída pelo desenvolvedor.

**Conector Amazon S3**: O [!DNL Amazon] O conector S3 permite que os clientes do Experience Platform se conectem e acessem com segurança seus [!DNL Amazon] Dados S3.

**Anexar estratégia de salvamento**: A estratégia de salvar &quot;anexar&quot; é uma opção usada ao especificar dados de terceiros para assimilar por meio de uma conexão e ao anexar quaisquer novos dados ou linhas no final do conjunto de dados. As linhas assimiladas anteriormente permanecem intocadas e apenas as linhas criadas desde a última execução agendada são assimiladas ao Experience Platform. Todas as linhas que foram alteradas no sistema de origem permanecem inalteradas no Experience Platform.

**Matriz**: As matrizes são usadas para elementos ordenados com o mesmo tipo de dados.

**Inteligência artificial**: A inteligência artificial é uma teoria e desenvolvimento de sistemas computacionais que são capazes de executar tarefas que normalmente exigem inteligência humana, como percepção visual, reconhecimento de voz, tomada de decisões e tradução entre línguas.

**Atributos**: Os atributos são características especificadas que representam um perfil.

**Mesclagem de atributos**: Ao definir uma política de mesclagem usando a API do Perfil do cliente em tempo real, a variável `attributeMerge` indica a maneira pela qual a política de mesclagem priorizará os atributos de perfil em caso de conflitos de dados. É equivalente a selecionar um [!UICONTROL Método de mesclagem] ao definir uma política de mesclagem na interface do usuário da plataforma.

**Attribution AI**: [!DNL Attribution AI] O é um serviço inteligente desenvolvido pela Adobe Sensei que oferece recursos algorítmicos de atribuição de vários canais em todo o ciclo de vida do cliente.

**Público**: Um público-alvo é o conjunto resultante de perfis que atendem aos critérios de uma definição de segmento.

**Tamanho do público-alvo**: Um tamanho de público-alvo é o número total de perfis que atendem aos critérios de uma definição de segmento e se qualificam para associação de público-alvo.

**Instantâneo do público-alvo**: Um instantâneo de público-alvo captura todos os perfis qualificados para os critérios de segmento no momento da segmentação.

## B

**Preenchimento retroativo**: Para fontes programadas, a opção de preenchimento retroativo permite a assimilação de dados históricos.

**Período de preenchimento retroativo**: O período de preenchimento retroativo é uma opção para definir o tempo para assimilar dados históricos de terceiros por meio de uma conexão de origem. Selecionar um período de preenchimento retroativo de &quot;para sempre&quot; assimilará todo o histórico dos dados de origem ao Experience Platform.

**Em lote**: Um lote é um conjunto de dados coletados durante um período de tempo e processados juntos como uma única unidade. Os conjuntos de dados são compostos de vários lotes.

**ID em lote**: Uma ID de lote é um identificador gerado por Adobe para um lote de dados.

**Ingestão em lote**: A assimilação em lote permite assimilar dados no Experience Platform como arquivos em lote. Lotes são unidades de dados que consistem em um ou mais arquivos que serão assimilados como uma única unidade.

**Segmentação em lote**: A segmentação em lote é uma alternativa a um processo de seleção de dados contínuo e move todos os dados de perfil de uma só vez por meio de definições de segmento para produzir públicos correspondentes. Depois de criado, esse segmento é salvo e armazenado para que possa ser exportado para uso.

**Criar**: No contexto de tags, uma build é um arquivo ou conjunto de arquivos que contêm todas as configurações e códigos necessários para executar a lógica comercial contida em uma biblioteca, permitindo implantar essa biblioteca no site ou no aplicativo móvel.

**Ferramentas de inteligência empresarial**: As ferramentas de Inteligência empresarial (BI, Business Intelligence) são integradas basicamente a [!DNL Experience Platform Query Service]. As ferramentas de BI são tipos de software de aplicativos que coletam e processam grandes quantidades de dados não estruturados de sistemas internos e externos.

## C

**Limitação**: Em [!DNL Offer Decisioning], o limite de frequência (também conhecido como limite de frequência) é usado em regras de decisão para definir quantas vezes uma oferta é apresentada. Há dois tipos de maiúsculas: quantas vezes uma oferta pode ser proposta para o público-alvo combinado (chamado de &quot;Limite global&quot;) e quantas vezes uma oferta pode ser proposta para o mesmo usuário final (chamado de &quot;Limite de perfil&quot;).

**Catálogo**: No contexto de fontes e destinos, um catálogo é uma galeria com conexões disponíveis para aplicativos Adobe e tecnologias de terceiros. Não confundir com [!DNL Catalog Service].

**[!DNL Catalog Service]**: [!DNL Catalog Service] (às vezes chamada de [!DNL Catalog]) é o sistema de registro para localização e linhagem de dados no Adobe Experience Platform. Enquanto todos os dados assimilados no Experience Platform são armazenados no lago de dados como arquivos e diretórios, [!DNL Catalog] contém os metadados e a descrição desses arquivos e diretórios para fins de pesquisa, monitoramento e controle de dados.

**Classe**: No Experience Data Model (XDM), uma classe define o menor conjunto de campos usados para criar um esquema e define o comportamento básico do objeto comercial que o esquema representa.

**Cliente**: Um cliente é uma ferramenta ou aplicativo externo que se conecta a [!DNL Query Service] via protocolo PostgreSQL ou API HTTP.

**Coleção**: Em [!DNL Offer Decisioning], as coleções são subconjuntos de ofertas com base em condições predefinidas definidas por um profissional de marketing, como a categoria da oferta.

**Combinar com ação de marketing PII**: Uma ação de marketing que combina informações pessoalmente identificáveis (PII) com dados anônimos. Os contratos para dados provenientes de redes de anúncios, servidores de anúncios e provedores de dados de terceiros frequentemente incluem proibições contratuais específicas sobre o uso desses dados com dados diretamente identificáveis.

**Interface de linha de comando**: Uma interface de linha de comando é uma ferramenta baseada em texto que pode ser usada para se conectar [!DNL Query Service] para execução de query bruta.

**Composição**: Uma composição é um agrupamento de componentes que formam juntos para formar o schema.

**Condição**: No contexto de tags, uma condição é um componente de regra que avalia uma instrução lógica que deve retornar `true` ou `false`. Todas as condições devem ser avaliadas para `true` e todas as condições de exceção devem ser avaliadas como `false` antes da execução de qualquer ação na regra.

**Console**: Em [!DNL Query Service], o console fornece informações sobre o status e a operação de um query. O console exibe o status da conexão com [!DNL Query Service], as operações de query sendo executadas e qualquer mensagem de erro que resulte dessas consultas.

**Rótulos contratuais (&quot;C&quot;)**: Os rótulos de uso de dados do contrato (&quot;C&quot;) são usados para categorizar os dados que têm obrigações contratuais ou estão relacionados às políticas de governança de dados de um cliente.

**Rótulo do contrato C1**: A `C1` o rótulo de uso de dados do contrato especifica que os dados só podem ser exportados da Adobe Experience Cloud em um formulário agregado sem incluir identificadores individuais ou de dispositivos. Por exemplo, dados que se originaram de redes sociais.

**Rótulo do contrato C2**: A `C2` o rótulo de uso de dados do contrato especifica os dados que não podem ser exportados para um terceiro. Alguns provedores de dados têm termos em seus contratos que proíbem a exportação de dados de onde eles foram originalmente coletados. Por exemplo, os contratos de redes sociais geralmente restringem a transferência de dados que você recebe deles. C2 é mais restritivo que C1, o que requer apenas agregação e dados anônimos.

**Rótulo do contrato C3**: A `C3` o rótulo de uso de dados do contrato especifica os dados que não podem ser combinados ou usados com informações diretamente identificáveis. Alguns provedores de dados têm termos em seus contratos que proíbem a combinação ou o uso desses dados com informações diretamente identificáveis. Por exemplo, os contratos para dados obtidos de redes de anúncios, servidores de anúncios e provedores de dados de terceiros geralmente incluem proibições contratuais específicas sobre o uso de dados diretamente identificáveis.

**Rótulo do contrato C4**: A `C4` o rótulo de uso de dados do contrato especifica que os dados não podem ser usados para direcionar qualquer anúncio ou conteúdo, seja no site ou entre sites. C4 é o rótulo mais restritivo, pois abrange rótulos C5, C6 e C7.

**Rótulo do contrato C5**: A `C5` o rótulo de uso de dados do contrato especifica que os dados não podem ser usados para direcionamento entre sites de conteúdo ou anúncios com base em interesses. O direcionamento baseado em interesses ou a personalização ocorrem se as três condições a seguir forem atendidas: Os dados recolhidos no local são utilizados para fazer ilações sobre o interesse de um utilizador; é usada em outro contexto, como em outro site ou aplicativo; e é usado para selecionar qual conteúdo ou anúncios são exibidos com base nessas inferências.

**Rótulo do contrato C6**: A `C6` o rótulo de uso de dados do contrato especifica que os dados não podem ser usados para direcionamento de anúncios no site. O direcionamento de anúncios no site inclui a seleção e a entrega de anúncios nos sites ou aplicativos de sua organização, ou para medir a entrega e a eficácia de tais anúncios. Isso inclui o uso de dados no site coletados anteriormente sobre o interesse dos usuários em selecionar anúncios, processar dados sobre quais anúncios foram mostrados, quando e onde foram exibidos e se os usuários tomaram alguma ação relacionada ao anúncio, como selecionar um anúncio ou fazer uma compra.

**Rótulo do contrato C7**: A `C7` o rótulo de uso de dados do contrato especifica que os dados não podem ser usados para direcionamento no site do conteúdo. O direcionamento de conteúdo no site inclui a seleção e a entrega de conteúdo nos sites ou aplicativos de sua organização, ou para medir a entrega e a eficácia de tal conteúdo. Isso inclui informações coletadas anteriormente sobre o interesse dos usuários em selecionar o conteúdo, processar dados sobre qual conteúdo foi exibido, com que frequência ou por quanto tempo foi exibido, quando e onde foi exibido e se os usuários realizaram ações relacionadas ao conteúdo, incluindo, por exemplo, a seleção de conteúdo.

**Rótulo do contrato C8**: A `C8` o rótulo de uso de dados do contrato especifica que os dados não podem ser usados para medir os sites ou aplicativos de sua organização. Isso não inclui o direcionamento baseado em interesses, que é a coleção de informações sobre o uso desse serviço para personalizar subsequentemente o conteúdo e/ou a publicidade em outros contextos.

**Rótulo do contrato C9**: A `C9` o rótulo de uso de dados do contrato especifica que os dados não podem ser usados em workflows da ciência de dados. Alguns contratos incluem proibições explícitas sobre os dados utilizados na ciência de dados. Às vezes, elas são redigidas em termos que proíbem o uso de dados para inteligência artificial (IA), aprendizado de máquina (ML) ou modelagem.

**Rótulo do contrato C10**: A `C10` o rótulo de uso de dados do contrato especifica que os dados não podem ser usados para a ativação de identidade compilada. Algumas políticas de uso de dados restringem o uso de dados de identidade compilados para personalização. O `C10` será aplicado automaticamente aos segmentos se suas políticas de mesclagem usarem a opção &quot;gráfico privado&quot;.

**Coluna Data de criação**: Selecionar uma coluna Data de criação é uma opção ao especificar dados de terceiros por meio de uma conexão de origem. Quando a estratégia append save é selecionada e o esquema do conjunto de dados contém vários campos de data, é necessário escolher entre o esquema disponível para especificar uma coluna chave Created Date . A opção Data de criação não está disponível quando a estratégia de salvar de substituição é selecionada.

**Criar tabela como selecionada**: Criar Tabela como Selecionar (CTAS) é um comando SQL que, quando executado como parte de uma consulta SQL completa e válida, instrui [!DNL Query Service] para manter os resultados da consulta em um conjunto de dados. Você pode criar um novo conjunto de resultados, substituir os resultados anteriores ou anexar aos resultados anteriores.

**Dados entre sites**: Dados entre sites é a combinação de dados de vários sites, incluindo uma combinação de dados no site e dados fora do site ou uma combinação de dados de várias fontes fora do site.

**Ação de marketing de direcionamento entre sites**: Uma ação de marketing que usa dados para o direcionamento de anúncios entre sites. A combinação de dados de vários sites, incluindo uma combinação de dados no local e dados fora do site ou uma combinação de dados de várias fontes fora do site, é chamada de dados entre sites. Os dados entre sites geralmente são coletados e processados para fazer inferências sobre os interesses dos clientes.

**Namespace de identidade personalizada**: Os namespaces de identidade personalizados podem ser criados pela organização para representar identidades de uma organização ou caso comercial específico.

**Rótulos personalizados**: Os rótulos de uso de dados personalizados permitem criar e aplicar rótulos específicos a campos de dados que atendam às necessidades específicas da empresa.

**Customer AI**: O Customer AI é um Serviço inteligente desenvolvido pela Adobe Sensei que enriquece os perfis do cliente com propensões baseadas em IA e capacita os esforços de segmentação e direcionamento do cliente.

## D

**Diariamente**: No contexto de exportações de arquivos programadas, o agenda exportações completas ou incrementais de arquivos uma vez por dia, todos os dias, da data de início à data de término no momento especificado pelo usuário.

**Dicionário de dados**: No contexto de tags, um dicionário de dados (também conhecido como mapa de dados) é um conjunto de elementos de dados definidos em uma propriedade.

**Elemento de dados**: No contexto de tags, um elemento de dados é um ponteiro usado em regras e extensões para apontar para uma parte específica dos dados existentes no dispositivo cliente.

**Assimilação de dados**: A assimilação de dados é o processo de adição de dados de uma fonte ao Experience Platform. Os dados podem ser assimilados na plataforma de várias maneiras, incluindo streaming, lotes ou adicionados por meio de conectores de origem.

**Camada de dados**: No contexto de tags, uma camada de dados é uma estrutura de dados existente no dispositivo cliente que contém metadados sobre o contexto em que uma página ou tela é visualizada.

**Governança de dados**: O controle de dados abrange as estratégias e tecnologias usadas para garantir que os dados estejam em conformidade com os regulamentos e as políticas organizacionais em relação ao uso de dados.

**Parceiros de integração de dados**: Os parceiros de integração de dados simplificam e automatizam o carregamento e a transformação de grandes volumes de dados de mais de 200 fontes para Experience Platform sem gravar código.

**Rótulos do conjunto de dados**: Os rótulos de uso de dados podem ser adicionados aos conjuntos de dados. Todos os campos nesse conjunto de dados herdarão os rótulos do conjunto de dados.

**Data Science Workspace**: [!DNL Data Science Workspace] no Experience Platform permite que os clientes criem modelos de aprendizado automatizado utilizando dados em aplicativos da plataforma e do Adobe para criar segmentos inteligentes, gerar insights e fornecer previsões, permitindo que você aprimore consideravelmente as experiências digitais do usuário final.

**Fonte de dados**: Uma fonte de dados é uma origem de dados designada pelo usuário. Os exemplos de uma fonte de dados são um aplicativo móvel, eventos de perfil e/ou experiência, eventos de perfil de site ou um CRM.

**Data steward**: Um administrador de dados é a pessoa responsável pelo gerenciamento, supervisão e aplicação efetiva dos ativos de dados de uma organização. Um administrador de dados também garante que as políticas de governança de dados sejam salvaguardadas e mantidas para serem compatíveis com os regulamentos governamentais e as políticas organizacionais.

**Fluxo de dados**: Um fluxo de dados é um conjunto ou coleção de mensagens que compartilham o mesmo esquema e são enviadas pela mesma fonte.

**Tipo de dados**: Um tipo de dados é um recurso XDM reutilizável que define um campo do tipo objeto contendo várias propriedades em uma representação hierárquica.

**Rótulos de uso de dados**: Os rótulos de uso de dados permitem categorizar os dados que refletem considerações relacionadas à privacidade e às condições contratuais para manter a conformidade com os regulamentos e as políticas corporativas. Os rótulos de uso de dados adicionados a um conjunto de dados são herdados ou aplicados a todos os campos nesse conjunto de dados. Os rótulos de uso de dados também podem ser aplicados diretamente aos campos.

**Fluxo de dados**: Um fluxo de dados é um pipeline virtual de dados que flui para a Platform de uma origem e de saída para destinos.

**Execução do fluxo de dados**: Uma execução de fluxo de dados é um fluxo de dados que chega ao Experience Platform com base em um agendamento especificado pelo usuário.

**Conjunto de dados**: Um conjunto de dados é uma construção de armazenamento e gerenciamento para uma coleção de dados, normalmente uma tabela, que contém um esquema (colunas) e campos (linhas).

**ID do conjunto de dados**: Um identificador gerado por Adobe para um conjunto de dados assimilado.

**Saída do conjunto de dados**: A saída do conjunto de dados fornece um mecanismo para determinar o que a opção &quot;Criar tabela como seleção&quot; será usada para um determinado [!DNL Query Service] executar.

**Chave de desduplicação**: Uma chave primária definida pelo usuário que determina a identidade pela qual os usuários desejam que seus perfis sejam desduplicados. &#x200B;

**Coluna delta**: Uma coluna delta permite selecionar um campo de dados de origem para representar um carimbo de data e hora para assimilação incremental.

**Estratégia de salvamento delta**: A estratégia de salvamento do delta é uma opção para assimilar dados de terceiros por meio de uma conexão de origem. A opção permite que o usuário especifique que linhas novas ou alteradas de dados de origem são assimiladas ao Experience Platform. Novas linhas são adicionadas ao final do conjunto de dados e as linhas alteradas são atualizadas no conjunto de dados no Experience Platform.

**Descritor**: No Experience Data Model (XDM), um descritor é um conjunto adicional de metadados relacionados ao esquema que descreve um comportamento específico para um campo. Os descritores podem ser usados pelo Experience Platform para entender o comportamento pretendido do schema, como a relação entre dois schemas.

**Destino**: Um destino é um termo geral para qualquer endpoint, como um aplicativo de Adobe, plataforma de publicidade, serviço de armazenamento em nuvem ou serviço de marketing, em que um público-alvo é ativado e entregue.

**Categoria de destino**: Uma categoria de destino é um agrupamento de destinos com características semelhantes.

**Catálogo de destino**: Um catálogo de destino é uma lista de destinos disponíveis no Experience Platform.

**Regras de chamada direta**: No contexto das tags , uma regra de chamada direta é uma regra que é executada quando é chamada diretamente da página, ignorando a detecção de eventos e os sistemas de pesquisa.

**Nome de exibição**: No Experience Data Model (XDM), um nome de exibição é amigável para um campo que é mostrado na interface do usuário.

## E

**Oferta elegível**: Uma oferta elegível pode ser oferecida de forma consistente a um perfil, pois atende às restrições definidas upstream.

**Regras de elegibilidade**: Em [!DNL Offer Decisioning], as regras de elegibilidade são aplicadas a um perfil relacionado a restrições de calendário, cronograma e limite.

**Ação de marketing de direcionamento de email**: Uma ação de marketing que usa dados em campanhas de segmentação de email.

**Código incorporado**: No contexto de tags, o código incorporado é uma tag de script colocada no HTML em um site ou ambiente. O código incorporado instrui o navegador para onde recuperar a build.

**Enumeração**: Uma enumeração (enum) é um campo XDM restrito a um conjunto de valores predefinidos.

**Ambiente**: No contexto de tags, um ambiente é um conjunto de instruções de implantação que especifica o delivery do host e o formato de arquivo de uma build. Uma biblioteca deve ser emparelhada a um ambiente antes de ser criada.

**Diagnóstico de erros**: Os diagnósticos de erros permitem a geração de mensagens de erro detalhadas para lotes assimilados. O limite de erro permite configurar a porcentagem de erros aceitáveis antes que um lote falhe.

**Evento**: No contexto de tags, um evento é um tipo específico de componente de regra, que é um acionador que ocorre em um dispositivo cliente para iniciar a execução de uma regra.

**Entidades de evento**: No contexto da modelagem de dados, as entidades de evento representam conceitos relacionados às ações que um cliente pode realizar, eventos do sistema ou qualquer outro conceito, onde você pode querer rastrear as alterações ao longo do tempo. As entidades abrangidas por esta categoria devem ser representadas por esquemas baseados no [!DNL XDM ExperienceEvent] classe .

**Eventos**: Eventos são os dados de comportamento associados a um perfil.

**Experience Data Model (XDM)** [!DNL Experience Data Model] (XDM) é uma estrutura de código aberto que usa esquemas padrão para unificar dados para uso com aplicativos Experience Platform e Adobe Experience Cloud. O XDM padroniza como os dados são estruturados e acelera e simplifica o processo de obter insights de grandes quantidades de dados.

**Experimento**: Um experimento é o processo de criação de um modelo treinado pela formação da instância com uma amostra de dados de produção ao vivo. Isso é diferente de um modelo treinado que é testado em um conjunto de dados de teste de retenção. Isso também é diferente do conceito de um experimento em alguns quadros de aprendizado de máquina, onde realmente significa um projeto de modelagem de amostra.

**Evento de experiência**: Um Evento de experiência representa um instantâneo do sistema quando ocorre uma interação ou evento relacionado a uma experiência do cliente. Os Eventos de experiência são registros de fatos imutáveis do que aconteceu e representam o que aconteceu sem agregação ou interpretação. No Experience Data Model (XDM), esse conceito é capturado pelo [!DNL XDM ExperienceEvent] classe .

**Exportar arquivo completo**: Um arquivo de exportação que contém um instantâneo completo de todas as qualificações de perfil para o segmento selecionado.

**Exportar arquivos incrementais**: Uma série de arquivos exportados, onde o primeiro arquivo é um instantâneo completo de todas as qualificações de perfil para o segmento selecionado e os arquivos subsequentes são qualificações de perfil incrementais desde a exportação anterior.

**Extensão**: No contexto de tags, uma extensão é um pacote de funcionalidade adicionada a uma propriedade de tag. Normalmente, uma extensão é focada em uma solução de marketing ou análise específica e fornece as ferramentas necessárias para implantar essa tecnologia em um ambiente cliente.

**Pacote de extensão**: No contexto de tags, um pacote de extensão é um arquivo ZIP criado e carregado por um desenvolvedor de extensão que fornece tudo o que é necessário para que os usuários das tags instalem a extensão dentro de suas propriedades. Um pacote de extensão contém um manifesto especificando informações sobre a extensão, o HTML/JavaScript necessário para que os usuários finais configurem o comportamento da extensão de tag e o JavaScript executável entregue ao ambiente do cliente (se necessário).

## F

**Ofertas de fallback**: Uma oferta de fallback é a oferta padrão exibida quando um usuário final não está qualificado para nenhuma das ofertas na coleção usada.

**Mapeamento de recursos**: O mapeamento de recursos refere-se ao processo de mapeamento de recursos de dados para recursos de entrada e destino exigidos por um modelo de aprendizado de máquina.

**Campo**: Um campo é o elemento de nível mais baixo de um conjunto de dados, conforme definido pelo esquema XDM do conjunto de dados. Cada campo tem um nome para fins de referência e um tipo para indicar o tipo de dados que ele contém. Os tipos de campo podem incluir (mas não estão limitados a) número inteiro, número, string, booleano e objeto.

**Grupo de campos**: Consulte &quot;Grupo de campos do esquema&quot;.

**Rótulos de campos**: Os rótulos de campo são rótulos de governança de dados que são herdados de um conjunto de dados ou aplicados diretamente a um campo.

**Nome do campo**: Um nome de campo é usado para referenciar o valor de um campo em queries e serviços downstream.

**Frequência**: Em [!DNL Query Service], a frequência determina a frequência de execução de uma consulta agendada recorrente.

## G

**Geofence**: Uma geofence é um limite geográfico virtual, definido pela tecnologia GPS ou RFID, que permite que o software acione uma resposta quando um dispositivo móvel entra ou sai de uma área específica.

**GDPR (Regulamento Geral sobre a Proteção de Dados)**: O Regulamento Geral sobre a Proteção de Dados (GDPR) é um quadro jurídico que estabelece diretrizes para a coleta e o processamento de informações pessoais de indivíduos dentro da União Europeia (UE). O GDPR estabelece os princípios para a gestão de dados e os direitos do indivíduo e abrange todas as empresas que lidam com os dados de cidadãos da UE.

**Medidas de proteção**: As garantias são limites que fornecem orientação para o uso de dados e do sistema, otimização de desempenho e prevenção de erros ou resultados inesperados no Adobe Experience Platform. As garantias podem se referir à utilização ou ao consumo de dados e ao processamento em relação aos direitos de licenciamento.

## H

**Host**: No contexto de tags, um host especifica o local, o domínio e as credenciais do usuário necessárias para que o sistema forneça uma build.

**Por hora**: No contexto de exportações de arquivos programadas, o agenda exportações de arquivos incrementais a cada 3, 6, 8 ou 12 horas.

## I

**Identidade**: Uma identidade é um identificador que representa exclusivamente um cliente individual, como uma ID de cookie, ID de dispositivo ou ID de email.

**Campos de identidade**: Campos de identidade são campos XDM usados para unir informações sobre clientes individuais provenientes de várias fontes de dados. Uma única identidade primária deve ser definida para que o schema seja ativado para uso no Perfil do cliente em tempo real.

**Rótulos de identidade (&quot;I&quot;)**: Os rótulos de uso de dados de identidade (&quot;I&quot;) são usados para categorizar dados que podem identificar ou entrar em contato com uma pessoa específica.

**Gráfico de identidade**: Um gráfico de identidade é um mapa de relacionamentos entre identidades compiladas e vinculadas que existem para um cliente individual. Cada gráfico de identidade é atualizado em tempo quase real com a atividade do cliente. A estrutura comum de relacionamentos de identidade em seus dados é representada pela variável [!UICONTROL Gráfico privado], que serve como o plano estrutural de cada gráfico de identidade individual.

**Namespace de identidade**: Um namespace de identidade define o contexto de um identificador, como um endereço de email ou ID de CRM.

**Serviço de identidade**: [!DNL Experience Platform Identity Service] permite a criação e o gerenciamento de tipos de identidade, permitindo vincular identidades de clientes em dispositivos e canais. A capacidade do serviço de vincular identidades permite que o Perfil do cliente em tempo real forneça uma representação completa de cada cliente individual.

**Compilação de identidade**: A identificação é o processo de identificação de fragmentos de dados e sua compilação para formar um registro de perfil completo.

**Símbolo de identidade**: Um símbolo de identidade é uma abreviação de um namespace de identidade que pode ser usado como referência em APIs.

**Valor de identidade**: Um valor de identidade, combinado com um namespace de identidade, é um identificador que representa um indivíduo, uma organização ou um ativo exclusivo. Ao corresponder dados de registro em fragmentos de perfil, o namespace e o valor de identidade devem corresponder.

**Rótulo de uso de dados I1**: O `I1` o rótulo de uso de dados é usado para classificar dados que podem identificar ou contatar diretamente uma pessoa específica em vez de um dispositivo.

**Rótulo de uso de dados I2**: O `I2` o rótulo de uso de dados é usado para classificar dados que podem ser usados em combinação com quaisquer outros dados para identificar ou contatar indiretamente uma pessoa específica.

**IMS Organization**: Uma Organização IMS (às vezes chamada de Organização IMS) é o nome usado para identificar uma empresa ou um grupo específico em uma empresa entre produtos de Adobe. Os administradores podem configurar e gerenciar o acesso e as permissões dos recursos para usuários de uma organização.

**Assimilação**: Consulte assimilação de dados.

**Cronograma de assimilação**: Um agendamento de assimilação fornece opções baseadas em tempo ao assimilar de uma origem para o Experience Platform.

**Recurso de entrada**: Um recurso de entrada é especificado no mapeamento de recursos e é usado por um modelo de aprendizado de máquina para fazer previsões.

**[!DNL Intelligent Services]**: [!DNL Intelligent Services] como [!DNL Attribution AI] e [!DNL Customer AI] são modelos baseados em inteligência artificial e aprendizado de máquina que exigem o Experience Platform (ou aplicativos criados sobre a plataforma, como o Real-time Customer Data Platform) para serem executados e operados.

**Direcionamento ou personalização com base em interesses**: O direcionamento baseado em juros, também conhecido como personalização, ocorre se as três condições a seguir forem atendidas:

1. Os dados coletados no site são usados para fazer inferências sobre o interesse de um usuário.
1. Os dados são usados em outro contexto, como em outro site ou aplicativo (fora do site).
1. Os dados são usados para selecionar qual conteúdo ou anúncios são exibidos com base nessas inferências.

## J

**[!DNL JupyterLab]**: Uma interface de código aberto baseada na Web para o Project [!DNL Jupyter] que é integrado à interface do usuário da plataforma.

**[!DNL Jupyter Notebook]**: Integrados ao JupyterLab, notebooks Jupyter permitem que você faça limpeza e transformação de dados, simulação numérica, modelagem estatística, visualização de dados, aprendizado de máquina e mais em seus dados de Experience Platform em uma variedade de idiomas como Python, Scala e PySpark.

##  mil

## L

**Biblioteca**: No contexto de tags, uma biblioteca é um conjunto de lógicas de negócios que contém instruções de como a biblioteca de tags deve se comportar no dispositivo cliente.

**Entidades de pesquisa**: No contexto da modelagem de dados, as entidades de pesquisa representam conceitos que podem estar relacionados a uma pessoa individual, mas não podem ser usadas diretamente para identificar o indivíduo. As entidades que se enquadram nesta categoria devem ser representadas por esquemas baseados em classes personalizadas do Experience Data Model (XDM).

## M

**Aprendizagem de máquina (ML)**: O aprendizado de máquina é o campo de estudo que permite que os computadores aprendam sem ser explicitamente programados.

**Modelo de aprendizagem de máquina**: Um modelo de aprendizado de máquina é uma instância de uma fórmula de aprendizado de máquina treinada com dados históricos e configurações para resolver um caso de uso comercial. No Adobe Experience Platform Data Science Workspace, os modelos de aprendizado por máquina são chamados de receitas.

**Atributo obrigatório**: Uma caixa de seleção ativada pelo usuário que garante que todos os registros de perfil contenham o atributo selecionado. Por exemplo: todos os perfis exportados contêm um endereço de email.

**Mapeamento**: O mapeamento de dados é o processo de mapeamento de campos de dados de origem para campos de destino relacionados em um destino.

**Ação de marketing**: Na estrutura de governança de dados, uma ação de marketing (também conhecida como caso de uso de marketing) é uma ação que um consumidor de dados de Experience Platform toma, para a qual há necessidade de verificar violações das políticas de uso de dados.

**Método de mesclagem**: Ao definir uma política de mesclagem usando a interface do usuário da plataforma, o método de mesclagem especifica como os fragmentos de dados devem ser priorizados quando ocorrer um conflito. Ao usar a API do perfil do cliente em tempo real para definir uma política de mesclagem, o método de mesclagem é determinado usando o `attributeMerge` objeto.

**Política de mesclagem**: As políticas de mesclagem são regras que o Experience Platform usa para determinar como os fragmentos de dados do cliente de várias fontes serão combinados para criar um perfil individual. Quando ocorre um conflito de dados, a política de mesclagem determina quais dados devem ser priorizados para inclusão no perfil.

**Mistura**: Consulte &quot;Grupo de campos do esquema&quot;.

**Módulo**: No contexto de tags, um módulo é um snippet do JavaScript executável fornecido por uma extensão, que executa ações em um ambiente cliente sem precisar criar uma regra.

## N

**Caixa de proteção de não produção**: As sandboxes de não produção são sandboxes normalmente usadas para experimentos de desenvolvimento, testes ou testes. Diferentemente das sandboxes de produção, as sandboxes de não produção podem ser redefinidas e excluídas.

**[!DNL Notebooks]**: [!DNL Notebooks] são criados usando [!DNL Jupyter Notebook] e podem ser executados para executar a análise de dados.

## O

**Oferta**: Uma oferta é uma mensagem de marketing contendo uma proposta de negócios ou de vendas para um cliente (potencial). As ofertas geralmente têm regras específicas que determinam quem está qualificado para vê-las ou recebê-las.

**[!DNL Offer Decisioning]**: [!DNL Offer Decisioning] permite que os profissionais de marketing gerenciem regras e modelos treinados de apresentações de oferta ao se envolverem com usuários finais com base em dados coletados em canais e aplicativos.

**Biblioteca de ofertas**: A biblioteca de ofertas é uma biblioteca central usada para gerenciar ofertas personalizadas e de fallback, regras de decisão e atividades.

**Ação de marketing de personalização no site**: Uma ação de marketing que usa dados para personalização de conteúdo no site. A personalização no site é qualquer dado usado para fazer inferências sobre os interesses dos usuários e é usado para selecionar qual conteúdo ou anúncios são exibidos com base nessas inferências.

**Ação de marketing de direcionamento no site**: Uma ação de marketing que usa dados para anúncios no site, incluindo a seleção e o delivery de anúncios nos sites ou aplicativos de sua organização, ou para medir a entrega e a eficácia de tais anúncios.

**Uma vez**: No contexto de exportações programadas de arquivos, o agenda uma única exportação de arquivos, sob demanda e completa.

**Substituir estratégia de salvamento**: A estratégia de salvamento &quot;Substituir&quot; é uma opção para assimilar dados de terceiros por meio de uma conexão, onde é possível especificar se os dados assimilados serão substituídos em um agendamento especificado.

## P

**Ingestão parcial**: A assimilação parcial permite a assimilação de registros válidos de dados em lote dentro de um limite de erro especificado. O diagnóstico de erro para registros com falha pode ser baixado ou acessado em [!UICONTROL Monitoramento] ou [!UICONTROL Fontes] visão geral da execução do fluxo de dados.

**Arquivos de parâmetro**: Um arquivo Parquet é um formato de arquivo de armazenamento em colunas com estruturas de dados aninhadas complexas. Os arquivos de parâmetro são necessários para adicionar dados para preencher um conjunto de dados de esquema.

**Ofertas personalizadas**: Uma oferta personalizada é uma mensagem de marketing personalizável com base em regras e restrições de elegibilidade.

**Posicionamentos**: um posicionamento é o local e/ou contexto em que uma oferta é exibida para um usuário final.

**Área de trabalho de políticas**: Um espaço de trabalho na interface do usuário da plataforma que permite aos administradores de dados visualizar e gerenciar rótulos e políticas de uso de dados para sua organização.

**Política**: Uma política de uso de dados é uma regra que especifica ações de marketing restritas com base na aplicação de rótulos de uso aplicados aos dados da plataforma.

**Aplicação da política**: Permite aplicar políticas de uso de dados com ações de marketing aplicadas para evitar operações de dados que constituem violações de política em uma organização.

**Chave primária**: Uma chave primária é uma designação em um schema para identificar exclusivamente todos os registros.

**Prioridade**: Em [!DNL Offer Decisioning], a prioridade é usada para classificar ofertas que atendem a todas as restrições, como qualificação, calendário e limite.

**Gráfico de identidade privada**: O gráfico de identidade privada (às vezes chamado de gráfico privado) é um mapa privado de relacionamentos entre identidades compiladas e vinculadas, que é criado com base nos dados primários e é visível somente pela sua organização. Existe apenas um gráfico privado para cada organização e serve como o blueprint estrutural para os gráficos de identidade individuais gerados para cada cliente que interage com sua marca.

**Perfil de produto**: Os perfis de produto permitem que os administradores concedam acesso de usuário a todos ou a um subconjunto de serviços associados ao Experience Platform.

**Sandbox de produção**: Uma sandbox de produção é uma sandbox destinada ao uso no ambiente de produção. Diferentemente das sandboxes de não produção, as sandboxes de produção não podem ser redefinidas ou excluídas.

**Perfil**: Para não ser confundido com o Real-time Customer Profile como um serviço, um perfil é uma representação completa de um cliente individual, construída a partir de dados de registro e série de tempo unidos de várias fontes.

**Acesso ao perfil**: O `/entities` O endpoint na API do Perfil do cliente em tempo real permite acessar dados de registro e eventos de série de tempo no armazenamento de dados do perfil. Consulte também: Entidades de perfil

**Dados do perfil**: Os dados do perfil se referem a quaisquer dados localizados no armazenamento de dados do Perfil.

**Armazenamento de dados do perfil**: O armazenamento de dados do Perfil (às vezes chamado de armazenamento de perfil) é um sistema de armazenamento de dados separado do lago de dados, usado pelo Perfil do cliente em tempo real para criar e armazenar perfis.

**Entidades de perfil**: As entidades de perfil representam atributos relacionados a uma pessoa individual, normalmente um cliente. As entidades abrangidas por esta categoria devem ser representadas por esquemas baseados no [!DNL XDM Individual Profile] classe . Consulte também: Acesso ao perfil

**Exportação de perfil**: [!DNL Profile] a exportação é um dos dois tipos de destinos em Experience Platform. [!DNL Profile] a exportação gera um arquivo contendo perfis e atributos, e usa dados PII brutos com email para integrar-se às plataformas de marketing e automação de email.

**Fragmento de perfil**: Um fragmento de perfil é a informação do perfil para apenas uma identidade da lista de identidades que existem para um cliente específico.

**ID do perfil**: Uma ID de perfil é um identificador gerado automaticamente associado a um tipo de identidade e representa um perfil.

**Propriedade**: No contexto de tags, uma propriedade é um contêiner de tudo o que é necessário para implantar um conjunto de tags.

## Q

**Query**: Queries são solicitações de dados de tabelas de banco de dados.

**Editor de consultas**: O Editor de consultas é uma ferramenta para gravar, validar e enviar instruções SQL em [!DNL Query Service].

## R

**Real-time Customer Data Platform**: [!DNL Real-time Customer Data Platform] reúne dados conhecidos e desconhecidos do cliente para criar perfis confiáveis do cliente com integração simplificada, segmentação inteligente e ativação em tempo real na jornada digital do cliente.

**Perfil do cliente em tempo real**: O Perfil do cliente em tempo real (às vezes chamado de Perfil) fornece uma visualização holística de cada cliente individual ao combinar dados de vários canais, incluindo online, offline, CRM e de terceiros. O Perfil permite consolidar os dados do cliente em perfis individuais que oferecem contas acionáveis com carimbos de data e hora de cada interação com o cliente.

**Receita**: Uma receita é um termo treinado para uma especificação de modelo e um contêiner de nível superior que representa processos específicos de aprendizado de máquina, algoritmos de IA, lógica de processamento e parâmetros de configuração necessários para criar e executar um modelo e, portanto, ajudar a resolver problemas específicos de negócios.

**Registro**: Um registro são dados que persistem como linhas em um conjunto de dados.

**Registrar dados**: Fornece informações sobre os atributos de um assunto. Um assunto pode ser uma organização ou um indivíduo.

**Recorrência**: Em [!DNL Query Service], uma recorrência define se um query é agendado para ser executado apenas uma vez ou de forma recorrente.

**Representação**: Em [!DNL Offer Decisioning], uma representação são informações usadas por um canal para exibir uma oferta, como local ou idioma.

**Recurso**: No contexto de tags, um recurso é um termo genérico que se refere às opções que o usuário da tag pode configurar dentro do ambiente do cliente, incluindo extensões, elementos de dados e regras.

**Controle de acesso baseado em funções**: O controle de acesso baseado em funções permite que os administradores atribuam acesso e permissões aos usuários do Experience Platform. As permissões incluem a capacidade de exibir e/ou usar recursos do Experience Platform, como criar sandboxes, definir esquemas e gerenciar conjuntos de dados.

**Regra**: No contexto de tags, uma regra é uma coleção de componentes que definem um conjunto específico de eventos, condições e ações que devem ser agrupados logicamente.

**Componente de regra**: No contexto de tags, os componentes da regra são os eventos, as condições e as ações que compõem uma regra.

**Tempo de execução**: O tempo de execução especifica um ambiente de tempo de execução para uma fórmula de aprendizado de máquina. [!DNL Python], R, [!DNL Spark]Os tempos de execução do , do PySpark e do Tensorflow permitem que você insira um URL para uma imagem do Docker de uma fonte de receita.

## S

**Dados de exemplo**: Dados de amostra são uma visualização de um arquivo de dados, normalmente as primeiras 100 linhas, que fornece a um cientista ou engenheiro de dados uma ideia de qual esquema ou dados está no arquivo de dados.

**Sandbox**: Uma sandbox é uma construção virtual que particiona uma única instância da Platform em um ambiente virtual separado, a fim de ajudar a desenvolver aplicativos de experiência digital.

**Redefinição de sandbox**: Uma redefinição de sandbox exclui todos os dados, incluindo dados, perfis e segmentos em uma sandbox. As redefinições de sandbox podem afetar dados conectados a destinos internos ou externos.

**Seletor de sandbox**: O controle do alternador de sandbox no Experience Platform permite que os usuários naveguem entre sandboxes às quais têm acesso. A alternância de uma sandbox mudará todo o conteúdo e poderá alterar o acesso a recursos com base em permissões.

**Agendar**: Um agendamento é uma especificação definida pelo usuário sobre a frequência ou a cadência da assimilação de dados de uma fonte de dados de terceiros para o Adobe Experience Platform.

**Pontuação**: A pontuação é o processo de geração de insights de dados usando um modelo treinado.

**Esquema**: Um esquema é um conjunto de regras que representam e validam a estrutura e o formato dos dados. Um esquema é composto por uma classe e grupos de campos opcionais e é usado para criar conjuntos de dados e conjuntos de dados. Um esquema pode incluir atributos comportamentais, carimbos de data e hora, identidades, definições de atributos, relacionamentos e muito mais.

**Grupo de campos Esquema**: No Experience Data Model (XDM), um grupo de campos de esquema permite que os usuários estendam campos reutilizáveis para definir um ou mais atributos destinados a serem incluídos em um esquema.

**Biblioteca de esquemas**: A Biblioteca de esquemas contém recursos XDM padrão do setor disponibilizados pelo Adobe, bem como recursos personalizados definidos pela organização.

**Registro de esquema**: O Registro de esquema fornece uma interface de usuário e a API RESTful usadas para exibir e gerenciar todos os recursos relacionados ao esquema na Biblioteca de esquemas.

**Chave de acesso secreta**: Uma chave de acesso secreta é uma [!DNL Amazon] Chave S3 usada em conjunto com a ID da chave de acesso para assinar solicitações do AWS.

**Segmento**: Um segmento é um conjunto de regras que inclui atributos e dados de evento que qualificam vários perfis para se tornarem um público-alvo.

**Construtor de segmentos**: O [!DNL Segment Builder] é um ambiente de desenvolvimento visual usado para criar definições de segmento. Ele serve como um componente comum de todos os aplicativos que usam o serviço de segmentação do Experience Platform.

**Definição de segmento**: Uma definição de segmento é o conjunto de regras usado para descrever as principais características ou o comportamento de um público-alvo. Depois de conceitualizadas, as regras descritas em uma definição de segmento são usadas para determinar membros de público-alvo qualificados para um segmento.

**Método de avaliação do segmento**: Há dois métodos de avaliação de segmento: programada e sob demanda. A avaliação programada permite uma programação recorrente para executar um trabalho de exportação em um horário específico, enquanto a avaliação sob demanda envolve a criação de um trabalho de segmento para criar o público-alvo imediatamente.

**Exportação de segmento**: A exportação de segmento é um dos dois tipos de destinos no Experience Platform. Com a exportação de segmentos, você pode enviar os perfis qualificados e que foram mapeados para o destino. Usa IDs de segmento e usuário e dados pseudônimos e normalmente integra-se às redes sociais e outras plataformas de destino de mídia digital.

**ID do segmento**: Uma ID de segmento é um identificador gerado automaticamente associado a um segmento.

**Associação de segmento**: A associação de segmento exibe quais segmentos um perfil faz parte atualmente.

**Regras de segmento**: As regras de segmento definem as condições que determinam se um perfil se qualifica para um segmento.

**Segmentação**: A segmentação é o processo de dividir um grande grupo de clientes, prospetos ou consumidores em grupos menores que compartilham atributos similares e responderão de forma semelhante a estratégias de marketing específicas.

**Sensei ML Framework**: O Sensei ML Framework é uma estrutura unificada de aprendizado de máquina (ML) que aproveita os dados de Experience Platform para capacitar os cientistas de dados para o desenvolvimento de serviços de inteligência orientados por ML de maneira mais rápida, escalável e reutilizável.

**Rótulos sensíveis (&quot;S&quot;)**: Os rótulos sensíveis (&quot;S&quot;) são usados para classificar dados considerados confidenciais, como diferentes tipos de dados comportamentais ou geográficos que você deseja marcar como confidenciais.

**Serviços**: Uma estrutura poderosa para operacionalizar serviços de IA e ML, aproveitando os serviços inteligentes do Adobe. Os serviços proporcionam experiências personalizadas do cliente em tempo real ou operam serviços inteligentes personalizados.

**Ação de marketing de personalização de identidade única**: Uma ação de marketing que usa dados para personalização de conteúdo no site. A personalização no site é qualquer dado usado para fazer inferências sobre os interesses dos usuários e é usado para selecionar qual conteúdo ou anúncios são exibidos com base nessas inferências.

**Rótulo de uso de dados S1**: Um `S1` o rótulo de uso de dados é usado para classificar dados que especificam latitude e longitude que podem ser usados para determinar a localização precisa de um dispositivo.

**Rótulo de uso de dados S2**: Um `S2` o rótulo de uso de dados é usado para classificar dados que podem ser usados para determinar uma área de geofence amplamente definida.

**Origem**: Uma fonte é um termo geral para qualquer conector de entrada na Platform. Consulte também: Conector de origem

**Atributo de origem**: Um atributo de origem é um campo no conjunto de dados de origem. Os atributos de origem são mapeados para campos de esquema de destino.

**Catálogo de origem**: O catálogo de origem é a lista de conectores de origem disponíveis no Experience Platform.

**Categoria de origem**: Uma categoria de origem é um agrupamento de fontes com características semelhantes.

**Conector de origem**: Os conectores de origem (também conhecidos como fontes) ajudam os usuários a assimilar facilmente dados de várias fontes, permitindo a estruturação, rotulagem e aprimoramento de dados usando serviços de Experience Platform. Os dados podem ser assimilados de várias fontes, como armazenamento baseado em nuvem, software de terceiros e sistemas CRM.

**Conexão de transmissão**: Uma conexão de transmissão é um terminal exclusivo fornecido pelo Adobe e vinculado à Organização IMS de um cliente para transmitir dados no Experience Platform.

**Namespace de identidade padrão**: Os namespaces de identidade padrão são namespaces de identidade predefinidos fornecidos pelo Adobe, que representam soluções padrão do setor, comumente usadas para identificar clientes.

**Assimilação de fluxo**: A assimilação de streaming permite enviar dados de dispositivos cliente e servidor para o Experience Platform em tempo real.

**Segmentação de streaming**: A segmentação de streaming é um processo contínuo de seleção de dados que atualiza os segmentos em resposta à atividade do usuário. Depois que um segmento é criado e salvo, a definição do segmento é aplicada aos dados de entrada para [!DNL Real-time Customer Profile]. Adições e remoções de segmentos são processadas regularmente, garantindo que o público-alvo permaneça relevante.

**Exibição do sistema**: Exibição do sistema é uma representação visual de conjuntos de dados de origem que fluem [!DNL Real-time Customer Profile] para destinos.

## T

**Tags**: No Adobe Experience Platform, as tags fornecem ferramentas para implantar, unificar e gerenciar integrações de análise, marketing e anúncios necessárias para potencializar experiências de cliente relevantes em todos os dispositivos clientes.

**Recursos do Target**: No mapeamento de recursos, um recurso de destino é o recurso previsto por um modelo.

**Dados da série cronológica**: Os dados das séries cronológicas fornecem um instantâneo do sistema no momento em que uma ação foi tomada direta ou indiretamente por um titular de um registro.

**Modelo treinado**: Um modelo treinado representa o resultado executável de um processo de treinamento modelo, no qual um conjunto de dados de treinamento foi aplicado à instância do modelo. Um modelo treinado manterá uma referência a qualquer Serviço Web Inteligente criado a partir dele. Um modelo treinado é adequado para pontuar e criar um serviço Web inteligente.

**Token**: Um token é um tipo de segurança de autenticação de dois fatores que pode ser usado para autorizar o uso de serviços de computador com [!DNL Query Service].

## U

**Schema da União**: Um schema de união é uma consolidação de schemas que compartilham a mesma classe e foram habilitados para [!DNL Real-time Customer Profile]. Vários esquemas de união podem existir para uma organização, mas só pode haver um esquema de união por classe.

## V

## W

## X

**XDM**: Consulte Experience Data Model (XDM).

**Evento de decisão XDM**: Evento de decisão XDM é uma classe baseada em séries de tempo usada para capturar observações sobre o resultado e o contexto de uma atividade de decisão. Isto inclui informações sobre como a decisão foi tomada, quando ocorreu, quais opções foram propostas (e escolhidas) e qual estado contextual existia que influenciou a decisão ou podia ser observado durante o processo de decisão.

**ExperiênciaEvento XDM**: O XDM ExperienceEvent é uma classe baseada em séries de tempo usada para capturar o estado do sistema quando um evento (ou conjunto de eventos) ocorreu, incluindo o ponto no tempo e a identidade do assunto envolvido. Consulte também: Evento de experiência

**Perfil individual XDM**: XDM [!DNL Individual Profile] é uma classe baseada em registros que forma uma representação singular dos atributos de indivíduos identificados e parcialmente identificados. Os perfis altamente identificados podem ser usados para comunicações pessoais ou participações direcionadas e podem conter informações pessoais detalhadas, como nome, gênero, data de nascimento, local e informações de contato, incluindo números de telefone e endereços de email.

**Sistema XDM**: O Sistema XDM representa a estrutura que opera esquemas XDM para uso em serviços Experience Platform downstream.

## Y

## Z
