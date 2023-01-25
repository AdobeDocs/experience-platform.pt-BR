---
title: Logs de consulta
description: Os logs de query são gerados automaticamente sempre que um query é executado e estão disponíveis por meio da interface do usuário para ajudar na solução de problemas. Este documento descreve como usar e navegar na seção Logs do serviço de query da interface do usuário.
source-git-commit: 22deca5f9bcf6bcf97cca01b97fce9d22800b767
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---

# Logs de consulta

A Adobe Experience Platform mantém um log de todos os eventos de query que ocorrem por meio da API e da interface do usuário. Essas informações estão disponíveis na interface do usuário do serviço de query do [!UICONTROL Logs] guia .

Os arquivos de log são gerados automaticamente por qualquer evento de query e contêm informações, incluindo o SQL usado, o status da query, o tempo necessário e o tempo de última execução. Você pode usar os dados do log de consultas como uma ferramenta poderosa para solucionar problemas de consultas ineficientes ou com problemas. Informações de log mais abrangentes são mantidas como parte do recurso de log de auditoria e podem ser encontradas no [documentação do log de auditoria](../../landing/governance-privacy-security/audit-logs/overview.md).

## Verificar logs de consulta

Para verificar os logs de consulta, selecione [!UICONTROL Queries] para navegar até a área de trabalho Serviço de query e selecione [!UICONTROL Log] nas opções disponíveis.

![A interface do usuário da plataforma com consultas e registro foi realçada.](../images/ui/query-log/logs.png)

## Personalizar e pesquisar {#customize-and-search}

Os logs do Serviço de query são apresentados em um formato de tabela personalizável. Para personalizar as colunas da tabela, selecione o ícone de configurações (![Um ícone de configurações.](../images/ui/query-log/settings-icon.png)) à direita da tela. A [!UICONTROL Personalizar tabela] será exibida onde cada coluna pode ser desmarcada.

Também é possível pesquisar logs relacionados a templates de query específicos, digitando o nome do template no campo de pesquisa.

![A área de trabalho Log de consultas com a barra de pesquisa e a lista suspensa da tabela de colunas gerenciar está realçada.](../images/ui/query-log/customize-logs.png)

A [descrição de cada coluna da tabela de log](./overview.md#log) pode ser encontrado na seção Log da visão geral do Serviço de query .

## Dados de log do Discover

Cada linha representa dados de log de uma execução de consulta associada a um modelo de consulta. Selecione qualquer linha da tabela para preencher a barra lateral direita com dados de log da execução.

![A área de trabalho Log de consultas com uma linha selecionada e os dados de log na barra lateral direita realçados.](../images/ui/query-log/log-details.png)

No painel de detalhes do log, é possível selecionar um novo conjunto de dados de saída e ver ou copiar a consulta SQL completa usada na execução.

![O espaço de trabalho Log de consultas com uma linha selecionada e o conjunto de dados de saída e a consulta SQL são realçados.](../images/ui/query-log/edit-output-dataset.png)

Também é possível selecionar um nome de modelo de consulta na variável [!UICONTROL Nome] para navegar diretamente para a [!UICONTROL Detalhes do log de consultas] exibir.

>[!NOTE]
>
>Se a consulta foi criada usando a API e nenhum nome de modelo foi fornecido durante a inicialização, as primeiras dezenas de caracteres da consulta SQL são exibidos.

![A exibição de detalhes do log de consultas.](../images/ui/query-log/query-log-details.png)

Ao lado do nome do modelo de cada linha ou do trecho SQL, há um ícone de lápis (![Um ícone de lápis.](../images/ui/query-log/edit-icon.png)) que você pode usar para navegar até o Editor de consultas. O query é então preenchido previamente no editor para edição.

![A área de trabalho Log de consultas com um ícone de lápis foi realçada.](../images/ui/query-log/edit-query.png)

## Próximas etapas

Ao ler este documento, agora você tem uma melhor compreensão de como os logs de consulta são acessados e usados na interface do usuário do Serviço de query.

Consulte a [Visão geral da interface do usuário](./overview.md)ou o [Guia da API do Serviço de query](../api/getting-started.md) para saber mais sobre os recursos do Serviço de query.

Consulte a [documento de consultas de monitor](./monitor-queries.md) para saber como o Serviço de query melhora a visibilidade de execuções de query agendadas.
