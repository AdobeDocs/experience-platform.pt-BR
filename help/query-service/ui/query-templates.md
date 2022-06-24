---
title: Modelos de Consulta
description: Os modelos de consulta são consultas SQL salvas reutilizáveis que podem ser reutilizadas por outros usuários para economizar tempo e esforço. Eles podem ser criados usando o Editor de consultas ou a API do serviço de consultas e estão disponíveis para uso em todos os conjuntos de dados do Experience Platform.
source-git-commit: 5ed822ec16e8e8d38e93370440242ec4c1c01320
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 1%

---

# Modelos de Consulta

O Adobe Experience Platform Query Service permite salvar e reutilizar o código SQL na forma de templates de query. Os modelos poupam esforço ao evitar a repetição de tarefas comumente realizadas. Você pode compartilhar modelos em sua organização e alterar facilmente os valores de query sem precisar acessar ou entender o SQL subjacente.

Este documento fornece as informações necessárias para criar modelos de consulta no Serviço de Consulta.

## Pré-requisitos

Você deve ter o [!UICONTROL Gerenciar consultas] permissão habilitada para acessar o Editor de consultas e exibir o painel de consultas na interface do usuário da plataforma. A permissão é ativada por meio do Adobe [Admin Console](https://adminconsole.adobe.com/). Entre em contato com o administrador da organização se você não tiver privilégios de administrador para habilitar essa permissão. Consulte a documentação de controle de acesso para [instruções completas sobre como adicionar permissões por meio do Admin Console](../../access-control/home.md).

## Criar um modelo de consulta

Você pode criar templates de query por meio de dois métodos, fazendo uma solicitação de POST para a API do Serviço de query `query-templates` endpoint ou gravando, nomeando e salvando uma consulta por meio do Editor de consultas.

### Usar o Editor de consultas para criar e salvar uma consulta como modelo

Consulte a documentação para obter instruções sobre como usar o Editor de consultas para [gravação](./user-guide.md#query-authoring) e [salvar consultas](./user-guide.md#saving-queries). Depois de nomear e salvar seu query, ele estará disponível para ser reutilizado como um template de consulta a partir do [!UICONTROL Procurar] guia .

No espaço de trabalho Consultas da interface do usuário da plataforma, selecione **[!UICONTROL Procurar]** para exibir a lista de consultas salvas disponíveis.

![A área de trabalho de consultas com a guia Procurar foi realçada.](../images/ui/query-templates/query-templates.png)

Para encontrar informações relevantes do modelo, selecione qualquer modelo de consulta na lista disponível para abrir o painel de detalhes.

![O painel de detalhes no espaço de trabalho de consultas com a ID de consulta realçada.](../images/ui/query-templates/details-panel.png)

### Usar a API do Serviço de query para criar um modelo

Consulte a documentação para obter instruções sobre [como fazer um template de query](../api/query-templates.md#create-a-query-template) usando a API do Serviço de query. Os detalhes de um template de query recém-criado estão contidos no corpo da resposta.

>[!NOTE]
>
>Os modelos criados usando a API também estão visíveis na guia Navegação do serviço de consulta da interface do usuário da plataforma.

## Próximas etapas

Ao ler este documento, agora você tem uma melhor compreensão de como criar templates de query no Serviço de query. Consulte a [Visão geral da interface do usuário](./overview.md)ou o [Guia da API do Serviço de query](../api/getting-started.md) para saber mais sobre os recursos do Serviço de query.

Consulte a [guia do endpoint de consultas agendadas](../api/scheduled-queries.md) para saber como agendar consultas usando a API ou o [Guia do Editor de consultas](./user-guide.md#scheduled-queries) para a interface do usuário do .
