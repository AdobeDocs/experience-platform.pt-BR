---
title: Extensão de camada de dados da Google
description: Saiba mais sobre a extensão de tag da Camada de dados do cliente da Google no Adobe Experience Platform.
exl-id: 7990351d-8669-432b-94a9-4f9db1c2b3fe
source-git-commit: 9c608f69f6ba219f9cb4e938a77bd4838158d42c
workflow-type: tm+mt
source-wordcount: '867'
ht-degree: 13%

---

# Extensão da camada de dados do Google

A extensão Camada de dados da Google permite usar uma camada de dados da Google na implementação de tags. A extensão pode ser usada de forma independente ou simultânea com as soluções da Google e com o código aberto da Google [Biblioteca de ajuda da camada de dados](https://github.com/google/data-layer-helper).

A Biblioteca do Auxiliar fornece funcionalidade semelhante orientada por eventos ao Adobe Client Data Dayer (ACDL). Os elementos de dados, as regras e as ações da extensão da Camada de dados da Google oferecem funcionalidade semelhante àquelas no [Extensão ACDL](../client-data-layer/overview.md).

## Prazo

A versão 1.2.x é um beta atrasado que está em uso na produção.

## Instalação

Para instalar a extensão, navegue até o catálogo de extensões na interface do usuário da Coleta de dados e selecione **[!UICONTROL Camada de dados da Google]**.

Depois de instalada, a extensão cria ou acessa uma camada de dados em cada carregamento da biblioteca de Tags do Adobe Experience Platform.

## Exibição de extensão

A configuração da extensão pode ser usada para definir o nome da camada de dados consumida pela extensão. Se nenhuma camada de dados com o nome configurado estiver presente quando as Tags do Adobe Experience Platform forem carregadas, a extensão criará uma.

O padrão do nome da camada de dados é o nome padrão do Google `dataLayer`.

>[!NOTE]
>
>Não importa se o código Google ou Adobe é carregado primeiro e cria a camada de dados. Ambos os sistemas se comportam da mesma forma - crie a camada de dados se ela não estiver presente ou use a camada de dados existente.

## Eventos

>[!NOTE]
>
>A palavra _evento_ é sobrecarregada quando uma camada de dados orientada por evento é usada nas Tags do Adobe Experience Platform. _Eventos_ pode ser:
> - Eventos de Tags do Adobe Experience Platform (Biblioteca carregada e assim por diante).
> - Eventos JavaScript.
> - Dados enviados para a camada de dados com a _evento_ palavra-chave.


A extensão oferece a possibilidade de acompanhar as alterações na camada de dados.

>[!NOTE]
>
>É importante compreender o uso da variável _evento_ palavra-chave quando os dados são enviados para uma camada de dados da Google, de forma semelhante à Camada de dados do cliente do Adobe. O _evento_ A palavra-chave altera o comportamento da camada de dados do Google e, portanto, dessa extensão.\
> Leia a documentação do Google ou pesquise se não tiver certeza sobre esse ponto.

### Analisar todos os envios para a camada de dados

Se você selecionar essa opção, seu ouvinte de eventos ouvirá qualquer alteração feita na camada de dados.

### Analisar os envios excluindo eventos

Se você selecionar essa opção, o ouvinte do evento ouvirá qualquer push de dados para a camada de dados, excluindo eventos.

O exemplo de eventos de push a seguir seria rastreado pelo ouvinte:

```js
dataLayer.push({"data":"something"})
```

O exemplo de eventos de push a seguir não seria rastreado pelo ouvinte:

```js
dataLayer.push({"event":"myevent"})
dataLayer.push({"event":"myevent","data":"something"})
```

### Analisar todos os eventos

Se você selecionar essa opção, o ouvinte do evento ouvirá qualquer evento enviado para a camada de dados.

O exemplo de eventos de push a seguir seria rastreado pelo ouvinte:

```js
dataLayer.push({"event":"myevent"})
dataLayer.push({"event":"myevent","data":"something"})
```

O exemplo de evento de push a seguir não seria rastreado pelo ouvinte:

```js
dataLayer.push({"data":"something"})
```

### Acompanhamento de evento específico

No caso de você especificar um evento, o ouvinte do evento rastreia todos os eventos que correspondem a uma string específica.

Por exemplo, definir `myEvent` ao usar essa configuração faz com que o ouvinte rastreie somente o seguinte evento de push:

```js
dataLayer.push({"event":"myEvent"})
```

Um regex (ECMAScript / JavaScript) pode ser usado para corresponder a nomes de evento.

Por exemplo, definir &#39;myEvent\d&#39; rastrearia `myEvent` com um dígito (\d):

```js
dataLayer.push({"event":"myEvent1"})
dataLayer.push({"event":"myEvent2"})
```

## Ações

### Encaminhar para a camada de dados {#push-to-data-layer}

A extensão fornece duas ações para encaminhar o JSON para a camada de dados; um campo de texto livre para criar manualmente o JSON a ser enviado e, da versão 1.2.0, uma caixa de diálogo de vários campos de valor chave.

#### JSON de texto livre

A ação de texto livre possibilita o uso de elementos de dados diretamente no JSON. No editor JSON, os elementos de dados devem ser referenciados usando a notação de porcentagem. Por exemplo, `%dataElementName%`.

```json
{
    "page": {
        "url": "%url%",
        "previous_url": "%previous_url%",
        "concatenated_values": "static string %dataElement%"
    }
}
```

#### Multifield de valor-chave

A caixa de diálogo de vários campos de valor-chave mais recente é uma interface mais fácil de usar que permite que um push seja configurado sem gravar manualmente o JSON.

### Google DL Redefinir para Estado Calculado

A extensão fornece uma ação para redefinir a camada de dados. Se usada em uma regra que processa uma alteração na camada de dados do Google, a camada de dados é redefinida para o estado calculado da camada de dados no momento em que a regra foi acionada. Se a ação for usada em uma regra que não processa uma alteração de camada de dados do Google, a ação esvaziará a camada de dados.

## Elementos de dados

O elemento de dados fornecido pode ser usado durante a execução de uma regra acionada por uma alteração na camada de dados do Google (evento de push) ou em uma regra não relacionada, como Biblioteca carregada. No primeiro caso, o elemento de dados retorna um valor obtido do estado calculado no momento da alteração da camada de dados. No último caso, o estado calculado no momento da execução da regra é usado.

Um alternador de alternância permite selecionar se o elemento de dados deve retornar valores de todo o estado calculado ou apenas das informações do evento (se usado em uma regra acionada por uma alteração na camada de dados).

O elemento de dados pode retornar:

- Campo vazio: estado calculado da camada de dados.
- Campo com chave (como page.previous_url no exemplo acima): valor da chave no objeto de evento ou no estado calculado.

## Informações adicionais 

O elemento de dados e as caixas de diálogo de evento da extensão contêm informações e exemplos detalhados de uso.

Informações gerais adicionais estão na seção [LEITURA DO projeto](https://github.com/adobe/reactor-extension-googledatalayer/blob/main/README.md)
