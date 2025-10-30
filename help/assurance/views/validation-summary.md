---
title: Visualização do Editor de validação
description: Este manual detalha informações sobre a visualização do Editor de validação no Adobe Experience Platform Assurance.
exl-id: 09be531c-8dc3-48b8-814f-b7a06adf1da3
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 93%

---

# Visualização do Editor de validação

O Editor de validação permite gerenciar funções JavaScript de maneira rápida e fácil para validar eventos em uma sessão do Adobe Experience Platform Assurance. Cada função recebe os eventos em uma sessão do Assurance. É possível criar funções para validar a configuração do cliente, condições de evento, testes e casos de uso.

## Introdução ao Editor de validação

Depois de [configurar o Assurance](../tutorials/implement-assurance.md), na exibição **[!UICONTROL Home]**, selecione **[!UICONTROL Validation Editor]**.

![Validation-Editor-Screen-Shot](https://user-images.githubusercontent.com/6597105/198680074-f548a646-6f2f-4a65-82fd-0f1687d869bf.png)

## Criação de uma função de validação

Esse recurso permite criar, editar ou excluir funções de validação para suas sessões do Adobe Experience Platform Assurance.

1. Selecione **[!UICONTROL Create a New Validation]**.
2. Insira um **nome** para identificar a validação e, em seguida, forneça uma **categoria** e uma **descrição**.
3. Edite o código no editor para validar os eventos da sua sessão do Assurance.

Após a conclusão dos testes de função, selecione **[!UICONTROL Publish]** para salvar sua validação.

### Definição de evento

| Chave | Tipo | Descrição |
| :--- | :--- | :--- |
| `uuid` | String | Identificador universal exclusivo do evento. |
| `timestamp` | Número | Carimbo de data e hora do cliente quando o evento foi enviado para o Assurance. |
| `eventNumber` | Número | Usado para ordenar quando o evento foi enviado. Essa chave é útil quando os eventos têm o mesmo carimbo de data e hora. |
| `vendor` | String | String de identificação do fornecedor no formato reverso do nome do domínio (por exemplo, com.adobe.assurance). |
| `type` | String | Usado para indicar o tipo de evento. |
| `payload` | Objeto | Define os dados do evento e contém propriedades exclusivas e comuns. Algumas propriedades comuns incluem `ACPExtensionEventSource` e `ACPExtensionEventType`. |
| `annotations` | Matriz | Uma matriz de objetos de anotação. |

### Definição de anotação

| Chave | Tipo | Descrição |
| :--- | :--- | :--- |
| `uuid` | String | Identificador universal exclusivo da anotação. |
| `type` | String | Usado para indicar o tipo de anotação. Em geral, é o nome do plug-in (por exemplo, analytics). |
| `payload` | Objeto | Define os dados que devem complementar o evento. Para o Adobe Analytics, é aqui que os dados de ocorrências pós-processados estão contidos. |

### Resultados da validação

A função de validação deve retornar um objeto que contenha o seguinte:

| Chave | Tipo | Descrição |
| :--- | :--- | :--- |
| `message` | String | A mensagem de validação a ser exibida nos resultados do resumo. |
| `events` | Matriz | Uma matriz de uuids de evento a serem relatados como correspondentes ou não correspondentes. |
| `links` | Matriz | Uma matriz de `ValidationResultLink` objetos para fazer referência à documentação e a outros recursos `{( type: 'doc'`&amp;vert;`'product', url: String )}` |
| `result` | String | Este é o resultado da validação. Espera-se que seja uma das seguintes strings enumeradas: “correspondente”, “não correspondente”, “desconhecido” |

## Visualizar os resultados da validação

Os resultados da função são exibidos na seção de resultados abaixo do editor de código. Se o resultado da validação for `unknown` ou `not matched` e a matriz `events` tiver um ou mais `uuids`, os eventos serão destacados na linha do tempo com as seguintes cores:

* Verde: correspondente
* Laranja: desconhecido
* Vermelho: não correspondente

![Timeling-Validation-Highlights-Screen-Shot](https://user-images.githubusercontent.com/6597105/198681412-93d10a5a-3212-4e85-850a-aeaf5caf0521.png)

## Solução de problemas

E possível adicionar `console.log()` na sua função para imprimir itens no Developer Console. Como alternativa, você pode usar a propriedade mensagem do objeto resultante para depurar mensagens no painel de resultados.

Se ocorrer um erro no editor de código JavaScript, um status de erro será exibido junto com o motivo.

Para saber mais sobre validações, visite o GitHub de [Validações do Adobe Experience Platform Assurance](https://github.com/adobe/griffon-validation-plugins). Lá, você encontrará exemplos de validações de propriedade da Adobe. Consulte o [wiki](https://github.com/adobe/griffon-validation-plugins/wiki) para obter descrições mais detalhadas das validações.
