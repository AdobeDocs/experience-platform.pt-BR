---
title: (Beta) Usar campos calculados para exportar matrizes em arquivos simples
type: Tutorial
description: Saiba como exportar matrizes e campos calculados do Real-Time CDP para destinos baseados em perfil em lote.
badge: "Beta"
source-git-commit: 79924b9a7d5114c94a004f99fb194102845b2127
workflow-type: tm+mt
source-wordcount: '1180'
ht-degree: 2%

---


# (Beta) Usar campos calculados para exportar matrizes em arquivos de esquema simples {#use-calculated-fields-to-export-arrays-in-flat-schema-files}

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_flat_files"
>title="(Beta) Suporte a arrays de exportação"
>abstract="Exporte matrizes simples de valores int, string ou booleanos do Experience Platform para o destino de armazenamento na nuvem desejado. Algumas limitações se aplicam. Consulte a documentação para obter exemplos abrangentes e as funções compatíveis."

<!--

additional links for contextualhelp:

>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-calculated-fields.html#examples" text="Examples"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-calculated-fields.html#known-limitations" text="Known limitations"

-->

>[!AVAILABILITY]
>
>* A funcionalidade para exportar matrizes por meio de campos calculados está atualmente em Beta. A documentação e a funcionalidade estão sujeitas a alterações.

Saiba como exportar matrizes por meio de campos calculados do Real-Time CDP em arquivos de esquema simples para destinos de armazenamento na nuvem. Leia este documento para entender os casos de uso ativados por essa funcionalidade.

Obtenha informações abrangentes sobre campos calculados - o que são e por que são importantes. Leia as páginas vinculadas abaixo para obter uma introdução aos campos calculados no Preparo de dados e mais informações sobre todas as funções disponíveis:

