---
title: Builds
description: Saiba mais sobre o conceito de builds e como eles funcionam no Adobe Experience Platform.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '787'
ht-degree: 58%

---

# Builds

>[!NOTE]
>
>A Adobe Experience Platform Launch foi reformulada como um conjunto de tecnologias de coleta de dados no Adobe Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

Uma build é o conjunto de arquivos que contém todo o código executado no dispositivo cliente.

Ele é composto pelas alterações especificadas na biblioteca, bem como por tudo o que foi enviado, aprovado ou publicado antes dela.

A build consiste em arquivos de código do lado do cliente que fazem referência um ao outro. Esses arquivos são entregues no local da hospedagem usando o ambiente e o host escolhidos para a biblioteca. O código implantado no site aponta para esse mesmo local, para que os arquivos possam carregar quando um usuário acessa seu site ou aplicativo.

## Conteúdo do arquivo

Uma biblioteca define um conjunto discreto de recursos de tags (extensões, regras e elementos de dados) que devem ser incluídos dentro dela.

Uma build contém todo o código do módulo (fornecido pelos desenvolvedores de extensão) e a configuração (inserida por você) necessária para potencializar os recursos contidos na biblioteca. Por exemplo, se uma extensão fornecer ações que não são usadas em suas regras, o código para executar essas ações não estará contido na criação.

As builds são divididas no arquivo da biblioteca principal e, possivelmente, em muitos arquivos menores. O arquivo da biblioteca principal é referido no código incorporado e carregado na página no tempo de execução. Ele contém:

* O mecanismo de regras
* Toda a configuração da extensão
* Todo o código e configuração do elemento de dados
* Todo o código e configuração do evento de regra
* Todo o código e configuração da condição
* Código e configuração de evento para quaisquer regras com biblioteca carregada ou final de página como o evento (já que sabemos que será necessário imediatamente).

Os arquivos menores contêm código e configuração para ações individuais que são carregadas na página, conforme necessário. Quando uma Regra é acionada e suas Condições são avaliadas de forma que as Ações precisem ser executadas, o código e a configuração necessários para essa ação específica são recuperados de um dos arquivos menores. Isso significa que apenas o código necessário para realizar as ações necessárias é carregado na página, tornando a biblioteca principal o menor possível.

## Formato do arquivo

O formato de arquivo padrão para builds é um pacote de arquivos que contém todo o código necessário para suas extensões, elementos de dados e regras para executar da maneira que você desejar.

No entanto, em alguns casos, você pode preferir um arquivo .zip dos arquivos, em vez do arquivo de código executável do lado do cliente. Por exemplo, pode ser necessário criar um arquivo, se hospedar sua própria build e quiser usar a build em outra implantação. Se você fornecer algo no caminho auto-hospedado para o campo da biblioteca, poderá salvar seu ambiente. Juntamente com o novo código, um link para o download arquivado ficará disponível. Depois que a biblioteca for criada, você terá a opção de implantar um arquivo zip no Akamai e baixá-lo de `assets.adobedtm.com/...`.

>[!NOTE]
>
>Nada existe nesse local, até que você faça uma build.

Independentemente do formato de arquivo, a build é sempre fornecida no local especificado pelo host.

Para concluir um build, selecione uma biblioteca e clique na opção Build disponível no nível do processo de publicação (Build para desenvolvimento, Build para preparação e assim por diante).

## Minificação

A minificação diminui os custos da largura de banda e melhora a velocidade, removendo os dados que não são necessários para a execução de um arquivo.

Para aumentar o desempenho, o Platform minifica tudo, inclusive:

* A biblioteca principal de tags
* O código do módulo fornecido pelos desenvolvedores de extensão como parte de uma extensão
* O código personalizado fornecido pelos usuários do Platform 

>[!NOTE]
>
>Se o código do módulo e o código personalizado já estiverem minificados, o Platform os minificará novamente. Essa segunda minificação não oferece benefícios adicionais, mas não causa nenhum dano e torna o Platform menos complexo e mais fácil de manter.

Qualquer código do lado do cliente fornecido aponta para a versão minificada do código. Isso é visto nos nomes de arquivos que seguem a convenção de nomenclatura padrão para arquivos minificados:

`launch-%environment_id%.min.js`

Se quiser ver o código não minificado, remova .min do nome do arquivo:

`launch-%environment_id%.js`

Se um desenvolvedor de extensão fornecer códigos minificados com sua extensão, a Platform não fornecerá código não minificado na build não minificada. Da mesma forma, se um usuário da Platform colocar código minificado em uma caixa de código personalizada, esse código ainda será minificado em builds não minificadas. A plataforma não diminui nada.

Para obter mais informações sobre a minificação, consulte [este artigo stackpath](https://blog.stackpath.com/glossary/minification/).

Ao executar uma build, ele construirá primeiro a biblioteca não minificada e depois minificará toda a biblioteca de uma só vez.
