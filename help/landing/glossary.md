---
keywords: Experience Platform;home;populares tópicos
solution: Experience Platform
title: Glossário do Adobe Experience Platform
topic: getting started
description: Um glossário de terminologia importante na Experience Platform.
translation-type: tm+mt
source-git-commit: 5575d5e45bddcc007dcf78720cd7a7e20475f78c
workflow-type: tm+mt
source-wordcount: '7139'
ht-degree: 1%

---


# Glossário da Adobe Experience Platform {#adobe-experience-platform-glossary}

## A

**Controle de acesso**: O controle de acesso baseado em funções permite que os administradores atribuam acesso e permissões aos usuários do Experience Platform. As permissões incluem a capacidade de visualização e/ou usar recursos de Experience Platform, como criar caixas de proteção, definir schemas e gerenciar conjuntos de dados.

**ID** da chave de acesso: Uma ID de chave de acesso é um identificador exclusivo associado a uma chave de acesso secreta  [!DNL Amazon] S3. A ID da chave de acesso e a chave de acesso secreta são usadas juntas para assinar [!DNL Amazon Web Services] (AWS) solicitações.

**Ação**: Em  [!DNL Platform Launch], uma ação é um tipo específico de componente de regra que define o que deve ocorrer depois que um evento ocorre e as condições são avaliadas e passadas.

**Ativar**: Ativar é a ação executada por um usuário para mapear um segmento ou perfis para um destino, como  [!DNL Oracle Eloqua],  [!DNL Google]ou  [!DNL Salesforce Marketing Cloud].

**Atividade**: Em  [!DNL Offer Decisioning], uma atividade contém a lógica que informa a seleção de uma oferta.

**Administrador**: Um ou mais indivíduos em sua organização que podem configurar e personalizar permissões para o Experience Platform no Adobe Admin Console.

**Adobe Admin Console**: A Adobe Admin Console fornece um local central para gerenciar os direitos e o acesso de produtos do Adobe para sua organização. Por meio do console, os administradores podem conceder a grupos de usuários permissões de acesso para vários recursos da plataforma, como &quot;Gerenciar conjuntos de dados&quot;, &quot;Conjuntos de dados de Visualização&quot; ou &quot;Gerenciar Perfis&quot;.

**Adobe Experience Platform**: A Adobe Experience Platform padroniza dados e conteúdo em toda a empresa, acionando perfis de consumidor em tempo real, permitindo a ciência de dados e acelerando a velocidade do conteúdo para impulsionar a personalização da experiência na jornada do cliente.

**Adobe Experience Platform Launch**:  [!DNL Platform Launch] é um ecossistema de gerenciamento de tags e SDK, integrado com Experience Platform e  [!DNL Experience Cloud] aplicativos. [!DNL Platform Launch] fornece ferramentas para implantar, unificar e gerenciar as integrações de análises, marketing e publicidade necessárias para potencializar as experiências relevantes do cliente em todos os dispositivos do cliente.

**Serviço** de Query Adobe Experience Platform: Permite que os analistas de dados façam eventos e perfis de query para uso em análise e aprendizado de máquina. Com o Serviço de Query, os cientistas e analistas de dados podem extrair todos os seus conjuntos de dados armazenados no Experience Platform (incluindo dados comportamentais, bem como POS (point-of-sale, ponto de venda), CRM (Customer Relationship Management, gerenciamento de relacionamento com o cliente) e muito mais) e query desses conjuntos de dados para responder a perguntas específicas sobre os dados.

**Serviço** de segmentação do Adobe Experience Platform: Permite a construção de segmentos e a geração de audiências a partir dos dados do Perfil do cliente em tempo real. Essas audiências podem ser exportadas para seus próprios conjuntos de dados no Data Lake.

**Serviços** inteligentes Adobe: Serviços inteligentes, como Attribution AI e IA do cliente, são modelos baseados em inteligência artificial, com aprendizado de máquina, criados especificamente e que exigem Experience Platform para funcionar e operar.

**Adobe I/O**: O Adobe I/O faz parte do Experience Platform e fornece acesso a tudo que os desenvolvedores precisam para integrar, estender e personalizar a Plataforma, incluindo APIs, eventos, console do desenvolvedor e ferramentas úteis.

**Adobe Sensei**: A Adobe Sensei é a estrutura de inteligência que alimenta o Experience Platform. Ele também fornece um conjunto de serviços de IA que capacita as marcas a melhorar sua capacidade de fornecer experiências personalizadas e em tempo real aos clientes.

**Bucket** Amazon S3:  [!DNL Amazon S3] os buckets são os container fundamentais para os dados armazenados no  [!DNL Amazon] ecossistema. Os buckets contêm objetos, cada objeto é armazenado e recuperado usando uma chave exclusiva atribuída ao desenvolvedor.

**Conector** Amazon S3: O conector  [!DNL Amazon] S3 permite que os clientes do Experience Platform conectem e acessem com segurança seus dados  [!DNL Amazon] S3.

**Anexar estratégia** de salvamento: A estratégia de salvamento &quot;acrescentar&quot; é uma opção usada ao especificar dados de terceiros para assimilar por meio de uma conexão e anexar quaisquer novos dados ou linhas ao final do conjunto de dados. As linhas ingeridas anteriormente permanecem intocadas e somente as linhas criadas desde a última execução programada são ingeridas no Experience Platform. Quaisquer linhas que foram alteradas no sistema de origem permanecem inalteradas no Experience Platform.

**Matriz**: As matrizes são usadas para elementos ordenados com o mesmo tipo de dados.

**Inteligência** artificial: A inteligência artificial é uma teoria e desenvolvimento de sistemas computacionais que são capazes de executar tarefas que normalmente exigem inteligência humana, como percepção visual, reconhecimento de voz, tomada de decisão e tradução entre línguas.

**Atributos**: Os atributos são características especificadas que representam um perfil.

**Mesclagem** de atributos: Ao definir uma política de mesclagem usando a API Perfil do cliente em tempo real, o  `attributeMerge` objeto indica a maneira pela qual a política de mesclagem priorizará os atributos do perfil em caso de conflitos de dados. É equivalente a selecionar um [!UICONTROL método de mesclagem] ao definir uma política de mesclagem na interface do usuário da plataforma.

**Attribution AI**:  [!DNL Attribution AI] é um Serviço Inteligente fornecido pela Adobe Sensei que oferece recursos algorítmicos de atribuição de vários canais durante todo o ciclo de vida do cliente.

**Audiência**: Uma audiência é o conjunto resultante de perfis que atendem aos critérios de uma definição de segmento.

**Tamanho** da audiência: Tamanho de audiência é o número total de perfis que atendem aos critérios de uma definição de segmento e se qualificam para associação de audiência.

**Instantâneo** da audiência: Um instantâneo de audiência captura todos os perfis que se qualificam para os critérios do segmento no momento da segmentação.

