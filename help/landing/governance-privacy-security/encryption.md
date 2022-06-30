---
title: Criptografia de dados no Adobe Experience Platform
topic-legacy: data protection
description: Saiba como os dados são criptografados em trânsito e em repouso no Adobe Experience Platform.
exl-id: 184b2b2d-8cd7-4299-83f8-f992f585c336
source-git-commit: 0a01dd2b0d8a1039178e3593475f9a87639ccdcd
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 5%

---

# Criptografia de dados no Adobe Experience Platform

O Adobe Experience Platform é um sistema poderoso e extensível que centraliza e padroniza os dados de experiência do cliente nas soluções corporativas. Todos os dados utilizados pela Platform são criptografados em trânsito e em repouso para manter seus dados protegidos. Este documento descreve os processos de criptografia da Platform em alto nível.

O diagrama de fluxo de processo a seguir ilustra como os dados são assimilados, criptografados e persistentes por [!DNL Experience Platform]:

![](../images/governance-privacy-security/encryption/flow.png)

## Dados em trânsito {#in-transit}

Todos os dados em trânsito entre a Platform e qualquer componente externo são realizados por conexões seguras e criptografadas usando HTTPS [TLS v1.2](https://datatracker.ietf.org/doc/html/rfc5246).

Em geral, os dados são trazidos para a Platform de três maneiras:

* [Coleta de dados](../../rtcdp-connections/home.md) Os recursos do permitem que sites e aplicativos móveis enviem dados para a Rede de borda da plataforma para preparo e preparação para assimilação.
* [Conectores de origem](../../sources/home.md) Transmita dados diretamente para a plataforma a partir de aplicativos Adobe Experience Cloud e outras fontes de dados corporativas.
* Ferramentas não Adobe ETL (extrair, transformar, carregar) enviam dados para a [API de assimilação em lote](../../ingestion/batch-ingestion/overview.md) para consumo.

Depois que os dados forem trazidos para o sistema e [criptografado em repouso](#at-rest), pode ser enriquecido pelos serviços da plataforma e trazido para fora do sistema das seguintes maneiras:

* [Destinos](../../destinations/home.md) permite ativar os dados para aplicativos Adobe e aplicativos de parceiros.
* Aplicativos da plataforma nativa, como [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=pt-BR) e [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=pt-BR) O também pode usar os dados do .

## Dados em repouso {#at-rest}

Os dados assimilados e usados pela Platform são armazenados no lago de dados, um armazenamento de dados altamente granular que contém todos os dados gerenciados pelo sistema, independentemente da origem ou do formato de arquivo. Todos os dados persistentes no lago de dados são criptografados, armazenados e gerenciados em um [[!DNL Microsoft Azure Data Lake] Armazenamento](https://docs.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-introduction) que é exclusiva da sua organização.

Para obter detalhes sobre como os dados em repouso são criptografados no Armazenamento Azure Data Lake e no banco de dados do Cosmos, consulte o [documentação oficial do Azure](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption).

## Próximas etapas

Este documento forneceu uma visão geral de alto nível de como os dados são criptografados na plataforma. Para obter mais informações sobre os procedimentos de segurança no Platform, consulte a visão geral em [governança, privacidade e segurança](./overview.md) no Experience League, ou dê uma olhada no [White paper sobre segurança da plataforma](https://www.adobe.com/content/dam/cc/en/security/pdfs/AEP_SecurityOverview.pdf).
