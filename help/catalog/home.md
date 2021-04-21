---
keywords: Experience Platform, home, tópicos populares, serviço de catálogo, catálogo, serviço de catálogo, localização de dados, gestão de dados, gestão de dados, linhagem, catálogo, ativar conjunto de dados
solution: Experience Platform
title: Visão geral do serviço de catálogo
topic-legacy: overview
description: O Serviço de catálogo é o sistema de registro para localização e linhagem de dados no Adobe Experience Platform. Embora todos os dados assimilados no Experience Platform sejam armazenados no Data Lake como arquivos e diretórios, o Catalog retém os metadados e a descrição desses arquivos e diretórios para fins de pesquisa e monitoramento.
exl-id: ef0c173b-607b-41b8-8676-c54ae9472e23
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 5%

---

# [!DNL Catalog Service]visão geral

[!DNL Catalog Service] é o sistema de registro para localização e linhagem de dados no Adobe Experience Platform. Embora todos os dados assimilados em [!DNL Experience Platform] sejam armazenados no [!DNL Data Lake] como arquivos e diretórios, [!DNL Catalog] retém os metadados e a descrição desses arquivos e diretórios para fins de pesquisa e monitoramento.

Simplificando, [!DNL Catalog] atua como um armazenamento de metadados ou &quot;catálogo&quot;, onde você pode encontrar informações sobre seus dados em [!DNL Experience Platform]. Você pode usar [!DNL Catalog] para responder as seguintes perguntas:

* Onde meus dados estão localizados?
* Em que fase de processamento se encontram esses dados?
* Quais sistemas ou processos agiram em meus dados?
* Quantos dados foram processados com êxito?
* Quais erros ocorreram durante o processamento?

[!DNL Catalog] O fornece uma RESTful API que permite gerenciar programaticamente  [!DNL Platform] metadados usando operações básicas de CRUD. Consulte o [Guia do desenvolvedor do catálogo](api/getting-started.md) para obter mais informações.

## [!DNL Catalog] e  [!DNL Experience Platform] serviços

Os recursos que [!DNL Catalog Service] rastreia são usados por vários serviços [!DNL Experience Platform]. Para aproveitar ao máximo os recursos [!DNL Catalog's], é recomendável que você se familiarize com esses serviços e como eles interagem com [!DNL Catalog].

### [!DNL Experience Data Model] Sistema (XDM)

[!DNL Experience Data Model] (XDM) System é a estrutura padronizada pela qual  [!DNL Platform] organiza os dados de experiência do cliente. [!DNL Experience Platform] Usa esquemas XDM para descrever a estrutura dos dados de uma maneira consistente e reutilizável.

Quando os dados são assimilados em [!DNL Platform], a estrutura desses dados é mapeada para um esquema XDM e armazenada no [!DNL Data Lake] como parte de um conjunto de dados. Os metadados para cada conjunto de dados são rastreados por [!DNL Catalog Service], que inclui uma referência ao esquema XDM ao qual o conjunto de dados está em conformidade.

Para obter informações mais gerais sobre o Sistema XDM, consulte a [Visão geral do Sistema XDM](../xdm/home.md).

### [!DNL Data Ingestion]

[!DNL Experience Platform] O assimila dados de várias fontes e mantém registros como conjuntos de dados no  [!DNL Data Lake]. [!DNL Catalog] rastreia os metadados desses conjuntos de dados, independentemente da origem ou do método de assimilação.

Ao usar o método de ingestão em lote, [!DNL Catalog] também rastreia metadados adicionais para arquivos em lote. Lotes são unidades de dados que consistem em um ou mais arquivos que serão assimilados como uma única unidade. [!DNL Catalog] rastreia os metadados desses arquivos em lote, bem como os conjuntos de dados em que eles persistem após a assimilação. Os metadados de lote incluem informações sobre o número de registros assimilados com êxito, bem como quaisquer registros com falha e mensagens de erro associadas.

Consulte a [visão geral da assimilação de dados](../ingestion/home.md) para obter mais informações.

## [!DNL Catalog] objetos

Conforme descrito na seção anterior, [!DNL Catalog] rastreia metadados para vários tipos de recursos e operações que são usados por outros serviços [!DNL Platform]. [!DNL Catalog] O mantém seu próprio armazenamento de &quot;objetos&quot; que encapsulam esses metadados. [!DNL Catalog] objetos são representações consultáveis de  [!DNL Platform] dados que permitem pesquisar, monitorar e rotular os dados sem precisar acessar os dados propriamente ditos.

A tabela a seguir descreve os diferentes tipos de objetos suportados por [!DNL Catalog]:

| Objeto | Ponto de extremidade da API | Definição |
|---|---|---|
| Conta | `/accounts` | Ao criar conexões de origem, as credenciais de autenticação devem ser fornecidas. Uma conta representa uma coleção de credenciais de autenticação que foram usadas para criar uma conexão de um tipo específico. Cada conexão tem um conjunto de parâmetros exclusivos que são mantidos por [!DNL Catalog] e protegidos em um [!DNL Azure Key Vault]. |
| Em lote | `/batches` | Lotes são unidades de dados que consistem em um ou mais arquivos que serão assimilados como uma única unidade. Um objeto em lote em [!DNL Catalog] descreve as métricas de assimilação do lote (como o número de registros processados ou o tamanho no disco) e também pode incluir links para conjuntos de dados, exibições e outros recursos que foram afetados pela operação em lote. |
| Conexão | `/connections` | Uma conexão é uma única instância de um conector de origem, exclusivo de sua organização e configurado usando as credenciais de autenticação apropriadas para o tipo de conector. |
| Conector | `/connectors` | Os conectores definem como as conexões de origem são para coletar dados de outros aplicativos do Adobe (como Adobe Analytics e Adobe Audience Manager), fontes de armazenamento em nuvem de terceiros (como [!DNL Azure Blob], [!DNL Amazon S3], servidores FTP e servidores SFTP) e sistemas CRM de terceiros (como [!DNL Microsoft Dynamics] e [!DNL Salesforce]). |
| Conjunto de dados | `/dataSets` | Um conjunto de dados é uma construção de armazenamento e gerenciamento usada para a coleta de dados (geralmente uma tabela) que contém um esquema (colunas) e campos (linhas). Consulte a [visão geral dos conjuntos de dados](./datasets/overview.md) para obter mais informações. |
| Arquivo do conjunto de dados | `/datasetFiles` | Os arquivos do conjunto de dados representam blocos de dados que foram salvos em [!DNL Platform]. Como registros de arquivos literais, é aqui que você pode encontrar o tamanho do arquivo, o número de registros que ele contém e uma referência ao lote que assimilou o arquivo. |

## Próximas etapas

Este documento forneceu uma introdução a [!DNL Catalog Service] e como ele funciona dentro do escopo maior de [!DNL Experience Platform]. Consulte o [[!DNL Catalog] guia do desenvolvedor](api/getting-started.md) para obter etapas sobre como interagir com os diferentes endpoints dessa API [!DNL Catalog]. É recomendável consultar o guia em [filtrar dados do catálogo](api/filter-data.md) para seguir as práticas recomendadas para limitar os dados retornados nas respostas da API.
