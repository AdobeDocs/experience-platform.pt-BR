---
title: Notas da versão de março de 2022 da Adobe Experience Platform
description: As notas da versão de março de 2022 da Adobe Experience Platform.
exl-id: 0d499aa6-e25d-4d34-ad32-5e4ab361cba1
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1182'
ht-degree: 13%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: quinta-feira, 30 de março de 2022**

Novos recursos na Adobe Experience Platform:

- [Logs de auditoria](#audit-logs)
- [Contas relacionadas no Real-Time CDP B2B edition](#related-accounts)

Atualizações dos recursos já existentes na Adobe Experience Platform:

- [Alertas](#alerts)
- [[!DNL Dashboards]](#dashboards)
- [Coleção de dados](#data-collection)
- [[!DNL Query Service]](#query-service)
- [Origens](#sources)

## Logs de auditoria {#audit-logs}

O Experience Platform permite auditar a atividade do usuário em vários serviços e recursos. Os logs de auditoria fornecem informações sobre quem fez o quê e quando.

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Logs de auditoria para conjunto de dados, esquema, classe, grupo de campo, tipo de dados, sandbox, destino, segmento, política de mesclagem, atributo calculado, perfil de produto e conta (Adobe) | Esses são os recursos que são registrados pelos logs de auditoria. Se o recurso estiver ativado, os logs de auditoria serão coletados automaticamente conforme a atividade ocorrer. Não é necessário ativar manualmente a coleção de logs. |
| Exportar logs de auditoria | Os logs de auditoria podem ser baixados como um arquivo `CSV` ou `JSON`. Os arquivos gerados são salvos diretamente em sua máquina. |

{style="table-layout:auto"}

Para obter mais informações sobre logs de auditoria no Experience Platform, consulte a [visão geral dos logs de auditoria](../../landing/governance-privacy-security/audit-logs/overview.md).

## Contas relacionadas no Real-Time CDP B2B edition {#related-accounts}

>[!NOTE]
>
>O recurso Contas relacionadas está disponível somente para clientes do Real-Time CDP B2B edition.

As empresas B2B geralmente têm suas informações de clientes armazenadas em vários sistemas, cada um incluindo apenas dados parciais ou até mesmo conflitantes para a mesma entidade comercial real. Isso cria um enorme desafio de chegar a uma visão precisa de seus clientes, reduzindo, portanto, a eficiência e a eficácia de seus esforços de marketing e vendas B2B. Com o lançamento de contas relacionadas, o [!DNL Real-Time CDP B2B] agora mostra uma lista de contas semelhantes à conta que você está navegando. É possível incluir as contas relacionadas nas definições de segmento para ampliar seu alcance ou aplicar critérios mais amplos em seus segmentos.

Leia mais sobre o recurso nas seguintes páginas de documentação:

- [Contas relacionadas na visão geral do Real-Time CDP B2B edition](../../rtcdp/b2b-ai-ml-services/related-accounts.md)
- [Guia Contas relacionadas no guia da interface do usuário Perfil de conta](../../rtcdp/accounts/account-profile-ui-guide.md#related-accounts-tab)
- [Como usar contas relacionadas nas definições de segmento](../../rtcdp/segmentation/b2b.md#related-accounts)

Para saber mais sobre o Real-Time CDP B2B edition, consulte a [visão geral](../../rtcdp/overview.md).

## Alertas {#alerts}

O Experience Platform permite assinar alertas baseados em eventos para várias atividades do Experience Platform. Você pode assinar diferentes regras de alerta por meio da guia [!UICONTROL Alertas] na interface do usuário do Experience Platform e pode optar por receber mensagens de alerta na própria interface ou por meio de notificações por email.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Novas regras de alerta | Duas novas regras de alerta agora estão disponíveis para fontes relacionadas à assimilação de dados. Consulte a visão geral em [regras de alerta](../../observability/alerts/rules.md) para obter a lista atualizada dos tipos de alerta. |

{style="table-layout:auto"}

Para obter mais informações sobre alertas no Experience Platform, consulte a [visão geral dos alertas](../../observability/alerts/overview.md).

## Painéis {#dashboards}

A Adobe Experience Platform fornece vários [!DNL dashboards] por meio dos quais você pode exibir informações importantes sobre os dados de sua organização, conforme capturados durante os instantâneos diários.

### Painéis de Perfil

O painel Perfis exibe um instantâneo dos dados do atributo (registro) que sua organização tem na área de armazenamento Perfil da Experience Platform.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Widget de Perfis não segmentados | O widget fornece o número total de todos os perfis não anexados a nenhum segmento. O número gerado é preciso desde o último instantâneo e representa a oportunidade de ativação de perfil em sua organização. Consulte a [documentação de widgets padrão de perfis](../../dashboards/guides/profiles.md#standard-widgets) para obter mais informações. |
| Widget de Tendência de perfis não segmentados | Esse widget fornece uma ilustração de gráfico de linhas para o número de perfis que não estão anexados a nenhum segmento em um determinado período. A tendência pode ser visualizada em períodos de 30 dias, 90 dias e 12 meses. Consulte a [documentação de widgets padrão de perfis](../../dashboards/guides/profiles.md#standard-widgets) para obter mais informações. |
| Widget Perfis não segmentados por identidade | Este widget categoriza o número total de perfis não segmentados por seu identificador exclusivo. Os dados são visualizados em um gráfico de barras. Consulte a [documentação de widgets padrão de perfis](../../dashboards/guides/profiles.md#standard-widgets) para obter mais informações. |
| Widget de perfis de identidade únicos | Esse widget fornece uma contagem dos perfis da sua organização que têm apenas um tipo de ID que cria a identidade, seja um email ou ECID. Consulte a [documentação de widgets padrão de perfis](../../dashboards/guides/profiles.md#standard-widgets) para obter mais informações. |

{style="table-layout:auto"}

Para obter mais informações sobre os painéis de Perfis, consulte a [Visão geral dos painéis de perfis](../../dashboards/guides/profiles.md).

### Painéis de destinos

O painel Destinos exibe um instantâneo dos destinos que sua organização ativou na Experience Platform.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Widget de contagem de destinos | O widget fornece o número total de endpoints disponíveis nos quais um público-alvo pode ser ativado e entregue no sistema. Esse número inclui destinos ativos e inativos. Consulte a [documentação do widget padrão de destinos](../../dashboards/guides/destinations.md#standard-widgets) para obter mais informações. |

{style="table-layout:auto"}

Para obter mais informações sobre painéis de Destinos no Experience Platform, consulte a [Visão geral dos painéis de Destinos](../../dashboards/guides/destinations.md).

## Coleção de dados {#data-collection}

O Experience Platform fornece um conjunto de tecnologias que permitem coletar dados de experiência do cliente do lado do cliente e enviá-los para o Adobe Experience Platform Edge Network, onde podem ser enriquecidos, transformados e distribuídos para destinos da Adobe ou que não sejam da Adobe.

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Configurações globais de sequência de dados | Agora você pode definir várias novas configurações globais ao configurar um fluxo de dados: localização geográfica, cookie de ID primária e sincronização de ID de terceiros. Consulte a seção sobre [configuração de uma sequência de dados](../../datastreams/overview.md#create) no guia da interface de sequências de dados para obter mais informações. |
| [API do Edge Network Server](../../server-api/overview.md) | A API do servidor permite que os clientes interajam com o Experience Platform Edge Network usando um novo endpoint autenticado para potencializar uma variedade de casos de uso de coleta de dados, personalização, publicidade e marketing. |

Para obter mais informações sobre a coleta de dados no Experience Platform, consulte a [visão geral da coleta de dados](../../collection/home.md).

## Query Service {#query-service}

[!DNL Query Service] permite que você use o SQL padrão para consultar dados no Adobe Experience Platform [!DNL Data Lake]. Você pode ingressar em qualquer conjunto de dados do [!DNL Data Lake] e capturar os resultados da consulta como um novo conjunto de dados para usar em relatórios, no Data Science Workspace ou para assimilação no Perfil do cliente em tempo real.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| `table_exists` | O comando new feature é usado para confirmar se uma tabela existe ou não no sistema. O comando retorna um valor booleano: `true` se a tabela **existir**, e `false` se a tabela existir **não**. Consulte a [documentação de sintaxe SQL](../../query-service/sql/syntax.md) para obter mais informações. |

{style="table-layout:auto"}

Para obter mais informações sobre recursos disponíveis, consulte a [Visão geral do Serviço de consulta](../../query-service/home.md).

## Origens {#sources}

O Adobe Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, estruturar, rotular e aprimorar esses dados usando os serviços da Experience Platform. É possível assimilar dados de várias origens, como aplicativos da Adobe, do armazenamento na nuvem, um software de terceiros e do seu sistema de CRM.

A Experience Platform fornece uma API RESTful e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar-se a sistemas de armazenamento externos e serviços de CRM, definir tempos para execuções de assimilação e gerenciar a assimilação de dados em todo o.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Novas fontes agora disponíveis para uso de B2B | Agora você pode usar todas as fontes disponíveis no Experience Platform para casos de uso de B2B. Consulte o [catálogo de fontes](../../sources/home.md) para obter uma lista completa das fontes disponíveis. |
| Disponibilidade geral da nova origem [!DNL Oracle Eloqua] | Agora você pode usar a origem [!DNL Oracle Eloqua] para assimilar dados facilmente da sua instância [!DNL Oracle Eloqua] (conta, campanha, contatos) na Experience Platform. Consulte a documentação sobre [criação de uma [!DNL Oracle Eloqua] conexão de origem](../../sources/connectors/marketing-automation/oracle-eloqua.md) para obter mais informações. |
| Aprimoramentos de API para [!DNL Data Landing Zone] | A origem [!DNL Data Landing Zone] agora oferece suporte à detecção automática de propriedades de arquivos ao usar a API [!DNL Flow Service]. Consulte a documentação sobre [criação de uma [!DNL Data Landing Zone] conexão de origem](../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md) para obter mais informações. |

{style="table-layout:auto"}

Para saber mais sobre fontes, consulte a [visão geral das fontes](../../sources/home.md).
