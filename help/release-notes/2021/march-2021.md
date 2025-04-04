---
title: Notas da versão de março de 2021 da Adobe Experience Platform
description: As notas da versão de março de 2021 da Adobe Experience Platform.
doc-type: release notes
last-update: March 31, 2021
author: ens72741
exl-id: 027cd7b1-1651-4939-bc97-968a41824117
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 38%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: quinta-feira, 31 de março de 2021**

Atualizações dos recursos já existentes na Adobe Experience Platform:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Segmentation Service]](#segmentation)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

O [!DNL Data Prep] permite que os engenheiros de dados mapeiem, transformem e validem dados de e para o Experience Data Model (XDM).

| Recurso | Descrição |
| ------- | ----------- |
| Função `add_to_array` | Atualização da funcionalidade para oferecer suporte a arrays como parâmetro. |
| Função `to_array` | Atualização da funcionalidade para oferecer suporte a objetos como parâmetro. |

Para obter mais informações, consulte a [[!DNL Data Prep] visão geral](../../data-prep/home.md).

## Serviço de segmentação {#segmentation}

O Serviço de Segmentação da Adobe Experience Platform fornece uma interface de usuário e uma API RESTful que permite criar segmentos e gerar públicos a partir dos dados do [!DNL Real-Time Customer Profile]. Esses segmentos são configurados e mantidos centralmente no [!DNL Experience Platform], tornando-os prontamente acessíveis por qualquer aplicativo do Adobe.

O [!DNL Segmentation Service] define um subconjunto específico de perfis descrevendo os critérios que distinguem um grupo de pessoas na sua base de clientes que pode ser direcionado por campanhas de marketing. Os segmentos podem ser baseados em dados de registro (como informações demográficas) ou em eventos de séries temporais que representam interações de clientes com sua marca.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Segmentação do Edge (Beta) | A segmentação do Edge avalia segmentos em tempo real, o que permite casos de uso de personalização da mesma página e da próxima página. Mais informações sobre a segmentação de borda podem ser encontradas na [Visão geral da interface de segmentação](../../segmentation/ui/overview.md). |
| (Beta) Segmentação incremental | Aumenta a atualização das definições de segmento existentes avaliadas na segmentação em lote para até uma hora. |

Para obter mais informações sobre o [!DNL Segmentation Service], consulte a [Visão geral de segmentação](../../segmentation/home.md).

## [!DNL Sources] {#sources}

O Adobe Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, estruturar, rotular e aprimorar esses dados usando os serviços da Experience Platform. É possível assimilar dados de várias origens, como aplicativos da Adobe, do armazenamento na nuvem, um software de terceiros e do seu sistema de CRM.

A Experience Platform fornece uma API RESTful e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar a sistemas de armazenamento externos e serviços de CRM, definir períodos para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

| Recurso | Descrição |
| ------- | ----------- |
| Origens do Beta migrando para o GA | As seguintes fontes foram promovidas de beta para GA: <ul><li>[[!DNL MySQL]](../../sources/connectors/databases/mysql.md)</li><li>[[!DNL PostGres]](../../sources/connectors/databases/postgres.md)</li><li>[[!DNL Salesforce Service Cloud]](../../sources/connectors/customer-success/salesforce-service-cloud.md)</li><li>[[!DNL SFTP]](../../sources/connectors/cloud-storage/sftp.md)</li><li>[[!DNL Shopify]](../../sources/connectors/ecommerce/shopify.md)</li></ul> |
| Suporte de API para assimilação de arquivo compactado | Agora é possível visualizar e assimilar arquivos JSON ou delimitados compactados usando fontes de armazenamento na nuvem. Para obter mais informações, consulte o tutorial sobre [coleta de dados de armazenamento na nuvem usando APIs](../../sources/tutorials/api/collect/cloud-storage.md). |
| Suporte à interface do usuário para carregamento recursivo de arquivos | Agora é possível assimilar pastas inteiras de forma recursiva ao usar uma fonte de armazenamento na nuvem. Ao assimilar uma pasta inteira, você deve garantir que seu conteúdo compartilhe o mesmo schema. Para obter mais informações, consulte o tutorial sobre [configuração de um fluxo de dados para conectores de armazenamento em nuvem na interface](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md). |

Para saber mais sobre fontes, consulte a [visão geral das fontes](../../sources/home.md).
