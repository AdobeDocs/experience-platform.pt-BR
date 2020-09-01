---
title: 'Notas de versão do Adobe Experience Platform '
description: Notas de versão de Experience Platform 11 de março de 2020
doc-type: release notes
last-update: March 10, 2020
author: ens71067
keywords: release notes;
translation-type: tm+mt
source-git-commit: 0f3a4ba6ad96d2226ae5094fa8b5073152df90f7
workflow-type: tm+mt
source-wordcount: '854'
ht-degree: 5%

---


# Notas de versão da Adobe Experience Platform

**Data de lançamento: 11 de março de 2020**

Atualizações dos recursos existentes no Adobe Experience Platform:

* [[!DNL Data Governance]](#governance)
* [[!Ingestão de Dados DNL]](#ingestion)
* [[!Destinos DNL]](#destinations)
* [[!DNL Identity Service]](#identity)
* [[!Fontes DNL]](#sources)

## [!DNL Data Governance] {#governance}

[!DNL Experience Platform] permite que as empresas reúnam dados de vários sistemas corporativos para melhor permitir que os profissionais de marketing identifiquem, entendam e envolvam clientes. [!DNL Experience Platform] inclui uma infraestrutura completa de controle de dados para garantir o uso adequado dos dados dentro [!DNL Platform] e quando compartilhados entre sistemas.

A Adobe Experience Platform [!DNL Data Governance] é uma série de estratégias e tecnologias usadas para gerenciar dados de clientes e garantir a conformidade com regulamentos, restrições e políticas aplicáveis ao uso de dados. Ele desempenha um papel fundamental em vários [!DNL Experience Platform] níveis, incluindo catalogação, linhagem de dados, rotulagem de uso de dados, políticas de acesso a dados e controle de acesso de dados para ações de marketing.

**Novos recursos**

>[!NOTE]
>
>Alguns dos novos recursos a seguir estão atualmente em beta e não estão disponíveis para todos os usuários. Os recursos Beta estão sujeitos a alterações.

| Recurso | Descrição |
| ------- | ----------- |
| Aplicação automatizada de políticas de uso de dados para [!DNL Real-time Customer Data Platform] | As políticas de uso de dados agora são aplicadas no fluxo de trabalho de ativação de dados para destinos. [!DNL Data Governance] também é incorporado e aplicado ao fazer alterações que afetam ativações existentes (como alterações em rótulos de conjuntos de dados, políticas de mesclagem, definições de segmentos e outros). |
| Linha de dados para aplicação | Quando uma política de uso de dados é violada no CDP em tempo real, a interface do usuário exibe uma notificação que contém informações de linhagem de dados para ajudar o usuário a entender por que as políticas foram violadas e o que podem fazer para resolver a violação. |


**Problemas conhecidos**

* None

Para obter mais informações sobre [!DNL Data Governance], consulte a visão geral [do](../../data-governance/home.md)Data Governance.

## Ingestão de dados {#ingestion}

A Adobe Experience Platform fornece um conjunto avançado de recursos para assimilar qualquer tipo e latência de dados. A Adobe Experience Platform [!DNL Data Ingestion] oferece várias alternativas para assimilar dados, incluindo APIs em lote, APIs de transmissão, conectores nativos de Adobe, parceiros de integração de dados ou a interface do usuário Adobe Experience Platform.

**Novos recursos**

| Recurso | Descrição |
|------- | -----------|
| Ingestão parcial em lote | A ingestão parcial em lote é a capacidade de assimilar dados que contenham erros, até um certo limite. Com esse recurso, os usuários podem assimilar com êxito todos os dados corretos no Adobe Experience Platform enquanto todos os dados incorretos são armazenados em lote separadamente. Os detalhes são adicionados aos lotes com falha para explicar por que eles não passaram na validação. Para mais informações sobre a ingestão parcial do lote, consultar a documentação [relativa à ingestão](../../ingestion/batch-ingestion/partial.md)parcial do lote. |

**Problemas conhecidos**

* None

Para saber mais sobre como ingerir dados na Plataforma, visite a documentação [de ingestão de](../../ingestion/home.md)dados.


## Destinos {#destinations}

Na Plataforma [de dados do cliente em tempo real do](../../rtcdp/overview.md)Adobe, os destinos são integrações pré-criadas com plataformas de destino que ativam os dados para esses parceiros de forma contínua.

**Novos destinos**

Novos destinos estão disponíveis onde você pode ativar seus dados do Adobe Experience Platform. Consulte abaixo para obter detalhes:

| Destino | Descrição |
|--- | ---|
| Destinos de armazenamentos na nuvem | A CDP em tempo real do Adobe agora pode fornecer seus segmentos como arquivos de dados para seus locais de armazenamento em nuvem [!DNL Amazon S3] ou SFTP. Isso permite que você envie audiências e seus atributos de perfil para seus sistemas internos, por meio de arquivos CSV ou delimitados por tabulação. |
| Destinos de publicidade | A placa de [!DNL Google] destino agora é dividida em três placas de destino, para as três [!DNL Google] plataformas diferentes atualmente suportadas no CDP em tempo real do Adobe: [!DNL Google Ads], [!DNL Google Ad Manager], [!DNL Google] Exibir e vídeo 360. |

Para saber mais, visite a visão geral de [destinos](../../rtcdp/destinations/destinations-overview.md)

## [!DNL Identity Service] {#identity}

Fornecer experiências digitais relevantes requer uma compreensão completa do cliente. Isso fica mais difícil quando os dados do cliente são fragmentados em sistemas diferentes, fazendo com que cada cliente individual pareça ter várias &quot;identidades&quot;.

A Adobe Experience Platform [!DNL Identity Service] ajuda você a obter uma melhor visualização de seu cliente e de seu comportamento ao unir identidades entre dispositivos e sistemas, permitindo que você forneça experiências digitais pessoais e de impacto em tempo real.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Gráfico privado aprimorado | A funcionalidade Gráfico privado foi aprimorada para reduzir a latência de geração de gráficos de um processo em lote semanal para um gráfico atualizado diário, permitindo que [!DNL Identity Service] os clientes acessem gráficos de identidade e links mais atualizados. |

**Problemas conhecidos**

* None

Para obter mais informações sobre [!DNL Identity Service], consulte a visão geral [do Serviço de](../../identity-service/home.md)identidade.

## Fontes {#sources}

A Adobe Experience Platform pode assimilar dados de fontes externas, permitindo que você estruture, rotule e aprimore esses dados usando [!DNL Platform] serviços. Você pode assimilar dados de várias fontes, como aplicativos de Adobe, armazenamentos baseados em nuvem, software de terceiros e seu sistema de CRM.

[!DNL Experience Platform] fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem que você se autentique e se conecte a sistemas de armazenamentos externos e serviços CRM, defina horários para execuções de ingestão e gerencie a throughput de ingestão de dados.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Sinais preteridos para o conector Adobe Audience Manager | Os dados de nível de sinal do Gerenciador de Audiências não serão mais enviados. Observe que a associação de segmento para Características e segmentos ainda será incluída. Como resultado dessa alteração, os conjuntos de dados de entrada não serão mais gerados. |
| Conjuntos de dados renomeados | Os conjuntos de dados gerados pelo conector do Gerenciador de Audiências terão nomes e descrições atualizados. |
| Ativar [!DNL Profile] alternância no Gerenciador de Audiências | [!DNL Profile] alternância pode ser ativada ou desativada para promover o conjunto de dados para [!DNL Real-time Customer Profile]. Alternar será ativado por padrão. |
| Suporte de interface para sistemas de armazenamentos em nuvem | Novo conector de origem para [!DNL Azure Data Lake Storage Gen2] na interface do usuário. |
| Suporte de interface para sistemas CRM | Novo conector de fonte para [!DNL HubSpot], [!DNL Salesforce Service Cloud]e [!DNL ServiceNow] na interface do usuário. |
| Suporte de interface para sistemas de banco de dados | Novo conector de fonte para [!DNL AWS Redshift], [!DNL Google BigQuery], [!DNL MariaDB], [!DNL Microsoft SQL Server]e [!DNL MySQL] na interface do usuário. |

**Problemas conhecidos**

* None

Para saber mais sobre fontes, consulte a visão geral [das](../../sources/home.md)fontes.