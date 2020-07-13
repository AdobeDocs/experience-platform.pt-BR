---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Visão geral de ingestão de dados de Adobe Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: 3f1c3c77a0755a3e305da0fb8a234be0f0ee1863
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 10%

---


# Visão geral da ingestão de dados

O Adobe Experience Platform reúne dados de várias fontes para ajudar os profissionais de marketing a entender melhor o comportamento de seus clientes. A ingestão de dados de Adobe Experience Platform representa os vários métodos pelos quais [!DNL Platform] ingere dados dessas fontes, bem como como como esses dados são persistentes no Data Lake para uso pelos [!DNL Platform] serviços de downstream.

Este documento apresenta as três principais formas de assimilação dos dados, com links para a respectiva documentação de visão geral para obter informações mais detalhadas. [!DNL Platform]

## Ingestão em lote

A ingestão em lote permite assimilar dados como arquivos em lote [!DNL Experience Platform] . Lotes são unidades de dados que consistem em um ou mais arquivos que serão assimilados como uma única unidade. Depois de assimilados, os lotes fornecem metadados que descrevem o número de registros assimilados com êxito, bem como qualquer registro com falha e mensagens de erro associadas.

Arquivos de dados carregados manualmente, como arquivos CSV simples (mapeados para schemas XDM) e quadros de dados Parquet devem ser assimilados usando esse método.

Consulte a visão geral [da ingestão em](./batch-ingestion/overview.md) lote para obter mais informações.

## Inclusão de transmissão

A ingestão de streaming permite enviar dados de dispositivos do cliente e do servidor para [!DNL Experience Platform] em tempo real. [!DNL Platform] suporta o uso de entradas de dados para transmitir dados de experiência de entrada, que são mantidos em conjuntos de dados habilitados para streaming dentro do Data Lake. As entradas de dados podem ser configuradas para autenticar automaticamente os dados coletados, garantindo que os dados sejam provenientes de uma fonte confiável.

Consulte a visão geral [da ingestão de](./streaming-ingestion/overview.md) streaming para obter mais informações.

## Fontes

[!DNL Experience Platform] permite configurar conexões de origem para vários provedores de dados. Essas conexões permitem que você se autentique em suas fontes de dados externas, defina horários para execuções de ingestão e gerencie o throughput de ingestão.

Conexões de origem podem ser configuradas para coletar dados de outros aplicativos da Adobe (como o Adobe Analytics e o Adobe Audience Manager), fontes de armazenamentos em nuvem de terceiros (como [!DNL Azure Blob][!DNL Amazon] S3, servidores FTP e servidores SFTP) e sistemas CRM de terceiros (como o Microsoft Dynamics e o Salesforce).

Consulte a visão geral [das](../sources/home.md) Fontes para obter mais informações.

## Próximos passos e recursos adicionais

Este documento apresentou uma breve introdução aos diferentes aspectos do [!DNL Data Ingestion] In [!DNL Experience Platform]. Continue lendo a documentação de visão geral de cada método de ingestão para se familiarizar com seus diferentes recursos, casos de uso e práticas recomendadas. Você também pode complementar seu aprendizado assistindo ao vídeo de visão geral da ingestão abaixo. Para obter informações sobre como [!DNL Experience Platform] rastrear os metadados para registros ingeridos, consulte a visão geral [do Serviço de](../catalog/home.md)catálogo.

>[!WARNING]
>
> O termo &quot;Perfil unificado&quot; usado no vídeo a seguir está desatualizado. Os termos [!DNL "Profile"] ou [!DNL "Real-time Customer Profile"] são os termos corretos usados na [!DNL Experience Platform] documentação. Consulte a documentação para obter a funcionalidade mais recente.

>[!VIDEO](https://video.tv.adobe.com/v/27106?quality=12&learn=on)