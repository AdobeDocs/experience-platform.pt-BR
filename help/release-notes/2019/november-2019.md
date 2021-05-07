---
title: Notas de versão da Adobe Experience Platform
description: Notas de versão do Experience Platform 18 de novembro de 2019
doc-type: release notes
last-update: November 18, 2019
author: crhoades, ens28527
exl-id: 2c417c56-cc61-4788-b248-d98ea6cf89f0
translation-type: tm+mt
source-git-commit: ab0798851e5f2b174d9f4241ad64ac8afa20a938
workflow-type: tm+mt
source-wordcount: '1883'
ht-degree: 2%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 18 de novembro de 2019**

Novos recursos no Adobe Experience Platform:
* [[!DNL Real-time Customer Data Platform]](#rtcdp)
* [[!DNL Destinations]](#destinations)
* [[!DNL Sources]](#sources)

Atualizações dos recursos existentes:
* [[!DNL Data Science Workspace]](#dsw)
* [[!DNL Experience Data Model (XDM) System]](#xdm)
* [[!DNL Real-time Customer Profile]](#profile)
* [[!DNL Segmentation Service]](#segmentation)

## [!DNL Real-time Customer Data Platform] {#rtcdp}

Criada na Adobe Experience Platform, a Real-time Customer Data Platform (Real-time CDP) ajuda as empresas a unir dados conhecidos e desconhecidos para ativar perfis do cliente com decisões inteligentes em toda a jornada do cliente. A CDP em tempo real combina várias fontes de dados corporativas para criar perfis unificados em tempo real, que podem ser usados para fornecer experiências personalizadas individuais do cliente em todos os canais e dispositivos.

[!DNL Real-time Customer Data Platform] O inclui ferramentas para governança de dados, gerenciamento de identidade, segmentação avançada e ciência de dados, para que você possa criar perfis e definir públicos-alvo, bem como derivar informações avançadas e, ao mesmo tempo, poder aplicar políticas rigorosas de governança de dados.

O Adobe se conecta a um grande ecossistema de parceiros, para não mencionar as integrações nativas com o Adobe Experience Cloud, para que você possa ativar esses públicos com facilidade e fornecer excelentes experiências do cliente em todos os canais, desde a personalização no site ou no aplicativo até email, mídia paga, centrais de chamadas, dispositivos conectados e muito mais.

Com a CDP em tempo real, você pode:

* Obtenha uma visão única de seu cliente com a coleta contínua de dados do cliente em toda a empresa.
* Gerencie de maneira responsável perfis com controle confiável e controles de privacidade para identificadores conhecidos e desconhecidos.
* Gere insights acionáveis e dimensione públicos-alvo com IA e aprendizado de máquina fornecidos pela Adobe Sensei e criados para profissionais de marketing.
* Forneça experiências personalizadas em tempo real em todos os canais e destinos.

Para obter mais informações, consulte a [documentação da Plataforma de dados do cliente em tempo real](../../rtcdp/overview.md).

**Principais recursos**

| Recurso | Descrição |
|---|---|
| Destinos | Integrações pré-criadas com plataformas de destino compatíveis com o [!DNL Real-time Customer Data Platform] do Adobe que ativam os dados para esses parceiros de forma contínua. Consulte [Destinos](#destinations) abaixo para obter mais informações. |
| Painel de métricas da página inicial | A página inicial da Plataforma de dados do cliente em tempo real (CDP em tempo real) inclui um painel de métricas que mostra informações sobre perfis e segmentos. A página inicial também contém links para materiais de aprendizagem. Consulte a seção [Métricas da plataforma de dados do cliente em tempo real](#real-time-customer-data-platform-metrics) abaixo. |
| Fontes | Você pode assimilar dados de várias fontes, como Soluções Adobe, armazenamento baseado em nuvem, software de terceiros e seu CRM. Consulte a seção [Fontes](#sources) abaixo para saber mais. |

**[!DNL Real-time Customer Data Platform]métricas**

A página inicial da Plataforma de dados do cliente em tempo real (CDP em tempo real), que inclui um painel de métricas, é exibida ao fazer logon na CDP em tempo real.

A página inicial é apenas um dos locais onde os cartões de métrica são exibidos. A CDP em tempo real fornece cartões de métrica em toda a sua experiência. Essas métricas informam sobre os dados, o perfil e os públicos do segmento no sistema.

Se não houver dados no sistema quando você fizer logon na CDP em tempo real, o painel na página inicial não será exibido. Nesse caso, a página inicial fornece material de aprendizagem para uma primeira experiência do usuário. À medida que os dados são coletados, o painel é atualizado automaticamente para exibir informações sobre esses dados.

Para saber mais, consulte a [Visão geral das métricas da Plataforma de dados do cliente em tempo real](../../rtcdp/home-page-dashboards.md)

## [!DNL Destinations] {#destinations}

[!DNL Destinations] são integrações pré-criadas com plataformas de destino compatíveis com a Real-time Customer Data Platform do Adobe que ativam os dados para esses parceiros de forma contínua. Para obter mais informações, leia o artigo [Visão geral dos destinos](../../destinations/home.md) .

**Destinos disponíveis**

Com a versão de novembro, a Plataforma de dados do cliente em tempo real do Adobe oferece suporte aos seguintes destinos:

* Publicidade: [!DNL Google]
* Marketing por email: Adobe Campaign, [!DNL Salesforce Marketing Cloud], [!DNL Responsys], [!DNL Oracle Eloqua]

Consulte o [catálogo de destino](../../destinations/catalog/overview.md) para obter informações sobre cada um dos destinos.

**Limitações conhecidas**

* O controle para permitir agendamentos de ativação personalizados no [fluxo de ativação](../../destinations/ui/activate-destinations.md#activate-data) (etapa de agendamento) não está disponível com a versão inicial.
* No momento, não há como editar ou excluir uma configuração de destino. Para contornar essa limitação, você pode habilitar ou desabilitar o destino no canto superior direito da [página de detalhes do destino](../../destinations/ui/destination-details-page.md).
* Nenhuma validação está em vigor no momento para detalhes da conta, caminho ou credenciais ao se conectar ao destino ou à conta de armazenamento. Certifique-se de inserir as credenciais corretas e verifique novamente se há erros de ortografia ou erros de digitação.
* Não há renovações de credenciais em vigor com a versão inicial. Depois que uma conta expirar ou precisar de atualização, você deve criar uma nova conexão de destino e remapear os segmentos mapeados anteriormente.

## Fontes {#sources}

O Adobe Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, permite estruturar, rotular e aprimorar esses dados usando serviços [!DNL Platform]. Você pode assimilar dados de várias fontes, como Soluções Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

[!DNL Experience Platform] O fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar para seus sistemas de armazenamento e serviços de CRM, definir horários para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

**Principais recursos**

| Recurso | Descrição |
| ---------- | ------------ |
| Interface do usuário de fontes | Nova interface de usuário para criar, visualizar e gerenciar conexões de origem. |
| Fluxos de trabalho modernizados para conectores CRM | Novo fluxo de trabalho intuitivo da interface do usuário para criar e gerenciar conectores [!DNL Microsoft Dynamics] e [!DNL Salesforce]. |
| Suporte a conector para armazenamento baseado em nuvem | Os conectores agora podem acessar armazenamentos baseados em nuvem. As novas fontes incluem [!DNL Amazon S3], [!DNL Azure Blob] e servidores FTP/SFTP. |

**Problemas conhecidos**

* Os conectores de origem para armazenamentos baseados em nuvem não suportam a assimilação de arquivos compactados.

Para obter mais informações sobre fontes, consulte [Visão geral das fontes](../../sources/home.md).

## [!DNL Data Science Workspace] {#dsw}

O Adobe Experience Platform [!DNL Data Science Workspace] permite que os cientistas de dados gerem informações facilmente de dados e conteúdo em aplicativos Adobe e sistemas de terceiros, criando e operacionalizando Modelos de Aprendizagem de Máquina. [!DNL Data Science Workspace] O é totalmente integrado ao  [!DNL Platform] e alimenta o ciclo de vida completo da ciência de dados, incluindo a exploração e a preparação de dados XDM, seguido pelo desenvolvimento e pela operacionalização de modelos para enriquecer automaticamente  [!DNL Real-time Customer Profile] com os Insights de aprendizado de máquina.

**Novos recursos**

| Recurso | Descrição |
| -----------| ---------- |
| Acesso aos dados usando [!DNL Platform] SDK | Fórmulas pré-criadas e blocos de notas do iniciador no [!DNL Python] agora usam [!DNL Platform] SDK para acessar dados. |
| Suporte para sandboxes | Suporte para a futura funcionalidade de sandbox (atualmente em beta), incluindo a capacidade de isolar notebooks e receitas em sandboxes de desenvolvimento ou produção. Consulte a [visão geral das sandboxes](../../sandboxes/home.md) para obter mais informações. |

Para obter mais informações, consulte a [Visão geral do Data Science Workspace](../../data-science-workspace/home.md).

## [!DNL Experience Data Model] Sistema (XDM)  {#xdm}

A normalização e a interoperabilidade são conceitos-chave subjacentes a [!DNL Experience Platform]. [!DNL Experience Data Model] O (XDM), impulsionado pelo Adobe, é um esforço para padronizar os dados de experiência do cliente e definir esquemas para o gerenciamento da experiência do cliente.

O XDM é uma especificação publicamente documentada projetada para melhorar o poder das experiências digitais. Fornece estruturas e definições comuns para qualquer aplicativo se comunicar com serviços no Adobe Experience Platform. Ao seguir os padrões XDM, todos os dados de experiência do cliente podem ser incorporados a uma representação comum, fornecendo insights de forma mais rápida e integrada. Você pode obter informações valiosas das ações do cliente, definir públicos-alvo do cliente por meio de segmentos e usar atributos do cliente para fins de personalização.

**Novos recursos**

| Recurso | Descrição |
| ---------- | ------------ |
| Schema de notificação | Novo schema que representa dados de notificação enviados durante o processo de assimilação de dados. |
| Esquemas de DSP da Adobe AdCloud | Cinco novos esquemas foram adicionados para representar os metadados da plataforma de demanda (DSP) do Adobe Advertising Cloud: Disposição, Campanha, Pacote, Anunciante, Conta. |
| Grupos de campos de esquema Detalhes da implementação do ExperienceEvent | Novos grupos de campos ExperienceEvent que adicionam um campo padrão para armazenar informações sobre o software usado para coletar o evento. |
| [!DNL Profile Privacy] grupos de campos | Novos grupos de campos de perfil que adicionam campos para aceitar sinais de recusa gerais de saída e de vendas/compartilhamento para [!DNL Real-time Customer Profile]. |
| Restrições de formato para `xdm:alternateDisplayInfo` | Os campos &quot;Título&quot; e &quot;Descrição&quot; para `xdm:alternateDisplayInfo` devem ser strings para passar a validação. |
| Alteração de nome: XDM [!DNL Individual Profile] | O &quot;título&quot; da classe &quot;XDM [!DNL Profile]&quot; foi atualizado para &quot;XDM [!DNL Individual Profile]&quot;. O `$id` formal da classe não foi alterado. |

**Problemas conhecidos**

* None.

Para saber mais sobre como trabalhar com o XDM usando a API [!DNL Schema Registry] e a interface do usuário [!DNL Schema Editor], leia a [documentação do Sistema XDM](../../xdm/home.md).

## [!DNL Real-time Customer Profile] {#profile}

O Adobe Experience Platform permite que você conduza experiências coordenadas, consistentes e relevantes para seus clientes, independentemente de onde ou quando eles interagirem com sua marca. Com [!DNL Real-time Customer Profile], você pode ver uma visualização holística de cada cliente individual que combina dados de vários canais, incluindo dados online, offline, CRM e de terceiros. [!DNL Profile] O permite consolidar seus dados de clientes diferentes em uma visualização unificada que oferece uma conta acionável e com carimbos de data e hora de cada interação com o cliente.

| Recurso | Descrição |
| -----------| ---------- |
| Melhorias na pesquisa [!DNL Profile] | Os usuários agora podem pesquisar perfis usando descritores de referência e entidades relacionadas. |
| Limpar dados de um determinado conjunto de dados | Agora os usuários podem excluir dados de um determinado conjunto de dados ou lote usando a API de [!DNL Profile] Serviços do Sistema. |
| Aprimoramentos de consulta [!DNL Profile] de borda | Os aplicativos agora podem consultar o Edge [!DNL Profile] por qualquer uma das identidades de um determinado perfil. |
| Configurar políticas de mesclagem por projeção | Os aplicativos agora podem configurar políticas de mesclagem por projeção para gerar uma visualização dos dados conforme regido por uma política de mesclagem específica. |
| Atributos calculados | Os atributos calculados calculam automaticamente o valor dos campos com base em outros valores, cálculos e expressões. Os atributos calculados operam no nível do perfil para agregar valores como &quot;compra total&quot;, &quot;valor da vida útil&quot; ou &quot;status do funil&quot; com base em um evento de entrada, em um evento de entrada e em dados de perfil ou em um evento de entrada, em dados de perfil e em eventos históricos. |

**Correções de erros**

* Lista simplificada de estratégias de compilação de ID disponíveis no fluxo de trabalho de criação da política de mesclagem.

**Problemas conhecidos**

* Nenhum.

Para obter mais informações sobre [!DNL Real-time Customer Profile], incluindo tutoriais e práticas recomendadas para trabalhar com dados [!DNL Profile], leia a [Visão geral do perfil do cliente em tempo real](../../profile/home.md).

## [!DNL Segmentation Service] {#segmentation}

O Adobe Experience Platform [!DNL Segmentation Service] fornece uma interface de usuário e uma RESTful API que permite criar segmentos e gerar públicos-alvo a partir dos dados [!DNL Real-time Customer Profile]. Esses segmentos são configurados e mantidos centralmente em [!DNL Platform], tornando-os acessíveis a qualquer aplicativo do Adobe.

[!DNL Segmentation Service] O define um subconjunto específico de perfis ao descrever os critérios que distinguem um grupo comercializável de pessoas dentro da base do cliente. Os segmentos podem se basear em dados de registro (como informações demográficas) ou em eventos de séries cronológicas que representem as interações do cliente com sua marca.

| Recurso | Descrição |
| -----------| ---------- |
| Segmentação programada | Agora os usuários podem habilitar a avaliação de segmentos agendados para todos os segmentos por meio da interface do usuário e da API. Uma vez ativado, todos os segmentos serão avaliados uma vez por dia. Isso não afeta os recursos de segmentação sob demanda que continuam a funcionar como antes.<br/><br/>Observação: O recurso de segmentação agendada não pode ser usado em sandboxes com mais de cinco políticas de mesclagem para  [!DNL XDM Individual Profile]. |
| Segmentação de streaming | O suporte para a avaliação contínua dos segmentos (segmentação de fluxo) permite que a maioria das regras de segmento seja avaliada à medida que os dados estão transmitindo para [!DNL Platform]. Esse recurso significa que a associação de segmento estará atualizada sem a necessidade de executar tarefas de segmentação programadas. Algumas exceções se aplicam, como segmentos que usam relações de várias entidades ou com cargas enriquecidas. |
| Segmentos como blocos de construção | Ao criar segmentos usando a interface do usuário do Construtor de segmentos, os usuários agora podem usar segmentos definidos anteriormente como blocos de construção para segmentos adicionais. <ul><li>Fazer referência à associação de público-alvo atual: atualizações conforme as pessoas mudam de público-alvo.</li><li>Copiar lógica: use a definição de segmento selecionada e duplique-a no novo segmento.</li></ul> |
| Exibir associação de segmento por namespace de ID | A associação de segmento agora pode ser visualizada por namespace de ID (email, ECID e contagem total). |
| Suporte RBAC | O Construtor de segmentos agora oferece suporte para controles e permissões básicos de acesso com base em funções. |
| Suporte aprimorado para compartilhamento de público externo entre [!DNL Platform] e soluções Adobe | Agora os usuários podem trazer metadados de público-alvo externos (não[!DNL Experience Platform]) em cenários em que o número de públicos-alvo é grande ou não é conhecido a priori. Esta versão inclui acesso aos metadados [!DNL Audience Manager] para clientes que provisionaram o conector da solução. Os metadados do público-alvo podem ser usados no Construtor de segmentos para criar novos [!DNL Experience Platform] segmentos. <br/><br/> Além disso, os segmentos criados no agora  [!DNL Experience Platform] estarão disponíveis para uso em soluções Adobe integradas, incluindo  [!DNL Audience Manager],  [!DNL Target]e  [!DNL Ad Cloud]. |

**Correções de erros**

* Correção de um problema que fazia com que a Segmentação de várias entidades retornasse perfis zero no caso de relacionamentos aninhados.
* Correção de um problema em que a lógica de exclusão retornava resultados enganosos.
* Aprimorada a legibilidade de pastas de várias entidades. Agora, eles mostram o nome amigável da classe XDM.
* Correção de um problema intermitente em que várias cópias da mesma pasta XDM eram exibidas.
* As mensagens agora são produzidas para informar um usuário se as estimativas de segmento não estiverem disponíveis para a política de mesclagem selecionada.

**Problemas conhecidos**

* Nenhum.

Para saber mais sobre [!DNL Segmentation Service], leia a [Visão geral do serviço de segmentação](../../segmentation/home.md).
