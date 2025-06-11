---
title: Notas de pré-lançamento do Experience Platform
description: Uma visualização das notas de versão mais recentes do Adobe Experience Platform.
hide: true
hidefromtoc: true
source-git-commit: c34c41d384fbc4f309dffa8bba97a0f6f3468efc
workflow-type: tm+mt
source-wordcount: '1480'
ht-degree: 16%

---


# Notas de pré-lançamento do Adobe Experience Platform

>[!IMPORTANT]
>
>Este documento é uma **visualização** das notas de versão do mês atual. Os itens da versão estão sujeitos a alterações e podem ser adicionados ou removidos na versão final.

>[!TIP]
>
>Consulte a documentação a seguir para obter as notas de versão de outros aplicativos da Adobe Experience Platform:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/releases/latest?lang=pt-BR)
>- [Composição de público-alvo federado](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/en/docs/real-time-cdp-collaboration/using/latest)

**Data de lançamento: quinta-feira, 18 de junho de 2025**

Novos recursos e atualizações dos recursos existentes no Adobe Experience Platform:

- [Controle de acesso](#access-control)
- [Gerenciamento avançado do ciclo de vida dos dados](#advanced-data-lifecycle-management)
- [Painéis](#dashboards)
- [Governança de dados](#data-governance)
- [Destinos](#destinations)
- [Composição de público-alvo federado](#fac)
- [Privacy Service](#privacy-service)
- [Query Service](#query-service)
- [Sandboxes](#sandboxes)
- [Origens](#sources)

## Controle de acesso {#access-control}

O Experience Platform aproveita os perfis de produto do [Adobe Admin Console](https://adminconsole.adobe.com) para vincular usuários com permissões e sandboxes. As permissões controlam o acesso a vários recursos do Experience Platform, incluindo modelagem de dados, gerenciamento de perfis e administração de sandbox.

**Principais recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Permissão Exportar dados do painel | As opções **[!UICONTROL Baixar CSV]** e **[!UICONTROL Enviar como email]** nos painéis agora exigem a permissão **[!UICONTROL Exportar Dados do Painel]**. Essa permissão garante que somente os usuários autorizados possam exportar dados tabelados do insight, oferecendo suporte a políticas mais rigorosas de controle de governança e acesso aos dados. |

Para obter mais informações, consulte a [visão geral do controle de acesso](../access-control/home.md).

## Gerenciamento avançado do ciclo de vida dos dados {#advanced-data-lifecycle-management}

O Experience Platform fornece um conjunto de recursos de higiene de dados que permitem gerenciar os dados armazenados por meio de exclusões programáticas de registros e conjuntos de dados do consumidor. Usando o espaço de trabalho Ciclo de vida dos dados na interface do usuário ou por meio de chamadas para a API de higiene de dados, você pode gerenciar com eficiência seus armazenamentos de dados. Use esses recursos para garantir que as informações sejam usadas conforme esperado, sejam atualizadas quando dados incorretos precisarem de correção e sejam excluídas quando as políticas organizacionais considerarem necessário.

**Nova documentação**

| Nova documentação | Descrição |
| --- | --- |
| Disponibilidade Geral de Exclusão de Registro | Agora é possível excluir registros individuais com base em campos de identidade usando a interface ou a API. Esse recurso ajuda a reduzir o armazenamento, impor a governança e melhorar a higiene de dados permitindo exclusões de um único conjunto de dados ou em todos os conjuntos de dados. Limites de volume e requisitos de qualificação se aplicam. |

Para obter mais informações, leia a [visão geral avançada do gerenciamento do ciclo de vida dos dados](../hygiene/home.md).

## Painéis {#dashboards}

O Experience Platform fornece vários painéis por meio dos quais você pode visualizar insights importantes sobre os dados de sua organização, conforme capturados durante instantâneos diários.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| ------- | ----------- |
| Opção de exportação Enviar como email | Agora é possível exportar até 10.000 registros dos painéis do modo Query Pro selecionando **[!UICONTROL Enviar como email]** no menu **[!UICONTROL Exibir mais]**. Essa opção envia com segurança um link de download para o email associado à Adobe para exportações maiores. |

Para obter mais informações sobre painéis, incluindo como conceder permissões de acesso e criar widgets personalizados, comece lendo a [visão geral dos painéis](../dashboards/home.md).

## Governança de dados {#data-governance}

A Governança de dados da Adobe Experience Platform é uma série de estratégias e tecnologias usadas para gerenciar dados de clientes e garantir a conformidade com regulamentos, restrições e políticas aplicáveis ao uso de dados. Ele desempenha uma função importante no [!DNL Experience Platform] em vários níveis, incluindo catalogação, linhagem de dados, rotulagem de uso de dados, políticas de acesso a dados e controle de acesso a dados para ações de marketing.

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Configurações de Alertas CMK do Azure e Inclui na lista de permissões de IP | Incluir na lista de permissões Agora você pode atualizar o endereço IP estático da Adobe no Cofre de chaves do Azure para garantir acesso contínuo quando as restrições de rede forem ativadas. Isso ajuda a evitar interrupções nos serviços da Platform devido ao acesso restrito à chave. |
| Alertas e resoluções de configuração do CMK | O Experience Platform agora aciona alertas quando os serviços da Adobe perdem acesso ao Cofre de Chaves do Azure (por exemplo, devido a entradas de inclui na lista de permissões IP removidas ou chaves desabilitadas). Um novo guia ajuda você a entender cada alerta e tomar medidas corretivas. |

Para obter mais informações, leia a [visão geral da governança de dados](../data-governance/home.md).

## Destinos {#destinations}

[!DNL Destinations] são integrações pré-construídas com plataformas de destino que permitem a ativação perfeita de dados da Adobe Experience Platform. É possível usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas de email, publicidade direcionada e muitos outros casos de uso.

**Novos destinos**

| Destino | Descrição |
| --- | --- |
| Segmentos de usuário da Algólia | O destino Segmentos de usuário da Algolia permite que profissionais de marketing forneçam personalização consistente em todos os sites, desde a home page até a pesquisa. Crie públicos-alvo avançados de várias fontes de dados e compartilhe-os em vários canais para melhorar as estratégias de direcionamento e a personalização da campanha. |

**Funcionalidade nova ou atualizada**

| Recurso | Descrição |
| --- | --- |
| Informações de expiração da conta do LinkedIn | As informações de expiração de conta para destinos do LinkedIn agora estão disponíveis diretamente nos modos de exibição [!UICONTROL Procurar] e [!UICONTROL Contas]. Anteriormente, essas informações só estavam disponíveis na documentação. Esse aprimoramento oferece melhor visibilidade do status de autenticação e do gerenciamento de credenciais do LinkedIn. |
| Correspondência de clientes da Google + disponibilidade geral e aprimoramento do DV360 | O destino Google Customer Match + DV360 agora está disponível para todos os usuários do Experience Platform. A documentação agora inclui orientações detalhadas para a vinculação de contas entre as contas de publicidade do Adobe e da Google. |
| Suporte à criptografia de destino da Zona de aterrissagem de dados (DLZ) | Adição de suporte de criptografia para o destino da Data Landing Zone. Agora é possível anexar chaves públicas formatadas em RSA para adicionar criptografia aos arquivos exportados. |
| Monitoramento no nível do público-alvo para destinos corporativos | O monitoramento no nível de público agora está disponível para os seguintes destinos corporativos: [[!DNL Azure Event Hubs]](/help/destinations/catalog/cloud-storage/azure-event-hubs.md), [[!DNL HTTP API]](/help/destinations/catalog/streaming/http-destination.md), [[!DNL Amazon Kinesis]](/help/destinations/catalog/cloud-storage/amazon-kinesis.md). |

{style="table-layout:auto"}

Para obter mais informações, leia a [Visão geral dos Destinos](../destinations/home.md).

## Composição de público-alvo federado {#fac}

A Federated Audience Composition permite que as empresas componham dados para obter uma melhor aplicação em vários casos de uso. Com essa nova abordagem, como usuário da Adobe Real-Time Customer Data Platform e/ou Adobe Journey Optimizer, você pode federar conjuntos de dados diretamente do data warehouse existente para criar e enriquecer públicos-alvo e atributos da Adobe Experience Platform, tudo em um sistema.

| Novo recurso | Descrição |
| ----------- | ----------- |
| Preparo para a HIPAA | A Federated Audience Composition agora é compatível com a HIPAA. Para obter mais informações sobre as medidas de privacidade e segurança da Federated Audience Composition, leia a [visão geral sobre privacidade e segurança na Federated Audience Composition](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/start/privacy-security). Para obter mais informações sobre a conformidade com a HIPAA para produtos da Experience Platform em geral, leia a [visão geral sobre produtos e serviços da HIPAA e da Adobe](https://www.adobe.com/trust/compliance/hipaa-ready.html). |

Para obter mais informações, leia a [documentação sobre a Composição de Público-Alvo Federado](https://experienceleague.adobe.com/pt-br/docs/federated-audience-composition/using/home).

## [!DNL Privacy Service] {#privacy}

Várias regulamentações legais e organizacionais dão aos usuários o direito de acessar ou excluir seus dados pessoais dos armazenamentos de dados, mediante solicitação. O Adobe Experience Platform [!DNL Privacy Service] fornece uma API RESTful e uma interface para ajudar você a gerenciar essas solicitações de dados de seus clientes. Com o [!DNL Privacy Service], você pode enviar solicitações para acessar e excluir dados privados ou pessoais dos clientes por meio dos aplicativos da Adobe Experience Cloud, facilitando a conformidade automatizada com as regulamentações legais e organizacionais de privacidade.

**Novos recursos**

| Recurso | Descrição |
|--- | ---|
| Suporte às leis de privacidade do Tennessee e de Minnesota | A Privacy Service agora oferece suporte à Lei de Proteção de Informações do Tennessee (`tipa_tn_usa`) e à Lei de Privacidade de Dados do Consumidor de Minnesota (`mcdpa_mn_usa`). Você pode processar solicitações de acesso e exclusão em conformidade com esses novos regulamentos de nível de estado. Consulte a [Visão geral de Regulamentos](https://experienceleague.adobe.com/en/docs/experience-platform/privacy/regulations/overview) para obter mais detalhes. |

Consulte a [visão geral do Privacy Service](../privacy-service/home.md) para obter mais informações sobre o serviço.

## Query Service {#query-service}

Consultar dados no data lake da Adobe Experience Platform usando SQL padrão com Serviço de consulta. Combine conjuntos de dados facilmente e gere novos a partir dos resultados da consulta para potencializar os relatórios, ativar fluxos de trabalho de ciência de dados ou facilitar a assimilação no Perfil do cliente em tempo real.

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Funções estatísticas avançadas | **Interseção de rascunho teta**: nova função para calcular interseções de conjunto usando rascunhos teta para contagem distinta aproximada e operações de conjunto. **Histogramas KLL**: recursos aprimorados de histograma usando rascunhos KLL (Kth menor, L maior, itens grandes) para estimativa quantil e análise de distribuição. Essas funções estão disponíveis para clientes do Data Distiller. |
| Biblioteca de Modelos SQL | Uma biblioteca abrangente de modelos SQL para casos de uso comum está disponível. Esse recurso acelera o desenvolvimento de consultas fornecendo modelos de práticas recomendadas para padrões analíticos frequentes, ajudando os clientes do Data Distiller a implementar análises complexas com mais eficiência. |

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Exemplo de modelagem RFM | Adição de um exemplo abrangente de modelagem de Recenticidade, Frequência e Monetário (RFM) para clientes do Data Distiller. Isso inclui documentação detalhada e guias de implementação para segmentação do cliente e análise de valor usando técnicas de RFM. |

{style="table-layout:auto"}

Para obter mais informações sobre [!DNL Query Service], consulte a [[!DNL Query Service] visão geral](../query-service/home.md).

## Sandboxes {#sandboxes}

O Adobe Experience Platform foi criado para enriquecer aplicativos de experiência digital em escala global. As empresas geralmente executam vários aplicativos de experiência digital em paralelo e precisam atender ao desenvolvimento, ao teste e à implantação desses aplicativos enquanto garantem a conformidade operacional.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Migração de atualizações de configuração de objeto | Agora é possível migrar atualizações de configuração de objetos iterativos em sandboxes após a replicação inicial. Esse aprimoramento suporta fluxos de trabalho de desenvolvimento em que as configurações precisam ser atualizadas e propagadas entre ambientes sem recriar toda a configuração da sandbox. |

{style="table-layout:auto"}

Para obter mais informações sobre sandboxes, leia a [visão geral das sandboxes](../sandboxes/home.md).

## Origens {#sources}

A Experience Platform fornece uma API RESTful e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar a sistemas de armazenamento externos e serviços de CRM, definir períodos para execuções de ingestão e gerenciar a taxa de transferência de ingestão de dados.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Suporte para novo tipo de autenticação para [!DNL Azure Synapse Analytics] | O [!DNL Azure Synapse Analytics] agora também oferecerá suporte à autenticação da entidade de serviço, além da autenticação da cadeia de conexão existente. |

**Atualizações importantes de autenticação**

| Atualização | Descrição |
| --- | --- |
| Descontinuação da Autenticação Básica do [!DNL Salesforce] | A Autenticação básica do Salesforce CRM e do Salesforce Service Cloud será substituída em janeiro de 2026. Os clientes devem migrar para a autenticação OAuth 2.0 para manter a conectividade. Essa alteração afeta os conectores de origem e garante maior segurança e conformidade com os padrões de autenticação da Salesforce. |

{style="table-layout:auto"}

Para obter mais informações, leia a [visão geral de fontes](../sources/home.md).
