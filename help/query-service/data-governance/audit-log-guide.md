---
title: Integração do log de auditoria do serviço de consulta
description: Os logs de auditoria do serviço de consulta mantêm registros de várias ações do usuário para formar uma trilha de auditoria para solucionar problemas ou seguir as políticas corporativas de gerenciamento de dados e os requisitos normativos. Este tutorial fornece uma visão geral dos recursos de log de auditoria específicos do Serviço de consulta.
exl-id: 5fdc649f-3aa1-4337-965f-3f733beafe9d
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '930'
ht-degree: 1%

---

# Integração do log de auditoria do [!DNL Query Service]

A integração do log de auditoria [!DNL Query Service] do Adobe Experience Platform fornece registros de ações de usuário relacionadas à consulta. Os logs de auditoria são uma ferramenta essencial para solucionar problemas e seguir as políticas corporativas de gerenciamento de dados e os requisitos normativos. O recurso permite retornar um log de ação para vários tipos de evento e filtrar e exportar os registros. Os logs podem ser acessados por meio da interface do usuário da Platform ou da [API de Consulta de Auditoria](https://www.adobe.io/experience-platform-apis/references/audit-query/) e baixados nos formatos de arquivo CSV ou JSON.

Para saber mais sobre a interface do usuário de logs de auditoria, consulte o [documento de visão geral dos logs de auditoria](../../landing/governance-privacy-security/audit-logs/overview.md). Para saber mais sobre como fazer chamadas para APIs da Platform, consulte o [guia da API de logs de auditoria](../../landing/api-guide.md).

## Pré-requisitos

Você deve ter a permissão [!DNL Data Governance] [!UICONTROL Exibir Log de Atividades do Usuário] habilitada para exibir o painel de log de auditoria na interface do usuário da plataforma. A permissão é habilitada por meio do Adobe [Admin Console](https://adminconsole.adobe.com/). Entre em contato com o administrador da organização se você não tiver privilégios de administrador para habilitar essa permissão. Consulte a documentação de controle de acesso para obter [instruções completas sobre como adicionar permissões por meio do Admin Console](../../access-control/home.md).

## [!DNL Query Service] categorias de log de auditoria {#audit-log-categories}

As categorias de log de auditoria fornecidas por [!DNL Query Service] são as seguintes.

| Categoria | Descrição |
|---|---|
| [!UICONTROL Query] | Esta categoria permite auditar execuções de consulta. |
| [!UICONTROL Modelo de consulta] | Esta categoria permite auditar as várias ações (criar, atualizar e excluir) executadas em um template de query. |
| [!UICONTROL Consulta agendada] | Esta categoria permite a auditoria de agendamentos que foram criados, atualizados ou excluídos em [!DNL Query Service]. |

## Executar um log de auditoria [!DNL Query Service] {#perform-an-audit-log}

Para fazer uma auditoria para atividades de [!DNL Query Service], selecione **[!UICONTROL Auditorias]** na navegação à esquerda, seguido pelo ícone de funil (![Um ícone de filtro.](/help/images/icons/filter.png)) para exibir uma lista de controles de filtro para ajudar a limitar os resultados.

![O painel de log de auditoria da interface do usuário da plataforma com &quot;Auditorias&quot; na navegação à esquerda e nos controles de filtro realçados.](../images/audit-log/filter-controls.png)

Na guia [!UICONTROL Auditorias] do painel [!UICONTROL Log de atividades], você pode filtrar todas as ações gravadas da Platform por qualquer uma das [!DNL Query Service] categorias. Os resultados do log podem ser filtrados ainda mais com base no período em que foram executados, na ação/função executada ou no usuário que emitiu a consulta. Consulte a documentação do log de auditoria para [instruções completas sobre como filtrar os logs com base na categoria, ação, usuário e status](../../landing/governance-privacy-security/audit-logs/overview.md#managing-audit-logs-in-the-ui).

Os dados do log de auditoria retornados contêm as seguintes informações em todas as consultas que atendem aos critérios de filtro escolhidos.

| Nome da coluna | Descrição |
|---|---|
| [!UICONTROL Carimbo de data/hora] | A data e hora exatas da ação executada em um formato `month/day/year hour:minute AM/PM`. |
| [!UICONTROL Nome do ativo] | O valor do campo [!UICONTROL Nome do ativo] depende da categoria escolhida como filtro. Ao usar a categoria [!UICONTROL Consulta agendada], este é o **nome do agendamento**. Ao usar a categoria [!UICONTROL Modelo de consulta], este é o **Nome do modelo**. Ao usar a categoria [!UICONTROL Consulta], esta é a **identificação da sessão** |
| [!UICONTROL Categoria] | Este campo corresponde à categoria selecionada por você na lista suspensa de filtros. |
| [!UICONTROL Ação] | Pode ser criar, excluir, atualizar ou executar. As ações disponíveis dependem da categoria escolhida como filtro. |
| [!UICONTROL Usuário] | Esse campo fornece a ID do usuário que executou a consulta. |

![O painel de Auditorias com o log de atividades filtrado realçado.](../images/audit-log/filtered-activity.png)

>[!NOTE]
>
>Mais detalhes da consulta são fornecidos ao baixar os resultados do log nos formatos de arquivo CSV ou JSON, do que são exibidos por padrão no painel de log de auditoria.

## Painel de detalhes

Selecione qualquer linha de resultados de log de auditoria para abrir um painel de detalhes à direita da tela.

![Guia Log de atividade do painel de auditorias com o painel de detalhes realçado.](../images/audit-log/details-panel.png)

O painel de detalhes pode ser usado para localizar a [!UICONTROL ID do ativo] e o [!UICONTROL status do evento].

O valor da [!UICONTROL ID do ativo] muda dependendo da categoria usada na auditoria.

* Ao usar a categoria [!UICONTROL Consulta], a [!UICONTROL ID do ativo] é a **ID da sessão**.
* Ao usar a categoria [!UICONTROL Modelo de consulta], a [!UICONTROL ID do ativo] é a **ID do modelo** e tem o prefixo `[!UICONTROL templateID:]`.
* Ao usar a categoria [!UICONTROL Consulta agendada], a [!UICONTROL ID do ativo] é a **ID do agendamento** e tem o prefixo `[!UICONTROL scheduleID:]`.

O valor do [!UICONTROL Status do evento] muda dependendo da categoria usada na auditoria.

* Ao usar a categoria [!UICONTROL Consulta], o campo [!UICONTROL Status do evento] fornece uma lista de todas as **IDs de consulta** executadas pelo usuário nessa sessão.
* Ao usar a categoria [!UICONTROL Modelo de consulta], o campo [!UICONTROL Status do evento] fornece o **Nome do modelo** como um prefixo para o status do evento.
* Ao usar a categoria [!UICONTROL Agendamento de consulta], o campo [!UICONTROL Status do evento] fornece o **nome do agendamento** como prefixo para o status do evento.

## Filtros disponíveis para [!DNL Query Service] categorias de log de auditoria {#available-filters}

Os filtros disponíveis variam de acordo com a categoria selecionada na lista suspensa. A tabela a seguir detalha os filtros disponíveis para [[!DNL Query Service] categorias de log de auditoria](#audit-log-categories).

| Filtro | Descrição |
|---|---|
| Categoria | Consulte a seção [[!DNL Query Service] categorias de log de auditoria](#audit-log-categories) para obter uma lista completa das categorias disponíveis. |
| Ação | Ao se referir a [!DNL Query Service] categorias de auditoria, a atualização é uma **modificação no formulário existente**, a exclusão é a **remoção do agendamento ou modelo**, a criação é **criação de um novo agendamento ou modelo** e a execução é **execução de uma consulta**. |
| Usuário(a)  | Insira a ID de usuário completa (por exemplo, johndoe@acme.com) para filtrar por usuário. |
| Status | As opções [!UICONTROL Permitir], [!UICONTROL Sucesso] e [!UICONTROL Falha] filtram os logs com base no &quot;Status&quot; ou &quot;Status do Evento&quot;, enquanto a opção [!UICONTROL Negar] filtrará **todos** logs. |
| Data | Selecione uma data inicial e/ou final para definir um intervalo de datas para filtrar os resultados. |

## Próximas etapas

Ao ler este documento, você tem uma melhor compreensão do recurso de log de auditoria do [!DNL Query Service] e como ele pode ser usado para filtrar suas ações de usuário do [!DNL Query Service].

Se estiver usando o recurso de log de auditoria [!DNL Query Service] para fins de solução de problemas, você deverá ler o [guia de solução de problemas](../troubleshooting-guide.md).
