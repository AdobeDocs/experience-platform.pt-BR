---
title: Notas de pré-lançamento do Experience Platform
description: Uma visualização das notas de versão mais recentes do Adobe Experience Platform.
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: de95e9a51c979e9249ddf9ceb262fc521d2b38f4
workflow-type: tm+mt
source-wordcount: '1008'
ht-degree: 14%

---

# Notas de pré-lançamento do Adobe Experience Platform

>[!IMPORTANT]
>
>Este documento é uma **visualização** das notas de versão do mês atual. Os itens da versão estão sujeitos a alterações e podem ser adicionados ou removidos na versão final.

>[!TIP]
>
>Consulte a documentação a seguir para obter as notas de versão de outros aplicativos da Adobe Experience Platform:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/releases/pre-release-notes)
>- [Composição de público-alvo federado](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/e-release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/en/docs/real-time-cdp-collaboration/using/latest)

**Data de lançamento: outubro de 2025**

Novos recursos e atualizações dos recursos existentes no Adobe Experience Platform:

- [Alertas](#alerts)
- [Destinos](#destinations)
- [Serviço de segmentação](#segmentation-service)
- [Origens](#sources)

## Alertas {#alerts}

O Experience Platform permite assinar alertas baseados em eventos para várias atividades do Experience Platform. Você pode assinar diferentes regras de alerta por meio da guia [!UICONTROL Alertas] na interface do usuário do Experience Platform e pode optar por receber mensagens de alerta na própria interface ou por meio de notificações por email.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Alerta de taxa de falha de destino | Um novo alerta foi adicionado para destinos: **A taxa de falha de destino excede o limite**. Esse alerta notifica quando o número de registros com falha durante a ativação de dados excedeu o limite permitido, permitindo que você responda rapidamente aos problemas de ativação. |

{style="table-layout:auto"}

Para obter mais informações sobre alertas, leia a [[!DNL Observability Insights] visão geral](../observability/home.md).

## Destinos {#destinations}

[!DNL Destinations] são integrações pré-criadas com plataformas de destino que permitem a ativação contínua de dados do Experience Platform. É possível usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas de email, publicidade direcionada e muitos outros casos de uso.

**Destinos novos ou atualizados**

| Destino | Descrição |
| --- | --- |
| [!DNL AdForm] | Use este destino para enviar públicos-alvo da Adobe Real-Time CDP para o [!DNL AdForm] para ativação com base na Experience Cloud ID (ECID) e na Fusão de ID do [!DNL AdForm]. O ID Fusion do [!DNL AdForm] é um serviço de resolução de ID que permite ativar os públicos originais com base na Experience Cloud ID (ECID). |
| [!DNL Amazon Ads] | Adicionamos suporte adicional a identificadores pessoais, como `firstName`, `lastName`, `street`, `city`, `state`, `zip` e `country`. Mapear esses campos como identidades de destino pode melhorar as taxas de correspondência do público-alvo. |
| [!DNL Snowflake Batch] (Disponibilidade limitada) | Crie um compartilhamento de dados [!DNL Snowflake] em tempo real para receber atualizações diárias de público diretamente como tabelas compartilhadas em sua conta. Essa integração está disponível atualmente para organizações de clientes provisionadas na região do VA7. |
| [!DNL Snowflake Streaming] (Disponibilidade limitada) | Crie um compartilhamento de dados [!DNL Snowflake] em tempo real para receber atualizações de público-alvo de transmissão diretamente como tabelas compartilhadas na sua conta. Essa integração está disponível atualmente para organizações de clientes provisionadas na região do VA7. |

**Funcionalidade nova ou atualizada**

| Recurso | Descrição |
| --- | --- |
| Suporte para criptografia do lado do servidor [!DNL AES256] em [!DNL Amazon S3] destinos | [!DNL Amazon S3] destinos agora oferecem suporte à criptografia do lado do servidor do [!DNL AES256], fornecendo segurança aprimorada para seus dados exportados. Você pode configurar esse método de criptografia ao configurar ou atualizar suas conexões de destino do [!DNL Amazon S3], garantindo que seus dados sejam criptografados em repouso usando algoritmos de criptografia [!DNL AES256] padrão do setor. Para obter mais informações, leia a [[!DNL Amazon] documentação](https://docs.aws.amazon.com/AmazonS3/latest/userguide/UsingEncryption.html). |
| [Vários novos destinos que oferecem suporte ao monitoramento no nível do público-alvo](../dataflows/ui/monitor-destinations.md#audience-level-view) | Os seguintes destinos agora oferecem suporte ao monitoramento no nível do público-alvo: <ul><li>[!DNL Airship Tags]</li><li>(API) [!DNL Salesforce Marketing Cloud]</li><li>[!DNL Marketo Engage]</li><li>[!DNL Microsoft Bing]</li><li>(V1) [!DNL Pega CDH Realtime Audience]</li><li>(V2) [!DNL Pega CDH Realtime Audience]</li><li>Engajamento na conta de [!DNL Salesforce Marketing Cloud]</li><li>[!DNL The Trade Desk]</li></ul> |
| Correção das medidas de proteção de exportação do conjunto de dados | Uma correção foi implementada nas medidas de proteção de exportação do conjunto de dados. Anteriormente, alguns conjuntos de dados que incluíam uma coluna de carimbo de data e hora, mas _não_ com base no esquema de Eventos de experiência XDM, eram tratados incorretamente como conjuntos de dados de Eventos de experiência, limitando as exportações a uma janela de retrospectiva de 365 dias. A proteção de lookback de 365 dias documentada agora se aplica exclusivamente aos conjuntos de dados de Eventos de experiência. Os conjuntos de dados que usam qualquer esquema diferente do esquema XDM Experience Events agora são regidos pela proteção de 10 bilhões de registros. Alguns clientes podem ver maiores números de exportação para conjuntos de dados que incorretamente se enquadravam na janela de retrospectiva de 365 dias. Isso permite exportar conjuntos de dados para workflows preditivos que têm uma longa janela de pesquisa. Para obter mais informações, leia as [medidas de proteção de exportação do conjunto de dados](../destinations/guardrails.md#dataset-exports). |
| Relatórios aprimorados no nível do público-alvo para destinos corporativos | Melhoria na lógica de relatórios no nível do público-alvo para destinos corporativos. Após esta versão, os clientes verão números mais precisos de relatórios de público-alvo que incluem apenas públicos-alvo relevantes para o destino selecionado. Esse ajuste de monitoramento garante que os relatórios incluam apenas públicos-alvo mapeados no fluxo de dados, fornecendo insights mais claros sobre a ativação de dados real. Isso não afeta a quantidade de dados que está sendo ativada — trata-se meramente de um aprimoramento de monitoramento para melhorar a precisão dos relatórios. |

Para obter mais informações, leia a [Visão geral dos Destinos](../destinations/home.md).

## Serviço de segmentação {#segmentation-service}

O [!DNL Segmentation Service] define um subconjunto específico de perfis descrevendo os critérios que distinguem um grupo de pessoas na sua base de clientes que pode ser direcionado por campanhas de marketing. Os públicos podem ser baseados em dados de registro (como informações demográficas) ou eventos de séries temporais que representam interações do cliente com sua marca.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| ------- | ----------- |
| Monitoramento da segmentação de transmissão | O monitoramento em tempo real da segmentação por transmissão oferece transparência às métricas de taxa de avaliação, latência e qualidade de dados nos níveis de sandbox, conjunto de dados e público-alvo. Isso oferece suporte a alertas proativos e insights acionáveis para ajudar os engenheiros de dados a identificar violações de capacidade e problemas de assimilação. As métricas de monitoramento incluem taxa de avaliação, latência de assimilação P95, bem como registros recebidos, avaliados, com falha e ignorados. Os recursos visualizar por conjunto de dados e visualizar por público-alvo fornecem visibilidade abrangente sobre novos perfis qualificados e desqualificados. |

Para obter mais informações, leia a visão geral](../segmentation/home.md) do [[!DNL Segmentation Service] .

## Origens {#sources}

A Experience Platform fornece uma API RESTful e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar a sistemas de armazenamento externos e serviços de CRM, definir períodos para execuções de ingestão e gerenciar a taxa de transferência de ingestão de dados.

**Fontes novas ou atualizadas**

| Fonte | Descrição |
| --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL Talon.one] fontes de dados de fidelidade | Use as fontes [!DNL Talon.One] para assimilar dados de fidelidade em lote e streaming na Experience Platform. O conector oferece suporte à transmissão de dados de perfil, dados de transação e dados de fidelidade, incluindo pontos ganhos, pontos resgatados, pontos expirados e dados de camada. |

**Fontes atualizadas**

| Fonte | Descrição |
| --- | --- |
| Disponibilidade Geral de [!DNL Google Ads] origem (somente API) | A versão da API da origem [!DNL Google Ads] agora está em Disponibilidade Geral. A documentação da API foi atualizada para refletir que a versão mais recente agora é a `v21`, e o Experience Platform oferece suporte a todas as versões v19 e superiores. A versão da interface do usuário permanece na versão beta e oferece suporte somente à assimilação única. Para usar a assimilação de dados incremental, use a rota da API. |
| Suporte a rede virtual [!DNL Azure Event Hubs] | O Adobe agora oferece suporte explícito a conexões de rede virtual com os Hubs de Eventos do Azure, permitindo a transferência de dados em redes privadas em vez de redes públicas. Os clientes podem Experience Platform o incluir na lista de permissões VNet para rotear o tráfego dos Hubs de eventos de forma privada por meio do backbone privado do Azure, fornecendo segurança e conformidade aprimoradas para fluxos de trabalho de assimilação de dados. |

Para obter mais informações, leia a [visão geral de fontes](../sources/home.md).
