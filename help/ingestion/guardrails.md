---
keywords: Experience Platform; solução de problemas; medidas de proteção; diretrizes;
title: Grades de proteção para assimilação de dados
description: Este documento fornece orientação sobre medidas de proteção para a assimilação de dados no Adobe Experience Platform
source-git-commit: 3f558c9c11945cc9af51c42f7ed872101521259f
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 1%

---

# Grades de proteção para assimilação de dados

As garantias são limites que fornecem orientação para o uso de dados e do sistema, otimização de desempenho e prevenção de erros ou resultados inesperados no Adobe Experience Platform. As garantias podem se referir à utilização ou ao consumo de dados e ao processamento em relação aos direitos de licenciamento.

Este documento fornece orientação sobre grades de proteção para a assimilação de dados no Adobe Experience Platform.

## Garantias para a ingestão de lotes

A tabela a seguir descreve as medidas de proteção a serem consideradas ao usar o [API de assimilação em lote](./batch-ingestion/overview.md) ou fontes:

| Tipo de ingestão | Diretrizes | Notas |
| --- | --- | --- |
| Assimilação de lacre de dados usando a API de assimilação de lote | <ul><li>É possível assimilar até 20 GB de dados por hora para o data lake usando a API de assimilação de lote.</li><li>O número máximo de arquivos por lote é 1500.</li><li>O tamanho máximo do lote é de 100 GB.</li><li>O número máximo de propriedades ou campos por linha é 10000.</li><li>O número máximo de lotes por minuto, por usuário, é de 138.</li></ul> |
| Assimilação de lacete de dados usando fontes em lote | <ul><li>Você pode assimilar até 200 GB de dados por hora para o data lake usando fontes de ingestão em lote, como [!DNL Azure Blob], [!DNL Amazon S3]e [!DNL SFTP].</li><li>Um tamanho de lote deve estar entre 256 MB e 100 GB.</li><li>O número máximo de arquivos por lote é 1500.</li></ul> | Consulte a [visão geral das fontes](../sources/home.md) para um catálogo de fontes que pode ser usado para assimilação de dados. |
| Assimilação em lote ao perfil | <ul><li>É possível assimilar até 120 GB de dados por hora.</li><li>O tamanho máximo de uma classe de registro é de 100 KB (soft).</li><li>O tamanho máximo de uma classe ExperienceEvent é de 10 KB (soft).</li><li>O tamanho máximo de um único registro é de 1 MB.</li></ul> |

## Grades de proteção para assimilação de streaming

A tabela a seguir descreve as medidas de proteção a serem consideradas ao usar o [API de assimilação de streaming](./streaming-ingestion/overview.md) ou fontes de transmissão:

| Tipo de ingestão | Diretrizes | Notas |
| --- | --- | --- |
| Assimilação por streaming | <ul><li>O tamanho máximo do registro é de 1 MB, com o tamanho recomendado de 10 KB.</li><li>Você pode processar 20000 solicitações por segundo no Perfil em menos de um minuto.</li><li>É possível processar até 20000 solicitações por segundo para o data lake em menos de 15 minutos.</li></ul> | Use a API de assimilação de lote se precisar de uma taxa de transferência de dados mais alta. |
| Fontes de transmissão | <ul><li>O tamanho máximo do registro é de 1 MB, com o tamanho recomendado de 10 KB.</li><li>As fontes de transmissão suportam entre 4000 e 5000 solicitações por segundo após a criação de uma nova conexão de origem.</li><li>Você pode processar entre 4000 e 5000 solicitações por segundo no lago de dados.</li></ul> | Fontes de fluxo como [!DNL Kafka], [!DNL Azure Event Hubs]e [!DNL Amazon Kinesis] não use o [!DNL Data Collection Core Service] (DCCS) e pode ter limites de throughput diferentes. Consulte a [visão geral das fontes](../sources/home.md) para um catálogo de fontes que pode ser usado para assimilação de dados. |

## Próximas etapas

Consulte a documentação a seguir para obter mais informações sobre dados e medidas de proteção de processamento no Experience Platform:

* [Grades de proteção para dados de perfil do cliente em tempo real](../profile/guardrails.md)
* [Garantias dos dados do serviço de identidade](../identity-service/guardrails.md)