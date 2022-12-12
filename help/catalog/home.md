---
keywords: Experience Platform;página inicial;tópicos populares;serviço de catálogo;catálogo;Serviço de catálogo;localização de dados;Localização de dados;Gestão de dados;gestão de dados;Linhagem;linhagem;Catálogo;ativar conjunto de dados
solution: Experience Platform
title: Visão geral do serviço de catálogo
topic-legacy: overview
description: O Serviço de catálogo é o sistema de registro para localização e linhagem de dados na Adobe Experience Platform. Embora todos os dados assimilados na Experience Platform sejam armazenados no Data Lake como arquivos e diretórios, o Catálogo retém os metadados e a descrição desses arquivos e diretórios para fins de pesquisa e monitoramento.
exl-id: ef0c173b-607b-41b8-8676-c54ae9472e23
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: ht
source-wordcount: '805'
ht-degree: 100%

---

# Visão geral do [!DNL Catalog Service]

O [!DNL Catalog Service] é o sistema de registro para localização e linhagem de dados na Adobe Experience Platform. Embora todos os dados assimilados na [!DNL Experience Platform] sejam armazenados no [!DNL Data Lake] como arquivos e diretórios, o [!DNL Catalog] retém os metadados e a descrição desses arquivos e diretórios para fins de pesquisa e monitoramento.

Simplificando, o [!DNL Catalog] atua como um armazenamento de metadados ou “catálogo”, onde você pode encontrar informações sobre seus dados na [!DNL Experience Platform]. Você pode usar o [!DNL Catalog] para responder às seguintes perguntas:

* Onde meus dados estão localizados?
* Em que fase de processamento se encontram esses dados?
* Quais sistemas ou processos atuaram em meus dados?
* Quantos dados foram processados com sucesso?
* Quais erros ocorreram durante o processamento?

O [!DNL Catalog] fornece uma API RESTful que permite gerenciar programaticamente os metadados da [!DNL Platform] utilizando operações CRUD básicas. Consulte o [Guia do desenvolvedor do catálogo](api/getting-started.md) para obter mais informações.

## Serviços do [!DNL Catalog] e da [!DNL Experience Platform]

Os recursos que o [!DNL Catalog Service] rastreia são usados por vários serviços da [!DNL Experience Platform]. Para aproveitar ao máximo os recursos do [!DNL Catalog's], recomendamos que você se familiarize com esses serviços e como eles interagem com o [!DNL Catalog].

### Sistema de [!DNL Experience Data Model] (XDM)

O Sistema de [!DNL Experience Data Model] (XDM) é a estrutura padronizada pela qual a [!DNL Platform] organiza os dados de experiência do cliente. A [!DNL Experience Platform] utiliza esquemas XDM para descrever a estrutura dos dados de forma consistente e reutilizável.

Quando os dados são assimilados na [!DNL Platform], a estrutura desses dados é mapeada para um esquema XDM e armazenada no [!DNL Data Lake] como parte de um conjunto de dados. Os metadados de cada conjunto de dados são rastreados pelo [!DNL Catalog Service], que inclui uma referência ao esquema XDM com o qual o conjunto de dados está em conformidade.

Para obter informações mais gerais sobre o Sistema de XDM, consulte a [Visão geral do Sistema de XDM](../xdm/home.md).

### [!DNL Data Ingestion]

A [!DNL Experience Platform] assimila dados de várias origens e mantém registros como conjuntos de dados no [!DNL Data Lake]. O [!DNL Catalog] rastreia os metadados desses conjuntos de dados, independentemente da origem ou do método de assimilação.

Ao utilizar o método de assimilação em lote, o [!DNL Catalog] também rastreia metadados adicionais para arquivos em lote. Lotes são unidades de dados que consistem em um ou mais arquivos que serão assimilados como uma única unidade. O [!DNL Catalog] rastreia os metadados desses arquivos em lote, bem como os conjuntos de dados em que eles são mantidos após a assimilação. Os metadados de lote incluem informações sobre o número de registros assimilados com sucesso, bem como os registros com falha e mensagens de erro associadas.

Consulte a [visão geral da assimilação de dados](../ingestion/home.md) para obter mais informações.

## Objetos do [!DNL Catalog]

Conforme descrito na seção anterior, o [!DNL Catalog] rastreia metadados para vários tipos de recursos e operações usados por outros serviços da [!DNL Platform]. O [!DNL Catalog] mantém seu próprio armazenamento de “objetos” que encapsulam esses metadados. Os objetos do [!DNL Catalog] são representações consultáveis de dados da [!DNL Platform] que permitem pesquisar, monitorar e rotular os dados sem precisar acessá-los.

A tabela a seguir descreve os diferentes tipos de objetos aceitos pelo [!DNL Catalog]:

| Objeto | Ponto de acesso da API | Definição |
|---|---|---|
| Conta | `/accounts` | Ao criar conexões de origem, as credenciais de autenticação devem ser fornecidas. Uma conta representa uma coleção de credenciais de autenticação que foram usadas para criar uma conexão de um tipo específico. Cada conexão tem um conjunto de parâmetros exclusivos que são mantidos pelo [!DNL Catalog] e protegidos em um [!DNL Azure Key Vault]. |
| Lote | `/batches` | Lotes são unidades de dados que consistem em um ou mais arquivos que serão assimilados como uma única unidade. Um objeto em lote no [!DNL Catalog] descreve as métricas de assimilação do lote (como o número de registros processados ou o tamanho no disco) e também pode incluir links para conjuntos de dados, visualizações e outros recursos que foram afetados pela operação em lote. |
| Conexão | `/connections` | Uma conexão é uma única instância de um conector de origem. Ela é exclusiva da sua organização e configurada usando as credenciais de autenticação apropriadas para o tipo de conector. |
| Conector  | `/connectors` | Os conectores definem como as conexões de origem deverão coletar dados de outros aplicativos da Adobe (como o Adobe Analytics e Adobe Audience Manager), fontes de armazenamento na nuvem de terceiros (como o [!DNL Azure Blob], [!DNL Amazon S3], servidores FTP e servidores SFTP) e sistemas CRM de terceiros (como o [!DNL Microsoft Dynamics] e [!DNL Salesforce]). |
| Conjunto de dados | `/dataSets` | Um conjunto de dados é uma construção de armazenamento e gerenciamento usada para a coleta de dados (normalmente uma tabela) que contenham um esquema (colunas) e campos (linhas). Consulte a [visão geral dos conjuntos de dados](./datasets/overview.md) para obter mais informações. |
| Arquivo de conjunto de dados | `/datasetFiles` | Os arquivos de conjunto de dados representam blocos de dados que foram salvos na [!DNL Platform]. Como registros de arquivos literais, eles contém informações sobre o tamanho do arquivo, o número de registros que ele contém e uma referência ao lote que assimilou o arquivo. |

## Próximas etapas

Este documento forneceu uma introdução ao [!DNL Catalog Service] e como ele funciona dentro do escopo mais amplo da [!DNL Experience Platform]. Consulte o [[!DNL Catalog] guia do desenvolvedor](api/getting-started.md) para conferir as etapas de interação com diferentes pontos de acesso da API do [!DNL Catalog]. É recomendável que você também consulte o guia sobre [Filtragem de dados do catálogo](api/filter-data.md) para saber as práticas recomendadas para limitar os dados retornados nas respostas da API.
