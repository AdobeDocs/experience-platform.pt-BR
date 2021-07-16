---
title: Implantação assíncrona
description: Saiba como implantar de forma assíncrona as bibliotecas de tags da Adobe Experience Platform no seu site.
source-git-commit: 5f810ada57eeb12a56de603d974a091b888dc9d2
workflow-type: tm+mt
source-wordcount: '1009'
ht-degree: 59%

---

# Implantação assíncrona

>[!NOTE]
>
>O Adobe Experience Platform Launch está sendo reformulado como um conjunto de tecnologias de coleção de dados na Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

A implantação de desempenho e não de bloqueio das bibliotecas JavaScript necessárias para nossos produtos é cada vez mais importante para os usuários da Adobe Experience Cloud. Ferramentas como [[!DNL Google PageSpeed]](https://developers.google.com/speed/pagespeed/insights/) recomendam que os usuários alterem a forma como implantam as bibliotecas do Adobe em seu site. Este artigo explica como usar as bibliotecas JavaScript do Adobe de forma assíncrona.

## Síncrono versus assíncrono

### Implantação síncrona

Frequentemente, as bibliotecas são carregadas de forma síncrona na tag `<head>` de uma página. Por exemplo:

```markup
<script src="example.js"></script>
```

Por padrão, o navegador analisa o documento, chega a essa linha e começa a buscar o arquivo JavaScript do servidor. O navegador aguarda até que o arquivo seja retornado, então analisa e executa o arquivo JavaScript. Por fim, continua analisando o restante do documento HTML.

Se o analisador encontrar a tag `<script>` antes de renderizar o conteúdo visível, a exibição do conteúdo será adiada. Se o arquivo JavaScript que está sendo carregado não for absolutamente necessário para mostrar conteúdo aos usuários, você está exigindo desnecessariamente que seus visitantes aguardem o conteúdo. Quanto maior for a biblioteca, maior será o atraso. Por isso, as ferramentas de benchmark de desempenho do site como [!DNL Google PageSpeed] ou [!DNL Lighthouse] muitas vezes sinalizarão scripts carregados de forma síncrona.

As bibliotecas do Tag Management podem crescer rapidamente se você tiver muitas tags para gerenciar.

### Implantação assíncrona

É possível carregar qualquer biblioteca de maneira assíncrona adicionando um atributo `async` à tag `<script>`. Por exemplo:

```markup
<script src="example.js" async></script>
```

Isso indica ao navegador que quando essa tag de script é analisada, ele deve começar a carregar o arquivo JavaScript, mas em vez de esperar que a biblioteca seja carregada e executada, ela deve continuar analisando e renderizando o restante do documento.

## Considerações para implantação assíncrona

Conforme descrito acima, em implantações síncronas, o navegador pausa a análise e renderiza a página, enquanto a biblioteca de tags Adobe Experience Platform é carregada e executada. Em implantações assíncronas, por outro lado, o navegador continua analisando e renderizando a página enquanto a biblioteca é carregada. A variação de quando a biblioteca de tags pode terminar o carregamento em relação à análise e renderização da página deve ser levada em consideração.

Primeiro, como a biblioteca de tags pode terminar o carregamento antes ou depois que a parte inferior da página tenha sido analisada e executada, você não deve mais chamar `_satellite.pageBottom()` do código da página (`_satellite` não estará disponível até que a biblioteca tenha carregado). Isso é explicado em [Carregamento do código incorporado das tags de forma assíncrona](#loading-the-tags-embed-code-asynchronously).

Segundo, a biblioteca de tags pode terminar o carregamento antes ou depois que o evento do navegador [`DOMContentLoaded`](https://developer.mozilla.org/pt-BR/docs/Web/Events/DOMContentLoaded) (DOM Ready) ocorrer.

Por causa desses dois pontos, vale a pena demonstrar como os tipos de evento [Biblioteca carregada](../../extensions/web/core/overview.md#library-loaded-page-top), [Parte inferior da página](../../extensions/web/core/overview.md#page-bottom), [Pronto para DOM](../../extensions/web/core/overview.md#page-bottom) e [Janela carregada](../../extensions/web/core/overview.md#window-loaded) da função de extensão principal ao carregar uma biblioteca de tags de forma assíncrona.

Se a propriedade da tag contiver as quatro regras a seguir:

* Regra A: usa o tipo de evento Biblioteca carregada
* Regra B: usa o tipo de evento final da página
* Regra C: usa o tipo de evento DOM Pronto
* Regra D: usa o tipo de evento Janela carregada

Independentemente de quando a biblioteca de tags terminar o carregamento, todas as regras serão executadas e serão executadas na seguinte ordem:

Regra A → Regra B → Regra C → Regra D

Embora a ordem seja sempre aplicada, algumas regras podem ser executadas imediatamente quando a biblioteca de tags terminar de carregar, enquanto outras podem ser executadas posteriormente. O seguinte ocorre quando a biblioteca de tags termina o carregamento:

1. A regra A é executada imediatamente.
1. Se o evento do navegador `DOMContentLoaded` (DOM Pronto) já tiver ocorrido, a Regra B e a Regra C serão executadas imediatamente. Caso contrário, as Regras B e C serão executadas posteriormente quando o evento do navegador [`DOMContentLoaded`](https://developer.mozilla.org/en-US/docs/Web/Events/DOMContentLoaded) ocorrer.
1. Se o evento do navegador [`load`](https://developer.mozilla.org/pt-BR/docs/Web/Events/load) (janela carregada) já tiver ocorrido, a Regra D será executada imediatamente. Caso contrário, a Regra D será executada mais tarde quando o evento do navegador [`load`](https://developer.mozilla.org/en-US/docs/Web/Events/load) ocorrer. Observe que, se tiver instalado a biblioteca de tags de acordo com as instruções, a biblioteca de tags *sempre* finaliza o carregamento antes que o evento do navegador [`load`](https://developer.mozilla.org/en-US/docs/Web/Events/load) ocorra.

Ao aplicar esses princípios ao seu próprio site, considere o seguinte:

* **Uma regra que usa o tipo de evento da Biblioteca carregada pode ser executada antes que a camada de dados seja carregada totalmente.** Isso pode resultar nas ações da regra executadas com dados ausentes, pois os dados ainda não estavam disponíveis na página. Esses tipos de problemas podem ser mitigados ao ajustar a configuração da regra. Por exemplo, em vez de ter uma regra acionada pelo tipo de evento Biblioteca carregada, você pode usar o tipo de evento Evento personalizado ou Chamada direta acionado pelo código da página, assim que a camada de dados terminar o carregamento.
* **O tipo de evento Final da página não fornece especificamente valor quando a biblioteca é carregada de forma assíncrona.** Em vez disso, considere Biblioteca carregada, DOM Pronto, Janela carregada ou outros tipos de evento.

Caso veja algo fora de ordem, é provável que você tenha problemas com tempo para resolver. Implantações que requerem tempo preciso podem precisar usar ouvintes de eventos e o tipo de evento Evento personalizado ou Chamada direta para tornar suas implementações mais robustas e consistentes.

## Carregamento do código incorporado das tags de forma assíncrona

As tags fornecem um botão para ativar o carregamento assíncrono ao criar um código incorporado ao configurar um [ambiente](../publishing/environments.md). Você também pode configurar o carregamento assíncrono sozinho:

1. Adicione um atributo assíncrono à tag `<script>` para carregar o script de maneira assíncrona.

   Para o código incorporado das tags, isso significa alterar isso:

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

   Esse código informa à Platform que o analisador do navegador chegou à parte inferior da página. É provável que as tags não tenham sido carregadas e executadas antes dessa hora, portanto, chamar `_satellite.pageBottom()` resulta em um erro e o tipo de evento Final da página pode não se comportar conforme esperado.
