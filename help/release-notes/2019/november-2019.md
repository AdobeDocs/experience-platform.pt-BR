---
title: 'Notas de versão do Adobe Experience Platform '
description: Notas de versão de Experience Platform 18 de novembro de 2019
doc-type: release notes
last-update: November 18, 2019
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: f881c1365684b1ca9e6bf9a8ce866d234dc54128
workflow-type: tm+mt
source-wordcount: '1884'
ht-degree: 2%

---


# Notas de versão da Adobe Experience Platform

**Data de lançamento: 18 de novembro de 2019**

Novos recursos no Adobe Experience Platform:
* [!DNL Real-time Customer Data Platform](#rtcdp)
* [!DNL Destinations](#destinations)
* [!DNL Sources](#sources)

Atualizações dos recursos existentes:
* [!DNL Data Science Workspace](#dsw)
* [!DNL Experience Data Model (XDM) System](#xdm)
* [!DNL Real-time Customer Profile](#profile)
* [!DNL Segmentation Service](#segmentation)

## [!DNL Real-time Customer Data Platform] {#rtcdp}

Construído no Adobe Experience Platform, o Adobe Real-time Customer Data Platform (CDP em tempo real) ajuda as empresas a unir dados conhecidos e desconhecidos para ativar perfis do cliente com decisões inteligentes durante toda a jornada do cliente. A CDP em tempo real combina várias fontes de dados corporativos para criar perfis unificados em tempo real que podem ser usados para fornecer experiências personalizadas individuais do cliente em todos os canais e dispositivos.

[!DNL Real-time Customer Data Platform] inclui ferramentas para controle de dados, gerenciamento de identidade, segmentação avançada e ciência de dados, para que você possa criar perfis e definir audiências, bem como obter informações avançadas e, ao mesmo tempo, poder aplicar políticas rigorosas de controle de dados.

O Adobe se conecta a um grande ecossistema de parceiros, para não mencionar as integrações nativas com a Adobe Experience Cloud, para que você possa ativar essas audiências sem interrupções e fornecer excelentes experiências ao cliente em todos os canais, desde a personalização no site ou no aplicativo até o email, a mídia paga, as centrais de atendimento, os dispositivos conectados e muito mais.

Com a CDP em tempo real, você pode:

* Obtenha uma única visualização do seu cliente com a coleta contínua de dados do cliente em toda a empresa.
* Gerencie de forma responsável perfis com controle confiável e controles de privacidade para identificadores conhecidos e desconhecidos.
* Gerar insights acionáveis e audiências dimensionáveis com IA e aprendizado de máquina capacitado pela Adobe Sensei e desenvolvido para profissionais de marketing.
* Forneça experiências personalizadas em tempo real em todos os canais e destinos.

Para obter mais informações, consulte a documentação [](../../rtcdp/overview.md)Adobe Real-time Customer Data Platform.

**Principais recursos**

| Recurso | Descrição |
|---|---|
| Destinos | Integrações pré-criadas com plataformas de destino suportadas pela Adobe [!DNL Real-time Customer Data Platform] que ativam os dados para esses parceiros de forma contínua. See [Destinations](#destinations) below for more information. |
| painel de métricas de Home page | O home page Adobe Real-time Customer Data Platform (Real-time CDP) inclui um painel de métricas que mostra informações sobre perfis e segmentos. O home page também contém links para materiais de aprendizado. Consulte a seção sobre Dados do cliente em tempo [real Métricas](#real-time-customer-data-platform-metrics) da Platform abaixo. |
| Fontes | Você pode assimilar dados de várias fontes, como Adobe Solutions, armazenamento baseado em nuvem, software de terceiros e seu CRM. Consulte a seção [Fontes](#sources) abaixo para saber mais. |

**[!DNL Real-time Customer Data Platform]métricas **

O home page Adobe Real-time Customer Data Platform (Real-time CDP), que inclui um painel de métricas, é exibido quando você faz logon na CDP em tempo real.

O home page é apenas um dos locais onde os cartões de métrica aparecem. A CDP em tempo real fornece cartões de métricas em toda a sua experiência. Essas métricas informam sobre as audiências de dados, perfis e segmentos no sistema.

Se não houver dados no sistema quando você fizer logon na CDP em tempo real, o painel no home page não será exibido. Nesse caso, o home page fornece material de aprendizado para uma primeira experiência do usuário. À medida que os dados são coletados, o painel é atualizado automaticamente para exibir informações sobre esses dados.

Para saber mais, consulte a visão geral das métricas da Platform Dados do cliente em tempo [real](../../rtcdp/home-page-dashboards.md)

## [!DNL Destinations] {#destinations}

[!DNL Destinations] são integrações pré-criadas com plataformas de destino suportadas pela Platform de dados do cliente em tempo real do Adobe que ativam os dados para esses parceiros de forma contínua. Para obter mais informações, leia o artigo de visão geral [](../../rtcdp/destinations/destinations-overview.md) Destinos.

**Destinos disponíveis**

Com a versão de novembro, os dados do cliente em tempo real Adobe, a Platform oferece suporte aos seguintes destinos:

* Publicidade: [!DNL Google]
* Marketing por email: Adobe Campaign, [!DNL Salesforce Marketing Cloud], [!DNL Responsys], [!DNL Oracle Eloqua
   ]
Consulte o catálogo [de](../../rtcdp/destinations/destinations-catalog.md) destino para obter informações sobre cada um dos destinos.

**Limitações conhecidas**

* O controle para permitir programações de ativação personalizadas no fluxo [de](../../rtcdp/destinations/activate-destinations.md#activate-data) ativação (etapa de programação) não está disponível na versão inicial.
* No momento, não há como editar ou excluir uma configuração de destino. Para contornar essa limitação, você pode ativar ou desativar o destino no canto superior direito da página [de detalhes do](../../rtcdp/destinations/destination-details-page.md)destino.
* Nenhuma validação está atualmente em vigor para detalhes da conta, caminho ou credenciais ao se conectar ao destino ou à conta do armazenamento. Verifique se você está inserindo as credenciais corretas e duplo para verificar erros ortográficos ou erros de digitação.
* Nenhuma renovação de credenciais está em vigor com a versão inicial. Depois que uma conta expirar ou precisar de atualização, você deverá criar uma nova conexão de destino e remapear seus segmentos mapeados anteriormente.

## Fontes {#sources}

O Adobe Experience Platform pode assimilar dados de fontes externas, permitindo que você estruture, rotule e aprimore esses dados usando [!DNL Platform] serviços. Você pode assimilar dados de várias fontes, como Adobe Solutions, armazenamento baseado em nuvem, software de terceiros e sistema CRM.

[!DNL Experience Platform] fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem que você se autentique em seus sistemas de armazenamentos e serviços CRM, defina horários para execuções de ingestão e gerencie a throughput de ingestão de dados.

**Principais recursos**

| Recurso | Descrição |
| ---------- | ------------ |
| Interface do usuário de fontes | Nova interface de usuário para criar, exibir e gerenciar conexões de origem. |
| workflows remodelados para conectores CRM | Novo fluxo de trabalho intuitivo da interface para criar e gerenciar [!DNL Microsoft Dynamics] e [!DNL Salesforce] conectores. |
| Suporte de conector para armazenamentos baseados em nuvem | Os conectores agora podem acessar armazenamentos baseados em nuvem. As novas fontes incluem [!DNL Amazon S3], [!DNL Azure Blob]e servidores FTP/SFTP. |

**Problemas conhecidos**

* Os conectores de origem para armazenamentos baseados em nuvem não suportam a ingestão de arquivos compactados.

Para obter mais informações sobre fontes, consulte Visão geral [das](../../sources/home.md)fontes.

## [!DNL Data Science Workspace] {#dsw}

O Adobe Experience Platform [!DNL Data Science Workspace] permite que os cientistas de dados gerem informações de dados e conteúdo sem interrupções em aplicativos de Adobe e sistemas de terceiros, criando e operacionalizando Modelos de Aprendizagem de Máquinas. [!DNL Data Science Workspace] é totalmente integrada com [!DNL Platform] e potencializa o ciclo de vida completo da ciência de dados, incluindo a exploração e preparação de dados XDM, seguido pelo desenvolvimento e operacionalização de Modelos para enriquecer automaticamente [!DNL Real-time Customer Profile] com os Insights de Aprendizagem de Máquinas.

**Novos recursos**

| Recurso | Descrição |
| -----------| ---------- |
| Acesso aos dados usando o [!DNL Platform] SDK | As receitas pré-criadas e os notebooks de iniciação [!DNL Python] agora usam o [!DNL Platform] SDK para acessar dados. |
| Suporte para caixas de proteção | Suporte para a futura funcionalidade da caixa de proteção (atualmente em beta), incluindo a capacidade de isolar notebooks e Fórmulas em caixas de proteção de desenvolvimento ou produção. Consulte a visão geral [das](../../sandboxes/home.md) caixas de proteção para obter mais informações. |

Para obter mais informações, consulte a visão geral [da](../../data-science-workspace/home.md)Data Science Workspace.

## [!DNL Experience Data Model] Sistema (XDM) {#xdm}

A normalização e a interoperabilidade são conceitos fundamentais subjacentes [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM), impulsionado pelo Adobe, é um esforço para padronizar os dados de experiência do cliente e definir schemas para o gerenciamento da experiência do cliente.

A XDM é uma especificação publicamente documentada projetada para melhorar o poder das experiências digitais. Fornece estruturas e definições comuns para qualquer aplicativo que se comunique com os serviços no Adobe Experience Platform. Ao aderir aos padrões XDM, todos os dados de experiência do cliente podem ser incorporados a uma representação comum, fornecendo insights de forma mais rápida e integrada. Você pode obter informações importantes das ações do cliente, definir audiências do cliente por meio de segmentos e usar atributos do cliente para fins de personalização.

**Novos recursos**

| Recurso | Descrição |
| ---------- | ------------ |
| schema de notificação | Novo schema que representa os dados de notificação enviados durante o processo de ingestão de dados. |
| schemas de DSP da Adobe AdCloud | Cinco novos schemas foram adicionados para representar os metadados da plataforma de demanda (DSP) da Adobe Advertising Cloud: Posicionamento, Campanha, Pacote, Anunciante, Conta. |
| Mistura Detalhes da implementação do ExperienceEvent | Novo mixin ExperienceEvent que adiciona um campo padrão para armazenar informações sobre o software usado para coletar o evento. |
| [!DNL Profile Privacy] mistura | Novo mixin de perfil que adiciona campos para aceitar sinais gerais de saída e de não participação em vendas/compartilhamento para [!DNL Real-time Customer Profile]. |
| Restrições de formato para `xdm:alternateDisplayInfo` | Os campos &quot;Título&quot; e &quot;Descrição&quot; para `xdm:alternateDisplayInfo` devem ser strings para passar na validação. |
| Alteração de nome: XDM [!DNL Individual Profile] | O &quot;título&quot; da classe &quot;XDM [!DNL Profile]&quot; foi atualizado para &quot;XDM [!DNL Individual Profile]&quot;. O formal `$id` da classe não foi alterado. |

**Problemas conhecidos**

* None.

Para saber mais sobre como trabalhar com o XDM usando a [!DNL Schema Registry] API e a interface do [!DNL Schema Editor] usuário, leia a documentação [do Sistema](../../xdm/home.md)XDM.

## [!DNL Real-time Customer Profile] {#profile}

O Adobe Experience Platform permite que você direcione experiências coordenadas, consistentes e relevantes para seus clientes, independentemente de onde ou quando eles interagem com sua marca. Com [!DNL Real-time Customer Profile]o, você pode ver uma visualização holística de cada cliente individual que combina dados de vários canais, incluindo dados online, offline, CRM e de terceiros. [!DNL Profile] permite consolidar seus dados de clientes diferentes em uma visualização unificada, oferecendo uma conta acionável e com carimbos de data e hora de cada interação com o cliente.

| Recurso | Descrição |
| -----------| ---------- |
| Melhorias na [!DNL Profile] pesquisa | Os usuários agora têm a capacidade de pesquisar perfis usando descritores de referência e entidades relacionadas. |
| Limpar dados para um dado conjunto de dados | Os usuários agora podem excluir dados de um determinado conjunto de dados ou lote usando a API de Serviços do [!DNL Profile] Sistema. |
| Melhorias no [!DNL Profile] query Edge | Agora, os aplicativos podem query o Edge [!DNL Profile] por qualquer uma das identidades de um determinado perfil. |
| Configurar políticas de mesclagem por projeção | Os aplicativos agora podem configurar políticas de mesclagem por projeção para gerar uma visualização dos dados, conforme governado por uma política de mesclagem específica. |
| Atributos calculados | Os atributos calculados calculam automaticamente o valor dos campos com base em outros valores, cálculos e expressões. Os atributos calculados operam no nível do perfil para valores de agregação, como &quot;compra total&quot;, &quot;valor do tempo de vida&quot; ou &quot;status do funil&quot;, com base em um evento recebido, em dados de evento e perfil recebidos ou em um evento recebido, dados de perfil e eventos históricos. |

**Correções de erros**

* lista simplificada de estratégias de identificação disponíveis no fluxo de trabalho de criação de políticas de mesclagem.

**Problemas conhecidos**

* None.

Para obter mais informações sobre [!DNL Real-time Customer Profile], incluindo tutoriais e práticas recomendadas para trabalhar com [!DNL Profile] dados, leia a Visão geral [do Perfil do cliente em tempo](../../profile/home.md)real.

## [!DNL Segmentation Service] {#segmentation}

O Adobe Experience Platform [!DNL Segmentation Service] fornece uma interface de usuário e uma RESTful API que permite criar segmentos e gerar audiências a partir de seus [!DNL Real-time Customer Profile] dados. Esses segmentos são configurados e mantidos centralmente [!DNL Platform], tornando-os facilmente acessíveis por qualquer aplicativo Adobe.

[!DNL Segmentation Service] define um subconjunto específico de perfis descrevendo os critérios que distinguem um grupo comercializável de pessoas dentro da sua base de clientes. Os segmentos podem se basear em dados de registro (como informações demográficas) ou em eventos de séries cronológicas que representem as interações do cliente com sua marca.

| Recurso | Descrição |
| -----------| ---------- |
| Segmentação programada | Os usuários agora podem ativar a avaliação de segmentos agendados para todos os segmentos por meio da interface do usuário e da API. Depois de habilitados, todos os segmentos serão avaliados uma vez por dia. Isso não afeta os recursos de segmentação sob demanda que continuam a funcionar como antes.<br/><br/>Observação: O recurso de segmentação agendada não pode ser usado em caixas de proteção com mais de cinco políticas de mesclagem para [!DNL XDM Individual Profile]. |
| Segmentação em streaming | O suporte para a avaliação contínua de segmentos (segmentação de fluxo contínuo) permite que a maioria das regras de segmento seja avaliada à medida que os dados são transmitidos [!DNL Platform]. Esse recurso significa que a associação de segmento estará atualizada, sem a necessidade de executar tarefas de segmentação programadas. Algumas exceções se aplicam, como segmentos que usam relações de várias entidades ou com cargas aprimoradas. |
| Segmentos como blocos de construção | Ao criar segmentos usando a interface do usuário do Construtor de segmentos, os usuários agora podem usar segmentos previamente definidos como blocos de construção para segmentos adicionais. <ul><li>Referência à associação de audiência atual: é atualizada à medida que as pessoas entram e saem do audiência.</li><li>Lógica de cópia: use a definição de segmento selecionada e a duplicado no novo segmento.</li></ul> |
| associação de segmento de Visualização por namespace de ID | A associação ao segmento agora pode ser visualizada pela namespace de ID (email, ECID e contagem total). |
| Suporte RBAC | O Construtor de segmentos agora oferece suporte para permissões e controles de acesso básicos baseados em funções. |
| Suporte aprimorado para compartilhamento de audiências externas entre as soluções [!DNL Platform] e Adobe | Agora, os usuários podem trazer metadados externos (não[!DNL Experience Platform]) de audiência em cenários onde o número de audiências é grande ou desconhecido a priori. Esta versão inclui acesso aos [!DNL Audience Manager] metadados para clientes que provisionaram o conector da solução. Esses metadados de audiência podem ser usados no Construtor de segmentos para criar novos [!DNL Experience Platform] segmentos. <br/><br/> Além disso, os segmentos criados no [!DNL Experience Platform] agora estarão disponíveis para uso em soluções integradas de Adobe, incluindo [!DNL Audience Manager], [!DNL Target]e [!DNL Ad Cloud]. |

**Correções de erros**

* Corrigido um problema que fazia com que a Segmentação de várias entidades retornasse zero perfis no caso de relacionamentos aninhados.
* Correção de um problema em que a lógica de exclusão retornava resultados enganosos.
* Aprimoramento da legibilidade de pastas de várias entidades. Agora, eles mostram o nome amigável da classe XDM.
* Corrigido um problema intermitente no qual várias cópias da mesma pasta XDM apareciam.
* As mensagens agora são produzidas para informar um usuário se as estimativas de segmentos não estiverem disponíveis para a política de mesclagem selecionada.

**Problemas conhecidos**

* None.

Para saber mais sobre [!DNL Segmentation Service], leia a visão geral [do Serviço de](../../segmentation/home.md)segmentação.