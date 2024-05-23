---
title: Notas da versão de maio de 2024 da Adobe Experience Platform
description: As notas de versão de maio de 2024 da Adobe Experience Platform.
source-git-commit: 58de22b51bc721ec584b11e3f87c0ee210c0add5
workflow-type: tm+mt
source-wordcount: '1596'
ht-degree: 19%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: quarta-feira, 21 de maio de 2024**

>[!TIP]
>
>A variável [Documentação da API do Experience Platform](https://developer.adobe.com/experience-platform-apis/) O agora é interativo. Explore os endpoints da API diretamente nas páginas de documentação para obter feedback imediato e acelerar sua implementação técnica. [Leia mais](#interactive-api-documentation) sobre a nova funcionalidade.

Atualizações dos recursos existentes no Experience Platform:

- [Serviço de catálogo](#catalog-service)
- [Painéis](#dashboards)
- [Governança de dados](#governance)
- [Destinos](#destinations)
- [Query Service](#query-service)
- [Serviço de segmentação](#segmentation)
- [Origens](#sources)

Outras atualizações no Adobe Experience Platform:

- [Atualizações de documentação](#documentation-updates)

## Serviço de catálogo {#catalog-service}

O Serviço de catálogo é o sistema de registro para localização e linhagem de dados na Adobe Experience Platform. Embora todos os dados assimilados no Experience Platform sejam armazenados no data lake como arquivos e diretórios, o Catálogo retém os metadados e a descrição desses arquivos e diretórios para fins de pesquisa e monitoramento.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Ações em massa | O inventário do conjunto de dados agora oferece suporte a ações em massa. Simplifique os processos de gerenciamento de dados e garanta o gerenciamento eficiente de seus conjuntos de dados com ações em massa. Use ações em massa para economizar tempo, executando várias ações em vários conjuntos de dados simultaneamente.  As ações em massa incluem [Mover para a pasta](../../catalog/datasets/user-guide.md#move-to-folders), [Editar tags](../../catalog/datasets/user-guide.md#manage-tags), e [Excluir](../../catalog/datasets/user-guide.md#delete) conjuntos de dados. <br> ![Ações em massa no espaço de trabalho da interface do usuário de conjuntos de dados.](../2024/assets/may/bulk-actions.png "Ações em massa no espaço de trabalho da interface do usuário de conjuntos de dados."){width="100" zoomable="yes"} <br> Para obter mais informações sobre esse recurso, leia a [Guia da interface do usuário de conjuntos de dados](../../catalog/datasets/user-guide.md#bulk-actions). |

{style="table-layout:auto"}

## Painéis {#dashboards}

A Adobe Experience Platform fornece vários painéis para você visualizar insights importantes sobre os dados de sua organização, que são capturados por instantâneos diários.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Insights personalizáveis para relatórios estendidos do aplicativo | Perfeitamente [transforme o resultado da análise SQL em formatos visuais compreensíveis e amigáveis para os negócios](../../dashboards/data-distiller/customizable-insights/overview.md). Use consultas SQL personalizadas para manipulação de dados precisa e a criação de gráficos dinâmicos de diversos conjuntos de dados estruturados. Você pode usar o modo pro de consulta para executar análises complexas com SQL e, em seguida, compartilhar essa análise com usuários não técnicos por meio de gráficos em seu painel personalizado ou exportá-los em arquivos CSV. |

{style="table-layout:auto"}

## Governança de dados {#governance}

A Governança de dados da Adobe Experience Platform é uma série de estratégias e tecnologias usadas para gerenciar dados de clientes e garantir a conformidade com regulamentos, restrições e políticas aplicáveis ao uso de dados. Desempenha um papel fundamental na [!DNL Experience Platform] em vários níveis, incluindo catalogação, linhagem de dados, rotulagem de uso de dados, políticas de acesso a dados e controle de acesso a dados para ações de marketing.

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Suporte mTLS para destinos da API HTTP e ações personalizadas do Adobe Journey Optimizer | Aumente a confiança do cliente com as medidas de segurança reforçadas do protocolo MTLS (Mutual Transport Layer Security). A variável [Destino da API HTTP do Experience Platform](../../destinations/catalog/streaming/http-destination.md#mtls-protocol-support) e [Ações personalizadas do Adobe Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/using-custom-actions) agora oferecem suporte ao protocolo mTLS ao enviar dados para endpoints configurados. Nenhuma configuração adicional é necessária em sua ação personalizada ou destino da API HTTP para ativar o mTLS; esse processo ocorre automaticamente quando um terminal habilitado para mTLS é detectado. Você pode [baixe o certificado público do Adobe Journey Optimizer aqui](../../landing/governance-privacy-security/encryption.md#download-certificates) e a variável [Certificado público do Serviço de destinos aqui](../../landing/governance-privacy-security/encryption.md#download-certificates).<br>Consulte a [Documentação da criptografia de dados Experience Platform](../../landing/governance-privacy-security/encryption.md#mtls-protocol-support) para obter mais informações sobre protocolos de conexão de rede ao exportar dados para sistemas de terceiros. |

{style="table-layout:auto"}

## Destinos {#destinations}

[!DNL Destinations] são integrações pré-construídas com plataformas de destino que permitem a ativação perfeita de dados da Adobe Experience Platform. É possível usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas de email, publicidade direcionada e muitos outros casos de uso.

**Funcionalidades novas ou atualizadas** {#destinations-new-updated-functionality}

| Funcionalidade | Descrição |
| ----------- | ----------- |
| Reordenar campos de mapeamento para destinos em lote | Agora é possível alterar a ordem das colunas nas exportações de CSV arrastando e soltando os campos de mapeamento na [etapa de mapeamento](../../destinations/ui/activate-batch-profile-destinations.md#mapping). A ordem dos campos mapeados na interface reflete a ordem das colunas no arquivo CSV exportado, de cima para baixo, com a linha superior sendo a coluna mais à esquerda do arquivo CSV. <br> ![Exibição de como os mapeamentos podem ser reordenados.](../2024/assets/may/reorder-mappings.gif "Exibição de como os mapeamentos podem ser reordenados."){width="100" zoomable="yes"} |
| Agendamentos de exportação padrão pré-selecionados para destinos de lote | O Experience Platform agora define automaticamente um agendamento padrão para cada exportação de arquivo. Consulte a documentação em [agendamento de exportações de público](../../destinations/ui/activate-batch-profile-destinations.md#scheduling) para saber como modificar o cronograma padrão. |
| Editar vários agendamentos de ativação de público para destinos em lote | Agora é possível editar o agendamento de ativação para vários públicos-alvo exportados para um destino em lote (baseado em arquivo) no **[!UICONTROL Dados de ativação]** guia do [página de detalhes do destino](../../destinations/ui/destination-details-page.md#bulk-edit-schedule). <br> ![Visualização de como selecionar vários públicos-alvo e editar o agendamento de exportação de arquivos.](../2024/assets/may/bulk-edit-schedule.gif "Visualização de como selecionar vários públicos-alvo e editar o agendamento de exportação de arquivos."){width="100" zoomable="yes"} |
| Exportar vários públicos-alvo sob demanda para destinos em lote | Agora é possível selecionar e exportar vários públicos para destinos em lote por meio do [exportar arquivos por demanda](../../destinations/ui/export-file-now.md) funcionalidade. |

{style="table-layout:auto"}

Para obter informações mais gerais sobre destinos, consulte a [visão geral de destinos](../../destinations/home.md).

## Query Service {#query-service}

O Query Service permite usar SQL padrão para consultar dados no [!DNL Data Lake] da Adobe Experience Platform. Você pode associar qualquer conjunto de dados da [!DNL Data Lake] e capture os resultados da consulta como um novo conjunto de dados para usar em relatórios, no Data Science Workspace ou para assimilação no Perfil do cliente em tempo real.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Editor herdado obsoleto | O editor herdado foi descontinuado e não está mais acessível para uso. Em seu lugar, você pode usar o [recursos aprimorados do Editor de consultas](../../query-service/ui/user-guide.md#query-authoring) para gravar, validar e executar suas consultas. |
| Atraso da execução da consulta | Mantenha o controle das horas de computação definindo alertas de atrasos para as execuções de consulta. Você pode optar por receber alertas se um status de consulta não mudar após um período específico. Basta definir o tempo de atraso desejado na interface do usuário da Platform para se manter informado sobre o progresso da consulta. Para saber como definir esse alerta na interface do usuário do, consulte o [documentação de agendamentos de consulta](../../query-service/ui/query-schedules.md#alerts-for-query-status) ou o [guia para ações de consulta em linha](../../query-service/ui/monitor-queries.md#query-run-delay). |
| Inventário de log de consulta simplificado | Agora você pode usar uma melhor eficiência na solução de problemas e no monitoramento de tarefas com um [interface simplificada de logs de consulta](../../query-service/ui/query-logs.md#filter-logs): <ul><li> A interface do usuário da Platform agora exclui todas as &quot;Consultas do sistema&quot; da guia Logs por padrão. </li><li> Exibir consultas do sistema ao desmarcar **Excluir consultas do sistema**. </li></ul> <br> ![Guia Logs no espaço de trabalho da interface de queries.](../2024/assets/may/query-log.png "Guia Logs no espaço de trabalho da interface de queries."){width="100" zoomable="yes"} <br> Use a interface simplificada de logs de consulta para obter uma visualização mais focada, que ajuda a identificar e analisar rapidamente os logs relevantes. |
| Seletor de banco de dados | Use o novo menu suspenso do seletor de banco de dados para [acesse visualizações de dados do Customer Journey Analytics de forma conveniente a partir do Power BI Tableau](../../query-service/ui/credentials.md#connect-to-customer-journey-analytics). Agora é possível selecionar o banco de dados desejado diretamente na interface do usuário da Platform, para uma integração mais simples das ferramentas de BI. <br> ![Guia Credenciais no espaço de trabalho da interface do Queries.](../2024/assets/may/database-selector.png "Guia Credenciais no espaço de trabalho da interface do Queries."){width="100" zoomable="yes"} <br> |

{style="table-layout:auto"}

## Serviço de segmentação {#segmentation}

O [!DNL Segmentation Service] permite segmentar dados relacionados a indivíduos (como clientes, prospectos, usuários ou organizações) que estão armazenados na [!DNL Experience Platform] em públicos-alvo. Você pode criar públicos-alvo por meio de definições de segmento ou outras fontes a partir dos dados do [!DNL Real-Time Customer Profile]. Esses públicos-alvo são configurados e mantidos de forma centralizada na [!DNL Platform] e podem ser acessados a qualquer momento usando as soluções da Adobe.

**Recurso atualizado**

| Recurso | Descrição |
| --- | --- |
| Importar públicos gerados externamente | Agora a importação de públicos gerados externamente requer a permissão &quot;Importar público-alvo&quot;. Para saber mais sobre permissões, leia a [guia da interface de permissões](../../access-control/home.md#permissions). |

{style="table-layout:auto"}

## Origens {#sources}

A Experience Platform fornece uma API RESTful e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar a sistemas de armazenamento externos e serviços de CRM, definir períodos para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

Use fontes no Experience Platform para assimilar dados de um aplicativo Adobe ou de uma fonte de dados de terceiros.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Autenticação de Credencial de Cliente OAuth2 para [!DNL Salesforce] origem | Agora você pode usar a Credencial do cliente OAuth2 para autenticar seu [!DNL Salesforce] conta no Experience Platform. Leia o [!DNL Salesforce] origem [Guia da API](../../sources/tutorials/api/create/crm/salesforce.md) e [Guia da interface do usuário](../../sources/tutorials/ui/create/crm/salesforce.md) para obter mais informações. |
| Suporte para exemplo de fluxo de dados para o [!DNL Marketo Engage] origem | A variável [!DNL Marketo Engage] A origem agora é compatível com fluxos de dados de amostra. Ative a configuração de fluxo de dados de amostra para limitar a taxa de assimilação e experimente os recursos de Experience Platform sem precisar assimilar grandes quantidades de dados. Para obter mais informações, leia o guia em [criação de um fluxo de dados para [!DNL Marketo Engage] na interface](../../sources/tutorials/ui/create/adobe-applications/marketo.md). |
| Atualizações na lista de permissões de endereço IP | Dependendo da sua localização, você deve adicionar um conjunto de novos endereços IP à lista de permissões para usar fontes de transmissão com êxito. Para obter uma lista abrangente dos novos endereços IP, leia a [Guia de lista de permissões de endereço IP](../../sources/ip-address-allow-list.md). |

{style="table-layout:auto"}

**Documentação nova ou atualizada**

| Atualização da documentação | Descrição |
| --- | --- |
| Atualizações de documentação do [!DNL Google PubSub] | A variável [!DNL Google PubSub] a documentação de origem foi atualizada com um guia de pré-requisitos abrangente. Use a nova seção de pré-requisitos para saber como criar sua conta de serviço, conceder permissões no nível de tópico ou de assinatura e definir configurações para otimizar o uso do [!DNL Google PubSub] origem. Leia o [[!DNL Google PubSub] visão geral](../../sources/connectors/cloud-storage/google-pubsub.md) para obter mais informações. |

{style="table-layout:auto"}

Para obter mais informações sobre fontes, leia a [visão geral das origens](../../sources/home.md).

## Atualizações na documentação {#documentation-updates}

### Documentação da API Experience Platform interativa {#interactive-api-documentation}

A variável [Documentação da API do Experience Platform](https://developer.adobe.com/experience-platform-apis/) O agora é interativo. Todas as páginas de referência da API agora têm uma **Experimente** .funcionalidade que você pode usar para testar chamadas de API diretamente na página do site de documentação. [Obter as credenciais de autenticação necessárias](/help/landing/api-authentication.md) e comece a usar a funcionalidade para explorar os endpoints da API.

Use essa nova funcionalidade para explorar as solicitações para o e as respostas dos endpoints da API, para obter feedback imediato e acelerar sua implementação técnica. Por exemplo, visite o [API do serviço de identidade](https://developer.adobe.com/experience-platform-apis/references/identity-service/) ou o [API do registro de esquema](https://developer.adobe.com/experience-platform-apis/references/schema-registry/) endpoints para explorar o novo **Experimente** no painel direito.

![Gravação de tela mostrando uma chamada de API feita diretamente do site de documentação.](../2024/assets/may/api-playground-demo.gif)

>[!CAUTION]
>
>Observe que ao usar a funcionalidade de API interativa nas páginas de documentação, você está fazendo chamadas de API reais para os endpoints. Lembre-se disso ao testar sandboxes de produção.

### Insights e engajamento personalizados {#personalized-insights-engagement}

Uma nova página de documentação completa de casos de uso para o [evolução do valor único para o valor vitalício](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/evolve-one-time-value-to-lifetime-value.md) O agora está ativo. Leia esta documentação para entender como você pode usar o Real-Time CDP e o Adobe Journey Optimizer para converter visitantes esporádicos em suas propriedades da Web para clientes fiéis.
