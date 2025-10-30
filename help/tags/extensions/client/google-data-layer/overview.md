---
title: Extensão da camada de dados do Google
description: Saiba mais sobre a extensão de tag da Camada de dados do cliente da Google na Adobe Experience Platform.
exl-id: 7990351d-8669-432b-94a9-4f9db1c2b3fe
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '934'
ht-degree: 12%

---

# Extensão da camada de dados do Google

A extensão Camada de dados do Google permite usar uma camada de dados do Google na implementação de tags. A extensão pode ser usada de forma independente ou simultânea com as soluções da Google e com a [Biblioteca de Auxiliar de Camada de Dados](https://github.com/google/data-layer-helper) de código aberto da Google.

A Biblioteca de ajuda fornece funcionalidade semelhante orientada por eventos para a Adobe Client Data Layer (ACDL). Os elementos de dados, as regras e as ações da extensão da Camada de Dados do Google fornecem funcionalidade semelhante àqueles na [extensão ACDL](../client-data-layer/overview.md).

## Instalação

Para instalar a extensão, navegue até o catálogo de extensões na interface da Coleção de Dados e selecione **[!UICONTROL Google Data Layer]**.

Depois de instalada, a extensão cria ou acessa uma camada de dados em cada carregamento da biblioteca de tags do Adobe Experience Platform.

## Exibição de extensão

A configuração de extensão pode ser usada para definir o nome da camada de dados que a extensão consome. Se nenhuma camada de dados com o nome configurado estiver presente quando as Tags do Adobe Experience Platform forem carregadas, a extensão criará uma.

O nome padrão da camada de dados é o nome padrão do Google `dataLayer`.

>[!NOTE]
>
>Não importa se o código do Google ou do Adobe é carregado primeiro e cria a camada de dados. Ambos os sistemas se comportam da mesma forma: crie a camada de dados se ela não estiver presente ou use a camada de dados existente.

## Eventos

>[!NOTE]
>
>A palavra _evento_ é sobrecarregada quando uma camada de dados orientada por eventos é usada em marcas Adobe Experience Platform. _Eventos_ podem ser:
>
> - Eventos de tags do Adobe Experience Platform (biblioteca carregada e assim por diante).
> - Eventos do JavaScript.
> - Dados enviados para a camada de dados com a palavra-chave _event_.

A extensão oferece a possibilidade de acompanhar as alterações na camada de dados.

>[!NOTE]
>
>É importante entender o uso da palavra-chave _event_ quando os dados são enviados para uma camada de dados do Google, de forma semelhante à Camada de Dados de Clientes Adobe. A palavra-chave _event_ altera o comportamento da camada de dados do Google e, portanto, dessa extensão.\
> Leia a documentação do Google ou faça uma pesquisa se não tiver certeza sobre esse ponto.

### Tipos de evento do Google

O Google oferece suporte a dois meios de enviar eventos: o Gerenciador de Tags do Google, usando o método `push()`, e o Google Analytics 4, usando o método `gtag()`.

As versões de extensão da Camada de Dados do Google anteriores à 1.2.1 só tinham suporte para eventos criados pelo `push()`, conforme mostrado nos exemplos de código desta página.

As versões 1.2.1 e posteriores dão suporte a eventos criados com o `gtag()`.  Isso é opcional e pode ser ativado na caixa de diálogo Configuração de extensão.

Para obter mais informações sobre os eventos `push()` e `gtag()`, consulte a [documentação do Google](https://developers.google.com/analytics/devguides/collection/ga4/reference/events?client_type=gtag).  As informações também são fornecidas nas caixas de diálogo de configuração e regra da extensão.

### Analise todos os envios para a camada de dados

Se você selecionar essa opção, seu ouvinte de eventos ouvirá qualquer alteração feita na camada de dados.

### Analise os eventos de push, exceto

Se você selecionar essa opção, o ouvinte do evento ouvirá qualquer envio de dados para a camada de dados, excluindo eventos.

O exemplo de eventos de push a seguir seria rastreado pelo ouvinte:

```js
dataLayer.push({"data":"something"})
```

O exemplo de eventos de push a seguir não seria rastreado pelo ouvinte:

```js
dataLayer.push({"event":"myevent"})
dataLayer.push({"event":"myevent","data":"something"})
```

### Ouvir todos os eventos

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

### Ouvir um evento específico

No caso de você especificar um evento, o ouvinte do evento rastreia todos os eventos que correspondem a uma string específica.

Por exemplo, definir `myEvent` ao usar essa configuração faz com que o ouvinte rastreie somente o seguinte evento de push:

```js
dataLayer.push({"event":"myEvent"})
```

Um regex (ECMAScript / JavaScript) pode ser usado para corresponder nomes de eventos.

Por exemplo, definir &#39;myEvent\d&#39; rastrearia `myEvent` com um dígito (\d):

```js
dataLayer.push({"event":"myEvent1"})
dataLayer.push({"event":"myEvent2"})
```

## Ações

### Encaminhar para a camada de dados {#push-to-data-layer}

A extensão fornece duas ações para enviar JSON para a camada de dados: um campo de texto livre para criar manualmente o JSON a ser enviado e, da versão 1.2.0, uma caixa de diálogo de vários campos com valores-chave.

#### JSON de texto livre

A ação de texto livre permite usar elementos de dados diretamente no JSON. No editor de JSON, os elementos de dados devem ser referenciados usando a notação de porcentagem. Por exemplo, `%dataElementName%`.

```json
{
  "page": {
    "url": "%url%",
    "previous_url": "%previous_url%",
    "concatenated_values": "static string %dataElement%"
  }
}
```

#### Chave-Valor multicampo

A caixa de diálogo de vários campos de valor-chave mais recente é uma interface mais amigável que permite a configuração de um push sem gravar manualmente o JSON.

### Google DL Redefinido para Estado Calculado

A extensão fornece uma ação para redefinir a camada de dados. Se usada em uma regra que processa uma alteração de camada de dados do Google, a camada de dados é redefinida para o estado calculado da camada de dados no momento em que a regra foi acionada. Se a ação for usada em uma regra que não processa uma alteração na camada de dados do Google, a ação esvazia a camada de dados.

## Elementos de dados

O elemento de dados fornecido pode ser usado durante a execução de uma regra acionada por uma alteração na camada de dados do Google (evento de push) ou em uma regra não relacionada, como Biblioteca carregada. No primeiro caso, o elemento de dados retorna um valor obtido do estado calculado no momento da alteração da camada de dados. No último caso, o estado calculado no momento da execução da regra é usado.

Um switch de alternância permite selecionar se o elemento de dados deve retornar valores de todo o estado calculado ou somente de informações do evento (se usado em uma regra acionada por uma alteração de camada de dados).

O elemento de dados pode, portanto, retornar:

- Campo vazio: estado calculado da camada de dados.
- Campo com a chave (como page.previous_url no exemplo acima): valor da chave no objeto do evento ou estado calculado.

## Informações adicionais 

O elemento de dados da extensão e as caixas de diálogo do evento contêm informações de uso detalhadas e exemplos.

Informações gerais adicionais estão no [LEIAME do projeto](https://github.com/adobe/reactor-extension-googledatalayer/blob/main/README.md)
