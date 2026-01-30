---
title: Notas da versão de janeiro de 2026 da Adobe Experience Platform
description: As notas da versão de janeiro de 2026 da Adobe Experience Platform.
source-git-commit: 76b2537b47c0f7bdf115afdec655a1de8460384c
workflow-type: tm+mt
source-wordcount: '1622'
ht-degree: 11%

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
| Avaliação vinculada ao uso dos Adobe Experience Platform Agents | **Os clientes selecionados agora têm acesso gratuito à avaliação dos Adobe Experience Platform Agents**. Você pode usar a versão de avaliação para explorar e interagir com agentes por meio da interface do Assistente de IA disponibilizada pelo Adobe Experience Platform Agent Orchestrator. A versão de avaliação oferece experiência prática com Agentes de IA que operam no contexto dos produtos e ambientes existentes do Experience Cloud dos clientes, permitindo que as equipes avaliem o valor antes de se comprometerem com uma compra completa. Os agentes da Adobe Experience Platform são orientados pela entrada e supervisão do usuário e respeitam os controles de acesso existentes no nível do produto, garantindo que os usuários só possam executar ações ou visualizar dados para os quais estejam autorizados nos aplicativos Experience Cloud subjacentes. Leia a [visão geral da avaliação associada ao uso dos Experience Platform Agents](https://experienceleague.adobe.com/en/docs/experience-cloud-ai/experience-cloud-ai/agents/trial) para obter informações sobre como começar. |

{style="table-layout:auto"}

Para obter mais informações, consulte a [documentação do Agent Orchestrator](https://experienceleague.adobe.com/pt-br/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator).

## Destinos {#destinations}

[!DNL Destinations] são integrações pré-criadas com plataformas de destino que permitem a ativação contínua de dados do Experience Platform. É possível usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas de email, publicidade direcionada e muitos outros casos de uso.

**Destinos novos ou atualizados**

| Destino | Descrição |
| --- | --- |
| O conector de [destino de nível de teclado](/help/destinations/catalog/advertising/kevel.md) está disponível | O destino de streaming [!DNL Kevel] para o Adobe Experience Platform permite que os clientes ativem os públicos do Adobe diretamente no UserDB e nas APIs de gerenciamento de segmento do [!DNL Kevel], para oferecer suporte ao direcionamento em tempo real no momento da decisão do anúncio. [[!DNL Kevel]](https://www.kevel.com/) fornece a tecnologia habilitada para IA e orientação de especialistas que ajudam líderes comerciais inovadores a lançar, escalar e ter sucesso na mídia de varejo. A Retail Media Cloud do [!DNL Kevel] possibilita formatos de anúncios direcionados, atribuíveis e personalizáveis para publicidade no local e fora do local. |
| O conector [Index Exchange destination](/help/destinations/catalog/advertising/index-exchange.md) agora está disponível | Use este conector de destino para exportar segmentos de público do Adobe Experience Platform diretamente para a plataforma de publicidade programática do [!DNL Index Exchange]. [!DNL Index] é uma plataforma global de fornecimento de publicidade que ajuda os proprietários de mídia a maximizar o valor de seu conteúdo em todas as telas. Com mais de 20 anos de liderança no setor, o [!DNL Index] conecta as maiores marcas do mundo com criadores de experiências premium para fornecer experiências de alta qualidade ao consumidor. |
| Suporte a endpoints regionais para conexões de Brasil | Todos os [pontos de extremidade específicos da região](https://www.braze.com/docs/user_guide/administrative/access_braze/sdk_endpoints) com suporte de [!DNL Braze] agora estão disponíveis para seleção durante o fluxo de configuração de destino. Pergunte ao representante do [!DNL Braze] qual instância de ponto de extremidade você deve usar. |
| Suporte de agendamento semanal e mensal para o [Liveramp Onboarding](../../destinations/catalog/advertising/liveramp-onboarding.md#scheduling) | Agora você pode configurar programações de exportação semanais e mensais para o destino de integração do Liveramp. <br> Esta versão está sendo lançada gradualmente e será concluída em 30 de janeiro. |
| Experiência de ativação aprimorada para [Destinos da Trade Desk](../../destinations/catalog/advertising/tradedesk.md) e [Microsoft Bing](../../destinations/catalog/advertising/bing.md) | Os destinos Trade Desk e Microsoft Bing agora incluem mapeamentos obrigatórios predefinidos para uma experiência de ativação otimizada.  <br> Esta versão está sendo lançada gradualmente e será concluída em 30 de janeiro. ![Imagem mostrando mapeamentos predefinidos para a Trade Desk](../2026/assets/january/mandatory-mappings-ttd.png) {width="150" align="center" zoomable="yes"} <br> ![Imagem mostrando mapeamentos predefinidos do Microsoft Bing](../2026/assets/january/mandatory-mappings-bing.png) {width="150" align="center" zoomable="yes"} |
| Suporte à criptografia AES256 para destinos do [Amazon S3](../../destinations/catalog/cloud-storage/amazon-s3.md#destination-details) | Agora você pode configurar a criptografia AES256 para suas exportações do Amazon S3. Estão disponíveis duas opções: <ul><li>**[!UICONTROL Default]**: Os dados serão criptografados em repouso com o algoritmo de criptografia padrão definido no seu bucket.</li><li>**[!UICONTROL SSE-S3/AES256]**: o Experience Platform adiciona o cabeçalho `s3:x-amz-server-side-encryption": "AES256` na exportação e os dados serão criptografados em repouso com o algoritmo AES256 quando ele chegar em S3. **Esta opção tem precedência sobre qualquer algoritmo de criptografia padrão configurado no seu bucket do S3**.</li></ul> Esta versão está sendo lançada gradualmente e será concluída em 30 de janeiro. |
| Suporte para ativação de número de telefone para a conexão [Trade Desk - CRM](../../destinations/catalog/advertising/tradedesk-emails.md#phone-hashing) | O destino Trade Desk - CRM agora oferece suporte à ativação de número de telefone, além de endereços de email. Você pode ativar números de telefone sem hash no formato E.164 e números de telefone com hash (formato SHA256_E.164) na sua conta da Trade Desk para direcionamento e supressão de público com base em dados de CRM. Os números de telefone devem ser normalizados para o formato E.164 antes da ativação. |
| [Snowflake Batch](../../destinations/catalog/warehouses/snowflake-batch.md) atualizações de destino | O destino em lote do Snowflake agora inclui o recurso de seleção de região durante a configuração do destino. Agora é possível selecionar a região específica do Snowflake onde sua instância é provisionada, garantindo a transferência de dados ideal e a conformidade com os requisitos regionais. Além disso, a restrição da política de mesclagem padrão foi removida, permitindo exportar públicos-alvo mapeados para qualquer política de mesclagem. <br> O [!DNL Snowflake] destino do lote está disponível no momento apenas para clientes do Real-Time CDP provisionados na região do Experience Platform VA7. |

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
| Monitorar status do trabalho de assimilação de perfil | Agora é possível monitorar a porcentagem de progresso no nível da tarefa para execuções de fluxo de dados de assimilação de perfil em lote. Esse recurso oferece visibilidade em tempo real do progresso atual dos trabalhos de assimilação em lote, incluindo pontos de verificação críticos que indicam se a assimilação está pronta para a segmentação do cliente e pesquisas do Adobe Journey Optimizer. Para assimilações grandes que podem levar várias horas para serem processadas, essa transparência de progresso ajuda você a entender se o trabalho está progredindo normalmente ou encontrando problemas, reduzindo a incerteza durante o processamento de dados. Para obter mais informações, leia o [guia de perfis de monitor](/help/dataflows/ui/monitor-profiles.md). |
| Melhorias do visualizador de perfil (GA) | As seguintes melhorias no visualizador de perfil estão disponíveis para o público geral. <ul><li>**Modo de exibição combinado**: atributo, eventos e insights foram combinados em um único modo de exibição.</li><li>**Insights gerados por IA**: a página de detalhes do perfil agora exibe insights gerados por IA, permitindo que você saiba detalhes gerados pelo seu perfil. Esses insights podem incluir informações como pontuações de propensão e análise de tendências.</li><li>**Atualização de estilo**: a página de detalhes do perfil foi atualizada visualmente.</li><li>**Navegar**: agora você pode explorar seus perfis em um carrossel interativo baseado em cartão com pesquisa e personalização.</li></ul> Para obter mais informações, leia o [guia do visualizador de perfis](/help/profile/ui/user-guide.md). |

{style="table-layout:auto"}

Para obter mais informações, leia a visão geral[&#128279;](../../profile/home.md) do [!DNL Real-Time Customer Profile] .

## Serviço de segmentação {#segmentation-service}

O [!DNL Segmentation Service] define um subconjunto específico de perfis descrevendo os critérios que distinguem um grupo de pessoas na sua base de clientes que pode ser direcionado por campanhas de marketing. Os públicos podem ser baseados em dados de registro (como informações demográficas) ou eventos de séries temporais que representam interações do cliente com sua marca.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| ------- | ----------- |
| Atualização da expiração dos dados do público-alvo externo | Públicos externos (como uploads de CSV) agora oferecem suporte a um recurso de atualização forçada para configurações de expiração de dados. Esse recurso permite que os usuários atualizem manualmente a expiração dos dados para públicos-alvo externos, fornecendo maior controle sobre o gerenciamento do ciclo de vida do público-alvo. Isso é particularmente útil para públicos-alvo que precisam persistir além do período de expiração inicial dos dados ou exigir reativação sem recarregar os dados. Para obter mais informações sobre este recurso, leia a [Visão geral do Portal de público-alvo](../../segmentation/ui/audience-portal.md#audience-summary). |

Para obter mais informações, leia a visão geral[&#128279;](../../segmentation/home.md) do [!DNL Segmentation Service] .

## Fontes {#sources}

A Experience Platform fornece uma API RESTful e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar a sistemas de armazenamento externos e serviços de CRM, definir períodos para execuções de ingestão e gerenciar a taxa de transferência de ingestão de dados.

**Fontes novas ou atualizadas**

| Fonte | Descrição |
| --- | --- |
| [[!DNL Oracle Eloqua]](/help/sources/connectors/marketing-automation/eloqua.md) origem V2 | Um novo conector de origem [!DNL Oracle Eloqua] está disponível, substituindo o [conector obsoleto](/help/sources/connectors/marketing-automation/oracle-eloqua.md). Este conector atualizado fornece funcionalidade aprimorada e maior confiabilidade para assimilar dados do [!DNL Oracle Eloqua] na Experience Platform. Os clientes que usam o conector existente devem migrar para a nova implementação, pois as conexões existentes não funcionarão mais. O novo conector dá suporte a todas as etapas de instalação e configuração necessárias para se conectar ao [!DNL Oracle Eloqua] e assimilar dados de automação de marketing. |
| [[!DNL Salesforce Marketing Cloud]](/help/sources/connectors/marketing-automation/sfmc.md) origem V2 | Um novo conector de origem [!DNL Salesforce Marketing Cloud] está disponível, substituindo o [conector obsoleto](/help/sources/connectors/marketing-automation/salesforce-marketing-cloud.md). Este conector atualizado fornece desempenho aprimorado e recursos adicionais para assimilação de dados do [!DNL Salesforce Marketing Cloud] na Experience Platform. Os clientes que usam o conector existente devem fazer a transição para a nova implementação. O novo conector inclui instruções de configuração abrangentes para conexão com o [!DNL Salesforce Marketing Cloud] e assimilação de dados de automação de marketing. |

Para obter mais informações, leia a [visão geral de fontes](../../sources/home.md).

