---
title: Modelos de consulta
description: Os modelos de consulta são consultas SQL salvas reutilizáveis que podem ser reutilizadas por outros usuários para economizar tempo e esforço. Eles podem ser criados usando o Editor de consultas ou a API de serviço de consultas e estão disponíveis para uso em todos os conjuntos de dados do Experience Platform.
exl-id: e74d058f-bb89-45ed-83cc-2e3a33401270
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 0%

---

# Modelos de consulta

O Adobe Experience Platform Query Service permite salvar e reutilizar o código SQL na forma de modelos de consulta. Os modelos economizam esforço, evitando a repetição de tarefas executadas com frequência. Você pode compartilhar modelos em sua organização e alterar facilmente os valores de query sem precisar acessar ou entender o SQL subjacente.

Este documento fornece as informações necessárias para criar modelos de consulta no Serviço de consulta.

## Pré-requisitos

Você deve ter a permissão [!UICONTROL Gerenciar consultas] habilitada para acessar o Editor de consultas e exibir o painel de consultas na interface do Experience Platform. A permissão é habilitada por meio da Adobe [Admin Console](https://adminconsole.adobe.com/). Entre em contato com o administrador da organização se você não tiver privilégios de administrador para habilitar essa permissão. Consulte a documentação de controle de acesso para obter [instruções completas sobre como adicionar permissões por meio do Admin Console](../../access-control/home.md).

## Criar um modelo de consulta

Você pode criar modelos de consulta por meio de dois métodos, fazendo uma solicitação POST para o ponto de extremidade da API de Serviço de Consulta `query-templates` ou gravando, nomeando e salvando uma consulta por meio do Editor de Consultas.

### Use o Editor de consultas para criar e salvar uma consulta como modelo

Consulte a documentação para obter instruções sobre como usar o Editor de consultas para [gravar](./user-guide.md#query-authoring) e [salvar consultas](./user-guide.md#saving-queries). Depois de nomear e salvar sua consulta, ela estará disponível para ser reutilizada como um modelo de consulta na guia [!UICONTROL Modelos].

>[!TIP]
>
>Quando você salva uma consulta no Editor de consultas, uma mensagem de confirmação aparece para notificá-lo sobre a ação bem-sucedida. Esta mensagem pop-up contém um link que fornece uma maneira conveniente de navegar até o espaço de trabalho de agendamento de consultas. Consulte a [documentação de consultas de agendamento](./query-schedules.md) para saber como executar consultas em uma cadência personalizada.

## Procurar modelos de consulta {#browse}

No espaço de trabalho Consultas da interface do Experience Platform, selecione **[!UICONTROL Modelos]** para exibir a lista de consultas salvas disponíveis.

![O espaço de trabalho de consultas com a guia Modelos realçada.](../images/ui/query-templates/query-templates.png)

Para encontrar informações relevantes sobre o modelo, selecione qualquer modelo de consulta na lista disponível para abrir o painel de detalhes.

![O painel de detalhes no espaço de trabalho de consultas com a ID de consulta realçada.](../images/ui/query-templates/details-panel.png)

No painel de detalhes, é possível executar as seguintes ações:

* Selecione **[!UICONTROL Executar como CTAS]** para criar uma nova tabela selecionando dados de uma ou mais tabelas existentes. Essa opção só estará disponível se você tiver uma consulta SELECT.
* Selecione **[!UICONTROL Adicionar agendamento]** para começar a editar seu agendamento para seu modelo de consulta.
* Selecione **[!UICONTROL Exibir agendamento]** para navegar até a guia [!UICONTROL Agendamentos] do Editor de Consulta. Essa exibição contém todas as informações de agendamento associadas à consulta.
* Selecione **[!UICONTROL Excluir consulta]** para excluir o modelo.
* Selecione o nome do modelo para navegar até o Editor de consultas onde o SQL está pré-preenchido para edição.

### Usar a API do Serviço de consulta para criar um modelo

Consulte a documentação para obter instruções sobre [como criar um modelo de consulta](../api/query-templates.md#create-a-query-template) usando a API do Serviço de Consulta. Os detalhes de um template de consulta recém-criado estão contidos no corpo da resposta.

>[!NOTE]
>
>Os modelos criados usando a API também estão visíveis na guia Modelos do serviço de consulta da interface do Experience Platform.

## Próximas etapas

Ao ler este documento, agora você tem uma melhor compreensão de como criar modelos de consulta no Serviço de consulta. Consulte a [visão geral da interface](./overview.md) ou o [Guia da API do Serviço de Consulta](../api/getting-started.md) para saber mais sobre os recursos do Serviço de Consulta.

Consulte o [manual de endpoint de consultas agendadas](../api/scheduled-queries.md) para saber como agendar consultas usando a API ou o [guia do Editor de Consultas](./user-guide.md#scheduled-queries) para a interface do usuário.
