---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Visão geral do serviço de catálogo
topic: overview
translation-type: tm+mt
source-git-commit: bfbf2074a9dcadd809de043d62f7d2ddaa7c7b31
workflow-type: tm+mt
source-wordcount: '732'
ht-degree: 6%

---


# [!DNL Catalog Service]visão geral

[!DNL Catalog Service] é o sistema de registro para localização e linhagem de dados dentro do Adobe Experience Platform. Embora todos os dados inseridos [!DNL Experience Platform] sejam armazenados no [!DNL Data Lake] como arquivos e diretórios, [!DNL Catalog] os metadados e a descrição desses arquivos e diretórios são mantidos para fins de pesquisa e monitoramento.

Simplificando, [!DNL Catalog] atua como um repositório de metadados ou &quot;[!UICONTROL catálogo]&quot; onde você pode encontrar informações sobre seus dados dentro [!DNL Experience Platform]. Você pode usar [!DNL Catalog] para responder as seguintes perguntas:

* Onde meus dados estão localizados?
* Em que fase de processamento estão esses dados?
* Que sistemas ou processos agiram em meus dados?
* Quantos dados foram processados com êxito?
* Quais erros ocorreram durante o processamento?

[!DNL Catalog] fornece uma RESTful API que permite gerenciar programaticamente [!DNL Platform] metadados usando operações CRUD básicas. Consulte o guia [do desenvolvedor](api/getting-started.md) Catálogo para obter mais informações.

## [!DNL Catalog] e [!DNL Experience Platform] serviços

Os recursos que [!DNL Catalog Service] rastreiam são usados por vários [!DNL Experience Platform] serviços. Para aproveitar ao máximo [!DNL Catalog's] os recursos, é recomendável que você se familiarize com esses serviços e com como eles interagem [!DNL Catalog].

### [!DNL Experience Data Model] Sistema (XDM)

[!DNL Experience Data Model] (XDM) O sistema é a estrutura padronizada pela qual [!DNL Platform] organiza os dados de experiência do cliente. [!DNL Experience Platform] aproveita os schemas XDM para descrever a estrutura dos dados de forma consistente e reutilizável.

Quando os dados são ingeridos, [!DNL Platform]a estrutura desses dados é mapeada para um schema XDM e armazenada dentro do [!DNL Data Lake] como parte de um **conjunto** de dados. Os metadados de cada conjunto de dados são rastreados por [!DNL Catalog Service], o que inclui uma referência ao schema XDM ao qual o conjunto de dados está em conformidade.

Para obter informações mais gerais sobre o Sistema XDM, consulte a visão geral [do Sistema](../xdm/home.md)XDM.

### [!DNL Data Ingestion]

[!DNL Experience Platform] assimila dados de várias fontes e persiste registros como conjuntos de dados no [!DNL Data Lake]. [!DNL Catalog] rastreia os metadados desses conjuntos de dados, independentemente da origem ou do método de ingestão.

Ao usar o método de ingestão em lote, [!DNL Catalog] também rastreia metadados adicionais para arquivos em **lote** . Lotes são unidades de dados que consistem em um ou mais arquivos que serão assimilados como uma única unidade. [!DNL Catalog] rastreia os metadados desses arquivos em lote, bem como os conjuntos de dados nos quais eles são persistentes após a ingestão. Os metadados do lote incluem informações sobre o número de registros ingeridos com êxito, bem como quaisquer registros com falha e mensagens de erro associadas.

Consulte a visão geral [da ingestão de](../ingestion/home.md) dados para obter mais informações.

## [!DNL Catalog] objetos

Conforme descrito na seção anterior, [!DNL Catalog] rastreia metadados para vários tipos de recursos e operações usados por outros [!DNL Platform] serviços. [!DNL Catalog] mantém sua própria loja de &quot;objetos&quot; que encapsulam esses metadados. [!DNL Catalog] objetos são representações consultáveis de [!DNL Platform] dados que permitem pesquisar, monitorar e rotular seus dados sem precisar acessar os próprios dados.

A tabela a seguir descreve os diferentes tipos de objetos suportados por [!DNL Catalog]:

| Objeto | Ponto de extremidade da API | Definição |
|---|---|---|
| Account | `/accounts` | Ao criar conexões de origem, as credenciais de autenticação devem ser fornecidas. Uma conta representa uma coleção de credenciais de autenticação que foram usadas para criar uma conexão de um tipo específico. Cada conexão tem um conjunto de parâmetros exclusivos que são persistentes por [!DNL Catalog] e protegidos em um [!DNL Azure Key Vault]. |
| Lote | `/batches` | Lotes são unidades de dados que consistem em um ou mais arquivos que serão assimilados como uma única unidade. Um objeto em lote [!DNL Catalog] descreve as métricas de ingestão do lote (como o número de registros processados ou o tamanho no disco) e também pode incluir links para conjuntos de dados, visualizações e outros recursos que foram afetados pela operação em lote. |
| Conexão | `/connections` | Uma conexão é uma única instância de um conector de origem, exclusivo para sua organização e configurado usando as credenciais de autenticação apropriadas para o tipo de conector. |
| Conector | `/connectors` | Os conectores definem como as conexões de origem devem coletar dados de outros aplicativos da Adobe (como o Adobe Analytics e o Adobe Audience Manager), fontes de armazenamentos de nuvem de terceiros (como [!DNL Azure Blob]servidores FTP [!DNL Amazon S3]e servidores SFTP) e sistemas CRM de terceiros (como [!DNL Microsoft Dynamics] e [!DNL Salesforce]). |
| Conjunto de dados | `/dataSets` | Um conjunto de dados é um armazenamento e uma construção de gerenciamento usados para a coleta de dados (geralmente uma tabela) que contém um schema (colunas) e campos (linhas). Consulte a visão geral [dos](./datasets/overview.md) conjuntos de dados para obter mais informações. |
| Arquivo de conjunto de dados | `/datasetFiles` | Os arquivos de conjunto de dados representam blocos de dados que foram salvos em [!DNL Platform]. Como registros de arquivos literais, é onde você pode encontrar o tamanho do arquivo, o número de registros que ele contém e uma referência ao lote que assimilou o arquivo. |

## Próximas etapas

Este documento forneceu uma introdução ao [!DNL Catalog Service] e como ele funciona dentro do maior escopo de [!DNL Experience Platform]. Consulte o guia [do desenvolvedor do](api/getting-started.md) Catálogo para obter etapas sobre como interagir com os diferentes pontos de extremidade dessa [!DNL Catalog] API. É recomendável que você também consulte o guia sobre a [filtragem de dados](api/filter-data.md) do catálogo para seguir as práticas recomendadas para limitar os dados retornados nas respostas da API.