## B

**Preenchimento retroativo**: Para fontes programadas, a opção de preenchimento retroativo permite a ingestão de dados históricos.

**Período** de preenchimento retroativo: O período de preenchimento retroativo é uma opção para definir o tempo de assimilação de dados históricos de terceiros por meio de uma conexão de origem. Selecionar um período de preenchimento retroativo de &quot;para sempre&quot; assimilará todo o histórico dos dados de origem ao Experience Platform.

**Lote**: Um lote é um conjunto de dados coletados durante um período de tempo e processados juntos como uma única unidade. Os conjuntos de dados são compostos de vários lotes.

**ID** do lote: Uma ID de lote é um identificador gerado por Adobe para um lote de dados.

**Ingestão** em lote: A ingestão em lote permite assimilar dados em Experience Platform como arquivos em lote. Lotes são unidades de dados que consistem em um ou mais arquivos que serão assimilados como uma única unidade.

**Segmentação** em lote: A segmentação em lote é uma alternativa a um processo contínuo de seleção de dados e move todos os dados do perfil de uma só vez pelas definições de segmento para produzir audiências correspondentes. Depois de criado, esse segmento é salvo e armazenado para que possa ser exportado para uso.

**Criar**: Em  [!DNL Platform Launch], uma compilação é um arquivo ou conjunto de arquivos que contém todas as configurações e códigos necessários para executar a lógica comercial contida dentro de uma biblioteca, permitindo que você implante essa biblioteca no seu site ou aplicativo móvel.

**Ferramentas** de inteligência empresarial: As ferramentas de inteligência empresarial (BI) são principalmente integradas  [!DNL Experience Platform Query Service]. As ferramentas BI são tipos de software de aplicativos que coletam e processam grandes quantidades de dados não estruturados de sistemas internos e externos.

## C

**Limite**: Em  [!DNL Offer Decisioning], o limite máximo (também conhecido como limite de frequência) é usado em regras de decisão para definir quantas vezes uma oferta é apresentada. Há dois tipos de limites: quantas vezes uma oferta pode ser proposta em toda a audiência de público alvo combinada (chamada de &quot;Cap global&quot;) e quantas vezes uma oferta pode ser proposta ao mesmo usuário final (chamada de &quot;Cap de Perfil&quot;).

**Catálogo**: No contexto de fontes e destinos, um catálogo é uma galeria com conexões disponíveis para aplicativos de Adobe e tecnologias de terceiros. Não confundir com [!DNL Catalog Service].

**[!DNL Catalog Service]**:  [!DNL Catalog Service] (às vezes chamado  [!DNL Catalog]) é o sistema de registro para localização e linhagem de dados no Adobe Experience Platform. Enquanto todos os dados ingeridos no Experience Platform são armazenados no lago de dados como arquivos e diretórios, [!DNL Catalog] armazena os metadados e a descrição desses arquivos e diretórios para fins de pesquisa, monitoramento e controle de dados.

**Classe**: No Modelo de dados de experiência (XDM), uma classe define o menor conjunto de campos usado para criar um schema e define o comportamento básico do objeto comercial que o schema representa.

**Cliente**: Um cliente é uma ferramenta ou aplicativo externo que se conecta  [!DNL Query Service] via protocolo PostgreSQL ou API HTTP.

**Coleção**: Em  [!DNL Offer Decisioning], as coleções são subconjuntos de ofertas com base em condições predefinidas definidas definidas por um comerciante, como a categoria da oferta.

**Combine com a ação** de marketing PII: Uma ação de marketing que combina qualquer informação pessoalmente identificável (PII) com dados anônimos. Os contratos para dados provenientes de redes de anúncios, servidores de anúncios e provedores de dados de terceiros geralmente incluem proibições contratuais específicas sobre o uso desses dados com dados diretamente identificáveis.

**Interface** de linha de comando: Uma interface de linha de comando é uma ferramenta baseada em texto que pode ser usada para conexão  [!DNL Query Service] para execução de query bruto.

**Composição**: Uma composição é um agrupamento de componentes que se formam juntos para formar o schema.

**Condição**: Em  [!DNL Platform Launch], uma condição é um componente de regra que avalia uma declaração lógica que deve retornar  `true` ou  `false`. Todas as condições devem ser avaliadas como `true` e todas as condições de exceção devem ser avaliadas como `false` antes que qualquer ação na regra seja executada.

**Console**: No  [!DNL Query Service], o console fornece informações sobre o status e a operação de um query. O console exibe o status da conexão com [!DNL Query Service], as operações de query que estão sendo executadas e quaisquer mensagens de erro que resultem desses query.

**Rótulos** do contrato (&quot;C&quot;): As etiquetas de uso de dados do contrato (&quot;C&quot;) são usadas para categorizar dados que têm obrigações contratuais ou estão relacionados às políticas de controle de dados de um cliente.

**Rótulo** do contrato C1: Um rótulo de uso de dados de  `C1` contrato especifica que os dados só podem ser exportados da Adobe Experience Cloud em um formulário agregado sem incluir identificadores individuais ou de dispositivos. Por exemplo, dados que se originaram de redes sociais.

**Rótulo** do contrato C2: Um rótulo de uso de dados de  `C2` contrato especifica dados que não podem ser exportados para terceiros. Alguns fornecedores de dados têm termos nos seus contratos que proíbem a exportação de dados de onde foram originalmente recolhidos. Por exemplo, os contratos de redes sociais muitas vezes restringem a transferência de dados que você recebe deles. C2 é mais restritivo que C1, o que requer apenas agregação e dados anônimos.

**Rótulo** do contrato C3: Um rótulo de uso de dados de  `C3` contrato especifica dados que não podem ser combinados ou usados de outra forma com informações diretamente identificáveis. Alguns fornecedores de dados têm termos nos seus contratos que proíbem a combinação ou utilização desses dados com informações diretamente identificáveis. Por exemplo, os contratos para dados provenientes de redes de anúncios, servidores de anúncios e provedores de dados de terceiros geralmente incluem proibições contratuais específicas sobre o uso de dados diretamente identificáveis.

**Rótulo** do contrato C4: Um rótulo de uso de dados de  `C4` contrato especifica que os dados não podem ser usados para direcionar qualquer anúncio ou conteúdo, seja no site ou entre sites. C4 é o rótulo mais restritivo, pois abrange os rótulos C5, C6 e C7.

**Rótulo** do contrato C5: Um rótulo de uso de dados de  `C5` contrato especifica que os dados não podem ser usados para direcionamento entre sites de conteúdo ou anúncios baseados em interesses. A definição de metas ou personalização baseada em interesses ocorre se as três condições a seguir forem atendidas: Os dados recolhidos no local são utilizados para inferir o interesse do utilizador; é usado em outro contexto, como em outro site ou aplicativo; e é usado para selecionar qual conteúdo ou anúncios são veiculados com base nessas inferências.