* [Guia e visão geral da interface](/help/data-prep/ui/mapping.md#calculated-fields)
* [Funções de preparação de dados](/help/data-prep/functions.md)

>[!IMPORTANT]
>
>Nem todas as funções listadas acima são suportadas *ao exportar campos para destinos de armazenamento na nuvem* usando a funcionalidade de campos calculados. Consulte a [seção funções suportadas](#supported-functions) mais abaixo para obter mais informações.

## Matrizes e outros tipos de objetos na Platform {#arrays-strings-other-objects}

No Experience Platform, é possível usar [Esquemas XDM](/help/xdm/home.md) para gerenciar diferentes tipos de campo. Anteriormente, era possível exportar campos simples de tipo de par de valor-chave, como cadeias de caracteres de Experience Platform, para os destinos desejados. Um exemplo de um campo compatível com a exportação anterior é `personalEmail.address`:`johndoe@acme.org`.

Outros tipos de campo no Experience Platform incluem campos de matriz. Leia mais sobre [gerenciamento de campos de matriz na interface do usuário do Experience Platform](/help/xdm/ui/fields/array.md). Além dos tipos de campo suportados anteriormente, agora é possível exportar objetos de matriz como: `organizations:[marketing, sales, engineering]`. Veja mais abaixo [exemplos abrangentes](#examples) Saiba como você pode usar várias funções para acessar elementos de matrizes, unir elementos de matriz em uma sequência e muito mais.

## Limitações conhecidas {#known-limitations}

Observe as seguintes limitações conhecidas da versão beta dessa funcionalidade:

* No momento, não há suporte para a exportação para arquivos JSON ou Parquet com esquemas hierárquicos. Você pode exportar matrizes somente para arquivos CSV de esquema simples, JSON e Parquet.
* Nesse momento, *você só pode exportar matrizes simples (ou matrizes de valores primitivos) para destinos de armazenamento na nuvem*. Isso significa que você pode exportar objetos de matriz que incluem valores de string, int ou booleanos. Não é possível exportar mapas ou matrizes de mapas ou objetos. A janela modal de campos calculados exibe apenas as matrizes que você pode exportar.

## Pré-requisitos {#prerequisites}

Progresso através da [etapas de ativação para destinos do cloud storage](/help/destinations/ui/activate-batch-profile-destinations.md) e acesse o [mapeamento](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) etapa.

## Como exportar campos calculados {#how-to-export-calculated-fields}

Na etapa de mapeamento do fluxo de trabalho de ativação para destinos de armazenamento na nuvem, selecione **[!UICONTROL (Beta) Adicionar campo calculado]**.

![Adicionar campo calculado à exportação](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields.png)

Essa ação abre uma janela modal onde é possível selecionar atributos que você pode usar para exportar atributos do Experience Platform.

>[!IMPORTANT]
>
>Somente alguns campos do esquema XDM estão disponíveis no **[!UICONTROL Campo]** exibição. Você pode ver valores de string e matrizes de string, int e valores booleanos. Por exemplo, a variável `segmentMembership` matriz não é exibida, pois inclui outros valores de matriz.

![Janela modal 1](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields-2.png)

Por exemplo, use o `join` na `loyaltyID` como mostrado abaixo para exportar uma matriz de IDs de fidelidade como uma string concatenada com um sublinhado em um arquivo CSV. Exibir [mais informações sobre este e outros exemplos abaixo](#join-function-export-arrays).

![Janela modal 2](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields-3.png)

Selecionar **[!UICONTROL Salvar]** para manter o campo calculado e retornar à etapa de mapeamento.

![Janela modal 3](/help/destinations/assets/ui/export-arrays-calculated-fields/save-calculated-field.png)

De volta à etapa de mapeamento do fluxo de trabalho, preencha o **[!UICONTROL Campo de destino]** com um valor do cabeçalho da coluna que você deseja para esse campo nos arquivos exportados.

![Selecionar campo de destino 1](/help/destinations/assets/ui/export-arrays-calculated-fields/fill-in-target-field.png)

![Selecionar campo de destino 2](/help/destinations/assets/ui/export-arrays-calculated-fields/target-field-filled-in.png)

Quando estiver pronto, selecione **[!UICONTROL Próxima]** para prosseguir para a próxima etapa do fluxo de trabalho de ativação.

![Selecione Avançar para continuar](/help/destinations/assets/ui/export-arrays-calculated-fields/select-next-to-proceed.png)

## Funções compatíveis {#supported-functions}

Observe que somente as seguintes funções são compatíveis com a versão beta de campos calculados e com a matriz de suporte para destinos:

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

### `join` função para exportar matrizes {#join-function-export-arrays}

Use o `join` para concatenar os elementos de uma matriz em uma string, usando um separador desejado, como `_` ou `|`.

Por exemplo, você pode combinar os seguintes campos XDM abaixo, como mostrado na captura de tela de mapeamento usando um `join('_',loyalty.loyaltyID)` sintaxe:

* `"organizations": ["Marketing","Sales,"Finance"]` matriz
* `person.name.firstName` string
* `person.name.lastName` string
* `personalEmail.address` string

![Captura de tela do mapeamento](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-join-function.png)

Nesse caso, o arquivo de saída é semelhante ao mostrado abaixo. Observe como os três elementos da matriz são concatenados em uma única string usando o `_` caractere.

```
`First_Name,Last_Name,Organization
John,Doe,"Marketing_Sales_Finance"
```

### `coalesce` função para exportar matrizes {#coalesce-function-export-arrays}

Use o `coalesce` função para acessar e exportar o primeiro elemento não nulo de uma matriz em uma cadeia de caracteres.

Por exemplo, você pode combinar os seguintes campos XDM abaixo, como mostrado na captura de tela de mapeamento usando um `coalesce(subscriptions.hasPromotion)` sintaxe para retornar o primeiro valor true de false na matriz:

* `"subscriptions.hasPromotion": [null, true, null, false, true]` matriz
* `person.name.firstName` string
* `person.name.lastName` string
* `personalEmail.address` string

![Captura de tela de mapeamento para a função de união](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-coalesce-function.png)

Nesse caso, o arquivo de saída é semelhante ao mostrado abaixo. Observe como a primeira variável não nula `true` na matriz é exportado no arquivo.

```
First_Name,Last_Name,hasPromotion
John,Doe,true
```


### `size_of` função para exportar matrizes {#sizeof-function-export-arrays}

Use o `size_of` função para indicar quantos elementos existem em uma matriz. Por exemplo, se você tiver uma `purchaseTime` objeto de matriz com vários carimbos de data e hora, você pode usar o `size_of` função para indicar quantas compras separadas foram feitas por uma pessoa.

Por exemplo, você pode combinar os seguintes campos XDM abaixo, como mostrado na captura de tela de mapeamento.

* `"purchaseTime": ["1538097126","1569633126,"1601255526","1632791526","1664327526"]` array indicando cinco tempos de compra separados pelo cliente
* `personalEmail.address` string

![Captura de tela de mapeamento para a função size_of](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-size-of-function.png)

Nesse caso, o arquivo de saída é semelhante ao mostrado abaixo. Observe como a segunda coluna indica o número de elementos na matriz, correspondente ao número de compras separadas feitas pelo cliente.

```
`Personal_Email,Times_Purchased
johndoe@acme.org,"5"
```

### Acesso ao array baseado em índice {#index-based-array-access}

Você pode acessar um índice de uma matriz para exportar um único item da matriz. Por exemplo, semelhante ao exemplo acima para o `size_of` função, se você quiser acessar e exportar apenas a primeira vez que um cliente comprar um determinado produto, será possível usar `purchaseTime[0]` para exportar o primeiro elemento do carimbo de data e hora, `purchaseTime[1]` para exportar o segundo elemento do carimbo de data e hora, `purchaseTime[2]` para exportar o terceiro elemento do carimbo de data e hora etc.

![Captura de tela de mapeamento para acessar o índice](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-index.png)

Nesse caso, o arquivo de saída tem a seguinte aparência:

```
`Personal_Email,First_Purchase
johndoe@acme.org,"1538097126"
```

### `first` e `last` funções para exportar matrizes {#first-and-last-functions-export-arrays}

Use o `first` e `last` funções para exportar o primeiro ou o último elemento em uma matriz. Por exemplo, continuar com a variável `purchaseTime` objeto de matriz com vários carimbos de data e hora dos exemplos anteriores, você pode usá-los para funções do para exportar a primeira ou a última compra feita por uma pessoa.

![Mapeamento da captura de tela para a primeira e a última funções](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-first-last-functions.png)

Nesse caso, o arquivo de saída tem a seguinte aparência:

```
`Personal_Email,First_Purchase, Last_Purchase
johndoe@acme.org,"1538097126","1664327526"
```

<!--

### `iif` function to export arrays {#iif-function-export-arrays}

Here are some examples of how you could use the `iif` function to access and export arrays and other fields: (STILL TO DO)

-->

### `md5` e `sha256` funções de hash {#hashing-functions}

Além das funções específicas para exportar matrizes ou elementos de uma matriz, você pode usar funções de hash para atributos de hash. Por exemplo, se você tiver informações de identificação pessoal nos atributos, é possível aplicar hash a esses campos ao exportá-los.

Por exemplo, é possível aplicar hash a valores de string diretamente `md5(personalEmail.address)`. Se desejar, também é possível aplicar hash a elementos individuais de campos de matriz, desta forma: `md5(purchaseTime[0])`


