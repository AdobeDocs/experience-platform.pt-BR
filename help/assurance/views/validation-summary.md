---
title: Exibição do Editor de Validação
description: Este guia detalha informações sobre a exibição do Editor de validação no Adobe Experience Platform Assurance.
source-git-commit: 5778d4db27d0f57281821dc8e042a31b69745514
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 3%

---


# Exibição do Editor de validação

O Editor de validação permite gerenciar de forma rápida e fácil as funções do JavaScript para validar eventos em uma sessão do Adobe Experience Platform Assurance. Cada função recebe os eventos em uma sessão de Controle. Você pode gravar funções para validar a configuração do cliente, condições de evento, testes e casos de uso.

## Introdução ao Editor de validação

Depois [configuração de garantia](../tutorials/implement-assurance.md), no **[!UICONTROL Início]** exibir, selecionar **[!UICONTROL Editor de validação]**.

![Validação-Editor-Captura de Tela](https://user-images.githubusercontent.com/6597105/198680074-f548a646-6f2f-4a65-82fd-0f1687d869bf.png)

## Escrever uma função de validação

Esse recurso permite criar, editar ou excluir funções de validação para suas sessões do Adobe Experience Platform Assurance.

1. Selecionar **[!UICONTROL Criar uma nova validação]**.
2. Insira um **name** para identificar a validação, forneça um **categoria** e **descrição**.
3. Edite o código no editor para validar os eventos da sua sessão de Controle.

Depois que os testes de função forem concluídos, selecione **[!UICONTROL Publicar]** para salvar sua validação.

### Definição de evento

| Chave | Tipo | Descrição |
| :--- | :--- | :--- |
| `uuid` | String | Identificador universal exclusivo para o evento. |
| `timestamp` | Número | Carimbo de data e hora do cliente quando o evento foi enviado para Controle. |
| `eventNumber` | Número | Usado para solicitar quando o evento foi enviado. Essa chave é útil quando os eventos têm o mesmo carimbo de data e hora. |
| `vendor` | String | Sequência de caracteres de identificação do fornecedor no formato de nome de domínio reverso (por exemplo, com.adobe.Assurance). |
| `type` | String | Usado para indicar o tipo de evento. |
| `payload` | Objeto | Define os dados do evento e contém propriedades exclusivas e comuns. Algumas propriedades comuns incluem `ACPExtensionEventSource` e `ACPExtensionEventType`. |
| `annotations` | Matriz | Uma matriz de objetos de anotação. |

### Definição de anotação

| Chave | Tipo | Descrição |
| :--- | :--- | :--- |
| `uuid` | String | Identificador universal exclusivo para a anotação. |
| `type` | String | Usado para indicar o tipo de anotação e geralmente é o nome do plug-in (por exemplo, analytics). |
| `payload` | Objeto | Define os dados que devem complementar o evento. Para o Adobe Analytics, é aqui que os dados de ocorrência pós-processados estão contidos. |

### Resultados da validação

Espera-se que a função de validação retorne um objeto que contenha o seguinte:

| Chave | Tipo | Descrição |
| :--- | :--- | :--- |
| `message` | String | A mensagem de validação a ser exibida nos resultados do resumo. |
| `events` | Matriz | Uma matriz de uuids de evento a serem relatadas como correspondidas ou não correspondidas. |
| `links` | Matriz | Uma matriz de `ValidationResultLink` objetos para fazer referência à documentação e outros recursos `{( type: 'doc'|'product', url: String )}` |
| `result` | String | Esse é o resultado da validação e deve ser uma das strings enumeradas: &quot;correspondente&quot;, &quot;não correspondido&quot;, &quot;desconhecido&quot; |

## Visualizar os resultados da validação

Os resultados da função são exibidos na seção de resultados abaixo do editor de código. Se o resultado da validação for `unknown` ou `not matched` e `events` matriz tem um ou mais `uuids`, os eventos serão destacados na linha do tempo com as seguintes cores:

* Verde - correspondente
* Laranja - desconhecido
* Vermelho - não correspondido

![Timeling-Validation-Highlights-Screen-Shot](https://user-images.githubusercontent.com/6597105/198681412-93d10a5a-3212-4e85-850a-aeaf5caf0521.png)

## Solução de problemas

Você pode adicionar `console.log()` na sua função de imprimir itens no console do desenvolvedor. Como alternativa, você pode usar a propriedade message do objeto result para depurar mensagens no painel de resultados.

Se ocorrer um erro no editor de código JavaScript, um status de erro será exibido junto com o motivo.

Para saber mais sobre validações, visite o [Validações do Adobe Experience Platform Assurance](https://github.com/adobe/griffon-validation-plugins) GitHub. Você encontrará exemplos de validações de propriedade do Adobe. Consulte a [wiki](https://github.com/adobe/griffon-validation-plugins/wiki) para obter descrições mais detalhadas de validações.
