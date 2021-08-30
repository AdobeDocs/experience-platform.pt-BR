---
title: Visão geral dos logs de auditoria
description: Saiba como os logs de auditoria permitem ver quem fez quais ações no Adobe Experience Platform.
source-git-commit: 937225ff08e2e02c5840f86d6ed50644e05bdfe5
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 4%

---

# Logs de auditoria (Beta)

>[!IMPORTANT]
>
>O recurso de logs de auditoria no Adobe Experience Platform está atualmente na versão beta. A funcionalidade descrita nesta documentação está sujeita a alterações.

Para aumentar a transparência e a visibilidade das atividades realizadas no sistema, o Adobe Experience Platform permite auditar a atividade do usuário para vários serviços e recursos na forma de &quot;logs de auditoria&quot;. Esses registros formam uma trilha de auditoria que pode ajudar na solução de problemas na plataforma e ajudar sua empresa a cumprir com eficácia as políticas corporativas de gerenciamento de dados e os requisitos normativos.

Em um sentido básico, um log de auditoria informa **quem** executou a ação **o que** e **quando**. Cada ação registrada em um log contém metadados que indicam o tipo de ação, a data e a hora, a ID do email do usuário que executou a ação e atributos adicionais relevantes ao tipo de ação.

Este documento aborda logs de auditoria na Platform, incluindo como visualizá-los e gerenciá-los na interface do usuário ou na API.

## Tipos de evento capturados por logs de auditoria

A tabela a seguir descreve quais ações em que os recursos são registrados pelos logs de auditoria:

| Recurso | Ações |
| --- | --- |
| [Sandbox](../../../sandboxes/home.md) | <ul><li>Criar</li><li>Atualização</li><li>Redefinir</li><li>Excluir</li></ul> |
| [Conjunto de dados](../../../catalog/datasets/overview.md) | <ul><li>Criar</li><li>Atualização</li><li>Excluir</li><li>Habilitar para [Perfil do cliente em tempo real](../../../profile/home.md)</li></ul> |
| [Esquema](../../../xdm/schema/composition.md) | <ul><li>Criar</li><li>Atualização</li><li>Excluir</li></ul> |
| [Grupo de campos](../../../xdm/schema/composition.md#field-group) | <ul><li>Criar</li><li>Atualização</li><li>Excluir</li></ul> |
| [Destino](../../../destinations/home.md) | <ul><li>Ativar</li></ul> |

## Acesso a logs de auditoria

Quando o recurso é ativado para sua organização, os logs de auditoria são coletados automaticamente conforme a atividade ocorre. Não é necessário ativar manualmente a coleta de log.

Para visualizar e exportar logs de auditoria, você deve ter a permissão de controle de acesso &quot;Exibir logs de auditoria&quot; concedida. Para saber como gerenciar permissões individuais para recursos da plataforma, consulte a [documentação de controle de acesso](../../../access-control/home.md).

## Gerenciamento de logs de auditoria na interface do usuário

Você pode visualizar logs de auditoria para diferentes recursos do Experience Platform no espaço de trabalho **[!UICONTROL Audits]** na interface do usuário da plataforma. O espaço de trabalho mostra uma lista de logs registrados, por padrão classificados do mais recente para o menos recente.

![Painel de logs de auditoria](../../images/audit-logs/audits.png)

O sistema exibe somente logs de auditoria do ano passado. Todos os logs que excederem esse limite serão automaticamente removidos do sistema.

Selecione um evento na lista para exibir seus detalhes no painel direito.

![Detalhes do evento](../../images/audit-logs/select-event.png)

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