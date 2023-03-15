---
title: Integração do log de auditoria do serviço de consulta
description: Os logs de auditoria do serviço de consulta mantêm registros de várias ações do usuário para formar uma trilha de auditoria para solucionar problemas ou seguir as políticas corporativas de gerenciamento de dados e os requisitos normativos. Este tutorial fornece uma visão geral dos recursos de log de auditoria específicos do Serviço de consulta.
exl-id: 5fdc649f-3aa1-4337-965f-3f733beafe9d
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '935'
ht-degree: 2%

---

# [!DNL Query Service] integração do log de auditoria

O ADOBE EXPERIENCE PLATFORM [!DNL Query Service] a integração do log de auditoria fornece registros de ações do usuário relacionadas à consulta. Os logs de auditoria são uma ferramenta essencial para solucionar problemas e seguir as políticas corporativas de gerenciamento de dados e os requisitos normativos. O recurso permite retornar um log de ação para vários tipos de evento e filtrar e exportar os registros. Os logs podem ser acessados por meio da interface do usuário da plataforma ou do [API de consulta de auditoria](https://www.adobe.io/experience-platform-apis/references/audit-query/) e baixados nos formatos de arquivo CSV ou JSON.

Para saber mais sobre a interface do usuário de logs de auditoria, consulte o [documento de visão geral dos logs de auditoria](../../landing/governance-privacy-security/audit-logs/overview.md). Para saber mais sobre como fazer chamadas para APIs da Platform, consulte o [guia da API de logs de auditoria](../../landing/api-guide.md).

## Pré-requisitos

Você deve ter o [!DNL Data Governance] [!UICONTROL Exibir log de atividades do usuário] permissão ativada para exibir o painel de log de auditoria na interface do usuário da plataforma. A permissão é ativada por meio do Adobe [Admin Console](https://adminconsole.adobe.com/). Entre em contato com o administrador da organização se você não tiver privilégios de administrador para habilitar essa permissão. Consulte a documentação de controle de acesso para [instruções completas sobre como adicionar permissões por meio do Admin Console](../../access-control/home.md).

## [!DNL Query Service] categorias de log de auditoria {#audit-log-categories}

As categorias de log de auditoria fornecidas por [!DNL Query Service] são as seguintes.

| Categoria | Descrição |
|---|---|
| [!UICONTROL Consulta] | Esta categoria permite auditar execuções de consulta. |
| [!UICONTROL Modelo de consulta] | Esta categoria permite auditar as várias ações (criar, atualizar e excluir) executadas em um template de query. |
| [!UICONTROL Consulta agendada] | Esta categoria permite auditar os agendamentos que foram criados, atualizados ou excluídos no [!DNL Query Service]. |

## Execute um [!DNL Query Service] log de auditoria {#perform-an-audit-log}

Para executar uma auditoria para [!DNL Query Service] atividades, selecione **[!UICONTROL Auditorias]** na navegação à esquerda, seguido pelo ícone de funil (![Um ícone de filtro.](../images/audit-log/filter.png)) para exibir uma lista de controles de filtro para ajudar a limitar os resultados.

![O painel de log de auditoria da interface do usuário da Platform com &quot;Auditorias&quot; na navegação à esquerda e controles de filtro realçados.](../images/audit-log/filter-controls.png)

No [!UICONTROL Auditorias] painel [!UICONTROL Log de atividades] você pode filtrar todas as ações gravadas do Platform por qualquer uma das [!DNL Query Service] categorias. Os resultados do log podem ser filtrados ainda mais com base no período em que foram executados, na ação/função executada ou no usuário que emitiu a consulta. Consulte a documentação do log de auditoria para [instruções completas sobre como filtrar os logs com base na categoria, ação, usuário e status](../../landing/governance-privacy-security/audit-logs/overview.md#managing-audit-logs-in-the-ui).

Os dados do log de auditoria retornados contêm as seguintes informações em todas as consultas que atendem aos critérios de filtro escolhidos.

| Nome da coluna | Descrição |
|---|---|
| [!UICONTROL Carimbo de data e hora] | A data e a hora exatas da ação executada em um `month/day/year hour:minute AM/PM` formato. |
| [!UICONTROL Nome do ativo] | O valor para a variável [!UICONTROL Nome do ativo] depende da categoria escolhida como filtro. Ao usar o [!UICONTROL Consulta agendada] categoria esta é a **nome da programação**. Ao usar o [!UICONTROL Modelo de consulta] categoria, esta é a **nome do modelo**. Ao usar o [!UICONTROL Query] categoria, esta é a **session ID** |
| [!UICONTROL Categoria] | Este campo corresponde à categoria selecionada por você na lista suspensa de filtros. |
| [!UICONTROL Ação] | Pode ser criar, excluir, atualizar ou executar. As ações disponíveis dependem da categoria escolhida como filtro. |
| [!UICONTROL Usuário] | Esse campo fornece a ID do usuário que executou a consulta. |

![O painel Auditorias com o log de atividades filtrado realçado.](../images/audit-log/filtered-activity.png)

>[!NOTE]
>
>Mais detalhes da consulta são fornecidos ao baixar os resultados do log nos formatos de arquivo CSV ou JSON, do que são exibidos por padrão no painel de log de auditoria.

## Painel de detalhes

Selecione qualquer linha de resultados de log de auditoria para abrir um painel de detalhes à direita da tela.

![Painel de auditorias Guia Log de atividade com o painel de detalhes realçado.](../images/audit-log/details-panel.png)

O painel de detalhes pode ser usado para encontrar o [!UICONTROL ID do ativo] e a variável [!UICONTROL Status do evento].

O valor de [!UICONTROL ID do ativo] alterações dependendo da categoria usada na auditoria.

* Ao usar o [!UICONTROL Query] categoria, a variável [!UICONTROL ID do ativo] é o  **session ID**.
* Ao usar o [!UICONTROL Modelo de consulta] categoria, a variável [!UICONTROL ID do ativo] é o **ID do modelo** e com prefixo `[!UICONTROL templateID:]`.
* Ao usar o [!UICONTROL Consulta agendada] categoria, a variável [!UICONTROL ID do ativo] é o  **ID da programação** e com prefixo `[!UICONTROL scheduleID:]`.

O valor de [!UICONTROL Status do evento] alterações dependendo da categoria usada na auditoria.

* Ao usar o [!UICONTROL Query] categoria, a variável [!UICONTROL Status do evento] O campo fornece uma lista de todas as **IDs de consulta** executado pelo usuário nessa sessão.
* Ao usar o [!UICONTROL Modelo de consulta] categoria, a variável [!UICONTROL Status do evento] o campo fornece a **nome do modelo** como um prefixo para o status do evento.
* Ao usar o [!UICONTROL Agendamento da consulta] categoria, a variável [!UICONTROL Status do evento] o campo fornece a **nome da programação** como um prefixo para o status do evento.

## Filtros disponíveis para [!DNL Query Service] categorias de log de auditoria {#available-filters}

Os filtros disponíveis variam de acordo com a categoria selecionada na lista suspensa. A tabela a seguir detalha os filtros disponíveis para [[!DNL Query Service] categorias de log de auditoria](#audit-log-categories).

| Filtro | Descrição |
|---|---|
| Categoria | Consulte a [[!DNL Query Service] categorias de log de auditoria](#audit-log-categories) para obter uma lista completa das categorias disponíveis. |
| Ação | Quando se refere a [!DNL Query Service] categorias de auditoria, a atualização é um **modificação do formulário existente**, excluir é o **remoção do agendamento ou modelo**, criar é **criação de um novo agendamento ou modelo**, e executar é **execução de um query**. |
| Usuário | Insira a ID de usuário completa (por exemplo, johndoe@acme.com) para filtrar por usuário. |
| Status | A variável [!UICONTROL Permitir], [!UICONTROL Sucesso], e [!UICONTROL Falha] filtrar os logs com base no &quot;Status&quot; ou &quot;Status do evento&quot;, enquanto as opções [!UICONTROL Negar] a opção filtrará **all** logs. |
| Data | Selecione uma data inicial e/ou final para definir um intervalo de datas para filtrar os resultados. |

## Próximas etapas

Ao ler este documento, você terá uma melhor compreensão das [!DNL Query Service] recurso de log de auditoria e como ele pode ser usado para filtrar o [!DNL Query Service] ações do usuário.

Se você estiver usando o [!DNL Query Service] recurso de log de auditoria para fins de solução de problemas, é recomendável ler a [guia de solução de problemas](../troubleshooting-guide.md).
