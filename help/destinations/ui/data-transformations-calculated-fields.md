---
title: Executar transformações nos dados exportados para destinos de armazenamento na nuvem usando campos calculados
type: Tutorial
description: Entenda como usar a funcionalidade de campos calculados para executar transformações nos dados exportados para destinos de armazenamento na nuvem
exl-id: 1e14f964-4c03-4d0c-be8d-c3dcb48a335a
source-git-commit: bd9efc1bcf6058827cc5c603b9976c9e42c7ec9e
workflow-type: tm+mt
source-wordcount: '1604'
ht-degree: 8%

---

# Executar transformações nos dados exportados para destinos de armazenamento na nuvem usando campos calculados {#data-transformation-calculated-fields}

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_flat_files"
>title="Adicionar campos calculados"
>abstract="<p>Use o controle **Adicionar campo calculado** para executar várias transformações de dados em dados exportados para destinos de armazenamento na nuvem. Por exemplo, é possível aplicar hash em dados, concatenar matrizes em strings e muito mais."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/data-transformations-calculated-fields.html?lang=pt-BR#examples" text="Exemplos"

>[!AVAILABILITY]
>
>A funcionalidade para executar transformações nos dados exportados para destinos de armazenamento na nuvem está geralmente disponível para os seguintes destinos: [[!DNL Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md), [[!DNL Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md), [[!DNL Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md), [[!DNL Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md), [[!DNL Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md), [[!DNL SFTP]](../../destinations/catalog/cloud-storage/sftp.md), bem como para quaisquer destinos de armazenamento na nuvem criados pelo parceiro personalizado por meio do [Destination SDK](/help/destinations/destination-sdk/overview.md).

Para executar várias transformações nos dados exportados para destinos de armazenamento na nuvem, você deve usar a funcionalidade de campos calculados na etapa de mapeamento do fluxo de trabalho de exportação. Para obter informações detalhadas sobre campos calculados, visite as páginas vinculadas abaixo. Essas páginas incluem uma introdução aos campos calculados no Preparo de dados e mais informações sobre todas as funções disponíveis:

* [Guia e visão geral da interface](/help/data-prep/ui/mapping.md#calculated-fields)
* [Funções de Preparo de dados](/help/data-prep/functions.md)

## Pré-requisitos {#prerequisites}

Para usar campos calculados para transformações de dados:

1. [Conecte](/help/destinations/ui/connect-destination.md) a um destino de armazenamento na nuvem desejado. Ao conectar ao destino de nuvem desejado, desative a **[!UICONTROL Export arrays, maps, objects]** [opção](/help/destinations/ui/export-arrays-maps-objects.md##export-arrays-maps-objects-toggle).
2. Percorra as [etapas de ativação para destinos de armazenamento na nuvem](/help/destinations/ui/activate-batch-profile-destinations.md) e vá para a etapa [mapeamento](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).

## Como trabalhar com campos calculados {#how-to-export-calculated-fields}

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_control"
>title="Habilitar esquema de saída hierárquico"
>abstract="Ative esta configuração para habilitar a exportação de matrizes, mapas e objetos para arquivos JSON ou Parquet."

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_calculated_field_disabled"
>title="Controle Adicionar campos calculados desabilitado"
>abstract="Este controle está desabilitado porque você *ativou* o botão de alternância **Exportar matrizes, mapas e objetos** ao configurar a conexão de destino. Para usar campos calculados e as funções disponíveis neles, configure uma nova conexão de destino com o botão de alternância **Exportar matrizes, mapas e objetos***desativado*."

>[!IMPORTANT]
>
>Sempre que trabalhar com campos calculados, além de qualquer função de transformação de dados aplicada, você também deve usar a função `array_to_string` para concatenar campos em uma cadeia de caracteres.

Na etapa de mapeamento do fluxo de trabalho de ativação para destinos de armazenamento na nuvem, selecione **[!UICONTROL Add calculated field]**.

>[!TIP]
>
>O controle **[!UICONTROL Add calculated field]** está desabilitado para conexões de destino nas quais o controle **[!UICONTROL Export arrays, maps, and objects]** foi desligado. [Leia mais](/help/destinations/ui/export-arrays-maps-objects.md#export-arrays-maps-objects-toggle).

![Adicionar campo calculado realçado na etapa de mapeamento do fluxo de trabalho de ativação em lote.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields.png)

Isso abre uma janela modal onde você pode selecionar funções e campos para exportar atributos do Experience Platform.

![Janela modal da funcionalidade de campo calculado com nenhuma função selecionada ainda.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields-2.png)

Por exemplo, use a função `array_to_string` no campo `organizations`, como mostrado abaixo, para exportar a matriz de organizações como uma cadeia de caracteres em um arquivo CSV. Exibir [mais informações sobre este e outros exemplos mais abaixo](#array-to-string-function-export-arrays).

![Janela modal da funcionalidade de campo calculado com a função de matriz para cadeia de caracteres selecionada.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields-3.png)

Selecione **[!UICONTROL Save]** para manter o campo calculado e retornar à etapa de mapeamento.

![Janela modal da funcionalidade de campo calculado com a função de matriz para cadeia de caracteres selecionada e o controle Salvar realçado.](/help/destinations/assets/ui/export-arrays-calculated-fields/save-calculated-field.png)

De volta à etapa de mapeamento do fluxo de trabalho, preencha o **[!UICONTROL Target field]** com um valor do cabeçalho da coluna que você deseja para este campo nos arquivos exportados.

![Etapa de mapeamento com o campo de destino realçado.](/help/destinations/assets/ui/export-arrays-calculated-fields/fill-in-target-field.png)

![Selecionar campo de destino 2](/help/destinations/assets/ui/export-arrays-calculated-fields/target-field-filled-in.png)

Quando estiver pronto, selecione **[!UICONTROL Next]** para prosseguir para a próxima etapa do fluxo de trabalho de ativação.

![Etapa de mapeamento com o campo de destino realçado e um valor de destino preenchido.](/help/destinations/assets/ui/export-arrays-calculated-fields/select-next-to-proceed.png)

## Amostras de funções compatíveis para executar transformações de dados {#supported-functions}

Todas as [funções de Preparo de Dados](/help/data-prep/functions.md) documentadas têm suporte ao ativar dados para destinos baseados em arquivo.

As funções abaixo, específicas para lidar com exportações de matrizes ou aplicar hash a campos, estão documentadas junto com exemplos.

* `array_to_string`
* `flattenArray`
* `filterArray`
* `transformArray`
* `coalesce`
* `size_of`
* `iif`
* `index-based array access`
* `add_to_array`
* `to_array`
* `first`
* `last`

## Exemplos de funções usadas para executar transformações de dados {#examples}

Consulte exemplos e informações adicionais nas seções abaixo para algumas das funções listadas acima. Para o restante das funções listadas, consulte a [documentação de funções gerais na seção Preparo de dados](/help/data-prep/functions.md).

### Função `array_to_string` para exportar matrizes {#array-to-string-function-export-arrays}

Use a função `array_to_string` para concatenar os elementos de uma matriz em uma sequência, usando um separador desejado, como `_` ou `|`. Essa função é útil quando você deseja exportar os elementos de uma matriz do Experience Platform para um arquivo CSV.

Por exemplo, você pode combinar os seguintes campos XDM abaixo, como mostrado na captura de tela de mapeamento, usando uma sintaxe `array_to_string('_',organizations)`:

* Matriz `organizations`
* Sequência de caracteres `person.name.firstName`
* Sequência de caracteres `person.name.lastName`
* Sequência de caracteres `personalEmail.address`

![Exemplo de mapeamento incluindo a função array_to_string.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-array-to-string-function.png)

Nesse caso, o arquivo de saída é semelhante ao mostrado abaixo. Observe como os elementos da matriz são concatenados em uma única string usando o caractere `_`.

```
First_Name,Last_Name,Personal_Email,Organization
John,Doe,johndoe@acme.org, "{'id':123,'orgName':'Acme Inc','founded':1990,'latestInteraction':1708041600000}_{'id':456,'orgName':'Superstar Inc','founded':2004,'latestInteraction':1692921600000}_{'id':789,'orgName':'Energy Corp','founded':2021,'latestInteraction':1725753600000}"
```

### Função `filterArray` para exportar matrizes filtradas {#filter-array}

Use a função `filterArray` para filtrar os elementos de uma matriz exportada. É possível combinar essa função com a função `array_to_string` descrita mais acima.

Continuando com o objeto de matriz `organizations` acima, você pode gravar uma função como `array_to_string('_', filterArray(organizations, org -> org.founded > 2021))`, que retorna as organizações com um valor para `founded` no ano de 2021 ou mais recente.

![Exemplo da função filterArray.](/help/destinations/assets/ui/export-arrays-calculated-fields/filter-array-function.png)

Nesse caso, o arquivo de saída é semelhante ao mostrado abaixo. Observe como os dois elementos da matriz que atendem ao critério são concatenados em uma única string usando o caractere `_`.

```
John,Doe,johndoe@acme.org, "{'id':123,'orgName':'Acme Inc','founded':1990,'latestInteraction':1708041600000}_{'id':789,'orgName':'Energy Corp','founded':2021,'latestInteraction':1725753600000}"
```

### Função `transformArray` para exportar matrizes transformadas {#transform-array}

Use a função `transformArray` para transformar os elementos de uma matriz exportada. É possível combinar essa função com a função `array_to_string` descrita mais acima.

Continuando com o objeto de matriz `organizations` acima, você pode gravar uma função como `array_to_string('_', transformArray(organizations, org -> ucase(org.orgName)))`, retornando os nomes das organizações convertidas em maiúsculas.

![Exemplo da função transformArray.](/help/destinations/assets/ui/export-arrays-calculated-fields/transform-array-function.png)

Nesse caso, o arquivo de saída é semelhante ao mostrado abaixo. Observe como os três elementos da matriz são transformados e concatenados em uma única string usando o caractere `_`.

```
John,Doe,johndoe@acme.org,ACME INC_SUPERSTAR INC_ENERGY CORP
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

Use a função `add_to_array` para adicionar elementos a uma matriz exportada. É possível combinar essa função com a função `array_to_string` descrita mais acima.

Continuando com o objeto de matriz `organizations` acima, você pode gravar uma função como `source: array_to_string('_', add_to_array(organizations,"2023"))`, retornando as organizações das quais uma pessoa é membro no ano de 2023.

![Exemplo de mapeamento incluindo a função add_to_array.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-add-to-array-function.png)

Nesse caso, o arquivo de saída é semelhante ao mostrado abaixo. Observe como os três elementos da matriz são concatenados em uma única string usando o caractere `_` e 2023 também é anexado ao final da string.

```
`First_Name,Last_Name,Personal_Email,Organization_Member_2023
John,Doe, johndoe@acme.org,"Marketing_Sales_Finance_2023"
```

### Função `flattenArray` para exportar matrizes niveladas {#flatten-array}

Use a função `flattenArray` para nivelar uma matriz multidimensional exportada. É possível combinar essa função com a função `array_to_string` descrita mais acima.

Continuando com o objeto de matriz `organizations` acima, você pode gravar uma função como `array_to_string('_', flattenArray(organizations))`. Observe que a função `array_to_string` nivela a matriz de entrada por padrão em uma cadeia de caracteres.

A saída resultante é a mesma da função `array_to_string` descrita mais acima.

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

>[!IMPORTANT]
>
>Diferentemente das outras funções descritas nesta página, para exportar elementos individuais de uma matriz, você *não precisa* usar o controle **[!UICONTROL Calculated fields]** na interface do usuário.

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

Outras funções disponíveis são específicas para exportar matrizes ou elementos de uma matriz. Você pode usar funções de hash para fazer hash de atributos nos arquivos exportados. Por exemplo, se você tiver informações de identificação pessoal nos atributos, é possível aplicar hash a esses campos ao exportá-los.

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
