---
title: Extensão da camada de dados do Google
description: Saiba mais sobre a extensão de tag da Camada de dados do cliente da Google na Adobe Experience Platform.
exl-id: 7990351d-8669-432b-94a9-4f9db1c2b3fe
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '823'
ht-degree: 6%

---

# Extensão da camada de dados do Google (Beta)

>[!IMPORTANT]
>
>No momento, essa extensão está na versão beta e não foi totalmente testada na produção.

A extensão Camada de dados da Google permite usar uma camada de dados da Google na implementação de tags. A extensão pode ser usada de forma independente ou simultânea com as soluções da Google e com o código aberto da Google [Biblioteca de ajuda da camada de dados](https://github.com/google/data-layer-helper).

A Biblioteca de ajuda fornece funcionalidade semelhante orientada por eventos para o Adobe Client Data Day (ACDL). Os elementos de dados, as regras e as ações da extensão da Camada de dados do Google fornecem funcionalidade semelhante àqueles na [Extensão ACDL](../client-data-layer/overview.md).

## Maturidade

A versão 1.0.x da extensão é beta. Essa extensão não foi totalmente testada na produção.

## Instalação

Para instalar a extensão, navegue até o catálogo de extensões na interface do usuário do Experience Platform ou na interface da Coleção de dados e selecione **Camada de dados Google**.

Depois de instalada, a extensão cria ou acessa uma camada de dados sempre que a biblioteca de tags é carregada no site.

## Exibição de extensão

Ao configurar a extensão (ao instalar a extensão ou selecionando **[!UICONTROL Configurar]** no catálogo de extensões ), você deve definir o nome da camada de dados que a extensão consome. Se nenhuma camada de dados com o nome configurado estiver presente quando a biblioteca for carregada, a extensão criará uma.

>[!NOTE]
>
>Não importa se o código Google ou Adobe é carregado primeiro e cria a camada de dados. Ambos os sistemas criarão a camada de dados, se não estiver presente, ou usarão a camada de dados existente.

Por padrão, a camada de dados usa o nome padrão do Google `dataLayer`.

## Eventos

A extensão permite acompanhar as alterações (eventos) na camada de dados. Um evento pode ser qualquer um dos seguintes:

* Eventos de tag (como uma biblioteca sendo carregada)
* Eventos JavaScript
* Os dados enviados para a camada de dados com o `event` palavra-chave.

É importante compreender a utilização do [`event` palavra-chave](https://developers.google.com/tag-platform/devguides/datalayer#use_a_data_layer_with_event_handlers) quando os dados são enviados para uma camada de dados do Google, de forma semelhante à Camada de dados do cliente Adobe. A variável `event` Essa palavra-chave altera o comportamento da camada de dados do Google e, portanto, o comportamento da extensão é atualizado de acordo.

As seções abaixo descrevem os diferentes tipos de evento que a extensão pode registrar.

### Analise todos os envios para a camada de dados

Se você selecionar essa opção, a extensão escutará qualquer alteração feita na camada de dados.

### Analise os eventos de push, exceto

Se você selecionar essa opção, a extensão escutará tudo o que estiver sendo enviado para a camada de dados, excluindo eventos.

O exemplo de evento de push a seguir seria rastreado pelo ouvinte:

```js
dataLayer.push({"data":"something"})
```

O exemplo de eventos de push a seguir não seria rastreado pelo ouvinte:

```js
dataLayer.push({"event":"myevent"})
dataLayer.push({"event":"myevent","data":"something"})
```

### Ouvir todos os eventos

Se você selecionar essa opção, a extensão ouvirá qualquer evento enviado para a camada de dados.

O exemplo de eventos de push a seguir seria rastreado pelo ouvinte:

```js
dataLayer.push({"event":"myevent"})
dataLayer.push({"event":"myevent","data":"something"})
```

O exemplo de evento de push a seguir não seria rastreado pelo ouvinte:

```js
dataLayer.push({"data":"something"})
```

### Ouvir um evento específico

Se quiser ouvir um evento específico, selecione essa opção para que o ouvinte do evento rastreie todos os eventos que correspondem a uma string específica.

Por exemplo, definir `myEvent` ao usar essa configuração faz com que o ouvinte rastreie somente o seguinte evento de push:

```js
dataLayer.push({"event":"myEvent"})
```

Você também pode usar uma sequência de regex para corresponder aos nomes dos eventos. Por exemplo, configuração `myEvent\d` rastrearia eventos que começam com `myEvent` seguido por um dígito:

```js
dataLayer.push({"event":"myEvent1"})
dataLayer.push({"event":"myEvent2"})
```

## Ações

As seções abaixo descrevem as diferentes ações que a extensão pode executar quando incluída em um [regra](../../../ui/managing-resources/rules.md).

### Encaminhar para a camada de dados {#push-to-data-layer}

Essa ação envia o conteúdo JSON para a própria camada de dados, possibilitando o uso de elementos de dados diretamente em cargas JSON. No editor de JSON fornecido, é possível fazer referência a elementos de dados usando a notação de porcentagem (por exemplo, `%dataElementName%`).

```json
{
    "page": {
        "url": "%url%",
        "previous_url": "%previous_url%",
        "concatenated_values": "static string %dataElement%"
    }
}
```

### Google DL Redefinido para Estado Calculado

>[!NOTE]
>
>Esta ação está disponível a partir da v1.0.5.

Essa ação redefine a camada de dados. Se usada em uma regra que processa uma alteração de camada de dados do Google, a camada de dados é redefinida para o estado calculado da camada de dados no momento em que a regra foi acionada. Se a ação for usada em uma regra que não processa uma alteração na camada de dados do Google, a ação esvazia a camada de dados.

## Elementos de dados

A extensão fornece um elemento de dados exclusivo que acessa a camada de dados usando uma chave (por exemplo, `page.url` no [trecho acima](#push-to-data-layer)).

O elemento de dados pode fornecer qualquer um dos seguintes itens:

* Um valor específico da camada de dados (por exemplo, `page.url`)
* Toda a matriz da camada de dados (campo de chave vazio)
* Valores de um evento de camada de dados usando a chave (se a variável `event` palavra-chave foi usada)
* O objeto de evento inteiro (campo de chave vazio)

A extensão sempre dá prioridade às informações do evento. Se uma camada de dados `event` estiver sendo processado, os valores serão sempre lidos nesse evento. Se um `event` não estiver presente, os valores serão lidos diretamente na camada de dados.

## Informações adicionais 

Informações adicionais estão disponíveis no [LEIAME do projeto](https://github.com/adobe/reactor-extension-googledatalayer/blob/main/README.md) e nas caixas de diálogo do elemento de dados e do evento da extensão.
