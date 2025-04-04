---
title: Notas da versão de março de 2020 da Adobe Experience Platform
description: As notas da versão de março de 2020 da Adobe Experience Platform.
doc-type: release notes
last-update: March 10, 2020
author: ens71067
keywords: Notas de versão;
exl-id: 407c2bac-4c8a-4939-b3dd-788250f15650
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '859'
ht-degree: 17%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: quinta-feira, 11 de março de 2020**

Atualizações dos recursos já existentes na Adobe Experience Platform:

* [Governança de dados](#governance)
* [[!DNL Data Ingestion]](#ingestion)
* [[!DNL Destinations]](#destinations)
* [[!DNL Identity Service]](#identity)
* [[!DNL Sources]](#sources)

## Governança de dados {#governance}

O [!DNL Experience Platform] permite que as empresas reúnam dados de vários sistemas corporativos para melhor permitir que os profissionais de marketing identifiquem, compreendam e envolvam os clientes. O [!DNL Experience Platform] inclui uma infraestrutura completa de governança de dados para garantir o uso adequado dos dados no [!DNL Experience Platform] e quando compartilhados entre sistemas.

A Governança de dados da Adobe Experience Platform é uma série de estratégias e tecnologias usadas para gerenciar dados de clientes e garantir a conformidade com regulamentos, restrições e políticas aplicáveis ao uso de dados. Ele desempenha uma função importante no [!DNL Experience Platform] em vários níveis, incluindo catalogação, linhagem de dados, rotulagem de uso de dados, políticas de acesso a dados e controle de acesso a dados para ações de marketing.

**Novos recursos**

>[!NOTE]
>
>Alguns dos novos recursos a seguir estão atualmente na versão beta e não estão disponíveis para todos os usuários. Os recursos do Beta estão sujeitos a alterações.

| Recurso | Descrição |
| ------- | ----------- |
| Aplicação automatizada de políticas de uso de dados para [!DNL Real-Time Customer Data Platform] | As políticas de uso de dados agora são aplicadas no fluxo de trabalho de ativação de dados para destinos. A Governança de dados também é incorporada e aplicada ao fazer alterações que afetam as ativações existentes (como alterações nos rótulos do conjunto de dados, políticas de mesclagem, definições de segmento e outras). |
| Linhagem de dados para aplicação | Quando uma política de uso de dados é violada no Real-Time CDP, a interface do usuário exibe uma notificação que contém informações de linhagem de dados para ajudar o usuário a entender por que as políticas foram violadas e o que podem fazer para resolver a violação. |


**Problemas conhecidos**

* None

Para obter mais informações sobre Governança de dados, consulte a [visão geral sobre Governança de dados](../../data-governance/home.md).

## Assimilação de dados {#ingestion}

O Adobe Experience Platform fornece um conjunto avançado de recursos para assimilar qualquer tipo e latência de dados. O Adobe Experience Platform [!DNL Data Ingestion] fornece várias alternativas para assimilação de dados, incluindo APIs em lote, APIs de streaming, conectores nativos do Adobe, parceiros de integração de dados ou a interface do usuário do Adobe Experience Platform.

**Novos recursos**

| Recurso | Descrição |
|------- | -----------|
| Assimilação parcial de lote | A assimilação parcial de lotes é a capacidade de assimilar dados que contêm erros até um determinado limite. Com esse recurso, os usuários podem assimilar todos os dados corretos na Adobe Experience Platform com sucesso, enquanto todos os dados incorretos são armazenados em lote separadamente. Detalhes são adicionados aos lotes malsucedidos para explicar por que eles não passaram na validação. Mais informações sobre assimilação parcial de lotes podem ser encontradas na [documentação de assimilação parcial de lotes](../../ingestion/batch-ingestion/partial.md). |

**Problemas conhecidos**

* None

Para saber mais sobre assimilação de dados na Experience Platform, visite a [documentação de Assimilação de dados](../../ingestion/home.md).


## Destinos {#destinations}

No [Real-Time Customer Data Platform](../../rtcdp/overview.md), os destinos são integrações pré-criadas com plataformas de destino que ativam dados para esses parceiros de forma contínua.

**Novos destinos**

Novos destinos estão disponíveis onde você pode ativar os dados do Adobe Experience Platform. Veja os detalhes abaixo:

| Destino | Descrição |
|--- | ---|
| Destinos de armazenamento na nuvem | Agora a Real-Time CDP pode entregar seus segmentos como arquivos de dados para seus locais de armazenamento na nuvem [!DNL Amazon S3] ou SFTP. Isso permite enviar públicos-alvo e seus atributos de perfil para os sistemas internos, por meio de arquivos CSV ou delimitados por tabulação. |
| Destinos do Advertising | A placa de destino [!DNL Google] agora está dividida em três placas de destino, para as três plataformas [!DNL Google] diferentes atualmente compatíveis com o Real-Time CDP: [!DNL Google Ads], [!DNL Google Ad Manager], [!DNL Google] Display &amp; Video 360. |

Para saber mais, visite a [visão geral de destinos](../../destinations/home.md)

## [!DNL Identity Service] {#identity}

Para fornecer experiências digitais relevantes, é necessário ter uma compreensão completa do cliente. Isso se torna mais difícil quando os dados do cliente são fragmentados em sistemas diferentes, fazendo com que cada cliente individual pareça ter várias &quot;identidades&quot;.

O Adobe Experience Platform [!DNL Identity Service] ajuda você a ter uma melhor visão do seu cliente e do comportamento dele unindo identidades de vários dispositivos e sistemas, permitindo que você forneça experiências digitais pessoais e impactantes em tempo real.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Gráfico privado aprimorado | A funcionalidade de Gráfico privado foi aprimorada para reduzir a latência de geração de gráficos de um processo em lote semanal para um gráfico atualizado diário, permitindo que [!DNL Identity Service] clientes acessem gráficos de identidade e links mais atualizados. |

**Problemas conhecidos**

* None

Para obter mais informações sobre [!DNL Identity Service], consulte a [visão geral do Serviço de Identidade](../../identity-service/home.md).

## Origens {#sources}

O Adobe Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, permitir que você estruture, rotule e aprimore esses dados usando os serviços do [!DNL Experience Platform]. É possível assimilar dados de várias origens, como aplicativos da Adobe, do armazenamento na nuvem, um software de terceiros e do seu sistema de CRM.

O [!DNL Experience Platform] fornece uma API RESTful e uma interface do usuário interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar a sistemas de armazenamento externos e serviços de CRM, definir períodos para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Sinais obsoletos para o conector do Adobe Audience Manager | Os dados de nível de sinal do Audience Manager não serão mais enviados. Observe que a associação de segmento para Características e Segmentos ainda será incluída. Como resultado dessa alteração, os conjuntos de dados de entrada não serão mais gerados. |
| Conjuntos de dados renomeados | Os conjuntos de dados gerados pelo conector do Audience Manager terão nomes e descrições atualizados. |
| Ativar a opção [!DNL Profile] no Audience Manager | A opção [!DNL Profile] pode ser habilitada ou desabilitada para promover o conjunto de dados a [!DNL Real-Time Customer Profile]. A alternância será ativada por padrão. |
| Suporte à interface do usuário para sistemas de armazenamento em nuvem | Novo conector de origem para [!DNL Azure Data Lake Storage Gen2] na interface do usuário. |
| Suporte à interface do usuário para sistemas de CRM | Novo conector de origem para [!DNL HubSpot], [!DNL Salesforce Service Cloud] e [!DNL ServiceNow] na interface do usuário. |
| Suporte à interface do usuário para sistemas de banco de dados | Novo conector de origem para [!DNL AWS Redshift], [!DNL Google BigQuery], [!DNL MariaDB], [!DNL Microsoft SQL Server] e [!DNL MySQL] na interface. |

**Problemas conhecidos**

* None

Para saber mais sobre fontes, consulte a [visão geral das fontes](../../sources/home.md).
