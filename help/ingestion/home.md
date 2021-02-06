---
keywords: Experience Platform;home;popular tópicos;ingestão de dados;localização de dados;Localização de dados;Gestão de dados;gestão de dados;linhagem;linhagem;lote;lote;dados ingeridos
solution: Experience Platform
title: Visão geral da ingestão de dados
topic: overview
description: Este documento apresenta as três principais formas de assimilação dos dados na Plataforma, com links para a respectiva documentação de visão geral para obter informações mais detalhadas.
translation-type: tm+mt
source-git-commit: 089a4d517476b614521d1db4718966e3ebb13064
workflow-type: tm+mt
source-wordcount: '460'
ht-degree: 14%

---


# Visão geral da ingestão de dados

A Adobe Experience Platform reúne dados de várias fontes para ajudar os profissionais de marketing a entender melhor o comportamento de seus clientes. A ingestão de dados da Adobe Experience Platform representa os vários métodos pelos quais [!DNL Platform] ingere dados dessas fontes, bem como como como esses dados são persistentes no Data Lake para uso pelos serviços downstream [!DNL Platform].

Este documento apresenta as três principais maneiras pelas quais os dados são ingeridos em [!DNL Platform], com links para a respectiva documentação de visão geral para obter informações mais detalhadas.

## Assimilação em lote

A ingestão em lote permite assimilar dados em [!DNL Experience Platform] como arquivos em lote. Lotes são unidades de dados que consistem em um ou mais arquivos que serão assimilados como uma única unidade. Depois de assimilados, os lotes fornecem metadados que descrevem o número de registros assimilados com êxito, bem como qualquer registro com falha e mensagens de erro associadas.

Arquivos de dados carregados manualmente, como arquivos CSV simples (mapeados para schemas XDM) e quadros de dados Parquet devem ser assimilados usando esse método.

Consulte [visão geral da ingestão em lote](./batch-ingestion/overview.md) para obter mais informações.

## Assimilação por streaming

A ingestão de streaming permite enviar dados de dispositivos do cliente e do servidor para [!DNL Experience Platform] em tempo real. [!DNL Platform] suporta o uso de entradas de dados para transmitir dados de experiência de entrada, que são mantidos em conjuntos de dados habilitados para streaming dentro do Data Lake. As entradas de dados podem ser configuradas para autenticar automaticamente os dados coletados, garantindo que os dados sejam provenientes de uma fonte confiável.

Consulte a [visão geral de ingestão de streaming](./streaming-ingestion/overview.md) para obter mais informações.

## Fontes

[!DNL Experience Platform] permite configurar conexões de origem para vários provedores de dados. Essas conexões permitem que você se autentique em suas fontes de dados externas, defina horários para execuções de ingestão e gerencie o throughput de ingestão.

Conexões de origem podem ser configuradas para coletar dados de outros aplicativos de Adobe (como Adobe Analytics e Adobe Audience Manager), fontes de armazenamentos de nuvem de terceiros (como [!DNL Azure Blob], [!DNL Amazon] S3, servidores FTP e servidores SFTP) e sistemas CRM de terceiros (como [!DNL Microsoft Dynamics] e [!DNL Salesforce]).

Consulte [Visão geral das fontes](../sources/home.md) para obter mais informações.

## Próximos passos e recursos adicionais

Este documento apresentou uma breve introdução aos diferentes aspectos de [!DNL Data Ingestion] em [!DNL Experience Platform]. Continue lendo a documentação de visão geral de cada método de ingestão para se familiarizar com seus diferentes recursos, casos de uso e práticas recomendadas. Você também pode complementar sua aprendizagem assistindo ao vídeo de visão geral da ingestão abaixo. Para obter informações sobre como [!DNL Experience Platform] rastreia os metadados para registros assimilados, consulte [Visão geral do serviço de catálogo](../catalog/home.md).

>[!WARNING]
>
>O termo &quot;Perfil unificado&quot; usado no vídeo a seguir está desatualizado. Os termos [!DNL "Profile"] ou [!DNL "Real-time Customer Profile"] são os termos corretos usados na documentação [!DNL Experience Platform]. Consulte a documentação para obter a funcionalidade mais recente.

>[!VIDEO](https://video.tv.adobe.com/v/27106?quality=12&learn=on)