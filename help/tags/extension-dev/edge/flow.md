---
title: Fluxo de extensão de borda
description: Saiba como os componentes de uma extensão de borda na Adobe Experience Platform interagem entre si no tempo de execução.
exl-id: 99058e22-3e14-4ec6-858e-bb1c1fafdb7c
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 78%

---

# Fluxo de extensão de borda

Em extensões de borda, cada condição, ação e tipo de elemento de dados tem uma visualização que permite aos usuários modificar as configurações e um módulo de biblioteca para agir de acordo com essas configurações definidas pelo usuário.

Como mostra o diagrama de alto nível a seguir, a visualização do tipo de ação da extensão será mostrada em um iframe no aplicativo integrado ao Adobe Experience Platform. A exibição é usada para modificar configurações que são salvas no Experience Platform. Quando a biblioteca de tempo de execução da tag for criada, tanto o módulo de biblioteca do tipo de ação da extensão quanto as configurações definidas pelo usuário serão incluídos na biblioteca de tempo de execução que é implantada no nó de borda. As configurações definidas pelo usuário do Experience Platform são inseridas no módulo de biblioteca no tempo de execução.

![diagrama do fluxo de extensão](../images/flow/edge/event-processing-flow.png)

No diagrama a seguir, é possível ver a conexão entre eventos, condições e ações no fluxo de processamento da regra.

![diagrama de fluxo de processamento de regras](../images/flow/edge/rule-processing-flow.png)

O fluxo de processamento de regras contém as seguintes fases:

1. Os métodos `settings` e `trigger` são fornecidos ao módulo da biblioteca de eventos na inicialização.
1. Quando o módulo da biblioteca de eventos determina que o evento ocorreu, o módulo da biblioteca de eventos chama `trigger`.
1. O Experience Platform passa `settings` para os módulos de biblioteca de tipo de condição de regra, nos quais as condições são avaliadas.
1. Cada tipo de condição retorna se uma condição é avaliada como verdadeira.
1. Se todas as condições forem aprovadas, as ações da regra serão executadas.