**Rótulo** do contrato C6: Um rótulo de uso de dados de  `C6` contrato especifica que os dados não podem ser usados para direcionamento de anúncios no site. O direcionamento de anúncios no site inclui a seleção e o delivery de anúncios nos sites ou aplicativos de sua organização ou para medir o delivery e a eficácia desses anúncios. Isso inclui o uso de dados no site coletados anteriormente sobre o interesse dos usuários em selecionar anúncios, processar dados sobre o que os anúncios foram exibidos, quando e onde eles foram mostrados e se os usuários tomaram alguma ação relacionada ao anúncio, como selecionar um anúncio ou fazer uma compra.

**Rótulo** do contrato C7: Um rótulo de uso de dados de  `C7` contrato especifica que os dados não podem ser usados para direcionamento de conteúdo no site. A definição de metas de conteúdo no site inclui a seleção e o delivery de conteúdo nos sites ou aplicativos de sua organização ou para medir o delivery e a eficácia de tal conteúdo. Isso inclui informações coletadas anteriormente sobre o interesse dos usuários em selecionar o conteúdo, processar dados sobre qual conteúdo foi exibido, com que frequência ou por quanto tempo ele foi exibido, quando e onde ele foi exibido e se os usuários tomaram quaisquer ações relacionadas ao conteúdo, incluindo, por exemplo, a seleção de conteúdo.

**Rótulo** do contrato C8: Um rótulo de uso de dados de  `C8` contrato especifica que os dados não podem ser usados para medir os sites ou aplicativos de sua organização. Isso não inclui direcionamento baseado em interesses, que é a coleta de informações sobre o uso desse serviço para personalizar subsequentemente o conteúdo e/ou a publicidade em outros contextos.

**Rótulo** do contrato C9: Um rótulo de uso de dados de  `C9` contrato especifica que os dados não podem ser usados em workflows de ciência de dados. Alguns contratos incluem proibições explícitas sobre os dados utilizados para a ciência dos dados. Às vezes, são redigidos em termos que proíbem o uso de dados para inteligência artificial (AI), aprendizado de máquina (ML) ou modelagem.

**Rótulo** do contrato C10: Um rótulo de uso de dados de  `C10` contrato especifica que os dados não podem ser usados para ativação de identidade costurada. Algumas políticas de uso de dados restringem o uso de dados de identidade agrupados para personalização. O rótulo `C10` será aplicado automaticamente aos segmentos se suas políticas de mesclagem usarem a opção &quot;gráfico privado&quot;.

**Coluna** Data de criação: Selecionar uma coluna Data de criação é uma opção ao especificar dados de terceiros por meio de uma conexão de origem. Quando a estratégia de salvamento de anexo é selecionada e o schema de conjunto de dados contém vários campos de data, você deve escolher entre o schema disponível para especificar uma coluna chave Data de criação. A opção Data de criação não está disponível quando a estratégia de gravação de substituição está selecionada.

**Criar tabela como selecionar**: Criar tabela como seleção (CTAS) é um comando SQL que, quando executado como parte de um query SQL completo e válido, instrui  [!DNL Query Service] a persistir nos resultados do query em um conjunto de dados. Você pode criar um novo conjunto de resultados, substituir os resultados anteriores ou anexar aos resultados anteriores.

**Dados** entre sites: Os dados entre sites são a combinação de dados de vários sites, incluindo uma combinação de dados no site e fora dele ou uma combinação de dados de várias fontes fora do site.

**Ação** de marketing de direcionamento entre sites: Uma ação de marketing que usa dados para direcionamento de anúncios entre sites. A combinação de dados de vários sites, incluindo uma combinação de dados no local e dados fora do local ou uma combinação de dados de várias fontes fora do local, é chamada de dados entre sites. Os dados entre sites são normalmente coletados e processados para fazer inferências sobre os interesses dos clientes.

**Namespace** de identidade personalizada: Namespaces de identidade personalizadas podem ser criadas por sua organização para representar identidades para uma organização ou caso comercial específico.

**Rótulos** personalizados: Rótulos personalizados de uso de dados permitem que você crie e aplique rótulos específicos a campos de dados que atendam às necessidades específicas da empresa.

**AI** do cliente: A IA do cliente é um Serviço Inteligente fornecido pela Adobe Sensei que enriquece os perfis do cliente com propensões baseadas em IA e capacita os esforços de segmentação e segmentação do cliente.

## D

**Dicionário** de dados: Em  [!DNL Platform Launch], um dicionário de dados (também conhecido como mapa de dados) é um conjunto de elementos de dados definidos em uma propriedade.

**Elemento** de dados: Em  [!DNL Platform Launch], um elemento de dados é um ponteiro usado em regras e extensões para apontar para um dado específico que existe no dispositivo cliente.

**Inclusão** de dados: A ingestão de dados é o processo de adicionar dados de uma fonte para o Experience Platform. Os dados podem ser assimilados na Plataforma de várias maneiras, incluindo streaming, lotes ou adicionados por meio de conectores de origem.

**Camada** de dados: Em  [!DNL Platform Launch], uma camada de dados é uma estrutura de dados que existe no dispositivo cliente que contém metadados sobre o contexto em que uma página ou tela é visualizada.

**Governação** de dados: O controle de dados abrange as estratégias e tecnologias usadas para garantir que os dados estejam em conformidade com os regulamentos e as políticas organizacionais em relação ao uso de dados.

**Parceiros** de integração de dados: Os parceiros de integração de dados simplificam e automatizam o carregamento e a transformação de grandes volumes de dados de mais de 200 fontes para Experience Platform sem programação.

**Rótulos** do conjunto de dados: Os rótulos de uso de dados podem ser adicionados aos conjuntos de dados. Todos os campos nesse conjunto de dados herdarão os rótulos do conjunto de dados.

**Área de trabalho** da ciência de dados:  [!DNL Data Science Workspace] o Experience Platform permite que os clientes criem modelos de aprendizado por computador utilizando dados em aplicativos de plataforma e Adobe para criar segmentos inteligentes, gerar insights e fornecer previsões, permitindo que você aprimore consideravelmente as experiências digitais dos usuários finais.

**Fonte** de dados: Uma fonte de dados é uma origem de dados designada pelo usuário. Exemplos de uma fonte de dados são aplicativos móveis, eventos de perfil e/ou experiência, eventos de perfis de sites da Web ou um CRM.

**Gerente** de dados: Um administrador de dados é a pessoa responsável pelo gerenciamento, supervisão e aplicação efetiva dos ativos de dados de uma organização. Um administrador de dados também garante que as políticas de controle de dados sejam salvaguardadas e mantidas para serem compatíveis com os regulamentos governamentais e políticas organizacionais.

**Fluxo** de dados: Um fluxo de dados é um conjunto ou uma coleção de mensagens que compartilham o mesmo schema e são enviadas pela mesma fonte.

