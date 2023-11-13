---
title: Notas da versão de março de 2022 da Adobe Experience Platform
description: As notas da versão de março de 2022 da Adobe Experience Platform.
exl-id: 0d499aa6-e25d-4d34-ad32-5e4ab361cba1
source-git-commit: 3d0f2823dcf63f25c3136230af453118c83cdc7e
workflow-type: tm+mt
source-wordcount: '1176'
ht-degree: 19%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 30 de março de 2022**

Novos recursos na Adobe Experience Platform:

- [Logs de auditoria](#audit-logs)
- [Contas relacionadas no Real-Time CDP B2B Edition](#related-accounts)

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
| Logs de auditoria para conjunto de dados, esquema, classe, grupo de campo, tipo de dados, sandbox, destino, segmento, política de mesclagem, atributo calculado, perfil de produto e conta (Adobe) | Esses são os recursos que são registrados pelos logs de auditoria. Se o recurso estiver ativado, os logs de auditoria serão coletados automaticamente conforme a atividade ocorrer. Não é necessário ativar manualmente a coleção de log. |
| Exportar logs de auditoria | Os logs de auditoria podem ser baixados como um `CSV` ou `JSON` arquivo. Os arquivos gerados são salvos diretamente em sua máquina. |

{style="table-layout:auto"}

Para obter mais informações sobre logs de auditoria na Platform, consulte o [visão geral dos logs de auditoria](../../landing/governance-privacy-security/audit-logs/overview.md).

## Contas relacionadas no Real-Time CDP B2B Edition {#related-accounts}

>[!NOTE]
>
>O recurso Contas relacionadas está disponível somente para clientes do Real-Time CDP B2B Edition.

As empresas B2B geralmente têm suas informações de clientes armazenadas em vários sistemas, cada um incluindo apenas dados parciais ou até mesmo conflitantes para a mesma entidade comercial real. Isso cria um enorme desafio de chegar a uma visão precisa de seus clientes, reduzindo, portanto, a eficiência e a eficácia de seus esforços de marketing e vendas B2B. Com o lançamento das contas relacionadas, [!DNL Real-Time CDP B2B] O agora mostra uma lista de contas semelhantes à conta que você está navegando. É possível incluir as contas relacionadas nas definições de segmento para ampliar seu alcance ou aplicar critérios mais amplos em seus segmentos.

Leia mais sobre o recurso nas seguintes páginas de documentação:

- [Contas relacionadas na visão geral do Real-Time CDP B2B Edition](../../rtcdp/b2b-ai-ml-services/related-accounts.md)
- [Guia Contas relacionadas no guia da interface do usuário Perfil de conta](../../rtcdp/accounts/account-profile-ui-guide.md#related-accounts-tab)
- [Como usar contas relacionadas nas definições de segmento](../../rtcdp/segmentation/b2b.md#related-accounts)

Para saber mais sobre o Real-Time CDP B2B Edition, consulte a [visão geral](../../rtcdp/overview.md).

## Alertas {#alerts}

O Experience Platform permite assinar alertas baseados em eventos para várias atividades da Platform. É possível assinar diferentes regras de alerta por meio da [!UICONTROL Alertas] na interface do usuário da Platform e podem optar por receber mensagens de alerta na própria interface ou por notificações por email.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Novas regras de alerta | Duas novas regras de alerta agora estão disponíveis para fontes relacionadas à assimilação de dados. Consulte a visão geral em [regras de alerta](../../observability/alerts/rules.md) para obter a lista atualizada dos tipos de alerta. |

{style="table-layout:auto"}

Para obter mais informações sobre alertas na Platform, consulte a [visão geral dos alertas](../../observability/alerts/overview.md).

## Painéis {#dashboards}

O Adobe Experience Platform fornece vários [!DNL dashboards] por meio do qual você pode visualizar informações importantes sobre os dados de sua organização, conforme capturados durante instantâneos diários.

### Painéis de Perfil

O painel Perfis exibe um instantâneo dos dados do atributo (registro) que sua organização tem na Loja de perfis do Experience Platform.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Widget de Perfis não segmentados | O widget fornece o número total de todos os perfis não anexados a nenhum segmento. O número gerado é preciso desde o último instantâneo e representa a oportunidade de ativação de perfil em sua organização. Consulte a [documentação de widgets padrão de perfis](../../dashboards/guides/profiles.md#standard-widgets) para obter mais informações. |
| Widget de Tendência de perfis não segmentados | Esse widget fornece uma ilustração de gráfico de linhas para o número de perfis que não estão anexados a nenhum segmento em um determinado período. A tendência pode ser visualizada em períodos de 30 dias, 90 dias e 12 meses. Consulte a [documentação de widgets padrão de perfis](../../dashboards/guides/profiles.md#standard-widgets) para obter mais informações. |
| Widget Perfis não segmentados por identidade | Esse widget categoriza o número total de perfis não segmentados por seu identificador exclusivo. Os dados são visualizados em um gráfico de barras. Consulte a [documentação de widgets padrão de perfis](../../dashboards/guides/profiles.md#standard-widgets) para obter mais informações. |
| Widget de perfis de identidade únicos | Esse widget fornece uma contagem dos perfis da sua organização que têm apenas um tipo de ID que cria a identidade, seja um email ou ECID. Consulte a [documentação de widgets padrão de perfis](../../dashboards/guides/profiles.md#standard-widgets) para obter mais informações. |

{style="table-layout:auto"}

Para obter mais informações sobre painéis de perfis, consulte a [Visão geral dos painéis de perfis](../../dashboards/guides/profiles.md).

### Painéis de destinos

O painel Destinos exibe um instantâneo dos destinos que sua organização ativou no Experience Platform.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Widget de contagem de destinos | O widget fornece o número total de endpoints disponíveis nos quais um público-alvo pode ser ativado e entregue no sistema. Esse número inclui destinos ativos e inativos. Consulte a [documentação do widget padrão de destinos](../../dashboards/guides/destinations.md#standard-widgets) para obter mais informações. |

{style="table-layout:auto"}

Para obter mais informações sobre Painéis de destinos na Platform, consulte o [Visão geral dos painéis de destinos](../../dashboards/guides/destinations.md).

## Coleção de dados {#data-collection}

A Platform fornece um conjunto de tecnologias que permitem coletar dados da experiência do cliente e enviá-los à Rede de borda da Adobe Experience Platform, onde eles podem ser enriquecidos, transformados e distribuídos para destinos da Adobe ou de outras empresas.

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Configurações globais de sequência de dados | Agora você pode definir várias novas configurações globais ao configurar um fluxo de dados: localização geográfica, cookie de ID primária e sincronização de ID de terceiros. Consulte a seção sobre [configurar um fluxo de dados](../../datastreams/overview.md#create) no guia da interface dos fluxos de dados para obter mais informações. |
| [API do servidor da rede de borda](../../server-api/overview.md) | A API do servidor permite que os clientes interajam com a Rede de borda do Experience Platform usando um novo endpoint autenticado para potencializar uma variedade de casos de uso de coleta de dados, personalização, publicidade e marketing. |

Para obter mais informações sobre a coleta de dados na Platform, consulte a [visão geral da coleção de dados](../../collection/home.md).

## Query Service {#query-service}

[!DNL Query Service]O permite usar SQL padrão para consultar dados no [!DNL Data Lake] da Adobe Experience Platform. Você pode associar qualquer conjunto de dados da [!DNL Data Lake] e capture os resultados da consulta como um novo conjunto de dados para usar em relatórios, no Data Science Workspace ou para assimilação no Perfil do cliente em tempo real.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| `table_exists` | O comando new feature é usado para confirmar se uma tabela existe ou não no sistema. O comando retorna um valor booleano: `true` se a tabela **faz** existir, e `false` se a tabela não **não** existe. Consulte a [Documentação da sintaxe SQL](../../query-service/sql/syntax.md) para obter mais informações. |

{style="table-layout:auto"}

Para obter mais informações sobre recursos disponíveis, consulte [Visão geral do Serviço de consulta](../../query-service/home.md).

## Origens {#sources}

O Adobe Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, estruturar, rotular e aprimorar esses dados usando os serviços da plataforma. É possível assimilar dados de várias origens, como aplicativos da Adobe, do armazenamento na nuvem, um software de terceiros e do seu sistema de CRM.

A Experience Platform fornece uma API RESTful e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar-se a sistemas de armazenamento externos e serviços de CRM, definir tempos para execuções de assimilação e gerenciar a assimilação de dados em todo o.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Novas fontes agora disponíveis para uso de B2B | Agora você pode usar todas as fontes disponíveis na Platform para casos de uso de B2B. Consulte a [catálogo de origens](../../sources/home.md) para obter uma lista completa de fontes disponíveis. |
| Disponibilidade geral de novos [!DNL Oracle Eloqua] origem | Agora você pode usar o [!DNL Oracle Eloqua] fonte para assimilar dados facilmente de seus [!DNL Oracle Eloqua] instância (conta, campanha, contatos) para a Platform. Consulte a documentação em [criação de um [!DNL Oracle Eloqua] conexão de origem](../../sources/connectors/marketing-automation/oracle-eloqua.md) para obter mais informações. |
| Aprimoramentos na API para [!DNL Data Landing Zone] | A variável [!DNL Data Landing Zone] A origem agora oferece suporte à detecção automática de propriedades de arquivos ao usar o [!DNL Flow Service] API. Consulte a documentação em [criação de um [!DNL Data Landing Zone] conexão de origem](../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md) para obter mais informações. |

{style="table-layout:auto"}

Para saber mais sobre fontes, consulte a [visão geral das origens](../../sources/home.md).
