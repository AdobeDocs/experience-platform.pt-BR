---
title: Notas de versão da Adobe Experience Platform de setembro de 2025
description: As notas de versão de setembro de 2025 da Adobe Experience Platform.
source-git-commit: e21381f2683070fdbf24c473fa6794b89160864b
workflow-type: tm+mt
source-wordcount: '1402'
ht-degree: 21%

---

# Notas de versão da Adobe Experience Platform

>[!TIP]
>
>Consulte a documentação a seguir para obter as notas de versão de outros aplicativos da Adobe Experience Platform:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/whats-new/release-no)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/releases/pre-release-notes)
>- [Composição de público-alvo federado](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/e-release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/en/docs/real-time-cdp-collaboration/using/latest)

**Data de lançamento: 23 de setembro de 2025**

Novos recursos e atualizações dos recursos existentes no Adobe Experience Platform:

- [Agent Orchestrator](#agent-orchestrator)
- [Alertas](#alerts)
- [Destinos](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Perfil do cliente em tempo real](#profile)
- [Serviço de segmentação](#segmentation-service)
- [Origens](#sources)

## Agent Orchestrator {#agent-orchestrator}

O Adobe Experience Platform Agent Orchestrator é a nova camada de agente no Adobe Experience Platform.

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Agent Orchestrator | O Adobe Experience Platform Agent Orchestrator é a nova camada de agente no Adobe Experience Platform. Projetada para aproveitar os valiosos dados e conhecimentos de clientes da plataforma, a Experience Platform Agent Orchestrator capacita a inteligência e o raciocínio por trás dos agentes especializados Adobe Experience Platform criados com propósitos específicos, permitindo que eles executem tarefas complexas de tomada de decisões e solução de problemas em velocidade e escala — tudo com supervisão humana. Quando você faz perguntas ou solicita ajuda por meio da linguagem natural em uma interface conversacional como o AI Assistant, o Agent Orchestrator chama automaticamente agentes especializados para obter as respostas certas. O Agent Orchestrator lembra seu histórico de conversas, permitindo que você se baseie em perguntas anteriores naturalmente sem repetir o contexto e combina insights de vários agentes para apresentar respostas claras e unificadas. Para obter mais informações, leia a [documentação do Agent Orchestrator](https://experienceleague.adobe.com/en/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator). |
| Audience Agent | O Audience Agent permite exibir insights sobre públicos-alvo, incluindo a detecção de alterações significativas no tamanho do público-alvo, a detecção de públicos-alvo duplicados, a exploração do inventário do público-alvo e a recuperação do tamanho dele. Para obter mais informações, leia a [documentação do Audience Agent](https://experienceleague.adobe.com/en/docs/experience-cloud-ai/experience-cloud-ai/agents/audience). |

Para obter mais informações, leia a [documentação do Agent Orchestrator](https://experienceleague.adobe.com/en/docs/experience-cloud-ai/experience-cloud-ai/home).

## Alertas {#alerts}

O Experience Platform permite assinar alertas baseados em eventos para várias atividades do Experience Platform. Você pode assinar diferentes regras de alerta por meio da guia [!UICONTROL Alertas] na interface do usuário do Experience Platform e pode optar por receber mensagens de alerta na própria interface ou por meio de notificações por email.

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Alertas de assimilação de perfil de transmissão | Agora é possível assinar dois novos alertas para assimilação de streaming em um nível de fluxo de dados: <ul><li>Taxa de Falha de Assimilação de Streaming Excedida</li><li>Taxa de assimilação de streaming ignorada excedida</li></ul> Os alertas na plataforma ou por e-mail notificarão quando os limites forem excedidos para o limite padrão ou um limite personalizado definido por você. Para obter mais informações, leia o [Guia de alertas de perfil](../../observability/alerts/rules.md#profile). |

{style="table-layout:auto"}

Para obter mais informações sobre alertas, leia a [[!DNL Observability Insights] visão geral](../../observability/home.md).

## Destinos {#destinations}

[!DNL Destinations] são integrações pré-criadas com plataformas de destino que permitem a ativação contínua de dados do Experience Platform. É possível usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas de email, publicidade direcionada e muitos outros casos de uso.

**Destinos novos ou atualizados**

| Destino | Descrição |
| --- | --- |
| Conector [!BADGE Beta]{type=Informative} [[!DNL Snowflake Batch]](../../destinations/catalog/cloud-storage/snowflake-batch.md) | Um novo conector [!DNL Snowflake Batch] agora está disponível, fornecendo uma alternativa ao conector de streaming para casos de uso específicos. |
| Suporte a criptografia do [[!DNL Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md) | Agora é possível anexar chaves públicas formatadas em RSA para criptografar seus arquivos exportados, proporcionando o mesmo nível de segurança que outros destinos de armazenamento em nuvem oferecem para suas informações confidenciais. |
| Detalhes de expiração da autenticação para [[!DNL Pinterest]](../../destinations/catalog/advertising/pinterest.md) destinos | As informações de expiração da autenticação para destinos [!DNL Pinterest] agora estão visíveis diretamente na interface do Experience Platform, para que você possa ver quando sua autenticação expirará e a renovará antes de causar interrupções em seus fluxos de dados. É possível monitorar as datas de expiração do token a partir da coluna **[!UICONTROL Data de expiração da conta]** nas guias **[[!UICONTROL Contas]](../../destinations/ui/destinations-workspace.md#accounts)** ou **[[!UICONTROL Procurar]](../../destinations/ui/destinations-workspace.md#browse)**. |

**Funcionalidade nova ou atualizada**

| Recurso | Descrição |
| --- | --- |
| Recursos aprimorados de gerenciamento de destino na interface do usuário do Experience Platform | Melhore seu fluxo de trabalho de gerenciamento de destino com novos recursos de classificação nas guias [[!UICONTROL Procurar]](../../destinations/ui/destinations-workspace.md#browse) e [[!UICONTROL Contas]](../../destinations/ui/destinations-workspace.md#accounts). Agora, você também pode ver um indicador visual quando a autenticação da conta estiver prestes a expirar. <br> ![](../../destinations/assets/ui/workspace/expired-accounts.png){width="100" zoomable="yes"} |
| Configurações de largura da coluna persistente | As configurações de largura da coluna agora persistem ao sair de uma página e retornar a ela. Por exemplo, se você ajustar a largura de uma coluna na guia [[!UICONTROL Procurar]](../../destinations/ui/destinations-workspace.md#browse), a largura da coluna personalizada permanecerá a mesma quando você sair e retornar a essa guia. |

Para obter mais informações, leia a [Visão geral dos Destinos](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

O XDM é uma especificação de código aberto que fornece estruturas e definições comuns (esquemas) para dados trazidos para o Experience Platform. Ao aderir aos padrões do XDM, todos os dados de experiência do cliente podem ser incorporados em uma representação comum para fornecer insights de maneira mais rápida e integrada. Você pode obter insights valiosos sobre ações de clientes, definir públicos-alvo por meio de segmentos e usar atributos de clientes para fins de personalização.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Esquemas baseados em modelo | Simplifique a modelagem de dados com esquemas baseados em modelo. Agora é possível criar esquemas mais facilmente com exemplos e orientação abrangentes. Esse recurso está disponível no momento para os titulares de licença do Campaign Orchestration e será expandido para os clientes do Data Distiller em GA, tornando a modelagem de dados mais acessível e eficiente. O recurso inclui suporte para dados de série temporal e recursos de captura de dados de alteração. |

Para obter mais informações, leia a [visão geral do XDM](../../xdm/home.md).

<!--

| Data Mirror | Ingest row-level changes from cloud data warehouses (e.g., Snowflake, Databricks, BigQuery) into Adobe Experience Platform using model-based schemas. Data Mirror eliminates upstream ETL and preserves relationships, versioning, and deletions by mirroring existing database structures directly into the data lake. Time-series and record event schema behavior with change data capture capabilities are all supported. This feature is currently available for Campaign Orchestration license holders and will expand through this limited release, also including Customer Journey Analytics customers. See the [Data Mirror documentation](../../xdm/data-mirror/overview.md) for more details. Contact your Adobe representative for access. |
-->

## Perfil do cliente em tempo real {#profile}

A Adobe Experience Platform permite gerar experiências coordenadas, consistentes e relevantes para seus clientes, independentemente de onde ou quando eles interagem com sua marca. Com o Perfil do cliente em tempo real, é possível ter uma visão integral de cada cliente ao combinar dados de vários canais, incluindo online, offline, CRM e de terceiros. O Perfil permite consolidar os dados do cliente em uma visualização unificada, oferecendo uma conta acionável com carimbo de data e hora de cada interação com o cliente.

**Recursos atualizados**

| Recurso | Descrição |
| ------- | ----------- |
| Aprimoramentos do visualizador de perfil | A versão de setembro de 2025 inclui as seguintes melhorias no visualizador de perfil. <ul><li>**Modo de exibição combinado**: atributo, eventos e insights foram combinados em um único modo de exibição.</li><li>**Insights gerados por IA**: a página de detalhes do perfil agora exibe insights gerados por IA, permitindo que você saiba detalhes gerados pelo seu perfil. Esses insights podem incluir informações como pontuações de propensão e análise de tendências.</li><li>**Atualização de estilo**: a página de detalhes do perfil foi atualizada visualmente.</li><li>**Navegar**: agora você pode explorar seus perfis em um carrossel interativo baseado em cartão com pesquisa e personalização.</li></ul> |

Para obter mais informações, leia a [Visão geral do Perfil do cliente em tempo real](../../profile/home.md).

## Serviço de segmentação {#segmentation-service}

O [!DNL Segmentation Service] define um subconjunto específico de perfis descrevendo os critérios que distinguem um grupo de pessoas na sua base de clientes que pode ser direcionado por campanhas de marketing. Os públicos podem ser baseados em dados de registro (como informações demográficas) ou eventos de séries temporais que representam interações do cliente com sua marca.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| ------- | ----------- |
| Públicos-alvo da conta com descontinuação de eventos de experiência | Após a atualização da arquitetura B2B, os públicos-alvo da conta com eventos de experiência não serão mais compatíveis. Em vez disso, use a nova abordagem de segmento de segmentos: crie um público-alvo de Pessoas com eventos de experiência e, em seguida, consulte esse público-alvo de Pessoas ao criar um público-alvo de Conta. Isso fornece uma abordagem mais flexível e preservável para a criação de públicos-alvo B2B. |

**Atualizações importantes**

| Atualização | Descrição |
| ------- | ----------- |
| O público estima a reversão de atualização automática | O aprimoramento da atualização automática para estimativas de público-alvo foi revertido. As estimativas de público-alvo continuarão a ser geradas no Construtor de segmentos, mas a funcionalidade de atualização automática foi removida. |
| Público externo | A partir de 30 de setembro, os públicos-alvo externos serão recuperados por meio da Pesquisa unificada no Construtor de segmentos. Se você estiver usando a Correspondência de segmentos, poderá habilitar a experiência herdada no Construtor de segmentos. |

Para obter mais informações, leia a visão geral[&#128279;](../../segmentation/home.md) do [!DNL Segmentation Service] .

## Origens {#sources}

A Experience Platform fornece uma API RESTful e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar a sistemas de armazenamento externos e serviços de CRM, definir períodos para execuções de ingestão e gerenciar a taxa de transferência de ingestão de dados.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Novas fontes de disponibilidade geral | As seguintes origens estão agora em Disponibilidade geral: vários conectores de origem foram atualizados do Beta para o GA: <ul><li>[Assimilação de dados da Acxiom](../../sources/connectors/data-partners/acxiom-data-ingestion.md)</li><li>[Assimilação de dados de prospecto da Acxiom](../../sources/connectors/data-partners/acxiom-prospecting-data-import.md)</li><li>[Merkury Empresa](../../sources/connectors/data-partners/merkury.md)</li><li>[SAP Commerce](../../sources/connectors/ecommerce/sap-commerce.md)</li></ul>. Essas origens agora estão totalmente compatíveis e prontas para uso de produção. |
| Suporte à autenticação de par de chaves do [!DNL Snowflake] | Segurança aprimorada para conexões do Snowflake com suporte para autenticação de par de chaves. A autenticação básica (nome de usuário/senha) será descontinuada em novembro de 2025, portanto, os clientes são incentivados a migrar para a autenticação de par de chaves para melhorar a segurança. Para obter mais informações, leia a [[!DNL Snowflake] documentação](../../sources/connectors/databases/snowflake.md). |
| [!BADGE Beta]{type=Informative} [!DNL Capillary Streaming Events] | Use a [[!DNL Capillary Streaming Events] origem](../../sources/connectors/loyalty/capillary.md) para transmitir dados de fidelidade da sua conta do [!DNL Capillary] para a Experience Platform. |
| Disponibilidade geral do suporte a link privado nas origens | Agora você pode usar **links privados** para um grupo selecionado de fontes. Use este recurso para criar um ponto de extremidade privado ao qual a fonte possa se conectar. Com endpoints privados, você pode configurar conexões e fluxos de dados que ignoram a Internet pública, proporcionando maior segurança e isolamento de rede para seus dados confidenciais. O suporte para links privados está disponível para as seguintes fontes: <ul><li>[[!DNL Azure Blob Storage]](../../sources/connectors/cloud-storage/blob.md)</li><li>[[!DNL ADLS Gen2]](../../sources/connectors/cloud-storage/adls-gen2.md)</li><li>[[!DNL Azure File Storage]](../../sources/connectors/cloud-storage/azure-file-storage.md)</li></ul>. Para obter mais informações, leia os guias sobre como criar links privados [na API](../../sources/tutorials/api/private-link.md) e [na interface](../../sources/tutorials/ui/private-link.md). |

Para obter mais informações, leia a [visão geral de fontes](../../sources/home.md).
