---
title: Notas de versão da Adobe Experience Platform de março de 2020
description: As notas de versão de março de 2020 para o Adobe Experience Platform.
doc-type: release notes
last-update: March 10, 2020
author: ens71067
keywords: notas de versão;
exl-id: 407c2bac-4c8a-4939-b3dd-788250f15650
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '855'
ht-degree: 6%

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

[!DNL Experience Platform] O permite que as empresas reúnam dados de vários sistemas corporativos para melhor permitir que os profissionais de marketing identifiquem, compreendam e envolvam os clientes. [!DNL Experience Platform] inclui uma infraestrutura completa de controle de dados para garantir o uso adequado dos dados em [!DNL Platform] e quando compartilhados entre sistemas.

O Adobe Experience Platform Data Governance é uma série de estratégias e tecnologias usadas para gerenciar dados de clientes e garantir conformidade com normas, restrições e políticas aplicáveis ao uso de dados. Desempenha um papel fundamental na [!DNL Experience Platform] em vários níveis, incluindo catalogação, linhagem de dados, rotulagem de uso de dados, políticas de acesso a dados e controle de acesso a dados para ações de marketing.

**Novos recursos**

>[!NOTE]
>
>Alguns dos novos recursos a seguir estão atualmente na versão beta e não estão disponíveis para todos os usuários. Os recursos beta estão sujeitos a alterações.

| Recurso | Descrição |
| ------- | ----------- |
| Aplicação automatizada de políticas de uso de dados para [!DNL Real-Time Customer Data Platform] | As políticas de uso de dados agora são aplicadas no fluxo de trabalho de ativação de dados para destinos. A Governança de dados também é incorporada e aplicada ao fazer alterações que afetam as ativações existentes (como alterações nos rótulos do conjunto de dados, políticas de mesclagem, definições de segmento e outras). |
| Linhagem de dados para aplicação | Quando uma política de uso de dados é violada no Real-Time CDP, a interface do usuário exibe uma notificação que contém informações de linhagem de dados para ajudar o usuário a entender por que as políticas foram violadas e o que podem fazer para resolver a violação. |


**Problemas conhecidos**

* None

Para obter mais informações sobre a Governança de dados, consulte a [Visão geral da governança de dados](../../data-governance/home.md).

## Assimilação de dados {#ingestion}

O Adobe Experience Platform fornece um conjunto avançado de recursos para assimilar qualquer tipo e latência de dados. Adobe Experience Platform [!DNL Data Ingestion] O fornece várias alternativas para assimilação de dados, incluindo APIs de lote, APIs de streaming, conectores de Adobe nativos, parceiros de integração de dados ou a interface do usuário do Adobe Experience Platform.

**Novos recursos**

| Recurso | Descrição |
|------- | -----------|
| Assimilação parcial de lote | A assimilação parcial de lotes é a capacidade de assimilar dados que contêm erros até um determinado limite. Com esse recurso, os usuários podem assimilar todos os dados corretos na Adobe Experience Platform com sucesso, enquanto todos os dados incorretos são armazenados em lote separadamente. Detalhes são adicionados aos lotes malsucedidos para explicar por que eles não passaram na validação. Mais informações sobre assimilação parcial de lotes podem ser encontradas no [documentação de assimilação parcial de lotes](../../ingestion/batch-ingestion/partial.md). |

**Problemas conhecidos**

* None

Para saber mais sobre a assimilação de dados na Platform, visite o [Documentação de assimilação de dados](../../ingestion/home.md).


## Destinos {#destinations}

Entrada [Real-time Customer Data Platform](../../rtcdp/overview.md), os destinos são integrações pré-criadas com plataformas de destino que ativam os dados para esses parceiros de forma contínua.

**Novos destinos**

Novos destinos estão disponíveis onde você pode ativar os dados do Adobe Experience Platform. Veja os detalhes abaixo:

| Destino | Descrição |
|--- | ---|
| Destinos de armazenamento na nuvem | O Real-Time CDP agora pode fornecer seus segmentos como arquivos de dados para o seu [!DNL Amazon S3] ou locais de armazenamento na nuvem SFTP. Isso permite enviar públicos-alvo e seus atributos de perfil para os sistemas internos, por meio de arquivos CSV ou delimitados por tabulação. |
| Destinos de publicidade | A variável [!DNL Google] cartão de destino é agora dividido em três cartões de destino, para os três [!DNL Google] plataformas atualmente compatíveis com o Real-Time CDP: [!DNL Google Ads], [!DNL Google Ad Manager], [!DNL Google] Vídeo e tela 360. |

Para saber mais, visite o [visão geral dos destinos](../../destinations/home.md)

## [!DNL Identity Service] {#identity}

Para fornecer experiências digitais relevantes, é necessário ter uma compreensão completa do cliente. Isso se torna mais difícil quando os dados do cliente são fragmentados em sistemas diferentes, fazendo com que cada cliente individual pareça ter várias &quot;identidades&quot;.

Adobe Experience Platform [!DNL Identity Service] O ajuda você a obter uma melhor visualização do cliente e do comportamento dele, unindo identidades em dispositivos e sistemas, permitindo que você forneça experiências digitais pessoais e impactantes em tempo real.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Gráfico privado aprimorado | A funcionalidade de gráfico privado foi aprimorada para reduzir a latência de geração de gráficos de um processo em lote semanal para um gráfico atualizado diário, permitindo [!DNL Identity Service] clientes para acessar gráficos de identidade e links mais atualizados. |

**Problemas conhecidos**

* None

Para obter mais informações sobre [!DNL Identity Service], consulte o [Visão geral do serviço de identidade](../../identity-service/home.md).

## Fontes {#sources}

O Adobe Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, permitir estruturar, rotular e aprimorar esses dados usando [!DNL Platform] serviços. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

[!DNL Experience Platform] O fornece uma API RESTful e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar a sistemas de armazenamento externos e serviços de CRM, definir tempos para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Sinais obsoletos para o conector do Adobe Audience Manager | Os dados de nível de sinal do Audience Manager não serão mais enviados. Observe que a associação de segmento para Características e Segmentos ainda será incluída. Como resultado dessa alteração, os conjuntos de dados de entrada não serão mais gerados. |
| Conjuntos de dados renomeados | Os conjuntos de dados gerados pelo conector do Audience Manager terão nomes e descrições atualizados. |
| Ativar [!DNL Profile] alternar no Audience Manager | [!DNL Profile] pode ser ativada ou desativada para promover o conjunto de dados a [!DNL Real-Time Customer Profile]. A alternância será ativada por padrão. |
| Suporte à interface do usuário para sistemas de armazenamento em nuvem | Novo conector de origem para [!DNL Azure Data Lake Storage Gen2] na interface. |
| Suporte à interface do usuário para sistemas de CRM | Novo conector de origem para [!DNL HubSpot], [!DNL Salesforce Service Cloud], e [!DNL ServiceNow] na interface. |
| Suporte à interface do usuário para sistemas de banco de dados | Novo conector de origem para [!DNL AWS Redshift], [!DNL Google BigQuery], [!DNL MariaDB], [!DNL Microsoft SQL Server], e [!DNL MySQL] na interface. |

**Problemas conhecidos**

* None

Para saber mais sobre fontes, consulte a [visão geral das origens](../../sources/home.md).
