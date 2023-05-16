---
description: Saiba como criar campos de entrada na interface do usuário do Experience Platform que permitem que os usuários especifiquem várias informações relevantes para como se conectar e exportar dados para seu destino.
title: Campos de dados do cliente
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '1436'
ht-degree: 2%

---


# Configurar entrada de usuário por meio de campos de dados do cliente

Ao se conectar ao seu destino na interface do usuário do Experience Platform, você pode precisar que seus usuários forneçam detalhes de configuração específicos ou selecionem opções específicas que você disponibiliza para eles. No Destination SDK, essas opções são chamadas de campos de dados do cliente.

Para entender onde esse componente se encaixa em uma integração criada com o Destination SDK, consulte o diagrama no [opções de configuração](../configuration-options.md) ou veja as seguintes páginas de visão geral da configuração de destino:

* [Use o Destination SDK para configurar um destino de transmissão](../../guides/configure-destination-instructions.md#create-destination-configuration)
* [Use o Destination SDK para configurar um destino baseado em arquivo](../../guides/configure-file-based-destination-instructions.md#create-destination-configuration)

## Casos de uso para campos de dados do cliente {#use-cases}

Use campos de dados do cliente para obter uma variedade de casos de uso em que você precisa que usuários insiram dados na interface do usuário do Experience Platform. Por exemplo, use campos de dados do cliente quando os usuários precisarem fornecer:

* Nomes e caminhos do bucket de armazenamento na nuvem, para destinos com base em arquivo.
* O formato aceito pelos campos de dados do cliente.
* Tipos de compactação de arquivo disponíveis que os usuários podem selecionar.
* Listas de endpoints disponíveis para integrações em tempo real (streaming).

Você pode configurar os campos de dados do cliente por meio da variável `/authoring/destinations` endpoint . Consulte as páginas de referência da API a seguir para obter exemplos detalhados de chamadas de API, onde é possível configurar os componentes mostrados nesta página.

* [Criar uma configuração de destino](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Atualizar uma configuração de destino](../../authoring-api/destination-configuration/update-destination-configuration.md)

Este artigo descreve todos os tipos de configuração de campos de dados do cliente suportados que você pode usar para seu destino e mostra o que os clientes verão na interface do usuário do Experience Platform.

>[!IMPORTANT]
>
>Todos os nomes de parâmetros e valores suportados pelo Destination SDK são **distinção entre maiúsculas e minúsculas**. Para evitar erros de diferenciação entre maiúsculas e minúsculas, use os nomes e valores dos parâmetros exatamente como mostrado na documentação.

## Tipos de integração compatíveis {#supported-integration-types}

Consulte a tabela abaixo para obter detalhes sobre quais tipos de integrações oferecem suporte à funcionalidade descrita nesta página.

| Tipo de integração | Oferece suporte à funcionalidade |
|---|---|
| Integrações em tempo real (streaming) | Sim |
| Integrações baseadas em arquivo (em lote) | Sim |

## Parâmetros compatíveis {#supported-parameters}

Ao criar seus próprios campos de dados do cliente, você pode usar os parâmetros descritos na tabela abaixo para configurar seu comportamento.

| Parâmetro | Tipo | Obrigatório / Opcional | Descrição |
|---------|----------|------|---|
| `name` | String | Obrigatório | Forneça um nome para o campo personalizado que está sendo introduzido. Esse nome não está visível na interface do usuário da plataforma, a menos que a variável `title` campo está vazio ou ausente. |
| `type` | String | Obrigatório | Indica o tipo de campo personalizado que está sendo introduzido. Valores aceitos: <ul><li>`string`</li><li>`object`</li><li>`integer`</li></ul> |
| `title` | String | Opcional | Indica o nome do campo, como é visto pelos clientes na interface do usuário da plataforma. Se esse campo estiver vazio ou ausente, a interface do usuário herdará o nome do campo do `name` valor. |
| `description` | String | Opcional | Forneça uma descrição para o campo personalizado. Esta descrição não está visível na interface do usuário da plataforma. |
| `isRequired` | Booleano | Opcional | Indica se os usuários devem fornecer um valor para esse campo no fluxo de trabalho de configuração de destino. |
| `pattern` | String | Opcional | Impõe um padrão para o campo personalizado, se necessário. Use expressões regulares para impor um padrão. Por exemplo, se as IDs do cliente não incluírem números ou sublinhados, insira `^[A-Za-z]+$` neste campo. |
| `enum` | String | Opcional | Renderiza o campo personalizado como um menu suspenso e lista as opções disponíveis para o usuário. |
| `default` | String | Opcional | Define o valor padrão de um `enum` lista. |
| `hidden` | Booleano | Opcional | Indica se o campo de dados do cliente é mostrado na interface do usuário ou não. |
| `unique` | Booleano | Opcional | Use esse parâmetro quando precisar criar um campo de dados do cliente cujo valor deve ser exclusivo em todos os fluxos de dados de destino configurados pela organização do usuário. Por exemplo, a variável **[!UICONTROL Alias de integração]** no campo [Personalização personalizada](../../../catalog/personalization/custom-personalization.md) o destino deve ser exclusivo, o que significa que dois fluxos de dados separados para esse destino não podem ter o mesmo valor para esse campo. |
| `readOnly` | Booleano | Opcional | Indica se o cliente pode ou não alterar o valor do campo. |

{style="table-layout:auto"}

No exemplo abaixo, a variável `customerDataFields` define dois campos que os usuários devem inserir na interface do usuário da plataforma ao se conectar ao destino:

* `Account ID`: Uma ID de conta de usuário para a plataforma de destino.
* `Endpoint region`: O endpoint regional da API à qual eles se conectarão. O `enum` cria um menu suspenso com os valores definidos em , disponíveis para os usuários selecionarem.

```json
"customerDataFields":[
   {
      "name":"accountID",
      "title":"User account ID",
      "description":"User account ID for the destination platform.",
      "type":"string",
      "isRequired":true
   },
   {
      "name":"region",
      "title":"API endpoint region",
      "description":"The API endpoint region that the user should connect to.",
      "type":"string",
      "isRequired":true,
      "enum":[
         "EU"
         "US",
      ],
      "readOnly":false,
      "hidden":false
   }
]
```

A experiência resultante da interface do usuário é mostrada na imagem abaixo.

![Imagem da interface do usuário mostrando um exemplo de campos de dados do cliente.](../../assets/functionality/destination-configuration/customer-data-fields-example.png)

## Nomes e descrições de conexões de destino {#names-description}

Ao criar um novo destino, o Destination SDK adiciona automaticamente **[!UICONTROL Nome]** e **[!UICONTROL Descrição]** para a tela de conexão de destino na interface do usuário da plataforma. Como você pode ver no exemplo acima, a variável **[!UICONTROL Nome]** e **[!UICONTROL Descrição]** são renderizados na interface do usuário sem ser incluídos na configuração dos campos de dados do cliente.

>[!IMPORTANT]
>
>Se você adicionar **[!UICONTROL Nome]** e **[!UICONTROL Descrição]** na configuração dos campos de dados do cliente, os usuários os verão duplicados na interface do usuário.

## Campos de dados do cliente da ordem {#ordering}

A ordem em que você adiciona os campos de dados do cliente na configuração de destino é refletida na interface do usuário da plataforma.

Por exemplo, a configuração abaixo é refletida adequadamente na interface do usuário, com as opções exibidas na ordem **[!UICONTROL Nome]**, **[!UICONTROL Descrição]**, **[!UICONTROL Nome do bucket]**, **[!UICONTROL Caminho da pasta]**, **[!UICONTROL Tipo de arquivo]**, **[!UICONTROL Formato de compactação]**.

```json
"customerDataFields":[
{
   "name":"bucketName",
   "title":"Bucket name",
   "description":"Amazon S3 bucket name",
   "type":"string",
   "isRequired":true,
   "pattern":"(?=^.{3,63}$)(?!^(\\d+\\.)+\\d+$)(^(([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])\\.)*([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])$)",
   "readOnly":false,
   "hidden":false
},
{
   "name":"path",
   "title":"Folder path",
   "description":"Enter the path to your S3 bucket folder",
   "type":"string",
   "isRequired":true,
   "pattern":"^[0-9a-zA-Z\\/\\!\\-_\\.\\*\\''\\(\\)]*((\\%SEGMENT_(NAME|ID)\\%)?\\/?)+$",
   "readOnly":false,
   "hidden":false
},
{
   "name":"fileType",
   "title":"File Type",
   "description":"Select the exported file type.",
   "type":"string",
   "isRequired":true,
   "readOnly":false,
   "hidden":false,
   "enum":[
      "csv",
      "json",
      "parquet"
   ],
   "default":"csv"
},
{
   "name":"compression",
   "title":"Compression format",
   "description":"Select the desired file compression format.",
   "type":"string",
   "isRequired":true,
   "readOnly":false,
   "enum":[
      "SNAPPY",
      "GZIP",
      "DEFLATE",
      "NONE"
   ]
}
]
```

![Imagem que mostra a ordem das opções de formatação de arquivo na interface do usuário do Experience Platform.](../../assets/functionality/destination-configuration/customer-data-fields-order.png)

## Agrupar campos de dados do cliente {#grouping}

Você pode agrupar vários campos de dados do cliente em uma seção. Ao configurar a conexão com o destino na interface do usuário, os usuários podem ver e se beneficiar de um agrupamento visual de campos semelhantes.

Para fazer isso, use `"type": "object"` para criar o grupo e coletar os campos de dados do cliente desejados em um `properties` como mostrado na imagem abaixo, onde o agrupamento **[!UICONTROL Opções de CSV]** é realçada.

```json {line-numbers="true" highlight="6-28"}
"customerDataFields":[
   {
      "name":"csvOptions",
      "title":"CSV Options",
      "description":"Select your CSV options",
      "type":"object",
      "properties":[
         {
            "name":"delimiter",
            "title":"Delimiter",
            "description":"Select your Delimiter",
            "type":"string",
            "isRequired":false,
            "default":",",
            "namedEnum":[
               {
                  "name":"Comma (,)",
                  "value":","
               },
               {
                  "name":"Tab (\\t)",
                  "value":"\t"
               }
            ],
            "readOnly":false,
            "hidden":false
         }
      ]
   }
]
```

![Imagem que mostra os campos de dados do cliente agrupados na interface do usuário.](../../assets/functionality/destination-configuration/group-customer-data-fields.png)

## Criar seletores suspensos para campos de dados do cliente {#dropdown-selectors}

Para situações em que você deseja permitir que os usuários selecionem entre várias opções, por exemplo, qual caractere deve ser usado para delimitar os campos nos arquivos CSV, é possível adicionar campos suspensos à interface do usuário.

Para fazer isso, use o `namedEnum` conforme mostrado abaixo e configure um `default` para as opções que o usuário pode selecionar.

```json {line-numbers="true" highlight="15-24"}
"customerDataFields":[
   {
      "name":"csvOptions",
      "title":"CSV Options",
      "description":"Select your CSV options",
      "type":"object",
      "properties":[
         {
            "name":"delimiter",
            "title":"Delimiter",
            "description":"Select your Delimiter",
            "type":"string",
            "isRequired":false,
            "default":",",
            "namedEnum":[
               {
                  "name":"Comma (,)",
                  "value":","
               },
               {
                  "name":"Tab (\\t)",
                  "value":"\t"
               }
            ],
            "readOnly":false,
            "hidden":false
         }
      ]
   }
]
```

![Gravação de tela mostrando um exemplo de seletores suspensos criados com a configuração mostrada acima.](../../assets/functionality/destination-configuration/customer-data-fields-dropdown.gif)

## Criar campos de dados condicionais do cliente {#conditional-options}

Você pode criar campos de dados condicionais do cliente, que são exibidos no fluxo de trabalho de ativação somente quando os usuários selecionam uma determinada opção.

Por exemplo, você pode criar opções condicionais de formatação de arquivo para serem exibidas somente quando os usuários selecionarem um tipo específico de exportação de arquivo.

A configuração abaixo cria um agrupamento condicional para opções de formatação de arquivos CSV. As opções do arquivo CSV são exibidas somente quando o usuário seleciona CSV como o tipo de arquivo desejado para exportação.

Para definir um campo como condicional, use a variável `conditional` como mostrado abaixo:

```json
"conditional": {
   "field": "fileType",
   "operator": "EQUALS",
   "value": "CSV"
}
```

Em um contexto mais amplo, é possível ver a variável `conditional` campo que está sendo usado na configuração de destino abaixo, junto com o `fileType` e a `csvOptions` objeto no qual está definido.

```json {line-numbers="true" highlight="3-15, 21-25"}
"customerDataFields":[
   {
      "name":"fileType",
      "title":"File Type",
      "description":"Select your file type",
      "type":"string",
      "isRequired":true,
      "enum":[
         "PARQUET",
         "CSV",
         "JSON"
      ],
      "readOnly":false,
      "hidden":false
   },
   {
      "name":"csvOptions",
      "title":"CSV Options",
      "description":"Select your CSV options",
      "type":"object",
      "conditional":{
         "field":"fileType",
         "operator":"EQUALS",
         "value":"CSV"
      },
      "properties":[
         {
            "name":"delimiter",
            "title":"Delimiter",
            "description":"Select your Delimiter",
            "type":"string",
            "isRequired":false,
            "default":",",
            "namedEnum":[
               {
                  "name":"Comma (,)",
                  "value":","
               },
               {
                  "name":"Tab (\\t)",
                  "value":"\t"
               }
            ],
            "readOnly":false,
            "hidden":false
         },
         {
            "name":"quote",
            "title":"Quote Character",
            "description":"Select your Quote character",
            "type":"string",
            "isRequired":false,
            "default":"",
            "namedEnum":[
               {
                  "name":"Double Quotes (\")",
                  "value":"\""
               },
               {
                  "name":"Null Character (\u0000)",
                  "value":"\u0000"
               }
            ],
            "readOnly":false,
            "hidden":false
         },
         {
            "name":"escape",
            "title":"Escape Character",
            "description":"Select your Escape character",
            "type":"string",
            "isRequired":false,
            "default":"\\",
            "namedEnum":[
               {
                  "name":"Back Slash (\\)",
                  "value":"\\"
               },
               {
                  "name":"Single Quote (')",
                  "value":"'"
               }
            ],
            "readOnly":false,
            "hidden":false
         },
         {
            "name":"emptyValue",
            "title":"Empty Value",
            "description":"Select the output value of blank fields",
            "type":"string",
            "isRequired":false,
            "default":"",
            "namedEnum":[
               {
                  "name":"Empty String",
                  "value":""
               },
               {
                  "name":"\"\"",
                  "value":"\"\""
               },
               {
                  "name":"null",
                  "value":"null"
               }
            ],
            "readOnly":false,
            "hidden":false
         },
         {
            "name":"nullValue",
            "title":"Null Value",
            "description":"Select the output value of 'null' fields",
            "type":"string",
            "isRequired":false,
            "default":"null",
            "namedEnum":[
               {
                  "name":"Empty String",
                  "value":""
               },
               {
                  "name":"\"\"",
                  "value":"\"\""
               },
               {
                  "name":"null",
                  "value":"null"
               }
            ],
            "readOnly":false,
            "hidden":false
         }
      ],
      "isRequired":false,
      "readOnly":false,
      "hidden":false
   }
]
```

Abaixo, você pode ver a tela da interface do usuário resultante, com base na configuração acima. Quando o usuário seleciona o CSV do tipo de arquivo, opções adicionais de formatação de arquivo referentes ao tipo de arquivo CSV são exibidas na interface do usuário.

![Gravação de tela mostrando a opção de formatação condicional de arquivo para arquivos CSV.](../../assets/functionality/destination-configuration/customer-data-fields-conditional.gif)

## Acesso aos campos de dados do cliente modelos {#accessing-templatized-fields}

Quando seu destino exigir entrada do usuário, você deve fornecer uma seleção de campos de dados do cliente para seus usuários, que eles podem preencher por meio da interface do usuário da plataforma. Em seguida, você deve configurar o servidor de destino para ler corretamente a entrada do usuário dos campos de dados do cliente. Isso é feito por campos templatizados.

Campos modelos usam o formato `{{customerData.fieldName}}`, onde `fieldName` é o nome do campo de dados do cliente do qual você está lendo informações. Todos os campos de dados de cliente modelos são precedidos por `customerData.` e incluso em chaves duplas `{{ }}`.

Por exemplo, considere a seguinte configuração de destino do Amazon S3:

```json
"customerDataFields":[
   {
      "name":"bucketName",
      "title":"Enter the name of your Amazon S3 bucket",
      "description":"Amazon S3 bucket name",
      "type":"string",
      "isRequired":true,
      "pattern":"(?=^.{3,63}$)(?!^(\\d+\\.)+\\d+$)(^(([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])\\.)*([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])$)",
      "readOnly":false,
      "hidden":false
   },
   {
      "name":"path",
      "title":"Enter the path to your S3 bucket folder",
      "description":"Enter the path to your S3 bucket folder",
      "type":"string",
      "isRequired":true,
      "pattern":"^[0-9a-zA-Z\\/\\!\\-_\\.\\*\\''\\(\\)]*((\\%SEGMENT_(NAME|ID)\\%)?\\/?)+$",
      "readOnly":false,
      "hidden":false
   }
]
```

Essa configuração solicita que os usuários digitem seus [!DNL Amazon S3] nome do bucket e caminho da pasta em seus respectivos campos de dados do cliente.

Para que o Experience Platform se conecte corretamente ao [!DNL Amazon S3], seu servidor de destino deve ser configurado para ler os valores desses dois campos de dados do cliente, conforme mostrado abaixo:

```json
 "fileBasedS3Destination":{
      "bucketName":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.bucketName}}"
      },
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      }
   }
```

Os valores templatizados `{{customerData.bucketName}}` e `{{customerData.path}}` leia os valores fornecidos pelo usuário para que o Experience Platform possa se conectar com êxito à plataforma de destino.

Para obter mais informações sobre como configurar o servidor de destino para ler campos modelos, consulte a documentação em [campos embutidos em código fixo versus campos templatizados](../destination-server/server-specs.md#templatized-fields).

## Próximas etapas {#next-steps}

Após a leitura deste artigo, você deve ter uma melhor compreensão de como pode permitir que seus usuários insiram informações na interface do usuário do Experience Platform por meio de campos de dados do cliente. Agora você também sabe selecionar o campo de dados do cliente correto para o caso de uso e configurar, solicitar e agrupar campos de dados do cliente na interface do usuário da plataforma.

Para saber mais sobre os outros componentes de destino, consulte os seguintes artigos:

* [Autenticação do cliente](customer-authentication.md)
* [Autenticação OAuth2](oauth2-authentication.md)
* [Atributos da interface do usuário](ui-attributes.md)
* [Configuração do esquema](schema-configuration.md)
* [Configuração do namespace de identidade](identity-namespace-configuration.md)
* [Configurações de mapeamento suportadas](supported-mapping-configurations.md)
* [Delivery de destino](destination-delivery.md)
* [Configuração de metadados de público-alvo](audience-metadata-configuration.md)
* [Política de agregação](aggregation-policy.md)
* [Configuração em lote](batch-configuration.md)
* [Qualificações de perfil histórico](historical-profile-qualifications.md)