**Tipo** de dados: Um tipo de dados é um recurso XDM reutilizável que define um campo de tipo de objeto que contém várias propriedades em uma representação hierárquica.

**Rótulos** de uso de dados: As etiquetas de uso de dados permitem que você categorize dados que refletem considerações relacionadas à privacidade e condições contratuais para cumprir regulamentos e políticas corporativas. Os rótulos de uso de dados adicionados a um conjunto de dados são herdados ou aplicados a todos os campos nesse conjunto de dados. Os rótulos de uso de dados também podem ser aplicados diretamente aos campos.

**Fluxo de dados**: Um fluxo de dados é um pipeline virtual de dados que flui para a Plataforma de uma fonte e de uma saída para destinos.

**Execução** de fluxo de dados: Uma execução de fluxo de dados é um fluxo de dados que chega em Experience Platform com base em um agendamento especificado pelo usuário.

**Conjunto de dados**: Um conjunto de dados é um armazenamento e uma construção de gerenciamento para uma coleção de dados, geralmente uma tabela, que contém um schema (colunas) e campos (linhas).

**ID** do conjunto de dados: Um identificador gerado por Adobe para um conjunto de dados ingerido.

**Saída** do conjunto de dados: A saída do conjunto de dados fornece um mecanismo para determinar qual a opção &quot;Criar tabela como selecionada&quot; será usada para uma  [!DNL Query Service] execução específica.

**Coluna** delta: Uma coluna delta permite selecionar um campo de dados de origem para representar um carimbo de data e hora para a ingestão incremental.

**Estratégia** de salvamento delta: A estratégia de salvamento delta é uma opção para assimilar dados de terceiros por meio de uma conexão de origem. A opção permite que o usuário especifique se linhas novas ou alteradas de dados de origem são assimiladas ao Experience Platform. Novas linhas são adicionadas ao final do conjunto de dados e as linhas alteradas são atualizadas no conjunto de dados no Experience Platform.

**Descritor**: No Experience Data Model (XDM), um descritor é um conjunto adicional de metadados relacionados ao schema que descreve um comportamento específico para um campo. Os descritores podem ser usados pelo Experience Platform para entender o comportamento pretendido do schema, como a relação entre dois schemas.

**Destino**: Um destino é um termo geral para qualquer terminal, como um aplicativo de Adobe, plataforma de publicidade, serviço de armazenamento em nuvem ou serviço de marketing, onde uma audiência é ativada e fornecida.

**Categoria** de destino: Uma categoria de destino é um agrupamento de destinos com características semelhantes.

**Catálogo** de destino: Um catálogo de destino é uma lista de destinos disponíveis no Experience Platform.

**Regras** de chamada direta: Em  [!DNL Platform Launch], uma regra de chamada direta é uma regra que é executada quando é chamada diretamente da página, ignorando sistemas de detecção e pesquisa de eventos.

**Nome** de exibição: No Experience Data Model (XDM), um nome para exibição é um nome fácil de usar para um campo que é mostrado na interface do usuário.

## E

**Oferta** elegível: Uma oferta elegível pode ser consistentemente oferecida a um perfil, pois atende às restrições definidas acima.

**Regras de elegibilidade**: Em  [!DNL Offer Decisioning], as regras de elegibilidade são aplicadas a um perfil relacionado a restrições de calendário, agendamento e limite.

**Ação** de marketing de direcionamento de email: Uma ação de marketing que usa dados em campanhas de direcionamento de email.

**Código** incorporado: Em  [!DNL Platform Launch], o código incorporado é uma tag de script colocada dentro do HTML em um site ou ambiente. O código incorporado instrui o navegador para onde recuperar a compilação.

**Lista discriminada**: Uma lista discriminada (enum) é um campo XDM restrito a um conjunto de valores predefinidos.

**Ambiente**: Em  [!DNL Platform Launch], um ambiente é um conjunto de instruções de implantação que especifica o delivery host e o formato de arquivo de uma compilação. Uma biblioteca deve ser emparelhada a um ambiente antes de ser criada.

**Diagnóstico** de erro: O diagnóstico de erros permite a geração de mensagens de erro detalhadas para lotes ingeridos. O limite de erro permite que você configure a porcentagem de erros aceitáveis antes que um lote falhe.

**Evento**: Em  [!DNL Platform Launch], um evento é um tipo específico de componente de regra, que é um acionador que ocorre em um dispositivo cliente para iniciar a execução de uma regra.

**Entidades** eventos: No contexto da modelagem de dados, as entidades de evento representam conceitos relacionados às ações que um cliente pode realizar, eventos do sistema ou qualquer outro conceito em que você pode desejar rastrear as alterações ao longo do tempo. As entidades incluídas nesta categoria devem ser representadas por schemas baseados na classe [!DNL XDM ExperienceEvent].

**Eventos**: Eventos são os dados de comportamento associados a um perfil.

**O Experience Data Model (XDM)** [!DNL Experience Data Model] (XDM) é uma estrutura de código aberto que usa schemas padrão para unificar dados para uso com aplicativos Experience Platform e Adobe Experience Cloud. O XDM padroniza como os dados são estruturados e acelera e simplifica o processo de obtenção de insights de grandes quantidades de dados.

**Experimento**: Um experimento é o processo de criação de um modelo treinado por meio do treinamento da instância com uma amostra de dados de produção ao vivo. Isso é diferente de um modelo treinado que é testado contra um conjunto de dados de teste de retenção. Isso também é diferente do conceito de um experimento em algumas estruturas de aprendizado de máquina onde realmente significa um projeto de modelagem de amostra.

**Evento** da experiência: Um Evento da experiência representa um instantâneo do sistema quando ocorre uma interação ou evento relacionado à experiência do cliente. Os Eventos de experiência são registros imutáveis do que ocorreu e representam o que aconteceu sem agregação ou interpretação. No Experience Data Model (XDM), esse conceito é capturado pela classe [!DNL XDM ExperienceEvent].

**Extensão**: Em  [!DNL Platform Launch], uma extensão é um pacote de funcionalidade adicionado a uma  [!DNL Platform Launch] propriedade. Geralmente, uma extensão é focada em uma determinada solução de marketing ou análise e fornece as ferramentas necessárias para implantar essa tecnologia em um ambiente cliente.

**Pacote** de extensão: Em  [!DNL Platform Launch], um pacote de extensão é um arquivo ZIP criado e carregado por um desenvolvedor de extensão que fornece tudo o que é necessário para que  [!DNL Platform Launch] os usuários instalem a extensão dentro de sua propriedade. Um pacote de extensão contém um manifesto especificando informações sobre a extensão, o HTML/JavaScript necessário para que os usuários finais configurem o comportamento da extensão [!DNL Platform Launch] e o JavaScript executável entregue ao ambiente cliente (se necessário).

## F

