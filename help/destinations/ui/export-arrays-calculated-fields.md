---
title: (Beta) Usar campos calculados para exportar matrizes em arquivos de esquema simples
type: Tutorial
description: Saiba como usar campos calculados para exportar matrizes em arquivos de esquema simples do Real-Time CDP para destinos de armazenamento na nuvem.
badge: Beta
exl-id: ff13d8b7-6287-4315-ba71-094e2270d039
source-git-commit: 787aaef26fab5ca3acff8303f928efa299cafa93
workflow-type: tm+mt
source-wordcount: '1477'
ht-degree: 5%

---

# (Beta) Usar campos calculados para exportar matrizes em arquivos de esquema simples {#use-calculated-fields-to-export-arrays-in-flat-schema-files}

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_flat_files"
>title="(Beta) Suporte a matrizes de exportação"
>abstract="Use o controle **Adicionar campo calculado** para exportar matrizes simples de valores int, string ou booleanos da Experience Platform para o destino desejado no armazenamento em nuvem. Algumas limitações se aplicam. Consulte a documentação para ver exemplos abrangentes e as funções compatíveis."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-calculated-fields.html?lang=pt-BR#examples" text="Exemplos"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-calculated-fields.html?lang=pt-BR#known-limitations" text="Limitações conhecidas"

>[!AVAILABILITY]
>
>* A funcionalidade para exportar matrizes por meio de campos calculados está atualmente no Beta. A documentação e a funcionalidade estão sujeitas a alterações.

Saiba como exportar matrizes por meio de campos calculados do Real-Time CDP em arquivos de esquema simples para [destinos de armazenamento na nuvem](/help/destinations/catalog/cloud-storage/overview.md). Leia este documento para entender os casos de uso ativados por essa funcionalidade.

Obtenha informações abrangentes sobre campos calculados - o que são e por que são importantes. Leia as páginas vinculadas abaixo para obter uma introdução aos campos calculados no Preparo de dados e mais informações sobre todas as funções disponíveis:

