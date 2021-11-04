---
title: Notas de versão da Adobe Experience Platform
description: Notas de versão do Experience Platform 11 de março de 2020
doc-type: release notes
last-update: March 10, 2020
author: ens71067
keywords: notas de versão;
exl-id: 407c2bac-4c8a-4939-b3dd-788250f15650
source-git-commit: 03e7863f38b882a2fbf6ba0de1755e1924e8e228
workflow-type: tm+mt
source-wordcount: '851'
ht-degree: 7%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 11 de março de 2020**

Atualizações dos recursos existentes na Adobe Experience Platform:

* [Governança de dados](#governance)
* [[!DNL Data Ingestion]](#ingestion)
* [[!DNL Destinations]](#destinations)
* [[!DNL Identity Service]](#identity)
* [[!DNL Sources]](#sources)

## Governança de dados {#governance}

[!DNL Experience Platform] O permite que as empresas reúnam dados de vários sistemas corporativos para melhor permitir que os profissionais de marketing identifiquem, entendam e envolvam clientes. [!DNL Experience Platform] inclui uma infraestrutura completa de governança de dados para garantir o uso adequado dos dados no [!DNL Platform] e quando compartilhado entre sistemas.

A Governança de dados da Adobe Experience Platform é uma série de estratégias e tecnologias usadas para gerenciar dados de clientes e garantir a conformidade com regulamentos, restrições e políticas aplicáveis ao uso de dados. Ele desempenha um papel fundamental no [!DNL Experience Platform] em vários níveis, incluindo catalogação, linhagem de dados, rotulagem de uso de dados, políticas de acesso a dados e controle de acesso a dados para ações de marketing.

**Novos recursos**

>[!NOTE]
>
>Alguns dos novos recursos a seguir estão atualmente na versão beta e não estão disponíveis para todos os usuários. Os recursos beta estão sujeitos a alterações.

| Recurso | Descrição |
| ------- | ----------- |
| Aplicação automatizada de políticas de uso de dados para [!DNL Real-time Customer Data Platform] | As políticas de uso de dados agora são aplicadas no fluxo de trabalho da ativação de dados para destinos. A Governança de dados também é incorporada e aplicada ao fazer alterações que afetam as ativações existentes (como alterações nos rótulos do conjunto de dados, políticas de mesclagem, definições de segmento e outras). |
| Linguagem de dados para aplicação | Quando uma política de uso de dados é violada na CDP em tempo real, a interface do usuário exibe uma notificação que contém informações de linhagem de dados para ajudar o usuário a entender por que as políticas foram violadas e o que ele pode fazer para resolver a violação. |


**Problemas conhecidos**

* None

Para obter mais informações sobre a Governança de dados, consulte [Visão geral da governança de dados](../../data-governance/home.md).

## Assimilação de dados {#ingestion}

O Adobe Experience Platform fornece um conjunto avançado de recursos para assimilar qualquer tipo e latência de dados. Adobe Experience Platform [!DNL Data Ingestion] O fornece várias alternativas para assimilar dados, incluindo APIs em lote, APIs de streaming, conectores nativos do Adobe, parceiros de integração de dados ou a interface do usuário da Adobe Experience Platform.

**Novos recursos**

| Recurso | Descrição |
|------- | -----------|
| Ingestão parcial por lote | A assimilação parcial em lote é a capacidade de assimilar dados que contêm erros, até um determinado limite. Com esse recurso, os usuários podem assimilar com êxito todos os dados corretos no Adobe Experience Platform, enquanto todos os dados incorretos são armazenados em lote separadamente. Detalhes são adicionados a lotes sem sucesso para explicar por que eles não passaram na validação. Mais informações sobre a ingestão parcial de lote podem ser encontradas no [documentação de ingestão em lote parcial](../../ingestion/batch-ingestion/partial.md). |

**Problemas conhecidos**

* Nenhum

Para saber mais sobre como assimilar dados no Platform, visite a [Documentação da assimilação de dados](../../ingestion/home.md).


## Destinos {#destinations}

Em [Real-time Customer Data Platform](../../rtcdp/overview.md), os destinos são integrações pré-criadas com plataformas de destino que ativam os dados para esses parceiros de forma contínua.

**Novos destinos**

Novos destinos estão disponíveis, onde você pode ativar os dados do Adobe Experience Platform. Veja os detalhes abaixo:

| Destino | Descrição |
|--- | ---|
| Destinos de armazenamento na nuvem | A CDP em tempo real agora pode fornecer seus segmentos como arquivos de dados para o [!DNL Amazon S3] ou locais de armazenamento em nuvem SFTP. Isso permite enviar públicos-alvo e seus atributos de perfil para seus sistemas internos, por meio de arquivos CSV ou delimitados por tabulação. |
| Destinos de publicidade | O [!DNL Google] o cartão de destino agora é dividido em três cartões de destino, para os três diferentes [!DNL Google] plataformas atualmente compatíveis com a CDP em tempo real: [!DNL Google Ads], [!DNL Google Ad Manager], [!DNL Google] Exibição e vídeo 360. |

Para saber mais, visite o [visão geral dos destinos](../../destinations/home.md)

## [!DNL Identity Service] {#identity}

Fornecer experiências digitais relevantes requer ter uma compreensão completa do cliente. Isso fica mais difícil quando os dados do cliente são fragmentados em sistemas diferentes, fazendo com que cada cliente individual pareça ter várias &quot;identidades&quot;.

Adobe Experience Platform [!DNL Identity Service] O ajuda você a obter uma melhor visão de seu cliente e de seu comportamento ao unir identidades em dispositivos e sistemas, permitindo que você forneça experiências digitais pessoais e impactantes em tempo real.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Gráfico privado aprimorado | A funcionalidade de Gráfico privado foi aprimorada para reduzir a latência de geração de gráficos de um processo em lote semanal para um gráfico atualizado diário, permitindo [!DNL Identity Service] para acessar gráficos de identidade e links mais atualizados. |

**Problemas conhecidos**

* Nenhum

Para obter mais informações sobre [!DNL Identity Service], consulte o [Visão geral do Serviço de identidade](../../identity-service/home.md).

## Fontes {#sources}

O Adobe Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, permitir estruturar, rotular e aprimorar esses dados usando [!DNL Platform] serviços. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

[!DNL Experience Platform] O fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e se conectar a sistemas de armazenamento externos e serviços CRM, definir horários para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Sinais obsoletos para o conector Adobe Audience Manager | Os dados a nível de sinal do Audience Manager não serão mais enviados. Observe que a associação de segmentos para Características e segmentos ainda será incluída. Como resultado dessa alteração, os conjuntos de dados de entrada não serão mais gerados. |
| Conjuntos de dados renomeados | Os conjuntos de dados gerados pelo conector do Audience Manager terão nomes e descrições atualizados. |
| Habilitar [!DNL Profile] alternar no Audience Manager | [!DNL Profile] alternar pode ser ativado ou desativado para promover o conjunto de dados para [!DNL Real-time Customer Profile]. Alternar será ativado por padrão. |
| Suporte à interface do usuário para sistemas de armazenamento em nuvem | Novo conector de origem para [!DNL Azure Data Lake Storage Gen2] na interface do usuário do . |
| Suporte à interface do usuário para sistemas CRM | Novo conector de origem para [!DNL HubSpot], [!DNL Salesforce Service Cloud]e [!DNL ServiceNow] na interface do usuário do . |
| Suporte à interface do usuário para sistemas de banco de dados | Novo conector de origem para [!DNL AWS Redshift], [!DNL Google BigQuery], [!DNL MariaDB], [!DNL Microsoft SQL Server]e [!DNL MySQL] na interface do usuário do . |

**Problemas conhecidos**

* Nenhum

Para saber mais sobre fontes, consulte o [visão geral das fontes](../../sources/home.md).
