---
title: Visão geral dos logs de auditoria
description: Saiba como os logs de auditoria permitem ver quem realizou quais ações na Adobe Experience Platform.
exl-id: 00baf615-5b71-4e0a-b82a-ca0ce8566e7f
source-git-commit: 8f61840ad60b7d24c980b218b6f742485f5ebfdd
workflow-type: tm+mt
source-wordcount: '1156'
ht-degree: 23%

---

# Logs de auditoria {#audit-logs}

>[!CONTEXTUALHELP]
>id="platform_audits_privacyconsole_actions"
>title="Principais ações"
>abstract="Este widget mostra os principais tipos de ações que foram realizadas no Experience Platform dentro do período de tempo selecionado. Para ver a lista completa de ações registradas na Platform, selecione **Auditorias** no painel de navegação esquerdo."

>[!CONTEXTUALHELP]
>id="platform_audits_privacyconsole_users"
>title="Principais usuários"
>abstract="Este widget mostra os usuários que executaram mais ações no Experience Platform dentro do período de tempo selecionado. Para ver a lista completa de ações registradas na Platform, selecione **Auditorias** no painel de navegação esquerdo."

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_audits_description"
>title="Monitorar atividades do usuário no Platform"
>abstract="<h2>Descrição</h2><p>Você pode monitorar a atividade do usuário para obter vários serviços e recursos da plataforma no formato de logs de auditoria. Esses logs formam uma trilha de auditoria que registra <b>who</b> executado <b>what</b> ação e <b>when</b>. Os registros de auditoria podem ajudar na solução de problemas no Platform e ajudar sua empresa a cumprir com as políticas corporativas de gerenciamento de dados e os requisitos normativos.</p>"

Para aumentar a transparência e a visibilidade das atividades realizadas no sistema, o Adobe Experience Platform permite auditar a atividade do usuário para vários serviços e recursos na forma de &quot;logs de auditoria&quot;. Esses registros formam uma trilha de auditoria que pode ajudar na solução de problemas na plataforma e ajudar sua empresa a cumprir com eficácia as políticas corporativas de gerenciamento de dados e os requisitos normativos.

Basicamente, um log de auditoria informa **quem** executou **qual** ação e **quando**. Cada ação registrada em um log contém metadados que indicam o tipo de ação, a data e a hora, a ID do email do usuário que executou a ação e atributos adicionais relevantes ao tipo de ação.

Este documento aborda logs de auditoria na Platform, incluindo como visualizá-los e gerenciá-los na interface do usuário ou na API.

## Tipos de evento capturados por logs de auditoria {#category}

A tabela a seguir descreve quais ações, em quais recursos do , são registradas por logs de auditoria:

| Recurso | Ações |
| --- | --- |
| [Política de controle de acesso (controle de acesso baseado em atributo)](../../../access-control/home.md) | <ul><li>Criar</li><li>Atualização</li><li>Excluir</li></ul> |
| [Conta (Adobe)](../../../sources/connectors/tutorials/ui/../../../tutorials/ui/update.md) | <ul><li>Criar</li><li>Atualização</li><li>Excluir</li></ul> |
| [Instância do Attribution AI](../../../intelligent-services/attribution-ai/overview.md) | <ul><li>Criar</li><li>Atualização</li><li>Excluir</li><li>Ativar</li><li>Desativar</li></ul> |
| [Logs de auditoria](../../../landing/governance-privacy-security/audit-logs/overview.md) | <ul><li>Exportar</li></ul> |
| [Classe](../../../xdm/schema/composition.md#class) | <ul><li>Criar</li><li>Atualização</li><li>Excluir</li></ul> |
| Atributo calculado | <ul><li>Criar</li><li>Atualização</li><li>Excluir</li></ul> |
| [Instância do Customer AI](../../../intelligent-services/customer-ai/overview.md) | <ul><li>Criar</li><li>Atualização</li><li>Excluir</li><li>Ativar</li><li>Desativar</li></ul> |
| [Conjunto de dados](../../../catalog/datasets/overview.md) | <ul><li>Criar</li><li>Atualização</li><li>Excluir</li><li>Ativar para [Perfil do cliente em tempo real](../../../profile/home.md)</li><li>Desativar para Perfil</li><li>Adicionar dados</li><li>Excluir lote</li></ul> |
| [Datastream](../../../edge/datastreams/overview.md) | <ul><li>Criar</li><li>Atualização</li><li>Excluir</li><li>Ativar</li><li>Desativar</li><li>[Editar mapeamento](../../../edge/datastreams/data-prep.md)</li></ul> |
| [Tipos de dados](../../../xdm/schema/composition.md#data-type) | <ul><li>Criar</li><li>Atualização</li><li>Excluir</li></ul> |
| [Destino](../../../destinations/home.md) | <ul><li>Criar</li><li>Atualização</li><li>Excluir</li><li>Ativar</li><li>Desativar</li><li>Ativação do conjunto de dados</li><li>Remoção do conjunto de dados</li><li>Ativação de perfil</li><li>Remover perfil</li></ul> |
| [Grupo de campos](../../../xdm/schema/composition.md#field-group) | <ul><li>Criar</li><li>Atualização</li><li>Excluir</li></ul> |
| [Gráfico de identidade](../../../identity-service/ui/identity-graph-viewer.md) | <ul><li>Exibir</li></ul> |
| [Namespace de identidade](../../../identity-service/ui/identity-graph-viewer.md) | <ul><li>Criar</li><li>Atualização</li></ul> |
| [Política de mesclagem](../../../profile/merge-policies/overview.md) | <ul><li>Criar</li><li>Atualização</li><li>Excluir</li></ul> |
| [Perfil de produto](../../../access-control/home.md) | <ul><li>Criar</li><li>Atualização</li><li>Excluir</li></ul> |
| [Consulta](../../../query-service/ui/overview.md) | <ul><li>Executar</li></ul> |
| [Modelo de consulta](../../../query-service/ui/overview.md) | <ul><li>Criar</li><li>Atualização</li><li>Excluir</li></ul> |
| [Função (controle de acesso baseado em atributo)](../../../access-control/home.md) | <ul><li>Criar</li><li>Atualização</li><li>Excluir</li><li>Adicionar usuário</li><li>Remover usuário</li></ul> |
| [Sandbox](../../../sandboxes/home.md) | <ul><li>Criar</li><li>Atualização</li><li>Redefinir</li><li>Excluir</li></ul> |
| [Consulta agendada](../../../query-service/ui/overview.md) | <ul><li>Criar</li><li>Atualização</li><li>Excluir</li></ul> |
| [Esquema](../../../xdm/schema/composition.md) | <ul><li>Criar</li><li>Atualização</li><li>Excluir</li><li>Ative para o Perfil</li></ul> |
| [Segmento](../../../segmentation/home.md) | <ul><li>Criar</li><li>Excluir</li><li>Ativar segmento</li><li>Remoção de segmento</li></ul> |
| [Fluxo de dados de origem](../../../sources/connectors/tutorials/ui/../../../tutorials/ui/update.md) | <ul><li>Criar</li><li>Atualização</li><li>Excluir</li><li>Ativar</li><li>Desativar</li><li>Ativação do conjunto de dados</li><li>Remoção do conjunto de dados</li><li>Ativar perfil</li><li>Remover perfil</li></ul> |
| [Ordem de serviço](../../../hygiene/home.md) | <ul><li>Criar</li></ul> |

## Acesso a logs de auditoria

Quando o recurso é ativado para sua organização, os logs de auditoria são coletados automaticamente conforme a atividade ocorre. Não é necessário ativar manualmente a coleção de log.

Para visualizar e exportar logs de auditoria, é necessário ter o **[!UICONTROL Exibir registro de atividades do usuário]** permissão de controle de acesso concedida (encontrada no [!UICONTROL Governança de dados] categoria). Para saber como gerenciar permissões individuais para recursos da plataforma, consulte [documentação de controle de acesso](../../../access-control/home.md).

## Gerenciamento de logs de auditoria na interface do usuário {#managing-audit-logs-in-the-ui}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_audits_instructions"
>title="Instruções"
>abstract="<ul><li>Selecionar <b>Auditorias</b> no painel de navegação esquerdo. O espaço de trabalho Audits mostra uma lista de logs registrados, por padrão classificados do mais recente para o menos recente.</li>   <li> OBSERVAÇÃO: Os logs de auditoria são retidos por 365 dias após o que serão excluídos do sistema. Portanto, você só pode voltar por um período máximo de 365 dias. Se precisar retroceder dados com mais de 365 dias, exporte logs regularmente para atender aos requisitos de política interna. </li><li>Selecione um evento na lista para exibir seus detalhes no painel direito. </li><li>Selecione o ícone de funil para exibir uma Lista de controles de filtro para ajudar a limitar os resultados. Somente os últimos 1000 registros são exibidos, independentemente dos filtros selecionados. </li><li>Para exportar a lista atual de logs de auditoria, selecione **Baixar log**.</li><li>Para obter mais ajuda com esse recurso, consulte o <a href="https://experienceleague.adobe.com/docs/experience-platform/landing/governance-privacy-security/audit-logs/overview.html?lang=pt-BR">visão geral dos logs de auditoria</a> na Experience League.</li></ul>"

Você pode visualizar logs de auditoria para diferentes recursos do Experience Platform na **[!UICONTROL Auditorias]** na interface do usuário da plataforma. O espaço de trabalho mostra uma lista de logs registrados, por padrão classificados do mais recente para o menos recente.

![Painel de logs de auditoria](../../images/audit-logs/audits.png)

Os logs de auditoria são retidos por 365 dias após o que serão excluídos do sistema. Portanto, você só pode voltar por um período máximo de 365 dias. Se você precisar de dados de mais de 365 dias, exporte logs regularmente para atender aos requisitos de política interna.

Selecione um evento na lista para exibir seus detalhes no painel direito.

![Detalhes do evento](../../images/audit-logs/select-event.png)

### Filtrar logs de auditoria

>[!NOTE]
Como esse é um novo recurso, os dados exibidos apenas retornam a março de 2022. Dependendo do recurso selecionado, dados anteriores poderão estar disponíveis a partir de janeiro de 2022.


Selecione o ícone de funil (![Ícone Filtro](../../images/audit-logs/icon.png)) para exibir uma lista de controles de filtro para ajudar a limitar os resultados. Somente os últimos 1000 registros são exibidos independentemente dos vários filtros selecionados.

![Filtros](../../images/audit-logs/filters.png)

Os seguintes filtros estão disponíveis para eventos de auditoria na interface do usuário:

| Filtro | Descrição |
| --- | --- |
| [!UICONTROL Categoria] | Use o menu suspenso para filtrar os resultados exibidos por [categoria](#category). |
| [!UICONTROL Ação] | Filtrar por ação. Somente no momento [!UICONTROL Criar] e [!UICONTROL Excluir] as ações podem ser filtradas. |
| [!UICONTROL Usuário] | Insira a ID completa do usuário (por exemplo, `johndoe@acme.com`) para filtrar por usuário. |
| [!UICONTROL Status] | Filtrar se a ação foi permitida (concluída) ou negada devido à falta de [controle de acesso](../../../access-control/home.md) permissões. |
| [!UICONTROL Data] | Selecione uma data inicial e/ou uma data final para definir um intervalo de datas para filtrar os resultados. Os dados podem ser exportados com um período de lookback de 90 dias (por exemplo, 2021-12-15 para 2022-03-15). Isso pode ser diferente por tipo de evento. |

Para remover um filtro, selecione o &quot;X&quot; no ícone de comprimido do filtro em questão ou selecione **[!UICONTROL Limpar tudo]** para remover todos os filtros.

![Limpar filtros](../../images/audit-logs/clear-filters.png)

### Exportar logs de auditoria

Para exportar a lista atual de logs de auditoria, selecione **[!UICONTROL Baixar log]**.

![Baixar log](../../images/audit-logs/download.png)

Na caixa de diálogo exibida, selecione o formato preferido (ou **[!UICONTROL CSV]** ou **[!UICONTROL JSON]**) e, em seguida, selecione **[!UICONTROL Baixar]**. O navegador baixa o arquivo gerado e o salva no computador.

![Selecionar formato de download](../../images/audit-logs/select-download-format.png)

## Gerenciamento de logs de auditoria na API

Todas as ações que você pode executar na interface do usuário também podem ser realizadas usando chamadas de API. Consulte a [documentação de referência da API do ](https://www.adobe.io/experience-platform-apis/references/audit-query/) para obter mais informações.

## Gerenciamento de logs de auditoria para o Adobe Admin Console

Para saber como gerenciar logs de auditoria de atividades no Adobe Admin Console, consulte o seguinte [documento](https://helpx.adobe.com/enterprise/using/audit-logs.html).

## Próximas etapas e recursos adicionais

Este guia cobriu como gerenciar logs de auditoria no Experience Platform. Para obter mais informações sobre como monitorar atividades da Platform, consulte a documentação em [Insights da capacidade de observação](../../../observability/home.md) e [monitoramento da ingestão de dados](../../../ingestion/quality/monitor-data-ingestion.md).

Para reforçar sua compreensão dos logs de auditoria no Experience Platform, assista ao seguinte vídeo:

>[!VIDEO](https://video.tv.adobe.com/v/341450?quality=12&learn=on)