**Ofertas** de fallback: Uma oferta de fallback é a oferta padrão exibida quando um usuário final não está qualificado para nenhuma das ofertas na coleção usada.

**Mapeamento** de recursos: O mapeamento de recursos refere-se ao processo de mapeamento de recursos de dados para recursos de entrada e público alvo exigidos por um modelo de aprendizado de máquina.

**Campo**: Um campo é o elemento de nível mais baixo de um conjunto de dados, conforme definido pelo schema XDM do conjunto de dados. Cada campo tem um nome para fins de referência e um tipo para indicar o tipo de dados que contém. Os tipos de campo podem incluir (mas não estão limitados a) inteiros, números, sequências de caracteres, booleanos e objetos.

**Rótulos** de campo: Rótulos de campo são rótulos de controle de dados herdados de um conjunto de dados ou aplicados diretamente a um campo.

**Nome** do campo: Um nome de campo é usado para fazer referência ao valor de um campo em query e serviços downstream.

**Frequência**: Em  [!DNL Query Service]geral, a frequência determina a frequência de execução de um query programado recorrente.

## G

**Geofence**: Uma geofence é um limite geográfico virtual, definido pela tecnologia GPS ou RFID, que permite que o software dispare uma resposta quando um dispositivo móvel entra ou sai de uma área específica.

**RGPD (Regulamento geral de proteção de dados)**: O Regulamento Geral sobre a Proteção de Dados (RGPD) é um quadro jurídico que estabelece orientações para a recolha e tratamento de informações pessoais de pessoas singulares no seio da União Europeia (UE). O RGPD estabelece os princípios da gestão de dados e dos direitos do indivíduo e abrange todas as empresas que tratam dos dados dos cidadãos da UE.

## H

**Host**: Em  [!DNL Platform Launch], um host especifica o local, o domínio e as credenciais do usuário necessários  [!DNL Platform Launch] para fornecer uma compilação.

## I

**Identidade**: Uma identidade é um identificador que representa exclusivamente um cliente individual, como uma ID de cookie, ID de dispositivo ou ID de email.

**Campos** de identidade: Campos de identidade são campos XDM usados para unir informações sobre clientes individuais provenientes de várias fontes de dados. Uma única identidade primária deve ser definida para que o schema seja habilitado para uso no Perfil do cliente em tempo real.

**Rótulos** de identidade (&quot;I&quot;): Rótulos de uso de dados de identidade (&quot;I&quot;) são usados para categorizar dados que podem identificar ou entrar em contato com uma pessoa específica.

**Gráfico** de identidade: Um gráfico de identidade é um mapa de relações entre identidades pontilhadas e ligadas que existem para um cliente individual. Cada gráfico de identidade é atualizado em tempo quase real com a atividade do cliente. A estrutura comum de relacionamentos de identidade em seus dados é representada pelo [!UICONTROL Gráfico privado], que serve como o modelo estrutural para cada gráfico de identidade individual.

**Namespace** de identidade: Uma namespace de identidade define o contexto de um identificador, como um endereço de email ou uma ID de CRM.

**Serviço** de identidade:  [!DNL Experience Platform Identity Service] permite a criação e o gerenciamento de tipos de identidade, permitindo que você vincule identidades de clientes entre dispositivos e canais. A capacidade do serviço de vincular identidades permite que o Perfil do cliente em tempo real forneça uma representação completa de cada cliente individual.

**Arranque** de identidade: A identificação é o processo de identificação de fragmentos de dados e a junção deles para formar um registro de perfil completo.

**Símbolo** de identidade: Um símbolo de identidade é a abreviação de uma namespace de identidade que pode ser usada como referência nas APIs.

**Valor** de identidade: Um valor de identidade, combinado com uma namespace de identidade, é um identificador que representa um indivíduo, organização ou ativo exclusivo. Ao corresponder dados de registro em fragmentos de perfil, a namespace e o valor de identidade devem corresponder.

**Rótulo** de uso de dados I1: O rótulo de uso de  `I1` dados é usado para classificar dados que podem identificar ou entrar em contato diretamente com uma pessoa específica em vez de um dispositivo.

**Rótulo** de uso de dados I2: O rótulo de uso de  `I2` dados é usado para classificar dados que podem ser usados em combinação com quaisquer outros dados para identificar ou entrar em contato indiretamente com uma pessoa específica.

**Organização** IMS: Uma Organização IMS (às vezes chamada de Organização IMS) é o nome usado para identificar uma empresa ou um grupo específico em uma empresa entre produtos Adobe. Os administradores podem configurar e gerenciar o acesso e as permissões dos recursos para os usuários de uma organização.

**Ingestão**: Consulte ingestão de dados.

**Esquema** de ingestão: Um agendamento de ingestão fornece opções baseadas em tempo ao assimilar de uma fonte para o Experience Platform.

**Recurso** de entrada: Um recurso de entrada é especificado no mapeamento de recursos e é usado por um modelo de aprendizado de máquina para fazer previsões.

**[!DNL Intelligent Services]**:  [!DNL Intelligent Services] como  [!DNL Attribution AI] e  [!DNL Customer AI] são modelos baseados em inteligência artificial, de aprendizado de máquina, que exigem Experience Platform (ou aplicativos criados sobre a plataforma, como a Plataforma de dados do cliente em tempo real) para serem executados e operados.

**Definição de metas ou personalização** com base em interesses: A definição de metas baseada em juros, também conhecida como personalização, ocorre se as três condições a seguir forem atendidas:

1. Os dados coletados no site são usados para fazer inferências sobre o interesse do usuário.
1. Os dados são usados em outro contexto, como em outro site ou aplicativo (fora do site).
1. Os dados são usados para selecionar qual conteúdo ou anúncios são veiculados com base nessas inferências.

## J

**[!DNL JupyterLab]**: Uma interface de código aberto, baseada na Web, para o Project  [!DNL Jupyter] que está integrada na interface do usuário da plataforma.

**[!DNL Jupyter Notebook]**: Integrados ao JupyterLab, Notebooks Jupyter permitem que você realize limpeza e transformação de dados, simulação numérica, modelagem estatística, visualização de dados, aprendizado de máquina e muito mais em seus dados de Experience Platform em vários idiomas, como Python, Scala e PySpark.

## K

## L

**Biblioteca**: Em  [!DNL Platform Launch], uma biblioteca é um conjunto de lógicas de negócios que contém instruções sobre como a  [!DNL Platform Launch] biblioteca deve se comportar no dispositivo cliente.

**Entidades** de pesquisa: No contexto da modelagem de dados, as entidades de pesquisa representam conceitos que podem se relacionar a uma pessoa individual, mas não podem ser usadas diretamente para identificar o indivíduo. As entidades abrangidas por esta categoria devem ser representadas por schemas com base em classes personalizadas do Experience Data Model (XDM).

## M

