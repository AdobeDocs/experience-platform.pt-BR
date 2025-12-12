---
title: Fluxo de extensão da Web
description: Saiba como os componentes de extensão da Web interagem entre si durante o tempo de execução na Adobe Experience Platform.
exl-id: 90a0c64c-d240-4e2c-876b-22f05d6f3f82
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 77%

---

# Fluxo de extensão da Web

Em extensões da Web, cada evento, condição, ação e tipo de elemento de dados tem uma visualização que permite aos usuários modificar as configurações e um módulo de biblioteca para agir de acordo com essas configurações definidas pelo usuário.

Como mostra o diagrama de alto nível a seguir, a visualização do tipo de evento da extensão será mostrada em um iframe no aplicativo integrado ao Adobe Experience Platform. O usuário usa a visualização para modificar as configurações, que são salvas no Experience Platform. Quando a biblioteca de tempo de execução de tag for criada, tanto o módulo da biblioteca de tipos de evento da extensão quanto as configurações definidas pelo usuário serão incluídos na biblioteca de tempo de execução. No tempo de execução, o Experience Platform injetará as configurações definidas pelo usuário no módulo da biblioteca.

![diagrama do fluxo de extensão](../images/flow/web/extension-flow.png)

No diagrama a seguir, é possível ver a conexão entre eventos, condições e ações no fluxo de processamento da regra.

![diagrama de fluxo de processamento de regras](../images/flow/web/rule-processing-flow.png)

O fluxo de processamento de regras contém as seguintes fases:

1. Os métodos `settings` e `trigger` são fornecidos ao módulo da biblioteca de eventos na inicialização.
1. Quando o módulo da biblioteca de eventos determina que o evento ocorreu, o módulo da biblioteca de eventos chama `trigger`.
1. As marcas transmitem `settings` para os módulos de biblioteca de condições de regra, nos quais as condições são avaliadas.
1. Cada módulo de biblioteca de condições retorna se uma condição é avaliada como verdadeira.
1. Se todas as condições forem aprovadas, as ações da regra serão executadas.
