---
title: Notas de pré-lançamento do Experience Platform
description: Uma visualização das notas de versão mais recentes do Adobe Experience Platform.
exl-id: a1b52e9f-1c4d-4a2b-9d3e-5f6a7b8c9d0e
source-git-commit: 3a45b3aadb08af98d6d379ecfc858474ea1e55db
workflow-type: tm+mt
source-wordcount: '1052'
ht-degree: 20%

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
>- [Customer Journey Analytics](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/releases/latest)
>- [Composição de público-alvo federado](https://experienceleague.adobe.com/pt-br/docs/federated-audience-composition/using/release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/pt-br/docs/real-time-cdp-collaboration/using/latest)

**Data de lançamento: fevereiro de 2026**

Novos recursos e atualizações dos recursos existentes no Adobe Experience Platform:

- [Agent Orchestrator](#agent-orchestrator)
- [Alertas](#alerts)
- [Coleção de dados](#data-collection)
- [Destinos](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Serviço de consultas](#query-service)
- [Fontes](#sources)

## Agent Orchestrator {#agent-orchestrator}

O Agent Orchestrator permite criar e implantar agentes alimentados por IA que podem automatizar fluxos de trabalho e interagir com clientes em vários canais.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Agente de integração de dados | Use o Agente de integração de dados para configurar conexões de origem, validar a qualidade dos dados, aplicar o enriquecimento semântico, revisar e validar esquemas e executar a assimilação de dados. Siga os workflows passo a passo para fluxos B2C e B2B, revise as saídas esperadas e solucione problemas comuns. |
| Data Distiller Agent | Use o Data Distiller Agent para criar jobs SQL a partir de linguagem natural, otimizar o desempenho SQL, recuperar de erros SQL, agendar e gerenciar jobs SQL e monitorar o status do job. Revise as medidas de proteção, as permissões necessárias e as orientações para solução de problemas para começar. |
| Agente de coleta de dados | Use o Agente de coleta de dados para obter orientação em contexto para configurações complexas de coleta de dados e explorar a linhagem, as dependências e os relacionamentos entre seus objetos de coleta de dados por meio de insights conversacionais. |

{style="table-layout:auto"}

Para obter mais informações, consulte a [documentação do Agent Orchestrator](https://experienceleague.adobe.com/pt-br/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator).

## Alertas {#alerts}

O Experience Platform permite assinar alertas baseados em eventos para várias atividades do Experience Platform. Você pode assinar diferentes regras de alerta por meio da guia [!UICONTROL Alerts] na interface do usuário do Experience Platform e pode optar por receber mensagens de alerta na própria interface do usuário ou por notificações de email.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Integração do [!DNL Slack] para alertas voltados para o cliente | Agora você pode enviar alertas voltados para o cliente para [!DNL Slack]. Siga o tutorial passo a passo para configurar a integração do [!DNL Slack] e receber notificações de alerta diretamente no seu espaço de trabalho [!DNL Slack]. |

{style="table-layout:auto"}

Para obter mais informações, leia a visão geral[&#128279;](../observability/home.md) do [!DNL Observability Insights] .

## Coleção de dados {#data-collection}

A Coleta de dados do Adobe Experience Platform fornece um conjunto de tecnologias que permitem coletar dados de experiência do cliente e enviá-los para o Adobe Experience Platform Edge Network e outros destinos.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Gerenciamento de extensões de tags da Adobe Platform | Use o novo recurso Gerenciamento de extensão para fazer upload, disponibilizar e lançar as extensões de sua organização para desenvolvimento, distribuição privada e pública. Encontre extensões privadas compartilhadas junto com suas extensões próprias na visualização da empresa de nível superior. Esse recurso oferece suporte a extensões da Web, de borda e móveis. |

{style="table-layout:auto"}

Para obter mais informações, leia a [documentação sobre Coleção de dados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/collection/home).

## Destinos {#destinations}

[!DNL Destinations] são integrações pré-criadas com plataformas de destino que permitem a ativação contínua de dados do Experience Platform. É possível usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas de email, publicidade direcionada e muitos outros casos de uso.

**Destinos novos ou atualizados**

| Destino | Descrição |
| --- | --- |
| Destino da conta [!DNL ZoomInfo] | Os usuários da CDP B2B agora podem ativar dados no nível da conta para [!DNL ZoomInfo] por meio do novo conector de destino da conta [!DNL ZoomInfo]. Configure o conector para começar a enviar os públicos da sua conta para o [!DNL ZoomInfo]. |
| [!DNL Snowflake] Lote geralmente disponível | O destino do lote [!DNL Snowflake] foi movido para disponibilidade geral. Agora você pode visualizar a coluna ID da política de mesclagem nos dados exportados junto com as colunas existentes, como carimbo de data e hora, atributos de mapeamento e associação de público-alvo. |
| Suporte à criptografia AES256 para destinos do [Amazon S3](../destinations/catalog/cloud-storage/amazon-s3.md#destination-details) | Agora você pode configurar a criptografia AES256 para suas exportações do Amazon S3. Escolha entre duas opções: <ul><li>**[!UICONTROL Default]**: o Experience Platform criptografa dados em repouso com o algoritmo de criptografia padrão definido no seu bucket.</li><li>**[!UICONTROL SSE-S3/AES256]**: o Experience Platform adiciona o cabeçalho `s3:x-amz-server-side-encryption": "AES256` à exportação e criptografa dados em repouso com o algoritmo AES256 quando chega ao S3. **Esta opção tem prioridade sobre qualquer algoritmo de criptografia padrão que você configurar no seu bucket do S3**.</li></ul> |

{style="table-layout:auto"}

Para obter mais informações, leia a [Visão geral dos Destinos](../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

O XDM é uma especificação de código aberto que fornece estruturas e definições comuns (esquemas) para dados trazidos para o Experience Platform. Ao aderir aos padrões do XDM, todos os dados de experiência do cliente podem ser incorporados em uma representação comum para fornecer insights de maneira mais rápida e integrada. Você pode obter insights valiosos sobre ações de clientes, definir públicos-alvo por meio de segmentos e usar atributos de clientes para fins de personalização.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| ------- | ----------- |
| Organização e Pesquisa do Inventário do Esquema | A página Navegar por esquemas agora inclui pesquisa e filtragem aprimoradas, ações em linha e suporte para tags e pastas definidas pelo usuário. Essas atualizações facilitam a localização, organização e gerenciamento de esquemas em sandboxes, reduzindo a navegação manual e o esforço de manutenção. |

Para obter mais informações, leia a [[!DNL Schemas] visão geral] (../xdm/home.md).

## Serviço de consultas {#query-service}

O Serviço de consultas permite usar SQL padrão para consultar dados no [!DNL Data Lake] da Adobe Experience Platform. Você pode ingressar em qualquer conjunto de dados do [!DNL Data Lake] e capturar os resultados da consulta como um novo conjunto de dados para usar em relatórios, no Data Science Workspace ou para assimilação no Perfil do cliente em tempo real.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Alinhamento da data de redefinição de cálculo anual do Data Distiller (Versão limitada) | As horas anuais de computação do Data Distiller agora são redefinidas na data de aniversário do contrato do Data Distiller, com base em quando a licença foi adquirida ou renovada. Isso alinha os relatórios de Uso de licença aos termos do contrato e pode resultar em um ajuste único aos valores de uso atuais. |
| Gerenciamento de sessão do Data Distiller (Versão limitada) | Como administrador autorizado, você pode exibir e gerenciar sessões ativas do Serviço de consulta e do Data Distiller na sua organização e sandbox por meio da interface do usuário. Use o gerenciamento de sessões para identificar sessões ociosas e encerrá-las para liberar capacidade. As proteções integradas impedem que você encerre sessões com consultas ativas. O recurso registra todas as ações de remoção para auditoria e notifica os usuários afetados. Você precisa da permissão **Gerenciar Sessões de Consulta** para acessar este recurso. |

{style="table-layout:auto"}

Para obter mais informações, leia a [Visão geral do Serviço de consulta](../query-service/home.md).

## Fontes {#sources}

A Experience Platform fornece uma API RESTful e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar a sistemas de armazenamento externos e serviços de CRM, definir períodos para execuções de ingestão e gerenciar a taxa de transferência de ingestão de dados.

**Fontes novas ou atualizadas**

| Fonte | Descrição |
| --- | --- |
| Suporte ao Catálogo de Unity no conector de origem [!DNL Databricks] | O conector de origem [!DNL Databricks] agora dá suporte ao Catálogo de Unidade. Leia a documentação atualizada do [[!DNL Databricks]](../sources/connectors/databases/databricks.md) para saber como usar o Catálogo do Unity ao configurar sua conexão de origem. |

{style="table-layout:auto"}

Para obter mais informações, leia a [visão geral de fontes](../sources/home.md).