* [Guia e visão geral da interface](/help/data-prep/ui/mapping.md#calculated-fields)
* [Funções de Preparo de dados](/help/data-prep/functions.md)

<!--

>[!IMPORTANT]
>
>Not all functions listed above are supported *when exporting fields to cloud storage destinations* using the calculated fields functionality. See the [supported functions section](#supported-functions) further below for more information.

-->

## Matrizes e outros tipos de objetos na Platform {#arrays-strings-other-objects}

No Experience Platform, você pode usar [esquemas XDM](/help/xdm/home.md) para gerenciar diferentes tipos de campos. Anteriormente, era possível exportar campos simples de tipo de par de valor-chave, como cadeias de caracteres de Experience Platform, para os destinos desejados. Um exemplo de um campo com suporte para exportação anterior é `personalEmail.address`:`johndoe@acme.org`.

Outros tipos de campo no Experience Platform incluem campos de matriz. Leia mais sobre [gerenciamento de campos de matriz na interface do usuário do Experience Platform](/help/xdm/ui/fields/array.md). Além dos tipos de campo suportados anteriormente, agora é possível exportar objetos de matriz como: `organizations:[marketing, sales, engineering]`. Veja mais abaixo [exemplos extensos](#examples) de como você pode usar várias funções para acessar elementos de matrizes, unir elementos de matriz em uma cadeia de caracteres e muito mais.

## Limitações conhecidas {#known-limitations}

Observe as seguintes limitações conhecidas da versão beta dessa funcionalidade:

* No momento, não há suporte para a exportação para arquivos JSON ou Parquet com esquemas hierárquicos. Você pode exportar matrizes somente para arquivos CSV de esquema simples, JSON e Parquet.
* No momento, *você só pode exportar matrizes simples (ou matrizes de valores primitivos) para destinos de armazenamento na nuvem*. Isso significa que você pode exportar objetos de matriz que incluem valores de string, int ou booleanos. Não é possível exportar mapas ou matrizes de mapas ou objetos. A janela modal de campos calculados exibe apenas as matrizes que você pode exportar.

## Pré-requisitos {#prerequisites}

[Conecte](/help/destinations/ui/connect-destination.md) a um destino de armazenamento na nuvem desejado. Prossiga pelas [etapas de ativação para destinos de armazenamento na nuvem](/help/destinations/ui/activate-batch-profile-destinations.md) e vá para a etapa [mapeamento](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).

## Como exportar campos calculados {#how-to-export-calculated-fields}

Na etapa de mapeamento do fluxo de trabalho de ativação para destinos de armazenamento na nuvem, selecione **[!UICONTROL (Beta) Adicionar campo calculado]**.

![Adicionar campo calculado realçado na etapa de mapeamento do fluxo de trabalho de ativação em lote.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields.png)

Essa ação abre uma janela modal onde é possível selecionar atributos que você pode usar para exportar atributos do Experience Platform.

>[!IMPORTANT]
>
>Somente alguns campos do esquema XDM estão disponíveis na exibição **[!UICONTROL Campo]**. Você pode ver valores de string e matrizes de string, int e valores booleanos. Por exemplo, a matriz `segmentMembership` não é exibida, pois inclui outros valores de matriz.

![Janela modal da funcionalidade de campo calculado com nenhuma função selecionada ainda.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields-2.png)

Por exemplo, use a função `join` no campo `loyaltyID`, como mostrado abaixo, para exportar uma matriz de IDs de fidelidade como uma cadeia de caracteres concatenada com um sublinhado em um arquivo CSV. Exibir [mais informações sobre este e outros exemplos mais abaixo](#join-function-export-arrays).

![Janela modal da funcionalidade de campo calculado com a função de associação selecionada.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields-3.png)

Selecione **[!UICONTROL Salvar]** para manter o campo calculado e retornar à etapa de mapeamento.

![Janela modal da funcionalidade de campo calculado com a função de junção selecionada e o controle Salvar realçado.](/help/destinations/assets/ui/export-arrays-calculated-fields/save-calculated-field.png)

De volta à etapa de mapeamento do fluxo de trabalho, preencha o **[!UICONTROL campo de Destino]** com um valor do cabeçalho de coluna desejado para este campo nos arquivos exportados.

![Etapa de mapeamento com o campo de destino realçado.](/help/destinations/assets/ui/export-arrays-calculated-fields/fill-in-target-field.png)

![Selecionar campo de destino 2](/help/destinations/assets/ui/export-arrays-calculated-fields/target-field-filled-in.png)

Quando estiver pronto, selecione **[!UICONTROL Avançar]** para prosseguir para a próxima etapa do fluxo de trabalho de ativação.

![Etapa de mapeamento com o campo de destino realçado e um valor de destino preenchido.](/help/destinations/assets/ui/export-arrays-calculated-fields/select-next-to-proceed.png)

## Funções compatíveis {#supported-functions}

Todas as [funções de Preparo de Dados](/help/data-prep/functions.md) documentadas têm suporte ao ativar dados para destinos baseados em arquivo.

No entanto, observe que descrições abrangentes de casos de uso e informações de saída de exemplo são fornecidas atualmente apenas para as seguintes funções na versão beta de campos calculados e suporte de matriz para destinos:

* `join`
* `coalesce`
* `size_of`
* `iif`
* `index-based array access`
* `add_to_array`
* `to_array`
* `first`
* `last`
* `sha256`
* `md5`

## Exemplos de funções usadas para exportar matrizes {#examples}

Consulte exemplos e informações adicionais nas seções abaixo para algumas das funções listadas acima. Para o restante das funções listadas, consulte a [documentação de funções gerais na seção Preparo de dados](/help/data-prep/functions.md).

### Função `join` para exportar matrizes {#join-function-export-arrays}

Use a função `join` para concatenar os elementos de uma matriz em uma sequência, usando um separador desejado, como `_` ou `|`.

Por exemplo, você pode combinar os seguintes campos XDM abaixo, como mostrado na captura de tela de mapeamento, usando uma sintaxe `join('_',loyalty.loyaltyID)`:

* Matriz `"organizations": ["Marketing","Sales,"Finance"]`
* Sequência de caracteres `person.name.firstName`
* Sequência de caracteres `person.name.lastName`
* Sequência de caracteres `personalEmail.address`

![Exemplo de mapeamento incluindo a função de junção.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-join-function.png)

Nesse caso, o arquivo de saída é semelhante ao mostrado abaixo. Observe como os três elementos da matriz são concatenados em uma única string usando o caractere `_`.

```
`First_Name,Last_Name,Personal_Email,Organization
John,Doe,johndoe@acme.org, "Marketing_Sales_Finance"
```

### Função `iif` para exportar matrizes {#iif-function-export-arrays}

Use a função `iif` para exportar elementos de uma matriz sob determinadas condições. Por exemplo, ao continuar com o objeto de matriz `organizations` acima, você pode gravar uma função condicional simples como `iif(organizations[0].equals("Marketing"), "isMarketing", "isNotMarketing")`.

![Exemplo de mapeamento incluindo a função iif.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-iif-function.png)

Nesse caso, o arquivo de saída é semelhante ao mostrado abaixo. Nesse caso, o primeiro elemento do array é Marketing, então a pessoa é um membro do departamento de marketing.

```
`First_Name,Last_Name, Personal_Email, Is_Member_Of_Marketing_Dept
John,Doe, johndoe@acme.org, "isMarketing"
```

### Função `add_to_array` para exportar matrizes {#add-to-array-function-export-arrays}

Use a função `add_to_array` para adicionar elementos a uma matriz exportada. É possível combinar essa função com a função `join` descrita mais acima.

Continuando com o objeto de matriz `organizations` acima, você pode gravar uma função como `source: join('_', add_to_array(organizations,"2023"))`, retornando as organizações das quais uma pessoa é membro no ano de 2023.

![Exemplo de mapeamento incluindo a função add_to_array.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-add-to-array-function.png)

Nesse caso, o arquivo de saída é semelhante ao mostrado abaixo. Observe como os três elementos da matriz são concatenados em uma única string usando o caractere `_` e 2023 também é anexado ao final da string.

```
`First_Name,Last_Name,Personal_Email,Organization_Member_2023
John,Doe, johndoe@acme.org,"Marketing_Sales_Finance_2023"
```

### Função `coalesce` para exportar matrizes {#coalesce-function-export-arrays}

Use a função `coalesce` para acessar e exportar o primeiro elemento não nulo de uma matriz em uma cadeia de caracteres.

Por exemplo, você pode combinar os seguintes campos XDM abaixo, conforme mostrado na captura de tela de mapeamento, usando uma sintaxe `coalesce(subscriptions.hasPromotion)` para retornar o primeiro `true` de valor `false` na matriz:

* Matriz `"subscriptions.hasPromotion": [null, true, null, false, true]`
* Sequência de caracteres `person.name.firstName`
* Sequência de caracteres `person.name.lastName`
* Sequência de caracteres `personalEmail.address`

![Exemplo de mapeamento incluindo a função de união.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-coalesce-function.png)

Nesse caso, o arquivo de saída é semelhante ao mostrado abaixo. Observe como o primeiro valor `true` não nulo na matriz é exportado no arquivo.

```
First_Name,Last_Name,hasPromotion
John,Doe,true
```

### Função `size_of` para exportar matrizes {#sizeof-function-export-arrays}

Use a função `size_of` para indicar quantos elementos existem em uma matriz. Por exemplo, se você tiver um objeto de matriz `purchaseTime` com vários carimbos de data e hora, poderá usar a função `size_of` para indicar quantas compras separadas foram feitas por uma pessoa.

Por exemplo, você pode combinar os seguintes campos XDM abaixo, como mostrado na captura de tela de mapeamento.

* Matriz `"purchaseTime": ["1538097126","1569633126,"1601255526","1632791526","1664327526"]` indicando cinco compras separadas pelo cliente
* Sequência de caracteres `personalEmail.address`

![Exemplo de mapeamento incluindo a função size_of.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-size-of-function.png)

Nesse caso, o arquivo de saída é semelhante ao mostrado abaixo. Observe como a segunda coluna indica o número de elementos na matriz, correspondente ao número de compras separadas feitas pelo cliente.

```
`Personal_Email,Times_Purchased
johndoe@acme.org,"5"
```

### Acesso ao array baseado em índice {#index-based-array-access}

Você pode acessar um índice de uma matriz para exportar um único item da matriz. Por exemplo, semelhante ao exemplo acima para a função `size_of`, se você quiser acessar e exportar apenas a primeira vez que um cliente tiver comprado um determinado produto, você poderá usar `purchaseTime[0]` para exportar o primeiro elemento do carimbo de data e hora, `purchaseTime[1]` para exportar o segundo elemento do carimbo de data e hora, `purchaseTime[2]` para exportar o terceiro elemento do carimbo de data e hora e assim por diante.

![Exemplo de mapeamento mostrando como um elemento de uma matriz pode ser acessado.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-index.png)

Nesse caso, o arquivo de saída é semelhante ao mostrado abaixo, exportando a primeira vez que o cliente fez uma compra:

```
`Personal_Email,First_Purchase
johndoe@acme.org,"1538097126"
```

### `first` e `last` funções para exportar matrizes {#first-and-last-functions-export-arrays}

Use as funções `first` e `last` para exportar o primeiro ou o último elemento em uma matriz. Por exemplo, continuando com o objeto de matriz `purchaseTime` com vários carimbos de data e hora dos exemplos anteriores, você pode usá-los para funções a fim de exportar a primeira ou a última compra feita por uma pessoa.

![Exemplo de mapeamento incluindo a primeira e a última funções.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-first-last-functions.png)

Nesse caso, o arquivo de saída é semelhante ao mostrado abaixo, exportando a primeira e a última vez que o cliente fez uma compra:

```
`Personal_Email,First_Purchase, Last_Purchase
johndoe@acme.org,"1538097126","1664327526"
```

### Funções de hash {#hashing-functions}

Além das funções específicas para exportar matrizes ou elementos de uma matriz, você pode usar funções de hash para hash de atributos nos arquivos exportados. Por exemplo, se você tiver informações de identificação pessoal nos atributos, é possível aplicar hash a esses campos ao exportá-los.

Você pode hash de valores de cadeias de caracteres diretamente, por exemplo `md5(personalEmail.address)`. Se desejar, você também pode aplicar hash a elementos individuais de campos de matriz, supondo que os elementos na matriz sejam cadeias de caracteres, como esta: `md5(purchaseTime[0])`

As funções de hash compatíveis são:

| Função | Exemplo de expressão |
|---------|----------|
| `sha1` | `sha1(organizations[0])` |
| `sha256` | `sha256(organizations[0])` |
| `sha512` | `sha512(organizations[0])` |
| `hash` | `hash("crc32", organizations[0], "UTF-8")` |
| `md5` | `md5(organizations[0], "UTF-8")` |
| `crc32` | `crc32(organizations[0])` |

{style="table-layout:auto"}