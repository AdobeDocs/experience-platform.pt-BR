---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Criação de integrações de ETL
topic: overview
translation-type: tm+mt
source-git-commit: 8b1b61b6446b28f92d6cf221003674fa09716c53
workflow-type: tm+mt
source-wordcount: '4153'
ht-degree: 0%

---


# Desenvolvimento de integrações de ETL para Adobe Experience Platform

O guia de integração ETL descreve as etapas gerais para a criação de conectores seguros e de alto desempenho para [!DNL Experience Platform] a incorporação de dados em [!DNL Platform].


- [[!Catálogo DNL]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)
- [[!DNL Data Access]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml)
- [[!Ingestão de Dados DNL]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml)
- [APIs de autenticação e autorização](../tutorials/authentication.md)
- [[!DNL Schema Registry]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)

Este guia também inclui exemplos de chamadas de API a serem usadas ao projetar um conector ETL, com links para a documentação que descreve cada [!DNL Experience Platform] serviço e o uso de sua API, com mais detalhes.

Uma amostra de integração está disponível [!DNL GitHub] por meio do Código [de referência de integração de ecossistema](https://github.com/adobe/acp-data-services-etl-reference) ETL na versão 2.0 da [!DNL Apache] licença.

## Fluxo de trabalho

O diagrama de fluxo de trabalho a seguir fornece uma visão geral de alto nível para a integração de componentes do Adobe Experience Platform com um aplicativo e conector ETL.

![](images/etl.png)

## Componentes Adobe Experience Platform

Há vários componentes de Experience Platform envolvidos nas integrações do conector ETL. A lista a seguir descreve vários componentes e funcionalidades principais:

- **Adobe Identity Management System (IMS)** - fornece estrutura para autenticação para serviços Adobe.
- **Organização** IMS - uma entidade corporativa que pode ser proprietária ou licenciar produtos e serviços e permitir o acesso a seus membros.
- **Usuário** IMS - Membros de uma organização IMS. A relação Organização-usuário é de muitas para muitas.
- **[!DNL Sandbox]** - Uma partição virtual como uma única [!DNL Platform] instância, para ajudar a desenvolver e desenvolver aplicativos de experiência digital.
- **Descoberta** de dados - registra os metadados dos dados ingeridos e transformados em [!DNL Experience Platform].
- **[!DNL Data Access]** - Fornece aos usuários uma interface para acessar seus dados em [!DNL Experience Platform].
- **[!DNL Data Ingestion]** - envia dados para [!DNL Experience Platform] as [!DNL Data Ingestion] APIs.
- **[!DNL Schema Registry]** - Define e armazena schemas que descrevem a estrutura dos dados a serem usados em [!DNL Experience Platform].

## Getting started with [!DNL Experience Platform] APIs

As seções a seguir fornecem informações adicionais que você precisará conhecer ou ter em mãos para fazer chamadas com êxito para [!DNL Experience Platform] APIs.

### Lendo chamadas de exemplo da API

Este guia fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção sobre [como ler chamadas](../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de exemplo no guia de [!DNL Experience Platform] solução de problemas.

### Reunir valores para cabeçalhos necessários

Para fazer chamadas para [!DNL Platform] APIs, você deve primeiro concluir o tutorial [de](../tutorials/authentication.md)autenticação. A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de [!DNL Experience Platform] API, como mostrado abaixo:

- Autorização: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos em [!DNL Experience Platform] são isolados para caixas de proteção virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifique o nome da caixa de proteção em que a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre caixas de proteção em [!DNL Platform], consulte a documentação [de visão geral da](../sandboxes/home.md)caixa de proteção.

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho adicional:

- Tipo de conteúdo: application/json

## Fluxo geral do usuário

Para começar, um usuário ETL faz logon na interface do [!DNL Experience Platform] usuário (UI) e cria conjuntos de dados para ingestão usando um conector padrão ou um conector de serviço de push.

Na interface do usuário, o usuário cria o conjunto de dados de saída selecionando um schema de conjunto de dados. A escolha do schema depende do tipo de dados (registro ou série cronológica) que está sendo assimilado [!DNL Platform]. Ao clicar na guia Schemas na interface do usuário, o usuário poderá visualização todos os schemas disponíveis, incluindo o tipo de comportamento suportado pelo schema.

Na ferramenta ETL, o usuário será start ao projetar suas transformações de mapeamento depois de configurar a conexão apropriada (usando suas credenciais). Pressupõe-se que a ferramenta ETL já tenha [!DNL Experience Platform] conectores instalados (processo não definido neste Guia de integração).

Mockups de uma ferramenta ETL de amostra e fluxo de trabalho foram fornecidos no fluxo de trabalho [](./workflow.md)ETL. Embora as ferramentas ETL possam diferir no formato, a maioria expõe funcionalidades semelhantes.

>[!NOTE]
>
>O conector ETL deve especificar um filtro de carimbo de data/hora que indique a data para a recepção dos dados e o deslocamento (ou seja, a janela para a qual os dados devem ser lidos). A ferramenta ETL deve suportar a utilização destes dois parâmetros nesta ou noutra interface relevante. No Adobe Experience Platform, esses parâmetros serão mapeados para datas disponíveis (se presentes) ou datas capturadas presentes no objeto de lote do conjunto de dados.

### Lista de visualizações de conjuntos de dados

Usando a fonte de dados para mapeamento, uma lista de todos os conjuntos de dados disponíveis pode ser obtida usando a [[!DNL Catalog API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml).

Você pode emitir uma única solicitação de API para visualização de todos os conjuntos de dados disponíveis (por exemplo, `GET /dataSets`), com a prática recomendada de incluir parâmetros de query que limitem o tamanho da resposta.

Nos casos em que são solicitadas informações _completas_ do conjunto de dados, a carga da resposta pode atingir 3 GB de tamanho, o que pode retardar o desempenho geral. Portanto, usar parâmetros de query para filtrar somente as informações necessárias tornará os [!DNL Catalog] query mais eficientes.

#### Filtragem de lista

Ao filtrar respostas, você pode usar vários filtros em uma única chamada separando parâmetros com um E comercial (`&`). Alguns parâmetros de query aceitam listas de valores separadas por vírgulas, como o filtro &quot;propriedades&quot; na solicitação de amostra abaixo.

[!DNL Catalog] as respostas são medidas automaticamente de acordo com os limites configurados, no entanto, o parâmetro de query &quot;limite&quot; pode ser usado para personalizar as restrições e limitar o número de objetos retornados. Os limites de [!DNL Catalog] resposta pré-configurados são:

- Se um parâmetro de limite não for especificado, o número máximo de objetos por carga de resposta será 20.
- O limite global para todos os outros [!DNL Catalog] query é de 100 objetos.
- Para query de conjunto de dados, se observableSchema for solicitado usando o parâmetro de query de propriedades, o número máximo de conjuntos de dados retornados será 20.
- Parâmetros de limite inválidos (incluindo `limit=0`) são atendidos com um erro HTTP 400 que descreve intervalos adequados.
- Se os limites ou deslocamentos forem passados como parâmetros de query, eles terão precedência sobre os passados como cabeçalhos.

Os parâmetros do query são abordados com mais detalhes na visão geral [do serviço de](../catalog/home.md)catálogo.

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
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

Consulte a visão geral [do Serviço de](../catalog/home.md) Catálogo para obter exemplos detalhados de como fazer chamadas para a [[!DNL Catalog API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml).

**Resposta**

A resposta inclui três (`limit=3`) conjuntos de dados que mostram &quot;nome&quot;, &quot;descrição&quot; e &quot;schemaRef&quot;, conforme indicado pelo parâmetro do `properties` query.

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

### Schema de conjunto de dados de visualização

A propriedade &quot;schemaRef&quot; de um conjunto de dados contém um URI que faz referência ao schema XDM no qual o conjunto de dados se baseia. O schema XDM (&quot;schemaRef&quot;) representa todos os campos _potenciais_ que podem ser usados pelo conjunto de dados, não necessariamente os campos que _estão_ sendo usados (consulte &quot;observableSchema&quot; abaixo).

O schema XDM é o schema que você usa quando precisa apresentar ao usuário uma lista de todos os campos disponíveis que podem ser gravados.

O primeiro valor &quot;schemaRef.id&quot; no objeto de resposta anterior (`https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18`) é um URI que aponta para um schema XDM específico no [!DNL Schema Registry]. O schema pode ser recuperado fazendo uma solicitação de pesquisa (GET) para a [!DNL Schema Registry] API.

>[!NOTE]
>
>A propriedade &quot;schemaRef&quot; substitui a propriedade &quot;schema&quot; agora obsoleta. Se &quot;schemaRef&quot; estiver ausente do conjunto de dados ou não contiver um valor, será necessário verificar a presença de uma propriedade &quot;schema&quot;. Isso pode ser feito substituindo &quot;schemaRef&quot; por &quot;schema&quot; no parâmetro `properties` query na chamada anterior. Mais detalhes sobre a propriedade &quot;schema&quot; estão disponíveis na seção Propriedade [&quot;schema&quot; do](#dataset-schema-property-deprecated---eol-2019-05-30) conjunto de dados a seguir.

**Formato da API**

```http
GET /schemaregistry/tenant/schemas/{url encoded schemaRef.id}
```

**Solicitação**

A solicitação usa o URL codificado `id` do schema (o valor do atributo &quot;schemaRef.id&quot;) e requer um cabeçalho Accept.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F274f17bc5807ff307a046bab1489fb18 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1' \
```

O formato de resposta depende do tipo de cabeçalho Accept enviado na solicitação. As solicitações de pesquisa também exigem que `version` sejam incluídas no cabeçalho Aceitar. A tabela a seguir descreve os cabeçalhos Accept disponíveis para pesquisas:

| Aceitar | Descrição |
| ------ | ----------- |
| `application/vnd.adobe.xed-id+json` | Solicitações, títulos, IDs e versões de lista (GET) |
| `application/vnd.adobe.xed-full+json; version={major version}` | $refs e allOf resolvidos, tem títulos e descrições |
| `application/vnd.adobe.xed+json; version={major version}` | Bruto com $ref e allOf, tem títulos e descrições |
| `application/vnd.adobe.xed-notext+json; version={major version}` | Bruto com $ref e allOf, sem títulos ou descrições |
| `application/vnd.adobe.xed-full-notext+json; version={major version}` | $refs e allOf resolvidos, sem títulos ou descrições |
| `application/vnd.adobe.xed-full-desc+json; version={major version}` | $refs e allOf resolvidos, descritores incluídos |

>[!NOTE]
>
>`application/vnd.adobe.xed-id+json` e `application/vnd.adobe.xed-full+json; version={major version}` são os cabeçalhos Accept mais usados. `application/vnd.adobe.xed-id+json` é preferencial para a listagem de recursos no [!DNL Schema Registry] , pois retorna somente o &quot;título&quot;, &quot;id&quot; e &quot;versão&quot;. `application/vnd.adobe.xed-full+json; version={major version}` é preferencial para exibir um recurso específico (por sua &quot;id&quot;), pois retorna todos os campos (aninhados em &quot;propriedades&quot;), bem como títulos e descrições.

**Resposta**

O schema JSON retornado descreve a estrutura e as informações de nível de campo (&quot;tipo&quot;, &quot;formato&quot;, &quot;mínimo&quot;, &quot;máximo&quot; etc.) dos dados, serializados como JSON. Se estiver usando um formato de serialização diferente de JSON para ingestão (como Parquet ou Scala), o Guia [do Registro do](../xdm/tutorials/create-schema-api.md) Schema contém uma tabela que mostra o tipo JSON desejado (&quot;meta:xdmType&quot;) e sua representação correspondente em outros formatos.

Junto com esta tabela, o Guia do [!DNL Schema Registry] desenvolvedor contém exemplos aprofundados de todas as chamadas possíveis que podem ser feitas usando a [!DNL Schema Registry] API.

### Propriedade &quot;schema&quot; do conjunto de dados (DEPRECATED - EOL 2019-05-30)

Os conjuntos de dados podem conter uma propriedade &quot;schema&quot; que agora está obsoleta e permanece disponível temporariamente para compatibilidade com versões anteriores. Por exemplo, uma solicitação de listagem (GET) semelhante à feita anteriormente, onde &quot;schema&quot; foi substituído por &quot;schemaRef&quot; no parâmetro do `properties` query, pode retornar o seguinte:

```json
{
  "5ba9452f7de80400007fc52a": {
    "name": "Sample Dataset 1",
    "description": "Description of Sample Dataset 1.",
    "schema": "@/xdms/context/person"
  }
}
```

Se a propriedade &quot;schema&quot; de um conjunto de dados for preenchida, isso indica que o schema é um `/xdms` schema obsoleto e, quando suportado, o conector ETL deve usar o valor na propriedade &quot;schema&quot; com o `/xdms` endpoint (um endpoint obsoleto na [[!DNL Catalog API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)) para recuperar o schema herdado.

**Formato da API**

```http
GET /catalog/{"schema" property without the "@"}
```

**Solicitação**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/xdms/context/person?expansion=xdm" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

>[!NOTE]
>
>Um parâmetro de query opcional, `expansion=xdm`, diz à API para expandir completamente e em linha quaisquer schemas referenciados. Você pode desejar fazer isso ao apresentar uma lista de todos os campos em potencial ao usuário.

**Resposta**

Semelhante às etapas de [exibição do schema](#view-dataset-schema)de conjunto de dados, a resposta contém um schema JSON que descreve a estrutura e as informações de nível de campo dos dados, serializados como JSON.

>[!NOTE]
>
>Quando o campo &quot;schema&quot; estiver vazio ou ausente completamente, o conector deverá ler o campo &quot;schemaRef&quot; e usar a API [do Registro do](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) Schema, conforme mostrado nas etapas anteriores, para [visualização de um schema](#view-dataset-schema)de conjunto de dados.

### A propriedade &quot;observableSchema&quot;

A propriedade &quot;observableSchema&quot; de um conjunto de dados tem uma estrutura JSON correspondente à do schema XDM JSON. O &quot;observableSchema&quot; contém os campos que estavam presentes nos arquivos de entrada. Ao gravar dados para [!DNL Experience Platform], o usuário não é obrigado a usar todos os campos do schema do público alvo. Em vez disso, devem fornecer apenas os campos que estão sendo usados.

O schema observável é o schema que você usaria se lesse os dados ou apresentasse uma lista de campos disponíveis para ler/mapear.

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

### dados de pré-visualização

O aplicativo ETL pode fornecer uma capacidade de pré-visualização de dados ([&quot;Figura 8&quot; no fluxo de trabalho](./workflow.md)ETL). A API de acesso a dados fornece várias opções para pré-visualização de dados.

Informações adicionais, incluindo orientação passo a passo para a visualização de dados usando a API de acesso a dados, podem ser encontradas no tutorial [de acesso a](../data-access/tutorials/dataset-data.md)dados.

### Obter detalhes do conjunto de dados usando o parâmetro de query &quot;properties&quot;

Conforme mostrado nas etapas acima para [visualização de uma lista de conjuntos de dados](#view-list-of-datasets), é possível solicitar &quot;arquivos&quot; usando o parâmetro de query &quot;propriedades&quot;.

Consulte a visão geral [do Serviço de](../catalog/home.md) Catálogo para obter informações detalhadas sobre como consultar conjuntos de dados e filtros de resposta disponíveis.

**Formato da API**

```http
GET /catalog/dataSets?limit={value}&properties={value}
```

**Solicitação**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/dataSets?limit=1&properties=files" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
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

### Lista de arquivos de conjunto de dados usando o atributo &quot;files&quot;

Você também pode usar uma solicitação de GET para buscar detalhes do arquivo usando o atributo &quot;files&quot;.

**Formato da API**

```http
GET /catalog/dataSets/{DATASET_ID}/views/{VIEW_ID}/files
```

**Solicitação**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/dataSets/5bf479a6a8c862000050e3c7/views/5bf479a654f52014cfffe7f1/files" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
```

**Resposta**

A resposta inclui a ID do Arquivo do Conjunto de Dados como a propriedade de nível superior, com detalhes do arquivo contidos no objeto da ID do Arquivo do Conjunto de Dados.

```json
{
    "194e89b976494c9c8113b968c27c1472-1": {
        "batchId": "194e89b976494c9c8113b968c27c1472",
        "dataSetViewId": "5bf479a654f52014cfffe7f1",
        "imsOrg": "{IMS_ORG}",
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
        "imsOrg": "{IMS_ORG}",
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
        "imsOrg": "{IMS_ORG}",
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

As IDs de arquivo do conjunto de dados retornadas na resposta anterior podem ser usadas em uma solicitação de GET para buscar mais detalhes do arquivo por meio da [!DNL Data Access] API.

A visão geral [do acesso aos](../data-access/home.md) dados contém detalhes sobre como usar a [!DNL Data Access] API.

**Formato da API**

```http
GET /export/files/{DATASET_FILE_ID}
```

**Solicitação**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/ea40946ac03140ec8ac4f25da360620a-1" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
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

### Dados do arquivo de pré-visualização

A propriedade &quot;href&quot; pode ser usada para buscar dados de pré-visualização por meio da [[!DNL Data Access API]](../data-access/home.md).

**Formato da API**

```http
GET /export/files/{FILE_ID}?path={FILE_NAME}.{FILE_FORMAT}
```

**Solicitação**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/ea40946ac03140ec8ac4f25da360620a-1?path=samplefile.parquet" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
```

A resposta à solicitação acima contém uma pré-visualização do conteúdo do arquivo.

Mais informações sobre a [!DNL Data Access] API, incluindo solicitações e respostas detalhadas, estão disponíveis na visão geral [do acesso aos](../data-access/home.md)dados.

### Obter &quot;fileDescription&quot; do conjunto de dados

O componente de destino como saída de dados transformados, o Engenheiro de Dados escolherá um Conjunto de Dados de Saída ([&quot;Figura 12&quot; no Fluxo de Trabalho](workflow.md)ETL). O schema XDM está associado ao conjunto de dados de saída. Os dados a serem gravados serão identificados pelo atributo &quot;fileDescription&quot; da entidade do conjunto de dados das APIs de descoberta de dados. Essas informações podem ser obtidas usando uma ID de conjunto de dados (`{DATASET_ID}`). A propriedade &quot;fileDescription&quot; na resposta JSON fornecerá as informações solicitadas.

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
-H "x-gw-ims-org-id: {IMS_ORG}" \
-H "x-sandbox-name: {SANDBOX_NAME}" \
-H "Authorization: Bearer {ACCESS_TOKEN}" \
-H "x-api-key : {API_KEY}"
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

Os dados serão gravados [!DNL Experience Platform] usando a API [de ingestão de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml)dados.  A gravação de dados é um processo assíncrono. Quando os dados são gravados na Adobe Experience Platform, um lote é criado e marcado como um sucesso somente depois que os dados são totalmente gravados.

Os dados em [!DNL Experience Platform] devem ser gravados na forma de arquivos parquet.

## Fase de execução

Como os start de execução, o conector (conforme definido no componente de origem) lerá os dados a partir da [!DNL Experience Platform] API [[!DNL Data Access]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml). O processo de transformação lerá os dados de um determinado intervalo de tempo. Internamente, ele query lotes de conjuntos de dados de origem. Durante a consulta, ele usará uma data de start e arquivos de conjunto de dados de lista parametrizados (rolando para dados de séries de tempo ou dados incrementais) para esses lotes, e o start que faz solicitações de dados para esses arquivos de conjunto de dados.

### Exemplo de transformações

O documento de transformações [ETL de](./transformations.md) amostra contém várias transformações de exemplo, incluindo manuseio de identidade e mapeamentos de tipo de dados. Use essas transformações para referência.

### Ler dados de [!DNL Experience Platform]

Usando a [[!DNL Catalog API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml), você pode buscar todos os lotes entre uma hora e hora de término do start especificado e classificá-los pela ordem em que foram criados.

**Solicitação**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches?dataSet=DATASETID&createdAfter=START_TIMESTAMP&createdBefore=END_TIMESTAMP&sort=desc:created" \
  -H "Accept: application/json" \
  -H "Authorization:Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

Detalhes sobre a filtragem de lotes podem ser encontrados no tutorial [Acesso a](../data-access/tutorials/dataset-data.md)dados.

### Obter arquivos de um lote

Depois que você tiver a ID do lote que está procurando (`{BATCH_ID}`), é possível recuperar uma lista de arquivos pertencentes a um lote específico por meio da [[!DNL Data Access API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml).  Os detalhes para fazer isso estão disponíveis no [[!DNL Data Access] tutorial](../data-access/tutorials/dataset-data.md).

**Solicitação**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/files" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
```

### Acessar arquivos usando a ID de arquivo

Usando a ID exclusiva de um arquivo (`{FILE_ID`), a [[!DNL Data Access API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml) pode ser usada para acessar os detalhes específicos do arquivo, incluindo seu nome, tamanho em bytes e um link para baixá-lo.

**Solicitação**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/{FILE_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key : {API_KEY}"
```

A resposta pode apontar para um único arquivo ou diretório. Detalhes de cada um podem ser encontrados no [[!DNL Data Access] tutorial](../data-access/tutorials/dataset-data.md).

### Acessar conteúdo do arquivo

A [[!DNL Data Access API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml) pode ser usada para acessar o conteúdo de um arquivo específico. Para obter o conteúdo, uma solicitação de GET é feita usando o valor retornado para `_links.self.href` acessar um arquivo usando a ID do arquivo.

**Solicitação**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/{DATASET_FILE_ID}?path=filename1.csv" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

A resposta a esta solicitação contém o conteúdo do arquivo. Para obter mais informações, incluindo detalhes sobre a paginação de resposta, consulte o tutorial [Como Query dados por meio da API](../data-access/tutorials/dataset-data.md) de acesso a dados.

### Validar registros para conformidade com o schema

Quando os dados são gravados, os usuários podem optar por validar os dados de acordo com as regras de validação definidas no schema XDM. Para obter mais informações sobre a validação do schema, consulte o Código de Referência sobre [Integração de Ecossistemas [!DNL GitHub]](https://github.com/adobe/experience-platform-etl-reference/blob/fd08dd9f74ae45b849d5482f645f859f330c1951/README.md#validation)ETL em.

Se você estiver usando a implementação de referência encontrada em [[!DNL GitHub]](https://github.com/adobe/experience-platform-etl-reference/blob/fd08dd9f74ae45b849d5482f645f859f330c1951/README.md), poderá ativar a validação de schema nesta implementação usando a propriedade do sistema `-DenableSchemaValidation=true`.

A validação pode ser executada para tipos XDM lógicos, usando atributos como `minLength` e `maxlength` para strings `minimum` e `maximum` para inteiros e muito mais. O guia [do desenvolvedor da API do Registro de](../xdm/api/getting-started.md) Schemas contém uma tabela que descreve os tipos XDM e as propriedades que podem ser usadas para validação.

>[!NOTE]
>
>Os valores mínimo e máximo fornecidos para vários `integer` tipos são os valores MIN e MAX que o tipo pode suportar, mas esses valores podem ser ainda mais restritos aos mínimos e máximos de sua escolha.

### Criar um lote

Depois que os dados forem processados, a ferramenta ETL gravará os dados de volta [!DNL Experience Platform] usando a API [de ingestão](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml)em lote. Antes que os dados possam ser adicionados a um conjunto de dados, eles devem estar vinculados a um lote que será carregado posteriormente em um conjunto de dados específico.

**Solicitação**

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -d '{
        "datasetId":"{DATASET_ID}"
      }'
```

Detalhes para a criação de um lote, incluindo solicitações de amostra e respostas, podem ser encontrados na visão geral [da](../ingestion/batch-ingestion/overview.md)Ingestão de lote.

### Gravar no conjunto de dados

Depois de criar com êxito um novo lote, os arquivos podem ser carregados em um conjunto de dados específico. Vários arquivos podem ser publicados em um lote até que seja promovido. Os arquivos podem ser carregados usando a _Small File Upload API_; no entanto, se os arquivos forem muito grandes e o limite do gateway for excedido, você poderá usar a API _de upload de arquivo_ grande. Detalhes sobre o uso de Upload de Arquivo Grande e Pequeno podem ser encontrados na visão geral [de Ingestão em](../ingestion/batch-ingestion/overview.md)Lote.

**Solicitação**

Os dados em [!DNL Experience Platform] devem ser gravados na forma de arquivos parquet.

```shell
curl -X PUT "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/dataSets/{DATASET_ID}/files/{FILE_NAME}.parquet" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id:{IMS_ORG}" \
  -H "Authorization:Bearer ACCESS_TOKEN" \
  -H "x-api-key: API_KEY" \
  -H "content-type: application/octet-stream" \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

### Marcar carregamento em lote concluído

Depois que todos os arquivos forem carregados no lote, o lote poderá ser sinalizado para conclusão. Ao fazer isso, as entradas [!DNL Catalog] &quot;DataSetFile&quot; são criadas para os arquivos concluídos e associadas ao lote de geração. O [!DNL Catalog] lote é marcado como bem-sucedido, o que aciona os fluxos downstream para assimilar os dados disponíveis.

Os dados chegarão primeiro no local de armazenamento temporário no Adobe Experience Platform e serão movidos para o local final após a catalogação e validação. Os lotes serão marcados como bem-sucedidos assim que todos os dados forem movidos para um local permanente.

**Solicitação**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization:Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
```

Se bem-sucedido, a resposta retornará HTTP Status 200 OK e o corpo da resposta estará vazio.

A ferramenta ETL observará o carimbo de data e hora dos conjuntos de dados de origem à medida que os dados forem lidos.

Na próxima execução de transformação, provavelmente por agendamento ou invocação de evento, o ETL start solicitando os dados do carimbo de data e hora salvo anteriormente e todos os dados em diante.

### Obter status do último lote

Antes de executar novas tarefas na ferramenta ETL, verifique se o último lote foi concluído com êxito. A [[!DNL Catalog Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) fornece uma opção específica para lote que fornece os detalhes dos lotes relevantes.

**Solicitação**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches?limit=1&sort=desc:created" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**Resposta**

As novas tarefas podem ser programadas se o valor do &quot;status&quot; do lote anterior for &quot;bem-sucedido&quot;, conforme mostrado abaixo:

```json
"{BATCH_ID}": {
    "imsOrg": "{IMS_ORG}",
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

Um status de lote individual pode ser recuperado por meio da [[!DNL Catalog Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) emitindo uma solicitação de GET usando a `{BATCH_ID}`. A ID `{BATCH_ID}` usada seria a mesma retornada quando o lote era criado.

**Solicitação**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches/{BATCH_ID}" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**Resposta - Êxito**

A resposta a seguir mostra um &quot;sucesso&quot;:

```json
"{BATCH_ID}": {
    "imsOrg": "{IMS_ORG}",
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
    "imsOrg": "{IMS_ORG}",
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

Os dados podem ser representados em uma matriz dois por dois, da seguinte forma:

| Eventos incrementais | Perfis incrementais |
|-------------------------------|----------------------|
| Eventos de instantâneo (menos provável) | Perfis de instantâneos |

Os dados do evento geralmente são obtidos quando há colunas de carimbo de data e hora indexadas em cada linha.

Os dados do perfil geralmente são exibidos quando não há um carimbo de data e hora nos dados e cada linha pode ser identificada por uma chave primária/composta.

Os dados incrementais são o local onde somente os dados novos/atualizados entram no sistema e se acrescentam aos dados atuais nos conjuntos de dados.

Dados de instantâneo são quando todos os dados entram no sistema e substituem alguns ou todos os dados anteriores em um conjunto de dados.

No caso de eventos incrementais, a ferramenta ETL deve usar as datas disponíveis/data de criação da entidade de lote. No caso do serviço de push, as datas disponíveis não estarão presentes, portanto, a ferramenta usará a data de criação/atualização do lote para marcação de incrementos. Cada lote de eventos incrementais deve ser processado.

Para perfis incrementais, a ferramenta ETL usará datas criadas/atualizadas da entidade de lote. Normalmente, cada lote de dados incrementais de perfil é necessário para processamento.

Eventos de instantâneos são muito menos prováveis devido ao tamanho puro dos dados. Mas se isso for necessário, a ferramenta ETL deve selecionar apenas o último lote para processamento.

Quando perfis de instantâneo são usados, a ferramenta ETL terá que escolher o último lote de dados que chegou ao sistema. Mas se a exigência é acompanhar as versões das alterações, então todos os lotes serão processados. O processamento de eliminação da duplicação no processo ETL ajudará a controlar os custos do armazenamento.

## Reprodução em lote e reprocessamento de dados

A repetição em lote e o reprocessamento de dados podem ser necessários nos casos em que um cliente descobre que, nos últimos &quot;n&quot; dias, os dados processados ETL não ocorreram como esperado ou os próprios dados de origem podem não estar corretos.

Para fazer isso, os administradores de dados do cliente usarão a [!DNL Platform] interface do usuário para remover os lotes que contêm dados corrompidos. Em seguida, o ETL provavelmente precisará ser executado novamente, repovoando-o com os dados corretos. Se a fonte em si tiver dados corrompidos, o engenheiro/administrador de dados precisará corrigir os lotes de origem e reingerir os dados (no Adobe Experience Platform ou por meio de conectores ETL).

Com base no tipo de dados que está sendo gerado, será a escolha do engenheiro de dados para remover um único lote ou todos os lotes de determinados conjuntos de dados. Os dados serão removidos/arquivados de acordo com [!DNL Experience Platform] as diretrizes.

É provável que a funcionalidade ETL para expurgar dados seja importante.

Quando a remoção estiver concluída, os administradores do cliente terão que reconfigurar a Adobe Experience Platform para reiniciar o processamento dos principais serviços a partir do momento em que os lotes forem excluídos.

## Processamento em lote simultâneo

A critério do cliente, os administradores/engenheiros de dados podem decidir extrair, transformar e carregar dados de forma sequencial ou simultânea, dependendo das características de um conjunto de dados específico. Isso também se baseará no caso de uso que o cliente está direcionando com os dados transformados.

Por exemplo, se o cliente persistir em um armazenamento de persistência atualizável e a sequência ou ordem de eventos for importante, o cliente pode precisar processar tarefas estritamente com transformações de ETL sequenciais.

Em outros casos, os dados fora de ordem podem ser processados por aplicativos/processos de downstream que classificam internamente usando um carimbo de data e hora especificado. Nesses casos, as transformações paralelas de ETL podem ser viáveis para melhorar o tempo de processamento.

Para lotes de origem, ele dependerá novamente da preferência do cliente e da restrição do consumidor. Se os dados de origem puderem ser coletados em paralelo, independentemente da regularidade/ordem de uma linha, o processo de transformação poderá criar lotes de processos com um grau mais alto de paralelismo (otimização baseada no processamento fora de ordem). Mas se a transformação tiver que cumprir carimbos de data e hora ou alterar a ordem de precedência, o scheduler/invocação da API de acesso aos dados ou da ferramenta ETL terá que garantir que os lotes não sejam processados fora da ordem, sempre que possível.

## Adiamento

O diferimento é um processo no qual os dados de entrada ainda não estão completos o suficiente para serem enviados para processos de downstream, mas podem ser usados no futuro. Os clientes determinarão sua tolerância individual para a janela de dados para correspondência futura versus o custo de processamento para informar sua decisão de colocar os dados de lado e reprocessá-los na próxima execução de transformação, na esperança de que possam ser enriquecidos e reconciliados/costurados em algum momento futuro dentro da janela de retenção. Este ciclo está em andamento até que a linha seja processada o suficiente ou se considere demasiado obsoleta para continuar a investir. Cada iteração gerará dados adiados que são um superconjunto de todos os dados adiados em iterações anteriores.

A Adobe Experience Platform não identifica dados adiados no momento, portanto, as implementações do cliente devem depender das configurações manuais do ETL e do Conjunto de dados para criar outro conjunto de dados no [!DNL Platform] espelhamento do conjunto de dados de origem que pode ser usado para manter dados adiados. Nesse caso, os dados adiados serão semelhantes aos dados de snapshot. Em cada execução da transformação ETL, os dados de origem serão unidos com dados adiados e enviados para processamento.

## Changelog

| Data | Ação | Descrição |
| ---- | ------ | ----------- |
| 2019-01-19 | Propriedade &quot;fields&quot; removida dos conjuntos de dados | Anteriormente, os conjuntos de dados incluíam uma propriedade &quot;fields&quot; que continha uma cópia do schema. Esse recurso não deve mais ser usado. Se a propriedade &quot;fields&quot; for encontrada, ela deve ser ignorada e, em vez disso, &quot;watchSchema&quot; ou &quot;schemaRef&quot; deve ser usado. |
| 2019-03-15 | propriedade &quot;schemaRef&quot; adicionada aos conjuntos de dados | A propriedade &quot;schemaRef&quot; de um conjunto de dados contém um URI que faz referência ao schema XDM no qual o conjunto de dados se baseia e representa todos os campos potenciais que podem ser usados pelo conjunto de dados. |
| 2019-03-15 | Todos os identificadores de usuário final são mapeados para a propriedade &quot;identityMap&quot; | O &quot;identityMap&quot; é um encapsulamento de todos os identificadores exclusivos de um assunto, como ID de CRM, ECID ou ID de programa de fidelidade. Este mapa é usado pelo [[!DNL Identity Service]](../identity-service/home.md) para resolver todas as identidades conhecidas e anônimas de um assunto, formando um único gráfico de identidade para cada usuário final. |
| 2019-05-30 | Propriedade EOL e Remover &quot;schema&quot; dos conjuntos de dados | A propriedade &quot;schema&quot; do conjunto de dados forneceu um link de referência para o schema usando o `/xdms` terminal obsoleto na [!DNL Catalog] API. Isso foi substituído por um &quot;schemaRef&quot; que fornece &quot;id&quot;, &quot;version&quot; e &quot;contentType&quot; do schema, conforme referenciado na nova [!DNL Schema Registry] API. |