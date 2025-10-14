---
title: Notas da versão de março de 2025 da Adobe Experience Platform
description: As notas da versão de março de 2025 da Adobe Experience Platform.
exl-id: 3da1c912-2581-4afa-bd21-0b8303531dcd
source-git-commit: ca2793f6e498f63bffb0f30ebc9797ea5ed52a70
workflow-type: tm+mt
source-wordcount: '1248'
ht-degree: 20%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: quinta-feira, 26 de março de 2025**

Atualizações dos recursos e da documentação existentes no Adobe Experience Platform:

- [Notas de versão da Adobe Experience Platform](#adobe-experience-platform-release-notes)
   - [Painéis](#dashboards)
   - [Destinos](#destinations)
   - [Composição de público-alvo federado](#federated-audience-composition)
   - [Serviço de segmentação](#segmentation-service)
   - [Origens](#sources)

## Painéis {#dashboards}

O Experience Platform fornece vários painéis por meio dos quais você pode visualizar insights importantes sobre os dados de sua organização, conforme capturados durante instantâneos diários.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| ------- | ----------- |
| Painel de uso de licença baseado em métricas | O painel de uso de licença agora inclui uma interface simplificada com duas guias: **Métricas** e **Produtos**. A nova guia **Métricas** oferece uma exibição consolidada de todas as métricas de licença rastreáveis dos produtos comprados. Cada métrica inclui um ícone de informações em linha que exibe descrições e produtos associados. Os usuários podem selecionar sandboxes de produção ou desenvolvimento, visualizar tendências de uso histórico em gráficos interativos e exportar dados específicos da sandbox como arquivos CSV. Essas atualizações simplificam o rastreamento de licenças e fornecem insights mais claros. Saiba mais no [guia do painel de uso da licença](../../dashboards/guides/license-usage.md) para obter mais detalhes. |
| Frequência de previsão atualizada | O painel de uso de licença agora fornece insights mais precisos sobre o consumo projetado, atualizando as previsões de uso **weekly** em vez de mensalmente. Essas previsões mostram o uso estimado nas próximas seis semanas com base nas tendências recentes. Essa alteração permite tomada de decisão mais rápida, intervenção mais rápida e planejamento de licença aprimorado. Consulte o [guia do painel de uso da licença](../../dashboards/guides/license-usage.md#predicted-usage) para obter detalhes. |
| Descrições de métrica atualizadas na interface do | As definições de métrica no painel de uso da licença foram revisadas para maior clareza e consistência. Agora você pode exibir descrições atualizadas diretamente no painel usando ícones de informações incorporadas ao lado de cada métrica na guia **Métricas**. Essas atualizações facilitam a compreensão de como as métricas são rastreadas e a quais produtos elas se aplicam. Consulte o [guia do painel de uso da licença](../../dashboards/guides/license-usage.md#available-metrics) para obter mais detalhes. |

{style="table-layout:auto"}

Para obter mais informações sobre painéis, incluindo como conceder permissões de acesso e criar widgets personalizados, comece lendo a [visão geral dos painéis](../../dashboards/home.md).

## Destinos {#destinations}

[!DNL Destinations] são integrações pré-construídas com plataformas de destino que permitem a ativação perfeita de dados da Adobe Experience Platform. É possível usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas de email, publicidade direcionada e muitos outros casos de uso.

**Destinos novos ou atualizados** {#new-updated-destinations}

| Destino | Descrição |
| --- | --- |
| [Conexão de pessoas do Demandbase](/help/destinations/catalog/advertising/demandbase-people.md) | Use a conexão [!DNL Demandbase People] para ativar perfis para suas campanhas do Demandbase para direcionamento de público, personalização e supressão. |
| [Conexão de conta do Bombora](/help/destinations/catalog/advertising/bombora.md) | Use a conexão [!DNL Bombora] para ativar perfis para suas campanhas do Bombora para direcionamento de público, personalização e supressão, com base em [públicos-alvo de conta](/help/segmentation/types/account-audiences.md). |
| Atualização de [Atributos da Aeronave](/help/destinations/catalog/mobile-engagement/airship-attributes.md) | A partir de 25 de março de 2025, você poderá ver dois cartões **[!UICONTROL Atributos da aeronave]** lado a lado no catálogo de destinos. Isso se deve a uma atualização interna do serviço de destinos. O conector de destino **[!UICONTROL Atributos de Dirigível]** existente foi renomeado para **[!UICONTROL (Obsoleto) Atributos de Dirigível]** e uma nova placa com o nome **[!UICONTROL Atributos de Dirigível]** está disponível para você. <br> Use a conexão **[!UICONTROL Atributos da Aeronave]** no catálogo para novos fluxos de dados de ativação. Se você tiver fluxos de dados ativos para o destino [!DNL (Deprecated) Airship Attributes], eles serão atualizados automaticamente, portanto, nenhuma ação é necessária. <br> Se você estiver criando fluxos de dados por meio da [API de Serviço de Fluxo](https://developer.adobe.com/experience-platform-apis/references/destinations/), atualize o [!DNL flow spec ID] e o [!DNL connection spec ID] para os seguintes valores: <ul><li> ID da especificação de fluxo: `a862e0be-966e-4e5a-80d3-1bb566461986`</li><li> ID de especificação da conexão: `594bc002-4a47-49b7-8a98-ac0d21045502`</li> </ul> |

{style="table-layout:auto"}

**Funcionalidade nova ou atualizada** {#destinations-new-updated-functionality}

| Recurso | Descrição |
| --- | --- |
| [Aprimoramentos na precisão dos relatórios para destinos de streaming](../../dataflows/ui/monitor-destinations.md) | A partir de março de 2025, a Adobe está lançando uma atualização para aumentar a precisão dos relatórios para destinos de transmissão. Esse aprimoramento garante um melhor alinhamento entre os relatórios no Experience Platform e as plataformas de destino. <br> Antes desta atualização, **[!UICONTROL Falha nas identidades]** incluiu todas as tentativas de ativação. Após essa atualização, somente a última tentativa de ativação será incluída na contagem total. <br> Esse aprimoramento se aplica a todos os destinos de streaming. <br> Após esse aprimoramento, os usuários de destinos de streaming podem observar uma queda esperada em sua contagem de **[!UICONTROL Falha de identidades]**. |
| [Suporte à exportação de campos do tipo mapa para destinos corporativos e de borda](/help/destinations/ui/export-arrays-maps-objects.md) | Ao exportar dados para os destinos do [Amazon Kinesis](/help/destinations/catalog/cloud-storage/amazon-kinesis.md), [HTTP API](/help/destinations/catalog/streaming/http-destination.md) e [Azure Event Hubs](/help/destinations/catalog/cloud-storage/azure-event-hubs.md), agora é possível selecionar campos do tipo mapa para exportação na etapa de mapeamento do fluxo de trabalho de ativação. <br> ![Exportar campo do tipo mapa para destino da empresa.](../2025/assets/march/export-map.png "Exportar campo do tipo mapa para destino da empresa."){width="250" align="center" zoomable="yes"} |

{style="table-layout:auto"}

Para obter mais informações, leia a [visão geral de destinos](../../destinations/home.md).

## Composição de público-alvo federado {#federated-audience-composition}

Para obter informações sobre as atualizações mais recentes da Federated Audience Composition, leia as [notas de versão dedicadas](https://experienceleague.adobe.com/pt-br/docs/federated-audience-composition/using/release-notes) aqui.

## Serviço de segmentação {#segmentation-service}

O [!DNL Segmentation Service] define um subconjunto específico de perfis descrevendo os critérios que distinguem um grupo de pessoas na sua base de clientes que pode ser direcionado por campanhas de marketing. Os segmentos podem ser baseados em dados de registro (como informações demográficas) ou em eventos de séries temporais que representam interações de clientes com sua marca.

| Recurso | Descrição |
| ------- | ----------- |
| Aprimoramentos no Construtor de público-alvo da conta | No Audience Builder, agora é possível filtrar atributos para exibir somente atributos preenchidos, bem como exibir dados de resumo para esses atributos preenchidos. Mais informações sobre esses aprimoramentos podem ser encontradas na documentação do [Audience Builder](../../rtcdp/segmentation/audience-builder.md). |
| Disponibilidade geral da avaliação flexível do público-alvo | A avaliação flexível do público-alvo agora está disponível! Você pode usar a avaliação flexível do público-alvo para criar novos públicos-alvo sob demanda para comunicações sensíveis ao tempo. Mais informações sobre a avaliação flexível do público podem ser encontradas na [visão geral da avaliação flexível do público](../../segmentation/methods/flexible-audience-evaluation.md). |

Para obter mais informações sobre o [!DNL Segmentation Service], consulte a [Visão geral de segmentação](../../segmentation/home.md).

## Origens {#sources}

A Experience Platform fornece uma API RESTful e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar a sistemas de armazenamento externos e serviços de CRM, definir períodos para execuções de ingestão e gerenciar a taxa de transferência de ingestão de dados.

Use fontes na Experience Platform para assimilar dados de um aplicativo da Adobe ou de uma fonte de dados de terceiros.

**Novas fontes**

| Recurso | Descrição |
| --- | --- |
| [!DNL Bombora Intent] | A origem [!DNL Bombora Intent] agora está disponível no catálogo de origens. Use esta fonte para: <ul><li>Integre os dados de Intenção de sobretensão da empresa da Bombora para identificar contas que pesquisam ativamente seus produtos ou serviços.</li><li>Priorize contas no mercado para criar segmentos precisos e executar campanhas ABM hiperdirecionadas, garantindo que seus esforços de marketing se concentrem nas contas com maior probabilidade de conversão.</li><li>Aproveite estratégias orientadas por intenções para otimizar os gastos com anúncios, aumentar o engajamento e maximizar o ROI.</li></ul> Para obter mais informações, leia o guia em [conectando sua [!DNL Bombora] conta à Experience Platform](../../sources/tutorials/ui/create/data-partners/bombora.md). |
| [!DNL Demandbase Intent] | A fonte [!DNL Demandbase Intent], já está disponível no catálogo de fontes. Use esta fonte para: <ul><li>Integre os dados de Intenção de conta do Demandbase para identificar contas de alto interesse com base em compromissos em tempo real.</li><li>Ao priorizar os sinais de intenção mais fortes, você pode criar segmentos precisos e fornecer campanhas hiperdirecionadas para garantir que seus esforços de marketing se concentrem nas contas com maior probabilidade de conversão.</li><li>Ative estratégias orientadas por intenção para permitir a otimização de gastos com anúncios, maior engajamento e maior ROI.</li></ul> Para obter mais informações, leia o guia em [conectando sua [!DNL Demandbase] conta à Experience Platform](../../sources/tutorials/ui/create/data-partners/demandbase.md). |

{style="table-layout:auto"}

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Aprimoramentos na origem [!DNL Google Ads] | Agora você pode usar a [[!DNL Google Ads] origem](../../sources/connectors/advertising/ads.md) para assimilar dados agregados. Você pode usar o [!DNL Google Ads Query Builder] para especificar os atributos, segmentos e recursos que deseja assimilar no Experience Platform. Para obter mais informações, leia o guia em [conectando sua [!DNL Google Ads] conta à Experience Platform](../../sources/tutorials/ui/create/advertising/ads.md). |
| Aprimoramentos na origem [!DNL Microsoft Dynamics] | Agora você pode especificar a chave primária de uma determinada tabela [!DNL Microsoft Dynamics] ao explorar o conteúdo e a estrutura de seus dados. Use este recurso para otimizar suas consultas com a origem [!DNL Microsoft Dynamics]. Para obter mais informações, leia o guia em [conectando sua [!DNL Microsoft Dynamics] origem à Experience Platform usando a API](../../sources/tutorials/api/create/crm/ms-dynamics.md). |
| Suporte para autenticação de chave de API em fontes de autoatendimento (SDK em lote) | Agora você pode usar a autenticação de chave de API como um tipo de autenticação ao integrar uma nova fonte com Fontes de autoatendimento (SDK em lote). Para obter mais informações, leia o guia em [configurando sua especificação de autenticação no Batch SDK](../../sources/sources-sdk/config/authspec.md). |
| Suporte para controle de acesso baseado em atributos nas origens | Agora você pode usar funções de controle de acesso baseadas em atributos em relação aos fluxos de dados de origens. Leia os seguintes guias para obter mais informações: <ul><li>[Aplicar rótulos aos seus fluxos de dados de fontes usando a API](../../sources/tutorials/api/labels.md)</li><li>[Aplique rótulos aos seus fluxos de dados de fontes usando a interface &#x200B;](../../sources/tutorials/ui/labels.md). |

{style="table-layout:auto"}

Para obter mais informações, leia a [visão geral de fontes](../../sources/home.md).
