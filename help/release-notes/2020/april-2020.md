---
title: Notas de versão de abril de 2020 da Adobe Experience Platform
description: As notas de versão de abril de 2020 da Adobe Experience Platform.
doc-type: release notes
last-update: April 13, 2020
author: ens71067
keywords: Notas de versão;
exl-id: 0f68c71e-3c9d-453b-a953-1cd1b6ca2e35
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '972'
ht-degree: 20%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: quinta-feira, 8 de abril de 2020**

Novos recursos na Adobe Experience Platform:

* [[!DNL Intelligent Services]](#intelligent)

Atualizações dos recursos existentes:

* [[!DNL Experience Data Model (XDM)]](#xdm)
* [Governança de dados](#governance)
* [[!DNL Destinations]](#destinations)
* [[!DNL Privacy Service]](#privacy)
* [[!DNL Sources]](#sources)

## [!DNL Intelligent Services] {#intelligent}

[!DNL Intelligent Services] capacite analistas e profissionais de marketing a aproveitar o potencial da inteligência artificial e do aprendizado de máquina em casos de uso de experiência do cliente. Isso permite que os analistas de marketing definam previsões específicas para as necessidades de uma empresa usando configurações de nível empresarial sem a necessidade de conhecimento especializado em ciência de dados. Além disso, os profissionais de marketing podem ativar previsões no Adobe Experience Cloud, Adobe Experience Platform e aplicativos de terceiros.

**Principais recursos**

| Recurso | Descrição |
|---|---|
| [!DNL Customer AI] | A [!DNL Customer AI] fornece aos profissionais de marketing o poder de gerar previsões de clientes individualmente com explicações. Com a ajuda de fatores influentes, o [!DNL Customer AI] pode informar o que um cliente deve fazer e por quê. Além disso, os profissionais de marketing podem se beneficiar das previsões e insights do [!DNL Customer AI] para personalizar as experiências do cliente, disponibilizando as ofertas e mensagens mais apropriadas. |
| [!DNL Attribution AI] | [!DNL Attribution AI] é um serviço de atribuição de vários canais e algoritmos que calcula a influência e o impacto incremental das interações com o cliente em relação aos resultados especificados. Com o [!DNL Attribution AI], os profissionais de marketing podem medir e otimizar os gastos com marketing e publicidade, entendendo o impacto de cada interação individual com o cliente em cada fase das jornadas do cliente. |

**Problemas conhecidos**

* Nenhum problema conhecido no momento.

Para obter mais informações sobre o [!DNL Intelligent Services] e o que ele tem a oferecer, consulte a [visão geral dos Serviços Inteligentes](../../intelligent-services/home.md).

## Sistema de [!DNL Experience Data Model] (XDM) {#xdm}

A padronização e a interoperabilidade são os principais conceitos por trás do [!DNL Experience Platform]. O [!DNL Experience Data Model] (XDM), orientado pela Adobe, é um esforço para padronizar os dados de experiência do cliente e definir esquemas para o gerenciamento da experiência do cliente.

O XDM é uma especificação documentada publicamente projetada para melhorar o potencial das experiências digitais. Ele fornece estruturas e definições comuns para que qualquer aplicativo se comunique com os serviços na Adobe Experience Platform. Seguindo os padrões XDM, todos os dados de experiência do cliente podem ser incorporados a uma representação comum, fornecendo insights de maneira mais rápida e integrada. Você pode obter insights valiosos sobre ações de clientes, definir públicos-alvo por meio de segmentos e usar atributos de clientes para fins de personalização.

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Informações de exibição alternativa automática | O [!DNL Schema Registry] aplica automaticamente os valores de título e descrição personalizados configurados no descritor `alternateDisplayInfo`. |
| Restrições de campo escalar | O [!DNL Schema Registry] não permite mais de 6000 campos escalares em um único esquema. |
| Revisão de desempenho | O [!DNL Schema Registry] foi revisto para atender melhor às demandas de [!DNL Experience Platform]. |

**Correções de erros**

* XDM atualizado para XED convertido para oferecer suporte a um formato XED mais limpo para campos URI aninhados no XDM padrão.

**Problemas conhecidos**

* Conhecido

## Governança de dados {#governance}

A Governança de dados da Adobe Experience Platform é uma série de estratégias e tecnologias usadas para gerenciar dados de clientes e garantir a conformidade com regulamentos, restrições e políticas aplicáveis ao uso de dados. Ele desempenha uma função importante no [!DNL Experience Platform] em vários níveis, incluindo catalogação, linhagem de dados, rotulagem de uso de dados, políticas de acesso a dados e controle de acesso a dados para ações de marketing.

A introdução ao controle de dados requer uma compreensão completa das normas, obrigações contratuais e políticas corporativas que se aplicam aos dados do cliente. A partir daí, os dados podem ser classificados por meio da aplicação dos rótulos de uso de dados apropriados, e seu uso pode ser controlado por meio da definição de políticas de uso de dados.

A estrutura de Governança de Dados simplifica e simplifica o processo de categorização de dados e criação de políticas de uso de dados por meio da interface do usuário [!DNL Experience Platform] e da API [!DNL Policy Service].

**Novos recursos**

| Recurso | Descrição |
| -----------| ---------- |
| Gerenciar políticas de uso de dados na interface | As políticas de uso de dados agora podem ser gerenciadas no espaço de trabalho **Políticas** na interface do usuário [!DNL Experience Platform]. Consulte o [guia do usuário da política](../../data-governance/policies/user-guide.md) para obter mais informações. |

**Problemas conhecidos**

* Nenhum.

Para obter mais informações, consulte a [visão geral sobre governança de dados](../../data-governance/home.md).


## Destinos {#destinations}

No [Real-Time Customer Data Platform](../../rtcdp/overview.md), os destinos são integrações pré-criadas com plataformas de destino que ativam dados para esses parceiros de forma contínua.

**Novos destinos**

O Real-Time CDP agora oferece suporte à ativação de dados para mais de cinquenta extensões do [!DNL Experience Cloud Launch], permitindo análise, personalização e outros casos de uso. Veja os detalhes abaixo:

| Documentação | Descrição |
|--- | ---|
| [Tipos e categorias de destino](../../destinations/destination-types.md) | Este artigo explica a diferença entre conexões e extensões na interface do Real-Time CDP e recomenda quando usar cada um desses destinos. |
| [Extensões do Experience Platform Launch](../../destinations/catalog/launch-extensions/overview.md) | Esta página explica quais são as extensões do [!DNL Launch], lista os casos de uso para utilizá-las e fornece links para a documentação de cada extensão do [!DNL Launch] no Real-Time CDP. |

Para obter mais informações, consulte a [Visão geral dos Destinos](../../destinations/home.md).

## [!DNL Privacy Service] {#privacy}

As novas regulamentações legais e organizacionais dão aos usuários o direito de acessar ou excluir seus dados pessoais dos armazenamentos de dados, mediante solicitação. O Adobe Experience Platform [!DNL Privacy Service] fornece uma API RESTful e uma interface para ajudar você a gerenciar essas solicitações de dados de seus clientes. Com o [!DNL Privacy Service], você pode enviar solicitações para acessar e excluir dados privados ou pessoais dos clientes por meio dos aplicativos da Adobe Experience Cloud, facilitando a conformidade automatizada com as regulamentações legais e organizacionais de privacidade.

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Suporte a PDPA | As solicitações de privacidade agora podem ser criadas e rastreadas de acordo com a Lei de Proteção de Dados Pessoais (PDPA) na Tailândia. Ao criar solicitações de privacidade na API, a matriz `regulation` aceita o valor “pdpa_tha”. |
| Tipos de namespace na interface | Agora é possível especificar diferentes tipos de namespace no criador de solicitações da interface do [!DNL Privacy Service]. Consulte o [Guia do usuário](../../privacy-service/ui/user-guide.md) para obter mais informações. |
| Descontinuação do ponto de acesso antigo | O antigo ponto de acesso da API (`data/privacy/gdpr`) foi descontinuado. |

Problemas conhecidos

* None

Para obter mais informações sobre [!DNL Privacy Service], comece lendo a [visão geral do Privacy Service](../../privacy-service/home.md).

## Origens {#sources}

O Adobe Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, permitir que você estruture, rotule e aprimore esses dados usando os serviços do [!DNL Experience Platform]. Você pode assimilar dados de várias fontes, como aplicativos da Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

O [!DNL Experience Platform] fornece uma API RESTful e uma interface do usuário interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar a sistemas de armazenamento externos e serviços de CRM, definir períodos para execuções de ingestão e gerenciar a taxa de transferência de ingestão de dados.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Suporte a API e interface do usuário para bancos de dados | Novos conectores de origem para [!DNL Apache Spark] (em HDInsights), [!DNL Azure Synapse Analytics], [!DNL Azure Table Storage] e [!DNL Hive]. |
| Suporte de API e interface do usuário para aplicativos baseados em protocolos | Novos conectores de origem para [!DNL Generic OData]. |

**Problemas conhecidos**

* None

Para saber mais sobre fontes, consulte a [visão geral das fontes](../../sources/home.md).