**Aprendizagem por máquinas (ML)**: O aprendizado de máquina é o campo de estudo que permite que os computadores aprendam sem serem explicitamente programados.

**Modelo** de aprendizado de máquina: Um modelo de aprendizado de máquina é uma instância de uma fórmula de aprendizado de máquina que é treinada usando dados históricos e configurações para resolver um caso de uso comercial. Na Adobe Experience Platform Data Science Workspace, os modelos de aprendizado por máquina são chamados de receitas.

**Mapeamento**: O mapeamento de dados é o processo de mapeamento de campos de dados de origem para campos de público alvo relacionados em um destino.

**Ação** de marketing: Na estrutura de gerenciamento de dados, uma ação de marketing (também conhecida como caso de uso de marketing) é uma ação que um consumidor de dados de Experience Platform, para a qual há necessidade de verificar violações das políticas de uso de dados.

**Método** de mesclagem: Ao definir uma política de mesclagem usando a interface do usuário da plataforma, o método de mesclagem especifica como os fragmentos de dados devem ser priorizados quando ocorrer um conflito. Ao usar a API Perfil do cliente em tempo real para definir uma política de mesclagem, o método de mesclagem é determinado usando o objeto `attributeMerge`.

**Política** de mesclagem: As políticas de mesclagem são regras que o Experience Platform usa para determinar como os fragmentos de dados do cliente de várias fontes serão combinados para criar um perfil individual. Quando ocorre um conflito de dados, a política de mesclagem determina quais dados devem ser priorizados para inclusão no perfil.

**Mistura**: No Experience Data Model (XDM), uma combinação permite que os usuários estendam campos reutilizáveis para definir um ou mais atributos destinados a serem incluídos em um schema.

**Módulo**: Em  [!DNL Platform Launch]geral, um módulo é um trecho do JavaScript executável fornecido por uma extensão, que executa ações em um ambiente cliente sem precisar criar uma regra.

## N

**Caixa de proteção** de não produção: As caixas de proteção de não-produção são caixas de proteção normalmente usadas para experimentos de desenvolvimento, testes ou testes. Diferentemente das caixas de proteção de produção, as caixas de proteção de não produção podem ser redefinidas e excluídas.

**[!DNL Notebooks]**:  [!DNL Notebooks] são criados usando  [!DNL Jupyter Notebook] e podem ser executados para executar a análise de dados.

## O

**Oferta**: Uma oferta é uma mensagem de marketing que contém uma proposta de negócio ou venda para um cliente (potencial). Muitas vezes, as ofertas têm regras específicas que determinam quem é elegível para vê-las ou recebê-las.

**[!DNL Offer Decisioning]**:  [!DNL Offer Decisioning] permite que os profissionais de marketing gerenciem regras e modelos treinados de apresentações da oferta ao se envolverem com usuários finais com base em dados coletados em canais e aplicativos.

**Biblioteca** de ofertas: A biblioteca de ofertas é uma biblioteca central usada para gerenciar ofertas personalizadas e de fallback, regras de decisão e atividades.

**Ação** de marketing de personalização no site: Uma ação de marketing que usa dados para personalização de conteúdo no site. A personalização no site é qualquer dado usado para fazer inferências sobre os interesses dos usuários e é usado para selecionar qual conteúdo ou anúncios são fornecidos com base nessas inferências.

**Ação** de marketing de direcionamento no site: Uma ação de marketing que usa dados para anúncios no site, incluindo a seleção e o delivery de anúncios nos sites ou aplicativos de sua organização, ou para medir o delivery e a eficácia de tais anúncios.

**Substituir estratégia** de salvamento: A estratégia de salvamento &quot;Substituir&quot; é uma opção para assimilar dados de terceiros por uma conexão, na qual você pode especificar se os dados ingeridos serão sobrescritos em uma programação especificada.

## P

**Ingestão** parcial: A ingestão parcial permite a ingestão de registros válidos de dados em lote dentro de um limite de erro especificado. O diagnóstico de erros para registros com falha pode ser baixado ou acessado em [!UICONTROL Monitoramento] ou [!UICONTROL Visão geral da execução do fluxo de dados de Fontes].

**Arquivos** de parâmetro: Um arquivo Parquet é um formato de arquivo de armazenamento columnar com estruturas de dados aninhadas complexas. Os arquivos de parâmetro são necessários para adicionar dados para preencher um conjunto de dados de schema.

**Ofertas** personalizadas: Uma oferta personalizada é uma mensagem de marketing personalizável baseada em regras de elegibilidade e restrições.

**Inserções**: uma inserção é o local e/ou contexto em que uma oferta é exibida para um usuário final.

**Área de trabalho** Políticas: Um espaço de trabalho na interface do usuário da plataforma que permite que os administradores de dados visualizações e gerenciem as etiquetas e políticas de uso de dados para sua organização.

**Política**: Uma política de uso de dados é uma regra que especifica ações de marketing restritas com base na aplicação de rótulos de uso aplicados aos dados da plataforma.

**Aplicação** de políticas: Permite que você aplique políticas de uso de dados com ações de marketing aplicadas para evitar operações de dados que constituam violações de política em uma organização.

**Chave** primária: Uma chave primária é uma designação em um schema para identificar exclusivamente todos os registros.

**Prioridade**: Em  [!DNL Offer Decisioning], a prioridade é usada para classificar ofertas que atendem a todas as restrições, como qualificação, calendário e limite.

**Gráfico** de identidade privada: O gráfico de identidade particular (às vezes chamado de gráfico privado) é um mapa privado de relações entre identidades pontilhadas e vinculadas, criado com base nos dados primários e visível somente pela sua organização. Existe apenas um gráfico privado para cada organização e serve como o modelo estrutural para os gráficos de identidade individuais gerados para cada cliente que interage com sua marca.

**Perfil** do produto: Os perfis de produtos permitem que os administradores concedam acesso de usuário a todos os serviços ou a um subconjunto de serviços associados ao Experience Platform.

**Caixa de proteção** de produção: Uma caixa de proteção de produção é uma caixa de proteção destinada ao uso no ambiente de produção. Diferentemente das caixas de proteção de não produção, as caixas de proteção de produção não podem ser redefinidas ou excluídas.

**Perfil**: Para não ser confundido com o Perfil do cliente em tempo real como um serviço, um perfil é uma representação completa de um cliente individual, construído a partir de dados de registro e série de tempo unidos de várias fontes.

**Acesso** ao perfil: O  `/entities` terminal na API Perfil do cliente em tempo real permite acessar os dados de registro e eventos de série de tempo no armazenamento de dados do Perfil. Consulte também: entidades perfis

**Dados** do perfil: Os dados do perfil se referem a quaisquer dados localizados no armazenamento de dados do Perfil.

**Armazenamento** de dados do perfil: O armazenamento de dados do Perfil (às vezes chamado de armazenamento do Perfil) é um sistema de armazenamento de dados separado do lago de dados, usado pelo Perfil Cliente em tempo real para criar e armazenar perfis.

