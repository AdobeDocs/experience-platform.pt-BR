---
title: Modelos de consulta
description: Os modelos de consulta são consultas SQL salvas reutilizáveis que podem ser reutilizadas por outros usuários para economizar tempo e esforço. Eles podem ser criados usando o Editor de consultas ou a API de serviço de consultas e estão disponíveis para uso em todos os conjuntos de dados de Experience Platform.
exl-id: e74d058f-bb89-45ed-83cc-2e3a33401270
source-git-commit: d5d69134627b1a162691bda95732d989bd6e3469
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 0%

---

# Modelos de consulta

O Adobe Experience Platform Query Service permite salvar e reutilizar o código SQL na forma de modelos de consulta. Os modelos economizam esforço, evitando a repetição de tarefas executadas com frequência. Você pode compartilhar modelos em sua organização e alterar facilmente os valores de query sem precisar acessar ou entender o SQL subjacente.

Este documento fornece as informações necessárias para criar modelos de consulta no Serviço de consulta.

## Pré-requisitos

Você deve ter o [!UICONTROL Gerenciar consultas] permissão ativada para acessar o Editor de consultas e visualizar o painel de consultas na interface do usuário da Platform. A permissão é ativada por meio do Adobe [Admin Console](https://adminconsole.adobe.com/). Entre em contato com o administrador da organização se você não tiver privilégios de administrador para habilitar essa permissão. Consulte a documentação de controle de acesso para [instruções completas sobre como adicionar permissões por meio do Admin Console](../../access-control/home.md).

## Criar um modelo de consulta

Você pode criar modelos de consulta por meio de dois métodos, fazendo uma solicitação POST para a API do Serviço de consulta `query-templates` endpoint ou gravando, nomeando e salvando uma consulta por meio do Editor de consultas.

### Use o Editor de consultas para criar e salvar uma consulta como modelo

Consulte a documentação para obter instruções sobre como usar o Editor de consultas para [gravação](./user-guide.md#query-authoring) e [salvar consultas](./user-guide.md#saving-queries). Depois de nomear e salvar sua consulta, ela estará disponível para ser reutilizada como um template de consulta no [!UICONTROL Modelos] guia.

## Procurar modelos de consulta {#browse}

No espaço de trabalho Queries da interface do Platform, selecione **[!UICONTROL Modelos]** para exibir a lista de consultas salvas disponíveis.

![O espaço de trabalho de consultas com a guia Modelos realçada.](../images/ui/query-templates/query-templates.png)

Para encontrar informações relevantes sobre o modelo, selecione qualquer modelo de consulta na lista disponível para abrir o painel de detalhes.

![O painel de detalhes no espaço de trabalho de consultas com a ID de consulta destacada.](../images/ui/query-templates/details-panel.png)

No painel de detalhes, é possível executar quatro ações separadas:

* Selecionar **[!UICONTROL Conjunto de dados de saída]** para editar o conjunto de dados de saída do modelo selecionado.
* Selecionar **[!UICONTROL Exibir programação]** para navegar até o [!UICONTROL Agendamentos] guia. Essa exibição contém todas as informações de agendamento associadas à consulta.
* Selecionar **[!UICONTROL Excluir consulta]** para excluir o modelo.
* Selecione o nome do modelo para navegar até o Editor de consultas onde o SQL está pré-preenchido para edição.

### Usar a API do Serviço de consulta para criar um modelo

Consulte a documentação para obter instruções sobre [como criar um modelo de consulta](../api/query-templates.md#create-a-query-template) usando a API do Serviço de consulta. Os detalhes de um template de consulta recém-criado estão contidos no corpo da resposta.

>[!NOTE]
>
>Os modelos criados usando a API também estão visíveis na guia Modelos do serviço de consulta da interface do usuário da plataforma.

## Próximas etapas

Ao ler este documento, agora você tem uma melhor compreensão de como criar modelos de consulta no Serviço de consulta. Consulte a [Visão geral da interface](./overview.md)ou a variável [Guia da API do Serviço de consulta](../api/getting-started.md) para saber mais sobre os recursos do Serviço de consulta.

Consulte a [guia de endpoint de consultas programadas](../api/scheduled-queries.md) para saber como agendar consultas usando a API ou o [Guia do Editor de consultas](./user-guide.md#scheduled-queries) para a interface do usuário.
