---
title: Notas de pré-lançamento do Experience Platform
description: Uma visualização das notas de versão mais recentes do Adobe Experience Platform.
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: acb8303673c3271794dcda87b149b473328a7a21
workflow-type: tm+mt
source-wordcount: '1150'
ht-degree: 15%

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

**Data de lançamento: janeiro de 2026**

Novos recursos e atualizações dos recursos existentes no Adobe Experience Platform:

- [Agent Orchestrator](#agent-orchestrator)
- [Destinos](#destinations)
- [Perfil do cliente em tempo real](#real-time-customer-profile)
- [Esquemas](#schemas)
- [Serviço de segmentação](#segmentation-service)
- [Fontes](#sources)

## Agent Orchestrator {#agent-orchestrator}

O Agent Orchestrator permite criar e implantar agentes alimentados por IA que podem automatizar fluxos de trabalho e interagir com clientes em vários canais.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Movimento de avaliação do Agent Orchestrator | O Agent Orchestrator agora oferece uma versão de avaliação, permitindo que os clientes explorem e testem o serviço antes de se comprometerem com uma compra completa. Essa opção de experimentar antes de comprar permite que as organizações avaliem os recursos da Agent Orchestrator, incluindo habilidades e recursos de orquestração, em seu próprio ambiente. A avaliação fornece experiência prática com a criação de agentes alimentados por IA e entender como eles podem ser integrados aos fluxos de trabalho existentes. |

{style="table-layout:auto"}

Para obter mais informações, consulte a [documentação do Agent Orchestrator](https://experienceleague.adobe.com/pt-br/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator).

## Destinos {#destinations}

[!DNL Destinations] são integrações pré-criadas com plataformas de destino que permitem a ativação contínua de dados do Experience Platform. É possível usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas de email, publicidade direcionada e muitos outros casos de uso.

**Funcionalidade nova ou atualizada**

| Recurso | Descrição |
| --- | --- |
| Limites de proteção atualizados para o destino do Adobe Target | O número máximo de públicos que podem ser mapeados para um único destino do Adobe Target aumentou de 50 para 250. Isso alinha o Adobe Target ao limite de público-alvo padrão para outros destinos, fornecendo maior flexibilidade para os fluxos de trabalho de ativação de público-alvo. Agora, os clientes podem ativar mais públicos para destinos do Adobe Target sem precisar criar vários fluxos de dados. |

{style="table-layout:auto"}

Para obter mais informações, leia a [Visão geral dos Destinos](../destinations/home.md).

## Perfil do cliente em tempo real {#real-time-customer-profile}

O Perfil do cliente em tempo real permite ter uma visão holística de cada cliente individual ao combinar dados de vários canais, incluindo dados online, offline, de CRM e de terceiros. O Perfil permite consolidar os dados do cliente em uma visualização unificada, oferecendo uma conta acionável com carimbo de data e hora de cada interação com o cliente.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Aplicação da capacidade de transmissão | A Experience Platform agora reforça as capacidades de taxa de transferência de transmissão para o Perfil do cliente em tempo real e o Serviço de identidade. Quando os clientes excedem sua capacidade de transmissão contratada, os dados são enfileirados e processados da maneira primeiro a entrar, primeiro a sair. Isso garante um desempenho previsível do sistema e impede que violações de capacidade afetem a qualidade da assimilação de dados. Observações importantes: os upserts de transmissão não estarão disponíveis no data lake quando a capacidade for excedida, essa imposição não se aplica aos clientes com licenças do Adobe Journey Optimizer e os dados em fila serão processados sequencialmente quando a capacidade estiver disponível. |
| Descontinuação de acesso à API do Real-Time CDP Prime | O acesso à API para eventos de experiência agora está obsoleto para todos os clientes do Real-Time CDP Prime. Essa alteração afeta a capacidade de consultar eventos de experiência diretamente pela API. Os clientes do Real-Time CDP Ultimate podem solicitar uma exceção por meio de um processo formal de exceção para habilitar o acesso à API de eventos de experiência, se necessário, para seus casos de uso. Essa descontinuação ajuda a otimizar o desempenho do sistema e se alinha às práticas recomendadas para padrões de acesso a dados. |
| Monitorar execução de fluxo de dados | Agora você pode monitorar o progresso e a prontidão das execuções de fluxo de dados no Perfil. |

{style="table-layout:auto"}

Para obter mais informações, leia a visão geral[&#128279;](../profile/home.md) do [!DNL Real-Time Customer Profile] .

## Esquemas {#schemas}

A Experience Platform usa esquemas para descrever a estrutura dos dados de forma consistente e reutilizável. Ao definir os dados de forma consistente em todos os sistemas, fica mais fácil manter o significado e, portanto, obter valor dos dados. Os esquemas são compostos de uma classe base e zero ou mais grupos de campos de esquema.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| ------- | ----------- |
| Modernização do inventário de esquema com pesquisa, filtro, tags e pastas | A página de navegação do esquema foi modernizada para fornecer recursos organizacionais e de descoberta aprimorados. Os novos recursos incluem opções avançadas de pesquisa e filtragem, suporte para tags e pastas geradas pelo usuário para organizar esquemas e ações em linha para simplificar workflows. As principais melhorias incluem: colunas atualizadas (Nome, Classe, Conjuntos de dados, Identidades, Relacionamentos, Habilitar para Perfil, Comportamento, Tipo de esquema, Tags, Data de criação, Última modificação), filtros avançados (Mostrar perfis, Tipo de esquema, Classe, Tem qualquer tag, Criado por, Data de criação, Data de modificação, Tem identidade principal, Tem relacionamento, Namespace de identidade principal), ações em linha (Editar, Excluir, Aplicar rótulos, Criar conjunto de dados para esquemas não relacionais, Gerenciar tags, Mover para pasta, Adicionar ao pacote, Copiar estrutura JSON, Baixar arquivo de amostra) e a capacidade de organizar esquemas usando e pastas. Esses aprimoramentos fornecem visibilidade abrangente dos recursos do esquema e permitem um gerenciamento de esquema mais eficiente no nível da sandbox. |

Para obter mais informações, leia a visão geral[&#128279;](../xdm/home.md) do [!DNL Schemas] .

## Serviço de segmentação {#segmentation-service}

O [!DNL Segmentation Service] define um subconjunto específico de perfis descrevendo os critérios que distinguem um grupo de pessoas na sua base de clientes que pode ser direcionado por campanhas de marketing. Os públicos podem ser baseados em dados de registro (como informações demográficas) ou eventos de séries temporais que representam interações do cliente com sua marca.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| ------- | ----------- |
| Monitoramento da segmentação de transmissão | O monitoramento em tempo real da segmentação por transmissão oferece transparência às métricas de taxa de avaliação, latência e qualidade de dados nos níveis de sandbox, conjunto de dados e público-alvo. Isso oferece suporte a alertas proativos e insights acionáveis para ajudar os engenheiros de dados a identificar violações de capacidade e problemas de assimilação. As métricas de monitoramento incluem taxa de avaliação, latência de assimilação P95, bem como registros recebidos, avaliados, com falha e ignorados. Os recursos visualizar por conjunto de dados e visualizar por público-alvo fornecem visibilidade abrangente sobre novos perfis qualificados e desqualificados. |
| Atualização do TTL do público externo | Públicos externos (como uploads de CSV) agora oferecem suporte a um recurso de atualização forçada para configurações de Tempo de vida (TTL). Esse recurso permite que os usuários atualizem manualmente a expiração do TTL para públicos-alvo externos, fornecendo maior controle sobre o gerenciamento do ciclo de vida do público-alvo. Isso é particularmente útil para públicos que precisam persistir além do período TTL inicial ou exigir reativação sem recarregar os dados. |

Para obter mais informações, leia a visão geral[&#128279;](../segmentation/home.md) do [!DNL Segmentation Service] .

## Fontes {#sources}

A Experience Platform fornece uma API RESTful e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar a sistemas de armazenamento externos e serviços de CRM, definir períodos para execuções de ingestão e gerenciar a taxa de transferência de ingestão de dados.

**Fontes novas ou atualizadas**

| Fonte | Descrição |
| --- | --- |
| [!DNL Oracle Eloqua] origem V2 | Um novo conector de origem [!DNL Oracle Eloqua] está disponível, substituindo o conector obsoleto. Este conector atualizado fornece funcionalidade aprimorada e maior confiabilidade para assimilar dados do [!DNL Oracle Eloqua] na Experience Platform. Os clientes que usam o conector existente devem migrar para a nova implementação, pois as conexões existentes não funcionarão mais. O novo conector dá suporte a todas as etapas de instalação e configuração necessárias para se conectar ao [!DNL Oracle Eloqua] e assimilar dados de automação de marketing. |
| [!DNL Salesforce Marketing Cloud] origem V2 | Um novo conector de origem [!DNL Salesforce Marketing Cloud] está disponível, substituindo o conector obsoleto. Este conector atualizado fornece desempenho aprimorado e recursos adicionais para assimilação de dados do [!DNL Salesforce Marketing Cloud] na Experience Platform. Os clientes que usam o conector existente devem fazer a transição para a nova implementação. O novo conector inclui instruções de configuração abrangentes para conexão com o [!DNL Salesforce Marketing Cloud] e assimilação de dados de automação de marketing. |

Para obter mais informações, leia a [visão geral de fontes](../sources/home.md).