**Entidades** perfis: As entidades do perfil representam atributos relacionados a uma pessoa individual, normalmente um cliente. As entidades incluídas nesta categoria devem ser representadas por schemas baseados na classe [!DNL XDM Individual Profile]. Consulte também: Acesso ao perfil

**Exportação** de perfis:  [!DNL Profile] a exportação é um dos dois tipos de destinos em Experience Platform. [!DNL Profile] o Export gera um arquivo contendo perfis e atributos, e usa dados PII brutos com e-mail para integrar-se às plataformas de marketing e automação de e-mail.

**Fragmento** do perfil: Um fragmento de perfil são as informações do perfil para apenas uma identidade fora da lista de identidades existentes para um determinado cliente.

**ID** do perfil: Uma ID de perfil é um identificador gerado automaticamente associado a um tipo de identidade e representa um perfil.

**Propriedade**: Em  [!DNL Platform Launch], uma propriedade é um container para tudo o que é necessário para implantar um conjunto de tags.

## Q

**Query**: Query são solicitações de dados de tabelas de banco de dados.

**Editor** de query: O Editor de query é uma ferramenta para gravar, validar e enviar instruções SQL em  [!DNL Query Service].

## R

**Plataforma** de dados do cliente em tempo real:  [!DNL Real-time Customer Data Platform] reúne dados conhecidos e desconhecidos do cliente para criar perfis confiáveis do cliente com integração simplificada, segmentação inteligente e ativação em tempo real na jornada do cliente digital.

**Perfil** do cliente em tempo real: O Perfil do cliente em tempo real (também chamado de Perfil) oferece uma visualização holística de cada cliente individual ao combinar dados de vários canais, inclusive on-line, off-line, CRM e de terceiros. O Perfil permite consolidar os dados do cliente em perfis individuais, oferecendo contas acionáveis e com carimbos de data e hora de cada interação com o cliente.

**Receita**: Uma receita é um termo para uma especificação de modelo e um container de nível superior que representa processos específicos de aprendizado da máquina, algoritmos AI, lógica de processamento e parâmetros de configuração necessários para criar e executar um modelo treinado e, portanto, ajudar a resolver problemas específicos da empresa.

**Registro**: Um registro são dados que persistem como linhas em um conjunto de dados.

**Registrar dados**: Fornece informações sobre os atributos de um assunto. Um sujeito pode ser uma organização ou um indivíduo.

**Recorrência**: Em  [!DNL Query Service], uma recorrência define se um query está programado para ser executado apenas uma vez ou de forma recorrente.

**Representação**: Em,  [!DNL Offer Decisioning]uma representação são informações usadas por um canal para exibir uma oferta, como local ou idioma.

**Recurso**: Em  [!DNL Platform Launch]geral, um recurso é um termo genérico que se refere às opções que o  [!DNL Platform Launch] usuário pode configurar dentro do ambiente cliente, incluindo extensões, elementos de dados e regras.

**Controle de acesso** baseado em função: O controle de acesso baseado em funções permite que os administradores atribuam acesso e permissões aos usuários do Experience Platform. As permissões incluem a capacidade de visualização e/ou usar recursos de Experience Platform, como criar caixas de proteção, definir schemas e gerenciar conjuntos de dados.

**Regra**: Em  [!DNL Platform Launch], uma regra é uma coleção de componentes que definem um conjunto específico de eventos, condições e ações que devem ser agrupados logicamente.

**Componente** da regra: Em  [!DNL Platform Launch], os componentes da regra são os eventos, as condições e as ações que compõem uma regra.

**Tempo de execução**: O tempo de execução especifica um ambiente de tempo de execução para uma fórmula de aprendizado de máquina. [!DNL Python], R,  [!DNL Spark], PySpark e Tensorflow permitem que você insira um URL em uma imagem do Docker para uma fonte de receita.

## S

**Dados** de amostra: Dados de amostra são uma pré-visualização de um arquivo de dados, normalmente as primeiras 100 linhas, que fornece a um cientista ou engenheiro de dados uma ideia de qual schema ou dados está no arquivo de dados.

**Caixa de proteção**: Uma caixa de proteção é uma construção virtual que divide uma única instância da Plataforma em um ambiente virtual separado, a fim de ajudar a desenvolver e desenvolver aplicativos de experiência digital.

**Redefinição** da caixa de proteção: Uma redefinição de caixa de proteção exclui todos os dados, incluindo dados, perfis e segmentos em uma caixa de proteção. As redefinições da caixa de proteção podem afetar os dados conectados a destinos internos ou externos.

**Alternador** Sandbox: O controle de alternador de sandbox no Experience Platform permite que os usuários naveguem entre caixas de proteção às quais têm acesso. Alternar uma caixa de proteção alterará todo o conteúdo e poderá alterar o acesso ao recurso com base em permissões.

**Agendamento**: Um agendamento é uma especificação definida pelo usuário sobre a frequência ou cadência da ingestão de dados de uma fonte de dados de terceiros para a Adobe Experience Platform.

**Pontuação**: A pontuação é o processo de gerar insights a partir de dados usando um modelo treinado.

**Schema**: Um schema é um conjunto de regras que representam e validam a estrutura e o formato dos dados. Um schema é composto de uma classe e combinações opcionais e é usado para criar conjuntos de dados e datastreams. Um schema pode incluir atributos comportamentais, carimbos de data e hora, identidades, definições de atributos, relacionamentos e muito mais.

**Biblioteca** de schemas: A Biblioteca de Schemas contém recursos XDM padrão do setor disponibilizados pelo Adobe, bem como recursos personalizados definidos pela sua organização.

**Registro** do schema: O Registro de Schemas fornece uma interface de usuário e uma RESTful API usada para visualização e gerenciamento de todos os recursos relacionados ao schema na Biblioteca de Schemas.

**Chave** de acesso secreta: Uma chave de acesso secreta é uma chave  [!DNL Amazon] S3 usada em conjunto com a ID da chave de acesso para assinar solicitações AWS.

**Segmento**: Um segmento é um conjunto de regras que incluem atributos e dados de evento que qualificam vários perfis para se tornarem audiências.

**Construtor** de segmentos: O  [!DNL Segment Builder] é um ambiente de desenvolvimento visual usado para criar definições de segmento. Ela serve como um componente comum de todos os aplicativos que usam o Serviço de segmentação de Experience Platform.

**Definição** do segmento: Uma definição de segmento é o conjunto de regras usado para descrever as principais características ou comportamento de uma audiência de público alvo. Depois de conceitualizadas, as regras descritas em uma definição de segmento são usadas para determinar os membros da audiência qualificados para um segmento.

