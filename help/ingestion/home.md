---
keywords: Experience Platform, página inicial, tópicos populares, assimilação de dados, local dos dados, Localização de dados, Gerenciamento de dados, Lineage, linhagem, lote, lote, dados assimilados
solution: Experience Platform
title: Visão geral da assimilação de dados
topic-legacy: overview
description: Este documento apresenta as três principais maneiras pelas quais os dados são assimilados na Platform, com links para sua respectiva documentação de visão geral para obter informações mais detalhadas.
exl-id: c189dd4a-5c59-4189-a18c-a3e45a9ff01d
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 14%

---

# Visão geral da assimilação de dados

A Adobe Experience Platform reúne dados de várias fontes para ajudar os profissionais de marketing a entender melhor o comportamento de seus clientes. A Assimilação de dados do Adobe Experience Platform representa os vários métodos pelos quais [!DNL Platform] assimila dados dessas fontes, bem como como esses dados são mantidos no Data Lake para uso pelos serviços de downstream [!DNL Platform].

Este documento apresenta as três principais maneiras pelas quais os dados são assimilados em [!DNL Platform], com links para sua respectiva documentação de visão geral para obter informações mais detalhadas.

## Assimilação em lote

A assimilação em lote permite assimilar dados em [!DNL Experience Platform] como arquivos em lote. Lotes são unidades de dados que consistem em um ou mais arquivos que serão assimilados como uma única unidade. Depois de assimilados, os lotes fornecem metadados que descrevem o número de registros assimilados com êxito, bem como qualquer registro com falha e mensagens de erro associadas.

Arquivos de dados carregados manualmente, como arquivos CSV simples (mapeados para esquemas XDM) e dataframes do Parquet devem ser assimilados usando esse método.

Consulte a [visão geral da ingestão em lote](./batch-ingestion/overview.md) para obter mais informações.

## Assimilação por streaming

A assimilação de streaming permite enviar dados de dispositivos cliente e servidor para [!DNL Experience Platform] em tempo real. [!DNL Platform] O suporta o uso de entradas de dados para transmitir dados de experiência recebidos, que são mantidos em conjuntos de dados habilitados para transmissão no Data Lake. As entradas de dados podem ser configuradas para autenticar automaticamente os dados coletados, garantindo que os dados sejam provenientes de uma fonte confiável.

Consulte a [visão geral da assimilação de streaming](./streaming-ingestion/overview.md) para obter mais informações.

## Fontes

[!DNL Experience Platform] O permite configurar conexões de origem para vários provedores de dados. Essas conexões permitem autenticar em suas fontes de dados externas, definir horários para execuções de assimilação e gerenciar a taxa de transferência de assimilação.

As conexões de origem podem ser configuradas para coletar dados de outros aplicativos do Adobe (como Adobe Analytics e Adobe Audience Manager), fontes de armazenamento em nuvem de terceiros (como [!DNL Azure Blob], [!DNL Amazon] S3, servidores FTP e servidores SFTP) e sistemas CRM de terceiros (como [!DNL Microsoft Dynamics] e [!DNL Salesforce]).

Consulte a [Visão geral das fontes](../sources/home.md) para obter mais informações.

## Próximas etapas e recursos adicionais

Este documento forneceu uma breve introdução aos diferentes aspectos de [!DNL Data Ingestion] em [!DNL Experience Platform]. Continue lendo a documentação de visão geral de cada método de ingestão para se familiarizar com seus diferentes recursos, casos de uso e práticas recomendadas. Você também pode complementar seu aprendizado assistindo ao vídeo de visão geral da assimilação abaixo. Para obter informações sobre como [!DNL Experience Platform] rastreia os metadados para registros assimilados, consulte a [Visão geral do Serviço de Catálogo](../catalog/home.md).

>[!WARNING]
>
>O termo &quot;Perfil unificado&quot; usado no vídeo a seguir está desatualizado. Os termos [!DNL "Profile"] ou [!DNL "Real-time Customer Profile"] são os termos corretos usados na documentação [!DNL Experience Platform]. Consulte a documentação para obter a funcionalidade mais recente.

>[!VIDEO](https://video.tv.adobe.com/v/27106?quality=12&learn=on)
