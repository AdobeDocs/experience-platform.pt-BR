---
title: Extensão da camada de dados do cliente Adobe
description: Saiba mais sobre a extensão de tag da Camada de dados do cliente do Adobe na Adobe Experience Platform.
source-git-commit: 8dfb7bdc16d0654ee1d76dc5f5af50938b122d33
workflow-type: tm+mt
source-wordcount: '643'
ht-degree: 100%

---

# Extensão de camada de dados do cliente Adobe

Esta documentação fornece exemplos e práticas recomendadas de como usar a extensão de Camada de dados do cliente Adobe.

<!-- (Missing document?)
If you would like to have more details on development consideration, [please reach this page](./dev.md). -->

## Instalação

Para instalar a extensão, navegue até o catálogo de extensões na interface de usuário da Coleção de dados e selecione Camada de dados do cliente Adobe.

![Visualização da extensão ACDL no catálogo](./images/catalog.png)

<!-- (GitHub link?)
There is also the possibility to fork this project. You can download this github project, realize the change that you deem required for your specific use-case and re-upload it on your Organization as a private extension.
This installation will not be supported on our end.<br>
>[!NOTE]
>
> _Consider renaming the extension name in the extension.json file_ -->

## Exibição da extensão

Por padrão, o script ACDL cria uma nova camada de dados com o nome da variável `adobeDataLayer`. Caso você prefira, a exibição de extensão oferece a possibilidade de alterar esse nome. O nome definido será instanciado quando as tags forem carregadas.

>[!NOTE]
>
>Ao alterar o nome do objeto, o original `adobeDataLayer` ainda está sendo instanciado e, em seguida, duplicado para o novo nome de variável selecionado.

## Eventos

A extensão oferece a possibilidade de ouvir eventos na Camada de dados. Os seguintes eventos estão disponíveis:

### Analisar todas as alterações de dados

Se você selecionar essa opção, seu ouvinte de eventos ouvirá qualquer alteração feita na camada de dados.

>[!IMPORTANT]
>
>A publicação de eventos não altera a própria camada de dados.

O exemplo de eventos de push a seguir seria rastreado pelo ouvinte:

* ` adobeDataLayer.push({"data":"something"})`
* ` adobeDataLayer.push({"event":"myevent","data":"something"})`

O exemplo de evento de push a seguir não seria rastreado pelo ouvinte:

* ` adobeDataLayer.push({"event":"myevent"})`

### Ouvir todos os eventos

Se você selecionar essa opção, o ouvinte do evento ouvirá qualquer evento enviado para a camada de dados.

O exemplo de eventos de push a seguir seria rastreado pelo ouvinte:

* ` adobeDataLayer.push({"event":"myevent"})`
* ` adobeDataLayer.push({"event":"myevent","data":"something"})`

O exemplo de evento de push a seguir não seria rastreado pelo ouvinte:

* ` adobeDataLayer.push({"data":"something"}) `

### Ouvir um evento específico

No caso de você especificar um evento, o ouvinte do evento rastreia todos os eventos que correspondem a uma string específica.

Por exemplo, definir `myEvent` ao usar essa configuração faz com que o ouvinte rastreie somente o seguinte evento de push:

* `adobeDataLayer.push({"event":"myEvent"})`

Também é possível alterar o escopo do ouvinte de eventos. A seguir há um resumo das diferentes opções:

* `all`: esta é a opção padrão e acionará a regra sempre que a condição selecionada acima tiver sido atendida no passado ou for enviada no futuro. É a opção mais segura caso você esteja usando uma implementação assíncrona.
* `future`: esta opção aciona a regra somente quando novos eventos de push correspondentes à sua condição serão enviados para a Camada de dados.
* `past`: essa opção aciona a regra somente para eventos de push antigos que correspondam à sua condição. Novos eventos de push que corresponderem à sua condição serão ignorados e não acionarão mais a regra.

## Ações

As seções a seguir descrevem as ações compatíveis com a extensão.

### Redefinir camada de dados

A extensão fornece uma maneira de redefinir o comprimento da camada de dados, o que pode ajudar a manter um tamanho limitado para um aplicativo de página única (SPA).

No entanto, atualmente não há possibilidade de remover completamente as informações definidas anteriormente durante os métodos de push.

A ação **Redefinir e configurar estado calculado** copia o último estado calculado, esvazia o objeto da camada de dados e reenvia o último estado.

### Encaminhar para a camada de dados

A extensão fornece uma ação para enviar o conteúdo JSON para a própria Camada de dados. Tal ação possibilita o uso de elementos de dados diretamente no JSON. No editor de JSON, os elementos de dados devem ser referenciados usando a notação de porcentagem (por exemplo, `%dataElementName%`).

```json
{
    "page": {
        "url": "%url%",
        "previous_url": "%previous_url%",
        "concatenated_values": "static string %dataElement%"
    }
}
```

## Elementos de dados

As seções abaixo abordam os tipos exclusivos de elementos de dados fornecidos pela extensão.

### Estado calculado

O elemento de dados Estado calculado da camada de dados pode retornar um destes dois itens, dependendo de como você o configura:

* O estado completo da camada de dados: por padrão, o completo Estado calculado da camada de dados é retornado.
* Um caminho específico: é possível especificar o caminho que você deseja retornar na Camada de dados. Os caminhos são especificados usando a notação de pontos (por exemplo, `data.foo`).

### Tamanho da camada de dados

Esse elemento de dados retorna o tamanho da Camada de dados. O tamanho da Camada de dados é representado pelo número de elementos que foram enviados para esse objeto.

Dada a seguinte lista de eventos de push, esse elemento de dados retornaria o número inteiro `2`:

```js
adobeDataLayer.push({"event":"myEvent"})
adobeDataLayer.push({"data":{"foo":"bar"}})
```
