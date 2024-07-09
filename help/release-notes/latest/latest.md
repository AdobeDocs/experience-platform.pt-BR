---
title: Notas de versão da Adobe Experience Platform de junho de 2024
description: As notas de versão de junho de 2024 da Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 01ce38d26cf61706de84ec143e3dd8af720d0591
workflow-type: tm+mt
source-wordcount: '1357'
ht-degree: 18%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: quarta-feira, 18 de junho de 2024**

>[!TIP]
>
>[Assistente de IA no Experience Platform](https://platform.adobe.com) O agora está disponível. Use o Assistente de IA para acelerar seus fluxos de trabalho em aplicativos Adobe. [Leia mais](#ai-assistant) sobre a nova funcionalidade.

Novos recursos na Adobe Experience Platform:

- [Assistente de IA](#ai-assistant)
- [Autenticação para APIs da Experience Platform](#authentication-platform-apis)
- [Preparação de dados](#data-prep)
- [Destinos](#destinations)
- [Serviço de identidade](#identity-service)
- [Privacy Service](#privacy)
- [Serviço de segmentação](#segmentation)
- [Manuais de casos de uso ](#use-case-playbooks)

## Assistente de IA {#ai-assistant}

O Assistente de IA no Adobe Experience Platform é uma experiência de conversação que você pode usar para acelerar seus fluxos de trabalho em aplicativos Adobe. Você pode usar o AI Assistant para entender melhor o conhecimento do produto, solucionar problemas ou pesquisar informações e encontrar insights operacionais. O Assistente de IA é compatível com Experience Platform, Real-time Customer Data Platform, Adobe Journey Optimizer e Customer Journey Analytics.

**Novo recurso**

| Recurso | Descrição |
| --- | --- |
| Assistente de IA no Experience Platform | Agora você pode usar o Assistente de IA no Experience Platform. O Assistente de IA é compatível com Experience Platform, Real-time Customer Data Platform, Adobe Journey Optimizer e Customer Journey Analytics. <br> ![Assistente de IA na Experience Platform.](../2024/assets/june/ai-assistant-full.png "Assistente de IA na Experience Platform."){width="100" zoomable="yes"} <br> Para obter mais informações sobre esse recurso, leia a [Guia da interface do assistente de IA](../../ai-assistant/ui-guide.md). |
| Suporte para perguntas de conhecimento sobre produtos | [Conhecimento do produto](../../ai-assistant/home.md#product-knowledge) são conceitos e tópicos baseados na documentação do Experience League e podem ser usados para aprendizagem pontual, descoberta aberta e solução de problemas. Você pode fazer perguntas sobre o conhecimento do produto do Assistente de IA, como: <ul><li>O que são públicos-alvo semelhantes?</li><li>Como a riqueza do perfil é calculada?</li><li> Posso excluir um esquema ativado por perfil depois que os dados forem assimilados?</li></ul> |
| [!BADGE Beta]{type=Informative} Suporte para perguntas de insights operacionais | [Insights operacionais](../../ai-assistant/home.md#operational-insights) As respostas que o Assistente de IA gera sobre seus objetos de metadados, incluindo contagens, pesquisas e impacto de linhagem. Os insights operacionais não analisam quaisquer dados na sandbox. Você pode fazer perguntas sobre insights operacionais do Assistente de IA, como: <ul><li>Quais destinos estão em um estado ativo?</li><li>Quantos conjuntos de dados eu tenho?</li><li>Liste os públicos-alvo que são usados em jornadas ativas.</li></ul> Os insights operacionais são suportados nos seguintes domínios: atributos, públicos, fluxos de dados, conjuntos de dados, destinos, jornadas, esquemas e fontes. |
| Acessar o assistente do AI | Para acessar o Assistente de IA para Experience Platform, Real-Time CDP e Journey Optimizer, você deve ser adicionado a uma função que inclua o **Habilitar o assistente de IA** e **Exibir Insights Operacionais** permissões. Para obter mais informações, leia a [guia de acesso a recursos](../../ai-assistant/access.md). Você deve usar o Admin Console para [acesso no Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/ai-assistant?lang=en#feature-access). |

Para obter mais informações sobre o Assistente de IA, leia a [Visão geral do Assistente de IA](../../ai-assistant/home.md).

## Autenticação para APIs da Experience Platform {#authentication-platform-apis}

O método JWT para obter tokens de acesso agora está obsoleto para novas integrações e foi substituído por um método de autenticação de servidor para servidor OAuth mais simples.<p>![Novo método de autenticação OAuth para realçar tokens de acesso.](/help/landing/images/api-authentication/oauth-authentication-method.png "Novo método de autenticação OAuth para realçar tokens de acesso."){width="100" zoomable="yes"}</p>

Embora as integrações de API já existentes que usam o método de autenticação JWT continuem funcionando até 1º de janeiro de 2025, a Adobe recomenda fortemente que você migre essas integrações para o novo método servidor para servidor OAuth antes dessa data. Leia o manual em [migração da credencial de conta de serviço (JWT) para a credencial de servidor para servidor do OAuth](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/).

## Preparação de dados {#data-prep}

Use o preparo de dados para mapear, transformar e validar dados de e para o Experience Data Model (XDM).

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Adições à lista de palavras-chave reservadas | As seguintes palavras foram adicionadas à lista de palavras-chave reservadas do preparo de dados:<ul><li>`do`</li><li>`empty`</li><li>`function`</li><li>`size`</li></ul> Para obter mais informações, leia as [guia de funções de preparação de dados](../../data-prep/functions.md). |

{style="table-layout:auto"}

Para obter mais informações sobre o Preparo de dados, leia a [Visão geral do Preparo de dados](../../data-prep/home.md).

## Destinos {#destinations}

[!DNL Destinations] são integrações pré-construídas com plataformas de destino que permitem a ativação perfeita de dados da Adobe Experience Platform. É possível usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas de email, publicidade direcionada e muitos outros casos de uso.

**Funcionalidades novas ou atualizadas** {#destinations-new-updated-functionality}

| Funcionalidade | Descrição |
| ----------- | ----------- |
| Aprimoramento da API de exportação ad hoc para exportar públicos externos | Agora você pode usar a API de exportação ad-hoc para exportar públicos externos (upload personalizado). [Leia mais](/help/destinations/api/ad-hoc-activation-api.md) . |
| (Beta) Outras funções compatíveis com a fase beta do suporte a matriz de exportação | Anteriormente, ao ativar públicos-alvo para destinos baseados em arquivo e selecionar Usar campo calculado, você estava limitado a usar um subconjunto dos públicos-alvo disponíveis por meio do preparo de dados. Essa limitação foi removida e os clientes têm acesso a todas as funções disponíveis por meio do preparo de dados ao exportar públicos-alvo para destinos baseados em arquivo. [Leia mais](/help/destinations/ui/export-arrays-calculated-fields.md#supported-functions). |
| Mostrar apenas campos com dados na etapa de mapeamento | Ao mapear atributos de perfil para seus destinos, agora é possível alternar entre todos os atributos de perfil ou apenas aqueles que contêm dados. Por padrão, somente os campos com dados são exibidos. Consulte os guias de ativação para [lote](../../destinations/ui/activate-batch-profile-destinations.md#mapping) e [transmissão](../../destinations/ui/activate-segment-streaming-destinations.md#mapping) destinos para obter mais detalhes. |

{style="table-layout:auto"}

Para obter informações mais gerais sobre destinos, consulte a [visão geral de destinos](../../destinations/home.md).

## Serviço de identidade {#identity-service}

Use o Serviço de identidade da Adobe Experience Platform para criar uma visualização abrangente dos clientes e seus comportamentos, unindo identidades em dispositivos e sistemas, permitindo que você forneça experiências digitais pessoais e de impacto em tempo real.

**Recursos futuros**

| Recurso | Descrição |
| --- | --- |
| [!BADGE Beta]{type=Informative} Regras de vinculação do gráfico de identidade | Os participantes do programa beta podem usar regras de vinculação de gráficos de identidade para garantir a representação da entidade da pessoa no sistema, evitando o &quot;dispositivo compartilhado&quot; e outros cenários de recolhimento de gráficos. Para atingir essa meta, os participantes durante o programa beta terão acesso a três recursos em um ambiente de sandbox de desenvolvimento: <ul><li>A ferramenta de simulação de gráficos para entender como o algoritmo de gráfico funciona.</li><li>A tela de configurações de identidade para configurar namespaces exclusivos e prioridades de namespace.</li><li>Um painel de identidade para obter insights sobre gráficos assimilados.</li></ul> Além disso, o programa beta incluirá melhorias na estabilidade do comportamento do perfil. Para obter mais informações, leia a [regras de vinculação do gráfico de identidade](../../identity-service/identity-graph-linking-rules/overview.md) documentação. |

{style="table-layout:auto"}

Para obter mais informações sobre o Serviço de identidade, leia a [Visão geral do serviço de identidade](../../identity-service/home.md).

## [!DNL Privacy Service] {#privacy}

Várias regulamentações legais e organizacionais dão aos usuários o direito de acessar ou excluir seus dados pessoais dos armazenamentos de dados, mediante solicitação. Adobe Experience Platform [!DNL Privacy Service] O fornece uma API RESTful e uma interface para ajudar você a gerenciar essas solicitações de dados de seus clientes. Com [!DNL Privacy Service], você pode enviar solicitações para acessar e excluir dados privados ou pessoais dos clientes por meio dos aplicativos da Adobe Experience Cloud, facilitando a conformidade automatizada com as regulamentações legais e organizacionais de privacidade.

**Novos recursos**

| Recurso | Descrição |
|--- | ---|
| Suporte para Privacy Service para Adobe Journey Optimizer | Os recursos de Privacy Service agora são compatíveis com os protocolos Adobe Journey Optimizer para processar solicitações de exclusão. Consulte a [Documentação de solicitações de privacidade do Adobe Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/requests) para obter mais informações, ou a documentação do Experience Platform para obter uma lista de [aplicativos de Experience Cloud que estão integrados com o Privacy Service](../../privacy-service/experience-cloud-apps.md). |

Consulte a [visão geral do Privacy Service](../../privacy-service/home.md) para obter mais informações sobre o serviço.

## Serviço de segmentação {#segmentation}

O [!DNL Segmentation Service] define um subconjunto específico de perfis descrevendo os critérios que distinguem um grupo de pessoas na sua base de clientes que pode ser direcionado por campanhas de marketing. Os segmentos podem ser baseados em dados de registro (como informações demográficas) ou em eventos de séries temporais que representam interações de clientes com sua marca.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| ------- | ----------- |
| Atualização de restrições de tempo | O comportamento para &quot;Este mês&quot; e &quot;Este ano&quot; foi atualizado e agora representam o &quot;acumulado no mês&quot; e o &quot;acumulado no ano&quot;, respectivamente. Para obter mais informações sobre essa alteração, leia a [Guia do Construtor de segmentos](../../segmentation/ui/segment-builder.md#rule-builder-canvas). |

{style="table-layout:auto"}

Para obter mais informações sobre o [!DNL Segmentation Service], consulte a [Visão geral de segmentação](../../segmentation/home.md).

## Manuais de casos de uso  {#use-case-playbooks}

[!DNL Use Case Playbooks] estão disponíveis sem custo extra para todos os clientes do Adobe Experience Platform. Para acessar uma galeria avançada de manuais de casos de uso na interface do Experience Platform, agora é possível selecionar **[!UICONTROL Playbooks]** no painel de navegação esquerdo.

[!DNL Use Case Playbooks] foram projetados para ajudar a superar os desafios ao começar a usar o Real-time Customer Data Platform ou o Adobe Journey Optimizer. Eles oferecem orientação e geram vários ativos que você pode testar e importar para ambientes de produção quando estiver pronto, mesmo se não tiver certeza de onde começar ou como produzir os ativos corretos para os casos de uso desejados.

Para começar, leia o [Visão geral dos manuais de caso de uso](/help/use-case-playbooks/playbooks/overview.md), que fornece uma visão geral da funcionalidade dos manuais, sua finalidade e uma demonstração completa, incluindo como criar instâncias e importar ativos gerados para outros ambientes de sandbox.

Para saber como acessar e configurar uma sandbox inspiradora para experimentar e explorar vários manuais de casos de uso, consulte a [Navegar até os manuais de casos de uso](/help/use-case-playbooks/playbooks/navigate.md) documento.

Para saber mais sobre [!DNL Use Case Playbooks], leia as seguintes páginas de documentação:

- Obter uma lista de todos os [manuais disponíveis](/help/use-case-playbooks/playbooks/playbooks-list.md), agrupados por produto (Real-Time CDP ou Journey Optimizer).
- Saiba mais sobre [permissões](/help/use-case-playbooks/playbooks/get-started.md#grant-your-team-the-required-access-permissions) são necessários para usar manuais e os ativos que eles criam.
- Compreender o [funcionalidade de reconhecimento de dados](/help/use-case-playbooks/playbooks/data-awareness.md) que permite duplicar ativos gerados para outros ambientes de sandbox.
