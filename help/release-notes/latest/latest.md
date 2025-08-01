---
title: Notas de versão da Adobe Experience Platform de julho de 2025
description: As notas de versão de julho de 2025 da Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: b0c2d5535bb4cdf7d00eaca43d65f744276494f3
workflow-type: tm+mt
source-wordcount: '1574'
ht-degree: 13%

---

# Notas de versão da Adobe Experience Platform

>[!TIP]
>
>Consulte a documentação a seguir para obter as notas de versão de outros aplicativos da Adobe Experience Platform:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/releases/pre-release-notes)
>- [Composição de público-alvo federado](https://experienceleague.adobe.com/pt-br/docs/federated-audience-composition/using/e-release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/pt-br/docs/real-time-cdp-collaboration/using/latest)

**Data de lançamento: quarta-feira, 29 de julho de 2025**

Novos recursos e atualizações dos recursos existentes no Adobe Experience Platform:

- [Capacidade](#capacity)
- [Destinos](#destinations)
- [Ingestão de dados](#data-ingestion)
- [Real-Time CDP B2B Edition](#b2b)
- [Sandboxes](#sandboxes)
- [Serviço de segmentação](#segmentation-service)
- [Origens](#sources)


## Capacidade {#capacity}

>[!AVAILABILITY]
>
>Esse recurso estará disponível para uso, dependendo da sua região. Para usuários nas Américas, isso estará disponível a partir de 11 de agosto. Para usuários na Europa, isso estará disponível a partir de 25 de agosto. Para usuários na Ásia, isso estará disponível a partir de 8 de setembro.

O Capacity fornece uma visão abrangente das [medidas de proteção](../../rtcdp/guardrails/overview.md) da sua organização e fornece recomendações sobre como resolver possíveis violações de capacidade alocando suas capacidades em um nível de sandbox. Com esta versão, você pode visualizar sua capacidade de assimilação de streaming e segmentação de streaming.

Para obter mais informações, leia a [Visão geral da capacidade](../../landing/license-usage-and-guardrails/capacity.md).

## Destinos {#destinations}

[!DNL Destinations] são integrações pré-construídas com plataformas de destino que permitem a ativação perfeita de dados da Adobe Experience Platform. É possível usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas de email, publicidade direcionada e muitos outros casos de uso.

**Destinos atualizados**

| Destino | Descrição |
| --- | --- |
| Disponibilidade limitada da [Correspondência de cliente do Google + Exibição e vídeo da conexão 360](/help/destinations/catalog/advertising/google-customer-match-dv360.md) | Depois de estar disponível brevemente para todos os clientes em junho, a Adobe retornou essa integração para disponibilidade limitada. Atualmente, o acesso a esse destino está restrito aos clientes que já estão ativados, enquanto a Adobe e a Google trabalham para resolver problemas de implementação. Se você estiver interessado em usar essa integração depois que a implantação mais ampla for retomada, entre em contato com o representante da Adobe para expressar sua intenção. |
| Atualização interna de [[!DNL The Trade Desk]](../../destinations/catalog/advertising/tradedesk.md) | A partir de 31 de julho de 2025, você poderá ver dois cartões [!DNL The Trade Desk] lado a lado no catálogo de destinos. Isso se deve a uma atualização interna do serviço de destinos. <br><br>O conector de destino [!DNL The Trade Desk] existente foi renomeado para **[!UICONTROL (obsoleto) Trade Desk]** e um novo cartão com o nome **[!UICONTROL The Trade Desk]** está disponível. Use a nova conexão **[!UICONTROL Trade Desk]** no catálogo para novos fluxos de dados de ativação. <br><br>Se você tiver fluxos de dados ativos para o destino **[!UICONTROL (Obsoleto) da Trade Desk]**, eles serão atualizados automaticamente; portanto, nenhuma ação será necessária. <br><br>Se você estiver criando fluxos de dados por meio da [API de Serviço de Fluxo](https://developer.adobe.com/experience-platform-apis/references/destinations/), atualize o [!DNL flow spec ID] e o [!DNL connection spec ID] para os seguintes valores:<ul><li>ID da especificação de fluxo: `86134ea1-b014-49e8-8bd3-689f4ce70578`</li><li>ID de especificação da conexão: `1029798b-a97f-4c21-81b2-e0301471166e`</li></ul> |

**Funcionalidade nova ou atualizada**

| Recurso | Descrição |
| --- | --- |
| Nomes e descrições de conta para conexões de destino | Agora você pode [adicionar nomes e descrições de conta](/help/destinations/ui/connect-destination.md) ao se conectar aos destinos, permitindo um melhor gerenciamento dos destinos com várias contas. |
| Informações de sequência de dados aprimoradas para destinos de borda | As informações do painel direito dos destinos do [Adobe Target](/help/destinations/catalog/personalization/adobe-target-v2.md) e do [Personalization personalizado](/help/destinations/catalog/personalization/custom-personalization.md) foram aprimoradas para exibir o nome do fluxo de dados, oferecendo uma visibilidade mais clara das configurações do fluxo de dados associado e ajudando a reduzir a confusão na revisão dos fluxos de dados existentes. O seletor de **[!UICONTROL ID de Sequência de Dados]** na tela de configuração de destino foi atualizado para **[!UICONTROL Sequência de Dados]** para maior clareza na interface. |
| Visibilidade de ações de marketing na seleção de destino | As ações de marketing agora são exibidas no painel direito da guia **[[!UICONTROL Procurar]](/help/destinations/ui/destinations-workspace.md#browse)** no espaço de trabalho Destinos e na página **[[!UICONTROL Execuções de fluxo de dados]](/help/dataflows/ui/monitor-destinations.md)**, fornecendo visibilidade imediata das alterações das ações de marketing sem precisar navegar para a página de exibição. Esse aprimoramento melhora a experiência do usuário, facilitando a verificação das configurações de ação de marketing durante a configuração do destino. |
| [!BADGE Beta limitado]{type=Informative} Editar ações de marketing para destinos | Agora você pode [editar ações de marketing](/help/destinations/ui/edit-activation.md#edit-marketing-actions) para destinos existentes. No momento, esse recurso está na versão beta limitada. Para solicitar acesso, entre em contato com o representante da Adobe. |
| [!BADGE Beta limitado]{type=Informative} Editar destinos | Agora você pode [editar a configuração de destino](/help/destinations/ui/edit-destination.md) após sua criação. No momento, esse recurso está na versão beta limitada. Para solicitar acesso, entre em contato com o representante da Adobe. |

**Correções**

| Problema | Descrição |
| --- | --- |
| Funcionalidade de rolagem de categorias | Correção de um problema em que o menu lateral de categorias no catálogo de destinos e origens não rolava corretamente sobre o mouse, melhorando a usabilidade da navegação para usuários que navegavam em categorias de destino. |

Para obter mais informações, leia a [Visão geral dos Destinos](../../destinations/home.md).

## Ingestão de dados {#ingestion}

O Experience Platform fornece uma estrutura abrangente de assimilação de dados que oferece suporte à assimilação de dados em lote e por transmissão de várias fontes.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Suporte para monitorar a assimilação de perfil de transmissão | O monitoramento em tempo real para assimilação de perfil por transmissão agora está disponível, fornecendo transparência às métricas de taxa de transferência, latência e qualidade de dados. Isso oferece suporte a alertas proativos e insights acionáveis para ajudar os engenheiros de dados a identificar violações de capacidade e problemas de assimilação. Leia o guia em [assimilação do perfil de streaming de monitoramento](../../dataflows/ui/monitor-streaming-profile.md) para obter mais informações. |

Para obter mais informações, leia a [visão geral da assimilação de dados](../../ingestion/home.md).

## Real-Time CDP B2B Edition {#b2b}

O Real-Time CDP B2B edition fornece recursos abrangentes de gerenciamento de dados de clientes B2B, permitindo que as organizações criem perfis unificados de clientes, criem públicos B2B sofisticados e ativem dados em vários canais de marketing.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| ------- | ----------- |
| Atualização da arquitetura B2B | A Experience Platform está atualizando para uma nova arquitetura B2B que introduz melhorias significativas em públicos-alvo de várias entidades com atributos B2B. Essa atualização consolida o suporte à política de mesclagem, melhora a precisão das contagens de público e melhora os recursos de resolução da entidade. Leia a [visão geral da atualização da arquitetura do Real-Time CDP B2B edition](../../rtcdp/b2b-architecture-upgrade.md) para obter um detalhamento abrangente das alterações. |
| Consolidação de política de mesclagem para públicos-alvo de várias entidades | Públicos-alvo de várias entidades com atributos B2B agora oferecem suporte a apenas uma única política de mesclagem — a política de mesclagem padrão — em vez de oferecer suporte a várias políticas de mesclagem. Essa alteração garante uma composição consistente do público-alvo e simplifica o gerenciamento da lógica de mesclagem. Para obter mais informações, leia a [visão geral das políticas de mesclagem](../../profile/merge-policies/overview.md). |
| Contagens de público aprimoradas para entidades B2B | As estimativas de tamanho para públicos-alvo com entidades B2B, como Contas e Oportunidades, agora são exatas, com base nos resultados da segmentação em tempo real. Essa melhoria fornece estimativas mais precisas e confiáveis para públicos-alvo que envolvem relacionamentos complexos B2B. |
| Instantâneos de conta para associação de público-alvo | Os detalhes de associação ao público-alvo agora são incluídos para entidades Account em exportações de instantâneo, permitindo acesso ao status do público-alvo no nível da conta, carimbos de data e hora e indicadores de associação. Isso traz paridade de recursos entre os modelos de segmentação de Perfil (Pessoa) e Conta. |
| Alterações nas ferramentas de sandbox para públicos de várias entidades | Não há mais suporte para a importação de públicos-alvo de várias entidades com entidades B2B e eventos de experiência exportados antes da migração. Esses públicos-alvo falharão na validação da importação e não poderão ser convertidos automaticamente para a nova arquitetura. Os públicos devem ser reexportados após a migração antes da importação para sandboxes de destino. Para obter mais informações, leia o [guia sobre objetos com suporte para ferramentas de sandbox](../../sandboxes/ui/sandbox-tooling.md#objects-supported-for-sandbox-tooling). |
| Descontinuações da API de entidade B2B | As operações de pesquisa de API [!DNL Profile Access] para entidades B2B (Relação conta-pessoa, Relação de pessoa de oportunidade, Campanha, Membro da campanha, Lista de marketing e Membros da Lista de marketing) agora estão obsoletas. Além disso, as operações de exclusão da API [!DNL Profile Access] para entidades B2B (Conta, Relação Conta-Pessoa, Oportunidade, Relação de Pessoa da Oportunidade, Campanha, Membro da Campanha, Lista de Marketing e Membros da Lista de Marketing) também estão obsoletas. Para obter mais informações, leia o [manual de API de ponto de extremidade de entidades](../../profile/api/entities.md). |
| Atualizações no namespace de identidade para resolução de entidade | As entidades de Conta e Oportunidade agora usam mesclagem baseada em precedência de tempo com namespaces de identidade específicos (`b2b_account` para Conta, `b2b_opportunity` para Oportunidade). Todas as outras entidades são unificadas com sobreposições de identidade primárias mescladas usando a mesclagem baseada em precedência de tempo. Para obter mais informações sobre resolução de entidades, leia o [manual de API de ponto de extremidade de entidades](../../profile/api/entities.md). |

Para obter mais informações, leia a [visão geral do Real-Time CDP B2B edition](../../rtcdp/b2b-overview.md).

## Sandboxes {#sandboxes}

O Experience Platform foi criado para enriquecer aplicativos de experiência digital em escala global. As empresas geralmente executam vários aplicativos de experiência digital em paralelo e precisam atender ao desenvolvimento, ao teste e à implantação desses aplicativos enquanto garantem a conformidade operacional.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Alterações nas importações de público-alvo de várias entidades | As ferramentas de sandbox foram atualizadas para oferecer suporte à nova atualização da arquitetura B2B. Públicos-alvo de várias entidades contendo entidades B2B e Eventos de experiência devem ser reexportados após a atualização da arquitetura antes de serem importados para sandboxes de destino por meio de ferramentas de sandbox. A validação será falha ao importar versões pré-atualização. Para obter mais informações, leia o [guia sobre objetos com suporte para ferramentas de sandbox](../../sandboxes/ui/sandbox-tooling.md#objects-supported-for-sandbox-tooling). |

Para obter mais informações sobre sandboxes, leia a [visão geral das sandboxes](../../sandboxes/home.md).

## Serviço de segmentação {#segmentation-service}

O [!DNL Segmentation Service] define um subconjunto específico de perfis descrevendo os critérios que distinguem um grupo de pessoas na sua base de clientes que pode ser direcionado por campanhas de marketing. Os públicos podem ser baseados em dados de registro (como informações demográficas) ou eventos de séries temporais que representam interações do cliente com sua marca.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| ------- | ----------- |
| API de público-alvo externo | Você pode usar a API de públicos externos para importar programaticamente públicos gerados externamente para o Adobe Experience Platform. Para obter mais informações, leia o [manual de ponto de extremidade de públicos externos](../../segmentation/api/external-audiences.md). |

Para obter mais informações sobre segmentação, leia a [Visão geral do Serviço de segmentação](../../segmentation/home.md)

## Origens {#sources}

A Experience Platform fornece uma API RESTful e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar a sistemas de armazenamento externos e serviços de CRM, definir períodos para execuções de ingestão e gerenciar a taxa de transferência de ingestão de dados.

**Novas fontes**

| Fonte | Descrição |
| --- | --- |
| Suporte do [!BADGE Beta]{type=Informative} para [!DNL Didomi] (SDK de Streaming) | Use a fonte [!DNL Didomi] para assimilar dados de gerenciamento de consentimento e preferências de [!DNL Didomi], oferecendo suporte à conformidade com as regulamentações de privacidade e estratégias de marketing baseadas em consentimento. Leia a [[!DNL Didomi] visão geral da origem](../../sources/connectors/consent-and-preferences/didomi.md) para obter informações sobre como obter a instalação. Para obter etapas sobre como criar uma conexão de origem, leia o [[!DNL Didomi] guia de conexão de origem](../../sources/tutorials/ui/create/consent-and-preferences/didomi.md). |

**Funcionalidade nova ou atualizada**

| Recurso | Descrição |
| --- | --- |
| Suporte para captura de dados de alteração em fontes selecionadas usando a API [!DNL Flow Service] | Agora é possível criar fluxos de dados que permitem a captura de dados de alteração para assimilação incremental usando conectores de origem. Esse recurso permite que os clientes tragam tipos de dados de alteração para assimilação incremental, melhorando a atualização de dados e reduzindo a sobrecarga de processamento. Para obter mais informações, leia a documentação sobre [usando a captura de dados de alteração para fontes](../../sources/tutorials/api/change-data-capture.md) |
| Suporte para exclusão reversível de registros em [!DNL Salesforce] | A origem [!DNL Salesforce] agora dá suporte à inclusão de registros excluídos por meio de um parâmetro `includeDeletedObjects` opcional. Quando definido como verdadeiro, os clientes podem incluir registros excluídos por software em suas consultas [!DNL Salesforce] e trazer esses registros para a Experience Platform. Leia a documentação da origem[&#128279;](../../sources/connectors/crm/salesforce.md) do [!DNL Salesforce]  para obter mais informações. |

Para obter mais informações, leia a [visão geral de fontes](../../sources/home.md).
