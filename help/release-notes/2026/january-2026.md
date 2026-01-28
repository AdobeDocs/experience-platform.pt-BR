---
title: Notas da versão de janeiro de 2026 da Adobe Experience Platform
description: As notas da versão de janeiro de 2026 da Adobe Experience Platform.
source-git-commit: 9a3fbe281195041cf7444c5b6ec185395ff5ad23
workflow-type: tm+mt
source-wordcount: '1118'
ht-degree: 16%

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

**Data de lançamento: quarta-feira, 27 de janeiro de 2026**

Novos recursos e atualizações dos recursos existentes no Adobe Experience Platform:

<!-- - [Agent Orchestrator](#agent-orchestrator) -->

- [Destinos](#destinations)
- [Perfil do cliente em tempo real](#real-time-customer-profile)
- [Esquemas](#schemas)
- [Serviço de segmentação](#segmentation-service)
- [Fontes](#sources)

<!-- ## Agent Orchestrator {#agent-orchestrator}

Agent Orchestrator enables you to build and deploy AI-powered agents that can automate workflows and interact with customers across multiple channels.

**New or updated features**

| Feature | Description |
| --- | --- |
| Trial motion for Adobe Experience Platform Agents | **Select customers now have access to Adobe Experience Platform Agents for a complimentary trial**, enabling them to explore and interact with these Agents through the AI Assistant interface powered by Adobe Experience Platform Agent Orchestrator. The trial offers hands-on experience with AI Agents that operate within the context of customers' existing Experience Cloud products and environments, allowing teams to evaluate value before committing to a full purchase. Adobe Experience Platform Agents are guided by user input and oversight and respect existing product-level access controls, ensuring users can only perform actions or view data for which they are authorized within the underlying Experience Cloud applications.|

{style="table-layout:auto"}

For more information, see the [Agent Orchestrator documentation](https://experienceleague.adobe.com/en/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator). -->

## Destinos {#destinations}

[!DNL Destinations] são integrações pré-criadas com plataformas de destino que permitem a ativação contínua de dados do Experience Platform. É possível usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas de email, publicidade direcionada e muitos outros casos de uso.

**Destinos novos ou atualizados**

| Destino | Descrição |
| --- | --- |
| Conector de destino de Kevel agora disponível | O destino de streaming [!DNL Kevel] para o Adobe Experience Platform permite que os clientes ativem os públicos do Adobe diretamente no UserDB e nas APIs de gerenciamento de segmento do [!DNL Kevel], para oferecer suporte ao direcionamento em tempo real no momento da decisão do anúncio. [[!DNL Kevel]](https://www.kevel.com/) fornece a tecnologia habilitada para IA e orientação de especialistas que ajudam líderes comerciais inovadores a lançar, escalar e ter sucesso na mídia de varejo. A Retail Media Cloud do [!DNL Kevel] possibilita formatos de anúncios direcionados, atribuíveis e personalizáveis para publicidade no local e fora do local. |
| Conector de destino do Index Exchange agora disponível | Use este conector de destino para exportar segmentos de público do Adobe Experience Platform diretamente para a plataforma de publicidade programática do [!DNL Index Exchange]. [!DNL Index] é uma plataforma global de fornecimento de publicidade que ajuda os proprietários de mídia a maximizar o valor de seu conteúdo em todas as telas. Com mais de 20 anos de liderança no setor, o [!DNL Index] conecta as maiores marcas do mundo com criadores de experiências premium para fornecer experiências de alta qualidade ao consumidor. |
| Suporte a endpoints regionais para conexões de Brasil | Todos os [pontos de extremidade específicos da região](https://www.braze.com/docs/user_guide/administrative/access_braze/sdk_endpoints) com suporte de [!DNL Braze] agora estão disponíveis para seleção durante o fluxo de configuração de destino. Pergunte ao representante do [!DNL Braze] qual instância de ponto de extremidade você deve usar. |
| Suporte de agendamento semanal e mensal para o [Liveramp Onboarding](../../destinations/catalog/advertising/liveramp-onboarding.md#scheduling) | Agora você pode configurar programações de exportação semanais e mensais para o destino de integração do Liveramp. <br> Esta versão está sendo lançada gradualmente e será concluída em 30 de janeiro. |
| Experiência de ativação aprimorada para [Destinos da Trade Desk](../../destinations/catalog/advertising/tradedesk.md) e [Microsoft Bing](../../destinations/catalog/advertising/bing.md) | Os destinos Trade Desk e Microsoft Bing agora incluem mapeamentos obrigatórios predefinidos para uma experiência de ativação otimizada.  <br> Esta versão está sendo lançada gradualmente e será concluída em 30 de janeiro. |

<!-- |AES256 encryption support for [Amazon S3](../../destinations/catalog/cloud-storage/amazon-s3.md#destination-details) destinations | You can now configure AES256 encryption for your Amazon S3 exports. Two options are available: <br><br>**[!UICONTROL Default]**: If you don't have any custom policies applied on your buckets, data will be encrypted at rest when it lands in S3 with the AES256 algorithm. However, if you have custom policies applied, Experience Platform will respect those policies and Amazon S3 will continue to apply whichever custom encryption policies you have configured.<br><br>**[!UICONTROL SSE-S3/AES256]**: Experience Platform adds the `s3:x-amz-server-side-encryption": "AES256` header in the export and data will be encrypted at rest when it lands in S3 with the AES256 algorithm. | -->


**Funcionalidade nova ou atualizada**

| Recurso | Descrição |
| --- | --- |
| Limites de proteção atualizados para destinos do [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) | O número máximo de públicos que podem ser mapeados para um único destino do Adobe Target aumentou de 50 para 250. Isso alinha o Adobe Target ao limite de público-alvo padrão para outros destinos, fornecendo maior flexibilidade para os fluxos de trabalho de ativação de público-alvo. Agora você pode ativar mais públicos para destinos do Adobe Target sem precisar criar vários fluxos de dados. |
| [Editar destinos](/help/destinations/ui/edit-destination.md) e [editar ações de marketing](/help/destinations/ui/edit-activation.md#edit-marketing-actions) disponibilidade geral | A opção para editar destinos e ações de marketing agora está disponível para todos os usuários. |
| Alternar nomes para exibição de campo no Mapeamento [etapa](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) | Ao mapear campos de esquema para um destino, agora é possível alternar entre exibir o nome completo do campo XDM e mostrar apenas o nome de exibição. <br> ![Gravação de tela mostrando a alternância do nome para exibição.](/help/release-notes/2026/assets/january/show-display-names.gif) |

{style="table-layout:auto"}

Para obter mais informações, leia a [Visão geral dos Destinos](../../destinations/home.md).

## Perfil do cliente em tempo real {#real-time-customer-profile}

O Perfil do cliente em tempo real permite ter uma visão holística de cada cliente individual ao combinar dados de vários canais, incluindo dados online, offline, de CRM e de terceiros. O Perfil permite consolidar os dados do cliente em uma visualização unificada, oferecendo uma conta acionável com carimbo de data e hora de cada interação com o cliente.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Imposição de [capacidade de streaming](/help/landing/license-usage-and-guardrails/capacity.md) | A Experience Platform agora reforça as capacidades de taxa de transferência de transmissão para o Perfil do cliente em tempo real e o Serviço de identidade. Quando os clientes excedem sua capacidade de transmissão contratada, os dados são enfileirados e processados da maneira primeiro a entrar, primeiro a sair. Isso garante um desempenho previsível do sistema e impede que violações de capacidade afetem a qualidade da assimilação de dados. Observações importantes: <ul><li>Upserts de transmissão não estarão disponíveis no data lake quando a capacidade for excedida</li><li>Essa imposição não se aplica a clientes com licenças do Adobe Journey Optimizer</li><li>Os dados em fila serão processados sequencialmente assim que a capacidade estiver disponível.</li></ul> Para obter mais informações, leia a [visão geral da capacidade](/help/landing/license-usage-and-guardrails/capacity.md). |
| Descontinuação da pesquisa de entidade | O uso da API de pesquisa de entidade para eventos de experiência agora está obsoleto para todos os clientes do Real-Time CDP Prime. Essa descontinuação ajuda a alinhar o Real-Time CDP com a funcionalidade de licenciamento. Os clientes do Real-Time CDP Ultimate que pretendem usar essa funcionalidade podem entrar em contato com o Atendimento ao cliente da Adobe para reativar esse recurso.  Para obter mais informações, leia o [guia de API de entidades](/help/profile/api/entities.md). |
| Monitorar status do trabalho de assimilação de perfil | Agora é possível monitorar a porcentagem de progresso no nível da tarefa para execuções de fluxo de dados de assimilação de perfil em lote. Esse recurso oferece visibilidade em tempo real do progresso atual dos trabalhos de assimilação em lote, incluindo pontos de verificação críticos que indicam se a assimilação está pronta para a segmentação do cliente e pesquisas do Adobe Journey Optimizer. Para assimilações grandes que podem levar várias horas para serem processadas, essa transparência de progresso ajuda você a entender se o trabalho está progredindo normalmente ou se está encontrando problemas, reduzindo as incertezas durante o processamento de dados.Para obter mais informações, leia o [guia para monitorar perfis](/help/dataflows/ui/monitor-profiles.md). |

{style="table-layout:auto"}

Para obter mais informações, leia a visão geral](../../profile/home.md) do [[!DNL Real-Time Customer Profile] .

## Serviço de segmentação {#segmentation-service}

O [!DNL Segmentation Service] define um subconjunto específico de perfis descrevendo os critérios que distinguem um grupo de pessoas na sua base de clientes que pode ser direcionado por campanhas de marketing. Os públicos podem ser baseados em dados de registro (como informações demográficas) ou eventos de séries temporais que representam interações do cliente com sua marca.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| ------- | ----------- |
| Atualização da expiração dos dados do público-alvo externo | Públicos externos (como uploads de CSV) agora oferecem suporte a um recurso de atualização forçada para configurações de expiração de dados. Esse recurso permite que os usuários atualizem manualmente a expiração dos dados para públicos-alvo externos, fornecendo maior controle sobre o gerenciamento do ciclo de vida do público-alvo. Isso é particularmente útil para públicos-alvo que precisam persistir além do período de expiração inicial dos dados ou exigir reativação sem recarregar os dados. Para obter mais informações sobre este recurso, leia a [Visão geral do Portal de público-alvo](../../segmentation/ui/audience-portal.md#audience-summary). |

Para obter mais informações, leia a visão geral](../../segmentation/home.md) do [[!DNL Segmentation Service] .

## Fontes {#sources}

A Experience Platform fornece uma API RESTful e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar a sistemas de armazenamento externos e serviços de CRM, definir períodos para execuções de ingestão e gerenciar a taxa de transferência de ingestão de dados.

**Fontes novas ou atualizadas**

| Fonte | Descrição |
| --- | --- |
| [[!DNL Oracle Eloqua]](/help/sources/connectors/marketing-automation/eloqua.md) origem V2 | Um novo conector de origem [!DNL Oracle Eloqua] está disponível, substituindo o [conector obsoleto](/help/sources/connectors/marketing-automation/oracle-eloqua.md). Este conector atualizado fornece funcionalidade aprimorada e maior confiabilidade para assimilar dados do [!DNL Oracle Eloqua] na Experience Platform. Os clientes que usam o conector existente devem migrar para a nova implementação, pois as conexões existentes não funcionarão mais. O novo conector dá suporte a todas as etapas de instalação e configuração necessárias para se conectar ao [!DNL Oracle Eloqua] e assimilar dados de automação de marketing. |
| [[!DNL Salesforce Marketing Cloud]](/help/sources/connectors/marketing-automation/sfmc.md) origem V2 | Um novo conector de origem [!DNL Salesforce Marketing Cloud] está disponível, substituindo o [conector obsoleto](/help/sources/connectors/marketing-automation/salesforce-marketing-cloud.md). Este conector atualizado fornece desempenho aprimorado e recursos adicionais para assimilação de dados do [!DNL Salesforce Marketing Cloud] na Experience Platform. Os clientes que usam o conector existente devem fazer a transição para a nova implementação. O novo conector inclui instruções de configuração abrangentes para conexão com o [!DNL Salesforce Marketing Cloud] e assimilação de dados de automação de marketing. |

Para obter mais informações, leia a [visão geral de fontes](../../sources/home.md).

