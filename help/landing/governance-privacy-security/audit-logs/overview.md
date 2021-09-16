---
title: Visão geral dos logs de auditoria
description: Saiba como os logs de auditoria permitem ver quem fez quais ações no Adobe Experience Platform.
exl-id: 00baf615-5b71-4e0a-b82a-ca0ce8566e7f
source-git-commit: 4dc49c7219ebb613c74e5960f1f8d477dc1b7605
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 5%

---

# Logs de auditoria (Beta)

>[!IMPORTANT]
>
>O recurso de logs de auditoria no Adobe Experience Platform está atualmente na versão beta. A funcionalidade descrita nesta documentação está sujeita a alterações.

Para aumentar a transparência e a visibilidade das atividades realizadas no sistema, o Adobe Experience Platform permite auditar a atividade do usuário para vários serviços e recursos na forma de &quot;logs de auditoria&quot;. Esses registros formam uma trilha de auditoria que pode ajudar na solução de problemas na plataforma e ajudar sua empresa a cumprir com eficácia as políticas corporativas de gerenciamento de dados e os requisitos normativos.

Em um sentido básico, um log de auditoria informa **quem** executou a ação **o que** e **quando**. Cada ação registrada em um log contém metadados que indicam o tipo de ação, a data e a hora, a ID do email do usuário que executou a ação e atributos adicionais relevantes ao tipo de ação.

Este documento aborda logs de auditoria na Platform, incluindo como visualizá-los e gerenciá-los na interface do usuário ou na API.

## Tipos de evento capturados por logs de auditoria {#category}

A tabela a seguir descreve quais ações em que os recursos são registrados pelos logs de auditoria:

| Recurso | Ações |
| --- | --- |
| [Conjunto de dados](../../../catalog/datasets/overview.md) | <ul><li>Criar</li><li>Atualização</li><li>Excluir</li><li>Habilitar para [Perfil do cliente em tempo real](../../../profile/home.md)</li></ul> |
| [Esquema](../../../xdm/schema/composition.md) | <ul><li>Criar</li><li>Atualização</li><li>Excluir</li></ul> |
| [Classe](../../../xdm/schema/composition.md#class) | <ul><li>Criar</li><li>Atualização</li><li>Excluir</li></ul> |
| [Grupo de campos](../../../xdm/schema/composition.md#field-group) | <ul><li>Criar</li><li>Atualização</li><li>Excluir</li></ul> |
| [Tipo de dados](../../../xdm/schema/composition.md#data-type) | <ul><li>Criar</li><li>Atualização</li><li>Excluir</li></ul> |
| [Sandbox](../../../sandboxes/home.md) | <ul><li>Criar</li><li>Atualização</li><li>Redefinir</li><li>Excluir</li></ul> |
| [Destino](../../../destinations/home.md) | <ul><li>Ativar</li></ul> |

## Acesso a logs de auditoria

Quando o recurso é ativado para sua organização, os logs de auditoria são coletados automaticamente conforme a atividade ocorre. Não é necessário ativar manualmente a coleta de log.

Para visualizar e exportar logs de auditoria, você deve ter a permissão de controle de acesso &quot;Exibir logs de auditoria&quot; concedida (localizada na categoria &quot;Governança de dados&quot;). Para saber como gerenciar permissões individuais para recursos da plataforma, consulte a [documentação de controle de acesso](../../../access-control/home.md).

## Gerenciamento de logs de auditoria na interface do usuário

Você pode visualizar logs de auditoria para diferentes recursos do Experience Platform no espaço de trabalho **[!UICONTROL Audits]** na interface do usuário da plataforma. O espaço de trabalho mostra uma lista de logs registrados, por padrão classificados do mais recente para o menos recente.

![Painel de logs de auditoria](../../images/audit-logs/audits.png)

O sistema exibe somente logs de auditoria do ano passado. Todos os logs que excederem esse limite serão automaticamente removidos do sistema.

Selecione um evento na lista para exibir seus detalhes no painel direito.

![Detalhes do evento](../../images/audit-logs/select-event.png)

Selecione o ícone de funil (![Filter icon](../../images/audit-logs/icon.png)) para exibir uma lista de controles de filtro para ajudar a limitar os resultados.

![Filtros](../../images/audit-logs/filters.png)

Os seguintes filtros estão disponíveis para eventos de auditoria na interface do usuário:

| Filtro | Descrição |
| --- | --- |
| [!UICONTROL Categoria] | Use o menu suspenso para filtrar os resultados exibidos por [category](#category). |
| [!UICONTROL Ação] | Filtrar por ação. Atualmente, somente as ações [!UICONTROL Create] e [!UICONTROL Delete] podem ser filtradas. |
| [!UICONTROL Status do Controle de Acesso] | Filtre se a ação foi permitida (concluída) ou negada devido à falta de permissões de [controle de acesso](../../../access-control/home.md). |
| [!UICONTROL Data] | Selecione uma data inicial e/ou uma data final para definir um intervalo de datas para filtrar os resultados. |

Para remover um filtro, selecione o &quot;X&quot; no ícone de comprimido do filtro em questão ou selecione **[!UICONTROL Limpar todos]** para remover todos os filtros.

![Limpar filtros](../../images/audit-logs/clear-filters.png)

<!-- (Planned for post-beta release)
### Export an audit log

Select **[!UICONTROL Download log]** to export an audit log.
-->

## Gerenciamento de logs de auditoria na API

Todas as ações que você pode executar na interface do usuário também podem ser realizadas usando chamadas de API. Consulte o [documento de referência da API](https://www.adobe.io/experience-platform-apis/references/audit-query/) para obter mais informações.

## Gerenciamento de logs de auditoria para o Adobe Admin Console

Para saber como gerenciar logs de auditoria de atividades no Adobe Admin Console, consulte o seguinte [document](https://helpx.adobe.com/enterprise/using/audit-logs.html).

## Próximas etapas

Este guia cobriu como gerenciar logs de auditoria no Experience Platform. Para obter mais informações sobre como monitorar as atividades da plataforma, consulte a documentação sobre [Insights de capacidade de observação](../../../observability/home.md) e [como monitorar a assimilação de dados](../../../ingestion/quality/monitor-data-ingestion.md).
