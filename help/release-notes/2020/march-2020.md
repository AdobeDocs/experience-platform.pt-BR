---
title: 'Notas de versão do Adobe Experience Platform '
description: Notas de versão da plataforma Experience 11 de março de 2020
doc-type: release notes
last-update: March 10, 2020
author: ens71067
keywords: release notes;
translation-type: tm+mt
source-git-commit: 33ce1e83514d7aa3cdc5fcee66f444d2fd203097

---


# Notas de versão da Adobe Experience Platform

## Data de lançamento: 11 de março de 2020

## Governança de dados

A plataforma Experience permite que as empresas reúnam dados de vários sistemas corporativos para melhor permitir que os profissionais de marketing identifiquem, entendam e engajem os clientes. A plataforma de experiência inclui uma infraestrutura completa de controle de dados, incluindo a DULE (Data Usage Labeling and Implementation), para garantir o uso correto dos dados dentro da plataforma e quando compartilhados entre sistemas.

O Adobe Experience Platform Data Governance é uma série de estratégias e tecnologias usadas para gerenciar dados de clientes e garantir a conformidade com regulamentos, restrições e políticas aplicáveis ao uso de dados. Ele desempenha um papel fundamental na plataforma da experiência em vários níveis, incluindo catalogação, linhagem de dados, rotulagem de uso de dados, políticas de acesso a dados e controle de acesso de dados para ações de marketing.

### Novos recursos

>[!NOTE] Alguns dos novos recursos a seguir estão atualmente em beta e não estão disponíveis para todos os usuários. Os recursos Beta estão sujeitos a alterações.

| Recurso | Descrição |
| ------- | ----------- |
| Aplicação automatizada das políticas de uso de dados para a Plataforma de dados do cliente em tempo real | As políticas de uso de dados agora são aplicadas no fluxo de trabalho de ativação de dados para destinos. O controle de dados também é incorporado e aplicado ao fazer alterações que afetam ativações existentes (como alterações em rótulos de conjuntos de dados, políticas de mesclagem, definições de segmentos e outros). |
| Linha de dados para aplicação | Quando uma política de uso de dados é violada no CDP em tempo real, a interface do usuário exibe uma notificação que contém informações de linhagem de dados para ajudar o usuário a entender por que as políticas foram violadas e o que podem fazer para resolver a violação. |


### Problemas conhecidos

* Nenhum

Para obter mais informações sobre o Data Governance, consulte a visão geral [](../../data-governance/home.md)do Data Governance.

## Ingestão de dados

A plataforma Adobe Experience fornece um conjunto avançado de recursos para assimilar qualquer tipo e latência de dados. A assimilação de dados da plataforma Adobe Experience oferece várias alternativas para a assimilação de dados, incluindo APIs em lote, APIs de fluxo, conectores nativos da Adobe, parceiros de integração de dados ou a interface do usuário da plataforma Adobe Experience.

### Novos recursos

| Recurso | Descrição |
|------- | -----------|
| Ingestão parcial em lote | A ingestão parcial em lote é a capacidade de assimilar dados que contenham erros, até um certo limite. Com esse recurso, os usuários podem assimilar com êxito todos os dados corretos na Adobe Experience Platform, enquanto todos os dados incorretos são armazenados em lote separadamente. Os detalhes são adicionados aos lotes com falha para explicar por que eles não passaram na validação. Para mais informações sobre a ingestão parcial do lote, consultar a documentação [relativa à ingestão](../../ingestion/batch-ingestion/partial.md)parcial do lote. |

### Problemas conhecidos

* Nenhum

Para saber mais sobre como ingerir dados na plataforma, visite a documentação [de ingestão de](../../ingestion/home.md)dados.


## Destinos

Na Plataforma [de dados do cliente em tempo real da](../../rtcdp/overview.md)Adobe, os destinos são integrações pré-criadas com plataformas de destino que ativam os dados para esses parceiros de forma contínua.

### Novos destinos

Novos destinos estão disponíveis onde você pode ativar seus dados da plataforma Adobe Experience. Consulte abaixo para obter detalhes:

| Destino | Descrição |
|--- | ---|
| Destinos de armazenamentos na nuvem | A Adobe Real-time CDP agora pode fornecer seus segmentos como arquivos de dados para os locais do armazenamento em nuvem Amazon S3 ou SFTP. Isso permite que você envie audiências e seus atributos de perfil para seus sistemas internos, por meio de arquivos CSV ou delimitados por tabulação. |
| Destinos de publicidade | A placa de destino do Google agora é dividida em três placas de destino, para as três plataformas diferentes do Google atualmente suportadas pela CDP em tempo real da Adobe: Google Ads, Google Ad Manager, Google Display e Video 360. |

Para saber mais, visite a visão geral de [destinos](../../rtcdp/destinations/destinations-overview.md)

## Serviço de identidade

Fornecer experiências digitais relevantes requer uma compreensão completa do cliente. Isso fica mais difícil quando os dados do cliente são fragmentados em sistemas diferentes, fazendo com que cada cliente individual pareça ter várias &quot;identidades&quot;.

O Adobe Experience Platform Identity Service ajuda você a obter uma melhor visualização de seu cliente e de seu comportamento ao unir identidades entre dispositivos e sistemas, permitindo que você forneça experiências digitais pessoais e de impacto em tempo real.

### Novos recursos

| Recurso | Descrição |
| ------- | ----------- |
| Gráfico privado aprimorado | A funcionalidade Gráfico privado foi aprimorada para reduzir a latência de geração de gráficos de um processo em lote semanal para um gráfico atualizado diário, permitindo que os clientes do Serviço de identidade acessem gráficos de identidade e links mais atualizados. |

### Problemas conhecidos

* Nenhum

Para obter mais informações sobre o Serviço de identidade, consulte a visão geral [do Serviço de](../../identity-service/home.md)identidade.

## Fontes

A plataforma Adobe Experience pode assimilar dados de fontes externas, permitindo que você estruture, rotule e aprimore esses dados usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos da Adobe, armazenamentos baseados em nuvem, software de terceiros e seu sistema de CRM.

A plataforma Experience fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem que você se autentique e se conecte a sistemas de armazenamentos externos e serviços CRM, defina horários para execuções de ingestão e gerencie a throughput de ingestão de dados.

### Novos recursos

| Recurso | Descrição |
| ------- | ----------- |
| Sinais preteridos para o conector do Adobe Audiência Manager | Os dados de nível de sinal do Gerenciador de Audiências não serão mais enviados. Observe que a associação de segmento para Características e segmentos ainda será incluída. Como resultado dessa alteração, os conjuntos de dados de entrada não serão mais gerados. |
| Conjuntos de dados renomeados | Os conjuntos de dados gerados pelo conector do Gerenciador de Audiências terão nomes e descrições atualizados. |
| Ative a alternância de Perfis no Gerenciador de Audiências | A alternância de Perfis pode ser ativada ou desativada para promover o conjunto de dados para o Perfil Cliente em tempo real. Alternar será ativado por padrão. |
| Suporte de interface para sistemas de armazenamentos em nuvem | Novo conector de origem para o Armazenamento Gen2 do Azure Data Lake na interface do usuário. |
| Suporte de interface para sistemas CRM | Novo conector de origem para HubSpot, Salesforce Service Cloud e ServiceNow na interface do usuário. |
| Suporte de interface para sistemas de banco de dados | Novo conector de origem para AWS Redshift, Google BigQuery, MariaDB, Microsoft SQL Server e MySQL na interface do usuário. |

### Problemas conhecidos

* Nenhum

Para saber mais sobre fontes, consulte a visão geral [das](../../sources/home.md)fontes.