---
title: Manifesto de extensão
description: Saiba como configurar um arquivo de manifesto JSON que informa ao Adobe Experience Platform como consumir corretamente sua extensão.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '2647'
ht-degree: 77%

---

# Manifesto de extensão

>[!NOTE]
>
>O Adobe Experience Platform Launch está sendo reformulado como um conjunto de tecnologias de coleção de dados na Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

No diretório base da sua extensão, você deve criar um arquivo chamado `extension.json`. Ele contém detalhes críticos da sua extensão que permitem que o Adobe Experience Platform o consuma corretamente. Alguns conteúdos são formados à maneira de [npms `package.json`](https://docs.npmjs.com/files/package.json).

Um exemplo `extension.json` pode ser encontrado na [extensão Hello World](https://github.com/adobe/reactor-helloworld-extension/blob/master/extension.json) do repositório GitHub.

Um manifesto de extensão deve consistir no seguinte:

| Propriedade | Descrição |
| --- | --- |
| `name` | O nome da sua extensão. Ele deve ser exclusivo dentre todas as outras extensões do Reator e deve estar em conformidade com as [regras de nomenclatura](#naming-rules). **Isso é usado pelas tags como um identificador e não deve ser alterado após a publicação da extensão.** |
| `platform` | A plataforma para sua extensão. O único valor aceito neste momento é `web`. |
| `version` | A versão da sua extensão. Deve seguir o formato de controle de versão [semver](http://semver.org/). É consistente com o campo de versão [npm](https://docs.npmjs.com/files/package.json#version). |
| `displayName` | O nome legível da sua extensão. Isso será exibido para os usuários da plataforma. Não é necessário mencionar &quot;tags&quot; ou &quot;Extensão&quot;; os usuários já saberão que estão visualizando uma extensão de tag. |
| `description` | A descrição da sua extensão. Isso será exibido para os usuários da plataforma. Se sua extensão permitir que os usuários implementem seu produto no site deles, descreva o que o produto faz. Não é necessário mencionar &quot;tags&quot; ou &quot;Extensão&quot;; os usuários já saberão que estão visualizando uma extensão de tag. |
| `iconPath` *(Opcional)* | O caminho relativo para o ícone que será exibido para a extensão. Ele não deve começar com uma barra. Ele deve fazer referência a um arquivo SVG com uma extensão `.svg`. O SVG deve ser quadrado e pode ser dimensionado pelo Platform. |
| `author` | O &quot;autor&quot; é um objeto que deve ser estruturado da seguinte forma: <ul><li>`name`: O nome do autor da extensão. Como alternativa, o nome da empresa pode ser usado aqui.</li><li>`url` *(Opcional)*: Um URL em que você pode saber mais sobre o autor da extensão.</li><li>`email` *(Opcional)*: O endereço de email do autor da extensão.</li></ul>Ele é consistente com as regras [npm do campo do autor](https://docs.npmjs.com/files/package.json#people-fields-author-contributors). |
| `exchangeUrl` *(Obrigatório para extensões públicas)* | O URL para a lista da sua extensão no Adobe Exchange. Deve corresponder ao padrão `https://www.adobeexchange.com/experiencecloud.details.######.html`. |
| `viewBasePath` | O caminho relativo para o subdiretório que contém todas as visualizações e recursos relacionados à visualização (HTML, JavaScript, CSS, imagens). O Platform hospedará esse diretório em um servidor da Web e carregará o conteúdo iframe dele. Este campo é obrigatório e não deve começar com uma barra. Por exemplo, se todas as visualizações estiverem contidas em `src/view/`, o valor de `viewBasePath` será `src/view/`. |
| `hostedLibFiles` *(Opcional)* | Muitos de nossos usuários preferem hospedar todos os arquivos relacionados a tags em seus próprios servidores. Isso proporciona aos usuários um nível maior de certeza em relação à disponibilidade de arquivos no tempo de execução, e eles podem verificar facilmente se há vulnerabilidades de segurança no código. Se a parte da biblioteca da sua extensão precisa carregar arquivos JavaScript no tempo de execução, é recomendável usar essa propriedade para listar esses arquivos. Os arquivos listados serão hospedados junto com a biblioteca de tempo de execução de tags. Sua extensão pode carregar os arquivos por meio de um URL recuperado usando o método [getHostedLibFileUrl](./turbine.md#get-hosted-lib-file).<br><br>Esta opção contém uma matriz com caminhos relativos de arquivos de biblioteca de terceiros que precisam ser hospedados. |
| `main` *(Opcional)* | O caminho relativo de um módulo de biblioteca que deve ser executado no tempo de execução.<br><br>Este módulo sempre será incluído na biblioteca de tempo de execução e executado. Como o módulo é sempre incluído na biblioteca de tempo de execução, recomendamos usar apenas um módulo &quot;principal&quot; quando absolutamente necessário e manter o tamanho mínimo do código.<br><br>Não é garantido que este módulo seja executado primeiro; outros módulos podem ser executados antes dele. |
| `configuration` *(Opcional)* | Isso descreve a parte da [configuração de extensão](./configuration.md) da extensão. Será necessário se você precisar que os usuários forneçam configurações globais para a extensão. Consulte o [apêndice](#config-object) para obter detalhes sobre como este campo deve ser estruturado. |
| `events` *(Opcional)* | Uma matriz de definições de tipo de [evento](./web/event-types.md). Consulte a seção do apêndice sobre [definições de tipo](#type-definitions) para obter a estrutura de cada objeto na matriz. |
| `conditions` *(Opcional)* | Uma matriz de definições de tipo de [condição](./web/condition-types.md). Consulte a seção do apêndice sobre [definições de tipo](#type-definitions) para obter a estrutura de cada objeto na matriz. |
| `actions` *(Opcional)* | Uma matriz de definições de tipo de [ação](./web/action-types.md). Consulte a seção do apêndice em [definições de tipo](#type-definitions) para obter a estrutura de cada objeto na matriz. |
| `dataElements` *(Opcional)* | Uma matriz de definições de tipo de [elemento de dados](./web/data-element-types.md). Consulte a seção do apêndice em [definições de tipo](#type-definitions) para obter a estrutura de cada objeto na matriz. |
| `sharedModules` *(Opcional)* | Uma matriz de objetos de definição de módulo compartilhado. Cada objeto de módulo compartilhado na matriz deve ser estruturado da seguinte maneira: <ul><li>`name`: o nome do módulo compartilhado. Observe que esse nome será usado ao referenciar módulos compartilhados de outras extensões, conforme descrito em [Módulos compartilhados](./web/shared.md). Esse nome nunca é exibido em nenhuma interface do usuário. Ele deve ser diferente dos nomes de outros módulos compartilhados na sua extensão e deve estar em conformidade com as [regras de nomenclatura](#naming-rules). **Isso é usado pelas tags como um identificador e não deve ser alterado após a publicação da extensão.**</li><li>`libPath`: o caminho relativo para o módulo compartilhado. Ele não deve começar com uma barra. Ele deve fazer referência a um arquivo JavaScript com uma extensão `.js`.</li></ul> |

## Apêndice

### Regras de nomenclatura {#naming-rules}

O valor de qualquer campo `name` em `extension.json` deve estar em conformidade com as seguintes regras:

* Deve ter 214 caracteres ou menos
* Não deve começar com um ponto ou um sublinhado
* Não deve conter letras maiúsculas
* Deve conter somente caracteres seguros para URL

Eles são compatíveis com as regras de [nome de pacote npm](https://docs.npmjs.com/files/package.json#name).

### Propriedades de objetos de configuração {#config-object}

O objeto de configuração deve ser estruturado da seguinte maneira:

<table>
  <thead>
    <tr>
      <th>Propriedade</th>
      <th>Descrição</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>viewPath</code></td>
      <td>O URL relativo para a visualização de configuração da extensão. Deve ser relativo a <code>viewBasePath</code> e não deve começar com uma barra. Ele deve fazer referência a um arquivo HTML com uma extensão <code>.html</code>. Os sufixos de sequência de consulta e identificador de fragmento (hashes) são aceitáveis.</td>
    </tr>
    <tr>
      <td><code>schema</code></td>
      <td>Um objeto de <a href="http://json-schema.org/">Esquema JSON</a> que descreve o formato de um objeto válido sendo salvo da visualização de configuração de extensão. Como você é o desenvolvedor da visualização de configuração, é sua responsabilidade garantir que qualquer objeto de configuração salvo corresponda a esse esquema. Esse esquema também será usado para validação quando os usuários tentarem salvar dados usando os serviços do Platform <br><br>Este é um exemplo de objeto de esquema:
<pre class="JSON language-JSON hljs">
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type": "object",
  "properties": {
    "delay": {
      "type": "number",
      "minimum": 1
    }
  },
  "required": [
    "delay"
  ],
  "additionalProperties": false
}
</pre>
      Recomendamos usar uma ferramenta como <a href="http://www.jsonschemavalidator.net/">validador de Esquema JSON</a> para testar manualmente seu esquema.</td>
    </tr>
    <tr>
      <td><code>transforms</code> <em>(Opcional)</em></td>
      <td>Uma matriz de objetos em que cada objeto representa uma transformação que deve ser executada em cada objeto de configurações correspondente quando é emitida para a biblioteca de tempo de execução. Consulte a seção <a href="#transforms">transformações</a> para obter mais informações sobre por que isso pode ser necessário e como é usado.</td>
    </tr>
  </tbody>
</table>

### Definições de tipo {#type-definitions}

Uma definição de tipo é um objeto usado para descrever um evento, uma condição, uma ação ou um tipo de elemento de dados. O objeto consiste no seguinte:

<table>
  <thead>
    <tr>
      <th>Propriedade</th>
      <th>Descrição</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>name</code></td>
      <td>O nome do tipo. Deve ser um nome exclusivo na extensão. O nome deve estar em conformidade com as <a href="#naming-rules">regras de nomenclatura</a>. <strong>Isso é usado pelas tags como um identificador e não deve ser alterado após a publicação da extensão.</strong></td>
    </tr>
    <tr>
      <td><code>displayName</code></td>
      <td>O texto que será usado para representar o tipo na interface do usuário da Coleta de dados. Deve ser legível.</td>
    </tr>
    <tr>
      <td><code>categoryName</code> <em>(Opcional)</em></td>
      <td>Quando fornecido, <code>displayName</code> será listado em <code>categoryName</code> na interface do usuário da coleta de dados. Todos os tipos com o mesmo <code>categoryName</code> serão listados na mesma categoria. Por exemplo, se sua extensão fornecesse um tipo de evento <code>keyUp</code> e um tipo de evento <code>keyDown</code> e ambos tivessem um <code>categoryName</code> de <code>Keyboard</code>, ambos os tipos de evento seriam listados na categoria Teclado enquanto o usuário selecionava na lista de tipos de evento disponíveis ao criar uma regra. O valor de <code>categoryName</code> deve ser legível.</td>
    </tr>
    <tr>
      <td><code>libPath</code></td>
      <td>O caminho relativo para o módulo de biblioteca do tipo. Ele não deve começar com uma barra. Ele deve fazer referência a um arquivo JavaScript com uma extensão <code>.js</code>.</td>
    </tr>
    <tr>
      <td><code>viewPath</code> <em>(Opcional)</em></td>
      <td>O URL relativo da visualização do tipo. Deve ser relativo a <code>viewBasePath</code> e não deve começar com uma barra. Ele deve fazer referência a um arquivo HTML com uma extensão <code>.html</code>. Sequências de consulta e identificadores de fragmento (hashes) são aceitáveis. Se o módulo de biblioteca do seu tipo não usar nenhuma configuração de um usuário, você poderá excluir essa propriedade, e o Platform exibirá um espaço reservado informando que nenhuma configuração é necessária.</td>
    </tr>
    <tr>
      <td><code>schema</code></td>
      <td>Um objeto de <a href="http://json-schema.org/">Esquema JSON</a> descrevendo o formato de um objeto de configurações válido que pode ser salvo pelo usuário. Normalmente, as configurações são configuradas e salvas por um usuário usando a interface do usuário da Coleta de dados . Nesses casos, a visualização da extensão pode tomar as etapas necessárias para validar as configurações fornecidas pelo usuário. Por outro lado, alguns usuários optam por usar APIs de tags diretamente sem a ajuda de qualquer interface do usuário. A finalidade desse esquema é permitir que o Platform valide adequadamente se os objetos de configurações salvos pelos usuários, independentemente de uma interface do usuário ser usada, estão em um formato compatível com o módulo da biblioteca que atuará sobre o objeto de configurações no tempo de execução.<br><br>Este é um exemplo de objeto de esquema:<br>
<pre class="JSON language-JSON hljs">
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type": "object",
  "properties": {
    "delay": {
      "type": "número",
      "mínimo": 1
    }
  },
  "obrigatório": [
    "delay"
  ],
  "additionalProperties": false
}
</pre>
      Recomendamos usar uma ferramenta como <a href="http://www.jsonschemavalidator.net/">validador de Esquema JSON</a> para testar manualmente seu esquema.</td>
    </tr>
    <tr>
      <td><code>transforms</code> <em>(Opcional)</em></td>
      <td>Uma matriz de objetos em que cada objeto representa uma transformação que deve ser executada em cada objeto de configurações correspondente quando é emitida para a biblioteca de tempo de execução. Consulte a seção sobre <a href="#transforms">transformações</a> para obter mais informações sobre por que isso pode ser necessário e como é usado.</td>
    </tr>
  </tbody>
</table>

### Transformações {#transforms}

Para certos casos de uso específicos, as extensões precisam que os objetos de configuração salvos de uma exibição sejam transformados pela Platform antes de serem emitidos para a biblioteca de tempo de execução da tag. Você pode solicitar que uma ou mais dessas transformações ocorram definindo a propriedade `transforms` ao definir uma definição de tipo dentro de `extension.json`. A propriedade `transforms` é uma matriz de objetos na qual cada objeto representa uma transformação que deve ocorrer.

Todas as transformações exigem um `type` e um `propertyPath`. O `type` deve ser um dos seguintes `function`, `remove` e `file` e descreve qual transformação do Platform deve ser aplicada ao objeto de configurações. O `propertyPath` é uma string delimitada por ponto que informa às tags onde encontrar a propriedade que precisa ser modificada no objeto de configurações. Este é um exemplo de objeto de configurações e alguns `propertyPath`s:

```js
{
  foo: {
    bar: "A string",
    baz: [
      "A",
      "B",
      "C"
    ]
  }
}
```

* Se você definir um `propertyPath` de `foo.bar`, transformará o valor `"A string"`.
* Se você definir um `propertyPath` de `foo.baz[]`, transformará cada valor na matriz `baz`.
* Se você definir um `propertyPath` de `foo.baz`, transformará a matriz `baz`.

Os caminhos de propriedade podem usar qualquer combinação de matriz e notação de objeto para aplicar transformações em qualquer nível do objeto de configurações.

>[!WARNING]
>
>O uso de notação de matriz no atributo `propertyPath` (por exemplo, `foo.baz[]`) ainda não é suportado na ferramenta sandbox* de extensão.

As seções abaixo descrevem as transformações disponíveis e como usá-las.

#### Transformação de função

A transformação da função permite que o código gravado pelos usuários da plataforma seja executado por um módulo de biblioteca dentro da biblioteca de tempo de execução da tag emitida.

Suponhamos que gostaríamos de fornecer um tipo de ação de &quot;script personalizado&quot;. A visualização de ação &quot;script personalizado&quot; pode fornecer uma área de texto na qual o usuário pode digitar algum código. Suponhamos que um usuário tenha inserido o seguinte código na área de texto:

`console.log('Welcome, ' + username +'. This is ZomboCom.');`

Quando o usuário salva a regra, o objeto de configurações salvo pela visualização pode ter a seguinte aparência:

```javascript
{
  foo: {
    bar: "console.log('Welcome, ' + username +'. This is ZomboCom.');"
  }
}
```

Quando uma regra que usa nossa ação é acionada na biblioteca de tempo de execução de tags, gostaríamos de executar o código do usuário e passá-lo para um nome de usuário.

No ponto em que o objeto de configurações é salvo da visualização do tipo de ação, o código do usuário é simplesmente uma sequência. Isso é bom porque pode ser serializado corretamente de e para JSON; no entanto, também é ruim porque normalmente seria emitido na biblioteca de tempo de execução de tags como uma string, em vez de uma função executável. Embora você possa tentar executar o código no módulo de biblioteca do tipo de ação usando [`eval`](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/eval) ou um [construtor de função](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Function), isso é altamente desencorajado devido a [políticas de segurança de conteúdo](https://developer.mozilla.org/pt-BR/docs/Web/HTTP/CSP) que potencialmente bloqueiam a execução.

Como solução alternativa para essa situação, usar a função transform informa à Platform para envolver o código do usuário em uma função executável quando ele é emitido na biblioteca de tempo de execução de tag. Para resolver nosso problema de exemplo, definimos a transformação na definição de tipo em `extension.json` da seguinte forma:

```json
{
  "transforms": [
    {
      "type": "function",
      "propertyPath": "foo.bar",
      "parameters": ["username"]
    }
  ]
}
```

* `type` define o tipo de transformação que deve ser aplicado ao objeto de configurações.
* `propertyPath` é uma string delimitada por período que informa ao Platform onde localizar a propriedade que precisa ser modificada dentro do objeto de configurações.
* `parameters` é uma matriz de nomes de parâmetros que devem ser incluídos na assinatura da função de encapsulamento.

Quando o objeto de configurações é emitido na biblioteca de tempo de execução de tags, ele será transformado para o seguinte:

```javascript
{
  foo: {
    bar: function(username) {
      console.log('Welcome, ' + username +'. This is ZomboCom.');
    }
  }
}
```

Seu módulo de biblioteca pode então chamar a função que contém o código do usuário e passar o argumento `username`.

#### Transformação de arquivo

A transformação de arquivo permite que o código gravado pelos usuários da plataforma seja emitido em um arquivo separado da biblioteca de tempo de execução da tag. O arquivo será hospedado junto com a biblioteca de tempo de execução de tags e poderá ser carregado conforme necessário pela sua extensão no tempo de execução.

Suponhamos que gostaríamos de fornecer um tipo de ação de &quot;script personalizado&quot;. A visualização do tipo de ação pode fornecer uma área de texto na qual o usuário pode digitar algum código. Suponhamos que um usuário tenha inserido o seguinte código na área de texto:

`console.log('This is ZomboCom.');`

Quando o usuário salva a regra, o objeto de configurações salvo pela visualização pode ter a seguinte aparência:

```js
{
  foo: {
    bar: "console.log('This is ZomboCom.');"
  }
}
```

Gostaríamos que o código do usuário fosse colocado em um arquivo separado, em vez de ser incluído dentro da biblioteca de tempo de execução de tags. Quando uma regra que usa nossa ação é acionada na biblioteca de tempo de execução de tags, gostaríamos de carregar o código do usuário ao anexar um elemento de script ao corpo do documento. Para resolver nosso problema de exemplo, definiríamos a transformação na definição do tipo de ação em `extension.json` da seguinte maneira:

```json
{
  "transforms": [
    {
      "type": "file",
      "propertyPath": "foo.bar"
    }
  ]
}
```

* `type` define o tipo de transformação que deve ser aplicado ao objeto de configurações.
* `propertyPath` é uma string delimitada por período que informa ao Platform onde localizar a propriedade que precisa ser modificada dentro do objeto de configurações.

Quando o objeto de configurações é emitido na biblioteca de tempo de execução de tags, ele será transformado para o seguinte:

```javascript
{
  foo: {
    bar: "//launch.cdn.com/path/abc.js"
  }
}
```

Nesse caso, o valor de `foo.bar` foi transformado em um URL. O URL exato será determinado no momento em que a biblioteca for criada. O arquivo sempre receberá uma extensão `.js` e será entregue usando um tipo MIME orientado por JavaScript. Podemos adicionar suporte para outros tipos MIME no futuro.

#### Remover transformação

Por padrão, todas as propriedades do objeto de configurações são emitidas na biblioteca de tempo de execução de tags. Se determinadas propriedades forem usadas apenas para a visualização de extensão, especialmente se contiverem informações confidenciais (por exemplo, (token secreto), você deve usar a transformação remove para impedir que as informações sejam emitidas para a biblioteca de tempo de execução de tag.

Vamos supor que gostaríamos de oferecer um novo tipo de ação. A visualização do tipo de ação pode fornecer uma entrada na qual o usuário pode inserir uma chave secreta que permitirá a conexão com uma API específica. Vamos supor que um usuário tenha inserido o seguinte texto na entrada:

`ABCDEFG`

Quando o usuário salva a regra, o objeto de configurações salvo pela visualização pode ter a seguinte aparência:

```js
{
  foo: {
    bar: "ABCDEFG"
  }
}
```

Gostaríamos de não incluir a propriedade `bar` dentro da biblioteca de tempo de execução da tag. Para resolver nosso problema de exemplo, definiríamos a transformação na definição do tipo de ação em `extension.json` da seguinte maneira:

```json
{
  "transforms": [
    {
      "type": "remove",
      "propertyPath": "foo.bar"
    }
  ]
}
```

* `type` define o tipo de transformação que deve ser aplicado ao objeto de configurações.
* `propertyPath` é uma string delimitada por período que informa ao Platform onde localizar a propriedade que precisa ser modificada dentro do objeto de configurações.

Quando o objeto de configurações é emitido na biblioteca de tempo de execução de tags, ele será transformado para o seguinte:

```js
{
  foo: {
  }
}
```

Nesse caso, o valor de `foo.bar` foi removido do objeto de configurações.
