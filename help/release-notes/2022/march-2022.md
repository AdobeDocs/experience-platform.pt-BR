---
title: Notas de versão da Adobe Experience Platform
description: As notas de versão mais recentes do Adobe Experience Platform.
source-git-commit: 04d35137a301492794ab8c0c67183cf5c76f2105
workflow-type: tm+mt
source-wordcount: '1063'
ht-degree: 6%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 30 de março de 2022**

Novos recursos no Adobe Experience Platform:

- [Logs de auditoria](#audit-logs)

Atualizações dos recursos existentes na Adobe Experience Platform:

- [Alertas](#alerts)
- [[!DNL Dashboards]](#dashboards)
- [Experience Data Model (XDM)](#xdm)
- [[!DNL Query Service]](#query-service)
- [Fontes](#sources)

## Logs de auditoria {#audit-logs}

O Experience Platform permite auditar a atividade do usuário para vários serviços e recursos. Os logs de auditoria fornecem informações sobre quem fez o quê e quando.

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Logs de auditoria para conjunto de dados, esquema, classe, grupo de campos, tipo de dados, sandbox, destino, segmento, política de mesclagem, atributo calculado, perfil do produto e conta (Adobe) | Esses são os recursos que são registrados por logs de auditoria. Se o recurso estiver ativado, os logs de auditoria serão coletados automaticamente quando a atividade ocorrer. Não é necessário ativar manualmente a coleta de log. |
| Exportar logs de auditoria | Os logs de auditoria podem ser baixados como um `CSV` ou `JSON` arquivo. Os arquivos gerados são salvos diretamente no computador. |

{style=&quot;table-layout:auto&quot;}

Para obter mais informações sobre logs de auditoria na Platform, consulte [visão geral dos logs de auditoria](../../landing/governance-privacy-security/audit-logs/overview.md).

## Alertas {#alerts}

O Experience Platform permite assinar alertas baseados em eventos para várias atividades da plataforma. É possível assinar diferentes regras de alerta por meio do [!UICONTROL Alertas] na interface do usuário da plataforma e pode optar por receber mensagens de alerta na própria interface do usuário ou por meio de notificações por email.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Novas regras de alerta | Duas novas regras de alerta estão disponíveis para fontes relacionadas à assimilação de dados. Consulte a visão geral em [regras de alerta](../../observability/alerts/rules.md) para obter a lista atualizada de tipos de alertas. |

{style=&quot;table-layout:auto&quot;}

Para obter mais informações sobre alertas na Platform, consulte [visão geral dos alertas](../../observability/alerts/overview.md).

## Painéis {#dashboards}

O Adobe Experience Platform fornece vários [!DNL dashboards] através do qual você pode visualizar informações importantes sobre os dados de sua organização, conforme capturados durante os instantâneos diários.

### Painéis de perfil

O painel Perfis exibe um instantâneo dos dados de atributo (registro) que sua organização tem na Loja de perfis no Experience Platform.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Dispositivo de perfis não segmentados | O widget fornece o número total de perfis não anexados a nenhum segmento. O número gerado é preciso a partir do último instantâneo e representa a oportunidade para a ativação do perfil em toda a organização. Consulte a [documentação de perfis de widgets padrão](../../dashboards/guides/profiles.md#standard-widgets) para obter mais informações. |
| Dispositivo de tendência de perfis não segmentados | Este widget fornece uma ilustração de gráfico de linhas para o número de perfis que não estão anexados a nenhum segmento em um determinado período de tempo. A tendência pode ser visualizada por períodos de 30 dias, 90 dias e 12 meses. Consulte a [documentação de perfis de widgets padrão](../../dashboards/guides/profiles.md#standard-widgets) para obter mais informações. |
| Perfis não segmentados por dispositivo de identidade | Esse widget categoriza o número total de perfis não segmentados por seu identificador exclusivo. Os dados são visualizados em um gráfico de barras. Consulte a [documentação de perfis de widgets padrão](../../dashboards/guides/profiles.md#standard-widgets) para obter mais informações. |
| Dispositivo de perfis de identidade únicos | Esse widget fornece uma contagem dos perfis de sua organização que têm apenas um tipo de ID que cria sua identidade, seja um email ou uma ECID. Consulte a [documentação de perfis de widgets padrão](../../dashboards/guides/profiles.md#standard-widgets) para obter mais informações. |

Para obter mais informações sobre painéis de Perfis, consulte o [Visão geral dos painéis de perfis](../../dashboards/guides/profiles.md).

### Painéis de destinos

O painel Destinos exibe um instantâneo dos destinos que sua organização habilitou no Experience Platform.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Widget de contagem de destinos | O widget fornece o número total de endpoints disponíveis, onde um público-alvo pode ser ativado e entregue no sistema. Esse número inclui destinos ativos e inativos. Consulte a [documentação do widget padrão de destinos](../../dashboards/guides/destinations.md#standard-widgets) para obter mais informações. |

Para obter mais informações sobre painéis de Destinos na Platform, consulte o [Visão geral dos painéis de destinos](../../dashboards/guides/destinations.md).

## Experience Data Model (XDM) {#xdm}

O Experience Data Model (XDM) é uma especificação de código aberto que fornece estruturas e definições comuns (esquemas) para dados trazidos para o Adobe Experience Platform. Ao seguir os padrões XDM, todos os dados de experiência do cliente podem ser incorporados em uma representação comum para fornecer insights de uma maneira mais rápida e integrada. Você pode obter informações valiosas das ações do cliente, definir públicos-alvo do cliente por meio de segmentos e usar atributos do cliente para fins de personalização.

| Recurso | Descrição |
| --- | --- |
| Adicionar ou remover campos padrão individuais de um esquema | A interface do Editor de esquemas agora permite adicionar partes de grupos de campos padrão aos seus esquemas, fornecendo mais flexibilidade para os campos que você escolher incluir sem precisar criar recursos personalizados do zero.<br><br>Agora, também é possível definir campos personalizados ad-hoc diretamente na estrutura do schema e atribuí-los a um grupo de campos personalizado novo ou existente, sem precisar criar ou editar o grupo de campos antecipadamente.<br><br>Consulte o guia sobre [criar e editar esquemas na interface do usuário](../../xdm/ui/resources/schemas.md) para obter mais informações sobre esses novos workflows. |

{style=&quot;table-layout:auto&quot;}

Para obter mais informações sobre o XDM na Platform, consulte o [Visão geral do sistema XDM](../../xdm/home.md).

## Serviço de query {#query-service}

[!DNL Query Service] permite usar o SQL padrão para consultar dados no Adobe Experience Platform [!DNL Data Lake]. É possível unir qualquer conjunto de dados da [!DNL Data Lake] e capture os resultados do query como um novo conjunto de dados para usar nos relatórios, no Data Science Workspace ou para assimilação no Perfil do cliente em tempo real.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| `table_exists` | O novo comando feature é usado para confirmar se uma tabela existe ou não no sistema. O comando retorna um valor booleano: `true` se a tabela **does** existir e `false` se a tabela **not** existe. Consulte a [Documentação da sintaxe SQL](../../query-service/sql/syntax.md) para obter mais informações. |

Para obter mais informações sobre recursos disponíveis, consulte [Visão geral do Serviço de query](../../query-service/home.md).

## Fontes {#sources}

A Adobe Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, permitir estruturar, rotular e aprimorar esses dados usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

O Experience Platform fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e se conectar a sistemas de armazenamento externos e serviços CRM, definir horários para execuções de assimilação e gerenciar a assimilação de dados em todo o processo.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Novas fontes agora disponíveis para uso B2B | Agora você pode usar todas as fontes disponíveis na Plataforma para casos de uso B2B. Consulte a [catálogo de origens](../../sources/home.md) para obter uma lista completa das fontes disponíveis. |
| Disponibilidade geral de novos [!DNL Oracle Eloqua] source | Agora você pode usar o [!DNL Oracle Eloqua] fonte para assimilar dados com facilidade de sua [!DNL Oracle Eloqua] instância (conta, campanha, contatos) da Platform. Consulte a documentação em [criar um [!DNL Oracle Eloqua] conexão de origem](../../sources/connectors/oracle-eloqua.md) para obter mais informações. |
| Aprimoramentos de API para [!DNL Data Landing Zone] | O [!DNL Data Landing Zone] A origem agora oferece suporte à detecção automática de propriedades de arquivo ao usar o [!DNL Flow Service] API. Consulte a documentação em [criar um [!DNL Data Landing Zone] conexão de origem](../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md) para obter mais informações. |

{style=&quot;table-layout:auto&quot;}

Para saber mais sobre fontes, consulte o [visão geral das fontes](../../sources/home.md).
