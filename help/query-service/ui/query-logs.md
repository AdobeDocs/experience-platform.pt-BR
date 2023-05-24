---
title: Logs de consulta
description: Os logs de consulta são gerados automaticamente cada vez que uma consulta é executada e ficam disponíveis por meio da interface do usuário para ajudar na solução de problemas. Este documento descreve como usar e navegar na seção Logs do serviço de consulta da interface do usuário.
exl-id: 929e9fba-a9ba-4bf9-a363-ca8657a84f75
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '585'
ht-degree: 0%

---

# Logs de consulta

>[!IMPORTANT]
>
>Determinados recursos de logs de consulta estão atualmente em uma versão limitada e não estão disponíveis para todos os clientes. Sua interface do usuário pode parecer um pouco diferente sem um ícone de edição. Além disso, o processo de selecionar um nome de consulta pode navegar até o Editor de consultas em vez da variável [!UICONTROL Detalhes do log de consulta] exibição.

O Adobe Experience Platform mantém um log de todos os eventos de consulta que ocorrem por meio da API e da interface do usuário. Essas informações estão disponíveis na interface do usuário do Serviço de consulta no [!UICONTROL Logs] guia.

Os arquivos de log são gerados automaticamente por qualquer evento de consulta e contêm informações, incluindo o SQL usado, o status da consulta, quanto tempo ela levou e o último tempo de execução. Você pode usar os dados do log de consultas como uma ferramenta poderosa para solucionar problemas de consultas ineficientes ou com problemas. Informações de log mais abrangentes são mantidas como parte do recurso de log de auditoria e podem ser encontradas na [documentação do log de auditoria](../../landing/governance-privacy-security/audit-logs/overview.md).

## Verificar logs de consulta

Para verificar os logs de consulta, selecione [!UICONTROL Consultas] para navegar até o espaço de trabalho do Serviço de consulta e selecionar [!UICONTROL Log] nas opções disponíveis.

![A interface do usuário da Platform com Queries e Log está realçada.](../images/ui/query-log/logs.png)

## Personalizar e pesquisar {#customize-and-search}

Os logs do Serviço de consulta são apresentados em um formato de tabela personalizável. Para personalizar as colunas da tabela, selecione o ícone de configurações (![Um ícone de configurações.](../images/ui/query-log/settings-icon.png)) à direita da tela. A [!UICONTROL Personalizar tabela] será exibida, onde cada coluna poderá ser desmarcada.

Você também pode pesquisar logs relacionados a modelos de consulta específicos digitando o nome do modelo no campo de pesquisa.

![A área de trabalho Log de Consultas com a barra de pesquisa e a lista suspensa gerenciar tabela de colunas destacadas.](../images/ui/query-log/customize-logs.png)

A [descrição de cada coluna da tabela de log](./overview.md#log) pode ser encontrado na seção Log da visão geral do Serviço de consulta.

## Descobrir dados de log

Cada linha representa dados de log para uma execução de consulta associada a um modelo de consulta. Selecione qualquer linha da tabela para preencher a barra lateral direita com dados de log para essa execução.

![O espaço de trabalho Log de Queries com uma linha selecionada e os dados de log na barra lateral direita destacados.](../images/ui/query-log/log-details.png)

No painel de detalhes do log, é possível selecionar um novo conjunto de dados de saída e ver ou copiar a consulta SQL completa usada na execução.

![O espaço de trabalho Log de consultas com uma linha selecionada e o conjunto de dados de saída e a consulta SQL realçados.](../images/ui/query-log/edit-output-dataset.png)

>[!IMPORTANT]
>
>Determinados recursos de logs de consulta estão atualmente em uma versão limitada e não estão disponíveis para todos os clientes.

Você também pode selecionar um nome de modelo de consulta na [!UICONTROL Nome] para navegar diretamente para a [!UICONTROL Detalhes do log de consulta] exibição.

>[!NOTE]
>
>Se a consulta foi criada usando a API e nenhum nome de template foi fornecido durante a inicialização, as primeiras dezenas de caracteres da consulta SQL são exibidos.

![A exibição de detalhes do log de Query.](../images/ui/query-log/query-log-details.png)

Ao lado do nome do modelo de cada linha ou do trecho SQL há um ícone de lápis (![Um lápis.](../images/ui/query-log/edit-icon.png)) que você pode usar para navegar até o Editor de consultas. A consulta é então preenchida previamente no editor para edição.

![O espaço de trabalho Log de Consultas com um ícone de lápis realçado.](../images/ui/query-log/edit-query.png)

## Próximas etapas

Ao ler este documento, agora é possível entender melhor como os logs de consulta são acessados e usados na interface do usuário do serviço de consulta.

Consulte a [Visão geral da interface](./overview.md)ou a variável [Guia da API do Serviço de consulta](../api/getting-started.md) para saber mais sobre os recursos do Serviço de consulta.

Consulte a [monitorar documento de consultas](./monitor-queries.md) para saber como o Serviço de consulta melhora a visibilidade de execuções de consultas programadas.
