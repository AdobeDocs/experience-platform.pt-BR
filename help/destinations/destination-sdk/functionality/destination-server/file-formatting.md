---
description: Saiba como configurar as opções de formatação de arquivo para destinos com base em arquivo criados com o Adobe Experience Platform Destination SDK, por meio do terminal `/destination-servers`.
title: Configuração de formatação de arquivo
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 4%

---


# Configuração de formatação de arquivo

O Destination SDK suporta um conjunto flexível de recursos que você pode configurar de acordo com suas necessidades de integração. Entre esses recursos, há o suporte para [!DNL CSV] formatação de arquivo.

Ao criar destinos com base em arquivos por meio do Destination SDK, é possível definir como os arquivos CSV exportados devem ser formatados. É possível personalizar muitas opções de formatação, como, por exemplo, mas não se limitando a:

* Se o arquivo CSV deve incluir um cabeçalho;
* Qual caractere usar para citar valores?
* Como devem ser os valores vazios.

Dependendo da configuração de destino, os usuários verão determinadas opções na interface do usuário ao se conectarem a um destino baseado em arquivo. Você pode ver a aparência dessas opções no [opções de formatação de arquivo para destinos com base em arquivo](../../../ui/batch-destinations-file-formatting-options.md) documentação.


As configurações de formatação de arquivos fazem parte da configuração do servidor de destino para destinos com base em arquivos.

Para entender onde esse componente se encaixa em uma integração criada com o Destination SDK, consulte o diagrama no [opções de configuração](../configuration-options.md) ou consulte o guia sobre como [use o Destination SDK para configurar um destino baseado em arquivo](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration).

É possível configurar as opções de formatação de arquivo por meio da variável `/authoring/destination-servers` endpoint . Consulte as páginas de referência da API a seguir para obter exemplos detalhados de chamadas de API, onde é possível configurar os componentes mostrados nesta página.

* [Criar uma configuração de servidor de destino](../../authoring-api/destination-server/create-destination-server.md)
* [Atualizar uma configuração de servidor de destino](../../authoring-api/destination-server/update-destination-server.md)

Esta página descreve todas as configurações de formatação de arquivo suportadas para exportação `CSV` arquivos.

>[!IMPORTANT]
>
>Todos os nomes de parâmetros e valores suportados pelo Destination SDK são **distinção entre maiúsculas e minúsculas**. Para evitar erros de diferenciação entre maiúsculas e minúsculas, use os nomes e valores dos parâmetros exatamente como mostrado na documentação.

## Tipos de integração compatíveis {#supported-integration-types}

Consulte a tabela abaixo para obter detalhes sobre quais tipos de integrações oferecem suporte à funcionalidade descrita nesta página.

| Tipo de integração | Oferece suporte à funcionalidade |
|---|---|
| Integrações em tempo real (streaming) | Não |
| Integrações baseadas em arquivo (em lote) | Sim |

## Parâmetros compatíveis {#supported-parameters}

Você pode modificar várias propriedades dos arquivos exportados para corresponder aos requisitos do sistema de recepção de arquivos do seu destino, a fim de ler e interpretar de maneira ideal os arquivos recebidos do Experience Platform.

