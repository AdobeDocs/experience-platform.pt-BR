---
title: Notas de versão da Adobe Experience Platform de março de 2021
description: As notas de versão de março de 2021 para o Adobe Experience Platform.
doc-type: release notes
last-update: March 31, 2021
author: ens72741
exl-id: 027cd7b1-1651-4939-bc97-968a41824117
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 6%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 31 de março de 2021**

Atualizações dos recursos existentes na Adobe Experience Platform:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Segmentation Service]](#segmentation)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] O permite que os engenheiros de dados mapeiem, transformem e validem dados de e para o Experience Data Model (XDM).

| Recurso | Descrição |
| ------- | ----------- |
| Função `add_to_array`  | Atualização da funcionalidade para oferecer suporte a arrays como parâmetro. |
| Função `to_array`  | Atualização da funcionalidade para oferecer suporte a objetos como parâmetro. |

Para obter mais informações, consulte [[!DNL Data Prep] visão geral](../../data-prep/home.md).

## Serviço de segmentação {#segmentation}

O Serviço de segmentação da Adobe Experience Platform fornece uma interface de usuário e uma API RESTful que permite criar segmentos e gerar públicos-alvo a partir de seus [!DNL Real-Time Customer Profile] dados. Esses segmentos são configurados e mantidos de forma centralizada [!DNL Platform], tornando-os prontamente acessíveis por qualquer aplicativo Adobe.

[!DNL Segmentation Service] O define um subconjunto específico de perfis descrevendo os critérios que distinguem um grupo comercializável de pessoas na sua base de clientes. Os segmentos podem ser baseados em dados de registro (como informações demográficas) ou eventos de séries temporais que representam interações do cliente com sua marca.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| (Beta) Segmentação de borda | A segmentação de borda avalia segmentos em tempo real, o que permite casos de uso de personalização da mesma página e da próxima página. Mais informações sobre segmentação de borda podem ser encontradas no [Visão geral da interface de segmentação](../../segmentation/ui/overview.md). |
| (Beta) Segmentação incremental | Aumenta a atualização das definições de segmento existentes avaliadas na segmentação em lote para até uma hora. |

Para obter mais informações sobre [!DNL Segmentation Service], consulte o [Visão geral da segmentação](../../segmentation/home.md).

## [!DNL Sources] {#sources}

O Adobe Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, estruturar, rotular e aprimorar esses dados usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

O Experience Platform fornece uma API RESTful e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar a sistemas de armazenamento externos e serviços de CRM, definir tempos para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

| Recurso | Descrição |
| ------- | ----------- |
| Origens beta migrando para GA | As seguintes fontes foram promovidas de beta para GA: <ul><li>[[!DNL MySQL]](../../sources/connectors/databases/mysql.md)</li><li>[[!DNL PostGres]](../../sources/connectors/databases/postgres.md)</li><li>[[!DNL Salesforce Service Cloud]](../../sources/connectors/customer-success/salesforce-service-cloud.md)</li><li>[[!DNL SFTP]](../../sources/connectors/cloud-storage/sftp.md)</li><li>[[!DNL Shopify]](../../sources/connectors/ecommerce/shopify.md)</li></ul> |
| Suporte de API para assimilação de arquivo compactado | Agora é possível visualizar e assimilar arquivos JSON ou delimitados compactados usando fontes de armazenamento na nuvem. Para obter mais informações, consulte o tutorial em [coleta de dados de armazenamento na nuvem usando APIs](../../sources/tutorials/api/collect/cloud-storage.md). |
| Suporte à interface do usuário para carregamento recursivo de arquivos | Agora é possível assimilar pastas inteiras de forma recursiva ao usar uma fonte de armazenamento na nuvem. Ao assimilar uma pasta inteira, você deve garantir que seu conteúdo compartilhe o mesmo schema. Para obter mais informações, consulte o tutorial em [configuração de um fluxo de dados para conectores de armazenamento em nuvem na interface](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md). |

Para saber mais sobre fontes, consulte a [visão geral das origens](../../sources/home.md).
