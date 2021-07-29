---
title: Desenvolver uma extensão
description: Este documento fornece uma visão geral do processo de desenvolvimento da extensão de tag com links para documentação adicional para processos mais detalhados.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 43%

---

# Desenvolver uma extensão

>[!NOTE]
>
>A Adobe Experience Platform Launch foi reformulada como um conjunto de tecnologias de coleta de dados no Adobe Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

Uma extensão de tag deve ser considerada como um produto (pequeno) com suas próprias necessidades. Determinar como um usuário do Adobe Experience Platform desejará usar sua extensão pode ajudar você a classificar a funcionalidade em quais tipos de evento, tipos de condição, tipos de ação e tipos de elementos de dados sua extensão deve fornecer.

Com esse conhecimento, você pode planejar quais componentes devem ser fornecidos em sua extensão.

## Guias

Com um plano em vigor, esses guias podem ajudar você a entender o processo de desenvolvimento de extensão:

* O [guia de introdução](../getting-started.md) e outros documentos em **Desenvolvimento de extensão** na navegação à esquerda são um excelente material de referência para entender as extensões. Eles incluem detalhes sobre o que as extensões podem fazer, como as informações do usuário são armazenadas e transmitidas entre sua extensão e o Adobe Experience Platform, como seu código é fornecido em bibliotecas e como seu código de extensão é interpretado e usado no tempo de execução no navegador.
* O [vídeo tutorial de extensões](https://youtu.be/rxjtC9o4rl0) é um ótimo local para começar.
* A lista de reprodução do YouTube [Introdução às extensões](https://www.youtube.com/playlist?list=PLOdw8u2F8CIgynzKrPEwCPuDxzHW1WP5m) mostra o processo de criação de pacotes de extensão.
* Artigo [Entender o esquema JSON](https://spacetelescope.github.io/understanding-json-schema/index.html#).
* [JSON Lint/Validador](http://jsonlint.com/).
* [Visualizador de JSON](https://chrome.google.com/webstore/detail/json-viewer/gbmdgpbipfallnflgajpaliibnhdgobh) Extensão do Chrome para destacar e imprimir JSON e JSONP.
* Editor [jsonschema.net](https://jsonschema.net/#/editor) para ajudar a criar o esquema JSON por meio de seu objeto.
* [Validador de esquema JSON](http://www.jsonschemavalidator.net/) Um validador de esquema JSON online e interativo.

## Ferramentas

Há também várias ferramentas npm para ajudar no desenvolvimento do pacote de extensão:

* [A ](https://www.npmjs.com/package/@adobe/reactor-scaffold) Ferramenta de scaffold da extensão de tags ajuda você a criar facilmente um projeto inicial no computador local.
* [A ](https://www.npmjs.com/package/@adobe/reactor-sandbox) sandbox de extensão de tag ajuda a validar as exibições e os módulos de extensão no computador local.
* [Tag Extension ](https://www.npmjs.com/package/@adobe/reactor-packager) Packageré um utilitário de linha de comando para empacotar uma extensão de tag em um arquivo zip.
* [O ](https://www.npmjs.com/package/@adobe/reactor-uploader) Upload de extensão de tag é uma ferramenta de linha de comando interativa que ajuda você a inserir suas credenciais de conta técnica e carregar seu pacote de extensão nas tags.
* [A ](https://www.npmjs.com/package/@adobe/reactor-releaser) versão da extensão de tag é uma ferramenta de linha de comando interativa para ajudar você a liberar sua extensão para disponibilidade privada.

## Extensões de exemplo

Há extensões de exemplo no GitHub que você pode revisar ou usar como projetos iniciais:

* [Extensão de exemplo do Hello World](https://github.com/adobe/reactor-helloworld-extension)
* [Extensão de exemplo do Facebook](https://github.com/Adobe-Marketing-Cloud-Activation/extension-facebookpixel)
* [Extensão de exemplo do Typekit](https://github.com/jeffchasin/extension-typekit)
* [Extensão de exemplo do Pinterest](https://github.com/jeffchasin/extension-pinterest)

## Espaço de trabalho do Slack

Você pode solicitar acesso ao espaço de trabalho da comunidade do Slack, onde os autores de extensão podem oferecer suporte uns aos outros usando este [formulário de solicitação](http://join.launchdevelopers.chat).

**Observe**: embora existam membros do Adobe neste espaço de trabalho do Slack, ele é um recurso da comunidade não patrocinado ou moderado pelo Adobe.
