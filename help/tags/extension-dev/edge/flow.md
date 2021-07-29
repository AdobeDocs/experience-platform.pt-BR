---
title: Fluxo de extensão de borda
description: Saiba como os componentes de uma extensão de borda no Adobe Experience Platform interagem entre si no tempo de execução.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 60%

---

# Fluxo de extensão de borda

>[!NOTE]
>
>A Adobe Experience Platform Launch foi reformulada como um conjunto de tecnologias de coleta de dados no Adobe Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

Em extensões de borda, cada condição, ação e tipo de elemento de dados tem uma visualização que permite aos usuários modificar as configurações e um módulo de biblioteca para agir de acordo com essas configurações definidas pelo usuário.

Como mostra o diagrama de alto nível a seguir, a visualização do tipo de ação da extensão será mostrada em um iframe no aplicativo integrado ao Adobe Experience Platform. A exibição é então usada para modificar configurações que são salvas na Plataforma. Quando a biblioteca de tempo de execução da tag é criada, tanto o módulo da biblioteca de tipo de ação da extensão quanto as configurações definidas pelo usuário serão incluídos na biblioteca de tempo de execução que é implantada no nó de borda. As configurações definidas pelo usuário da Platform são inseridas no módulo da biblioteca no tempo de execução.

![diagrama do fluxo de extensão](../images/flow/edge/event-processing-flow.png)

No diagrama a seguir, é possível ver a conexão entre eventos, condições e ações no fluxo de processamento da regra.

![diagrama de fluxo de processamento de regras](../images/flow/edge/rule-processing-flow.png)

O fluxo de processamento de regras contém as seguintes fases:

1. Os métodos `settings` e `trigger` são fornecidos ao módulo da biblioteca de eventos na inicialização.
1. Quando o módulo da biblioteca de eventos determina que o evento ocorreu, o módulo da biblioteca de eventos chama `trigger`.
1. O Platform passa o `settings` para os módulos de biblioteca de tipo de condição de regra, nos quais as condições são avaliadas.
1. Cada tipo de condição retorna se uma condição é avaliada como verdadeira.
1. Se todas as condições forem aprovadas, as ações da regra serão executadas.
