---
keywords: Experience Platform;solução de problemas;medidas de proteção;diretrizes;
title: Medidas de proteção para a assimilação de dados
description: Este documento fornece orientação sobre medidas de proteção para a assimilação de dados no Adobe Experience Platform
exl-id: f07751cb-f9d3-49ab-bda6-8e6fec59c337
source-git-commit: 008537dffff4cc428de9070964446f4e7ebf039f
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 1%

---

# Medidas de proteção para a assimilação de dados

As garantias são limites que fornecem orientação para o uso de dados e do sistema, otimização do desempenho e prevenção de erros ou resultados inesperados no Adobe Experience Platform. As garantias podem se referir ao uso ou consumo de dados e processamento em relação aos seus direitos de licenciamento.

Este documento fornece orientação sobre medidas de proteção para a assimilação de dados no Adobe Experience Platform.

## Medidas de proteção para a assimilação em lote

A tabela a seguir descreve as medidas de proteção que devem ser consideradas ao usar o [API de assimilação em lote](./batch-ingestion/overview.md) ou fontes:

| Tipo de assimilação | Diretrizes | Notas |
| --- | --- | --- |
| Assimilação do data lake usando a API de assimilação em lote | <ul><li>Você pode assimilar até 20 GB de dados por hora no data lake usando a API de assimilação em lote.</li><li>O número máximo de arquivos por lote é 1500.</li><li>O tamanho máximo do lote é de 100 GB.</li><li>O número máximo de propriedades ou campos por linha é 10000.</li><li>O número máximo de lotes por minuto por usuário é 138.</li></ul> |
| Assimilação do data lake usando fontes de lote | <ul><li>Você pode assimilar até 200 GB de dados por hora no data lake usando fontes de assimilação em lote, como [!DNL Azure Blob], [!DNL Amazon S3], e [!DNL SFTP].</li><li>O tamanho do lote deve estar entre 256 MB e 100 GB.</li><li>O número máximo de arquivos por lote é 1500.</li></ul> | Consulte a [visão geral das origens](../sources/home.md) para um catálogo de fontes que você pode usar para assimilação de dados. |
| Assimilação em lote para Perfil | <ul><li>O tamanho máximo de uma classe de registro é 100 KB (soft).</li><li>O tamanho máximo de uma classe ExperienceEvent é 10 KB (soft).</li><li>O tamanho máximo de um único registro é de 1 MB.</li></ul> |
| Número de lotes Profile ou ExperienceEvent assimilados por dia | **O número máximo de lotes Profile ou ExperienceEvent assimilados por dia é 90.** Isso significa que o total combinado de lotes Profile e ExperienceEvent assimilados a cada dia não pode exceder 90. A ingestão de lotes adicionais afetará o desempenho do sistema. | Este é um limite flexível. É possível ir além de um limite flexível, no entanto, os limites flexíveis fornecem uma diretriz recomendada para o desempenho do sistema. |

## Medidas de proteção para assimilação por transmissão

Leia o [visão geral da assimilação por transmissão](./streaming-ingestion/overview.md) para obter informações sobre as medidas de proteção para a assimilação por transmissão.

## Medidas de proteção para fontes de transmissão

A tabela a seguir descreve as medidas de proteção a serem consideradas ao usar as fontes de transmissão:

| Tipo de assimilação | Diretrizes | Notas |
| --- | --- | --- |
| Fontes de transmissão | <ul><li>O tamanho máximo do registro é de 1 MB, com o tamanho recomendado de 10 KB.</li><li>As fontes de transmissão oferecem suporte a entre 4.000 e 5.000 solicitações por segundo após a criação de uma nova conexão de origem. **Nota**: pode levar até 30 minutos para que a transmissão de dados seja completamente processada para o data lake.</li><li>Você pode processar entre 4.000 e 5.000 solicitações por segundo no data lake. **Nota**: pode levar até 30 minutos para que a transmissão de dados seja completamente processada para o data lake.</li></ul> | Fontes de transmissão, como [!DNL Kafka], [!DNL Azure Event Hubs], e [!DNL Amazon Kinesis] não use o [!DNL Data Collection Core Service] (DCCS) e podem ter limites de rendimento diferentes. Consulte a [visão geral das origens](../sources/home.md) para um catálogo de fontes que você pode usar para assimilação de dados. |

## Próximas etapas

Consulte a documentação a seguir para obter mais informações sobre dados e medidas de proteção de processamento no Experience Platform:

* [Medidas de proteção aos dados de perfil do cliente em tempo real](../profile/guardrails.md)
* [Medidas de proteção de dados do serviço de identidade](../identity-service/guardrails.md)
