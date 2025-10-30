---
description: Saiba como configurar opções de formatação de arquivo para destinos baseados em arquivo criados com o Adobe Experience Platform Destination SDK, por meio do endpoint &grave;/destination-servers&grave;.
title: Configuração da formatação de arquivo
exl-id: 98fec559-9073-4517-a10e-34c2caf292d5
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '1094'
ht-degree: 2%

---

# Configuração da formatação de arquivo

O Destination SDK oferece suporte a um conjunto flexível de recursos que você pode configurar de acordo com suas necessidades de integração. Entre esses recursos está o suporte para a formatação de arquivo [!DNL CSV].

Ao criar destinos baseados em arquivo por meio do Destination SDK, é possível definir como os arquivos CSV exportados devem ser formatados. É possível personalizar muitas opções de formatação, como, mas não limitado a:

* Se o arquivo CSV deve incluir um cabeçalho;
* Qual caractere usar para citar valores;
* Como os valores vazios devem ser exibidos.

Dependendo da configuração de destino, os usuários verão determinadas opções na interface do usuário ao se conectarem a um destino baseado em arquivo. Você pode ver a aparência dessas opções na documentação [opções de formatação de arquivo para destinos baseados em arquivo](../../../ui/batch-destinations-file-formatting-options.md).


As configurações de formatação de arquivo fazem parte da configuração do servidor de destino para destinos baseados em arquivo.

Para entender onde esse componente se encaixa em uma integração criada com o Destination SDK, consulte o diagrama na documentação de [opções de configuração](../configuration-options.md) ou o guia sobre como [usar o Destination SDK para configurar um destino baseado em arquivo](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration).

Você pode configurar as opções de formatação de arquivo por meio do ponto de extremidade `/authoring/destination-servers`. Consulte as seguintes páginas de referência de API para obter exemplos detalhados de chamadas de API, onde é possível configurar os componentes mostrados nesta página.

* [Criar uma configuração do servidor de destino](../../authoring-api/destination-server/create-destination-server.md)
* [Atualizar uma configuração do servidor de destino](../../authoring-api/destination-server/update-destination-server.md)

Esta página descreve todas as configurações de formatação de arquivo com suporte para arquivos `CSV` exportados.

>[!IMPORTANT]
>
>Todos os nomes e valores de parâmetros com suporte do Destination SDK diferenciam maiúsculas de minúsculas **1&rbrace;.** Para evitar erros de diferenciação entre maiúsculas e minúsculas, use os nomes e valores dos parâmetros exatamente como mostrado na documentação.

## Tipos de integração compatíveis {#supported-integration-types}

Consulte a tabela abaixo para obter detalhes sobre quais tipos de integrações suportam a funcionalidade descrita nesta página.

| Tipo de integração | Suporte à funcionalidade |
|---|---|
| Integrações em tempo real (streaming) | Não |
| Integrações baseadas em arquivo (lote) | Sim |

## Parâmetros compatíveis {#supported-parameters}

Você pode modificar várias propriedades dos arquivos exportados para corresponder aos requisitos do sistema de recebimento de arquivos do destino, a fim de ler e interpretar de maneira ideal os arquivos recebidos do Experience Platform.

>[!NOTE]
>
>As opções de CSV são suportadas somente ao exportar arquivos CSV. A seção `fileConfigurations` não é obrigatória ao configurar um novo servidor de destino. Se você não passar nenhum valor na chamada de API para as opções de CSV, os valores padrão da [tabela de referência abaixo](#file-formatting-reference-and-example) serão usados.


## Opções de CSV nas quais os usuários não podem selecionar opções de configuração {#file-configuration-templating-none}

No exemplo de configuração abaixo, todas as opções de CSV são predefinidas. As configurações de exportação definidas em cada um dos parâmetros `csvOptions` são finais e os usuários não podem modificá-las.

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
        "maxFileRowCount":5000000,
        "includeFileManifest": {
            "templatingStrategy":"PEBBLE_V1",
            "value":"{{ customerData.includeFileManifest }}"
      }
    }
