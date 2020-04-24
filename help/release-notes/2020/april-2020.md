---
title: 'Notas de versão do Adobe Experience Platform '
description: Notas de versão da Experience Platform 8 de abril de 2020
doc-type: release notes
last-update: April 13, 2020
author: ens71067
keywords: release notes;
translation-type: tm+mt
source-git-commit: e5fa12b92f7006f2c5c428b25f81dade57733498

---


# Notas de versão da Adobe Experience Platform

**Data de lançamento: 8 de abril de 2020**

Novos recursos da Adobe Experience Platform:
* [Serviços inteligentes](#intelligent)

Atualizações dos recursos existentes:
* [Modelo de dados de experiência (XDM)](#xdm)
* [Governança de dados](#governance)
* [Destinos](#destinations)
* [Privacy Service](#privacy)
* [Fontes](#sources)

## Serviços inteligentes {#intelligent}

Os Serviços inteligentes capacitam analistas e profissionais de marketing a aproveitar o poder da inteligência artificial e do aprendizado de máquina em casos de uso de experiência do cliente. Isso permite que os analistas de marketing configurem previsões específicas para as necessidades de uma empresa usando configurações de nível empresarial sem a necessidade de especialização em ciência de dados. Além disso, os profissionais de marketing podem ativar previsões na Adobe Experience Cloud, na Adobe Experience Platform e em aplicativos de terceiros.

**Principais recursos**

| Recurso | Descrição |
|---|---|
| AI do cliente | A IA do cliente fornece aos comerciantes o poder de gerar previsões de clientes a nível individual com explicações. Com a ajuda de fatores influentes, a IA do cliente pode informar o que um cliente deve fazer e por que. Além disso, os profissionais de marketing podem se beneficiar das previsões e insights de IA do cliente para personalizar as experiências do cliente, atendendo às ofertas e mensagens mais apropriadas. |
| Atribuição AI | O AI de atribuição é um serviço de atribuição algorítmico e com vários canais que calcula a influência e o impacto incremental das interações do cliente em relação aos resultados especificados. Com a Atribuição AI, os profissionais de marketing podem medir e otimizar o gasto de marketing e publicidade ao compreender o impacto de cada interação individual do cliente em cada fase das viagens do cliente. |

**Problemas conhecidos**

* Nenhum problema conhecido no momento.

Para obter mais informações sobre os Serviços inteligentes e o que eles têm a oferta, consulte a visão geral [dos Serviços](../../intelligent-services/home.md)inteligentes.

## Sistema do Experience Data Model (XDM) {#xdm}

A normalização e a interoperabilidade são conceitos-chave por trás da plataforma da experiência. O Experience Data Model (XDM), desenvolvido pela Adobe, é um esforço para padronizar os dados de experiência do cliente e definir schemas para o gerenciamento da experiência do cliente.

A XDM é uma especificação publicamente documentada projetada para melhorar o poder das experiências digitais. Fornece estruturas e definições comuns para qualquer aplicativo que se comunique com os serviços na Adobe Experience Platform. Ao aderir aos padrões XDM, todos os dados de experiência do cliente podem ser incorporados a uma representação comum, fornecendo insights de forma mais rápida e integrada. Você pode obter informações importantes das ações do cliente, definir audiências do cliente por meio de segmentos e usar atributos do cliente para fins de personalização.

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Informações de exibição alternativas automáticas | O Registro do Schema aplica automaticamente os valores personalizados de título e descrição configurados no `alternateDisplayInfo` descritor. |
| Restrições de campo escalar | O Registro de Schemas não permite mais de 6000 campos escalares em um único schema. |
| Revisão do desempenho | O Registro do Schema foi revisado para executar e atender melhor às demandas da Plataforma de experiência. |

**Correções de erros**

* XDM atualizado para XED convertido para suportar um formato XED mais limpo para campos URI aninhados no XDM padrão.

**Problemas conhecidos**

* Conhecido

## Governança de dados {#governance}

O Adobe Experience Platform Data Governance é uma série de estratégias e tecnologias usadas para gerenciar dados de clientes e garantir a conformidade com regulamentos, restrições e políticas aplicáveis ao uso de dados. Ele desempenha um papel fundamental na plataforma da experiência em vários níveis, incluindo catalogação, linhagem de dados, rotulagem de uso de dados, políticas de acesso a dados e controle de acesso de dados para ações de marketing.

A introdução ao controle de dados exige uma compreensão completa dos regulamentos, obrigações contratuais e políticas corporativas aplicáveis aos dados do cliente. A partir daí, os dados podem ser classificados aplicando os rótulos de uso de dados apropriados, e seu uso pode ser controlado por meio da definição de políticas de uso de dados.

A estrutura DULE simplifica e simplifica o processo de categorização de dados e criação de políticas de uso de dados por meio da interface de usuário da plataforma Experience e da API do serviço de política DULE.

**Novos recursos**

| Recurso | Descrição |
| -----------| ---------- |
| Gerenciar políticas de uso de dados na interface do usuário | As políticas de uso de dados agora podem ser gerenciadas dentro da área de trabalho _Políticas_ na interface do usuário da plataforma de experiência. Consulte o guia [do usuário da](../../data-governance/policies/user-guide.md) política para obter mais informações. |

**Problemas conhecidos**

* Nenhum.

Para obter mais informações, consulte a visão geral [do](../../data-governance/home.md)Data Governance.


## Destinos {#destinations}

Na Plataforma [de dados do cliente em tempo real da](../../rtcdp/overview.md)Adobe, os destinos são integrações pré-criadas com plataformas de destino que ativam os dados para esses parceiros de forma contínua.

**Novos destinos**

A Adobe Real-time CDP agora oferece suporte à ativação de dados para mais de cinquenta extensões de lançamento da Experience Cloud, permitindo análises, personalização e outros casos de uso. Consulte abaixo para obter detalhes:

| Documentação | Descrição |
|--- | ---|
| [Tipos de destino e categorias](/help/rtcdp/destinations/destination-types.md) | Este artigo explica a diferença entre conexões e extensões na interface CDP em tempo real da Adobe e recomenda quando usar cada um desses destinos. |
| [Extensões do Experience Platform Launch](/help/rtcdp/destinations/experience-platform-launch-extensions.md) | Esta página explica o que são as extensões do Launch, os casos de uso do lista para usá-las e os links para a documentação de cada extensão do Launch no Adobe Real-time CDP. |

Para obter mais informações, consulte a visão geral [de](/help/rtcdp/destinations/destinations-overview.md)Destinos.

## Privacy Service {#privacy}

As novas regulamentações legais e organizacionais estão dando aos usuários o direito de acessar ou excluir seus dados pessoais dos armazenamentos de dados mediante solicitação. O Adobe Experience Platform Privacy Service fornece uma API RESTful e uma interface de usuário para ajudá-lo a gerenciar essas solicitações de dados de seus clientes. Com o Privacy Service, você pode enviar solicitações para acessar e excluir dados pessoais ou privados de clientes dos aplicativos da Adobe Experience Cloud, facilitando a conformidade automatizada com as regulamentações legais e organizacionais de privacidade.

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Suporte a PDPA | As solicitações de privacidade agora podem ser criadas e rastreadas sob o Personal Data Protection Act (PDPA) na Tailândia. Ao fazer solicitações de privacidade na API, a `regulation` matriz aceita o valor &quot;pdpa_tha&quot;. |
| Tipos de Namespace na interface do usuário | Agora você pode especificar diferentes tipos de namespace no Construtor de solicitações na interface do usuário do Privacy Service. Consulte o guia [do](../../privacy-service/ui/user-guide.md) usuário para obter mais informações. |
| Substituição de ponto final antigo | O ponto de extremidade da API antiga (`data/privacy/gdpr`) foi substituído. |

Problemas conhecidos

* Nenhum

Para obter mais informações sobre o Privacy Service, leia a visão geral [](../../privacy-service/home.md)do Privacy Service para obter start.

## Fontes {#sources}

A plataforma Adobe Experience pode assimilar dados de fontes externas, permitindo que você estruture, rotule e aprimore esses dados usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos da Adobe, armazenamentos baseados em nuvem, software de terceiros e seu sistema de CRM.

A plataforma Experience fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem que você se autentique e se conecte a sistemas de armazenamentos externos e serviços CRM, defina horários para execuções de ingestão e gerencie a throughput de ingestão de dados.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Suporte a API e interface do usuário para bancos de dados | Novos conectores de origem para Apache Spark (em HDInsights), Azure Synapse Analytics, Azure Table Armazenamento, Hive (em HDInsights) e Phoenix. |
| Suporte a API e interface para aplicativos baseados em pagamentos | Novos conectores de origem para o PayPal. |
| Suporte a API e interface para aplicativos baseados em protocolos | Novos conectores de origem para OData genérico. |

**Problemas conhecidos**

* Nenhum

Para saber mais sobre fontes, consulte a visão geral [das](../../sources/home.md)fontes.
