---
title: Elementos de dados
description: Os elementos de dados são os blocos fundamentais do seu dicionário de dados (ou mapa de dados). Use elementos de dados para coletar, organizar e entregar dados em toda a tecnologia de marketing e anúncios.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '1637'
ht-degree: 79%

---

# Elementos de dados

>[!NOTE]
>
>O Adobe Experience Platform Launch está sendo reformulado como um conjunto de tecnologias de coleção de dados na Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

Os elementos de dados são os blocos fundamentais do seu dicionário de dados (ou mapa de dados). Use elementos de dados para coletar, organizar e entregar dados em toda a tecnologia de marketing e anúncios.

Um único elemento de dados é uma variável cujo valor pode ser mapeado para consultar strings, URLs, valores de cookie, variáveis JavaScript e assim por diante. Você pode fazer referência a esse valor pelo nome da variável em todo o Adobe Experience Platform. Esta coleção de elementos de dados se torna o dicionário de dados definidos que você pode usar para criar suas regras (eventos, condições e ações). Esse dicionário de dados é compartilhado entre tags para uso com qualquer extensão adicionada à propriedade.

>[!IMPORTANT]
>
>As alterações não entrarão em vigor até serem [publicadas](../publishing/overview.md).

Use elementos de dados o mais amplamente possível em todo o processo de criação de regras, para consolidar a definição de dados dinâmicos e aumentar a eficiência do seu processo de marcação. Você define as regras de dados uma vez e as usa em vários lugares.

O conceito de elementos de dados reutilizáveis é muito eficaz, e você deve usá-lo como prática recomendada.

Por exemplo, se houver um modo específico pelo qual você faz referência a nomes de páginas, IDs de produtos ou captura informações de parâmetros de cadeias de caracteres de consulta de um link de marketing afiliado ou de [!DNL AdWords], e assim por diante, é possível criar um dicionário de dados (elementos de dados) obtendo informações da fonte e usando esses dados em várias regras de tags.

Usando o nome de página como exemplo, suponhamos que você use um esquema de nome de página específico referenciando uma camada de dados, elemento `document.title`, ou uma tag de título dentro do site. Tags no Adobe Experience Platform permitem criar um elemento de dados como um único ponto de referência para esse ponto de dados específico. Pode-se, então, usar esse elemento de dados em qualquer regra que precise fazer referência ao nome da página. Se futuramente, por algum motivo, você decidir mudar o modo como faz referência ao nome da página (por exemplo, se estiver fazendo referência a `document.title` e, a partir de determinado momento quiser referir uma camada de dados específica), não precisará editar muitas e diferentes regras para alterar essa referência. Bastará alterá-la uma vez no elemento de dados, e todas as regras que fizeram referência a esse elemento serão automaticamente atualizadas.

>[!NOTE]
>
>Se um elemento de dados não estiver referido em uma regra, não será carregado na página até que seja chamado especificamente no script personalizado.

Os elementos de dados são preenchidos com dados quando usados em regras ou chamados manualmente em um script. Em um alto nível, você:

