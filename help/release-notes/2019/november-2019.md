---
title: Notas de versão da Adobe Experience Platform de novembro de 2019
description: As notas de versão de novembro de 2019 da Adobe Experience Platform.
doc-type: release notes
last-update: November 18, 2019
author: crhoades, ens28527
exl-id: 2c417c56-cc61-4788-b248-d98ea6cf89f0
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '1889'
ht-degree: 7%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 18 de novembro de 2019**

Novos recursos na Adobe Experience Platform:

* [[!DNL Real-Time Customer Data Platform]](#rtcdp)
* [[!DNL Destinations]](#destinations)
* [[!DNL Sources]](#sources)

Atualizações dos recursos existentes:

* [[!DNL Data Science Workspace]](#dsw)
* [[!DNL Experience Data Model (XDM) System]](#xdm)
* [[!DNL Real-Time Customer Profile]](#profile)
* [[!DNL Segmentation Service]](#segmentation)

## [!DNL Real-Time Customer Data Platform] {#rtcdp}

Criada na Adobe Experience Platform, a Real-Time Customer Data Platform (Real-Time CDP) ajuda empresas a reunir dados conhecidos e desconhecidos para ativar perfis de clientes com decisões inteligentes em toda a jornada do cliente. A Real-Time CDP combina várias fontes de dados corporativas para criar perfis unificados em tempo real, que podem ser usados para fornecer experiências personalizadas individuais do cliente em todos os canais e dispositivos.

O [!DNL Real-Time Customer Data Platform] inclui ferramentas para governança de dados, gerenciamento de identidade, segmentação avançada e ciência de dados, de modo que você possa criar perfis e definir públicos, bem como obter insights avançados e aplicar políticas rigorosas de governança de dados.

O Adobe se conecta a um grande ecossistema de parceiros, sem mencionar as integrações nativas com o Adobe Experience Cloud, para que você possa ativar esses públicos com facilidade e fornecer excelentes experiências aos clientes em todos os canais, desde a personalização no local ou no aplicativo até email, mídia paga, call centers, dispositivos conectados e muito mais.

Com o Real-Time CDP, você pode:

* Obtenha uma visão única do seu cliente com a coleta contínua de dados do cliente em toda a empresa.
* Gerenciar perfis com responsabilidade e controles de governança e privacidade confiáveis para identificadores conhecidos e desconhecidos.
* Gere insights acionáveis e dimensione públicos com IA e aprendizado de máquina viabilizados pelo Adobe Sensei e criados para profissionais de marketing.
* Ofereça experiências personalizadas em tempo real em todos os canais e destinos.

Para obter mais informações, consulte a [documentação do Real-Time Customer Data Platform](../../rtcdp/overview.md).

**Principais recursos**

| Recurso | Descrição |
|---|---|
| Destinos | Integrações pré-criadas com plataformas de destino compatíveis com o [!DNL Real-Time Customer Data Platform] da Adobe que ativam dados para esses parceiros de forma contínua. Consulte [Destinos](#destinations) abaixo para obter mais informações. |
| Painel de métricas da página inicial | A página inicial do Real-Time Customer Data Platform (Real-Time CDP) inclui um painel de métricas que mostra informações sobre perfis e segmentos. A página inicial também contém links para materiais de aprendizado. Consulte a seção sobre [métricas do Real-Time Customer Data Platform](#real-time-customer-data-platform-metrics) abaixo. |
| Origens | Você pode assimilar dados de várias fontes, como Soluções da Adobe, armazenamento na nuvem, software de terceiros e seu CRM. Consulte a seção [Fontes](#sources) abaixo para saber mais. |

**[!DNL Real-Time Customer Data Platform]métricas**

A página inicial do Real-Time Customer Data Platform (Real-Time CDP), que inclui um painel de métricas, é exibida ao fazer logon no Real-Time CDP.

A página inicial é apenas um dos locais onde os cartões de métrica são exibidos. O Real-Time CDP fornece cartões de métrica em toda a sua experiência. Essas métricas informam sobre os dados, o perfil e os públicos-alvo de segmentos no sistema.

Se não houver dados no sistema ao fazer logon no Real-Time CDP, o painel na home page não será exibido. Nesse caso, a página inicial fornece material de aprendizado para uma primeira experiência de usuário. Conforme os dados são coletados, o painel é atualizado automaticamente para exibir informações sobre esses dados.

Para saber mais, consulte a [visão geral das métricas do Real-Time Customer Data Platform](../../rtcdp/home-page-dashboards.md)

## [!DNL Destinations] {#destinations}

[!DNL Destinations] são integrações pré-criadas com plataformas de destino compatíveis com o Real-Time Customer Data Platform da Adobe que ativam os dados para esses parceiros de forma contínua. Para obter mais informações, leia o artigo [Visão geral dos destinos](../../destinations/home.md).

**Destinos disponíveis**

Com a versão de novembro, o Real-Time Customer Data Platform da Adobe oferecerá suporte aos seguintes destinos:

* Advertising: [!DNL Google]
* Marketing por email: Adobe Campaign, [!DNL Salesforce Marketing Cloud], [!DNL Responsys], [!DNL Oracle Eloqua]

Consulte o [catálogo de destinos](../../destinations/catalog/overview.md) para obter informações sobre cada um dos destinos.

**Limitações conhecidas**

* O controle para permitir agendamentos de ativação personalizados no fluxo de ativação (etapa Agendar) não está disponível com a versão inicial.
* No momento, não há como editar ou excluir uma configuração de destino. Para contornar essa limitação, habilite ou desabilite o destino no canto superior direito da [página de detalhes do destino](../../destinations/ui/destination-details-page.md).
* No momento, não há validação em vigor para detalhes, caminho ou credenciais da conta ao se conectar ao destino ou à conta de armazenamento. Verifique se você está inserindo as credenciais corretas e se há erros de ortografia ou de digitação.
* Nenhuma renovação de credencial está em vigor com a versão inicial. Depois que uma conta expirar ou precisar de atualização, você deverá criar uma nova conexão de destino e remapear os segmentos mapeados anteriormente.

## Origens {#sources}

O Adobe Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, permitir que você estruture, rotule e aprimore esses dados usando os serviços do [!DNL Experience Platform]. Você pode assimilar dados de várias fontes, como Soluções da Adobe, armazenamento na nuvem, software de terceiros e seu sistema de CRM.

O [!DNL Experience Platform] fornece uma API RESTful e uma interface do usuário interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem que você faça autenticação em seus sistemas de armazenamento e serviços CRM, defina tempos para execuções de assimilação e gerencie a taxa de transferência de assimilação de dados.

**Principais recursos**

| Recurso | Descrição |
| ---------- | ------------ |
| IU de origens | Nova interface de usuário para criar, exibir e gerenciar conexões de origem. |
| Fluxos de trabalho renovados para conectores CRM | Novo fluxo de trabalho de interface intuitiva para criar e gerenciar conectores do [!DNL Microsoft Dynamics] e do [!DNL Salesforce]. |
| Suporte a conector para armazenamentos baseados em nuvem | Os conectores agora podem acessar armazenamentos baseados em nuvem. As novas fontes incluem [!DNL Amazon S3], [!DNL Azure Blob] e servidores FTP/SFTP. |

**Problemas conhecidos**

* Os conectores do Source para armazenamentos na nuvem não oferecem suporte à assimilação de arquivos compactados.

Para obter mais informações sobre origens, consulte [Visão geral das origens](../../sources/home.md).

## [!DNL Data Science Workspace] {#dsw}

O Adobe Experience Platform [!DNL Data Science Workspace] permite que cientistas de dados gerem insights de dados e conteúdo facilmente em aplicativos do Adobe e sistemas de terceiros, criando e operacionalizando Modelos de Aprendizado de Máquina. O [!DNL Data Science Workspace] é totalmente integrado ao [!DNL Experience Platform] e capacita o ciclo de vida completo da ciência de dados, incluindo a exploração e a preparação de dados XDM, seguidos pelo desenvolvimento e a operacionalização de Modelos para enriquecer automaticamente o [!DNL Real-Time Customer Profile] com Machine Learning Insights.

**Novos recursos**

| Recurso | Descrição |
| -----------| ---------- |
| Acesso a dados usando o SDK [!DNL Experience Platform] | Os blocos de anotações do iniciador e de Receitas pré-criados no [!DNL Python] agora usam o SDK [!DNL Experience Platform] para acessar dados. |
| Suporte para sandboxes | Suporte para a futura funcionalidade de sandbox (atualmente na versão beta), incluindo a capacidade de isolar notebooks e receitas em sandboxes de desenvolvimento ou produção. Consulte a [visão geral das sandboxes](../../sandboxes/home.md) para obter mais informações. |

Para obter mais informações, consulte a [visão geral do Data Science Workspace](../../data-science-workspace/home.md).

## Sistema de [!DNL Experience Data Model] (XDM) {#xdm}

A padronização e a interoperabilidade são os principais conceitos por trás do [!DNL Experience Platform]. O [!DNL Experience Data Model] (XDM), orientado pela Adobe, é um esforço para padronizar os dados de experiência do cliente e definir esquemas para o gerenciamento da experiência do cliente.

O XDM é uma especificação documentada publicamente projetada para melhorar o potencial das experiências digitais. Ele fornece estruturas e definições comuns para que qualquer aplicativo se comunique com os serviços na Adobe Experience Platform. Seguindo os padrões XDM, todos os dados de experiência do cliente podem ser incorporados a uma representação comum, fornecendo insights de maneira mais rápida e integrada. Você pode obter insights valiosos sobre ações de clientes, definir públicos-alvo por meio de segmentos e usar atributos de clientes para fins de personalização.

**Novos recursos**

| Recurso | Descrição |
| ---------- | ------------ |
| Esquema de notificação | Novo esquema que representa dados de notificação enviados durante o processo de assimilação de dados. |
| Esquemas do Adobe AdCloud DSP | Cinco novos esquemas foram adicionados para representar metadados da plataforma de demanda (DSP) da Adobe Advertising Cloud: Posicionamento, Campanha, Pacote, Anunciante e Conta. |
| Grupos de campos de esquema Detalhes da implementação do ExperienceEvent | Novos grupos de campos ExperienceEvent que adicionam um campo padrão para armazenar informações sobre o software usado para coletar o evento. |
| [!DNL Profile Privacy] grupos de campos | Novos grupos de campos de perfil que adicionam campos para aceitar sinais gerais de recusa e de recusa de vendas/compartilhamento para [!DNL Real-Time Customer Profile]. |
| Restrições de formato para `xdm:alternateDisplayInfo` | Os campos &quot;Título&quot; e &quot;Descrição&quot; de `xdm:alternateDisplayInfo` devem ser cadeias de caracteres para passar na validação. |
| Alteração de nome: XDM [!DNL Individual Profile] | O &quot;title&quot; da classe &quot;XDM [!DNL Profile]&quot; foi atualizado para &quot;XDM [!DNL Individual Profile]&quot;. O `$id` formal da classe não foi alterado. |

**Problemas conhecidos**

* Nenhum.

Para saber mais sobre como trabalhar com XDM usando a API [!DNL Schema Registry] e a interface de usuário [!DNL Schema Editor], leia a [documentação do Sistema XDM](../../xdm/home.md).

## [!DNL Real-Time Customer Profile] {#profile}

A Adobe Experience Platform permite gerar experiências coordenadas, consistentes e relevantes para seus clientes, independentemente de onde ou quando eles interagem com sua marca. Com o [!DNL Real-Time Customer Profile], você pode ter uma visão holística de cada cliente individual que combina dados de vários canais, incluindo dados online, offline, de CRM e de terceiros. O [!DNL Profile] permite consolidar seus dados diferentes de clientes em uma visualização unificada, oferecendo uma conta acionável com carimbo de data e hora de cada interação com o cliente.

| Recurso | Descrição |
| -----------| ---------- |
| Aprimoramentos na pesquisa de [!DNL Profile] | Os usuários agora podem pesquisar perfis usando descritores de referência e entidades relacionadas. |
| Limpar dados para um determinado conjunto de dados | Os usuários agora podem excluir dados de um determinado conjunto de dados ou lote usando a API de Trabalhos do Sistema [!DNL Profile]. |
| Aprimoramentos de consulta do Edge [!DNL Profile] | Os aplicativos agora podem consultar o Edge [!DNL Profile] por qualquer uma das identidades de um determinado perfil. |
| Configurar políticas de mesclagem por projeção | Os aplicativos agora podem configurar políticas de mesclagem por projeção para gerar uma visualização dos dados conforme regido por uma política de mesclagem específica. |
| Atributos computados | Os atributos computados calculam automaticamente o valor dos campos com base em outros valores, cálculos e expressões. Os atributos calculados operam no nível do perfil para agregar valores como &quot;compra total&quot;, &quot;valor vitalício&quot; ou &quot;status do funnel&quot; com base em um evento recebido, um evento recebido e dados de perfil, ou um evento recebido, dados de perfil e eventos históricos. |

**Correções de erros**

* Lista simplificada de estratégias de compilação de ID disponíveis no fluxo de trabalho de criação da política de mesclagem.

**Problemas conhecidos**

* Nenhum.

Para obter mais informações sobre o [!DNL Real-Time Customer Profile], incluindo tutoriais e práticas recomendadas para trabalhar com dados do [!DNL Profile], leia a [Visão geral do Perfil do cliente em tempo real](../../profile/home.md).

## [!DNL Segmentation Service] {#segmentation}

O Adobe Experience Platform [!DNL Segmentation Service] fornece uma interface de usuário e uma API RESTful que permite que você crie segmentos e gere públicos a partir dos dados do [!DNL Real-Time Customer Profile]. Esses segmentos são configurados e mantidos centralmente no [!DNL Experience Platform], tornando-os prontamente acessíveis por qualquer aplicativo do Adobe.

O [!DNL Segmentation Service] define um subconjunto específico de perfis descrevendo os critérios que distinguem um grupo de pessoas na sua base de clientes que pode ser direcionado por campanhas de marketing. Os segmentos podem ser baseados em dados de registro (como informações demográficas) ou em eventos de série temporal que representam interações de clientes com sua marca.

| Recurso | Descrição |
| -----------| ---------- |
| Segmentação programada | Os usuários agora podem ativar a avaliação de segmentos agendada para todos os segmentos por meio da interface do usuário e da API. Depois de habilitado, todos os segmentos serão avaliados uma vez por dia. Isso não afeta os recursos de segmentação sob demanda que continuam funcionando como antes.<br/><br/>Observação: o recurso de segmentação agendada não pode ser usado em sandboxes com mais de cinco políticas de mesclagem para [!DNL XDM Individual Profile]. |
| Segmentação de transmissão | O suporte para avaliação contínua de segmentos (segmentação por transmissão) permite que a maioria das regras de segmento sejam avaliadas, pois os dados estão sendo transmitidos para [!DNL Experience Platform]. Esse recurso significa que a associação do segmento será atualizada sem a necessidade de executar trabalhos de segmentação programados. Algumas exceções se aplicam, como segmentos que usam relacionamentos de várias entidades ou com cargas úteis enriquecidas. |
| Segmentos como blocos de construção | Ao criar segmentos usando a interface do construtor de segmentos, os usuários agora podem usar segmentos definidos anteriormente como blocos de construção para segmentos adicionais. <ul><li>Associação de público-alvo atual de referência: atualizações à medida que as pessoas entram e saem dos públicos-alvo.</li><li>Copiar lógica: pegue a definição de segmento selecionada e duplique-a no novo segmento.</li></ul> |
| Exibir associação de segmento por namespace de ID | A associação ao segmento agora pode ser visualizada pelo namespace de ID (email, ECID e contagem total). |
| Suporte a RBAC | O Construtor de segmentos agora oferece suporte a controles e permissões básicos de acesso com base em funções. |
| Suporte aprimorado para compartilhamento de público externo entre [!DNL Experience Platform] e soluções da Adobe | Os usuários agora podem trazer metadados de público-alvo externo (não [!DNL Experience Platform]) em cenários em que o número de públicos-alvo é grande ou não conhecido a priori. Esta versão inclui acesso aos metadados do [!DNL Audience Manager] para clientes que provisionaram o conector da solução. Esses metadados de público podem ser usados no Construtor de segmentos para criar novos [!DNL Experience Platform] segmentos. <br/><br/> Além disso, os segmentos criados em [!DNL Experience Platform] agora estarão disponíveis para uso nas soluções integradas da Adobe, incluindo [!DNL Audience Manager], [!DNL Target] e [!DNL Ad Cloud]. |

**Correções de erros**

* Correção de um problema que fazia com que a Segmentação de várias entidades retornasse zero perfil no caso de relações aninhadas.
* Correção de um problema em que a lógica de exclusão retornava resultados enganosos.
* Aprimoramento da legibilidade para pastas de várias entidades. Agora, eles mostram o nome amigável da classe XDM.
* Correção de um problema intermitente em que várias cópias da mesma pasta XDM eram exibidas.
* Agora são geradas mensagens para informar um usuário se as estimativas de segmento não estiverem disponíveis para a política de mesclagem selecionada.

**Problemas conhecidos**

* Nenhum.

Para saber mais sobre [!DNL Segmentation Service], leia a [Visão geral do Serviço de Segmentação](../../segmentation/home.md).
