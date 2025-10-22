---
title: Notas de versão da Adobe Experience Platform de outubro de 2025
description: As notas de versão de outubro de 2025 da Adobe Experience Platform.
source-git-commit: 199acd8d3bdbb0e89fc1ab881bff4d94063b7f78
workflow-type: tm+mt
source-wordcount: '920'
ht-degree: 13%

---

# Notas de versão da Adobe Experience Platform

>[!TIP]
>
>Consulte a documentação a seguir para obter as notas de versão de outros aplicativos da Adobe Experience Platform:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/releases/pre-release-notes)
>- [Composição de público-alvo federado](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/e-release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/en/docs/real-time-cdp-collaboration/using/latest)

**Data de lançamento: 22 de outubro de 2025**

Novos recursos e atualizações dos recursos existentes no Adobe Experience Platform:

- [Alertas](#alerts)
- [Destinos](#destinations)
- [Origens](#sources)

## Alertas {#alerts}

O Experience Platform permite assinar alertas baseados em eventos para várias atividades do Experience Platform. Você pode assinar diferentes regras de alerta por meio da guia [!UICONTROL Alerts] na interface do usuário do Experience Platform e pode optar por receber mensagens de alerta na própria interface do usuário ou por notificações de email.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Alerta de taxa de falha de destino | Um novo alerta foi adicionado para destinos: **A taxa de falha de destino excede o limite**. Esse alerta notifica quando o número de registros com falha durante a ativação de dados excedeu o limite permitido, permitindo que você responda rapidamente aos problemas de ativação. Leia a documentação sobre [regras padrão de alertas](../../observability/alerts/rules.md) para obter mais informações. |

{style="table-layout:auto"}

Para obter mais informações sobre alertas, leia a [[!DNL Observability Insights] visão geral](../../observability/home.md).

## Destinos {#destinations}

[!DNL Destinations] são integrações pré-criadas com plataformas de destino que permitem a ativação contínua de dados do Experience Platform. É possível usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas de email, publicidade direcionada e muitos outros casos de uso.

**Destinos novos ou atualizados**

| Destino | Descrição |
| --- | --- |
| [!DNL Adform] | Use este destino para enviar públicos-alvo da Adobe Real-Time CDP para o [!DNL Adform] para ativação com base na Experience Cloud ID (ECID) e na Fusão de ID do [!DNL Adform]. O ID Fusion do [!DNL Adform] é um serviço de resolução de ID que permite ativar os públicos originais com base na Experience Cloud ID (ECID). Leia a [[!DNL Adform] documentação](../../destinations/catalog/advertising/adform.md) para obter mais informações |
| [!DNL Amazon Ads] | Foi adicionado suporte adicional ao identificador pessoal. Isso inclui campos como `firstName`, `lastName`, `street`, `city`, `state`, `zip` e `country`. Mapear esses campos como identidades de destino pode melhorar as taxas de correspondência do público-alvo. Leia a [[!DNL Amazon Ads] documentação](../../destinations/catalog/advertising/amazon-ads.md) para obter mais informações. |

{style="table-layout:auto"}

**Funcionalidade nova ou atualizada**

| Recurso | Descrição |
| --- | --- |
| Suporte para criptografia do lado do servidor [!DNL AES256] em [!DNL Amazon S3] destinos | [!DNL Amazon S3] destinos agora oferecem suporte à criptografia do lado do servidor do [!DNL AES256], fornecendo segurança aprimorada para seus dados exportados. Você pode configurar esse método de criptografia ao configurar ou atualizar suas conexões de destino do [!DNL Amazon S3], garantindo que seus dados sejam criptografados em repouso usando algoritmos de criptografia [!DNL AES256] padrão do setor. Para obter mais informações, leia a [[!DNL Amazon] documentação](https://docs.aws.amazon.com/AmazonS3/latest/userguide/UsingEncryption.html). |
| [Vários novos destinos que oferecem suporte ao monitoramento no nível do público-alvo](../../dataflows/ui/monitor-destinations.md#audience-level-view) | Os seguintes destinos agora oferecem suporte ao monitoramento no nível do público-alvo: <ul><li>[!DNL Airship Tags]</li><li>(API) [!DNL Salesforce Marketing Cloud]</li><li>[!DNL Marketo Engage]</li><li>[!DNL Microsoft Bing]</li><li>(V1) [!DNL Pega CDH Realtime Audience]</li><li>(V2) [!DNL Pega CDH Realtime Audience]</li><li>Engajamento na conta de [!DNL Salesforce Marketing Cloud]</li><li>[!DNL The Trade Desk]</li></ul> |
| Correção das medidas de proteção de exportação do conjunto de dados | Uma correção foi implementada nas medidas de proteção de exportação do conjunto de dados. Anteriormente, alguns conjuntos de dados que incluíam uma coluna de carimbo de data e hora, mas _não_ com base no esquema de Eventos de experiência XDM, eram tratados incorretamente como conjuntos de dados de Eventos de experiência, limitando as exportações a uma janela de retrospectiva de 365 dias. A proteção de lookback de 365 dias documentada agora se aplica exclusivamente aos conjuntos de dados de Eventos de experiência. Os conjuntos de dados que usam qualquer esquema diferente do esquema XDM Experience Events agora são regidos pela proteção de 10 bilhões de registros. Alguns clientes podem ver maiores números de exportação para conjuntos de dados que incorretamente se enquadravam na janela de retrospectiva de 365 dias. Isso permite exportar conjuntos de dados para workflows preditivos que têm uma longa janela de pesquisa. Para obter mais informações, leia as [medidas de proteção de exportação do conjunto de dados](../../destinations/guardrails.md#dataset-exports). |
| Relatórios aprimorados no nível do público-alvo para destinos corporativos | Após esta versão, os clientes verão números mais precisos de relatórios de público-alvo que incluem apenas públicos-alvo relevantes para o destino selecionado. Esse ajuste de monitoramento garante que os relatórios incluam apenas públicos-alvo mapeados no fluxo de dados, fornecendo insights mais claros sobre a ativação de dados real. Isso não afeta a quantidade de dados que está sendo ativada — trata-se meramente de um aprimoramento de monitoramento para melhorar a precisão dos relatórios. |

{style="table-layout:auto"}

Para obter mais informações, leia a [Visão geral dos Destinos](../../destinations/home.md).

<!--
| [!DNL Snowflake Batch] (Limited availability) | Create a live [!DNL Snowflake] data share to receive daily audience updates directly as shared tables into your account. This integration is currently available for customer organizations provisioned in the VA7 region. |
| [!DNL Snowflake Streaming] (Limited availability) | Create a live [!DNL Snowflake] data share to receive streaming audience updates directly as shared tables into your account. This integration is currently available for customer organizations provisioned in the VA7 region. |
-->

## Origens {#sources}

A Experience Platform fornece uma API RESTful e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar a sistemas de armazenamento externos e serviços de CRM, definir períodos para execuções de ingestão e gerenciar a taxa de transferência de ingestão de dados.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Alteração na criação do conjunto de dados para a origem do Adobe Analytics | Como parte do processo de criação de fluxo de dados entre o Adobe Analytics e o Experience Platform, um conjunto de dados é criado por meio do Serviço de catálogo. Esse conjunto de dados serve como um container para que os dados cheguem ao. Atualmente, esse processo envolve uma DataSource ID que é retirada do conjunto de relatórios do Analytics, enviada para o Serviço de catálogo e, em seguida, é associada ao conjunto de dados recém-criado. Após a alteração, a opção para fornecer a ID da fonte de dados não estará mais disponível durante a criação do conjunto de dados. Portanto, os novos conjuntos de dados criados pela fonte do Analytics não terão mais uma ID da fonte de dados associada a ele no Serviço de catálogo. Essa alteração se aplica somente aos metadados e não altera de forma alguma o armazenamento de dados no conjunto de dados. No entanto, é importante saber que a ID da fonte de dados fornecida pelo Serviço de catálogo não estará mais disponível nos conjuntos de dados recém-criados para o Adobe Analytics. Leia a [documentação de origem do Adobe Analytics](../../sources/connectors/adobe-applications/analytics.md) para obter mais informações sobre o conector de origem do Adobe Analytics. |
| Disponibilidade Geral de [!DNL Google Ads] origem (somente API) | A versão da API [ da origem  [!DNL Google Ads]](../../sources/tutorials/api/create/advertising/ads.md) agora está em Disponibilidade Geral. A documentação da API foi atualizada para refletir que a versão mais recente agora é a `v21`, e o Experience Platform oferece suporte a todas as versões v19 e superiores. [A versão da interface do usuário](../../sources/tutorials/ui/create/advertising/ads.md) permanece na versão beta e dá suporte apenas à assimilação única. Para usar a assimilação de dados incremental, use a rota da API. |
| Suporte a rede virtual [!DNL Azure Event Hubs] | O Adobe agora oferece suporte explícito a conexões de rede virtual com [[!DNL Azure Event Hubs]](../../sources/connectors/cloud-storage/eventhub.md), permitindo a transferência de dados em redes privadas, em vez de redes públicas. Os clientes podem Experience Platform o incluir na lista de permissões VNet para rotear o tráfego dos Hubs de eventos de forma privada por meio do backbone privado do Azure, fornecendo segurança e conformidade aprimoradas para fluxos de trabalho de assimilação de dados. |

{style="table-layout:auto"}

Para obter mais informações, leia a [visão geral de fontes](../../sources/home.md).

<!--
| Source | Description |
| --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL Talon.one] sources for loyalty data | Use the [[!DNL Talon.One] sources](../../sources/connectors/loyalty/talon-one.md) to ingest batch and streaming loyalty data into Experience Platform. The connector supports streaming of profile data, transaction data, and loyalty data including points earned, points redeemed, points expired, and tier data. For more information, read the [!DNL Talon.One] [batch](../../sources/tutorials/ui/create/loyalty/talon-one-batch.md) and [streaming](../../sources/tutorials/ui/create/loyalty/talon-one-streaming.md) documentation. |
-->