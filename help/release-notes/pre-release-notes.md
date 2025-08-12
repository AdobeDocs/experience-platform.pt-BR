---
title: Notas de pré-lançamento do Experience Platform
description: Uma visualização das notas de versão mais recentes do Adobe Experience Platform.
hide: true
hidefromtoc: true
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: a26ad18b1e44b3198db9e8a36ad3749ed8a0afa2
workflow-type: tm+mt
source-wordcount: '1116'
ht-degree: 18%

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
>- [Customer Journey Analytics](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/releases/pre-release-notes)
>- [Composição de público-alvo federado](https://experienceleague.adobe.com/pt-br/docs/federated-audience-composition/using/e-release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/pt-br/docs/real-time-cdp-collaboration/using/latest)

**Data de lançamento: agosto de 2025**

Novos recursos e atualizações dos recursos existentes no Adobe Experience Platform:

- [Alertas](#alerts)
- [Destinos](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Serviço de segmentação](#segmentation-service)
- [Origens](#sources)

## Alertas {#alerts}

O Experience Platform permite assinar alertas baseados em eventos para várias atividades do Experience Platform. Você pode assinar diferentes regras de alerta por meio da guia [!UICONTROL Alertas] na interface do usuário do Experience Platform e pode optar por receber mensagens de alerta na própria interface ou por meio de notificações por email.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Alertas de capacidade de taxa de transferência de transmissão | Três novos alertas permitem que os usuários assinem e configurem alertas para gerenciar e monitorar proativamente o desempenho da capacidade de taxa de transferência de transmissão. Os novos alertas incluem quando a taxa de transferência de transmissão atinge 80%, 90% ou excede os limites de capacidade. Para obter mais informações, leia o [guia de regras de alerta de capacidade](../observability/alerts/rules.md#capacity). |

Para obter mais informações sobre alertas, leia a [[!DNL Observability Insights] visão geral](../observability/home.md).

## Destinos {#destinations}

[!DNL Destinations] são integrações pré-criadas com plataformas de destino que permitem a ativação contínua de dados do Experience Platform. É possível usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas de email, publicidade direcionada e muitos outros casos de uso.

**Novos destinos**

| Destino | Descrição |
| --- | --- |
| [!DNL Acxiom Real ID Audience] destino | Use o destino [!DNL Acxiom Real ID Audience Connection] para aprimorar públicos com a tecnologia [!DNL Acxiom's] [Real ID™](https://www.acxiom.com/real-id/real-id/) e ativar públicos para várias plataformas, como [!DNL Altice], [!DNL Ampersand], [!DNL Comcast] e muito mais. |


**Destinos atualizados**

| Destino | Descrição |
| --- | --- |
| Detalhes de expiração da autenticação para [!DNL LinkedIn] destinos | Nunca mais se preocupe com credenciais expiradas. As informações de expiração de conta agora estão visíveis diretamente na interface do Experience Platform, para que você possa ver quando a autenticação do [!DNL LinkedIn] expirará e a renovará antes de causar interrupções nos fluxos de dados. |
| Suporte a criptografia para [!DNL Data Landing Zone] destinos | Proteja seus dados exportados com criptografia. Agora é possível anexar chaves públicas formatadas em RSA para criptografar seus arquivos exportados, proporcionando o mesmo nível de segurança que outros destinos de armazenamento em nuvem oferecem para suas informações confidenciais. |
| Atualização interna de [[!DNL Microsoft Bing]](../destinations/catalog/advertising/bing.md) | A partir de 11 de agosto de 2025, você poderá ver dois cartões **[!DNL Microsoft Bing]** lado a lado no catálogo de destinos. Isso se deve a uma atualização interna do serviço de destinos. O conector de destino **[!DNL Microsoft Bing]** existente foi renomeado para **[!UICONTROL (obsoleto) Microsoft Bing]** e um novo cartão com o nome **[!UICONTROL Microsoft Bing]** está disponível para você. Use a nova conexão do **[!UICONTROL Microsoft Bing]** no catálogo para novos fluxos de dados de ativação. Se você tiver fluxos de dados ativos para o destino **[!UICONTROL (obsoleto) do Microsoft Bing]**, eles serão atualizados automaticamente, portanto, nenhuma ação é necessária. <br><br>Se você estiver criando fluxos de dados por meio da [API de Serviço de Fluxo](https://developer.adobe.com/experience-platform-apis/references/destinations/), atualize o [!DNL flow spec ID] e o [!DNL connection spec ID] para os seguintes valores:<ul><li>ID da especificação de fluxo: `8d42c81d-9ba7-4534-9bf6-cf7c64fbd12e`</li><li>ID de especificação da conexão: `dd69fc59-3bc5-451e-8ec2-1e74a670afd4`</li></ul> Após esta atualização, você pode enfrentar uma **queda no número de perfis ativados** em seus fluxos de dados para [!DNL Microsoft Bing]. Esta queda é causada pela introdução do **requisito de mapeamento ECID** para todas as ativações nesta plataforma de destino. |
| Identificadores adicionais para [!DNL Amazon Ads] destinos | O destino do Amazon Ads agora oferece suporte a novas identidades (`firstName`, `lastName`, `street`, `city`, `state`, `zip`, `country`). Esses campos têm como objetivo melhorar as taxas de correspondência do público-alvo e são transmitidos em texto sem formatação, com hash SHA256 opcional. |
| [!DNL Marketo] consolidação de cartões de destino | Simplifique a configuração de destino do [!DNL Marketo] com nosso cartão de destino unificado. Consolidamos os cartões [!DNL Marketo] V2 e V3 em uma opção simplificada, facilitando a escolha do destino certo e a rápida introdução. |

**Funcionalidade nova ou atualizada**

| Recurso | Descrição |
| --- | --- |
| Estender programações de exportação do conjunto de dados para fluxos de dados criados antes de novembro de 2024 | Se sua organização tiver fluxos de dados de exportação do conjunto de dados criados antes de novembro de 2024, esses fluxos de dados deixarão de funcionar em 1º de setembro de 2025. Se precisar que os fluxos de dados continuem exportando dados após 1º de setembro de 2025, estenda suas agendas para cada destino para o qual você está exportando conjuntos de dados seguindo as etapas no [este guia](../destinations/ui/dataset-expiration-update.md). |
| Recursos aprimorados de pesquisa, filtragem e marcação para destinos | Melhore o fluxo de trabalho de gerenciamento de destino com recursos aprimorados de pesquisa, filtragem e marcação nas guias Procurar e Contas. Agora é possível pesquisar fluxos de dados e contas específicos por nome, filtrar por vários critérios, incluindo plataforma de destino, status e datas, e criar tags personalizadas para organizar seus destinos. A classificação de colunas também está disponível para campos principais, como último tempo de execução do fluxo de dados, facilitando a identificação e o gerenciamento das conexões de destino. |

Para obter mais informações, leia a [Visão geral dos Destinos](../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

O XDM é uma especificação de código aberto que fornece estruturas e definições comuns (esquemas) para dados trazidos para o Experience Platform. Ao aderir aos padrões do XDM, todos os dados de experiência do cliente podem ser incorporados em uma representação comum para fornecer insights de maneira mais rápida e integrada. Você pode obter insights valiosos sobre ações de clientes, definir públicos-alvo por meio de segmentos e usar atributos de clientes para fins de personalização.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Esquemas Baseados Em Modelo | Simplifique a modelagem de dados com esquemas baseados em modelo. Agora é possível criar esquemas mais facilmente com exemplos e orientação abrangentes. Esse recurso está disponível no momento para os titulares de licença do Campaign Orchestration e será expandido para os clientes do Data Distiller em GA, tornando a modelagem de dados mais acessível e eficiente. |

Para obter mais informações, leia a [visão geral do XDM](../xdm/home.md).

## Serviço de segmentação {#segmentation-service}

O [!DNL Segmentation Service] define um subconjunto específico de perfis descrevendo os critérios que distinguem um grupo de pessoas na sua base de clientes que pode ser direcionado por campanhas de marketing. Os públicos podem ser baseados em dados de registro (como informações demográficas) ou eventos de séries temporais que representam interações do cliente com sua marca.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| ------- | ----------- |
| Estimativas de público | As estimativas de público-alvo agora são geradas automaticamente no Construtor de segmentos. Esse valor será atualizado sempre que você modificar o público-alvo e sempre refletirá as regras de público-alvo mais recentes. |

Para obter mais informações, leia a visão geral[&#128279;](../segmentation/home.md) do [!DNL Segmentation Service] .

## Origens {#sources}

A Experience Platform fornece uma API RESTful e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar a sistemas de armazenamento externos e serviços de CRM, definir períodos para execuções de ingestão e gerenciar a taxa de transferência de ingestão de dados.

**Funcionalidade nova ou atualizada**

| Recurso | Descrição |
| --- | --- |
| [!BADGE Suporte ao Link Privado do Beta]{type=Informative} na interface do usuário | Mantenha seus dados protegidos com conexões de rede privada. Agora é possível criar endpoints privados e configurar fluxos de dados que ignoram a Internet pública, proporcionando maior segurança e isolamento de rede para seus dados confidenciais. |
| Atualizações na documentação de origem de [!DNL Marketo] | Obtenha visibilidade completa de como seus dados do [!DNL Marketo] são transformados quando entram no Experience Platform. Todos os mapeamentos de campo agora incluem explicações detalhadas das transformações de dados, para que você possa entender exatamente como seu `PersonID` se torna `leadID` e `eventType` se torna `activityType`. |
| Suporte para autenticação de entidade de serviço para [!DNL Azure Blob Storage] | Agora você pode conectar sua conta do [!DNL Azure Blob Storage] à Experience Platform com a autenticação da entidade de serviço. |

Para obter mais informações, leia a [visão geral de fontes](../sources/home.md).

<!--

## Query Service {#query-service}

Adobe Experience Platform Query Service provides a robust SQL interface for data analysis and exploration across the platform.

**New or updated features**

| Feature | Description |
| ------- | ----------- |
| Data Distiller Session Management | Take control of your data analysis sessions with enhanced session management. You can now monitor and manage your sessions more effectively across development and production environments, giving you better visibility into your query performance and resource usage. |

For more information, read the [Query Service overview](../query-service/home.md).

## B2B CDP {#b2b-cdp}

Real-Time CDP B2B Edition provides comprehensive B2B customer data management capabilities, enabling organizations to build unified customer profiles, create sophisticated B2B audiences, and activate data across various marketing channels.

**New or updated features**

| Feature | Description |
| ------- | ----------- |
| Lookup Support for B2B Classes Only | Streamline your B2B data access with focused lookup support. You can now look up Person (Profile), Experience Events, Account, and Opportunity entities directly through the Entities API. This simplified approach helps you access the most important B2B data more efficiently while reducing complexity. |
| B2B Namespace and Schema Updates | Experience a cleaner, more streamlined B2B data model. We've simplified the B2B namespace and schema structure by removing complex relationship mappings and non-primary identity support for certain B2B classes. This makes your B2B data easier to work with and understand. |

For more information, read the [Real-Time CDP B2B Edition overview](../rtcdp/b2b-overview.md).

-->
