---
keywords: Experience Platform; solução de problemas; medidas de proteção; diretrizes;
title: Grades de proteção para assimilação de dados
description: Este documento fornece orientação sobre medidas de proteção para a assimilação de dados no Adobe Experience Platform
exl-id: f07751cb-f9d3-49ab-bda6-8e6fec59c337
source-git-commit: 96ab28f9f909cedd1148d6b27610aebb7cf61b29
workflow-type: tm+mt
source-wordcount: '536'
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
| Assimilação em lote ao perfil | <ul><li>O tamanho máximo de uma classe de registro é de 100 KB (soft).</li><li>O tamanho máximo de uma classe ExperienceEvent é de 10 KB (soft).</li><li>O tamanho máximo de um único registro é de 1 MB.</li></ul> |
| Número de lotes de Perfil ou ExperienceEvent assimilados por dia | **O número máximo de lotes de Perfil ou ExperienceEvent assimilados por dia é de 90.** Isso significa que o total combinado de lotes de Perfil e ExperienceEvent assimilados a cada dia não pode exceder 90. A inserção de lotes adicionais afetará o desempenho do sistema. | Este é um limite suave. É possível ir além de um limite suave, no entanto, os limites suaves fornecem uma diretriz recomendada para o desempenho do sistema. |

## Grades de proteção para assimilação de streaming

A tabela a seguir descreve as medidas de proteção a serem consideradas ao usar o [API de assimilação de streaming](./streaming-ingestion/overview.md) ou fontes de transmissão:

| Tipo de ingestão | Diretrizes | Notas |
| --- | --- | --- |
| Assimilação por streaming | <ul><li>O tamanho máximo do registro é de 1 MB, com o tamanho recomendado de 10 KB.</li><li>Você pode processar 20000 solicitações por segundo no Perfil em menos de um minuto.</li><li>É possível processar até 20000 solicitações por segundo para o data lake em menos de 15 minutos.</li></ul> | Use a API de assimilação de lote se precisar de uma taxa de transferência de dados mais alta. |
| Fontes de transmissão | <ul><li>O tamanho máximo do registro é de 1 MB, com o tamanho recomendado de 10 KB.</li><li>As fontes de transmissão suportam entre 4000 e 5000 solicitações por segundo após a criação de uma nova conexão de origem. **Observação**: Pode levar até 30 minutos para que o streaming de dados seja completamente processado no lago de dados.</li><li>Você pode processar entre 4000 e 5000 solicitações por segundo no lago de dados. **Observação**: Pode levar até 30 minutos para que o streaming de dados seja completamente processado no lago de dados.</li></ul> | Fontes de fluxo como [!DNL Kafka], [!DNL Azure Event Hubs]e [!DNL Amazon Kinesis] não use o [!DNL Data Collection Core Service] (DCCS) e pode ter limites de throughput diferentes. Consulte a [visão geral das fontes](../sources/home.md) para um catálogo de fontes que pode ser usado para assimilação de dados. |

## Próximas etapas

Consulte a documentação a seguir para obter mais informações sobre dados e medidas de proteção de processamento no Experience Platform:

* [Grades de proteção para dados de perfil do cliente em tempo real](../profile/guardrails.md)
* [Garantias dos dados do serviço de identidade](../identity-service/guardrails.md)
