---
title: Notas de versão da Adobe Experience Platform
description: Notas de versão do Experience Platform 8 de abril de 2020
doc-type: release notes
last-update: April 13, 2020
author: ens71067
keywords: notas de versão;
exl-id: 0f68c71e-3c9d-453b-a953-1cd1b6ca2e35
source-git-commit: 03e7863f38b882a2fbf6ba0de1755e1924e8e228
workflow-type: tm+mt
source-wordcount: '979'
ht-degree: 10%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 8 de abril de 2020**

Novos recursos no Adobe Experience Platform:
* [[!DNL Intelligent Services]](#intelligent)

Atualizações dos recursos existentes:
* [[!DNL Experience Data Model (XDM)]](#xdm)
* [Governança de dados](#governance)
* [[!DNL Destinations]](#destinations)
* [[!DNL Privacy Service]](#privacy)
* [[!DNL Sources]](#sources)

## [!DNL Intelligent Services] {#intelligent}

[!DNL Intelligent Services] capacite analistas e profissionais de marketing a aproveitar o potencial da inteligência artificial e do aprendizado de máquina em casos de uso da experiência do cliente. Isso permite que os analistas de marketing configurem previsões específicas para as necessidades de uma empresa usando configurações de nível empresarial sem a necessidade de experiência em ciência de dados. Além disso, os profissionais de marketing podem ativar previsões em aplicativos da Adobe Experience Cloud, Adobe Experience Platform e de terceiros.

**Principais recursos**

| Recurso | Descrição |
|---|---|
| [!DNL Customer AI] | [!DNL Customer AI] O fornece aos profissionais de marketing o poder de gerar previsões de clientes no nível individual com explicações. Com a ajuda de fatores influentes, [!DNL Customer AI] O pode informar o que um cliente provavelmente fará e por quê. Além disso, os profissionais de marketing podem se beneficiar do [!DNL Customer AI] previsões e insights para personalizar as experiências do cliente, disponibilizando as ofertas e mensagens mais apropriadas. |
| [!DNL Attribution AI] | [!DNL Attribution AI] é um serviço de atribuição de vários canais e algoritmos que calcula a influência e o impacto incremental das interações com o cliente em relação aos resultados especificados. Com o [!DNL Attribution AI], os profissionais de marketing podem medir e otimizar os gastos com marketing e publicidade, entendendo o impacto de cada interação individual com o cliente em cada fase das viagens do cliente. |

**Problemas conhecidos**

* Nenhum problema conhecido no momento.

Para obter mais informações sobre [!DNL Intelligent Services] e o que tem a oferecer, consulte a [Visão geral dos Serviços inteligentes](../../intelligent-services/home.md).

## [!DNL Experience Data Model] Sistema (XDM) {#xdm}

A normalização e a interoperabilidade são conceitos-chave subjacentes [!DNL Experience Platform]. [!DNL Experience Data Model] O (XDM), impulsionado pelo Adobe, é um esforço para padronizar os dados de experiência do cliente e definir esquemas para o gerenciamento da experiência do cliente.

O XDM é uma especificação publicamente documentada projetada para melhorar o poder das experiências digitais. Fornece estruturas e definições comuns para qualquer aplicativo se comunicar com serviços no Adobe Experience Platform. Ao seguir os padrões XDM, todos os dados de experiência do cliente podem ser incorporados a uma representação comum, fornecendo insights de forma mais rápida e integrada. Você pode obter informações valiosas das ações do cliente, definir públicos-alvo do cliente por meio de segmentos e usar atributos do cliente para fins de personalização.

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Informações de exibição alternativa automática | O [!DNL Schema Registry] aplica automaticamente os valores personalizados de título e descrição configurados no `alternateDisplayInfo` descritor. |
| Restrições de campo escalar | O [!DNL Schema Registry] não permite mais de 6000 campos escalares em um único schema. |
| Reformulação do desempenho | O [!DNL Schema Registry] foi revista para executar e atender às demandas de [!DNL Experience Platform] melhor. |

**Correções de erros**

* Atualização do XDM para XED convertido para suportar um formato XED mais limpo para campos de URI aninhados no XDM padrão.

**Problemas conhecidos**

* Conhecido

## Governança de dados {#governance}

A Governança de dados da Adobe Experience Platform é uma série de estratégias e tecnologias usadas para gerenciar dados de clientes e garantir a conformidade com regulamentos, restrições e políticas aplicáveis ao uso de dados. Ele desempenha um papel fundamental no [!DNL Experience Platform] em vários níveis, incluindo catalogação, linhagem de dados, rotulagem de uso de dados, políticas de acesso a dados e controle de acesso a dados para ações de marketing.

A introdução ao controle de dados requer uma compreensão completa dos regulamentos, obrigações contratuais e políticas corporativas aplicáveis aos dados do cliente. A partir daí, os dados podem ser classificados aplicando os rótulos de uso de dados apropriados e seu uso pode ser controlado por meio da definição de políticas de uso de dados.

A estrutura de Governança de dados simplifica e simplifica o processo de categorização de dados e criação de políticas de uso de dados por meio do [!DNL Experience Platform] interface do usuário e [!DNL Policy Service] API.

**Novos recursos**

| Recurso | Descrição |
| -----------| ---------- |
| Gerenciar políticas de uso de dados na interface do usuário | As políticas de uso de dados agora podem ser gerenciadas dentro do **Políticas** na área de trabalho do [!DNL Experience Platform] IU. Consulte a [guia do usuário de política](../../data-governance/policies/user-guide.md) para obter mais informações. |

**Problemas conhecidos**

* None.

Para obter mais informações, consulte o [Visão geral da governança de dados](../../data-governance/home.md).


## Destinos {#destinations}

Em [Real-time Customer Data Platform](../../rtcdp/overview.md), os destinos são integrações pré-criadas com plataformas de destino que ativam os dados para esses parceiros de forma contínua.

**Novos destinos**

A CDP em tempo real agora oferece suporte à ativação de dados para mais de cinquenta [!DNL Experience Cloud Launch] extensões, habilitando análises, personalização e outros casos de uso. Veja os detalhes abaixo:

| Documentação | Descrição |
|--- | ---|
| [Tipos e categorias de destino](../../destinations/destination-types.md) | Este artigo explica a diferença entre conexões e extensões na interface da CDP em tempo real e recomenda quando usar cada um desses destinos. |
| [Extensões do Experience Platform Launch](../../destinations/catalog/launch-extensions/overview.md) | Esta página explica o que [!DNL Launch] extensões são, listas de casos de uso para usá-las e links para a documentação de cada [!DNL Launch] na CDP em tempo real. |

Para obter mais informações, consulte o [Visão geral dos destinos](../../destinations/home.md).

## [!DNL Privacy Service] {#privacy}

As novas regulamentações legais e organizacionais dão aos usuários o direito de acessar ou excluir seus dados pessoais dos armazenamentos de dados, mediante solicitação. Adobe Experience Platform [!DNL Privacy Service] O fornece uma RESTful API e interface do usuário para ajudar você a gerenciar essas solicitações de dados de seus clientes. Com [!DNL Privacy Service], você pode enviar solicitações para acessar e excluir dados pessoais de clientes de aplicativos Adobe Experience Cloud, facilitando a conformidade automatizada com as regulamentações legais e organizacionais de privacidade.

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Suporte a PDPA | As solicitações de privacidade agora podem ser criadas e rastreadas de acordo com a Lei de Proteção de Dados Pessoais (PDPA) na Tailândia. Ao fazer solicitações de privacidade na API, a variável `regulation` A matriz aceita o valor &quot;pdpa_tha&quot;. |
| Tipos de namespace na interface do usuário | Agora você pode especificar diferentes tipos de namespace no Construtor de solicitações na [!DNL Privacy Service] IU. Consulte a [guia do usuário](../../privacy-service/ui/user-guide.md) para obter mais informações. |
| Substituição antiga do terminal | O endpoint da antiga API (`data/privacy/gdpr`) foi substituída. |

Problemas conhecidos

* None

Para obter mais informações sobre [!DNL Privacy Service], comece lendo o [Visão geral do Privacy Service](../../privacy-service/home.md).

## Fontes {#sources}

O Adobe Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, permitir estruturar, rotular e aprimorar esses dados usando [!DNL Platform] serviços. Você pode assimilar dados de várias fontes, como aplicativos de Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

[!DNL Experience Platform] O fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e se conectar a sistemas de armazenamento externos e serviços CRM, definir horários para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Suporte a API e interface do usuário para bancos de dados | Novos conectores de origem para [!DNL Apache Spark] (em HDInsights), [!DNL Azure Synapse Analytics], [!DNL Azure Table Storage], [!DNL Hive] (em HDInsights), e [!DNL Phoenix]. |
| Suporte a API e interface do usuário para aplicativos baseados em pagamentos | Novos conectores de origem para [!DNL PayPal]. |
| Suporte a API e interface do usuário para aplicativos baseados em protocolos | Novos conectores de origem para [!DNL Generic OData]. |

**Problemas conhecidos**

* Nenhum

Para saber mais sobre fontes, consulte o [visão geral das fontes](../../sources/home.md).
