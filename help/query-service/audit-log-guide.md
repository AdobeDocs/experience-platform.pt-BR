---
title: Integração de Log de Auditoria do Serviço de Query
description: Os registros de auditoria do Serviço de Consulta mantêm registros de várias ações do usuário para formar uma trilha de auditoria para solucionar problemas ou seguir políticas corporativas de gerenciamento de dados e requisitos normativos. Este tutorial fornece uma visão geral dos recursos de log de auditoria específicos do Serviço de query.
source-git-commit: e227d52e1db89f79baf809324dfb5bf4a7ef4ef9
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 2%

---

# [!DNL Query Service] integração de log de auditoria

A Adobe Experience Platform [!DNL Query Service] a integração do log de auditoria fornece registros de ações de usuários relacionadas a consultas. Os registros de auditoria são uma ferramenta essencial para solucionar problemas e seguir as políticas corporativas de gerenciamento de dados e os requisitos normativos. O recurso permite retornar um log de ação para muitos tipos de evento e filtrar e exportar os registros. Os logs podem ser acessados por meio da interface do usuário da plataforma ou da variável [Auditoria da API de consulta](https://www.adobe.io/experience-platform-apis/references/audit-query/) e baixadas nos formatos de arquivo CSV ou JSON.

Para saber mais sobre a interface do usuário de logs de auditoria, consulte [documento de visão geral dos logs de auditoria](../landing/governance-privacy-security/audit-logs/overview.md). Para saber mais sobre como fazer chamadas para APIs da plataforma, consulte [guia da API de logs de auditoria](../landing/api-guide.md).

## Pré-requisitos

Você deve ter o [!UICONTROL Governança de dados] [!UICONTROL Exibir registro de atividades do usuário] permissão habilitada para exibir o painel de log de auditoria na interface do usuário da plataforma. A permissão é ativada por meio do Adobe [Admin Console](https://adminconsole.adobe.com/). Entre em contato com o administrador da organização se você não tiver privilégios de administrador para habilitar essa permissão. Consulte a documentação de controle de acesso para [instruções completas sobre como adicionar permissões por meio do Admin Console](../access-control/home.md).

## [!DNL Query Service] categorias de log de auditoria {#audit-log-categories}

As categorias de log de auditoria fornecidas por [!DNL Query Service] são como se segue.

| Categoria | Descrição |
|---|---|
| [!UICONTROL Consulta agendada] | Esta categoria permite auditar os agendamentos criados no [!DNL Query Service]. |
| [!UICONTROL Modelo de consulta] | Esta categoria permite auditar as várias ações realizadas em um template de query. |

## Executar um [!DNL Query Service] registro de auditoria {#perform-an-audit-log}

Para executar uma auditoria para [!DNL Query Service] atividades, selecione **[!UICONTROL Auditorias]** no painel de navegação esquerdo da interface do usuário da plataforma, seguido pelo ícone de funil (![Um ícone de filtro.](./images/audit-log/filter.png)) para exibir uma lista de controles de filtro para ajudar a limitar os resultados.

![O painel de log de auditoria da interface do usuário da plataforma com &quot;Auditorias&quot; na navegação à esquerda e nos controles de filtro destacados.](./images/audit-log/filter-controls.png)

No [!UICONTROL Auditorias] painel [!UICONTROL Log de atividades] , você pode filtrar todas as ações da Plataforma gravada por qualquer uma das [!DNL Query Service] categorias. Os resultados do log podem ser filtrados ainda mais com base no período em que foram executados, na ação/função executada ou no usuário que implementou a consulta. Consulte a documentação do log de auditoria para [instruções completas sobre como filtrar os logs com base na categoria, ação, usuário e status](../landing/governance-privacy-security/audit-logs/overview.md#managing-audit-logs-in-the-ui).

Os dados de log de auditoria retornados contêm as seguintes informações em todas as consultas que atendem aos critérios de filtro escolhidos.

| Nome da coluna | Descrição |
|---|---|
| [!UICONTROL Carimbo de data e hora] | A data e hora exatas da ação executada em um `month/day/year hour:minute AM/PM` formato. |
| [!UICONTROL Nome do ativo] | O valor da variável [!UICONTROL Nome do ativo] depende da categoria escolhida como filtro. Ao usar a variável [!UICONTROL Consulta agendada] categoria essa é a variável **nome da programação**. Ao usar a variável [!UICONTROL Modelo de consulta] categoria , este é o **nome do modelo**. |
| [!UICONTROL Categoria] | Esse campo corresponde à categoria selecionada por você na lista suspensa de filtros. |
| [!UICONTROL Ação] | Isso pode ser criado, excluído, atualizado ou executado. As ações disponíveis dependem da categoria escolhida como filtro. |
| [!UICONTROL Usuário] | Este campo fornece a ID do usuário que executou a consulta. |

![O painel Audits com o log de atividade filtrado é realçado.](./images/audit-log/filtered-activity.png)

>[!NOTE]
>
>Mais detalhes da consulta são fornecidos pelo download dos resultados do log em formatos de arquivo CSV ou JSON, que são exibidos por padrão no painel de log de auditoria.

Selecione qualquer linha de resultados de log de auditoria para abrir um painel de detalhes à direita da tela.

![Guia Audits do painel Log de atividades com o painel de detalhes realçado.](./images/audit-log/details-panel.png)

>[!NOTE]
>
>O painel de detalhes pode ser usado para localizar o [!UICONTROL ID do ativo]. O valor da variável [!UICONTROL ID do ativo] alterações, dependendo da categoria usada na auditoria. Ao usar a variável [!UICONTROL Modelo de consulta] categoria , a variável [!UICONTROL ID do ativo] é **ID do modelo**. Ao usar a variável [!UICONTROL Consulta agendada] categoria , a variável [!UICONTROL ID do ativo] é  **ID de programação**.

## Filtros disponíveis para [!DNL Query Service] categorias de log de auditoria {#available-filters}

Os filtros disponíveis variam dependendo da categoria selecionada na lista suspensa. A tabela a seguir detalha os filtros disponíveis para [[!DNL Query Service] categorias de log de auditoria](#audit-log-categories).

| Filtro | Descrição |
|---|---|
| Categoria | Consulte a [[!DNL Query Service] categorias de log de auditoria](#audit-log-categories) para obter uma lista completa das categorias disponíveis. |
| Ação | Ao se referir a [!DNL Query Service] categorias de auditoria, atualização é um **modificação do formulário existente**, excluir é o **remoção do calendário ou do modelo**, criar é **criação de um novo agendamento ou template** e execute está executando uma consulta. |
| Usuário | Insira a ID completa do usuário (por exemplo, johndoe@acme.com) para filtrar por usuário. |
| Data | Selecione uma data inicial e/ou uma data final para definir um intervalo de datas para filtrar os resultados. |

## Próximas etapas

Ao ler este documento, você tem uma melhor compreensão do [!DNL Query Service] recurso de log de auditoria e como ele pode ser usado para filtrar seu [!DNL Query Service] ações do usuário.

Se estiver usando o [!DNL Query Service] recurso de log de auditoria para fins de solução de problemas, é recomendável ler o [guia de solução de problemas](./troubleshooting-guide.md).