**Método** de avaliação de segmentos: Existem dois métodos de avaliação de segmento: programado e sob demanda. A avaliação programada permite uma programação recorrente para executar uma tarefa de exportação em um horário específico, enquanto a avaliação sob demanda envolve a criação de uma tarefa de segmento para criar a audiência imediatamente.

**Exportação** de segmentos: A exportação de segmentos é um dos dois tipos de destinos no Experience Platform. Com a exportação de segmentos, você pode enviar os perfis que se qualificam e que foram mapeados para o destino. Usa IDs de segmento e usuário e dados pseudônimos e geralmente se integra às redes sociais e outras plataformas de público alvo de mídia digital.

**ID** do segmento: Uma ID de segmento é um identificador gerado automaticamente associado a um segmento.

**Associação** ao segmento: A associação de segmento exibe quais segmentos um perfil faz parte atualmente.

**Regras** do segmento: As regras de segmento definem as condições que determinam se um perfil se qualifica para um segmento.

**Segmentação**: A segmentação é o processo de dividir um grande grupo de clientes, prospectos ou consumidores em grupos menores que compartilham atributos semelhantes e responderão de forma semelhante a estratégias de marketing específicas.

**Sensei ML Framework**: O Sensei ML Framework é uma estrutura unificada de aprendizado de máquina (ML) que aproveita os dados de Experience Platform para capacitar os cientistas de dados para o desenvolvimento de serviços de inteligência orientados por ML de modo mais rápido, escalável e reutilizável.

**Rótulos** sensíveis: Rótulos (&quot;S&quot;) sensíveis são usados para categorizar dados considerados confidenciais, como tipos diferentes de dados comportamentais ou geográficos que você deseja marcar como confidenciais.

**Serviços**: Uma poderosa estrutura para operacionalizar serviços AI e ML, aproveitando os serviços inteligentes de Adobe. Os serviços fornecem experiências personalizadas e em tempo real do cliente ou operacionalizam serviços inteligentes personalizados.

**Ação** de marketing de personalização de identidade única: Uma ação de marketing que usa dados para personalização de conteúdo no site. A personalização no site é qualquer dado usado para fazer inferências sobre os interesses dos usuários e é usado para selecionar qual conteúdo ou anúncios são fornecidos com base nessas inferências.

**Rótulo** de uso de dados S1: Um rótulo de uso de  `S1` dados é usado para classificar dados que especificam latitude e longitude que podem ser usados para determinar a localização precisa de um dispositivo.

**Rótulo** de uso de dados S2: Um rótulo de uso de  `S2` dados é usado para classificar os dados que podem ser usados para determinar uma área de geofence definida de maneira ampla.

**Fonte**: Uma fonte é um termo geral para qualquer conector de entrada na Plataforma. Consulte também: Conector de origem

**Atributo** de origem: Um atributo de origem é um campo no conjunto de dados de origem. Os atributos de origem são mapeados para campos de schema de público alvo.

**Catálogo** de origem: O catálogo de origem é a lista dos conectores de origem disponíveis no Experience Platform.

**Categoria** de origem: Uma categoria de origem é um agrupamento de fontes com características semelhantes.

**Conector** de origem: Os conectores de origem (também conhecidos como fontes) ajudam os usuários a assimilar facilmente dados de várias fontes, permitindo a estruturação, a rotulagem e a melhoria de dados usando os serviços de Experience Platform. Os dados podem ser assimilados de várias fontes, como armazenamentos baseados em nuvem, software de terceiros e sistemas CRM.

**Conexão** de transmissão: Uma conexão de streaming é um terminal exclusivo fornecido pelo Adobe e vinculado à Organização IMS do cliente para transmitir dados em Experience Platform.

**Namespace** de identidade padrão: As namespaces de identidade padrão são namespaces de identidade pré-definidas fornecidas pela Adobe, que representam soluções padrão do setor, normalmente empregadas para identificar clientes.

**Inclusão** de transmissão: A ingestão de streaming permite enviar dados de dispositivos do cliente e do servidor para o Experience Platform em tempo real.

**Segmentação** de transmissão: A segmentação de transmissão é um processo contínuo de seleção de dados que atualiza os segmentos em resposta à atividade do usuário. Depois que um segmento é criado e salvo, a definição do segmento é aplicada em relação aos dados recebidos para [!DNL Real-time Customer Profile]. Adições e remoções do segmento são processadas regularmente, garantindo que sua audiência do público alvo permaneça relevante.

**Visualização** do sistema: A Visualização do sistema é uma representação visual de conjuntos de dados de origem que fluem  [!DNL Real-time Customer Profile] para destinos.

## T

**Recursos** do público alvo: No mapeamento de recursos, um recurso de público alvo é o recurso previsto por um modelo.

**Dados** da série cronológica: Os dados das séries cronológicas fornecem um instantâneo do sistema no momento em que uma ação foi tomada, direta ou indiretamente, por uma pessoa singular ou coletiva.

**Modelo** treinado: Um modelo treinado representa a saída executável de um processo de treinamento de modelo, no qual um conjunto de dados de treinamento foi aplicado à instância do modelo. Um modelo treinado manterá uma referência para qualquer Serviço Web Inteligente criado a partir dele. Um modelo treinado é adequado para pontuar e criar um serviço Web inteligente.

**Token**: Um token é um tipo de segurança de autenticação de dois fatores que pode ser usado para autorizar o uso de serviços de computador com  [!DNL Query Service].

## U

**Schema** de união: Um schema união é uma consolidação de schemas que compartilham a mesma classe e foram habilitados para  [!DNL Real-time Customer Profile]. Vários schemas de união podem existir para uma organização, mas só pode haver um schema de união por classe.

## V

## W

## X

**XDM**: Consulte Modelo de dados de experiência (XDM).

**Evento** de decisão XDM: O Evento XDM Decision é uma classe baseada em séries de tempo usada para capturar observações sobre o resultado e o contexto de uma atividade de decisão. Isto inclui informações sobre como a decisão foi tomada, quando ocorreu, quais opções foram propostas (e escolhidas) e que estado contextual existia que influenciou a decisão ou poderia ser observado durante o processo de decisão.

**ExperienceEvent** XDM: O XDM ExperienceEvent é uma classe baseada em série de tempo usada para capturar o estado do sistema quando um evento (ou conjunto de eventos) ocorreu, incluindo o ponto no tempo e a identidade do assunto envolvido. Consulte também: Evento da experiência

**Perfil** individual XDM: O XDM  [!DNL Individual Profile] é uma classe baseada em registros que forma uma representação singular dos atributos de indivíduos identificados e parcialmente identificados. Perfis altamente identificados podem ser usados para comunicações pessoais ou envolvimentos direcionados e podem conter informações pessoais detalhadas, como nome, gênero, data de nascimento, local e informações de contato, incluindo números de telefone e endereços de email.

**Sistema** XDM: O Sistema XDM representa a estrutura que opera schemas XDM para uso em serviços Experience Platform downstream.

## Y

## Z
