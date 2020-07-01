---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Documentação do produto Adobe Experience Platform
topic: getting started
translation-type: tm+mt
source-git-commit: 2e5668a8b1d5fb831188fbd4e453b9f4aa7474df
workflow-type: tm+mt
source-wordcount: '6594'
ht-degree: 0%

---


# Adobe Experience Platform Glossary {#adobe-experience-platform-glossary}

## A

**Controle de acesso:** {#access-control} Controle de acesso para [!DNL Experience Platform] links usuários com permissões de acesso e ambientes de caixa de proteção por meio de perfis de produtos no Adobe Admin Console.

**ID da chave de acesso:** A ID da chave de acesso é um identificador exclusivo associado a uma chave de acesso secreta do Amazon S3. A ID da chave de acesso e a chave de acesso secreta são usadas juntas para assinar solicitações AWS.

**Ação:** Em [!DNL Experience Platform Launch], uma ação é um tipo específico de componente de regra que define o que deve ocorrer depois que um evento ocorre e as condições são avaliadas e passadas.

**Ativar:** Em [!DNL Real-time Customer Data Platform], ativar é a ação executada por um usuário para mapear um segmento ou perfis para um destino como [!DNL Oracle Eloqua], [!DNL Google]ou [!DNL Salesforce Marketing Cloud].

**Atividade:** No [!DNL Decisioning Service], uma atividade é um conjunto de ofertas do qual o comerciante deseja que o mecanismo de decisão selecione a melhor oferta.

**Adobe Admin Console:** O Adobe Admin Console fornece um local central para gerenciar a permissão de acesso e recursos para sua organização.

**Adobe Experience Platform:** A Adobe Experience Platform padroniza dados e conteúdo em toda a empresa, acionando perfis de consumo em tempo real, permitindo a ciência de dados e acelerando a velocidade do conteúdo para impulsionar a personalização da experiência na jornada do cliente.

**Conectores da Adobe:** Os Conectores Adobe são conexões pré-configuradas criadas pela Adobe para permitir que os dados fluam para dentro e para fora [!DNL Experience Platform]. Os conectores incluem [!DNL Microsoft Dynamics], [!DNL Salesforce], [!DNL Amazon S3]e [!DNL Azure Blob].

**Serviços inteligentes da Adobe:** O Adobe Sensei é a estrutura de inteligência que é acionada [!DNL Experience Platform]. Ele também fornece um conjunto de serviços de IA que capacita as marcas a melhorar sua capacidade de fornecer experiências personalizadas e em tempo real aos clientes.

**E/S da Adobe:** A E/S da Adobe é parte do [!DNL Experience Platform] e fornece acesso a tudo o que os desenvolvedores precisam para integrar, estender e personalizar o Adobe Experience Platform, incluindo APIs, eventos, console do desenvolvedor e ferramentas úteis.

**Adobe Sensei:** O Adobe Sensei é a estrutura de inteligência que é acionada [!DNL Experience Platform]. Ele também fornece um conjunto de serviços de IA que capacita as marcas a melhorar sua capacidade de fornecer experiências personalizadas e em tempo real aos clientes.

**Balde Amazon S3:** [!DNL Amazon S3] os buckets são os container fundamentais para os dados armazenados no [!DNL Amazon] ecossistema. Os buckets contêm objetos, cada objeto é armazenado e recuperado usando uma chave exclusiva atribuída ao desenvolvedor.

**Conector Amazon S3:** [!DNL Amazon] O conector S3 permite que os clientes conectem e acessem [!DNL Experience Platform] com segurança seus dados [!DNL Amazon] S3.

**Anexar estratégia de gravação:** A estratégia de `Append` salvamento é uma opção usada ao especificar dados de terceiros para assimilar por meio de uma conexão e anexar quaisquer novos dados ou linhas ao final do conjunto de dados. As linhas ingeridas anteriormente permanecem intocadas e somente as linhas criadas desde a última execução programada são assimiladas [!DNL Experience Platform]. Todas as linhas que foram alteradas no sistema de origem permanecem inalteradas em [!DNL Experience Platform].

**Gerenciamento do ciclo de vida do aplicativo:** O gerenciamento do ciclo de vida do aplicativo permite criar ambientes virtuais separados para desenvolver e desenvolver aplicativos de experiência digital.

**Matriz:** As matrizes são usadas para elementos ordenados com o mesmo tipo de dados.

**Inteligência artificial:** A inteligência artificial é uma teoria e desenvolvimento de sistemas computacionais que são capazes de executar tarefas que normalmente exigem inteligência humana, como percepção visual, reconhecimento de voz, tomada de decisão e tradução entre línguas.

**Atributos:** Os atributos são características especificadas que representam um perfil.

**Mesclagem de atributos:** A mesclagem de atributos define como uma política de mesclagem prioriza o valor do atributo do perfil no caso de conflitos de dados.

**AI de atribuição:** [!DNL Attribution AI] é um serviço Adobe Sensei que oferece recursos algorítmicos de atribuição de vários canais durante todo o ciclo de vida do cliente.

**Audiência**: Uma audiência é o conjunto resultante de perfis que atendem aos critérios de uma definição de segmento.

**Instantâneo** da Audiência: Um instantâneo de audiência captura todos os perfis que se qualificam para os critérios do segmento no momento da segmentação.

[Voltar ao início](#adobe-experience-platform-glossary)

## B

**Preenchimento retroativo:** Em [!DNL Real-time Customer Data Platform]conexões de origem programadas, o preenchimento retroativo permite a ingestão de dados históricos.

**Período de preenchimento retroativo:** `Backfill period` é uma opção para definir o tempo necessário para assimilar dados históricos de terceiros por meio de uma conexão. Selecionar um período de preenchimento retroativo para sempre assimilará todo o histórico dos dados de origem ao [!DNL Experience Platform].

**Lote:** Lote é um conjunto de dados coletados durante um período de tempo e processados juntos como uma única unidade.

**ID do lote:** A ID do lote é um identificador gerado pela Adobe para um lote de dados.

**Ingestão em lote:** A ingestão em lote permite que os usuários ingeram petabytes de dados e os disponibilizem em sistemas corporativos. Com as tecnologias mais recentes, os usuários agora podem assimilar qualquer XDM e não-XDM do schema [!DNL Experience Platform].

**Segmentação em lote:** A segmentação em lote é uma alternativa a um processo contínuo de seleção de dados e move todos os dados do perfil de uma só vez pelas definições de segmento para produzir audiências correspondentes. Depois de criado, esse segmento é salvo e armazenado para que possa ser exportado para uso.

**Compilação:** Em [!DNL Experience Platform Launch], uma compilação é uma biblioteca implantada. A compilação é um arquivo ou conjunto de arquivos que contém todas as configurações e códigos necessários para executar a lógica comercial contida dentro dessa biblioteca.

**Ferramentas Business Intelligence:** A inteligência empresarial, também conhecida como ferramentas de &quot;BI&quot;, é integrada principalmente ao [!DNL Experience Platform Query Service]. As ferramentas BI são tipos de software de aplicativos que coletam e processam grandes quantidades de dados não estruturados de sistemas internos e externos.

[Voltar ao início](#adobe-experience-platform-glossary)

## C

**Limite:** No [!DNL Decisioning Service], o limite é usado nas regras de decisão para definir quantas vezes uma oferta é apresentada. Há dois tipos de tampas, quantas vezes uma oferta pode ser proposta através da audiência de público alvo combinada, também conhecida como &quot;Cap Global&quot;, e quantas vezes uma oferta pode ser proposta ao mesmo usuário final, também conhecida como &quot;Cap de Perfil&quot;.

**Catálogo:** Em [!DNL Real-time Customer Data Platform]fontes e destinos, um catálogo é uma galeria com conexões disponíveis para aplicativos da Adobe e tecnologias de terceiros.

**Classe:** Uma classe define o menor conjunto de campos usado para criar um schema e é o comportamento básico que descreve o objeto comercial.

**Cliente:** Um cliente é uma ferramenta externa ou um aplicativo que se conecta [!DNL Query Service] via protocolo de pôsteres ou API HTTP.

**Coleção:** No [!DNL Decisioning Service], as coleções são subconjuntos de ofertas com base em condições predefinidas definidas definidas por um comerciante, como a categoria da oferta.

**Interface de linha de comando:** Interface de linha de comando é uma ferramenta de linha de comando usada para conexão [!DNL Query Service] para execução de query bruto.

**Composição**: Uma composição é um agrupamento de componentes que se formam juntos para formar o schema.

**Conexão:** Uma conexão é um pipeline virtual que permite o fluxo de dados para entrada e saída [!DNL Experience Platform]. As conexões agora são substituídas por Fontes.

**Conector:** Os conectores de fonte de Adobe Experience Platform ajudam os usuários a ingerir facilmente dados de várias fontes, permitindo a estruturação, rotulagem e aprimoramento de dados usando [!DNL Experience Platform Services]. Os dados podem ser assimilados de várias fontes, como armazenamentos baseados em nuvem, software de terceiros e sistemas CRM.

**Condição:** No Experience Platform Launch, uma condição é um componente de regra que avalia uma declaração lógica que deve retornar `true` ou `false`. Todas as condições devem ser avaliadas `true` e todas as condições de exceção devem ser avaliadas `false` antes de qualquer ação na regra ser executada.

**Console:** No [!DNL Query Service], o console fornece informações sobre o status e a operação de um Query. O console exibe o status da conexão com [!DNL Query Service], as operações de query que estão sendo executadas e quaisquer mensagens de erro que resultem desses query.

**Rótulos &quot;C&quot; de Dados do Contrato:** As `C` etiquetas de contrato são usadas para categorizar dados que têm obrigações contratuais ou estão relacionados às políticas de controle de dados de um cliente.

**Rótulo do Contrato C1:** `C1` o rótulo de controle de dados do contrato especifica que os dados só podem ser exportados da Adobe Experience Cloud em um formulário agregado sem incluir identificadores individuais ou de dispositivos. Por exemplo, dados que se originaram de redes sociais.

**Rótulo do Contrato C2:** `C2` o rótulo de controle de dados do contrato especifica dados que não podem ser exportados para terceiros. Alguns fornecedores de dados têm termos nos seus contratos que proíbem a exportação de dados de onde foram originalmente recolhidos.  Por exemplo, os contratos de redes sociais muitas vezes restringem a transferência de dados que você recebe deles. C2 é mais restritivo que C1, o que requer apenas agregação e dados anônimos.

**Rótulo do Contrato C3:** `C3` o rótulo de controle de dados do contrato especifica dados que não podem ser combinados ou usados de outra forma com informações diretamente identificáveis. Alguns fornecedores de dados têm termos nos seus contratos que proíbem a combinação ou utilização desses dados com informações diretamente identificáveis.  Por exemplo, os contratos para dados provenientes de redes de anúncios, servidores de anúncios e provedores de dados de terceiros geralmente incluem proibições contratuais específicas sobre o uso de dados diretamente identificáveis.

**Rótulo do Contrato C4:** `C4` o rótulo de controle de dados do contrato especifica que os dados não podem ser usados para direcionar qualquer anúncio ou conteúdo, seja no site ou entre sites. C4 é o rótulo mais restritivo, pois abrange os rótulos C5, C6 e C7.

**Rótulo do Contrato C5:** `C5` o rótulo de controle de dados do contrato especifica que os dados não podem ser usados para direcionamento de conteúdo ou anúncios baseado em interesses entre sites. A definição de metas ou personalização baseada em interesses ocorre se as três condições a seguir forem atendidas:  Os dados coletados no site são usados para fazer inferências sobre o interesse de um usuário, são usados em outro contexto, como em outro site ou aplicativo, e são usados para selecionar qual conteúdo ou anúncios são fornecidos com base nessas inferências.

**Rótulo do Contrato C6:** `C6` o rótulo de controle de dados do contrato especifica que os dados não podem ser usados para direcionamento de anúncios no site. Os dados não podem ser usados para direcionamento de anúncios no site, incluindo a seleção e o delivery de anúncios nos sites ou aplicativos de sua organização, nem para medir o delivery e a eficácia desses anúncios.  Isso inclui o uso de dados no site coletados anteriormente sobre o interesse dos usuários em selecionar anúncios, processar dados sobre o que os anúncios foram exibidos, quando e onde eles foram mostrados e se os usuários tomaram alguma ação relacionada ao anúncio, como clicar em um anúncio ou fazer uma compra.

**Rótulo do Contrato C7:** `C7` o rótulo de controle de dados do contrato especifica que os dados não podem ser usados para direcionamento de conteúdo no site.  Os dados não podem ser usados para direcionamento de conteúdo no site, incluindo a seleção e o delivery de conteúdo nos sites ou aplicativos de sua organização, nem para medir o delivery e a eficácia de tal conteúdo.  Isso inclui informações coletadas anteriormente sobre o interesse dos usuários em selecionar conteúdo, processar dados sobre qual conteúdo foi exibido, com que frequência ou por quanto tempo ele foi exibido, quando e onde ele foi exibido e se os usuários tomaram quaisquer ações relacionadas ao conteúdo, incluindo, por exemplo, clicar no conteúdo.

**Rótulo do Contrato C8:** `C8` o rótulo de controle de dados do contrato especifica que os dados não podem ser usados para medir os sites ou aplicativos de sua organização. Os dados não podem ser usados para medir, entender e relatar sobre o uso pelos usuários dos sites ou aplicativos de sua organização. Isso não inclui direcionamento baseado em interesses, que é a coleta de informações sobre o uso desse serviço para personalizar subsequentemente o conteúdo e/ou a publicidade em outros contextos.

**Rótulo do Contrato C9:** `C9` o rótulo de controle de dados do contrato especifica que os dados não podem ser usados em workflows de Data Science. Alguns contratos incluem proibições explícitas sobre os dados utilizados para a ciência dos dados.  Às vezes, são redigidos em termos que proíbem o uso de dados para inteligência artificial (AI), aprendizado de máquina (ML) ou modelagem.

**Coluna Data de Criação:** Selecionar uma `Created Date` coluna é uma opção ao especificar dados de terceiros por meio de uma conexão. Quando a estratégia de salvamento de anexo é selecionada e o conjunto de dados contém um schema relacionado a várias datas, o usuário deve escolher entre o schema de data/hora disponível para especificar uma coluna `Created Date` chave. `Created Date` não está disponível quando a estratégia de gravação de substituição está selecionada.

**Criar tabela como selecionada:** Criar tabela como seleção é um comando SQL que, quando executado como parte de um query SQL completo e válido, instrui o [!DNL Query Service] para persistir os resultados do query em um conjunto de dados no Data Lake. As opções incluem: Criar novo, substituir todos os anteriores e anexar ao anterior.

**Dados entre sites:** Os dados entre sites são a combinação de dados de vários sites, incluindo uma combinação de dados no site e fora dele ou uma combinação de dados de várias fontes fora do site.

**Namespace de identidade personalizada:** namespaces de identidade personalizadas são identificadores criados pelo cliente usados para representar identidades para uma organização ou caso comercial específico.

**AI do cliente:** A IA do cliente é um serviço do Adobe Sensei que enriquece perfis de clientes com propensões baseadas em IA e capacita a segmentação e os esforços de definição de metas do cliente.

[Voltar ao início](#adobe-experience-platform-glossary)

## D

**Dicionário de dados:** Em [!DNL Experience Platform Launch], um dicionário de dados é um conjunto de elementos de dados definidos em uma propriedade.

**Elemento de dados:** Em [!DNL Experience Platform Launch], um elemento de dados é um ponteiro usado em regras e extensões para apontar para um dado específico que existe no dispositivo cliente.

**Camada de dados:** Em [!DNL Experience Platform Launch], uma camada de dados é uma estrutura de dados que existe no dispositivo cliente que contém metadados sobre o contexto em que uma página ou tela é visualizada.

**Mapeamento de dados:** O mapeamento de dados é o processo de mapeamento de campos de dados de origem para campos de público alvo relacionados ao destino.

**Fluxo de dados:** Um fluxo de dados é um conjunto ou uma coleção de mensagens que compartilham o mesmo schema e são enviadas pela mesma fonte.

**Controle de dados:** [!DNL Data governance] engloba as estratégias e tecnologias usadas para garantir que os dados estejam em conformidade com os regulamentos e as políticas da organização em relação ao uso dos dados.

**Rótulos de controle de dados:** [!DNL Data governance] as etiquetas fornecem aos usuários a capacidade de classificar dados que refletem considerações relacionadas à privacidade e condições contratuais para serem compatíveis com regulamentos e políticas corporativas. [!DNL Data governance] os rótulos adicionados a um conjunto de dados são herdados ou aplicados a todos os campos nesse conjunto de dados. [!DNL Data governance] os rótulos também podem ser aplicados diretamente aos campos.

**Parceiros de integração de dados:** Os parceiros de integração de dados simplificam e automatizam o carregamento e a transformação de grandes volumes de dados de mais de 200 fontes para [!DNL Experience Platform] sem programação.

**Rótulos do conjunto de dados:** Os rótulos de uso de dados podem ser adicionados aos conjuntos de dados. Todos os campos nesse conjunto de dados herdarão os rótulos do conjunto de dados.

**Área de trabalho da ciência de dados:** [!DNL Data Science Workspace] dentro [!DNL Experience Platform] permite que os clientes criem modelos de aprendizado de máquina utilizando dados em todos os aplicativos [!DNL Experience Platform] da Adobe e gerem insights e previsões inteligentes para tecer experiências digitais deliciosas para o usuário final.

**Fonte de dados:** Uma fonte de dados é uma origem de dados designada pelo usuário. Exemplos de uma fonte de dados são aplicativos móveis, eventos de perfil e/ou experiência, eventos de perfis de sites ou CRM.

**Data Stewer:** Um administrador de dados é a pessoa responsável pelo gerenciamento, supervisão e aplicação efetiva dos ativos de dados de uma organização. Um administrador de dados também garante que as políticas de controle de dados sejam salvaguardadas e mantidas para serem compatíveis com os regulamentos governamentais e as políticas de organização.

**Tipo de dados:** O tipo de dados é um objeto reutilizável com propriedades em uma representação hierárquica.

**Rótulos de uso de dados:** As etiquetas de uso de dados fornecem aos usuários a capacidade de categorizar dados que refletem considerações relacionadas à privacidade e condições contratuais para serem compatíveis com regulamentos e políticas corporativas.

**Fluxo de dados:** No [!DNL Real-time Customer Data Platform], um fluxo de dados é um pipeline virtual de dados que flui [!DNL Platform] de uma fonte para destinos.

**Conjunto de dados:** Um conjunto de dados é um armazenamento e uma construção de gerenciamento para uma coleção de dados, geralmente uma tabela, que contém schema (colunas) e campos (linhas).

**ID do conjunto de dados:** Um identificador gerado pela Adobe para um conjunto de dados assimilado.

**Saída do conjunto de dados:** A saída do conjunto de dados fornece um mecanismo para determinar qual a opção *Criar tabela como selecionada* será usada para uma [!DNL Query Service] execução específica.

**Evento de decisão:** Um evento de decisão é usado para capturar observações sobre o resultado e o contexto de uma atividade de decisão. O evento de decisão captura informações sobre como a decisão foi tomada, quando estava ocorrendo, quais opções foram propostas (escolhidas) e que estado contextual existia que influenciaram a decisão ou podiam ser observadas durante o processo de decisão. O evento de decisão também captura a ID da proposta, um identificador globalmente exclusivo que pode ser usado para correlacionar a decisão a outros eventos.

**Regra de decisão:** Na regra [!DNL Decisioning Service], uma regra de decisão é a lógica que define e controla o que, quando, onde e como uma oferta é apresentada aos usuários finais.

**Serviço de decisão:** A [!DNL Decisioning Service] é uma coleção de serviços e interface do usuário que permite aos comerciantes criar e fornecer experiências de oferta personalizadas para o usuário final em canais e aplicativos usando lógica de negócios e regras de decisão.

**Coluna Delta:** Em [!DNL Real-time Customer Data Platform], a coluna delta permite a seleção do campo de dados de origem para um carimbo de data e hora para ingestão incremental

**Estratégia de gravação Delta:** `Delta save strategy` é uma opção para assimilar dados de terceiros por meio de uma conexão. A opção permite que o usuário especifique se linhas novas ou alteradas de dados de origem são assimiladas [!DNL Experience Platform]. Novas linhas são adicionadas ao final do conjunto de dados e as linhas alteradas são atualizadas no conjunto de dados em [!DNL Experience Platform].

**Destino:** Em [!DNL Real-time Customer Data Platform] um destino é um termo geral para qualquer sistema, como um aplicativo da Adobe, servidor de anúncios ou rede de anúncios em que uma audiência é ativada e entregue.

**Categoria de destino:** Uma categoria de destino é um agrupamento de [!DNL Real-time Customer Data Platform] destinos com características semelhantes.

**Catálogo de destino:** Um catálogo de destino é uma lista de destinos disponíveis no [!DNL Real-time Customer Data Platform].

**Nome de exibição:** O nome de exibição é um nome amigável para o usuário de um campo que é mostrado na interface do usuário.

**MÓDULO:** DULE é um acrônimo para Rotulagem e Aplicação do Uso de *Dados*. DULE é uma parte essencial do gerenciamento de dados e uma coleção de recursos principais que permite a rotulagem de uso de dados e a aplicação de políticas de acesso a dados para necessidades de governança em uma organização.

[Voltar ao início](#adobe-experience-platform-glossary)

## E

**Diagnóstico de erro:** O diagnóstico de erros permite a geração de mensagens de erro detalhadas para lotes ingeridos. O limite Erro permite a configuração da porcentagem de erros aceitáveis antes que todo o lote falhe.

**Oferta elegível:** No [!DNL Decisioning Service], uma oferta elegível atende às restrições definidas em upstream que podem ser consistentemente oferecidas a um perfil.

**Regras qualificadas:** No [!DNL Decisioning Service], as regras de elegibilidade são aplicadas a um perfil relacionado a restrições de calendário, agendamento e limite.

**Código incorporado:** Em [!DNL Experience Platform Launch], o código incorporado é uma tag de script colocada dentro do HTML em um site ou ambiente. O código incorporado instrui o navegador para onde recuperar a compilação.

**Lista discriminada:** Uma enumeração é uma lista de valores que representam os dados válidos de um campo.

**Ambiente:** Em [!DNL Experience Platform Launch], um ambiente é um conjunto de instruções de implantação que especifica o delivery host e o formato de arquivo de uma compilação. Uma biblioteca deve ser emparelhada a um ambiente antes de ser criada.

**Evento** em [!DNL Experience Platform Launch], um evento é um tipo específico de componente de regra, um acionador que ocorre em um dispositivo cliente para iniciar a execução de uma regra.

**Eventos:** Eventos são os dados de comportamento associados a um perfil.

**Modelo de dados de experiência (XDM):** [!DNL Experience Data Model] (XDM) é o conceito de usar schemas padrão para unificar dados para uso com aplicativos [!DNL Experience Platform] e da Adobe Experience Cloud. O XDM padroniza como os dados são estruturados e acelera e simplifica o processo de obtenção de insights de grandes quantidades de dados.

**Experience Platform Launch:** [!DNL Launch] é um ecossistema de gerenciamento de tags e SDK, integrado com [!DNL Experience Platform] e [!DNL Experience Cloud] aplicativos. [!DNL Launch] fornece ferramentas para implantar, unificar e gerenciar as integrações de análises, marketing e publicidade necessárias para potencializar as experiências relevantes do cliente em todos os dispositivos do cliente.

**Extensões de Experience Platform Launch:** [!DNL Experience Platform Launch] as extensões permitem o delivery de dados brutos do evento diretamente para [!DNL Real-time Customer Data Platform] destinos. A instalação de [!DNL Launch] extensões requer acesso às [!DNL Launch] propriedades.

**Experimento:** Um experimento é um processo de criação de um modelo treinado por meio do treinamento da instância com uma porção de amostra dos dados de produção ao vivo.

**Experimentos:** Experimentos é o processo de aplicar um modelo treinado a uma pequena parte dos dados de produção ao vivo para validar seu desempenho. Isso é diferente de um modelo treinado que é testado contra um conjunto de dados de teste de retenção. Isto também é diferente do conceito de um Experimento em alguns enquadramentos do ML, onde realmente significa um projeto de modelagem de amostra.

**ExperienceEvent:** ExperienceEvent é um schema [!DNL Experience Platform] padrão que captura observações, incluindo o ponto no tempo e a identidade do assunto envolvido. Os Eventos de experiência são registros de fatos do que ocorreu, representando o que aconteceu sem agregação ou interpretação.

**Extensão:** Em [!DNL Experience Platform Launch], uma extensão é um pacote de funcionalidade adicionado a uma [!DNL Launch] propriedade.  Geralmente, uma extensão é focada em uma determinada solução de marketing ou análise e fornece as ferramentas necessárias para implantar essa tecnologia em um ambiente cliente.

**Pacote de extensão:** Em [!DNL Experience Platform Launch], um pacote de extensão é um arquivo .zip criado e carregado por um desenvolvedor de extensão que fornece tudo o que é necessário para que [!DNL Launch] os usuários instalem a extensão dentro de sua propriedade.  Um pacote de extensão contém um manifesto especificando informações sobre a extensão, o HTML e o JavaScript necessários para que os usuários finais configurem o comportamento da [!DNL Launch] extensão e o JavaScript executável entregue ao ambiente cliente, se necessário.

[Voltar ao início](#adobe-experience-platform-glossary)

## F

**Ofertas de fallback:** Na [!DNL Decisioning Service], uma oferta de fallback é a oferta padrão exibida quando um usuário final não está qualificado para nenhuma das ofertas na coleção usada.

**Mapeamento de recursos:** Mapeamento de recursos refere-se ao processo de mapeamento de recursos de dados para recursos de entrada e público alvo exigidos por um modelo de aprendizado de máquina.

**Campo:** Um campo é o elemento de nível mais baixo de um conjunto de dados. Cada campo tem um nome para referência e um tipo para identificar o tipo de dados que contém. Os tipos de campo podem incluir, número inteiro, número, string, booleano e schema.

**Rótulos de campo:** Rótulos de campo são rótulos de controle de dados herdados de um conjunto de dados ou aplicados diretamente a um campo.

**Nome do campo:** Campo é um nome usado para fazer referência ao campo em query e serviços.

**Frequência:** A frequência determina a frequência de execução de um [!DNL Query Service] query programado recorrente.

[Voltar ao início](#adobe-experience-platform-glossary)

## G

**Geofence:** Uma geofence é um limite geográfico virtual, definido pela tecnologia GPS ou RFID, que permite que o software dispare uma resposta quando um dispositivo móvel entra ou sai de uma área específica.

**RGPD:** O Regulamento Geral sobre a Proteção de Dados (RGPD) é um quadro jurídico que estabelece orientações para a recolha e tratamento de informações pessoais de pessoas singulares no seio da União Europeia (UE). O RGPD estabelece os princípios da gestão de dados e dos direitos do indivíduo e abrange todas as empresas que tratam dos dados dos cidadãos da UE.

**Rótulo de dados do RGPD:** A etiqueta de governança do RGPD é usada para definir os campos que podem conter identificadores pessoais para uso em solicitações de acesso e/ou exclusão do RGPD.

[Voltar ao início](#adobe-experience-platform-glossary)

## H

**Host:** Em [!DNL Experience Platform Launch], um host especifica o local, o domínio e as credenciais do usuário necessários para [!DNL Launch] fornecer uma compilação.

[Voltar ao início](#adobe-experience-platform-glossary)

## I

**Identidade:** Identidade é um identificador, como uma ID de cookie, uma ID de dispositivo ou uma ID de email que representa exclusivamente um cliente final.

**Rótulos de dados de identidade &quot;I&quot;:** `Identity I` as etiquetas são usadas para categorizar dados que podem identificar ou entrar em contato com uma pessoa específica.

**Gráfico de identidade:** O gráfico de identidade é um mapa de relações entre identidades pontilhadas e ligadas, que atualiza quase em tempo real com a atividade do cliente.

**Namespace de identidade:** Uma namespace de identidade é um identificador, como ID de cookie, ID de dispositivo ou ID de email, para indicar o contexto a partir do qual os dados são originados e são usados para reconhecer e vincular identidades em toda a [!DNL Experience Cloud].

**Serviço de identidade:** [!DNL Experience Platform Identity Service] A interface do usuário permite a criação e o gerenciamento de tipos de identidade para permitir a vinculação de identidades entre dispositivos e canais para uma visualização completa do usuário a partir de [!DNL Real-time Customer Profile].

**Configuração da identidade:** A identificação é o processo de identificação de fragmentos de dados e a junção deles para formar um registro completo de um perfil.

**Símbolo de identidade:** O símbolo de identidade é a abreviação de uma namespace de identidade que pode ser usada como referência nas APIs.

**Valor de identidade:** O valor de identificação é um dado associado a uma identidade atribuída no schema. Ao corresponder dados de registro em fragmentos de perfil, o valor de identidade e a namespace devem corresponder.

**Rótulo de dados I1:** O rótulo de `I1` dados é usado para classificar dados diretamente identificáveis que podem identificar ou entrar em contato com uma pessoa específica em vez de um dispositivo.

**Rótulo de dados I2:** O rótulo dos `I2` dados é usado para classificar dados indiretamente identificáveis que podem ser usados em combinação com quaisquer outros dados para identificar ou entrar em contato com uma pessoa específica.

**Ingest:** A ingestão é o processo de adicionar dados de uma fonte para [!DNL Experience Platform]. Os dados podem ser assimilados de várias [!DNL Experience Platform] formas, incluindo transmissão em fluxo, armazenamento em lote ou adição via conector.

**Agendamento de ingestão:** O agendamento de ingestão fornece opções baseadas em tempo ao assimilar de uma fonte para [!DNL Experience Platform].

**Recurso de entrada:** O recurso de entrada é especificado no mapeamento de recursos e é usado por um modelo de aprendizado de máquina para fazer previsões.

**Serviços inteligentes:** [!DNL Intelligent Services] como [!DNL Attribution AI] e [!DNL Customer AI] são aprendizado de máquina, modelos baseados em inteligência artificial que exigem que [!DNL Experience Platform] o usuário opere.

**Definição de metas ou personalização com base em interesses:** A definição de metas baseada em juros, também conhecida como personalização, ocorre se as três condições a seguir forem atendidas: os dados coletados no site são usados para fazer inferências sobre o interesse de um usuário, os dados são usados em outro contexto, como em outro site ou aplicativo (fora do site), e se os dados são usados para selecionar qual conteúdo ou anúncios são veiculados com base nessas inferências.

[Voltar ao início](#adobe-experience-platform-glossary)

## J

**[!DNL JupyterLab]:**Uma interface baseada na Web de código aberto para o Project[!DNL Jupyter]e é totalmente integrada ao[!DNL Experience Platform].

**[!DNL Jupyter Notebook]:**Um aplicativo da Web de código aberto que permite que os usuários criem e compartilhem documentos que contêm código ativo, equações, visualizações e texto narrativo.

## K

[Voltar ao início](#adobe-experience-platform-glossary)

## L

**Biblioteca:** Em [!DNL Experience Platform Launch], uma biblioteca é um conjunto de lógicas de negócios que contém instruções sobre como a [!DNL Launch] biblioteca deve se comportar no dispositivo cliente.

[Voltar ao início](#adobe-experience-platform-glossary)

## M

**Aprendizagem de Máquinas (ML):** O aprendizado de máquina é o campo de estudo que permite aos computadores aprenderem sem serem explicitamente programados.

**Modelo de aprendizado de máquina:** Um modelo de aprendizado de máquina é uma instância de uma fórmula de aprendizado de máquina que é treinada usando dados históricos e configurações para resolver um caso de uso comercial. Na Adobe [!DNL Data Science Workspace], os modelos de aprendizado de máquina são chamados de receitas.

**Mapeamento:** Em [!DNL Real-time Customer Data Platform], o mapeamento de dados é o processo de mapeamento dos campos de dados de origem para campos de público alvo relacionados ao destino.

**Ação de marketing:** Uma ação de marketing, no contexto da estrutura de gerenciamento de dados, é uma ação que um consumidor de [!DNL Experience Platform] dados toma, para a qual há necessidade de verificar violações das políticas de uso de dados.

**Método de mesclagem:** Uma `merge method` é uma opção de política de mesclagem que permite a priorização da mesclagem de fragmentos de dados. As opções do método de mesclagem são mescladas por precedência do conjunto de dados ou por carimbo de data e hora do conjunto de dados.

**Política de Mesclagem:** Uma política de mesclagem é um conjunto de regras usadas [!DNL Profile] para determinar como os dados serão priorizados e combinados em uma visualização unificada em determinadas condições.

**Mistura:** Uma combinação permite que os usuários estendam campos reutilizáveis que contêm variáveis que definem um ou mais atributos destinados a serem incluídos em um schema ou adicionados a uma classe.

**Coluna Data Modificada:** Selecionar uma `Modified Date` coluna é uma opção ao especificar dados de terceiros por meio de uma conexão. Quando a estratégia de `Delta` salvamento é selecionada e o conjunto de dados contém vários schemas relacionados à data, o usuário deve escolher entre o schema do tipo de data/hora disponível para especificar a coluna da chave de data modificada. `Modified Date` não está disponível quando a estratégia de `Overwrite` salvamento é selecionada.

**Módulo:** Em [!DNL Experience Platform Launch]geral, um módulo é um trecho do JavaScript executável fornecido por uma extensão, que executa ações em um ambiente cliente sem a necessidade do [!DNL Launch] usuário criar uma regra.

[Voltar ao início](#adobe-experience-platform-glossary)

## N

**Caixa de proteção de não produção:** As caixas de proteção de não produção são uma forma de virtualização de dados que permite isolar dados de outras caixas de proteção e são normalmente usadas para experimentos de desenvolvimento, testes ou testes. As caixas de proteção de não produção podem ser redefinidas e excluídas.

**[!DNL Notebooks]:**[!DNL Notebooks]são criados usando *[!DNL Jupyter Notebook]*e contêm descrição de análise, resultados e podem ser executados para executar a análise de dados.

[Voltar ao início](#adobe-experience-platform-glossary)

## O

**Oferta:** No [!DNL Decisioning Service], uma oferta é uma mensagem de marketing que pode ter regras associadas a ela que especificam quem está qualificado para ver a oferta.

**Decisão de Oferta:** Na decisão [!DNL Decisioning Service], a oferta permite que um profissional de marketing gerencie as regras e modelos treinados de apresentações da oferta ao se envolver com um usuário final com base em dados coletados em canais e aplicativos.

**Biblioteca de Ofertas:** Na biblioteca de ofertas [!DNL Decisioning Service], ela é uma biblioteca central usada para gerenciar ofertas personalizadas e de fallback, regras de decisão e atividades.

**Organização:** Uma organização é o nome usado para identificar uma empresa ou um grupo específico em uma empresa nos produtos da Adobe. O administrador pode configurar e gerenciar o acesso e as permissões dos recursos para os usuários de uma organização.

**Substituir estratégia de gravação:** `Overwrite` a estratégia de salvamento é uma opção para assimilar dados de terceiros por meio de uma conexão, na qual o usuário especifica se os dados ingeridos serão sobrescritos em um agendamento especificado. [!DNL Experience Platform] assimilará o conjunto de dados especificado da fonte de terceiros e substituirá o conjunto de dados em [!DNL Experience Platform].

[Voltar ao início](#adobe-experience-platform-glossary)

## P

**Ingestão parcial:** A ingestão parcial permite a ingestão de registros válidos de dados em lote dentro de um limite de erro especificado. O diagnóstico de erros para registros com falha pode ser baixado ou acessado no Monitoramento.

**Arquivos do Parquet:** Um arquivo parquet é um formato de arquivo de armazenamento columnar com estruturas de dados aninhadas complexas. Os arquivos de parâmetro são necessários para adicionar dados para preencher um conjunto de dados de schema.

**Ofertas personalizadas:** No [!DNL Decisioning Service], uma oferta personalizada é uma mensagem de marketing personalizável baseada em regras de elegibilidade e restrições.

**Disposições:** No [!DNL Decisioning Service], uma disposição é o local e/ou contexto em que uma oferta é exibida para um usuário final.

**Política:** Uma política de uso de dados é uma regra que especifica ações de marketing que são restritas com base na aplicação de rótulos de uso de dados nos dados em [!DNL Experience Platform].

**Chave primária:** A chave primária é uma designação em um schema para identificar exclusivamente todos os registros.

**Prioridade:** No [!DNL Decisioning Service], a prioridade é usada para classificar ofertas que atendem a todas as restrições, como qualificação, calendário e limite.

**Gráfico de identidade particular:** O Gráfico de identidade privada é um mapa privado de relacionamentos entre identidades pontilhadas e vinculadas, que é visível somente pela sua organização e construído com base nos seus dados primários.

**Perfil do produto:** Os perfis de produtos permitem que os administradores concedam acesso de usuário a todos os serviços associados ou a um subconjunto deles [!DNL Experience Platform].

**Área de segurança da produção:** Uma caixa de proteção de produção de dados virtuais isolados no Platform que não pode ser redefinida ou excluída.

**Perfil:** [!DNL Profile] é um modelo de dados [!DNL Experience Platform] normalizado utilizado para definir os atributos dos consumidores. Um perfil também pode ser uma agregação de dados e atributos do evento relacionados a uma pessoa e/ou dispositivo.

**Exportação de Perfil:** [!DNL Profile] a exportação é um dos dois tipos de destinos em [!DNL Real-time Customer Data Platform]. [!DNL Profile] o Export gera um arquivo contendo perfis e atributos, e usa dados PII brutos com e-mail e é usado para integração com plataformas de marketing e automação de e-mail.

**Fragmento do Perfil FProfile:** Um fragmento de perfil são as informações do perfil para apenas uma identidade da lista de identidades que existem para um usuário específico.

**ID do Perfil:** Uma ID de perfil é um identificador gerado automaticamente associado a um tipo de identidade e representa um perfil.

**Propriedade:** Em [!DNL Experience Platform Launch], uma propriedade é um container para tudo o que é necessário para implantar um conjunto de tags.

[Voltar ao início](#adobe-experience-platform-glossary)

## Q

**Query:** Um query é uma solicitação de dados de tabelas de banco de dados.

**Editor de Query:** O Editor de Query é uma ferramenta para gravar, validar e enviar instruções SQL em [!DNL Query Service].

**Serviço de Query para Adobe Experience Platform:** *[!DNL Experience Platform Query Service]* permite que analistas de dados query [!DNL ExperienceEvents] e XDMs para uso em análise e aprendizado de máquina. Com [!DNL Query Service]o, os cientistas e analistas de dados poderão obter todos os seus conjuntos de dados armazenados [!DNL Experience Platform] - incluindo dados comportamentais, assim como POS (point-of-sale, ponto de venda), CRM (Customer Relationship Management, gerenciamento de relacionamento com o cliente) e muito mais - e query desses conjuntos de dados para responder a perguntas específicas sobre os dados.

[Voltar ao início](#adobe-experience-platform-glossary)

## R

**Dados do cliente em tempo real Platform:** A Adobe [!DNL Real-time Customer Data Platform] reúne dados conhecidos e desconhecidos do cliente para criar perfis confiáveis do cliente com integração simplificada, segmentação inteligente e ativação em tempo real na jornada do cliente digital.

**Perfil do cliente em tempo real:** [!DNL Real-time Customer Profile] é um perfil centralizado para gerenciamento de experiência direcionado e personalizado.

**Receita:** Uma fórmula é o termo da Adobe para uma especificação de modelo e é um container de nível superior que representa um aprendizado de máquina específico, algoritmo AI ou conjunto de algoritmos, lógica de processamento e configuração necessários para criar e executar um modelo treinado e, portanto, ajudar a resolver problemas específicos de negócios.

**Registro:** Um registro são dados que persistem como linhas em um conjunto de dados.

**Recorrência:** Uma recorrência define se um [!DNL Query Service] query está programado para ser executado apenas uma vez ou de forma recorrente.

**Representação:** No [!DNL Decisioning Service], uma representação é informação usada por um canal, como localização ou idioma para exibir uma oferta.

**Recurso:** Em [!DNL Experience Platform Launch]geral, o recurso é um termo genérico que se refere às opções que o [!DNL Launch] usuário pode configurar dentro do ambiente cliente, incluindo extensões, elementos de dados e regras.

**Controle de acesso baseado em função:** O controle de acesso baseado em função permite que os administradores atribuam acesso e permissões aos usuários do [!DNL Experience Platform]. As permissões incluem a capacidade de visualização e/ou uso de [!DNL Experience Platform] recursos, como criação de caixas de proteção, definição de schemas e gerenciamento de conjuntos de dados.

**Regra:** Em [!DNL Experience Platform Launch], uma regra é uma coleção de componentes de regra que definem um conjunto específico de eventos, condições e ações que devem ser agrupados logicamente.

**Componente de regra:** Em [!DNL Experience Platform Launch], os componentes da regra são os eventos, as condições e as ações que compõem uma regra.

**Tempo de execução:** O tempo de execução especifica um ambiente de tempo de execução para uma fórmula de aprendizado de máquina. [!DNL Python], R, [!DNL Spark], PySpark e Tensorflow permitem a entrada de um URL para uma imagem mais âncora para uma fonte de receita.

[Voltar ao início](#adobe-experience-platform-glossary)

## S

**Dados de amostra:** Dados de amostra são uma pré-visualização de um arquivo de dados, normalmente as primeiras 100 linhas, para fornecer a um cientista ou engenheiro de dados uma ideia de qual schema ou dados está no arquivo de dados.

**Caixa de proteção:** Uma caixa de proteção é uma forma de isolar dados virtuais em uma organização de usuários [!DNL Experience Platform].

**Redefinição da caixa de proteção:** A caixa de proteção redefine, exclui todos os dados, incluindo dados, perfis e segmentos em uma caixa de proteção. A redefinição da caixa de proteção pode afetar os dados conectados a destinos internos ou externos.

**Comutador Sandbox:** O controle de alternador de sandbox em [!DNL Experience Platform] permite que os usuários naveguem entre caixas de proteção às quais têm acesso. Alternar uma caixa de proteção alterará todo o conteúdo e poderá alterar o acesso ao recurso com base em permissões.

**Agendamento:** Agendamento é uma especificação definida pelo usuário sobre a frequência ou cadência da ingestão de dados de uma fonte de dados de terceiros para a Adobe [!DNL Experience Platform].

**Pontuação:** A pontuação é o processo de gerar insights a partir de dados usando um modelo treinado.

**Schema:** O Schema é composto de uma combinação de classe e opcional e é usado para criar conjuntos de dados e fluxos de dados. Um schema inclui atributos comportamentais, carimbo de data e hora, identidade, definições de atributos e relacionamentos.

**Descritor do Schema:** O descritor do Schema é um metadados adicionais relacionados ao schema que descrevem o comportamento que pode ser usado [!DNL Experience Platform] para entender o comportamento pretendido do schema, como a relação entre dois schemas.

**Chave de acesso secreta:** Uma chave de acesso secreta é uma chave [!DNL Amazon] S3 usada em conjunto com a ID da chave de acesso para assinar solicitações AWS.

**Segmento:** Um segmento é um conjunto de regras que incluem atributos e dados de evento que qualificam vários perfis para se tornarem audiências.

**Construtor de segmentos:** [!DNL Segment Builder] é o ambiente de desenvolvimento visual usado para criar definições de segmentos e serve como um componente comum de todos os aplicativos que usam a [!DNL Real-time Customer Profile] Segmentação em [!DNL Experience Platform].

**Definição do segmento:** A definição de segmento é o conjunto de regras usado para descrever as principais características ou comportamento de uma audiência de público alvo. Depois de conceitualizadas, as regras descritas em uma definição de segmento são usadas para determinar os membros da audiência qualificados para um segmento.

**Método de avaliação de segmento:** A avaliação programada do segmento permite uma programação recorrente para executar uma tarefa de exportação em um horário específico, enquanto a avaliação sob demanda envolve a criação de uma tarefa de segmento para criar a audiência imediatamente.

**Exportação de segmento:** A exportação do segmento é um dos dois tipos de destinos e envia os perfis que se qualificam e foram mapeados para o destino. Usa IDs de segmento e usuário e dados pseudônimos e geralmente se integra às redes sociais e outras plataformas de público alvo de mídia digital.

**ID do segmento:** A ID do segmento é um identificador gerado automaticamente associado a um segmento.

**Associação ao segmento:** A associação de segmento exibe qual segmento um perfil faz parte atualmente.

**Regras de segmento:** As regras de segmento são onde e como o usuário define o que os perfis se qualificam para o segmento.

**Tipo de segmento:** Há dois tipos de segmentos: Um é um segmento que é atualizado dinamicamente com alterações de [!DNL Experience Platform] dados, e o outro é um instantâneo de audiência que captura todas as regras de segmentos de reunião de perfis, e elas não são alteradas.

**Segmentação:** A segmentação é o processo de dividir um grande grupo de clientes, prospectos ou consumidores em grupos menores que compartilham atributos semelhantes e responderão de forma semelhante às estratégias de marketing.

**Sensei ML Framework:** O Sensei ML Framework é uma estrutura unificada de aprendizado de máquina em toda a Adobe que aproveita os dados [!DNL Experience Platform] para capacitar os cientistas de dados no desenvolvimento de serviços de inteligência orientados por aprendizado de máquina de uma maneira mais rápida, escalável e reutilizável.

**Rótulos de dados confidenciais:** Os rótulos &quot;S&quot; sensíveis são usados para categorizar dados considerados confidenciais, como tipos diferentes de dados comportamentais ou geográficos que você deseja marcar como confidenciais.

**Serviços:** Uma poderosa estrutura para operacionalizar serviços AI e ML, aproveitando os serviços inteligentes da Adobe. Os serviços fornecem experiências personalizadas e em tempo real do cliente ou operacionalizam serviços inteligentes personalizados.

**Rótulo de dados S1:** `S1` o rótulo de dados é usado para classificar dados que especificam latitude e longitude que podem ser usados para determinar a localização precisa de um dispositivo.

**Rótulo de dados S2:** `S2` o rótulo de dados é usado para classificar os dados que podem ser usados para determinar uma área de fronteira geográfica amplamente definida.

**Fonte:** A fonte é um termo geral para qualquer conector de entrada no [!DNL Real-time Customer Data Platform].

**Atributo de origem:** Um atributo de origem é um campo no conjunto de dados de origem.  Os atributos de origem são mapeados para campos de schema de público alvo.

**Conector de origem:** Os conectores de fonte de Adobe Experience Platform ajudam os usuários a ingerir facilmente dados de várias fontes, permitindo a estruturação, rotulagem e aprimoramento de dados usando [!DNL Experience Platform Services]. Os dados podem ser assimilados de várias fontes, como armazenamentos baseados em nuvem, software de terceiros e sistemas CRM.

**Categoria de origem:** Uma categoria de origem é um agrupamento de [!DNL Real-time Customer Data Platform] fontes com características semelhantes.

**Catálogo de origem:** Um catálogo de origem é uma lista de fontes disponíveis no [!DNL Real-time Customer Data Platform].

**Namespace de identidade padrão:** namespaces de identidade padrão são identificadores predefinidos da Adobe, incluindo soluções padrão da Adobe e do setor empregadas para identificar usuários.

**Schema padrão:** Os schemas padrão consistem em classes e misturas e destinam-se a reutilização.

**Ingestão de transmissão:** A ingestão de transmissão contínua fornece aos usuários um método para enviar dados de dispositivos cliente e servidor para [!DNL Experience Platform] em tempo real.

**URL do Ponto Final de Transmissão:** Um URL de ponto de extremidade de transmissão é um terminal exclusivo fornecido pela Adobe e vinculado à organização IMS de um cliente para transmitir dados em [!DNL Experience Platform].

**Segmentação de transmissão:** A segmentação de transmissão é um processo contínuo de seleção de dados que atualiza os segmentos em resposta à atividade do usuário. Depois que um segmento é criado e salvo, a definição do segmento é aplicada em relação aos dados recebidos para [!DNL Real-time Customer Profile]. Adições e remoções do segmento são processadas regularmente, garantindo que sua audiência do público alvo permaneça relevante.

**Símbolo:** O símbolo é a abreviação de uma namespace de identidade que pode ser usada como referência nas APIs.

**Visualização do sistema:** A Visualização do sistema é uma representação visual de conjuntos de dados de origem que fluem por [!DNL Real-time Customer Profile] destinos.

[Voltar ao início](#adobe-experience-platform-glossary)

## T

**Recursos do Público alvo:** O recurso Público alvo especificado no mapeamento de recursos é o recurso previsto por um modelo.

**Modelo treinado:** Um modelo treinado representa a saída executável de um processo de treinamento modelo, no qual um conjunto de dados de treinamento foi aplicado à instância do modelo. Um modelo treinado manterá uma referência para qualquer Serviço Web Inteligente criado a partir dele. O modelo treinado é adequado para pontuação e criação de um serviço Web inteligente. As modificações em um modelo treinado podem ser rastreadas como uma nova versão.

**Token:** Um token é um tipo de segurança de autenticação de dois fatores que pode ser usado para autorizar o uso de serviços de computador com [!DNL Query Service].

**Tipo:** Tipo é a classe de problema de aprendizado de máquina para a qual uma receita é projetada e é usada após o treinamento para ajudar a avaliar a execução do treinamento.

[Voltar ao início](#adobe-experience-platform-glossary)

## U

**Schema da União:** O schema de União é uma consolidação de schemas para os quais foram habilitados [!DNL Real-time Customer Profile].

[Voltar ao início](#adobe-experience-platform-glossary)

## V

[Voltar ao início](#adobe-experience-platform-glossary)

## W

[Voltar ao início](#adobe-experience-platform-glossary)

## X

**XDM (Modelo de dados de experiência):** XDM (Experience Data Model) é o conceito de usar schemas padrão para unificar dados para uso com aplicativos [!DNL Experience Platform] e da Adobe Experience Cloud. O XDM é uma especificação formal usada para representar todos os dados de experiência do cliente em um único idioma ou modelo de dados padrão e padroniza como os dados são estruturados e acelera e simplifica o processo de obter insights de grandes quantidades de dados.

**XDM DecisionEvent:** Um DecisionEvent é usado para capturar observações sobre o resultado e o contexto de uma atividade de decisão, incluindo informações sobre como a decisão foi tomada, quando ocorreu, quais opções foram propostas (e escolhidas) e que estado contextual existia que influenciaram a decisão ou podiam ser observadas durante o processo de decisão. O DecisionEvents também captura a ID da proposta, um identificador globalmente exclusivo que pode ser usado para correlacionar a decisão a outros eventos. Os eventos de decisão não estão relacionados apenas aos Eventos de experiência que tiveram impacto em uma decisão, mas também ao ExperienceEvents que são uma resposta direta a uma proposta. É a expectativa de que os aplicativos façam referência à ID da proposta em cada ExperienceEvent que tenha sido influenciada pelas proposições. O histórico proposition-response em um perfil individual é mantido usando IDs de proposta.

**ExperienceEvent XDM:** Um ExperienceEvent é um registro de fatos do que ocorreu, incluindo o ponto no tempo e a identidade do indivíduo envolvido. O ExperienceEvents pode ser explícito (ações humanas diretamente observáveis) ou implícito (criado sem uma ação humana direta) e é registrado sem agregação ou interpretação. Eles são essenciais para análises de domínio de tempo, pois permitem observação e análise de alterações que ocorrem em uma determinada janela de tempo e a comparação entre várias janelas de tempo para rastrear tendências.

**Perfil individual XDM:** Um XDM [!DNL Individual Profile] forma uma representação singular dos atributos e interesses de indivíduos identificados e parcialmente identificados. perfis menos identificados podem conter apenas sinais comportamentais anônimos, como cookies de navegador, enquanto perfis altamente identificados podem conter informações pessoais detalhadas, como nome, data de nascimento, local e endereço de email. À medida que um perfil cresce, ele se torna um repositório robusto de informações pessoais, informações de identificação, detalhes de contato e preferências de comunicação para um indivíduo.

**Sistema XDM:** O Sistema XDM é a infraestrutura, a semântica de dados e o fluxo de trabalho em [!DNL Experience Platform] que é alimentado por schemas padrão.

[Voltar ao início](#adobe-experience-platform-glossary)

## S

[Voltar ao início](#adobe-experience-platform-glossary)

## Z

[Voltar ao início](#adobe-experience-platform-glossary)
