---
title: Exibição do Editor de Validação
description: Este guia detalha informações sobre a exibição do Editor de validação no Adobe Experience Platform Assurance.
exl-id: 09be531c-8dc3-48b8-814f-b7a06adf1da3
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 3%

---

# Visualização do Editor de validação

O Editor de validação permite gerenciar funções JavaScript de maneira rápida e fácil para validar eventos em uma sessão do Adobe Experience Platform Assurance. Cada função recebe os eventos em uma sessão do Assurance. Você pode gravar funções para validar a configuração do cliente, condições de evento, testes e casos de uso.

## Introdução ao Editor de validação

Depois [configurar o Assurance](../tutorials/implement-assurance.md), no **[!UICONTROL Início]** selecione **[!UICONTROL Editor de validação]**.

![Validation-Editor-Screen-Shot](https://user-images.githubusercontent.com/6597105/198680074-f548a646-6f2f-4a65-82fd-0f1687d869bf.png)

## Gravar uma função de validação

Esse recurso permite criar, editar ou excluir funções de validação para suas sessões do Adobe Experience Platform Assurance.

1. Selecionar **[!UICONTROL Criar uma nova validação]**.
2. Insira um **name** para identificar a validação e, em seguida, fornecer uma **categoria** e uma **descrição**.
3. Edite o código no editor para validar os eventos da sua sessão do Assurance.

Quando os testes de função estiverem concluídos, selecione **[!UICONTROL Publish]** para salvar sua validação.

### Definição de evento

| Chave | Tipo | Descrição |
| :--- | :--- | :--- |
| `uuid` | String | Identificador exclusivo universal do evento. |
| `timestamp` | Número | Carimbo de data e hora do cliente quando o evento foi enviado para o Assurance. |
| `eventNumber` | Número | Usado para solicitar quando o evento foi enviado. Essa chave é útil quando os eventos têm o mesmo carimbo de data e hora. |
| `vendor` | String | Sequência de identificação do fornecedor no formato reverso do nome de domínio (por exemplo, com.adobe.assurance). |
| `type` | String | Usado para indicar o tipo de evento. |
| `payload` | Objeto | Define os dados do evento e contém propriedades exclusivas e comuns. Algumas propriedades comuns incluem `ACPExtensionEventSource` e `ACPExtensionEventType`. |
| `annotations` | Matriz | Uma matriz de objetos de anotação. |

### Definição de anotação

| Chave | Tipo | Descrição |
| :--- | :--- | :--- |
| `uuid` | String | Identificador exclusivo universal da anotação. |
| `type` | String | Usado para indicar o tipo de anotação e geralmente é o nome do plug-in (por exemplo, analytics). |
| `payload` | Objeto | Define os dados que devem complementar o evento. Para o Adobe Analytics, é aqui que os dados de hit pós-processados estão contidos. |

### Resultados da validação

A função de validação deve retornar um objeto que contenha o seguinte:

| Chave | Tipo | Descrição |
| :--- | :--- | :--- |
| `message` | String | A mensagem de validação a ser exibida nos resultados do resumo. |
| `events` | Matriz | Uma matriz de uuids de evento a serem relatados como correspondentes ou não correspondentes. |
| `links` | Matriz | Uma matriz de `ValidationResultLink` objetos para fazer referência à documentação e a outros recursos `{( type: 'doc'|'product', url: String )}` |
| `result` | String | Este é o resultado da validação e espera-se que seja uma das cadeias de caracteres enumeradas: &quot;correspondente&quot;, &quot;não correspondente&quot;, &quot;desconhecido&quot; |

## Exibir os resultados da validação

Os resultados da função são exibidos na seção de resultados abaixo do editor de código. Se o resultado da validação for `unknown` ou `not matched` e a variável `events` matriz tem um ou mais `uuids`, os eventos serão destacados na linha do tempo com as seguintes cores:

* Verde - correspondente
* Laranja - desconhecido
* Vermelho - não correspondido

![Classificação De Tempo-Validação-Destaques-Captura De Tela](https://user-images.githubusercontent.com/6597105/198681412-93d10a5a-3212-4e85-850a-aeaf5caf0521.png)

## Solução de problemas

Você pode adicionar `console.log()` na sua função para imprimir itens no console do desenvolvedor. Como alternativa, você pode usar a propriedade message do objeto result para depurar mensagens no painel de resultados.

Se ocorrer um erro no editor de código JavaScript, um status de erro é exibido junto com o motivo.

Para saber mais sobre validações, visite o [Validações do Adobe Experience Platform Assurance](https://github.com/adobe/griffon-validation-plugins) GitHub. Lá você encontrará exemplos de validações de propriedade do Adobe. Consulte a [wiki](https://github.com/adobe/griffon-validation-plugins/wiki) para obter descrições mais detalhadas das validações.