>[!NOTE]
>
>As opções CSV só são compatíveis ao exportar arquivos CSV. O `fileConfigurations` não é obrigatória ao configurar um novo servidor de destino. Se você não passar nenhum valor na chamada da API para as opções CSV, os valores padrão da variável [quadro de referência mais abaixo](#file-formatting-reference-and-example) será usada.


## Opções de CSV nas quais os usuários não podem selecionar opções de configuração {#file-configuration-templating-none}

No exemplo de configuração abaixo, todas as opções de CSV são predefinidas. As configurações de exportação definidas em cada uma das `csvOptions` os parâmetros são finais e os usuários não podem modificá-los.

```json
"fileConfigurations": {
        "compression": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.compression}}"
        },
        "fileType": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.fileType}}"
        },
        "csvOptions": {
            "quote": {
                "templatingStrategy": "NONE",
                "value": "\""
            },
            "quoteAll": {
                "templatingStrategy": "NONE",
                "value": "false"
            },
            "escape": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "escapeQuotes": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "header": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreLeadingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreTrailingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "nullValue": {
                "templatingStrategy": "NONE",
                "value": ""
            },
            "dateFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd"
            },
            "timestampFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd'T':mm:ss[.SSS][XXX]"
            },
            "charToEscapeQuoteEscaping": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "emptyValue": {
                "templatingStrategy": "NONE",
                "value": ""
            }
        },
        "maxFileRowCount":5000000
    }
```

## Opções de CSV nas quais os usuários podem selecionar opções de configuração {#file-configuration-templating-pebble}

No exemplo de configuração abaixo, nenhuma das opções de CSV é predefinida. O `value` em cada uma das `csvOptions` é configurado em um campo de dados do cliente correspondente por meio da variável `/destinations` endpoint (por exemplo [`customerData.quote`](../../functionality/destination-configuration/customer-data-fields.md#conditional-options) para `quote` opção de formatação de arquivo) e os usuários podem usar a interface do usuário do Experience Platform para selecionar entre as várias opções configuradas no campo de dados do cliente correspondente. Você pode ver a aparência dessas opções no [opções de formatação de arquivo para destinos com base em arquivo](../../../ui/batch-destinations-file-formatting-options.md) documentação.

```json
{
   "fileConfigurations":{
      "compression":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{% if customerData contains 'compression' and customerData.compression is not empty %}{{customerData.compression}}{% else %}NONE{% endif %}"
      },
      "fileType":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.fileType}}"
      },
      "csvOptions":{
         "sep":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'delimiter' %}{{customerData.csvOptions.delimiter}}{% else %},{% endif %}"
         },
         "quote":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'quote' %}{{customerData.csvOptions.quote}}{% else %}\"{% endif %}"
         },
         "escape":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'escape' %}{{customerData.csvOptions.escape}}{% else %}\\{% endif %}"
         },
         "nullValue":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'nullValue' %}{{customerData.csvOptions.nullValue}}{% else %}null{% endif %}"
         },
         "emptyValue":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'emptyValue' %}{{customerData.csvOptions.emptyValue}}{% else %}{% endif %}"
         }
      }
   }
}
```

## Referência completa e exemplos para opções de formatação de arquivo suportadas {#file-formatting-reference-and-example}

>[!TIP]
>
>As opções de formatação de arquivos CSV descritas abaixo também estão documentadas na variável [Guia do Apache Spark para arquivos CSV](https://spark.apache.org/docs/latest/sql-data-sources-csv.html). As descrições usadas abaixo são obtidas do guia do Apache Spark.

Abaixo está uma referência completa de todas as opções disponíveis de formatação de arquivo no Destination SDK, junto com exemplos de saída para cada opção.

| Campo | Obrigatório / Opcional | Descrição | Valor padrão | Exemplo de saída 1 | Exemplo de saída 2 |
|---|---|---|---|---|---|
| `templatingStrategy` | Obrigatório | Para cada opção de formatação de arquivo configurada, é necessário adicionar o parâmetro `templatingStrategy`, que pode ter dois valores: <br><ul><li>`NONE`: use esse valor se você não estiver planejando permitir que os usuários selecionem entre valores diferentes para uma configuração. Consulte [essa configuração](#file-configuration-templating-none) para um exemplo em que as opções de formatação de arquivo são fixas.</li><li>`PEBBLE_V1`: use esse valor se desejar permitir que os usuários selecionem entre valores diferentes para uma configuração. Nesse caso, você também deve configurar um campo de dados do cliente correspondente na variável `/destination` configuração de ponto de extremidade, para exibir as várias opções para os usuários na interface do usuário. Consulte [essa configuração](#file-configuration-templating-pebble) por exemplo, onde os usuários podem selecionar entre valores diferentes para opções de formatação de arquivo.</li></ul> | - | - | - |
| `compression.value` | Opcional | Codec de compactação a ser usado ao salvar dados no arquivo. Valores compatíveis: `none`, `bzip2`, `gzip`, `lz4`e `snappy`. | `none` | - | - |
| `fileType.value` | Opcional | Especifica o formato do arquivo de saída. Valores compatíveis: `csv`, `parquet`e `json`. | `csv` | - | - |
| `csvOptions.quote.value` | Opcional | *Somente para`"fileType.value": "csv"`*. Define um caractere único usado para escapar de valores entre aspas, onde o separador pode fazer parte do valor. | `null` | - | - |
| `csvOptions.quoteAll.value` | Opcional | *Somente para`"fileType.value": "csv"`*. Indica se todos os valores devem ser sempre entre aspas. O padrão é apenas valores de escape contendo um caractere de aspas. | `false` | `quoteAll`:`false` --> `male,John,"TestLastName"` | `quoteAll`:`true` -->`"male","John","TestLastName"` |
| `csvOptions.delimiter.value` | Opcional | *Somente para`"fileType.value": "csv"`*. Define um separador para cada campo e valor. Esse separador pode ter um ou mais caracteres. | `,` | `delimiter`:`,` --> `comma-separated values"` | `delimiter`:`\t` --> `tab-separated values` |
| `csvOptions.escape.value` | Opcional | *Somente para`"fileType.value": "csv"`*. Define um caractere único usado para “escapar” citações dentro de um valor já citado. | `\` | `"escape"`:`"\\"` --> `male,John,"Test,\"LastName5"` | `"escape"`:`"'"` --> `male,John,"Test,'''"LastName5"` |
| `csvOptions.escapeQuotes.value` | Opcional | *Somente para`"fileType.value": "csv"`*. Indica se os valores que contêm aspas devem sempre ser entre aspas. O padrão é omitir todos os valores que contenham um caractere de aspas. | `true` | - | - |
| `csvOptions.header.value` | Opcional | *Somente para`"fileType.value": "csv"`*. Indica se os nomes das colunas devem ser gravados como a primeira linha no arquivo exportado. | `true` | - | - |
| `csvOptions.ignoreLeadingWhiteSpace.value` | Opcional | *Somente para`"fileType.value": "csv"`*. Indica se os espaços em branco à esquerda devem ser aparados a partir de valores. | `true` | `ignoreLeadingWhiteSpace`:`true` --> `"male","John","TestLastName"` | `ignoreLeadingWhiteSpace`:`false`--> `"    male","John","TestLastName"` |
| `csvOptions.ignoreTrailingWhiteSpace.value` | Opcional | *Somente para`"fileType.value": "csv"`*. Indica se os espaços em branco à direita devem ser aparados de valores. | `true` | `ignoreTrailingWhiteSpace`:`true` --> `"male","John","TestLastName"` | `ignoreTrailingWhiteSpace`:`false`--> `"male    ","John","TestLastName"` |
| `csvOptions.nullValue.value` | Opcional | *Somente para`"fileType.value": "csv"`*. Define a representação da string de um valor nulo. | `""` | `nullvalue`:`""` --> `male,"",TestLastName` | `nullvalue`:`"NULL"` --> `male,NULL,TestLastName` |
| `csvOptions.dateFormat.value` | Opcional | *Somente para`"fileType.value": "csv"`*. Indica o formato de data. | `yyyy-MM-dd` | `dateFormat`:`yyyy-MM-dd` --> `male,TestLastName,John,2022-02-24` | `dateFormat`:`MM/dd/yyyy` --> `male,TestLastName,John,02/24/2022` |
| `csvOptions.timestampFormat.value` | Opcional | *Somente para`"fileType.value": "csv"`*. Define a string que indica um formato de carimbo de data e hora. | `yyyy-MM-dd'T'HH:mm:ss[.SSS][XXX]` | - | - |
| `csvOptions.charToEscapeQuoteEscaping.value` | Opcional | *Somente para`"fileType.value": "csv"`*. Define um único caractere usado para escapar do escape para o caractere de aspas. | `\` quando os caracteres de escape e aspas são diferentes. `\0` quando o caractere escape e aspas são iguais. | - | - |
| `csvOptions.emptyValue.value` | Opcional | *Somente para`"fileType.value": "csv"`*. Define a representação da string de um valor vazio. | `""` | `"emptyValue":""` --> `male,"",John` | `"emptyValue":"empty"` --> `male,empty,John` |

{style="table-layout:auto"}

## Próximas etapas {#next-steps}

Após a leitura deste artigo, você deve entender melhor como a formatação de arquivo funciona em uma configuração de servidor de destino e como configurá-la.

Para saber mais sobre os outros componentes do servidor de destino, consulte os seguintes artigos:

* [Especificações do servidor para destinos criados com o Destination SDK](server-specs.md)
* [Especificações de modelo](templating-specs.md)
* [Formato de mensagem](message-format.md)