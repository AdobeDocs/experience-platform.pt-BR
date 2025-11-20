---
title: Implantação assíncrona
description: Saiba como implantar bibliotecas de tag da Adobe Experience Platform de forma assíncrona em seu site.
exl-id: ed117d3a-7370-42aa-9bc9-2a01b8e7794e
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1046'
ht-degree: 98%

---

# Implantação assíncrona {#asynchronous-deployment}

>[!CONTEXTUALHELP]
>id="platform_tags_asynchronous_deployment"
>title="Implantação assíncrona"
>abstract="Se essa opção estiver habilitada, quando esta tag de script for analisada, o navegador começará a carregar o arquivo JavaScript, mas em vez de esperar que a biblioteca seja carregada e executada, ele continuará a analisar e renderizar o restante do documento. Isso pode melhorar o desempenho da página da Web, mas tem implicações importantes sobre como determinadas regras são executadas. Consulte a documentação para obter mais detalhes."

>[!NOTE]
>
>O Adobe Experience Platform Launch foi reformulado como um conjunto de tecnologias de coleta de dados na Adobe Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

A implantação de desempenho e não de bloqueio das bibliotecas JavaScript necessárias a nossos produtos é cada vez mais importante para os usuários da Adobe Experience Cloud. Ferramentas como o [[!DNL Google PageSpeed]](https://developers.google.com/speed/pagespeed/insights/) recomendam que os usuários alterem a forma como implantam as bibliotecas da Adobe em seus sites. Este artigo explica como usar as bibliotecas JavaScript da Adobe de forma assíncrona.

## Síncrono versus assíncrono

### Implantação síncrona

Frequentemente, as bibliotecas são carregadas de forma síncrona na tag `<head>` de uma página. Por exemplo:

```markup
<script src="example.js"></script>
```

Por padrão, o navegador analisa o documento, chega a essa linha e começa a buscar o arquivo JavaScript do servidor. O navegador aguarda até que o arquivo seja retornado, então analisa e executa o arquivo JavaScript. Por fim, continua analisando o restante do documento HTML.

Se o analisador encontrar a tag `<script>` antes de renderizar o conteúdo visível, a exibição do conteúdo será adiada. Se o arquivo JavaScript que está sendo carregado não for absolutamente necessário para mostrar conteúdo aos usuários, você está exigindo desnecessariamente que seus visitantes aguardem o conteúdo. Quanto maior for a biblioteca, maior será o atraso. Por isso, as ferramentas de benchmark de desempenho do site como [!DNL Google PageSpeed] ou [!DNL Lighthouse] muitas vezes sinalizarão scripts carregados de forma síncrona.

As bibliotecas de gerenciamento de tag poderão crescer rapidamente se você tiver muitas tags para gerenciar.

### Implantação assíncrona

É possível carregar qualquer biblioteca de maneira assíncrona adicionando um atributo `async` à tag `<script>`. Por exemplo:

```markup
<script src="example.js" async></script>
```

Isso indica ao navegador que quando essa tag de script é analisada, ele deve começar a carregar o arquivo JavaScript, mas em vez de esperar que a biblioteca seja carregada e executada, ela deve continuar analisando e renderizando o restante do documento.

## Considerações para implantação assíncrona

Conforme descrito acima, em implantações síncronas, o navegador pausa a análise e renderiza a página enquanto a biblioteca de tags da Adobe Experience Platform é carregada e executada. Em implantações assíncronas, por outro lado, o navegador continua analisando e renderizando a página enquanto a biblioteca é carregada. É necessário levar em consideração a variabilidade de quando a biblioteca pode terminar o carregamento em relação à análise e à renderização da página.

Primeiramente, como a biblioteca de tags pode terminar o carregamento antes ou depois que a parte inferior da página tenha sido analisada e executada, você não deve mais chamar o `_satellite.pageBottom()` do seu código de página (o `_satellite` não estará disponível até que a biblioteca tenha sido carregada). Isso é explicado na página sobre como [Carregar o código incorporado de tag de forma assíncrona](#loading-the-tags-embed-code-asynchronously).

Em segundo lugar, a biblioteca de tags pode terminar de ser carregada antes ou depois que o evento do navegador [`DOMContentLoaded`](https://developer.mozilla.org/pt-BR/docs/Web/Events/DOMContentLoaded) (DOM Pronto) ocorra.

Devido a esses dois pontos, vale a pena demonstrar como funcionam os tipos de evento [Biblioteca carregada](../../extensions/client/core/overview.md#library-loaded-page-top), [Final da página](../../extensions/client/core/overview.md#page-bottom), [DOM Pronto](../../extensions/client/core/overview.md#page-bottom) e [Janela carregada](../../extensions/client/core/overview.md#window-loaded) da extensão principal ao carregar uma biblioteca de tags de forma assíncrona.

Se a propriedade da tag contiver as quatro seguintes regras:

* Regra A: usa o tipo de evento Biblioteca carregada
* Regra B: usa o tipo de evento final da página
* Regra C: usa o tipo de evento DOM Pronto
* Regra D: usa o tipo de evento Janela carregada

Independentemente de quando a biblioteca de tags terminar de ser carregada, haverá garantia de execução de todas as regras, na seguinte ordem:

Regra A → Regra B → Regra C → Regra D

Embora a ordem seja sempre aplicada, algumas regras poderão ser executadas imediatamente quando a biblioteca de tags terminar de ser carregada, enquanto outras poderão ser executadas posteriormente. Quando a biblioteca de tags termina o carregamento, ocorre o seguinte:

1. A regra A é executada imediatamente.
1. Se o evento do navegador `DOMContentLoaded` (DOM Pronto) já tiver ocorrido, a Regra B e a Regra C serão executadas imediatamente. Caso contrário, as Regras B e C serão executadas posteriormente quando o evento do navegador [`DOMContentLoaded`](https://developer.mozilla.org/pt-BR/docs/Web/Events/DOMContentLoaded) ocorrer.
1. Se o evento do navegador [`load`](https://developer.mozilla.org/pt-BR/docs/Web/Events/load) (janela carregada) já tiver ocorrido, a Regra D será executada imediatamente. Caso contrário, a Regra D será executada mais tarde quando o evento do navegador [`load`](https://developer.mozilla.org/pt-BR/docs/Web/Events/load) ocorrer. Observe que, se você tiver instalado a biblioteca de tags de acordo com as instruções, ela *sempre* finalizará o carregamento antes da ocorrência do evento de navegador [`load`](https://developer.mozilla.org/pt-BR/docs/Web/Events/load).

Ao aplicar esses princípios ao seu próprio site, considere o seguinte:

* **Uma regra que usa o tipo de evento da Biblioteca carregada pode ser executada antes que a camada de dados seja carregada totalmente.** Isso pode resultar nas ações da regra executadas com dados ausentes, pois os dados ainda não estavam disponíveis na página. Esses tipos de problemas podem ser mitigados ao ajustar a configuração da regra. Por exemplo, em vez de ter uma regra acionada pelo tipo de evento Biblioteca carregada, você pode usar o tipo de evento Evento personalizado ou Chamada direta acionado pelo código da página, assim que a camada de dados terminar o carregamento.
* **O tipo de evento Final da página não fornece especificamente valor quando a biblioteca é carregada de forma assíncrona.** Em vez disso, considere Biblioteca carregada, DOM Pronto, Janela carregada ou outros tipos de evento.

Caso veja algo fora de ordem, é provável que você tenha problemas com tempo para resolver. Implantações que requerem tempo preciso podem precisar usar ouvintes de eventos e o tipo de evento Evento personalizado ou Chamada direta para tornar suas implementações mais robustas e consistentes.

## Carregamento do código incorporado nas tags de forma assíncrona

As tags oferecem um botão de alternância para ativar o carregamento assíncrono ao ser criado um código incorporado quando você configura um [ambiente](../publishing/environments.md). Você também pode configurar o carregamento assíncrono sozinho:

1. Adicione um atributo assíncrono à tag `<script>` para carregar o script de maneira assíncrona.

   Para o código incorporado de tags, isso significa a alteração do seguinte:

   ```markup
   <script src="//www.yoururl.com/launch-EN1a3807879cfd4acdc492427deca6c74e.min.js"></script>
   ```

   para isto:

   ```markup
   <script src="//www.yoururl.com/launch-EN1a3807879cfd4acdc492427deca6c74e.min.js" async></script>
   ```

1. Remova qualquer código que tenha adicionado anteriormente na parte inferior da sua tag:

   ```markup
   <script type="text/javascript">_satellite.pageBottom();</script>
   ```

   Esse código informa ao Experience Platform que o analisador do navegador chegou à parte inferior da página. É possível que as tags não tenham sido carregadas e executadas antes disso. Assim, a chamada `_satellite.pageBottom()` resultará em um erro, e o tipo de evento Final da página talvez não se comporte conforme esperado.