```

## Opções de CSV nas quais os usuários podem selecionar opções de configuração {#file-configuration-templating-pebble}

No exemplo de configuração abaixo, nenhuma das opções de CSV é predefinida. O `value` em cada um dos parâmetros `csvOptions` é configurado em um campo de dados do cliente correspondente por meio do ponto de extremidade `/destinations` (por exemplo, [`customerData.quote`](../../functionality/destination-configuration/customer-data-fields.md#conditional-options) para a opção de formatação de arquivo `quote`) e os usuários podem usar a interface do usuário do Experience Platform para selecionar entre as várias opções configuradas no campo de dados do cliente correspondente. Você pode ver a aparência dessas opções na documentação [opções de formatação de arquivo para destinos baseados em arquivo](../../../ui/batch-destinations-file-formatting-options.md).

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
      },
      "maxFileRowCount":5000000,
      "includeFileManifest": {
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{ customerData.includeFileManifest }}"
      }
   }
}
```

## Referência completa e exemplos de opções de formatação de arquivo compatíveis {#file-formatting-reference-and-example}

>[!TIP]
>
>As opções de formatação de arquivo CSV descritas abaixo também estão documentadas no [guia do Apache Spark para arquivos CSV](https://spark.apache.org/docs/latest/sql-data-sources-csv.html). As descrições usadas abaixo foram tiradas do guia do Apache Spark.

Abaixo está uma referência completa de todas as opções de formatação de arquivo disponíveis no Destination SDK, juntamente com exemplos de saída para cada opção.

| Campo | Obrigatório/Opcional | Descrição | Valor padrão | Exemplo de saída 1 | Exemplo de saída 2 |
|---|---|---|---|---|---|
| `templatingStrategy` | Obrigatório | Para cada opção de formatação de arquivo configurada, é necessário adicionar o parâmetro `templatingStrategy`, que pode ter dois valores: <br><ul><li>`NONE`: use esse valor se não estiver planejando permitir que os usuários selecionem entre valores diferentes para uma configuração. Consulte [esta configuração](#file-configuration-templating-none) para obter um exemplo onde as opções de formatação de arquivo são corrigidas.</li><li>`PEBBLE_V1`: use este valor se quiser permitir que os usuários selecionem entre valores diferentes para uma configuração. Nesse caso, você também deve configurar um campo de dados do cliente correspondente na configuração do ponto de extremidade `/destination` para exibir as várias opções aos usuários na interface do usuário. Consulte [esta configuração](#file-configuration-templating-pebble) para obter um exemplo em que os usuários podem selecionar entre valores diferentes para opções de formatação de arquivo.</li></ul> | - | - | - |
| `compression.value` | Opcional | Codec de compactação a ser usado ao salvar dados no arquivo. Valores com suporte: `none`, `bzip2`, `gzip`, `lz4` e `snappy`. | `none` | - | - |
| `fileType.value` | Opcional | Especifica o formato do arquivo de saída. Valores com suporte: `csv`, `parquet` e `json`. | `csv` | - | - |
| `csvOptions.quote.value` | Opcional | *Somente para`"fileType.value": "csv"`*. Define um caractere único usado para sair de valores entre aspas onde o separador pode ser parte do valor. | `null` | Exemplo de valor padrão: `quote.value: "u0000"` —> `male,NULJohn,LastNameNUL` | Exemplo personalizado: `quote.value: "\""` —> `male,"John,LastName"` |
| `csvOptions.quoteAll.value` | Opcional | *Somente para`"fileType.value": "csv"`*. Indica se todos os valores devem sempre estar entre aspas. O padrão é omitir apenas valores que contenham um caractere de aspas. | `false` | `quoteAll`:`false` —> `male,John,"TestLastName"` | `quoteAll`:`true` —>`"male","John","TestLastName"` |
| `csvOptions.delimiter.value` | Opcional | *Somente para`"fileType.value": "csv"`*. Define um separador para cada campo e valor. Esse separador pode conter um ou mais caracteres. | `,` | `delimiter`:`,` —> `comma-separated values"` | `delimiter`:`\t` —> `tab-separated values` |
| `csvOptions.escape.value` | Opcional | *Somente para`"fileType.value": "csv"`*. Define um caractere único usado para fazer o escape de aspas dentro de um valor já citado. | `\` | `"escape"`:`"\\"` —> `male,John,"Test,\"LastName5"` | `"escape"`:`"'"` —> `male,John,"Test,'''"LastName5"` |
| `csvOptions.escapeQuotes.value` | Opcional | *Somente para`"fileType.value": "csv"`*. Indica se os valores contendo aspas devem sempre estar entre aspas. O padrão é omitir todos os valores que contenham um caractere de aspas. | `true` | - | - |
| `csvOptions.header.value` | Opcional | *Somente para`"fileType.value": "csv"`*. Indica se os nomes das colunas devem ser gravados como a primeira linha no arquivo exportado. | `true` | - | - |
| `csvOptions.ignoreLeadingWhiteSpace.value` | Opcional | *Somente para`"fileType.value": "csv"`*. Indica se os espaços em branco à esquerda devem ser aparados dos valores. | `true` | `ignoreLeadingWhiteSpace`:`true` —> `"male","John","TestLastName"` | `ignoreLeadingWhiteSpace`:`false`—> `"    male","John","TestLastName"` |
| `csvOptions.ignoreTrailingWhiteSpace.value` | Opcional | *Somente para`"fileType.value": "csv"`*. Indica se espaços em branco à direita devem ser aparados de valores. | `true` | `ignoreTrailingWhiteSpace`:`true` —> `"male","John","TestLastName"` | `ignoreTrailingWhiteSpace`:`false`—> `"male    ","John","TestLastName"` |
| `csvOptions.nullValue.value` | Opcional | *Somente para`"fileType.value": "csv"`*. Define a representação da cadeia de caracteres de um valor nulo. | `""` | `nullvalue`:`""` —> `male,"",TestLastName` | `nullvalue`:`"NULL"` —> `male,NULL,TestLastName` |
| `csvOptions.dateFormat.value` | Opcional | *Somente para`"fileType.value": "csv"`*. Indica o formato de data. | `yyyy-MM-dd` | `dateFormat`:`yyyy-MM-dd` —> `male,TestLastName,John,2022-02-24` | `dateFormat`:`MM/dd/yyyy` —> `male,TestLastName,John,02/24/2022` |
| `csvOptions.timestampFormat.value` | Opcional | *Somente para`"fileType.value": "csv"`*. Define a cadeia de caracteres que indica um formato de carimbo de data e hora. | `yyyy-MM-dd'T'HH:mm:ss[.SSS][XXX]` | - | - |
| `csvOptions.charToEscapeQuoteEscaping.value` | Opcional | *Somente para`"fileType.value": "csv"`*. Define um único caractere usado para escapar do escape para o caractere de citação. | `\` quando os caracteres de escape e aspas são diferentes. `\0` quando o caractere de escape e aspas são iguais. | - | - |
| `csvOptions.emptyValue.value` | Opcional | *Somente para`"fileType.value": "csv"`*. Define a representação da cadeia de caracteres de um valor vazio. | `""` | `"emptyValue":""` --> `male,"",John` | `"emptyValue":"empty"` --> `male,empty,John` |
| `maxFileRowCount` | Opcional | Indica o número máximo de linhas por arquivo exportado, entre 1.000.000 e 10.000.000 linhas. | 5.000.000 | - | - |
| `includeFileManifest` | Opcional | Habilita o suporte para exportação de um manifesto de arquivo junto com as exportações de arquivo. O arquivo JSON de manifesto contém informações sobre o local de exportação, o tamanho da exportação e muito mais. O manifesto é nomeado usando o formato `manifest-<<destinationId>>-<<dataflowRunId>>.json`. | Exibir um [arquivo de manifesto de exemplo](/help/destinations/assets/common/manifest-d0420d72-756c-4159-9e7f-7d3e2f8b501e-0ac8f3c0-29bd-40aa-82c1-f1b7e0657b19.json). O arquivo de manifesto inclui os seguintes campos: <ul><li>`flowRunId`: A [execução do fluxo de dados](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) que gerou o arquivo exportado.</li><li>`scheduledTime`: A hora em UTC quando o arquivo foi exportado. </li><li>`exportResults.sinkPath`: O caminho no local de armazenamento onde o arquivo exportado está depositado. </li><li>`exportResults.name`: O nome do arquivo exportado.</li><li>`size`: O tamanho do arquivo exportado, em bytes.</li></ul> | - | - |

{style="table-layout:auto"}

## Próximas etapas {#next-steps}

Depois de ler este artigo, você terá uma melhor compreensão de como a formatação de arquivos funciona em uma configuração de servidor de destino e como configurá-la.

Para saber mais sobre os outros componentes do servidor de destino, consulte os seguintes artigos:

* [Especificações do servidor para destinos criados com o Destination SDK](server-specs.md)
* [Especificações de modelo](templating-specs.md)
* [Formato da mensagem](message-format.md)
