---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Visão geral do serviço de catálogo
topic: overview
translation-type: tm+mt
source-git-commit: 1fce86193bc1660d0f16408ed1b9217368549f6c
workflow-type: tm+mt
source-wordcount: '804'
ht-degree: 5%

---


# Visão geral do serviço de catálogo

O serviço de catálogo é o sistema de registro para localização e linhagem de dados na Adobe Experience Platform. Embora todos os dados ingeridos na plataforma Experience sejam armazenados no Data Lake como arquivos e diretórios, o Catálogo armazena os metadados e a descrição desses arquivos e diretórios para fins de pesquisa e monitoramento.

Em outras palavras, o Catálogo atua como um armazenamento de metadados ou &quot;catálogo&quot;, onde você pode encontrar informações sobre seus dados na Experience Platform. Você pode usar o Catálogo para responder às seguintes perguntas:

* Onde meus dados estão localizados?
* Em que fase de processamento estão esses dados?
* Que sistemas ou processos agiram em meus dados?
* Quantos dados foram processados com êxito?
* Quais erros ocorreram durante o processamento?

O Catálogo fornece uma RESTful API que permite gerenciar programaticamente os metadados da plataforma usando operações CRUD básicas. Consulte o guia [do desenvolvedor](api/getting-started.md) Catálogo para obter mais informações.

## Serviços de catálogo e plataforma de experiência

Os recursos que o serviço de catálogo acompanha são usados por vários serviços da plataforma de experiência. Para aproveitar ao máximo os recursos do Catálogo, é recomendável que você se familiarize com esses serviços e como eles interagem com o Catálogo.

### Sistema do Experience Data Model (XDM)

O sistema Experience Data Model (XDM) é a estrutura padronizada pela qual a Plataforma organiza os dados de experiência do cliente. A plataforma Experience aproveita os schemas XDM para descrever a estrutura dos dados de forma consistente e reutilizável.

Quando os dados são ingeridos na Plataforma, a estrutura desses dados é mapeada para um schema XDM e armazenada no Data Lake como parte de um **conjunto de dados**. Os metadados de cada conjunto de dados são rastreados pelo serviço de catálogo, que inclui uma referência ao schema XDM ao qual o conjunto de dados está em conformidade.

Para obter informações mais gerais sobre o Sistema XDM, consulte a visão geral [do Sistema](../xdm/home.md)XDM.

### Ingestão de dados

A plataforma da experiência ingere dados de várias fontes e persiste registros como conjuntos de dados no Data Lake. O catálogo rastreia os metadados desses conjuntos de dados, independentemente da origem ou do método de ingestão.

Ao usar o método de ingestão em lote, o Catálogo também rastreia metadados adicionais para arquivos em **lote** . Lotes são unidades de dados que consistem em um ou mais arquivos que serão assimilados como uma única unidade. O catálogo rastreia os metadados desses arquivos em lote, bem como os conjuntos de dados em que eles são persistentes após a ingestão. Os metadados do lote incluem informações sobre o número de registros ingeridos com êxito, bem como quaisquer registros com falha e mensagens de erro associadas.

Consulte a visão geral [da ingestão de](../ingestion/home.md) dados para obter mais informações.

## Objetos de catálogo

Conforme descrito na seção anterior, o Catálogo rastreia metadados para vários tipos de recursos e operações usados por outros serviços da Plataforma. O catálogo mantém sua própria loja de &quot;objetos&quot; que encapsulam esses metadados. Objetos de catálogo são representações consultáveis de dados da plataforma que permitem pesquisar, monitorar e rotular seus dados sem precisar acessar os próprios dados.

A tabela a seguir descreve os diferentes tipos de objetos suportados pelo Catálogo:

| Objeto | Ponto de extremidade da API | Definição |
|---|---|---|
| Account | `/accounts` | Ao criar conexões de origem, as credenciais de autenticação devem ser fornecidas. Uma conta representa uma coleção de credenciais de autenticação que foram usadas para criar uma conexão de um tipo específico. Cada conexão tem um conjunto de parâmetros exclusivos que são mantidos pelo Catálogo e protegidos em um Cofre de Chaves do Azure. |
| Lote | `/batches` | Lotes são unidades de dados que consistem em um ou mais arquivos que serão assimilados como uma única unidade. Um objeto em lote no Catálogo descreve as métricas de ingestão do lote (como o número de registros processados ou o tamanho no disco) e também pode incluir links para conjuntos de dados, visualizações e outros recursos que foram afetados pela operação em lote. |
| Conexão | `/connections` | Uma conexão é uma única instância de um conector de origem, exclusivo para sua organização e configurado usando as credenciais de autenticação apropriadas para o tipo de conector. |
| Conector | `/connectors` | Os conectores definem como as conexões de origem devem coletar dados de outros aplicativos da Adobe (como o Adobe Analytics e o Adobe Audiência Manager), fontes de armazenamentos em nuvem de terceiros (como o Azure Blob, o Amazon S3, servidores FTP e servidores SFTP) e sistemas CRM de terceiros (como o Microsoft Dynamics e o Salesforce). |
| Conjunto de dados | `/dataSets` | Um conjunto de dados é um armazenamento e uma construção de gerenciamento usados para a coleta de dados (geralmente uma tabela) que contém um schema (colunas) e campos (linhas). Consulte a visão geral [dos](./datasets/overview.md) conjuntos de dados para obter mais informações. |
| Arquivo de conjunto de dados | `/datasetFiles` | Os arquivos de conjunto de dados representam blocos de dados que foram salvos na Plataforma. Como registros de arquivos literais, é onde você pode encontrar o tamanho do arquivo, o número de registros que ele contém e uma referência ao lote que assimilou o arquivo. |

## Próximas etapas

Este documento forneceu uma introdução ao serviço de catálogo e como ele funciona dentro do maior escopo da plataforma de experiência. Consulte o guia [do desenvolvedor do](api/getting-started.md) Catálogo para obter etapas sobre como interagir com os diferentes pontos de extremidade dessa API do Catálogo. É recomendável que você também consulte o guia sobre a [filtragem de dados](api/filter-data.md) do catálogo para seguir as práticas recomendadas para limitar os dados retornados nas respostas da API.