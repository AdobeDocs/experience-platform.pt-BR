---
title: Desenvolver uma extensão
description: Este documento fornece uma visão geral do processo de desenvolvimento da extensão de tag, com links para documentações adicionais com processos mais detalhados.
exl-id: fb2f7275-a5da-4a41-b915-822c71c02e5c
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 91%

---

# Desenvolver uma extensão

Uma extensão de tag deve ser considerada como um produto (pequeno) com requisitos próprios. Determinar como um usuário do Adobe Experience Platform desejará usar sua extensão pode ajudar você a classificar a funcionalidade em quais tipos de evento, tipos de condição, tipos de ação e tipos de elementos de dados sua extensão deve fornecer.

Com esse conhecimento, é possível planejar quais componentes devem ser fornecidos em sua extensão.

## Guias

Com um plano em vigor, esses guias podem ajudar você a entender o processo de desenvolvimento de extensão:

* O [guia de introdução](../getting-started.md) e outros documentos em **Desenvolvimento de extensão** no painel esquerdo são excelentes materiais de referência para entender as extensões. Eles incluem detalhes sobre as funcionalidades das extensões, como as informações do usuário são armazenadas e transmitidas entre sua extensão e a Adobe Experience Platform, como seu código é incorporado a bibliotecas e como seu código de extensão é interpretado e usado no tempo de execução no navegador.
* Artigo [Entender o esquema JSON](https://spacetelescope.github.io/understanding-json-schema/index.html#).
* [JSON Lint/Validator](https://jsonlint.com/).
* [Visualizador de JSON](https://chrome.google.com/webstore/detail/json-viewer/gbmdgpbipfallnflgajpaliibnhdgobh) Extensão do Chrome para destacar e imprimir JSON e JSONP.
* Editor [jsonschema.net](https://jsonschema.net/#/editor) para ajudar a criar o esquema JSON por meio de seu objeto.
* [Validador de esquema JSON](https://www.jsonschemavalidator.net) Um validador de esquema JSON online e interativo.

## Ferramentas

Há também várias ferramentas npm para ajudar no desenvolvimento do pacote de extensão:

* A [Ferramenta de scaffold para extensões de tag](https://www.npmjs.com/package/@adobe/reactor-scaffold) ajuda você a criar facilmente um projeto inicial em seu computador local.
* A [Sandbox para extensões de tag](https://www.npmjs.com/package/@adobe/reactor-sandbox) ajuda você a validar exibições e módulos de extensão em seu computador local.
* O [Criador de pacotes para extensões de tag](https://www.npmjs.com/package/@adobe/reactor-packager) é um utilitário de linha de comando para compactar uma extensão de tag em um arquivo zip.
* O [Carregador para extensões de tag](https://www.npmjs.com/package/@adobe/reactor-uploader) é uma ferramenta interativa de linha de comando que ajuda você a inserir suas credenciais de conta técnica e carregar o pacote de extensão para as tags.
* O [Liberador para extensões de tag](https://www.npmjs.com/package/@adobe/reactor-releaser) é uma ferramenta interativa de linha de comando que ajuda você a liberar sua extensão para disponibilidade privada.

## Extensões de exemplo

Você pode revisar ou usar extensões de exemplo do GitHub, como a [extensão de exemplo Hello World](https://github.com/adobe/reactor-helloworld-extension), como projetos iniciais.

## Espaço de trabalho do Slack

Você pode solicitar acesso ao espaço de trabalho da comunidade do Slack, em que os autores de extensões podem oferecer suporte uns aos outros usando este [formulário de solicitação](https://docs.google.com/forms/d/e/1FAIpQLScq1m63YkDrRpvPLhzUqtfoleWiDDTTXZsSivIXRfFdlSMzpQ/viewform).

**Observação**: embora existam membros da Adobe neste espaço de trabalho do Slack, ele é um recurso de comunidade que não é patrocinado ou moderado pela Adobe.
