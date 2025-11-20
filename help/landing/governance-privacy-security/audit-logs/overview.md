---
title: Audit Logs Overview
description: Saiba como os logs de auditoria permitem ver quem realizou quais ações na Adobe Experience Platform.
role: Admin,Developer
feature: Audits
exl-id: 00baf615-5b71-4e0a-b82a-ca0ce8566e7f
source-git-commit: d6575e44339ea41740fa18af07ce5b893f331488
workflow-type: tm+mt
source-wordcount: '1579'
ht-degree: 28%

---

# Logs de auditoria {#audit-logs}

>[!CONTEXTUALHELP]
>id="platform_audits_privacyconsole_actions"
>title="Principais ações"
>abstract="Esse widget mostra os principais tipos de ações que foram realizadas na Experience Platform no período selecionado. Para ver a lista completa de ações registradas na Experience Platform, selecione **Auditorias** no painel de navegação esquerdo."

>[!CONTEXTUALHELP]
>id="platform_audits_privacyconsole_users"
>title="Principais usuários"
>abstract="Esse widget mostra os usuários que executaram mais ações na Experience Platform no período selecionado. Para ver a lista completa de ações registradas na Experience Platform, selecione **Auditorias** no painel de navegação esquerdo."

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_audits_description"
>title="Monitorar atividades do usuário na Experience Platform"
>abstract="<h2>Descrição</h2><p>É possível monitorar a atividade do usuário em vários serviços e recursos da Experience Platform no formato de logs de auditoria. Esses logs formam uma trilha de auditoria que registra <b>quem</b> executou <b>qual</b> ação e <b>quando</b>. Os logs de auditoria podem ajudar com a solução de problemas na Experience Platform e auxiliar você a manter seu negócio em efetiva conformidade com as políticas corporativas de gerenciamento de dados e os requisitos regulatórios.</p>"

Para aumentar a transparência e a visibilidade das atividades realizadas no sistema, o Adobe Experience Platform permite auditar a atividade do usuário em vários serviços e recursos na forma de &quot;logs de auditoria&quot;. Esses registros formam uma trilha de auditoria que pode ajudar na solução de problemas no Experience Platform e ajudar sua empresa a cumprir com as políticas corporativas de gerenciamento de dados e os requisitos normativos.

Basicamente, um log de auditoria informa **quem** executou a ação **o que** e **quando**. Cada ação registrada em um log contém metadados que indicam o tipo de ação, a data e a hora, a ID do email do usuário que executou a ação e atributos adicionais relevantes ao tipo de ação.

Quando um usuário executa uma ação, dois tipos de eventos de auditoria são registrados. Um evento principal captura o resultado de autorização da ação, [!UICONTROL allow] ou [!UICONTROL deny], enquanto um evento aprimorado captura o resultado da execução, [!UICONTROL success] ou [!UICONTROL failure]. Vários eventos aprimorados podem ser vinculados ao mesmo evento principal. Por exemplo, ao ativar um destino, o evento principal registra a autorização da ação [!UICONTROL Destination Update], enquanto os eventos aprimorados registram várias ações [!UICONTROL Segment Activate].

>[!NOTE]
>
> Os metadados para as ações **Adicionar usuário** e **Remover usuário** dentro do recurso **Função** não conterão a ID de email do usuário que executou a ação. Em vez disso, os logs exibirão a ID de email gerada pelo sistema (system@adobe.com).

Este documento aborda logs de auditoria no Experience Platform, incluindo como visualizá-los e gerenciá-los na interface ou na API.

## Tipos de evento capturados por logs de auditoria {#category}

A tabela a seguir descreve quais ações em quais recursos são registrados por logs de auditoria:

| Recurso | Ações |
| --- | --- |
| [Política de controle de acesso (controle de acesso baseado em atributo)](../../../access-control/home.md) | <ul><li>Criar</li><li>Atualização</li><li>Excluir</li></ul> |
| [Conta (Adobe)](../../../sources/connectors/tutorials/ui/../../../tutorials/ui/update.md) | <ul><li>Criar</li><li>Atualização</li><li>Excluir</li></ul> |
| [Instância da IA de atribuição](../../../intelligent-services/attribution-ai/overview.md) | <ul><li>Criar</li><li>Atualização</li><li>Excluir</li><li>Habilitar</li><li>Desabilitar</li></ul> |
| [Logs de auditoria](../../../landing/governance-privacy-security/audit-logs/overview.md) | <ul><li>Exportar</li></ul> |
| [Classe](../../../xdm/schema/composition.md#class) | <ul><li>Criar</li><li>Atualização</li><li>Excluir</li></ul> |
| Computed attribute | <ul><li>Criar</li><li>Atualização</li><li>Excluir</li></ul> |
| [Instância da IA do cliente](../../../intelligent-services/customer-ai/overview.md) | <ul><li>Criar</li><li>Atualização</li><li>Excluir</li><li>Habilitar</li><li>Desabilitar</li></ul> |
| [Conjunto de dados](../../../catalog/datasets/overview.md) | <ul><li>Criar</li><li>Atualização</li><li>Excluir</li><li>Enable for [Real-Time Customer Profile](../../../profile/home.md)</li><li>Desativar para perfil</li><li>Adicionar dados</li><li>Excluir lote</li></ul> |
| [Datastream](../../../datastreams/overview.md) | <ul><li>Criar</li><li>Atualização</li><li>Excluir</li><li>Habilitar</li><li>Desabilitar</li><li>[Edit Mapping](../../../datastreams/data-prep.md)</li></ul> |
| [Tipos de dados](../../../xdm/schema/composition.md#data-type) | <ul><li>Criar</li><li>Atualização</li><li>Excluir</li></ul> |
| [Destino](../../../destinations/home.md) | <ul><li>Criar</li><li>Atualização</li><li>Excluir</li><li>Habilitar</li><li>Desabilitar</li><li>Ativar conjunto de dados</li><li>Remover conjunto de dados</li><li>Ativar perfil</li><li>Remover perfil</li></ul> |
| [Grupo de campos](../../../xdm/schema/composition.md#field-group) | <ul><li>Criar</li><li>Atualização</li><li>Excluir</li></ul> |
| [Gráfico de identidade](../../../identity-service/features/identity-graph-viewer.md) | <ul><li>Exibir</li></ul> |
| [Namespace de identidade](../../../identity-service/features/namespaces.md) | <ul><li>Criar</li><li>Atualização</li></ul> |
| [Política de mesclagem](../../../profile/merge-policies/overview.md) | <ul><li>Criar</li><li>Atualização</li><li>Excluir</li></ul> |
| [Perfil do produto](../../../access-control/home.md) | <ul><li>Criar</li><li>Atualização</li><li>Excluir</li></ul> |
| [Query](../../../query-service/ui/overview.md) | <ul><li>Executar</li></ul> |
| [Modelo de consulta](../../../query-service/ui/overview.md) | <ul><li>Criar</li><li>Atualização</li><li>Excluir</li></ul> |
| [Função (controle de acesso baseado no atributo)](../../../access-control/home.md) | <ul><li>Criar</li><li>Atualização</li><li>Excluir</li><li>Adicionar usuário</li><li>Remover usuário</li></ul> |
| [Sandbox](../../../sandboxes/home.md) | <ul><li>Criar</li><li>Atualização</li><li>Redefinir</li><li>Excluir</li></ul> |
| [Consulta agendada](../../../query-service/ui/overview.md) | <ul><li>Criar</li><li>Atualização</li><li>Excluir</li></ul> |
| [Esquema](../../../xdm/schema/composition.md) | <ul><li>Criar</li><li>Atualização</li><li>Excluir</li><li>Ativar para Perfil</li></ul> |
| [Segmento](../../../segmentation/home.md) | <ul><li>Criar</li><li>Excluir</li><li>Ativar segmento</li><li>Remover segmento</li></ul> |
| [Fluxo de dados do Source](../../../sources/connectors/tutorials/ui/../../../tutorials/ui/update.md) | <ul><li>Criar</li><li>Atualização</li><li>Excluir</li><li>Habilitar</li><li>Desabilitar</li><li>Ativar conjunto de dados</li><li>Remover conjunto de dados</li><li>Ativar perfil</li><li>Remover perfil</li></ul> |
| [Ordem de trabalho](../../../hygiene/home.md) | <ul><li>Criar</li></ul> |

## Acesso a logs de auditoria

Quando o recurso é ativado para sua organização, os logs de auditoria são coletados automaticamente conforme a atividade ocorre. Não é necessário ativar manualmente a coleção de logs.

Para exibir e exportar logs de auditoria, você deve ter a permissão de controle de acesso **[!UICONTROL View User Activity Log]** concedida (localizada na categoria [!UICONTROL Data Governance]). Para saber como gerenciar permissões individuais para recursos do Experience Platform, consulte a [documentação de controle de acesso](../../../access-control/home.md).

## Gerenciamento de logs de auditoria na interface {#managing-audit-logs-in-the-ui}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_audits_instructions"
>title="Instruções"
>abstract="<ul><li>Selecione <b>Auditorias</b> no painel de navegação esquerdo. O espaço de trabalho Auditorias mostra uma lista de logs registrados e por padrão classificados do mais recente para o menos recente.</li>   <li> OBSERVAÇÃO: Os logs de auditoria são retidos por 365 dias após o que serão excluídos do sistema. Portanto, você só pode voltar por um período máximo de 365 dias. Se precisar consultar dados com mais de 365 dias, exporte logs regularmente para atender aos requisitos de política interna. </li><li>Selecione um evento na lista para exibir seus detalhes no painel direito. </li><li>Selecione o ícone de funil para exibir uma lista de controles de filtro para ajudar a limitar os resultados. Somente os últimos 1.000 registros são exibidos, independentemente dos filtros selecionados. </li><li>Para exportar a lista atual de logs de auditoria, selecione **Baixar log**.</li><li>Para obter mais ajuda com esse recurso, consulte <a href="https://experienceleague.adobe.com/docs/experience-platform/landing/governance-privacy-security/audit-logs/overview.html?lang=pt-BR">visão geral dos logs de auditoria</a> na Experience League.</li></ul>"

Você pode visualizar logs de auditoria para diferentes recursos do Experience Platform no espaço de trabalho **[!UICONTROL Audits]** na interface do usuário do Experience Platform. O espaço de trabalho mostra uma lista de logs registrados, por padrão, classificados do mais recente ao menos recente.

![O painel Auditorias destacando Auditorias no menu esquerdo.](../../images/audit-logs/audits.png)

Os logs de auditoria são retidos por 365 dias após os quais serão excluídos do sistema. Se você precisar de dados com mais de 365 dias, exporte logs regularmente para atender aos requisitos da política interna.

Seu método de solicitar logs de auditoria altera o período permitido e o número de registros aos quais você terá acesso. [A exportação de logs](#export-audit-logs) permite voltar 365 dias (em intervalos de 90 dias) para um máximo de 10.000 logs de auditoria (principais ou aprimorados), em que a [IU do log de atividades](#filter-audit-logs) no Experience Platform exibe os últimos 90 dias a um máximo de 1.000 eventos principais, cada um deles com os eventos aprimorados correspondentes.

Selecione um evento na lista para exibir seus detalhes no painel direito.

![Guia Log de atividade do painel de auditorias com o painel de detalhes do evento realçado.](../../images/audit-logs/select-event.png)

### Filtrar logs de auditoria

Selecione o ícone do funnel (![Ícone de filtro](/help/images/icons/filter.png)) para exibir uma lista de controles de filtro para ajudar a limitar os resultados.

>[!NOTE]
>
>A interface do usuário do Experience Platform só exibe os últimos 90 dias até o máximo de 1000 eventos principais, cada um com os eventos aprimorados correspondentes, independentemente dos filtros aplicados. Se você precisar de logs depois disso (até um máximo de 365 dias), precisará [exportar seus logs de auditoria](#export-audit-logs).

![O painel de Auditorias com o log de atividades filtrado realçado.](../../images/audit-logs/filters.png)

Os seguintes filtros estão disponíveis para eventos de auditoria na interface do usuário:

| Filtro | Descrição |
| --- | --- |
| [!UICONTROL Category] | Use o menu suspenso para filtrar os resultados exibidos por [categoria](#category). |
| [!UICONTROL Action] | Filtrar por ação. As ações disponíveis para cada serviço podem ser vistas na tabela de recursos acima. |
| [!UICONTROL User] | Insira a ID de usuário completa (por exemplo, `johndoe@acme.com`) para filtrar por usuário. |
| [!UICONTROL Status] | Filtrar eventos de auditoria por resultado: êxito, falha, permissão ou negação devido à falta de [permissões de controle de acesso](../../../access-control/home.md). Para uma ação executada, os eventos principais mostram [!UICONTROL Allow] ou [!UICONTROL Deny]. When the core event is [!UICONTROL Allow], it may have attached one or more enhanced events showing **[!UICONTROL Success]** or **[!UICONTROL Failure]**. For example, a successful action shows [!UICONTROL Allow] on the core event and [!UICONTROL Success] on the attached enhanced event. |
| [!UICONTROL Date] | Selecione uma data inicial e/ou final para definir um intervalo de datas para filtrar os resultados. Data can be exported with a 90-day lookback period (for example, 2021-12-15 to 2022-03-15). This can differ by event type. |

Para remover um filtro, selecione o &quot;X&quot; no ícone de preenchimento do filtro em questão ou selecione **[!UICONTROL Clear all]** para remover todos os filtros.

![The Audits dashboard with clear filter highlighted.](../../images/audit-logs/clear-filters.png)

Os dados do log de auditoria retornados contêm as seguintes informações em todas as consultas que atendem aos critérios de filtro escolhidos.

| Nome da coluna | Descrição |
|---|---|
| [!UICONTROL Timestamp] | The exact date and time of the action performed in a `month/day/year hour:minute AM/PM` format. |
| [!UICONTROL Asset Name] | The value for the [!UICONTROL Asset Name] field depends on the category chosen as a filter. |
| [!UICONTROL Category] | This field matches the category selected in the filter dropdown. |
| [!UICONTROL Action] | As ações disponíveis dependem da categoria escolhida como filtro. |
| [!UICONTROL User] | Esse campo fornece a ID do usuário que executou a consulta. |

![O painel de Auditorias com o log de atividades filtrado realçado.](../../images/audit-logs/filtered.png)

### Exportar logs de auditoria {#export-audit-logs}

Para exportar a lista atual de logs de auditoria, selecione **[!UICONTROL Download log]**.

>[!NOTE]
>
>Os registros podem ser solicitados em intervalos de 90 dias até 365 dias retroativamente. However, the maximum amount of logs that can be returned during a single export is 10,000 audit events (either core or enhanced).

![O painel de Auditorias com o [!UICONTROL Download log] realçado.](../../images/audit-logs/download.png)

In the dialog that appears, select your preferred format (either **[!UICONTROL CSV]** or **[!UICONTROL JSON]**), then select **[!UICONTROL Download]**. The browser downloads the generated file and saves it to your machine.

![The file format selection dialog with [!UICONTROL Download] highlighted.](../../images/audit-logs/select-download-format.png)

## Ativar alertas {#enable-alerts}

You can enable audit alerts to receive notifications for the following rules:

* Criação de público
* Atualização de público
* Audience delete
* Dataset create
* Dataset update
* Exclusão do conjunto de dados
* Criação de esquema
* Atualização de esquema
* Exclusão de esquema

Selecione o alerta desejado na lista para assinar e receber notificações. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas usando a interface](../../../observability/alerts/ui.md).

## Gerenciamento de logs de auditoria na API

Todas as ações que você pode executar na interface do usuário também podem ser feitas usando chamadas de API. Consulte o [documento de referência da API](https://www.adobe.io/experience-platform-apis/references/audit-query/) para obter mais informações.

## Gerenciamento de logs de auditoria para o Adobe Admin Console

Para saber como gerenciar logs de auditoria para atividades no Adobe Admin Console, consulte o seguinte [documento](https://helpx.adobe.com/br/enterprise/using/audit-logs.html).

## Próximas etapas e recursos adicionais

Este guia abordou como gerenciar logs de auditoria no Experience Platform. Para obter mais informações sobre como monitorar as atividades do Experience Platform, consulte a documentação sobre [Insights de capacidade de observação](../../../observability/home.md) e [assimilação de dados de monitoramento](../../../ingestion/quality/monitor-data-ingestion.md).

Para reforçar sua compreensão de logs de auditoria no Experience Platform, assista ao seguinte vídeo:

>[!VIDEO](https://video.tv.adobe.com/v/344653?captions=por_br&quality=12&learn=on)