1. [Crie um elemento de dados](#create-a-data-element), se ainda não o fez.
1. Use o elemento de dados em uma [regra](./rules.md) ou um script personalizado.

Para assistir a um vídeo de introdução, consulte [Elementos de dados](../../quick-start/videos.md).

## Uso do elemento de dados

### Nas regras

É possível usar elementos de dados na interface de edição de regras usando a caixa de pesquisa para localizar o nome do elemento de dados.

### No script personalizado

Você pode usar elementos de dados em scripts personalizados usando a `_satellite` sintaxe de objeto:

`_satellite.getVar('data element name');`

## Criar um elemento de dados {#create-a-data-element}

Os elementos de dados são os blocos de construção das regras. Os elementos de dados permitem criar um dicionário de dados (ou mapa de dados) dos itens usados comumente em uma página, independentemente da sua origem (cadeias de caracteres de consulta, URLs ou valores de cookie) para qualquer objeto contido no seu site.

1. Em uma página Propriedade, abra a guia [!UICONTROL Elementos de dados] e selecione **[!UICONTROL Criar novo elemento de dados]**.
1. Nomeie o elemento de dados.
1. Selecione uma extensão e um tipo.

   Os tipos de elementos de dados disponíveis são determinados pela extensão. Para obter informações sobre os tipos disponíveis com a extensão da tag principal, consulte [Tipos de elementos de dados](data-elements.md#types-of-data-elements).

1. Forneça quaisquer informações solicitadas sobre o tipo escolhido nos campos fornecidos.
1. (Opcional) Insira um valor padrão.

   Se você não selecionar essa opção, não haverá valor padrão. A maioria dos usuários deixa essa opção no estado padrão. Sistemas diferentes lidam com uma variável vazia de forma diferente. Algumas pessoas escolhem inserir algo como &quot;nenhum&quot; ou &quot;n/a&quot; para que possam criar consistência no relatórios quando o elemento de dados não retornar um valor.

1. Selecione se deseja forçar um valor em minúsculas e se deseja remover quebras de linha e espaços.
1. Selecione uma duração.

   As opções disponíveis são:

   * None
      * O valor não está armazenado.
   * Page view
      * O valor é mantido em uma variável JavaScript até que a página seja atualizada ou que uma nova página seja carregada.
      * Pode ser criada e definida nos scripts usando a sintaxe do objeto `_satellite`:

         `_satellite.setVar('data_element_name')`
   * Session
      * Os valores persistem no armazenamento de sessão do navegador até que a guia do navegador seja fechada.
      * Disponível durante toda a visita ao site.
   * Visitor
      * O valor é armazenado indefinidamente no armazenamento local do navegador.

1. Selecione **[!UICONTROL Salvar]**.

Ao criar ou editar elementos, você pode salvar e construir sua [biblioteca ativa](../publishing/libraries.md#active-library). Isso salva imediatamente sua alteração na biblioteca e executa uma build. O status da build será exibido. Você também pode criar uma nova biblioteca na lista suspensa [!UICONTROL Biblioteca ativa].

## Tipos de elementos de dados {#types-of-data-elements}

Os tipos de elementos de dados são determinados pela extensão. Não há limite para os tipos que podem ser criados.

As seções a seguir descrevem os tipos de elementos de dados disponíveis na extensão principal. Outras extensões usam outros tipos de elementos de dados.

### Cookie

Todo cookie de domínio disponível pode ser referido no campo campo de nome do cookie.

#### Exemplo:

`cookieName`

### Custom code

JavaScript personalizado pode ser inserido na interface selecionando [!UICONTROL Abrir editor] e inserindo o código na janela do editor.

É preciso haver uma instrução de retorno na janela do editor indicando que o valor deve ser definido como aquele valor do elemento de dados. Se uma declaração de retorno não for incluída, o elemento de dados será resolvido como `undefined`. O fallback será acionado para procurar um valor armazenado e, em seguida, um valor padrão se nenhum valor armazenado estiver presente.

**Exemplo:**

```text
var pageType = $('div.page-wrapper').attr('class').split('')[1];
if (window.location.pathname == '/') {
  return 'homepage';
} else {
  return pageType;
}
```

O código personalizado pode aceitar o `event` objeto da regra de chamada como argumento. Isso permite que o código leia o valor lá.

**Exemplo:**

```text
// `event` is the default object provided by the rule
var eventType = event.$type;
return eventType; // if this data element is called from a "DOM Ready" event, then `core.dom-ready` is returned
```

Você pode usá-los nos scripts personalizados usando a `_satellite` sintaxe do objeto:

`_satellite.getVar('data element name', event);`

Ao usar a notação `%..%`, você só precisa especificar o nome do elemento de dados. Você não precisa especificar `event`.

`%data element name%`

### Atributo DOM

Todo valor de elemento pode ser recuperado, como uma tag div ou H1.

#### Exemplo:

Corrente do seletor de CSS:

`id#dc logo img`

Obtenha o valor de:

`src`

### variável JavaScript

Todo objeto ou variável disponíveis do JavaScript pode ser referido usando o campo de caminho.

Se você quiser coletar variáveis do JavaScript ou propriedades de objeto na marcação e usá-las com qualquer uma das extensões ou regras, os elementos de dados poderão ser usados para capturar esses valores. Dessa forma, você pode consultar o elemento de dados em suas regras. Além disso, se a fonte de dados mudar, será necessário alterar apenas sua referência à fonte (o elemento de dados) em um local da interface do usuário da coleta de dados.

Por exemplo, considere que a marcação contém uma variável de JavaScript chamada `Page_Name`, assim:

```markup
<script>
  //data layer
  var Page_Name = "Homepage"
</script>
```

Você deve fornecer o caminho para essa variável ao criar o elemento de dados.

Se você utilizar um objeto coletor de dados como parte da camada de dados, utilize a notação de pontos no Caminho para fazer referência ao objeto e propriedade que você deseja capturar no elemento de dados, como `_myData.pageName` ou `digitalData.pageName` etc.

#### Exemplo:

`window.document.title`

### Armazenamento local

Forneça o nome do item de armazenamento local no campo [!UICONTROL Nome do item de armazenamento local].

O armazenamento local fornece aos navegadores uma maneira de armazenar informações de página a página ([https://www.w3schools.com/html/html5_webstorage.asp](https://www.w3schools.com/html/html5_webstorage.asp)). O armazenamento local funciona muito como cookies, mas é muito maior e mais flexível.

Use o campo fornecido para especificar o valor criado para um item de armazenamento local, como `lastProductViewed.`

### Informações da página

Use esses pontos de dados para coletar informações de página para uso na lógica da regra ou para enviar informações para o [!DNL Analytics] ou sistemas de rastreamento externos.

Você pode selecionar um dos atributos de página a seguir para ser usado em seu elemento de dados:

* URL
* Hostname
* Pathname
* Protocolo
* Referenciador
* Title

### Query string Parameter

Especifique um único parâmetro de URL no campo [!UICONTROL Parâmetro de URL].

Somente a seção de nome é necessária e qualquer designador especial como “?” ou &quot;=&quot; deve ser omitido.

#### Exemplo:

`contentType`

### Número aleatório

Use esse elemento de dados para gerar um número aleatório. É usado frequentemente para amostra de dados ou para a criação de IDs, como uma ID de ocorrência. O número aleatório também pode ser usado para ofuscar ou eliminar dados confidenciais. Alguns exemplos podem incluir:

* Gerar uma ID de ocorrência
* Concatene o número para um token de usuário ou carimbo de data e hora para garantir exclusividade
* Executar um hash unidirecional em dados PII
* Decida aleatoriamente quando mostrar uma solicitação de pesquisa no site

Especifique os valores mínimos e máximos para o número aleatório.

**Padrões:**

Mínimo: 0

Máximo: 1000000000

### Armazenamento de sessão

Forneça o nome do item de armazenamento de sessão no campo [!UICONTROL Nome do item de armazenamento da sessão].

O armazenamento de sessão é semelhante ao armazenamento local, a diferença é que os dados são descartados depois que a sessão é encerrada, enquanto o armazenamento local ou um cookie pode reter os dados.

### Visitor behavior

Semelhante às Informações da página, esse elemento de dados usa tipos de comportamento comuns para enriquecer a lógica dentro de regras ou outras soluções da plataforma.

Selecione um dos seguintes atributos de comportamento do visitante:

* Landing page
* Traffic source
* Minutes on site
* Session count
* Session page view count
* Lifetime page view count
* Is new visitor

Alguns casos de uso comuns incluem:

* Mostrar uma pesquisa depois que um visitante estiver no site por cinco minutos
* Se esta for a página de aterrissagem da visita, preencha uma métrica [!DNL Analytics]
* Mostrar uma nova oferta ao visitante depois do número X de Contagens de sessão
* Exibir um cadastro de informativo se for um visitante novo

## Elementos de dados incorporados

Você deve criar um elemento de dados personalizado na interface do usuário da coleta de dados se tiver usado anteriormente um dos seguintes elementos de dados:

* URI
* Protocolo
* Hostname
