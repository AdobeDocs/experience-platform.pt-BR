---
title: Notas de pré-lançamento do Experience Platform
description: Uma visualização das notas de versão mais recentes do Adobe Experience Platform.
hide: true
hidefromtoc: true
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: 7e91181f71b84fdaf04a39e003cbbd415827e282
workflow-type: tm+mt
source-wordcount: '1387'
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

**Data de lançamento: quarta-feira, 29 de julho de 2025**

Novos recursos e atualizações dos recursos existentes no Adobe Experience Platform:

- [Destinos](#destinations)
- [Ingestão de dados](#ingestion)
- [Query Service](#query-service)
- [Real-Time CDP B2B Edition](#b2b)
- [Sandboxes](#sandboxes)
- [Serviço de segmentação](#segmentation)
- [Origens](#sources)

## Destinos {#destinations}

[!DNL Destinations] são integrações pré-construídas com plataformas de destino que permitem a ativação perfeita de dados da Adobe Experience Platform. É possível usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas de email, publicidade direcionada e muitos outros casos de uso.

**Destinos atualizados**

| Destino | Descrição |
| --- | --- |
| Consolidação de placas de destino Marketo | Os cartões de destino do Marketo V2 e do Marketo Engage Person Sync foram consolidados em um único cartão de destino unificado. Essa consolidação simplifica o processo de seleção de destino e fornece uma experiência mais simplificada para integrações do Marketo. |

**Funcionalidade nova ou atualizada**

| Recurso | Descrição |
| --- | --- |
| Informações de sequência de dados aprimoradas para destinos de borda | As informações aprimoradas do painel direito para destinos Adobe Target e Personalization personalizados agora exibem o nome do fluxo de dados, fornecendo visibilidade mais clara das configurações de fluxo de dados associadas e reduzindo a confusão ao revisar fluxos de dados existentes. O seletor de **[!UICONTROL ID de Sequência de Dados]** na tela de configuração de destino foi atualizado para **[!UICONTROL Sequência de Dados]** para maior clareza na interface. |
| Visibilidade de ações de marketing na seleção de destino | As ações de marketing agora são exibidas no painel direito da guia **[!UICONTROL Procurar]** de destino e na página **[!UICONTROL Execuções de fluxo de dados]**, fornecendo visibilidade imediata das alterações da ação de marketing sem exigir navegação para a página de exibição. Esse aprimoramento melhora a experiência do usuário, facilitando a verificação das configurações de ação de marketing durante a configuração do destino. |
| (Beta limitado) Editar ações de marketing para destinos | Agora é possível editar ações de marketing para destinos existentes. Essa funcionalidade está na versão beta limitada. Para solicitar acesso, entre em contato com o representante da Adobe. |
| (Beta limitado) Editar destinos | Agora você pode editar a configuração de destino depois de criá-la. Essa funcionalidade está na versão beta limitada. Para solicitar acesso, entre em contato com o representante da Adobe. |
| Nomes e descrições de conta para conexões de destino | Agora é possível adicionar nomes e descrições de conta ao se conectar a destinos, permitindo um melhor gerenciamento de destinos com várias contas. |

**Correções**

| Problema | Descrição |
| --- | --- |
| Funcionalidade de rolagem de categorias | Correção de um problema em que o menu lateral de categorias no catálogo de destinos e origens não rolava corretamente sobre o mouse, melhorando a usabilidade da navegação para usuários que navegavam em categorias de destino. |

Para obter mais informações, leia a [Visão geral dos Destinos](../destinations/home.md).

## Ingestão de dados {#ingestion}

O Experience Platform fornece uma estrutura abrangente de assimilação de dados que oferece suporte à assimilação de dados em lote e por transmissão de várias fontes.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Suporte para monitorar a assimilação de perfil de transmissão | O monitoramento em tempo real para assimilação de perfil por transmissão agora está disponível, fornecendo transparência às métricas de taxa de transferência, latência e qualidade de dados. Isso oferece suporte a alertas proativos e insights acionáveis para ajudar os engenheiros de dados a identificar violações de capacidade e problemas de assimilação. |

Para obter mais informações, leia a [visão geral da assimilação de dados](../ingestion/home.md).

## Query Service {#query-service}

O Adobe Experience Platform Query Service fornece uma interface SQL robusta para análise e exploração de dados em toda a plataforma.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| ------- | ----------- |
| Gerenciamento de sessão aprimorado | O Data Distiller agora inclui recursos aprimorados de gerenciamento de sessões, fornecendo melhor controle sobre as sessões do usuário e melhor monitoramento do desempenho em ambientes de desenvolvimento e produção. |
| Suporte para restrições de caracteres de senha de credenciais sem expiração | O Data Distiller agora oferece suporte a credenciais sem expiração com restrições de caracteres específicas. Embora as senhas exijam pelo menos um número, uma letra minúscula, uma maiúscula e um caractere especial, o cifrão ($) não é compatível. Os caracteres especiais recomendados incluem `!, @, #, ^, or &`. |
| Maior consistência de desempenho entre ambientes | O desempenho do Data Distiller agora é consistente entre sandboxes de desenvolvimento e produção, com recursos de back-end semelhantes disponíveis em ambos os ambientes. As horas de computação consumidas podem variar com base no volume de dados e nos recursos de computação de back-end disponíveis no momento do processamento. |

Para obter mais informações, leia a [Visão geral do Serviço de consulta](../query-service/home.md).

## Real-Time CDP B2B Edition {#b2b}

O Real-Time CDP B2B edition fornece recursos abrangentes de gerenciamento de dados de clientes B2B, permitindo que as organizações criem perfis unificados de clientes, criem públicos B2B sofisticados e ativem dados em vários canais de marketing.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| ------- | ----------- |
| Atualização da arquitetura B2B | A Experience Platform está atualizando para uma nova arquitetura B2B que introduz melhorias significativas em públicos-alvo de várias entidades com atributos B2B. Essa atualização consolida o suporte à política de mesclagem, melhora a precisão das contagens de público e melhora os recursos de resolução da entidade. |
| Consolidação de política de mesclagem para públicos-alvo de várias entidades | Públicos-alvo de várias entidades com atributos B2B agora oferecem suporte a apenas uma única política de mesclagem — a política de mesclagem padrão — em vez de oferecer suporte a várias políticas de mesclagem. Essa alteração garante uma composição consistente do público-alvo e simplifica o gerenciamento da lógica de mesclagem. |
| Atualizações das restrições de público-alvo da conta | Os públicos-alvo da conta não têm mais as restrições anteriores de uma janela de pesquisa de 30 dias para Eventos de experiência, restrições de entidade personalizadas ou limitações no uso de eventos `inSegment`. Essas atualizações fornecem maior flexibilidade ao criar definições complexas de público-alvo B2B. |
| Contagens de público aprimoradas para entidades B2B | As estimativas de tamanho para públicos-alvo com entidades B2B, como Contas e Oportunidades, agora são exatas, com base nos resultados da segmentação em tempo real. Essa melhoria fornece estimativas mais precisas e confiáveis para públicos-alvo que envolvem relacionamentos complexos B2B. |
| Instantâneos de conta para associação de público-alvo | Os detalhes de associação ao público-alvo agora são incluídos para entidades Account em exportações de instantâneo, permitindo acesso ao status do público-alvo no nível da conta, carimbos de data e hora e indicadores de associação. Isso traz paridade de recursos entre os modelos de segmentação de Perfil (Pessoa) e Conta. |
| Alterações nas ferramentas de sandbox para públicos de várias entidades | Não há mais suporte para a importação de públicos-alvo de várias entidades com entidades B2B e eventos de experiência exportados antes da migração. Esses públicos-alvo falharão na validação da importação e não poderão ser convertidos automaticamente para a nova arquitetura. Os públicos devem ser reexportados após a migração antes da importação para sandboxes de destino. |
| Desaprovações da API de entidade B2B | A criação de público-alvo por meio da API para entidades B2B (Conta, Oportunidade, Relação conta-pessoa, Relação oportunidade-pessoa, Campanha, Membro de campanha, Lista de marketing e Membro da Lista de marketing) agora está obsoleta. Além disso, as operações de pesquisa e exclusão da API de acesso ao perfil para essas entidades B2B também estão obsoletas. |
| Atualizações no namespace de identidade para Resolução de Entidade | As entidades de Conta e Oportunidade agora usam mesclagem baseada em precedência de tempo com namespaces de identidade específicos (`b2b_account` para Conta, `b2b_opportunity` para Oportunidade). Todas as outras entidades são unificadas com sobreposições de identidade primárias mescladas usando a mesclagem baseada em precedência de tempo. |

Para obter mais informações, leia a [visão geral do Real-Time CDP B2B edition](../rtcdp/b2b-overview.md).

## Sandboxes {#sandboxes}

O Experience Platform foi criado para enriquecer aplicativos de experiência digital em escala global. As empresas geralmente executam vários aplicativos de experiência digital em paralelo e precisam atender ao desenvolvimento, ao teste e à implantação desses aplicativos enquanto garantem a conformidade operacional.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Alterações nas importações de público-alvo de várias entidades | As ferramentas de sandbox foram atualizadas para oferecer suporte à nova atualização da arquitetura B2B. Públicos-alvo de várias entidades contendo entidades B2B e Eventos de experiência devem ser reexportados após a atualização da arquitetura antes de serem importados para sandboxes de destino por meio de ferramentas de sandbox. A validação será falha ao importar versões pré-atualização. |

Para obter mais informações sobre sandboxes, leia a [visão geral das sandboxes](../sandboxes/home.md).

## Serviço de segmentação {#segmentation-service}

O [!DNL Segmentation Service] define um subconjunto específico de perfis descrevendo os critérios que distinguem um grupo de pessoas na sua base de clientes que pode ser direcionado por campanhas de marketing. Os públicos podem ser baseados em dados de registro (como informações demográficas) ou eventos de séries temporais que representam interações do cliente com sua marca.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| ------- | ----------- |
| API de público-alvo externo | Você pode usar a API de públicos externos para importar programaticamente públicos gerados externamente para o Adobe Experience Platform. |

## Origens {#sources}

A Experience Platform fornece uma API RESTful e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar a sistemas de armazenamento externos e serviços de CRM, definir períodos para execuções de ingestão e gerenciar a taxa de transferência de ingestão de dados.

**Novas fontes**

| Fonte | Descrição |
| --- | --- |
| Suporte para [!DNL Didomi] (SDK de Streaming) | O conector de origem do [!DNL Didomi] permite assimilar dados de gerenciamento de consentimento da plataforma do [!DNL Didomi], oferecendo suporte à conformidade com as regulamentações de privacidade e estratégias de marketing baseadas em consentimento. |

**Funcionalidade nova ou atualizada**

| Recurso | Descrição |
| --- | --- |
| Suporte para captura de dados de alteração em origens selecionadas | Agora é possível criar fluxos de dados que permitem a captura de dados de alteração para assimilação incremental usando conectores de origem. Esse recurso permite que os clientes tragam tipos de dados de alteração para assimilação incremental, melhorando a atualização de dados e reduzindo a sobrecarga de processamento. |
| Suporte para exclusão reversível de registros em [!DNL Salesforce] | A origem [!DNL Salesforce] agora dá suporte à inclusão de registros excluídos por meio de um parâmetro `includeDeletedObjects` opcional. Quando definido como verdadeiro, os clientes podem incluir registros excluídos por software em suas consultas [!DNL Salesforce] e trazer esses registros para a Experience Platform. |

Para obter mais informações, leia a [visão geral de fontes](../sources/home.md).
