---
title: Introdução ao desenvolvimento de extensões
description: Introdução ao desenvolvimento de suas próprias extensões de tag no Adobe Experience Platform.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 90%

---

# Introdução ao desenvolvimento de extensões

>[!NOTE]
>
>A Adobe Experience Platform Launch foi reformulada como um conjunto de tecnologias de coleta de dados no Adobe Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

Para você poder começar a trabalhar e criar extensões, vamos usar a ferramenta de andaimes de código aberto, fornecida pelos engenheiros do Adobe para criar os arquivos necessários e a estrutura de arquivos para o pacote de extensão. Assim, tudo o que você ainda precisa fazer é a parte valiosa: na verdade, criar o código.

## Pré-requisitos

* Instale o [Node.js](https://nodejs.org/pt-br/download/).

## Configuração de extensão

Crie um diretório em que seus arquivos de extensão ficarão ativos.

```shell
mkdir example && cd example
```

Este guia utiliza a ferramenta de andaime de extensão para criar a estrutura de extensão inicial para que os desenvolvedores possam começar a criar código rapidamente. Esse processo pode ser feito manualmente sem a ferramenta de andaime, se desejado.

Execute a ferramenta de andaime.

```shell
npx @adobe/reactor-scaffold
```

A ferramenta de andaime solicitará algumas opções de configuração iniciais da seguinte maneira:

* Nome de exibição: o nome visível da extensão
* Versão: a versão da extensão
* Descrição: uma breve descrição da finalidade da extensão
* Autor: o nome do autor da extensão

A ferramenta de andaime fornecerá opções para a construção da estrutura de extensão:

* [Visualização da configuração de extensão](./configuration.md): a visualização, o arquivo HTML, por meio do qual uma extensão coleta configurações globais de um usuário.
* [Tipos de evento](./web/event-types.md): define uma atividade para observação. Por exemplo, saiba quando um usuário faz a rolagem rapidamente ou quando um usuário interagiu com um elemento da página. Eventos podem ser utilizados em regras para executar ações.
* [Tipos de condição](./web/condition-types.md): os tipos de condição avaliam se algo é verdadeiro ou falso.
Por exemplo, isso pode retornar se o navegador do usuário é o Chrome, se ele está usando um iPad ou se o usuário está em um domínio específico.
* [Tipos de ação](./web/action-types.md): a ação a ser executada quando ocorrer um evento. Por exemplo, enviar um beacon de análise, mostrar uma oferta, salvar um cookie ou abrir um bate-papo de suporte.
* [Tipos de elementos de dados](./web/data-element-types.md): um tipo de elemento de dados recupera dados. Esses dados podem estar no armazenamento local, em um cookie, em um elemento DOM ou em um local personalizado.
* [Módulos compartilhados](./web/shared.md): um módulo compartilhado é um mecanismo pelo qual as extensões podem se comunicar com outras extensões.
* [Visualizações](./web/views.md): cada tipo de evento, condição, ação ou elemento de dados pode fornecer uma visualização que permite ao usuário fornecer configurações.

>[!NOTE]
>
>* As execuções subsequentes da ferramenta de andaime vão ignorar a configuração inicial.
>* É possível adicionar mais de um de cada evento, condição e ação.
>* Apenas uma visualização de configuração pode existir.

