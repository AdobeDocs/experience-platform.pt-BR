---
keywords: Experience Platform;página inicial;tópicos populares;assimilação de dados;local de dados;Local de dados;Gerenciamento de dados;gerenciamento de dados;Linhagem;linhagem;lote;Lote;dados assimilados
solution: Experience Platform
title: Visão geral da assimilação de dados
description: Este documento apresenta as três principais maneiras pelas quais os dados são assimilados na Platform, com links para a respectiva documentação de visão geral para informações mais detalhadas.
exl-id: c189dd4a-5c59-4189-a18c-a3e45a9ff01d
source-git-commit: cde8db1f75cf83451e240f32a877b9d6d26a0e18
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 3%

---

# Visão geral da assimilação de dados

O Adobe Experience Platform reúne dados de várias fontes para ajudar os profissionais de marketing a entender melhor o comportamento de seus clientes. A assimilação de dados da Adobe Experience Platform representa os vários métodos pelos quais o Experience Platform assimila dados dessas fontes, bem como a forma como esses dados são mantidos no Data Lake para uso pelos serviços de Experience Platform downstream.

Este documento apresenta as três principais maneiras pelas quais os dados são assimilados no Experience Platform, com links para a respectiva documentação de visão geral para informações mais detalhadas.

## Assimilação em lote

A assimilação em lote permite assimilar dados em [!DNL Experience Platform] como arquivos em lote. Lotes são unidades de dados que consistem em um ou mais arquivos que serão assimilados como uma única unidade. Depois de assimilados, os lotes fornecem metadados que descrevem o número de registros assimilados com êxito, bem como quaisquer registros com falha e mensagens de erro associadas.

Os arquivos de dados carregados manualmente, como arquivos CSV simples (mapeados para esquemas XDM) e os dataframes do Parquet devem ser assimilados usando esse método.

Consulte a [visão geral de assimilação de lotes](./batch-ingestion/overview.md) para obter mais informações.

>[!TIP]
>
>Use JSON de linha única em vez de JSON de várias linhas como entrada para assimilação em lote. O JSON de linha única permite melhor desempenho, pois o sistema pode dividir um arquivo de entrada em várias partes e processá-las em paralelo, enquanto o JSON de várias linhas não pode ser dividido. Isso pode reduzir significativamente os custos de processamento de dados e melhorar a latência do processamento em lote.

## Assimilação por transmissão

A assimilação de streaming permite enviar dados de dispositivos no lado do cliente e do servidor para o [!DNL Experience Platform] em tempo real. O Experience Platform oferece suporte ao uso de entradas de dados para transmitir dados de experiência recebidos, que são mantidos em conjuntos de dados habilitados para transmissão no Data Lake. As entradas de dados podem ser configuradas para autenticar automaticamente os dados coletados, garantindo que os dados sejam provenientes de uma fonte confiável.

Consulte a [visão geral da assimilação de streaming](./streaming-ingestion/overview.md) para obter mais informações.

## Origens

[!DNL Experience Platform] permite configurar conexões de origem com vários provedores de dados. Essas conexões permitem que você se autentique em suas fontes de dados externas, defina horas para execuções de assimilação e gerencie a taxa de transferência de assimilação.

As conexões do Source podem ser configuradas para coletar dados de outros aplicativos Adobe (como Adobe Analytics e Adobe Audience Manager), fontes de armazenamento na nuvem de terceiros (como [!DNL Azure Blob], [!DNL Amazon] S3, servidores FTP e servidores SFTP) e sistemas CRM de terceiros (como [!DNL Microsoft Dynamics] e [!DNL Salesforce]).

Consulte a [Visão geral das fontes](../sources/home.md) para obter mais informações.

## Próximas etapas e recursos adicionais

Este documento forneceu uma breve introdução aos diferentes aspectos do [!DNL Data Ingestion] em [!DNL Experience Platform]. Continue lendo a documentação de visão geral de cada método de assimilação para se familiarizar com seus diferentes recursos, casos de uso e práticas recomendadas. Você também pode complementar seu aprendizado assistindo ao vídeo de visão geral da assimilação abaixo. Para obter informações sobre como o [!DNL Experience Platform] rastreia os metadados de registros assimilados, consulte a [visão geral do Serviço de Catálogo](../catalog/home.md).

>[!WARNING]
>
>O termo &quot;Perfil unificado&quot; usado no vídeo a seguir está desatualizado. Os termos [!DNL "Profile"] ou [!DNL "Real-Time Customer Profile"] são os termos corretos usados na documentação [!DNL Experience Platform]. Consulte a documentação para obter a funcionalidade mais recente.

>[!VIDEO](https://video.tv.adobe.com/v/27106?quality=12&learn=on)
