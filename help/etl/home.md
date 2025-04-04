---
keywords: Experience Platform;página inicial;tópicos populares;integrações de ETL;etl;etl;integrações de ETL
solution: Experience Platform
title: Desenvolvimento de integrações ETL para o Adobe Experience Platform
description: O guia de integração de ETL descreve as etapas gerais para criar conectores seguros e de alto desempenho para o Experience Platform e assimilar dados na Experience Platform.
exl-id: 7d29b61c-a061-46f8-a31f-f20e4d725655
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '3978'
ht-degree: 3%

---

# Desenvolvimento de integrações ETL para o Adobe Experience Platform

O guia de integração ETL descreve as etapas gerais para criar conectores seguros e de alto desempenho para [!DNL Experience Platform] e assimilar dados no [!DNL Experience Platform].


- [[!DNL Catalog]](https://www.adobe.io/experience-platform-apis/references/catalog/)
- [[!DNL Data Access]](https://www.adobe.io/experience-platform-apis/references/data-access/)
- [[!DNL Batch Ingestion]](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/)
- [[!DNL Streaming Ingestion]](https://developer.adobe.com/experience-platform-apis/references/streaming-ingestion/)
- [Autenticação e autorização para APIs do Experience Platform](https://www.adobe.com/go/platform-api-authentication-en)
- [[!DNL Schema Registry]](https://www.adobe.io/experience-platform-apis/references/schema-registry/)

Este guia também inclui exemplos de chamadas de API a serem usadas ao criar um conector ETL, com links para a documentação que descreve cada serviço do [!DNL Experience Platform], e o uso de sua API, com mais detalhes.

Uma integração de exemplo está disponível em [!DNL GitHub] através do [Código de referência de integração de ecossistema ETL](https://github.com/adobe/acp-data-services-etl-reference) sob a [!DNL Apache] Versão de licença 2.0.

## Fluxo de trabalho

O diagrama de fluxo de trabalho a seguir fornece uma visão geral de alto nível para a integração dos componentes do Adobe Experience Platform com um aplicativo e conector ETL.

![](images/etl.png)

## Componentes do Adobe Experience Platform

Há vários componentes do Experience Platform envolvidos nas integrações do conector ETL. A lista a seguir descreve vários componentes e funcionalidades principais:

- **Adobe Identity Management System (IMS)** - Fornece a estrutura de autenticação para os serviços da Adobe.
- **Organização IMS** - Uma entidade corporativa que pode ser proprietária ou licenciar produtos e serviços e permitir acesso aos membros.
- **Usuário do IMS** - Membros de uma Organização do IMS. A relação entre organização e usuário é do tipo muitos para muitos.
- **[!DNL Sandbox]** - Uma partição virtual em uma única instância do [!DNL Experience Platform], para ajudar a desenvolver aplicativos de experiência digital.
- **Descoberta de Dados** - Registra os metadados de dados assimilados e transformados em [!DNL Experience Platform].
- **[!DNL Data Access]** - Fornece aos usuários uma interface para acessar seus dados em [!DNL Experience Platform].
- **[!DNL Data Ingestion]** - Envia dados para [!DNL Experience Platform] com [!DNL Data Ingestion] APIs.
- **[!DNL Schema Registry]** - Define e armazena esquema que descreve a estrutura de dados a ser usada em [!DNL Experience Platform].

## Introdução às [!DNL Experience Platform] APIs

As seções a seguir fornecem informações adicionais que você precisará saber ou ter disponíveis para fazer chamadas com êxito para as APIs do [!DNL Experience Platform].

### Leitura de chamadas de API de amostra

Este manual fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e conteúdos de solicitação formatados corretamente. Também fornece exemplos de JSON retornado nas respostas da API. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas [!DNL Experience Platform].

### Coletar valores para cabeçalhos necessários

Para fazer chamadas para APIs do [!DNL Experience Platform], primeiro complete o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). Concluir o tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API da [!DNL Experience Platform], conforme mostrado abaixo:

- Autorização: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id `{ORG_ID}`

Todos os recursos em [!DNL Experience Platform] estão isolados em sandboxes virtuais específicas. Todas as solicitações para [!DNL Experience Platform] APIs exigem um cabeçalho que especifique o nome da sandbox em que a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre sandboxes em [!DNL Experience Platform], consulte a [documentação de visão geral da sandbox](../sandboxes/home.md).

Todas as solicitações que contêm um conteúdo (POST, PUT, PATCH) exigem um cabeçalho adicional:

- Tipo de conteúdo: application/json

## Fluxo geral de usuário

Para começar, um usuário do ETL faz logon na interface do usuário (UI) [!DNL Experience Platform] e cria conjuntos de dados para assimilação usando um conector padrão ou conector de serviço por push.

Na interface, o usuário cria o conjunto de dados de saída selecionando um esquema de conjunto de dados. A escolha do esquema depende do tipo de dados (registro ou série de tempo) que está sendo assimilado em [!DNL Experience Platform]. Ao clicar na guia Esquemas na interface do usuário, o usuário poderá exibir todos os esquemas disponíveis, incluindo o tipo de comportamento compatível com o esquema.

Na ferramenta ETL, o usuário começará a projetar suas transformações de mapeamento após configurar a conexão apropriada (usando suas credenciais). Pressupõe-se que a ferramenta ETL já tenha [!DNL Experience Platform] conectores instalados (processo não definido neste Guia de Integração).

Modelos para uma ferramenta e um fluxo de trabalho de exemplo do ETL foram fornecidos no [fluxo de trabalho do ETL](./workflow.md). Embora as ferramentas ETL possam diferir no formato, a maioria expõe uma funcionalidade semelhante.

>[!NOTE]
>
>O conector ETL deve especificar um filtro de carimbo de data e hora que marque a data para assimilar dados e deslocamento (ou seja, A janela para a qual os dados devem ser lidos). A ferramenta ETL deve ser compatível com a utilização desses dois parâmetros nesta ou em outra interface relevante. No Adobe Experience Platform, esses parâmetros serão mapeados para as datas disponíveis (se presentes) ou para a data capturada presente no objeto em lote do conjunto de dados.

### Exibir lista de conjuntos de dados

Usando a fonte de dados para mapeamento, uma lista de todos os conjuntos de dados disponíveis pode ser obtida usando o [[!DNL Catalog API]](https://www.adobe.io/experience-platform-apis/references/catalog/).

Você pode emitir uma única solicitação de API para exibir todos os conjuntos de dados disponíveis (por exemplo, `GET /dataSets`), com a prática recomendada de incluir parâmetros de consulta que limitam o tamanho da resposta.

Nos casos em que as informações completas do conjunto de dados estão sendo solicitadas, a carga de resposta pode atingir mais de 3 GB em tamanho, o que pode retardar o desempenho geral. Portanto, o uso de parâmetros de consulta para filtrar apenas as informações necessárias tornará as consultas [!DNL Catalog] mais eficientes.

#### Filtragem de lista

Ao filtrar respostas, você pode usar vários filtros em uma única chamada separando parâmetros com um E comercial (`&`). Alguns parâmetros de consulta aceitam listas de valores separados por vírgulas, como o filtro &quot;propriedades&quot; na solicitação de exemplo abaixo.

[!DNL Catalog] respostas são automaticamente medidas de acordo com os limites configurados, no entanto, o parâmetro de consulta &quot;limit&quot; pode ser usado para personalizar as restrições e limitar o número de objetos retornados. Os limites de resposta pré-configurados do [!DNL Catalog] são:

- Se um parâmetro de limite não for especificado, o número máximo de objetos por carga de resposta será 20.
- O limite global para todas as outras consultas [!DNL Catalog] é de 100 objetos.
- Para consultas de conjunto de dados, se observableSchema for solicitado usando o parâmetro de consulta de propriedades, o número máximo de conjuntos de dados retornado será 20.
- Parâmetros de limite inválidos (incluindo `limit=0`) foram atendidos com um erro HTTP 400 que define intervalos adequados.
- Se os limites ou deslocamentos forem transmitidos como parâmetros de consulta, eles terão prioridade sobre aqueles transmitidos como cabeçalhos.

Os parâmetros de consulta são abordados com mais detalhes na [visão geral do Serviço de catálogo](../catalog/home.md).

**Formato da API**

```http
GET /catalog/dataSets
GET /catalog/dataSets?{filter1}={value1},{value2}&{filter2}={value3}
```

**Solicitação**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/dataSets?limit=3&properties=name,description,schemaRef" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

Consulte a [Visão geral do Serviço de Catálogo](../catalog/home.md) para obter exemplos detalhados de como fazer chamadas para o [[!DNL Catalog API]](https://www.adobe.io/experience-platform-apis/references/catalog/).

**Resposta**

A resposta inclui três (`limit=3`) conjuntos de dados que mostram &quot;name&quot;, &quot;description&quot; e &quot;schemaRef&quot; conforme indicado pelo parâmetro de consulta `properties`.

```json
{
    "5b95b155419ec801e6eee780": {
        "name": "Store Transactions",
        "description": "Retails Store Transactions",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18",
            "contentType": "application/vnd.adobe.xed+json;version=1"
        }
    },
    "5c351fa2f5fee300000fa9e8": {
        "name": "Loyalty Members",
        "description": "Loyalty Program Members",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
            "contentType": "application/vnd.adobe.xed+json;version=1"
        }
    },
    "5c1823b19e6f400000993885": {
        "name": "Web Traffic",
        "description": "Retail Web Traffic",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/2025a705890c6d4a4a06b16f8cf6f4ca",
            "contentType": "application/vnd.adobe.xed+json;version=1"
        }
    }
}
```

### Exibir esquema do conjunto de dados

A propriedade &quot;schemaRef&quot; de um conjunto de dados contém um URI que faz referência ao esquema XDM no qual o conjunto de dados se baseia. O esquema XDM (&quot;schemaRef&quot;) representa todos os campos potenciais que podem ser usados pelo conjunto de dados, não necessariamente os campos que estão sendo usados (consulte &quot;observableSchema&quot; abaixo).

O esquema XDM é o esquema usado quando é necessário apresentar ao usuário uma lista de todos os campos disponíveis que podem ser gravados.

O primeiro valor &quot;schemaRef.id&quot; no objeto de resposta anterior (`https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18`) é um URI que aponta para um esquema XDM específico no [!DNL Schema Registry]. O esquema pode ser recuperado fazendo uma solicitação de pesquisa (GET) para a API [!DNL Schema Registry].

>[!NOTE]
>
>A propriedade &quot;schemaRef&quot; substitui a propriedade &quot;schema&quot;, agora obsoleta. Se &quot;schemaRef&quot; estiver ausente do conjunto de dados ou não contiver um valor, você precisará verificar a presença de uma propriedade &quot;schema&quot;. Isso pode ser feito substituindo &quot;schemaRef&quot; por &quot;schema&quot; no parâmetro de consulta `properties` na chamada anterior. Mais detalhes sobre a propriedade &quot;schema&quot; estão disponíveis na seção [Propriedade &quot;schema&quot; do conjunto de dados](#dataset-schema-property-deprecated---eol-2019-05-30) a seguir.

**Formato da API**

```http
GET /schemaregistry/tenant/schemas/{url encoded schemaRef.id}
```

**Solicitação**

A solicitação usa o URI `id` codificado na URL do esquema (o valor do atributo &quot;schemaRef.id&quot;) e requer um cabeçalho Accept.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F274f17bc5807ff307a046bab1489fb18 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1' \
```

O formato da resposta depende do tipo de cabeçalho Aceitar enviado na solicitação. As solicitações de pesquisa também exigem que `version` seja incluído no cabeçalho Aceitar. A tabela a seguir descreve os cabeçalhos Aceitar disponíveis para pesquisas:

| Aceitar | Descrição |
| ------ | ----------- |
| `application/vnd.adobe.xed-id+json` | Solicitações de lista (GET), títulos, IDs e versões |
| `application/vnd.adobe.xed-full+json; version={major version}` | $refs e allOf resolvidos, têm títulos e descrições |
| `application/vnd.adobe.xed+json; version={major version}` | Simples com $ref e allOf, tem títulos e descrições |
| `application/vnd.adobe.xed-notext+json; version={major version}` | Simples com $ref e allOf, sem títulos ou descrições |
| `application/vnd.adobe.xed-full-notext+json; version={major version}` | $refs e allOf resolvidos, sem títulos ou descrições |
| `application/vnd.adobe.xed-full-desc+json; version={major version}` | $refs e allOf resolvidos, descritores incluídos |

>[!NOTE]
>
>`application/vnd.adobe.xed-id+json` e `application/vnd.adobe.xed-full+json; version={major version}` são os cabeçalhos Aceitar mais usados. `application/vnd.adobe.xed-id+json` é preferido para listar recursos em [!DNL Schema Registry], pois retorna apenas &quot;title&quot;, &quot;id&quot; e &quot;version&quot;. `application/vnd.adobe.xed-full+json; version={major version}` é preferido para a exibição de um recurso específico (por sua &quot;id&quot;), pois retorna todos os campos (aninhados em &quot;propriedades&quot;), bem como títulos e descrições.

**Resposta**

O esquema JSON retornado descreve a estrutura e as informações no nível de campo (&quot;tipo&quot;, &quot;formato&quot;, &quot;mínimo&quot;, &quot;máximo&quot; etc.) dos dados, serializados como JSON. Se estiver usando um formato de serialização diferente de JSON para assimilação (como Parquet ou Scala), o [Guia do Registro de Esquemas](../xdm/tutorials/create-schema-api.md) contém uma tabela que mostra o tipo JSON desejado (&quot;meta:xdmType&quot;) e sua representação correspondente em outros formatos.

Junto com esta tabela, o Guia do Desenvolvedor do [!DNL Schema Registry] contém exemplos detalhados de todas as chamadas possíveis que podem ser feitas usando a API [!DNL Schema Registry].

### Propriedade &quot;esquema&quot; do conjunto de dados (DEPRECATED - EOL 2019-05-30)

Os conjuntos de dados podem conter uma propriedade de &quot;esquema&quot; que agora está obsoleta e permanece disponível temporariamente para compatibilidade com versões anteriores. Por exemplo, uma solicitação de listagem (GET) semelhante à feita anteriormente, em que &quot;schema&quot; foi substituído por &quot;schemaRef&quot; no parâmetro de consulta `properties`, pode retornar o seguinte:

```json
{
  "5ba9452f7de80400007fc52a": {
    "name": "Sample Dataset 1",
    "description": "Description of Sample Dataset 1.",
    "schema": "@/xdms/context/person"
  }
}
```

Se a propriedade &quot;schema&quot; de um conjunto de dados for preenchida, isso indica que o esquema é um esquema `/xdms` obsoleto e, onde houver suporte, o conector ETL deve usar o valor na propriedade &quot;schema&quot; com o ponto de extremidade `/xdms` (um ponto de extremidade obsoleto no [[!DNL Catalog API]](https://www.adobe.io/experience-platform-apis/references/catalog/)) para recuperar o esquema herdado.

**Formato da API**

```http
GET /catalog/{"schema" property without the "@"}
```

**Solicitação**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/xdms/context/person?expansion=xdm" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

>[!NOTE]
>
>Um parâmetro de consulta opcional, `expansion=xdm`, instrui a API a expandir totalmente e embutir todos os esquemas referenciados. Você pode querer fazer isso ao apresentar uma lista de todos os campos em potencial ao usuário.

**Resposta**

Semelhante às etapas para [exibição do esquema do conjunto de dados](#view-dataset-schema), a resposta contém um esquema JSON que descreve a estrutura e as informações no nível de campo dos dados, serializados como JSON.

>[!NOTE]
>
>Quando o campo &quot;schema&quot; estiver vazio ou totalmente ausente, o conector deverá ler o campo &quot;schemaRef&quot; e usar a [API do Registro de Esquema](https://www.adobe.io/experience-platform-apis/references/schema-registry/) como mostrado nas etapas anteriores para [exibir um esquema de conjunto de dados](#view-dataset-schema).

### A propriedade &quot;observableSchema&quot;

A propriedade &quot;observableSchema&quot; de um conjunto de dados tem uma estrutura JSON que corresponde à do JSON do esquema XDM. O &quot;observableSchema&quot; contém os campos que estavam presentes nos arquivos de entrada recebidos. Ao gravar dados em [!DNL Experience Platform], o usuário não precisa usar todos os campos do esquema de destino. Em vez disso, eles devem fornecer apenas os campos que estão sendo usados.

O esquema observável é o esquema que você usaria ao ler os dados ou apresentar uma lista de campos disponíveis para leitura/mapeamento.

```json
{
    "598d6e81b2745f000015edcb": {
        "observableSchema": {
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "name": {
                    "type": "string",
                },
                "age": {
                    "type": "string",
                }
            }
        }
    }
}
```

### Visualizar dados

O aplicativo ETL pode fornecer um recurso para visualizar dados ([&quot;Figura 8&quot; no Fluxo de Trabalho ETL](./workflow.md)). A API de acesso a dados fornece várias opções para visualizar dados.

Informações adicionais, incluindo a orientação passo a passo para a visualização de dados usando a API de acesso a dados, podem ser encontradas no [tutorial sobre acesso a dados](../data-access/tutorials/dataset-data.md).

### Obter detalhes do conjunto de dados usando o parâmetro de consulta &quot;propriedades&quot;

Conforme mostrado nas etapas acima para [exibir uma lista de conjuntos de dados](#view-list-of-datasets), você pode solicitar &quot;arquivos&quot; usando o parâmetro de consulta &quot;propriedades&quot;.

Você pode consultar a [Visão geral do Serviço de Catálogo](../catalog/home.md) para obter informações detalhadas sobre a consulta de conjuntos de dados e filtros de resposta disponíveis.

**Formato da API**

```http
GET /catalog/dataSets?limit={value}&properties={value}
```

**Solicitação**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/dataSets?limit=1&properties=files" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

**Resposta**

A resposta incluirá um conjunto de dados (`limit=1`) mostrando a propriedade &quot;files&quot;.

```json
{
  "5bf479a6a8c862000050e3c7": {
    "files": "@/dataSetFiles?dataSetId=5bf479a6a8c862000050e3c7"
  }
}
```

### Listar arquivos de conjunto de dados usando o atributo &quot;arquivos&quot;

Você também pode usar uma solicitação GET para buscar detalhes do arquivo usando o atributo &quot;arquivos&quot;.

**Formato da API**

```http
GET /catalog/dataSets/{DATASET_ID}/views/{VIEW_ID}/files
```

**Solicitação**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/dataSets/5bf479a6a8c862000050e3c7/views/5bf479a654f52014cfffe7f1/files" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**Resposta**

A resposta inclui a ID do arquivo do conjunto de dados como a propriedade de nível superior, com detalhes do arquivo contidos no objeto da ID do arquivo do conjunto de dados.

```json
{
    "194e89b976494c9c8113b968c27c1472-1": {
        "batchId": "194e89b976494c9c8113b968c27c1472",
        "dataSetViewId": "5bf479a654f52014cfffe7f1",
        "imsOrg": "{ORG_ID}",
        "availableDates": {},
        "createdUser": "{USER_ID}",
        "createdClient": "{API_KEY}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1542749145828,
        "updated": 1542749145828
    },
    "14d5758c107443e1a83c714e56ca79d0-1": {
        "batchId": "14d5758c107443e1a83c714e56ca79d0",
        "dataSetViewId": "5bf479a654f52014cfffe7f1",
        "imsOrg": "{ORG_ID}",
        "availableDates": {},
        "createdUser": "{USER_ID}",
        "createdClient": "{API_KEY}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1542752699111,
        "updated": 1542752699111
    },
    "ea40946ac03140ec8ac4f25da360620a-1": {
        "batchId": "ea40946ac03140ec8ac4f25da360620a",
        "dataSetViewId": "5bf479a654f52014cfffe7f1",
        "imsOrg": "{ORG_ID}",
        "availableDates": {},
        "createdUser": "{USER_ID}",
        "createdClient": "{API_KEY}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1542756935535,
        "updated": 1542756935535
    }
}
```

### Buscar detalhes do arquivo

As IDs de arquivo do conjunto de dados retornadas na resposta anterior podem ser usadas em uma solicitação do GET para buscar mais detalhes do arquivo por meio da API [!DNL Data Access].

A [visão geral sobre acesso a dados](../data-access/home.md) contém detalhes sobre como usar a API [!DNL Data Access].

**Formato da API**

```http
GET /export/files/{DATASET_FILE_ID}
```

**Solicitação**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/ea40946ac03140ec8ac4f25da360620a-1" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**Resposta**

```json
[
    {
    "name": "{FILE_NAME}.parquet",
    "length": 2576,
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/export/files/ea40946ac03140ec8ac4f25da360620a-1?path=samplefile.parquet"
            }
        }
    }
]
```

### Visualizar dados do arquivo

A propriedade &quot;href&quot; pode ser usada para buscar dados de visualização por meio de [[!DNL Data Access API]](../data-access/home.md).

**Formato da API**

```http
GET /export/files/{FILE_ID}?path={FILE_NAME}.{FILE_FORMAT}
```

**Solicitação**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/ea40946ac03140ec8ac4f25da360620a-1?path=samplefile.parquet" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

A resposta à solicitação acima conterá uma visualização do conteúdo do arquivo.

Mais informações sobre a API [!DNL Data Access], incluindo solicitações e respostas detalhadas, estão disponíveis na [visão geral sobre acesso a dados](../data-access/home.md).

### Obter &quot;fileDescription&quot; do conjunto de dados

O componente de destino como saída de dados transformados, o Engenheiro de Dados escolherá um Conjunto de Dados de Saída ([&quot;Figura 12&quot; no Fluxo de Trabalho ETL](workflow.md)). O esquema XDM está associado ao conjunto de dados de saída. Os dados a serem gravados serão identificados pelo atributo &quot;fileDescription&quot; da entidade do conjunto de dados das APIs de Descoberta de Dados. Essas informações podem ser buscadas usando uma ID de conjunto de dados (`{DATASET_ID}`). A propriedade &quot;fileDescription&quot; na resposta JSON fornecerá as informações solicitadas.

**Formato da API**

```shell
GET /catalog/dataSets/{DATASET_ID}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{DATASET_ID}` | O valor `id` do conjunto de dados que você está tentando acessar. |

**Solicitação**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/dataSets/59c93f3da7d0c00000798f68" \
-H "accept: application/json" \
-H "x-gw-ims-org-id: {ORG_ID}" \
-H "x-sandbox-name: {SANDBOX_NAME}" \
-H "Authorization: Bearer {ACCESS_TOKEN}" \
-H "x-api-key: {API_KEY}"
```

**Resposta**

```JSON
{
  "59c93f3da7d0c00000798f68": {
    "version": "1.0.4",
    "fileDescription": {
        "persisted": false,
        "format": "parquet"
    }
  }
}
```

Os dados serão gravados em [!DNL Experience Platform] usando a [API de assimilação em lote](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/).  A gravação de dados é um processo assíncrono. Quando os dados são gravados na Adobe Experience Platform, um lote é criado e marcado como bem-sucedido somente após os dados serem totalmente gravados.

Os dados em [!DNL Experience Platform] devem ser gravados na forma de arquivos Parquet.

## Fase de execução

Conforme a execução é iniciada, o conector (conforme definido no componente de origem) lerá os dados de [!DNL Experience Platform] usando [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/). O processo de transformação lerá os dados de um determinado intervalo de tempo. Internamente, ele consultará lotes de conjuntos de dados de origem. Durante a consulta, ele usará uma data de início parametrizada (rolagem para dados de séries de tempo ou dados incrementais) e listará arquivos de conjunto de dados para esses lotes e começará a fazer solicitações de dados para esses arquivos de conjunto de dados.

### Exemplo de transformações

O documento [transformações ETL de amostra](./transformations.md) contém várias transformações de exemplo, incluindo manipulação de identidade e mapeamentos de tipo de dados. Use essas transformações para referência.

### Ler dados de [!DNL Experience Platform]

Usando o [[!DNL Catalog API]](https://www.adobe.io/experience-platform-apis/references/catalog/), você pode buscar todos os lotes entre uma hora de início e uma hora de término especificadas e classificá-los pela ordem em que foram criados.

**Solicitação**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches?dataSet=DATASETID&createdAfter=START_TIMESTAMP&createdBefore=END_TIMESTAMP&sort=desc:created" \
  -H "Accept: application/json" \
  -H "Authorization:Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

Detalhes sobre a filtragem de lotes podem ser encontrados no [tutorial sobre acesso a dados](../data-access/tutorials/dataset-data.md).

### Obter arquivos de um lote

Depois de ter a ID do lote que você está procurando (`{BATCH_ID}`), é possível recuperar uma lista de arquivos que pertencem a um lote específico por meio do [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/).  Detalhes para fazer isso estão disponíveis no [[!DNL Data Access] tutorial](../data-access/tutorials/dataset-data.md).

**Solicitação**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/files" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

### Acessar arquivos usando a ID do arquivo

Usando o identificador exclusivo de um arquivo (`{FILE_ID`), o [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/) pode ser usado para acessar os detalhes específicos do arquivo, incluindo seu nome, tamanho em bytes e um link para baixá-lo.

**Solicitação**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/{FILE_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

A resposta pode apontar para um único arquivo ou diretório. Detalhes sobre cada um podem ser encontrados no [[!DNL Data Access] tutorial](../data-access/tutorials/dataset-data.md).

### Acessar conteúdo de arquivo

O [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/) pode ser usado para acessar o conteúdo de um arquivo específico. Para buscar o conteúdo, uma solicitação GET é feita usando o valor retornado para `_links.self.href` ao acessar um arquivo usando a ID do arquivo.

**Solicitação**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/{DATASET_FILE_ID}?path=filename1.csv" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

A resposta a essa solicitação contém o conteúdo do arquivo. Para obter mais informações, incluindo detalhes sobre paginação de resposta, consulte o [tutorial Como consultar dados por meio da API de acesso a dados](../data-access/tutorials/dataset-data.md).

### Validar registros para conformidade com esquema

Quando os dados estão sendo gravados, os usuários podem optar por validar os dados de acordo com as regras de validação definidas no esquema XDM. Mais informações sobre validação de esquema podem ser encontradas no [Código de referência de integração de ecossistema ETL em [!DNL GitHub]](https://github.com/adobe/experience-platform-etl-reference/blob/fd08dd9f74ae45b849d5482f645f859f330c1951/README.md#validation).

Se você estiver usando a implementação de referência encontrada em [[!DNL GitHub]](https://github.com/adobe/experience-platform-etl-reference/blob/fd08dd9f74ae45b849d5482f645f859f330c1951/README.md), poderá ativar a validação de esquema nesta implementação usando a propriedade do sistema `-DenableSchemaValidation=true`.

A validação pode ser executada para tipos XDM lógicos, usando atributos como `minLength` e `maxlength` para cadeias de caracteres, `minimum` e `maximum` para inteiros e muito mais. O [guia do desenvolvedor da API do Registro de Esquema](../xdm/api/getting-started.md) contém uma tabela que descreve os tipos XDM e as propriedades que podem ser usadas para validação.

>[!NOTE]
>
>Os valores mínimo e máximo fornecidos para vários tipos `integer` são os valores MIN e MAX que o tipo pode suportar, mas esses valores podem ser restritos ainda mais aos mínimos e máximos de sua escolha.

### Criar um lote

Depois que os dados forem processados, a ferramenta ETL gravará os dados em [!DNL Experience Platform] usando a [API de assimilação em lote](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/). Antes de serem adicionados a um conjunto de dados, os dados devem estar vinculados a um lote que será carregado posteriormente em um conjunto de dados específico.

**Solicitação**

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -d '{
        "datasetId":"{DATASET_ID}"
      }'
```

Detalhes para criar um lote, incluindo solicitações e respostas de exemplo, podem ser encontrados na [Visão geral de Assimilação em lote](../ingestion/batch-ingestion/overview.md).

### Gravar no conjunto de dados

Depois de criar um novo lote com êxito, os arquivos podem ser carregados para um conjunto de dados específico. Vários arquivos podem ser publicados em um lote até que ele seja promovido. Os arquivos podem ser carregados usando a API de Upload de Arquivo Pequeno. No entanto, se os arquivos forem muito grandes e o limite do gateway for excedido, você poderá usar a API de Upload de Arquivo Grande. Detalhes para usar o Upload de arquivos grandes e pequenos podem ser encontrados na [Visão geral de Assimilação em lote](../ingestion/batch-ingestion/overview.md).

**Solicitação**

Os dados em [!DNL Experience Platform] devem ser gravados na forma de arquivos Parquet.

```shell
curl -X PUT "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/dataSets/{DATASET_ID}/files/{FILE_NAME}.parquet" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id:{ORG_ID}" \
  -H "Authorization:Bearer ACCESS_TOKEN" \
  -H "x-api-key: API_KEY" \
  -H "content-type: application/octet-stream" \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

### Marcar carregamento em lote como concluído

Depois que todos os arquivos tiverem sido carregados no lote, o lote poderá ser marcado para conclusão. Ao fazer isso, as [!DNL Catalog] entradas &quot;DataSetFile&quot; são criadas para os arquivos concluídos e associadas ao lote de geração. O lote [!DNL Catalog] é marcado como bem-sucedido, o que aciona fluxos downstream para assimilar os dados disponíveis.

Os dados serão encaminhados primeiro para o local de preparo no Adobe Experience Platform e depois serão movidos para o local final após a catalogação e a validação. Os lotes serão marcados como bem-sucedidos assim que todos os dados forem movidos para um local permanente.

**Solicitação**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization:Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

Se bem-sucedido, a resposta retornará o Status HTTP 200 OK e o corpo da resposta estará vazio.

A ferramenta ETL observará o carimbo de data e hora dos conjuntos de dados de origem à medida que os dados são lidos.

Na próxima execução de transformação, provavelmente por agendamento ou invocação de evento, o ETL começará a solicitar os dados do carimbo de data e hora salvo anteriormente e de todos os dados a partir de agora.

### Obter status do último lote

Antes de executar novas tarefas na ferramenta ETL, verifique se o último lote foi concluído com êxito. O [[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/) fornece uma opção específica de lote que fornece os detalhes dos lotes relevantes.

**Solicitação**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches?limit=1&sort=desc:created" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**Resposta**

Novas tarefas podem ser agendadas se o valor anterior do lote &quot;status&quot; for &quot;sucesso&quot;, conforme mostrado abaixo:

```json
"{BATCH_ID}": {
    "imsOrg": "{ORG_ID}",
    "created": 1494349962314,
    "createdClient": "{API_KEY}",
    "createdUser": "CLIENT_USER_ID@AdobeID",
    "updatedUser": "CLIENT_USER_ID@AdobeID",
    "updated": 1494349963467,
    "status": "success",
    "errors": [],
    "version": "1.0.1",
    "availableDates": {}
}
```

### Obter o status do último lote por ID

Um status de lote individual pode ser recuperado por meio de [[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/) emitindo uma solicitação GET usando o `{BATCH_ID}`. O `{BATCH_ID}` usado seria o mesmo que a ID retornada quando o lote foi criado.

**Solicitação**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches/{BATCH_ID}" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**Resposta - Êxito**

A resposta a seguir mostra um &quot;sucesso&quot;:

```json
"{BATCH_ID}": {
    "imsOrg": "{ORG_ID}",
    "created": 1494349962314,
    "createdClient": "{API_KEY}",
    "createdUser": "{CREATED_USER}",
    "updatedUser": "{UPDATED_USER}",
    "updated": 1494349962314,
    "status": "success",
    "errors": [],
    "version": "1.0.1",
    "availableDates": {}
}
```

**Resposta - Falha**

Em caso de falha, os &quot;erros&quot; podem ser extraídos da resposta e exibidos na ferramenta ETL como mensagens de erro.

```json
"{BATCH_ID}": {
    "imsOrg": "{ORG_ID}",
    "created": 1494349962314,
    "createdClient": "{API_KEY}",
    "createdUser": "{CREATED_USER}",
    "updatedUser": "{UPDATED_USER}",
    "updated": 1494349962314,
    "status": "failure",
    "errors": [
        {
            "code": "200",
            "description": "Error in validating schema for file: 'adl://dataLake.azuredatalakestore.net/connectors-dev/stage/BATCHID/dataSetId/contact.csv' with errorMessage=adl://dataLake.azuredatalakestore.net/connectors-dev/stage/BATCHID/dataSetId/contact.csv is not a Parquet file. expected magic number at tail [80, 65, 82, 49] but found [57, 98, 55, 10] and errorType=java.lang.RuntimeException",
            "rows": []
        }
    ],
    "version": "1.0.1",
    "availableDates": {}
}
```

## Dados e eventos incrementais vs. instantâneos versus perfis

Os dados podem ser representados numa matriz dois por dois da seguinte forma:

| Eventos incrementais | Perfis incrementais |
|-------------------------------|----------------------|
| Eventos de snapshot (menos provável) | Perfis de instantâneo |

Os dados do evento normalmente são quando há colunas de carimbo de data e hora indexadas em cada linha.

Normalmente, os dados de perfil são usados quando não há um carimbo de data e hora nos dados e cada linha pode ser identificada por uma chave primária/composta.

Os dados incrementais são o local em que somente dados novos/atualizados entram no sistema e são anexados aos dados atuais nos conjuntos de dados.

Dados de instantâneo são quando todos os dados entram no sistema e substituem alguns ou todos os dados anteriores em um conjunto de dados.

No caso de eventos incrementais, a ferramenta ETL deve usar as datas disponíveis/data de criação da entidade de lote. No caso do serviço de push, as datas disponíveis não estarão presentes, portanto, a ferramenta usará a data de criação/atualização do lote para marcar incrementos. Cada lote de eventos incrementais deve ser processado.

Para perfis incrementais, a ferramenta ETL usará datas criadas/atualizadas da entidade de lote. Geralmente, cada lote de dados de perfil incrementais precisa ser processado.

Os eventos de snapshot têm menos probabilidade devido ao tamanho total dos dados. Mas se isso for necessário, a ferramenta ETL deverá selecionar somente o último lote para processamento.

Quando perfis de instantâneo forem usados, a ferramenta ETL terá que escolher o último lote dos dados que chegaram ao sistema. Mas se o requisito for rastrear as versões das alterações, todos os lotes precisarão ser processados. O processamento da eliminação de duplicação no processo ETL ajudará a controlar os custos de armazenamento.

## Repetição em lote e reprocessamento de dados

A repetição em lote e o reprocessamento de dados podem ser necessários nos casos em que um cliente descobrir que, nos últimos &quot;n&quot; dias, os dados que estão sendo processados pelo ETL não ocorreram conforme esperado ou os dados de origem podem não estar corretos.

Para fazer isso, os administradores de dados do cliente usarão a interface do usuário do [!DNL Experience Platform] para remover os lotes que contêm dados corrompidos. Em seguida, o ETL provavelmente precisará ser executado novamente, preenchendo novamente com dados corretos. Se a própria fonte tiver dados corrompidos, o engenheiro/administrador de dados precisará corrigir os lotes de origem e assimilar novamente os dados (no Adobe Experience Platform ou por meio de conectores ETL).

Com base no tipo de dados gerado, será a escolha do engenheiro de dados remover um único lote ou todos os lotes de determinados conjuntos de dados. Os dados serão removidos/arquivados de acordo com as diretrizes de [!DNL Experience Platform].

É um cenário provável de que a funcionalidade ETL para limpar dados seja importante.

Quando a limpeza for concluída, os administradores do cliente precisarão reconfigurar o Adobe Experience Platform para reiniciar o processamento dos serviços principais a partir do momento em que os lotes forem excluídos.

## Processamento em lote simultâneo

A critério do cliente, os administradores/engenheiros de dados podem decidir extrair, transformar e carregar dados de maneira sequencial ou simultânea, dependendo das características de um conjunto de dados específico. Isso também se baseará no caso de uso para o qual o cliente está direcionando com os dados transformados.

Por exemplo, se o cliente persistir em um armazenamento de persistência atualizável e a sequência ou a ordem dos eventos for importante, o cliente poderá precisar processar estritamente os trabalhos com transformações ETL sequenciais.

Em outros casos, dados fora de ordem podem ser processados por aplicativos/processos downstream que classificam internamente usando um carimbo de data e hora especificado. Nesses casos, as transformações ETL paralelas podem ser viáveis para melhorar os tempos de processamento.

Para lotes de origem, ele dependerá novamente da preferência do cliente e da restrição do consumidor. Se os dados de origem puderem ser coletados em paralelo, independentemente da regência/ordem de uma linha, o processo de transformação poderá criar lotes de processos com um grau mais alto de paralelismo (otimização baseada no processamento fora de ordem). Mas se a transformação precisar respeitar carimbos de data e hora ou alterar a ordem de precedência, o agendador/invocador de ferramentas da API de acesso a dados ou ETL terá que garantir que os lotes não sejam processados fora de ordem, quando possível.

## Adiamento

Adiamento é um processo no qual os dados de entrada ainda não estão completos o suficiente para serem enviados aos processos de downstream, mas podem ser utilizáveis no futuro. Os clientes determinarão sua tolerância individual à janela de dados para correspondência futura em relação ao custo do processamento para informar sua decisão de deixar os dados de lado e reprocessá-los na próxima execução de transformação, esperando que eles possam ser enriquecidos e reconciliados/compilados em algum momento futuro dentro da janela de retenção. Esse ciclo está em andamento até que a linha seja processada o suficiente ou considerada muito obsoleta para continuar investindo no. Cada iteração gerará dados adiados, que são um superconjunto de todos os dados adiados em iterações anteriores.

A Adobe Experience Platform não identifica dados adiados no momento, portanto, as implementações de clientes devem confiar nas configurações manuais de ETL e Conjunto de Dados para criar outro conjunto de dados em [!DNL Experience Platform], espelhando o conjunto de dados de origem, que pode ser usado para manter os dados adiados. Nesse caso, os dados adiados serão semelhantes aos dados do instantâneo. Em cada execução da transformação ETL, os dados de origem serão unidos aos dados adiados e enviados para processamento.

## Changelog

| Data | Ação | Descrição |
| ---- | ------ | ----------- |
| 19/01/2019 | Propriedade &quot;fields&quot; removida dos conjuntos de dados | Anteriormente, os conjuntos de dados incluíam uma propriedade &quot;fields&quot; que continha uma cópia do esquema. Esse recurso não deve mais ser usado. Se a propriedade &quot;fields&quot; for encontrada, ela deverá ser ignorada e &quot;observedSchema&quot; ou &quot;schemaRef&quot; deverá ser usado em seu lugar. |
| 03-2019-15 | Propriedade &quot;schemaRef&quot; adicionada aos conjuntos de dados | A propriedade &quot;schemaRef&quot; de um conjunto de dados contém um URI que faz referência ao esquema XDM no qual o conjunto de dados se baseia e representa todos os campos potenciais que podem ser usados pelo conjunto de dados. |
| 03-2019-15 | Todos os identificadores do usuário final são mapeados para a propriedade &quot;identityMap&quot; | O &quot;identityMap&quot; é um encapsulamento de todos os identificadores exclusivos de um assunto, como CRMID, ECID ou ID do programa de fidelidade. Este mapa é usado por [[!DNL Identity Service]](../identity-service/home.md) para resolver todas as identidades conhecidas e anônimas de um assunto, formando um único gráfico de identidade para cada usuário final. |
| 30/05/2019 | EOL e remover a propriedade &quot;schema&quot; dos conjuntos de dados | A propriedade &quot;schema&quot; do conjunto de dados forneceu um link de referência para o esquema usando o ponto de extremidade `/xdms` obsoleto na API [!DNL Catalog]. Isso foi substituído por um &quot;schemaRef&quot; que fornece a &quot;id&quot;, &quot;version&quot; e &quot;contentType&quot; do esquema conforme referenciado na nova API [!DNL Schema Registry]. |
