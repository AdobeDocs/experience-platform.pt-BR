---
title: Notas de versão da Adobe Experience Platform de abril de 2020
description: As notas de versão de abril de 2020 para Adobe Experience Platform.
doc-type: release notes
last-update: April 13, 2020
author: ens71067
keywords: notas de versão;
exl-id: 0f68c71e-3c9d-453b-a953-1cd1b6ca2e35
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '983'
ht-degree: 10%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 8 de abril de 2020**

Novos recursos na Adobe Experience Platform:
* [[!DNL Intelligent Services]](#intelligent)

Atualizações dos recursos existentes:
* [[!DNL Experience Data Model (XDM)]](#xdm)
* [Governança de dados](#governance)
* [[!DNL Destinations]](#destinations)
* [[!DNL Privacy Service]](#privacy)
* [[!DNL Sources]](#sources)

## [!DNL Intelligent Services] {#intelligent}

[!DNL Intelligent Services] capacite analistas e profissionais de marketing para aproveitar o potencial da inteligência artificial e do aprendizado de máquina em casos de uso de experiência do cliente. Isso permite que os analistas de marketing definam previsões específicas para as necessidades de uma empresa usando configurações de nível empresarial sem a necessidade de conhecimento especializado em ciência de dados. Além disso, os profissionais de marketing podem ativar previsões no Adobe Experience Cloud, Adobe Experience Platform e aplicativos de terceiros.

**Principais recursos**

| Recurso | Descrição |
|---|---|
| [!DNL Customer AI] | [!DNL Customer AI] O oferece aos profissionais de marketing o poder de gerar previsões de clientes individualmente com explicações. Com a ajuda de fatores influentes, [!DNL Customer AI] Você pode saber o que um cliente provavelmente fará e por quê. Além disso, os profissionais de marketing podem se beneficiar [!DNL Customer AI] previsões e insights para personalizar as experiências do cliente, disponibilizando as ofertas e mensagens mais apropriadas. |
| [!DNL Attribution AI] | [!DNL Attribution AI] O é um serviço de atribuição de vários canais e algoritmos que calcula a influência e o impacto incremental das interações com o cliente em relação aos resultados especificados. Com o [!DNL Attribution AI], os profissionais de marketing podem medir e otimizar os gastos com marketing e publicidade, entendendo o impacto de cada interação individual com o cliente em cada fase das viagens do cliente. |

**Problemas conhecidos**

* Nenhum problema conhecido no momento.

Para obter mais informações sobre [!DNL Intelligent Services] e o que ele tem a oferecer, veja o [Visão geral dos Serviços inteligentes](../../intelligent-services/home.md).

## Sistema de [!DNL Experience Data Model] (XDM) {#xdm}

A normalização e a interoperabilidade são conceitos fundamentais [!DNL Experience Platform]. [!DNL Experience Data Model] O (XDM), orientado pelo Adobe, é um esforço para padronizar os dados de experiência do cliente e definir esquemas para o gerenciamento da experiência do cliente.

O XDM é uma especificação documentada publicamente projetada para melhorar o potencial das experiências digitais. Ele fornece estruturas e definições comuns para que qualquer aplicativo se comunique com os serviços na Adobe Experience Platform. Seguindo os padrões XDM, todos os dados de experiência do cliente podem ser incorporados a uma representação comum, fornecendo insights de maneira mais rápida e integrada. Você pode obter insights valiosos das ações do cliente, definir públicos do cliente por meio de segmentos e usar atributos do cliente para fins de personalização.

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Informações de exibição alternativa automática | A variável [!DNL Schema Registry] automaticamente os valores personalizados de título e descrição configurados no `alternateDisplayInfo` descritor. |
| Restrições de campo escalar | A variável [!DNL Schema Registry] O não permite mais de 6000 campos escalares em um único esquema. |
| Revisão de desempenho | A variável [!DNL Schema Registry] foi revisto para executar e atender às demandas da [!DNL Experience Platform] melhor. |

**Correções de erros**

* XDM atualizado para XED convertido para oferecer suporte a um formato XED mais limpo para campos URI aninhados no XDM padrão.

**Problemas conhecidos**

* Conhecido

## Governança de dados {#governance}

O Adobe Experience Platform Data Governance é uma série de estratégias e tecnologias usadas para gerenciar dados de clientes e garantir conformidade com normas, restrições e políticas aplicáveis ao uso de dados. Desempenha um papel fundamental na [!DNL Experience Platform] em vários níveis, incluindo catalogação, linhagem de dados, rotulagem de uso de dados, políticas de acesso a dados e controle de acesso a dados para ações de marketing.

A introdução ao controle de dados requer uma compreensão completa das normas, obrigações contratuais e políticas corporativas que se aplicam aos dados do cliente. A partir daí, os dados podem ser classificados por meio da aplicação dos rótulos de uso de dados apropriados, e seu uso pode ser controlado por meio da definição de políticas de uso de dados.

A estrutura de governança de dados simplifica e simplifica o processo de categorização de dados e criação de políticas de uso de dados por meio da [!DNL Experience Platform] interface do usuário e [!DNL Policy Service] API.

**Novos recursos**

| Recurso | Descrição |
| -----------| ---------- |
| Gerenciar políticas de uso de dados na interface | As políticas de uso de dados agora podem ser gerenciadas no **Políticas** espaço de trabalho no [!DNL Experience Platform] IU. Consulte a [guia do usuário da política](../../data-governance/policies/user-guide.md) para obter mais informações. |

**Problemas conhecidos**

* None.

Para obter mais informações, consulte [Visão geral da governança de dados](../../data-governance/home.md).


## Destinos {#destinations}

Entrada [Real-time Customer Data Platform](../../rtcdp/overview.md), os destinos são integrações pré-criadas com plataformas de destino que ativam os dados para esses parceiros de forma contínua.

**Novos destinos**

O Real-Time CDP agora oferece suporte à ativação de dados para mais de cinquenta [!DNL Experience Cloud Launch] extensões, ativação do analytics, personalização e outros casos de uso. Veja os detalhes abaixo:

| Documentação | Descrição |
|--- | ---|
| [Tipos e categorias de destino](../../destinations/destination-types.md) | Este artigo explica a diferença entre conexões e extensões na interface do Real-Time CDP e recomenda quando usar cada um desses destinos. |
| [extensões do Experience Platform Launch](../../destinations/catalog/launch-extensions/overview.md) | Esta página explica o que [!DNL Launch] extensões são, lista casos de uso para usá-las e links para a documentação de cada [!DNL Launch] extensão no Real-Time CDP. |

Para obter mais informações, consulte [Visão geral dos destinos](../../destinations/home.md).

## [!DNL Privacy Service] {#privacy}

As novas regulamentações legais e organizacionais dão aos usuários o direito de acessar ou excluir seus dados pessoais dos armazenamentos de dados, mediante solicitação. Adobe Experience Platform [!DNL Privacy Service] O fornece uma API RESTful e uma interface para ajudar você a gerenciar essas solicitações de dados de seus clientes. Com [!DNL Privacy Service], você pode enviar solicitações para acessar e excluir dados privados ou pessoais dos clientes por meio dos aplicativos da Adobe Experience Cloud, facilitando a conformidade automatizada com as regulamentações legais e organizacionais de privacidade.

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Suporte a PDPA | As solicitações de privacidade agora podem ser criadas e rastreadas de acordo com a Lei de Proteção de Dados Pessoais (PDPA) na Tailândia. Ao fazer solicitações de privacidade na API, a variável `regulation` aceita o valor &quot;pdpa_tha&quot;. |
| Tipos de namespace na interface do | Agora você pode especificar diferentes tipos de namespace no Criador de solicitações na [!DNL Privacy Service] IU. Consulte a [guia do usuário](../../privacy-service/ui/user-guide.md) para obter mais informações. |
| Descontinuação de ponto de extremidade antigo | O endpoint da API antiga (`data/privacy/gdpr`) foi descontinuado. |

Problemas conhecidos

* None

Para obter mais informações sobre [!DNL Privacy Service], comece lendo o [visão geral do Privacy Service](../../privacy-service/home.md).

## Fontes {#sources}

O Adobe Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, permitir estruturar, rotular e aprimorar esses dados usando [!DNL Platform] serviços. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

[!DNL Experience Platform] O fornece uma API RESTful e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar a sistemas de armazenamento externos e serviços de CRM, definir tempos para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Suporte a API e interface do usuário para bancos de dados | Novos conectores de origem para o [!DNL Apache Spark] (em HDInsights), [!DNL Azure Synapse Analytics], [!DNL Azure Table Storage], [!DNL Hive] (no HDInsights) e [!DNL Phoenix]. |
| Suporte a API e IU para aplicativos baseados em pagamentos | Novos conectores de origem para o [!DNL PayPal]. |
| Suporte de API e interface do usuário para aplicativos baseados em protocolos | Novos conectores de origem para o [!DNL Generic OData]. |

**Problemas conhecidos**

* None

Para saber mais sobre fontes, consulte a [visão geral das origens](../../sources/home.md).
