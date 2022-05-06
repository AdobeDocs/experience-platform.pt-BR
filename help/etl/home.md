---
keywords: Experience Platform, home, tópicos populares, ETL, etl, integrações etl, integrações ETL
solution: Experience Platform
title: Desenvolvimento de integrações de ETL para o Adobe Experience Platform
topic-legacy: overview
description: O guia de integração ETL descreve as etapas gerais para criar conectores seguros e de alto desempenho para o Experience Platform e assimilar dados na plataforma.
exl-id: 7d29b61c-a061-46f8-a31f-f20e4d725655
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '4075'
ht-degree: 1%

---

# Desenvolvimento de integrações de ETL para o Adobe Experience Platform

O guia de integração ETL descreve as etapas gerais para criar conectores seguros e de alto desempenho para [!DNL Experience Platform] e assimilação de dados em [!DNL Platform].


- [[!DNL Catalog]](https://www.adobe.io/experience-platform-apis/references/catalog/)
- [[!DNL Data Access]](https://www.adobe.io/experience-platform-apis/references/data-access/)
- [[!DNL Data Ingestion]](https://www.adobe.io/experience-platform-apis/references/data-ingestion/)
- [Autenticação e autorização para APIs do Experience Platform](https://www.adobe.com/go/platform-api-authentication-en)
- [[!DNL Schema Registry]](https://www.adobe.io/experience-platform-apis/references/schema-registry/)

Este guia também inclui exemplos de chamadas de API a serem usadas ao projetar um conector ETL, com links para a documentação que descreve cada [!DNL Experience Platform] e o uso de sua API, com mais detalhes.

Uma amostra de integração está disponível em [!DNL GitHub] através da [Código de referência de integração do ecossistema ETL](https://github.com/adobe/acp-data-services-etl-reference) nos termos do [!DNL Apache] Licença versão 2.0.

## Fluxo de trabalho

O diagrama de workflow a seguir fornece uma visão geral de alto nível para a integração de componentes do Adobe Experience Platform com um aplicativo e conector ETL.

![](images/etl.png)

## Componentes do Adobe Experience Platform

Há vários componentes do Experience Platform envolvidos nas integrações do conector ETL. A lista a seguir descreve vários componentes e funcionalidades principais:

- **Sistema Adobe Identity Management (IMS)** - Fornece a estrutura para autenticação para os serviços da Adobe.
- **IMS Organization** - Uma entidade empresarial que possa possuir ou licenciar produtos e serviços e permitir o acesso aos seus membros.
- **Usuário IMS** - Membros de uma Organização IMS. A relação Organização-Usuário é de muitas para muitas.
- **[!DNL Sandbox]** - Uma partição virtual uma única [!DNL Platform] , para ajudar a desenvolver aplicativos de experiência digital.
- **Descoberta de dados** - Registra os metadados de dados assimilados e transformados em [!DNL Experience Platform].
- **[!DNL Data Access]** - Fornece aos usuários uma interface para acessar seus dados em [!DNL Experience Platform].
- **[!DNL Data Ingestion]** - Empurra dados para [!DNL Experience Platform] com [!DNL Data Ingestion] APIs.
- **[!DNL Schema Registry]** - Define e armazena um esquema que descreve a estrutura dos dados a serem usados em [!DNL Experience Platform].

## Introdução ao [!DNL Experience Platform] APIs

As seções a seguir fornecem informações adicionais que você precisará saber ou ter em mãos para fazer chamadas para o [!DNL Experience Platform] APIs.

### Lendo exemplos de chamadas de API

Este guia fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações do . Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de exemplo retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler exemplos de chamadas de API](../landing/troubleshooting.md#how-do-i-format-an-api-request) no [!DNL Experience Platform] guia de solução de problemas.

### Coletar valores para cabeçalhos necessários

Para fazer chamadas para [!DNL Platform] As APIs devem ser concluídas primeiro [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todos [!DNL Experience Platform] Chamadas de API, conforme mostrado abaixo:

- Autorização: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Todos os recursos em [!DNL Experience Platform] são isoladas em sandboxes virtuais específicas. Todas as solicitações para [!DNL Platform] As APIs exigem um cabeçalho que especifica o nome da sandbox em que a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre sandboxes em [!DNL Platform], consulte o [documentação de visão geral da sandbox](../sandboxes/home.md).

Todas as solicitações que contêm uma carga útil (POST, PUT, PATCH) exigem um cabeçalho adicional:

- Tipo de conteúdo: application/json

## Fluxo geral do usuário

Para começar, um usuário de ETL faz logon no [!DNL Experience Platform] interface do usuário (UI) e cria conjuntos de dados para assimilação usando um conector padrão ou um conector de serviço de push.

Na interface do usuário, o usuário cria o conjunto de dados de saída selecionando um esquema de conjunto de dados. A escolha do schema depende do tipo de dados (registro ou série de tempo) que está sendo assimilado no [!DNL Platform]. Ao clicar na guia Schemas na interface do usuário, o usuário poderá exibir todos os esquemas disponíveis, incluindo o tipo de comportamento compatível com o esquema.

Na ferramenta ETL, o usuário começará a projetar suas transformações de mapeamento após configurar a conexão apropriada (usando suas credenciais). Pressupõe-se que a ferramenta ETL já tenha [!DNL Experience Platform] conectores instalados (processo não definido neste Guia de Integração).

Os modelos para uma ferramenta ETL de amostra e o fluxo de trabalho foram fornecidos na [Fluxo de trabalho ETL](./workflow.md). Embora as ferramentas ETL possam diferir no formato, a maioria expõe funcionalidade semelhante.

>[!NOTE]
>
>O conector ETL deve especificar um filtro de carimbo de data/hora que marque a data para assimilar dados e deslocamento (ou seja, a janela para a qual os dados devem ser lidos). A ferramenta ETL deve suportar a inclusão desses dois parâmetros nesta ou em outra interface de usuário relevante. No Adobe Experience Platform, esses parâmetros serão mapeados para datas disponíveis (se presentes) ou para a data capturada presente no objeto de lote do conjunto de dados.

### Exibir lista de conjuntos de dados

Usando a fonte de dados para mapeamento, é possível buscar uma lista de todos os conjuntos de dados disponíveis usando o [[!DNL Catalog API]](https://www.adobe.io/experience-platform-apis/references/catalog/).

Você pode emitir uma única solicitação de API para exibir todos os conjuntos de dados disponíveis (por exemplo, `GET /dataSets`), com a prática recomendada é incluir parâmetros de consulta que limitam o tamanho da resposta.

Nos casos em que informações completas do conjunto de dados estão sendo solicitadas, a carga da resposta pode atingir mais de 3 GB, o que pode retardar o desempenho geral. Portanto, usar parâmetros de consulta para filtrar somente as informações necessárias fará [!DNL Catalog] consultas mais eficientes.

#### Filtragem de lista

Ao filtrar respostas, você pode usar vários filtros em uma única chamada ao separar parâmetros com um E comercial (`&`). Alguns parâmetros de consulta aceitam listas de valores separadas por vírgulas, como o filtro &quot;propriedades&quot; na solicitação de amostra abaixo.

[!DNL Catalog] as respostas são medidas automaticamente de acordo com os limites configurados, no entanto, o parâmetro de consulta &quot;limite&quot; pode ser usado para personalizar as restrições e limitar o número de objetos retornados. O pré-configurado [!DNL Catalog] os limites de resposta são:

- Se um parâmetro de limite não for especificado, o número máximo de objetos por carga de resposta será 20.
- O limite global para todos os outros [!DNL Catalog] consultas são 100 objetos.
- Para consultas de conjunto de dados, se observableSchema for solicitado usando o parâmetro de consulta de propriedades, o número máximo de conjuntos de dados retornados será 20.
- Parâmetros de limite inválidos (incluindo `limit=0`) são atendidas com um erro HTTP 400 que descreve intervalos adequados.
- Se os limites ou deslocamentos forem passados como parâmetros de consulta, eles terão precedência sobre os passados como cabeçalhos.

Os parâmetros de query são abordados com mais detalhes na seção [Visão geral do serviço de catálogo](../catalog/home.md).

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

Consulte a [Visão geral do serviço de catálogo](../catalog/home.md) para obter exemplos detalhados de como fazer chamadas para o [[!DNL Catalog API]](https://www.adobe.io/experience-platform-apis/references/catalog/).

**Resposta**

A resposta inclui três (`limit=3`) conjuntos de dados que mostram &quot;nome&quot;, &quot;descrição&quot; e &quot;schemaRef&quot;, conforme indicado pelo `properties` parâmetro de consulta.

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

A propriedade &quot;schemaRef&quot; de um conjunto de dados contém um URI que faz referência ao esquema XDM no qual o conjunto de dados se baseia. O esquema XDM (&quot;schemaRef&quot;) representa todos os campos em potencial que podem ser usados pelo conjunto de dados, não necessariamente os campos que estão sendo usados (consulte &quot;observableSchema&quot; abaixo).

O esquema XDM é o esquema usado quando é necessário apresentar ao usuário uma lista de todos os campos disponíveis que podem ser gravados.

O primeiro valor &quot;schemaRef.id&quot; no objeto de resposta anterior (`https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18`) é um URI que aponta para um esquema XDM específico na [!DNL Schema Registry]. O esquema pode ser recuperado fazendo uma solicitação de pesquisa (GET) para o [!DNL Schema Registry] API.

>[!NOTE]
>
>A propriedade &quot;schemaRef&quot; substitui a propriedade &quot;schema&quot;, agora obsoleta. Se &quot;schemaRef&quot; estiver ausente do conjunto de dados ou não contiver um valor, será necessário verificar a presença de uma propriedade &quot;schema&quot;. Isso pode ser feito substituindo &quot;schemaRef&quot; por &quot;schema&quot; no `properties` parâmetro de consulta na chamada anterior. Mais detalhes sobre a propriedade &quot;schema&quot; estão disponíveis na variável [Propriedade &quot;schema&quot; do conjunto de dados](#dataset-schema-property-deprecated---eol-2019-05-30) que se segue.

**Formato da API**

```http
GET /schemaregistry/tenant/schemas/{url encoded schemaRef.id}
```

**Solicitação**

A solicitação usa o URL codificado `id` URI do schema (o valor do atributo &quot;schemaRef.id&quot;) e requer um cabeçalho Accept .

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F274f17bc5807ff307a046bab1489fb18 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1' \
```

O formato de resposta depende do tipo de cabeçalho Accept enviado na solicitação. As solicitações de pesquisa também exigem uma `version` ser incluído no cabeçalho Accept . A tabela a seguir descreve os cabeçalhos Aceitos disponíveis para pesquisas:

| Accept | Descrição |
| ------ | ----------- |
| `application/vnd.adobe.xed-id+json` | Listar solicitações (GET), títulos, ids e versões |
| `application/vnd.adobe.xed-full+json; version={major version}` | $refs e allOf resolvidos, tem títulos e descrições |
| `application/vnd.adobe.xed+json; version={major version}` | Bruto com $ref e allOf, tem títulos e descrições |
| `application/vnd.adobe.xed-notext+json; version={major version}` | Simples com $ref e allOf, sem títulos ou descrições |
| `application/vnd.adobe.xed-full-notext+json; version={major version}` | $refs e allOf resolvidos, sem títulos ou descrições |
| `application/vnd.adobe.xed-full-desc+json; version={major version}` | $refs e allOf resolvidos, descritores incluídos |

>[!NOTE]
>
>`application/vnd.adobe.xed-id+json` e `application/vnd.adobe.xed-full+json; version={major version}` são os cabeçalhos Accept mais usados. `application/vnd.adobe.xed-id+json` é preferível para listar recursos no [!DNL Schema Registry] já que retorna somente o &quot;título&quot;, &quot;id&quot; e &quot;versão&quot;. `application/vnd.adobe.xed-full+json; version={major version}` é preferível para visualizar um recurso específico (por sua &quot;id&quot;), pois retorna todos os campos (aninhados em &quot;propriedades&quot;), bem como títulos e descrições.

**Resposta**

O esquema JSON retornado descreve a estrutura e as informações de nível de campo (&quot;type&quot;, &quot;format&quot;, &quot;Minimum&quot;, &quot;maximum&quot; etc.) dos dados, serializado como JSON. Se estiver usando um formato de serialização diferente de JSON para assimilação (como Parquet ou Scala), a variável [Guia do Registro de Schema](../xdm/tutorials/create-schema-api.md) contém uma tabela que mostra o tipo JSON desejado (&quot;meta:xdmType&quot;) e sua representação correspondente em outros formatos.

Junto com esta tabela, a [!DNL Schema Registry] O Guia do desenvolvedor contém exemplos detalhados de todas as chamadas possíveis que podem ser feitas usando o [!DNL Schema Registry] API.

### Propriedade &quot;schema&quot; do conjunto de dados (OBSOLETO - EOL 2019-05-30)

Os conjuntos de dados podem conter uma propriedade &quot;schema&quot; que agora está obsoleta e permanece disponível temporariamente para compatibilidade com versões anteriores. Por exemplo, uma solicitação de listagem (GET) semelhante à feita anteriormente, onde &quot;schema&quot; foi substituído por &quot;schemaRef&quot; no `properties` parâmetro de consulta , pode retornar o seguinte:

```json
{
  "5ba9452f7de80400007fc52a": {
    "name": "Sample Dataset 1",
    "description": "Description of Sample Dataset 1.",
    "schema": "@/xdms/context/person"
  }
}
```

Se a propriedade &quot;schema&quot; de um conjunto de dados for preenchida, isso indicará que o schema está obsoleto `/xdms` e, quando suportado, o conector ETL deve usar o valor na propriedade &quot;schema&quot; com a variável `/xdms` endpoint (um endpoint obsoleto na função [[!DNL Catalog API]](https://www.adobe.io/experience-platform-apis/references/catalog/)) para recuperar o schema herdado.

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
>Um parâmetro de consulta opcional, `expansion=xdm`informa à API para expandir e incorporar completamente todos os esquemas referenciados. Talvez você queira fazer isso ao apresentar uma lista de todos os campos em potencial ao usuário.

**Resposta**

Semelhante às etapas para [como visualizar o esquema do conjunto de dados](#view-dataset-schema), a resposta contém um esquema JSON que descreve a estrutura e as informações de nível de campo dos dados, serializadas como JSON.

>[!NOTE]
>
>Quando o campo &quot;schema&quot; estiver vazio ou ausente totalmente, o conector deverá ler o campo &quot;schemaRef&quot; e usar o [API do Registro de Schema](https://www.adobe.io/experience-platform-apis/references/schema-registry/) conforme mostrado nas etapas anteriores para [exibir um esquema de conjunto de dados](#view-dataset-schema).

### A propriedade &quot;observableSchema&quot;

A propriedade &quot;observableSchema&quot; de um conjunto de dados tem uma estrutura JSON correspondente à do JSON do esquema XDM. O &quot;observableSchema&quot; contém os campos que estavam presentes nos arquivos de entrada. Ao gravar dados em [!DNL Experience Platform], um usuário não é obrigado a usar todos os campos do schema de destino. Em vez disso, eles devem fornecer apenas os campos que estão sendo usados.

O schema observável é o schema que você usaria ao ler os dados ou apresentar uma lista de campos disponíveis para ler/mapear.

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

O aplicativo ETL pode fornecer uma capacidade de visualização de dados ([&quot;Figura 8&quot; no workflow ETL](./workflow.md)). A API de acesso aos dados fornece várias opções para a visualização dos dados.

Informações adicionais, incluindo orientação passo a passo para a visualização de dados usando a API de acesso aos dados, podem ser encontradas no [tutorial de acesso a dados](../data-access/tutorials/dataset-data.md).

### Obter detalhes do conjunto de dados usando o parâmetro de consulta &quot;propriedades&quot;

Conforme mostrado nas etapas acima para [exibir uma lista de conjuntos de dados](#view-list-of-datasets), é possível solicitar &quot;arquivos&quot; usando o parâmetro de consulta &quot;propriedades&quot;.

Você pode fazer referência à variável [Visão geral do serviço de catálogo](../catalog/home.md) para obter informações detalhadas sobre consultas de conjuntos de dados e filtros de resposta disponíveis.

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
    "files": "@/dataSets/5bf479a6a8c862000050e3c7/views/5bf479a654f52014cfffe7f1/files"
  }
}
```

### Listar arquivos do conjunto de dados usando o atributo &quot;arquivos&quot;

Também é possível usar uma solicitação do GET para buscar detalhes do arquivo usando o atributo &quot;files&quot;.

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

A resposta inclui a ID do arquivo do conjunto de dados como a propriedade de nível superior, com detalhes do arquivo contidos no objeto de ID do arquivo do conjunto de dados.

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

As IDs de arquivo do conjunto de dados retornadas na resposta anterior podem ser usadas em uma solicitação do GET para buscar mais detalhes do arquivo por meio do [!DNL Data Access] API.

O [visão geral do acesso aos dados](../data-access/home.md) contém detalhes sobre como usar o [!DNL Data Access] API.

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

A propriedade &quot;href&quot; pode ser usada para buscar dados de visualização por meio do [[!DNL Data Access API]](../data-access/home.md).

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

A resposta à solicitação acima conterá uma pré-visualização do conteúdo do arquivo.

Mais informações sobre o [!DNL Data Access] A API, incluindo solicitações e respostas detalhadas, está disponível na variável [visão geral do acesso aos dados](../data-access/home.md).

### Obter &quot;fileDescription&quot; do conjunto de dados

O componente de destino como saída de dados transformados, o Engenheiro de Dados escolherá um Conjunto de Dados de Saída ([&quot;Figura 12&quot; no workflow ETL](workflow.md)). O esquema XDM está associado ao conjunto de dados de saída. Os dados a serem gravados serão identificados pelo atributo &quot;fileDescription&quot; da entidade do conjunto de dados das APIs de Descoberta de Dados. Essas informações podem ser buscadas usando uma ID de conjunto de dados (`{DATASET_ID}`). A propriedade &quot;fileDescription&quot; na resposta JSON fornecerá as informações solicitadas.

**Formato da API**

```shell
GET /catalog/dataSets/{DATASET_ID}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{DATASET_ID}` | O `id` valor do conjunto de dados que você está tentando acessar. |

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

Os dados serão gravados em [!DNL Experience Platform] usar [API de assimilação de dados](https://www.adobe.io/experience-platform-apis/references/data-ingestion/).  A gravação de dados é um processo assíncrono. Quando os dados são gravados no Adobe Experience Platform, um lote é criado e marcado como um sucesso somente após os dados serem totalmente gravados.

Entrada de dados [!DNL Experience Platform] deve ser gravado na forma de arquivos Parquet.

## Fase de execução

Conforme a execução é iniciada, o conector (conforme definido no componente de origem) lerá os dados de [!DNL Experience Platform] usando o [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/). O processo de transformação lerá os dados de um determinado intervalo de tempo. Internamente, ele consultará lotes de conjuntos de dados de origem. Ao fazer consultas, ele usará uma data inicial parametrizada (rolando para dados de séries de tempo ou dados incrementais) e listará arquivos de conjunto de dados para esses lotes e começará a fazer solicitações de dados para esses arquivos de conjunto de dados.

### Exemplos de transformações

O [amostras de transformações de ETL](./transformations.md) O documento contém várias transformações de exemplo, incluindo manuseio de identidade e mapeamentos de tipo de dados. Use essas transformações para referência.

### Ler dados de [!DNL Experience Platform]

Usar o [[!DNL Catalog API]](https://www.adobe.io/experience-platform-apis/references/catalog/), é possível buscar todos os lotes entre uma hora inicial e uma hora final especificadas e classificá-los pela ordem em que foram criados.

**Solicitação**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches?dataSet=DATASETID&createdAfter=START_TIMESTAMP&createdBefore=END_TIMESTAMP&sort=desc:created" \
  -H "Accept: application/json" \
  -H "Authorization:Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

Os detalhes sobre os lotes de filtragem podem ser encontrados na variável [Tutorial de acesso a dados](../data-access/tutorials/dataset-data.md).

### Obter arquivos de um lote

Depois de ter a ID do lote, você está procurando (`{BATCH_ID}`), é possível recuperar uma lista de arquivos pertencentes a um lote específico por meio do [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/).  Os detalhes para isso estão disponíveis na seção [[!DNL Data Access] tutorial](../data-access/tutorials/dataset-data.md).

**Solicitação**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/files" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

### Acessar arquivos usando a ID do arquivo

Usar a ID exclusiva de um arquivo (`{FILE_ID`), [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/) O pode ser usado para acessar os detalhes específicos do arquivo, incluindo seu nome, tamanho em bytes e um link para baixá-lo.

**Solicitação**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/{FILE_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

A resposta pode apontar para um único arquivo ou um diretório. Os detalhes de cada um podem ser encontrados no [[!DNL Data Access] tutorial](../data-access/tutorials/dataset-data.md).

### Acessar conteúdo do arquivo

O [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/) pode ser usada para acessar o conteúdo de um arquivo específico. Para buscar o conteúdo, uma solicitação do GET é feita usando o valor retornado para `_links.self.href` ao acessar um arquivo usando a ID do arquivo.

**Solicitação**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/{DATASET_FILE_ID}?path=filename1.csv" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

A resposta a essa solicitação contém o conteúdo do arquivo . Para obter mais informações, incluindo detalhes sobre a paginação da resposta, consulte o [Como consultar dados por meio da API de acesso a dados](../data-access/tutorials/dataset-data.md) tutorial.

### Validar registros para conformidade de esquema

Quando os dados são gravados, os usuários podem optar por validar os dados de acordo com as regras de validação definidas no esquema XDM. Mais informações sobre a validação do esquema podem ser encontradas na [Código de referência de integração do ecossistema ETL em [!DNL GitHub]](https://github.com/adobe/experience-platform-etl-reference/blob/fd08dd9f74ae45b849d5482f645f859f330c1951/README.md#validation).

Se estiver usando a implementação de referência encontrada em [[!DNL GitHub]](https://github.com/adobe/experience-platform-etl-reference/blob/fd08dd9f74ae45b849d5482f645f859f330c1951/README.md), você pode ativar a validação de esquema nesta implementação usando a propriedade do sistema `-DenableSchemaValidation=true`.

A validação pode ser executada para tipos XDM lógicos, usando atributos como `minLength` e `maxlength` para cadeias de caracteres, `minimum` e `maximum` para números inteiros e muito mais. O [Guia do desenvolvedor da API da API do Registro de Schema](../xdm/api/getting-started.md) contém uma tabela que descreve os tipos XDM e as propriedades que podem ser usadas para validação.

>[!NOTE]
>
>Os valores mínimo e máximo previstos para os diversos `integer` são os valores MIN e MAX que o tipo pode suportar, mas esses valores podem ser restritos ainda mais aos mínimos e máximos de sua escolha.

### Criar um lote

Depois que os dados forem processados, a ferramenta ETL gravará os dados de volta para [!DNL Experience Platform] usando o [API de assimilação em lote](https://www.adobe.io/experience-platform-apis/references/data-ingestion/). Antes de serem adicionados a um conjunto de dados, os dados devem ser vinculados a um lote que será carregado posteriormente em um conjunto de dados específico.

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

Detalhes para criar um lote, incluindo solicitações e respostas de amostra, podem ser encontrados no [Visão geral da Assimilação em lote](../ingestion/batch-ingestion/overview.md).

### Gravar no conjunto de dados

Depois de criar um novo lote com êxito, os arquivos podem ser carregados em um conjunto de dados específico. Vários arquivos podem ser publicados em um lote até que sejam promovidos. Os arquivos podem ser carregados usando a API de upload de arquivo pequeno; no entanto, se os arquivos forem muito grandes e o limite do gateway for excedido, você poderá usar a API de upload de arquivo grande. Os detalhes para usar o Upload de arquivo grande e pequeno podem ser encontrados no [Visão geral da Assimilação em lote](../ingestion/batch-ingestion/overview.md).

**Solicitação**

Entrada de dados [!DNL Experience Platform] deve ser gravado na forma de arquivos Parquet.

```shell
curl -X PUT "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/dataSets/{DATASET_ID}/files/{FILE_NAME}.parquet" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id:{ORG_ID}" \
  -H "Authorization:Bearer ACCESS_TOKEN" \
  -H "x-api-key: API_KEY" \
  -H "content-type: application/octet-stream" \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

### Marcar upload em lote concluído

Depois que todos os arquivos tiverem sido carregados no lote, o lote poderá ser sinalizado para conclusão. Ao fazer isso, a variável [!DNL Catalog] As entradas &quot;DataSetFile&quot; são criadas para os arquivos concluídos e associadas ao lote gerado. O [!DNL Catalog] em seguida, o lote é marcado como bem-sucedido, o que aciona os fluxos downstream para assimilar os dados disponíveis.

Os dados chegarão primeiro ao local de preparo no Adobe Experience Platform e serão movidos para o local final após a catalogação e validação. Os lotes serão marcados como bem-sucedidos assim que todos os dados forem movidos para um local permanente.

**Solicitação**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization:Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

Se bem-sucedido, a resposta retornará HTTP Status 200 OK e o corpo da resposta estará vazio.

A ferramenta ETL deve observar o carimbo de data e hora dos conjuntos de dados de origem conforme os dados são lidos.

Na próxima execução da transformação, provavelmente por invocação de agendamento ou evento, o ETL começará a solicitar os dados do carimbo de data e hora salvo anteriormente e todos os dados a partir de então.

### Obter o status do último lote

Antes de executar novas tarefas na ferramenta ETL, verifique se o último lote foi concluído com êxito. O [[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/) O fornece uma opção específica para cada lote que fornece os detalhes dos lotes relevantes.

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

Novas tarefas podem ser agendadas se o valor do &quot;status&quot; do lote anterior for &quot;bem-sucedido&quot;, conforme mostrado abaixo:

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

Um status de lote individual pode ser recuperado por meio do [[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/) mediante a emissão de um pedido de GET utilizando a `{BATCH_ID}`. O `{BATCH_ID}` usada seria a mesma ID retornada quando o lote era criado.

**Solicitação**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches/{BATCH_ID}" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**Resposta - Sucesso**

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

Em caso de falha, os &quot;erros&quot; podem ser extraídos da resposta e aparecer na ferramenta ETL como mensagens de erro.

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

## Dados e eventos incrementais vs instantâneos vs perfis

Os dados podem ser representados em uma matriz dois por dois da seguinte maneira:

| Eventos incrementais | Perfis incrementais |
|-------------------------------|----------------------|
| Eventos de instantâneo (menos provável) | Perfis de instantâneo |

Os dados do evento normalmente são quando há colunas de carimbo de data e hora indexadas em cada linha.

Os dados do perfil normalmente são quando não há um carimbo de data e hora nos dados e cada linha pode ser identificada por uma chave primária/composta.

Os dados incrementais são o local onde somente os dados novos/atualizados entram no sistema e anexam aos dados atuais nos conjuntos de dados.

Dados de instantâneo são quando todos os dados entram no sistema e substituem alguns ou todos os dados anteriores em um conjunto de dados.

No caso de eventos incrementais, a ferramenta ETL deve usar as datas disponíveis/criar a data da entidade em lote. No caso do serviço de push, as datas disponíveis não estarão presentes, portanto, a ferramenta usará a data de criação/atualização do lote para marcação de incrementos. Todo lote de eventos incrementais deve ser processado.

Para perfis incrementais, a ferramenta ETL usará datas criadas/atualizadas da entidade em lote. Geralmente, cada lote de dados de perfil incrementais deve ser processado.

Os eventos de instantâneo são muito menos prováveis devido ao tamanho absoluto dos dados. Mas se isso for necessário, a ferramenta ETL deve selecionar apenas o último lote para processamento.

Quando perfis de instantâneo são usados, a ferramenta ETL terá que selecionar o último lote de dados que chegou ao sistema. Mas se o requisito for monitorar as versões das alterações, todos os lotes serão processados. O processamento de desduplicação no processo ETL ajudará a controlar os custos de armazenamento.

## Reprodução em lote e reprocessamento de dados

A reprodução em lote e o reprocessamento de dados podem ser necessários nos casos em que um cliente descubra que, nos últimos &quot;n&quot; dias, os dados que estão sendo processados ETL não ocorreram como esperado ou os dados de origem podem não ter sido corretos.

Para fazer isso, os administradores de dados do cliente usarão a variável [!DNL Platform] Interface do usuário para remover os lotes que contêm dados corrompidos. Em seguida, o ETL provavelmente precisará ser executado novamente, preenchendo-o novamente com os dados corretos. Se a fonte em si tiver dados corrompidos, o engenheiro/administrador de dados precisará corrigir os lotes de origem e assimilar novamente os dados (no Adobe Experience Platform ou por meio de conectores ETL).

Com base no tipo de dados que está sendo gerado, será a opção do engenheiro de dados remover um único lote ou todos os lotes de determinados conjuntos de dados. Os dados serão removidos/arquivados como de [!DNL Experience Platform] orientações.

É provável que a funcionalidade ETL para limpar dados seja importante.

Quando a limpeza for concluída, os administradores do cliente precisarão reconfigurar o Adobe Experience Platform para reiniciar o processamento dos serviços principais a partir do momento em que os lotes forem excluídos.

## Processamento em lote simultâneo

A critério do cliente, os administradores/engenheiros de dados podem decidir extrair, transformar e carregar dados de forma sequencial ou simultânea, dependendo das características de um conjunto de dados específico. Isso também se baseará no caso de uso que o cliente está direcionando com os dados transformados.

Por exemplo, se o cliente persistir em um armazenamento de persistência atualizável e a sequência ou a ordem dos eventos for importante, o cliente pode precisar processar trabalhos estritamente com transformações de ETL sequenciais.

Em outros casos, os dados fora de ordem podem ser processados por aplicativos/processos downstream que classificam internamente usando um carimbo de data/hora especificado. Nesses casos, as transformações paralelas de ETL podem ser viáveis para melhorar os tempos de processamento.

Para lotes de origem, ele novamente dependerá da preferência do cliente e da restrição do consumidor. Se os dados de origem puderem ser coletados em paralelo sem considerar a regência/pedido de uma linha, o processo de transformação poderá criar lotes de processos com um grau mais alto de paralelismo (otimização baseada em processamento fora de ordem). Mas, se a transformação tiver que honrar os carimbos de data e hora ou alterar a ordem de precedência, a API de acesso aos dados ou o agendador/invocação da ferramenta ETL terão que garantir que os lotes não sejam processados fora de ordem sempre que possível.

## Adiamento

Adiamento é um processo no qual os dados de entrada ainda não estão completos o suficiente para serem enviados para processos downstream, mas podem ser utilizáveis no futuro. Os clientes determinarão sua tolerância individual para a janela de dados para correspondência futura versus o custo de processamento para informar sua decisão de colocar dados de lado e reprocessá-los na próxima execução de transformação, na esperança de que possam ser enriquecidos e reconciliados/compilados em algum momento futuro dentro da janela de retenção. Esse ciclo está em andamento até que a linha seja processada o suficiente ou seja considerado obsoleto para continuar investindo no. Cada iteração gerará dados adiados que são um superconjunto de todos os dados adiados em iterações anteriores.

A Adobe Experience Platform não identifica dados adiados no momento, portanto, as implementações do cliente devem depender das configurações manuais do ETL e do Conjunto de dados para criar outro conjunto de dados no [!DNL Platform] espelhamento do conjunto de dados de origem que pode ser usado para manter dados adiados. Nesse caso, os dados adiados serão semelhantes aos dados do instantâneo. Em cada execução da transformação de ETL, os dados de origem serão unidos com dados adiados e enviados para processamento.

## Changelog

| Data | Ação | Descrição |
| ---- | ------ | ----------- |
| 2019-01-2019 | Remoção da propriedade &quot;campos&quot; dos conjuntos de dados | Anteriormente, os conjuntos de dados incluíam uma propriedade &quot;fields&quot; que continha uma cópia do esquema. Esse recurso não deve mais ser usado. Se a propriedade &quot;fields&quot; for encontrada, ela deverá ser ignorada e, em vez disso, &quot;observationSchema&quot; ou &quot;schemaRef&quot; deverá ser usado. |
| 2019-03-2015 | propriedade &quot;schemaRef&quot; adicionada aos conjuntos de dados | A propriedade &quot;schemaRef&quot; de um conjunto de dados contém um URI que faz referência ao esquema XDM no qual o conjunto de dados se baseia e representa todos os campos em potencial que podem ser usados pelo conjunto de dados. |
| 2019-03-2015 | Todos os identificadores de usuários finais mapeiam para a propriedade &quot;identityMap&quot; | O &quot;identityMap&quot; é um encapsulamento de todos os identificadores exclusivos de um assunto, como ID do CRM, ECID ou ID do programa de fidelidade. Este mapa é usado por [[!DNL Identity Service]](../identity-service/home.md) para resolver todas as identidades conhecidas e anônimas de um assunto, formando um único gráfico de identidade para cada usuário final. |
| 2019-05-30 | EOL e Remover a propriedade &quot;schema&quot; dos conjuntos de dados | A propriedade &quot;schema&quot; do conjunto de dados forneceu um link de referência para o esquema usando o `/xdms` endpoint no [!DNL Catalog] API. Isso foi substituído por um &quot;schemaRef&quot; que fornece o &quot;id&quot;, &quot;version&quot; e &quot;contentType&quot; do schema, conforme referenciado no novo [!DNL Schema Registry] API. |
