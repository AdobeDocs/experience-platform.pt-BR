---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Visão geral da ingestão de dados da plataforma Adobe Experience
topic: overview
translation-type: tm+mt
source-git-commit: 4817162fe2b7cbf4ae4c1ed325db2af31da5b5d3

---


# Visão geral da ingestão de dados

A Adobe Experience Platform reúne dados de várias fontes para ajudar os profissionais de marketing a entender melhor o comportamento de seus clientes. A ingestão de dados da plataforma Adobe Experience representa os vários métodos pelos quais a plataforma ingere dados dessas fontes, bem como como como esses dados são persistentes no Data Lake para uso pelos serviços da plataforma downstream.

Este documento apresenta as três principais formas de assimilação dos dados na Plataforma, com links para a respectiva documentação de visão geral para obter informações mais detalhadas.

## Ingestão em lote

A ingestão em lote permite que você ingira dados na Experience Platform como arquivos em lote. Lotes são unidades de dados que consistem em um ou mais arquivos a serem ingeridos como uma única unidade. Depois de ingeridos, os lotes fornecem metadados que descrevem o número de registros ingeridos com êxito, bem como quaisquer registros com falha e mensagens de erro associadas.

Arquivos de dados carregados manualmente, como arquivos CSV simples (mapeados para schemas XDM) e quadros de dados Parquet devem ser assimilados usando esse método.

Consulte a visão geral [da ingestão em](./batch-ingestion/overview.md) lote para obter mais informações.

## Inclusão de transmissão

A ingestão de streaming permite enviar dados de dispositivos do cliente e do servidor para a plataforma Experience em tempo real. A plataforma suporta o uso de entradas de dados para transmitir dados de experiência de entrada, que são mantidos em conjuntos de dados habilitados para streaming dentro do Data Lake. As entradas de dados podem ser configuradas para autenticar automaticamente os dados coletados, garantindo que os dados sejam provenientes de uma fonte confiável.

Consulte a visão geral [da ingestão de](./streaming-ingestion/overview.md) streaming para obter mais informações.

## Fontes

A plataforma Experience permite configurar conexões de origem para vários provedores de dados. Essas conexões permitem que você se autentique em suas fontes de dados externas, defina horários para execuções de ingestão e gerencie o throughput de ingestão.

Conexões de origem podem ser configuradas para coletar dados de outros aplicativos da Adobe (como o Adobe Analytics e o Adobe Audiência Manager), fontes de armazenamentos em nuvem de terceiros (como o Azure Blob, o Amazon S3, servidores FTP e servidores SFTP) e sistemas CRM de terceiros (como o Microsoft Dynamics e o Salesforce).

Consulte a visão geral [das](../source-connectors/home.md) Fontes para obter mais informações.

## Próximas etapas

Este documento apresentou brevemente os diferentes aspectos da ingestão de dados na plataforma da experiência. Continue lendo a documentação de visão geral de cada método de ingestão para se familiarizar com seus diferentes recursos, casos de uso e práticas recomendadas. Para obter informações sobre como a plataforma Experience rastreia os metadados para registros ingeridos, consulte a visão geral [do serviço de](../catalog/home.md)catálogo.