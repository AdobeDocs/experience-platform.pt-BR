---
title: 'Notas de versão do Adobe Experience Platform '
description: Notas de versão de Experience Platform 8 de abril de 2020
doc-type: release notes
last-update: April 13, 2020
author: ens71067
keywords: release notes;
translation-type: tm+mt
source-git-commit: f881c1365684b1ca9e6bf9a8ce866d234dc54128
workflow-type: tm+mt
source-wordcount: '975'
ht-degree: 5%

---


# Notas de versão da Adobe Experience Platform

**Data de lançamento: 8 de abril de 2020**

Novos recursos no Adobe Experience Platform:
* [!DNL Intelligent Services](#intelligent)

Atualizações dos recursos existentes:
* [!DNL Experience Data Model (XDM)](#xdm)
* [!DNL Data Governance](#governance)
* [!DNL Destinations](#destinations)
* [!DNL Privacy Service](#privacy)
* [!DNL Sources](#sources)

## [!DNL Intelligent Services] {#intelligent}

[!DNL Intelligent Services] capacite analistas e profissionais de marketing a aproveitar o poder da inteligência artificial e do aprendizado de máquina em casos de uso de experiência do cliente. Isso permite que os analistas de marketing configurem previsões específicas para as necessidades de uma empresa usando configurações de nível empresarial sem a necessidade de especialização em ciência de dados. Além disso, os profissionais de marketing podem ativar previsões em aplicativos Adobe Experience Cloud, Adobe Experience Platform e de terceiros.

**Principais recursos**

| Recurso | Descrição |
|---|---|
| [!DNL Customer AI] | [!DNL Customer AI] fornece aos profissionais de marketing o poder de gerar previsões de clientes a nível individual com explicações. Com a ajuda de fatores influentes, [!DNL Customer AI] você pode dizer o que um cliente deve fazer e por quê. Além disso, os profissionais de marketing podem se beneficiar de [!DNL Customer AI] previsões e insights para personalizar as experiências do cliente, atendendo às ofertas e mensagens mais apropriadas. |
| [!DNL Attribution AI] | [!DNL Attribution AI] é um serviço de atribuição de vários canais e algoritmos que calcula a influência e o impacto incremental das interações do cliente em relação aos resultados especificados. Com [!DNL Attribution AI]ele, os profissionais de marketing podem medir e otimizar o gasto de marketing e publicidade, entendendo o impacto de cada interação individual do cliente em cada fase das viagens do cliente. |

**Problemas conhecidos**

* Nenhum problema conhecido no momento.

Para obter mais informações sobre [!DNL Intelligent Services] e o que ele tem a oferta, consulte a visão geral [dos Serviços](../../intelligent-services/home.md)inteligentes.

## [!DNL Experience Data Model] Sistema (XDM) {#xdm}

A normalização e a interoperabilidade são conceitos fundamentais subjacentes [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM), impulsionado pelo Adobe, é um esforço para padronizar os dados de experiência do cliente e definir schemas para o gerenciamento da experiência do cliente.

A XDM é uma especificação publicamente documentada projetada para melhorar o poder das experiências digitais. Fornece estruturas e definições comuns para qualquer aplicativo que se comunique com os serviços no Adobe Experience Platform. Ao aderir aos padrões XDM, todos os dados de experiência do cliente podem ser incorporados a uma representação comum, fornecendo insights de forma mais rápida e integrada. Você pode obter informações importantes das ações do cliente, definir audiências do cliente por meio de segmentos e usar atributos do cliente para fins de personalização.

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Informações de exibição alternativas automáticas | O [!DNL Schema Registry] aplica automaticamente os valores personalizados de título e descrição configurados no `alternateDisplayInfo` descritor. |
| Restrições de campo escalar | O [!DNL Schema Registry] não permite mais de 6000 campos escalares em um único schema. |
| Revisão do desempenho | O projeto [!DNL Schema Registry] foi reformulado para atender às demandas de [!DNL Experience Platform] melhor qualidade. |

**Correções de erros**

* XDM atualizado para XED convertido para suportar um formato XED mais limpo para campos URI aninhados no XDM padrão.

**Problemas conhecidos**

* Conhecido

## [!DNL Data Governance] {#governance}

O Adobe Experience Platform [!DNL Data Governance] é uma série de estratégias e tecnologias usadas para gerenciar dados de clientes e garantir a conformidade com regulamentos, restrições e políticas aplicáveis ao uso de dados. Ele desempenha um papel fundamental em vários [!DNL Experience Platform] níveis, incluindo catalogação, linhagem de dados, rotulagem de uso de dados, políticas de acesso a dados e controle de acesso de dados para ações de marketing.

A introdução ao controle de dados exige uma compreensão completa dos regulamentos, obrigações contratuais e políticas corporativas aplicáveis aos dados do cliente. A partir daí, os dados podem ser classificados aplicando os rótulos de uso de dados apropriados, e seu uso pode ser controlado por meio da definição de políticas de uso de dados.

A estrutura DULE simplifica e simplifica o processo de categorização de dados e criação de políticas de uso de dados por meio da interface do [!DNL Experience Platform] usuário e da API DULE [!DNL Policy Service] .

**Novos recursos**

| Recurso | Descrição |
| -----------| ---------- |
| Gerenciar políticas de uso de dados na interface do usuário | As políticas de uso de dados agora podem ser gerenciadas dentro da área de trabalho _Políticas_ na [!DNL Experience Platform] UI. Consulte o guia [do usuário da](../../data-governance/policies/user-guide.md) política para obter mais informações. |

**Problemas conhecidos**

* None.

Para obter mais informações, consulte a visão geral [do](../../data-governance/home.md)Data Governance.


## Destinos {#destinations}

No [Adobe Real-time Customer Data Platform](../../rtcdp/overview.md), os destinos são integrações pré-criadas com plataformas de destino que ativam os dados para esses parceiros de forma contínua.

**Novos destinos**

A CDP em tempo real do Adobe agora oferece suporte à ativação de dados para mais de cinquenta [!DNL Experience Cloud Launch] extensões, permitindo análises, personalização e outros casos de uso. Consulte abaixo para obter detalhes:

| Documentação | Descrição |
|--- | ---|
| [Tipos de destino e categorias](/help/rtcdp/destinations/destination-types.md) | Este artigo explica a diferença entre conexões e extensões na interface CDP em tempo real do Adobe e recomenda quando usar cada um desses destinos. |
| [extensões Experience Platform Launch](/help/rtcdp/destinations/experience-platform-launch-extensions.md) | Esta página explica quais são [!DNL Launch] as extensões, os casos de uso do lista para usá-las e os links para a documentação de cada [!DNL Launch] extensão no Adobe Real-time CDP. |

Para obter mais informações, consulte a visão geral [de](/help/rtcdp/destinations/destinations-overview.md)Destinos.

## [!DNL Privacy Service] {#privacy}

As novas regulamentações legais e organizacionais estão dando aos usuários o direito de acessar ou excluir seus dados pessoais dos armazenamentos de dados mediante solicitação. O Adobe Experience Platform [!DNL Privacy Service] fornece uma API RESTful e uma interface de usuário para ajudá-lo a gerenciar essas solicitações de dados de seus clientes. Com [!DNL Privacy Service]o, você pode enviar solicitações para acessar e excluir dados pessoais ou particulares de clientes de aplicativos Adobe Experience Cloud, facilitando a conformidade automatizada com as regulamentações legais e organizacionais de privacidade.

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Suporte a PDPA | As solicitações de privacidade agora podem ser criadas e rastreadas sob o Personal Data Protection Act (PDPA) na Tailândia. Ao fazer solicitações de privacidade na API, a `regulation` matriz aceita o valor &quot;pdpa_tha&quot;. |
| Tipos de Namespace na interface do usuário | Agora é possível especificar diferentes tipos de namespace no Construtor de solicitações na [!DNL Privacy Service] interface do usuário. Consulte o guia [do](../../privacy-service/ui/user-guide.md) usuário para obter mais informações. |
| Substituição de ponto final antigo | O ponto de extremidade da API antiga (`data/privacy/gdpr`) foi substituído. |

Problemas conhecidos

* None

Para obter mais informações sobre [!DNL Privacy Service], leia a visão geral [do](../../privacy-service/home.md)Privacy Service.

## Fontes {#sources}

O Adobe Experience Platform pode assimilar dados de fontes externas, permitindo que você estruture, rotule e aprimore esses dados usando [!DNL Platform] serviços. Você pode assimilar dados de várias fontes, como aplicativos de Adobe, armazenamentos baseados em nuvem, software de terceiros e seu sistema de CRM.

[!DNL Experience Platform] fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem que você se autentique e se conecte a sistemas de armazenamentos externos e serviços CRM, defina horários para execuções de ingestão e gerencie a throughput de ingestão de dados.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Suporte a API e interface do usuário para bancos de dados | Novos conectores de origem para [!DNL Apache Spark] (em HDInsights), [!DNL Azure Synapse Analytics], [!DNL Azure Table Storage], [!DNL Hive] (em HDInsights) e [!DNL Phoenix]. |
| Suporte a API e interface para aplicativos baseados em pagamentos | Novos conectores de origem para [!DNL PayPal]. |
| Suporte a API e interface para aplicativos baseados em protocolos | Novos conectores de origem para [!DNL Generic OData]. |

**Problemas conhecidos**

* None

Para saber mais sobre fontes, consulte a visão geral [das](../../sources/home.md)fontes.
