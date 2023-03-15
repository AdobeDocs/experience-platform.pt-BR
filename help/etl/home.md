---
keywords: Experience Platform;página inicial;tópicos populares;integrações de ETL;etl;etl;integrações de ETL
solution: Experience Platform
title: Desenvolvimento de integrações ETL para o Adobe Experience Platform
description: O guia de integração de ETL descreve as etapas gerais para criar conectores seguros de alto desempenho para o Experience Platform e assimilar dados na plataforma.
exl-id: 7d29b61c-a061-46f8-a31f-f20e4d725655
source-git-commit: 1a7ba52b48460d77d0b7695aa0ab2d5be127d921
workflow-type: tm+mt
source-wordcount: '4075'
ht-degree: 1%

---

# Desenvolvimento de integrações ETL para o Adobe Experience Platform

O guia de integração de ETL descreve as etapas gerais para criar conectores seguros e de alto desempenho para o [!DNL Experience Platform] e assimilação de dados em [!DNL Platform].


- [[!DNL Catalog]](https://www.adobe.io/experience-platform-apis/references/catalog/)
- [[!DNL Data Access]](https://www.adobe.io/experience-platform-apis/references/data-access/)
- [[!DNL Data Ingestion]](https://www.adobe.io/experience-platform-apis/references/data-ingestion/)
- [Autenticação e autorização para APIs Experience Platform](https://www.adobe.com/go/platform-api-authentication-en)
- [[!DNL Schema Registry]](https://www.adobe.io/experience-platform-apis/references/schema-registry/)

Este guia também inclui exemplos de chamadas de API para usar ao criar um conector ETL, com links para a documentação que descreve cada um [!DNL Experience Platform] e uso de sua API, em mais detalhes.

Um exemplo de integração está disponível em [!DNL GitHub] por meio da [Código de referência de integração de ecossistema ETL](https://github.com/adobe/acp-data-services-etl-reference) no [!DNL Apache] Versão da licença 2.0.

## Fluxo de trabalho

O diagrama de fluxo de trabalho a seguir fornece uma visão geral de alto nível para a integração dos componentes do Adobe Experience Platform com um aplicativo e conector ETL.

![](images/etl.png)

## Componentes do Adobe Experience Platform

Há vários componentes de Experience Platform envolvidos nas integrações do conector ETL. A lista a seguir descreve vários componentes e funcionalidades principais:

- **Sistema Adobe Identity Management (IMS)** - Fornece a estrutura de autenticação para os serviços da Adobe.
- **Organização IMS** - Uma entidade corporativa que pode ser proprietária ou licenciar produtos e serviços e permitir o acesso a seus membros.
- **Usuário do IMS** - Membros de uma organização IMS. A relação entre organização e usuário é do tipo muitos para muitos.
- **[!DNL Sandbox]** - Uma partição virtual uma única [!DNL Platform] para ajudar a desenvolver aplicativos de experiência digital.
- **Descoberta de dados** - Registra os metadados de dados assimilados e transformados no [!DNL Experience Platform].
- **[!DNL Data Access]** - Fornece aos usuários uma interface para acessar seus dados no [!DNL Experience Platform].
- **[!DNL Data Ingestion]** - Envia dados para [!DNL Experience Platform] com [!DNL Data Ingestion] APIs.
- **[!DNL Schema Registry]** - Define e armazena schema que descreve a estrutura dos dados a serem usados no [!DNL Experience Platform].

## Introdução ao [!DNL Experience Platform] APIs

As seções a seguir fornecem informações adicionais que você precisará saber ou ter em mãos para fazer chamadas com êxito para o [!DNL Experience Platform] APIs.

### Leitura de chamadas de API de amostra

Este guia fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O exemplo de JSON retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../landing/troubleshooting.md#how-do-i-format-an-api-request) no [!DNL Experience Platform] guia de solução de problemas.

### Coletar valores para cabeçalhos obrigatórios

Para fazer chamadas para [!DNL Platform] APIs, primeiro conclua o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). Concluir o tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todos os [!DNL Experience Platform] Chamadas de API, conforme mostrado abaixo:

- Autorização: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Todos os recursos em [!DNL Experience Platform] são isolados em sandboxes virtuais específicas. Todas as solicitações para [!DNL Platform] As APIs exigem um cabeçalho que especifique o nome da sandbox em que a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre sandboxes no [!DNL Platform], consulte o [documentação de visão geral da sandbox](../sandboxes/home.md).

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho adicional:

- Tipo de conteúdo: application/json

## Fluxo geral de usuário

Para começar, um usuário do ETL faz logon na [!DNL Experience Platform] A interface do usuário (UI) do e cria conjuntos de dados para assimilação usando um conector padrão ou conector de serviço por push.

Na interface, o usuário cria o conjunto de dados de saída selecionando um esquema de conjunto de dados. A escolha do esquema depende do tipo de dados (registro ou série de tempo) que está sendo assimilado na [!DNL Platform]. Ao clicar na guia Esquemas na interface do usuário, o usuário poderá exibir todos os esquemas disponíveis, incluindo o tipo de comportamento compatível com o esquema.

Na ferramenta ETL, o usuário começará a projetar suas transformações de mapeamento após configurar a conexão apropriada (usando suas credenciais). Pressupõe-se que a ferramenta ETL já tenha [!DNL Experience Platform] conectores instalados (processo não definido neste Guia de integração).

Os modelos para uma ferramenta e um fluxo de trabalho de ETL de amostra foram fornecidos na [Fluxo de trabalho ETL](./workflow.md). Embora as ferramentas ETL possam diferir no formato, a maioria expõe uma funcionalidade semelhante.

>[!NOTE]
>
>O conector ETL deve especificar um filtro de carimbo de data e hora que marque a data para assimilar dados e deslocamento (ou seja, A janela para a qual os dados devem ser lidos). A ferramenta ETL deve ser compatível com a utilização desses dois parâmetros nesta ou em outra interface relevante. No Adobe Experience Platform, esses parâmetros serão mapeados para as datas disponíveis (se presentes) ou para a data capturada presente no objeto em lote do conjunto de dados.

### Exibir lista de conjuntos de dados

Usando a fonte de dados para mapeamento, uma lista de todos os conjuntos de dados disponíveis pode ser buscada usando o [[!DNL Catalog API]](https://www.adobe.io/experience-platform-apis/references/catalog/).

Você pode emitir uma única solicitação de API para exibir todos os conjuntos de dados disponíveis (por exemplo, `GET /dataSets`), com a prática recomendada de incluir parâmetros de consulta que limitam o tamanho da resposta.

Nos casos em que as informações completas do conjunto de dados estão sendo solicitadas, a carga de resposta pode atingir mais de 3 GB em tamanho, o que pode retardar o desempenho geral. Portanto, usar parâmetros de consulta para filtrar somente as informações necessárias tornará [!DNL Catalog] consultas mais eficientes.

#### Filtragem de lista

Ao filtrar respostas, é possível usar vários filtros em uma única chamada do separando parâmetros com um E comercial (`&`). Alguns parâmetros de consulta aceitam listas de valores separados por vírgulas, como o filtro &quot;propriedades&quot; na solicitação de exemplo abaixo.

[!DNL Catalog] as respostas são medidas automaticamente de acordo com os limites configurados, no entanto, o parâmetro de consulta &quot;limit&quot; pode ser usado para personalizar as restrições e limitar o número de objetos retornados. O pré-configurado [!DNL Catalog] os limites de resposta são:

- Se um parâmetro de limite não for especificado, o número máximo de objetos por carga de resposta será 20.
- O limite global para todos os outros [!DNL Catalog] queries tem 100 objetos.
- Para consultas de conjunto de dados, se observableSchema for solicitado usando o parâmetro de consulta de propriedades, o número máximo de conjuntos de dados retornado será 20.
- Parâmetros de limite inválidos (incluindo `limit=0`) são recebidos com um erro HTTP 400 que descreve intervalos adequados.
- Se os limites ou deslocamentos forem transmitidos como parâmetros de consulta, eles terão prioridade sobre aqueles transmitidos como cabeçalhos.

Os parâmetros de consulta são abordados com mais detalhes na [Visão geral do Serviço de catálogo](../catalog/home.md).

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

Consulte a [Visão geral do Serviço de catálogo](../catalog/home.md) para obter exemplos detalhados de como fazer chamadas para a [[!DNL Catalog API]](https://www.adobe.io/experience-platform-apis/references/catalog/).

**Resposta**

A resposta inclui três (`limit=3`) mostrando o &quot;name&quot;, &quot;description&quot; e &quot;schemaRef&quot; como indicado pela variável `properties` parâmetro de consulta.

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

O primeiro valor &quot;schemaRef.id&quot; no objeto de resposta anterior (`https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18`) é um URI que aponta para um esquema XDM específico na variável [!DNL Schema Registry]. O esquema pode ser recuperado fazendo uma solicitação de pesquisa (GET) ao [!DNL Schema Registry] API.

>[!NOTE]
>
>A propriedade &quot;schemaRef&quot; substitui a propriedade &quot;schema&quot;, agora obsoleta. Se &quot;schemaRef&quot; estiver ausente do conjunto de dados ou não contiver um valor, você precisará verificar a presença de uma propriedade &quot;schema&quot;. Isso pode ser feito substituindo &quot;schemaRef&quot; por &quot;schema&quot; no `properties` parâmetro de consulta na chamada anterior. Mais detalhes sobre a propriedade &quot;schema&quot; estão disponíveis no [Propriedade &quot;schema&quot; do conjunto de dados](#dataset-schema-property-deprecated---eol-2019-05-30) a seguir.

**Formato da API**

```http
GET /schemaregistry/tenant/schemas/{url encoded schemaRef.id}
```

**Solicitação**

A solicitação usa o URL codificado `id` O URI do esquema (o valor do atributo &quot;schemaRef.id&quot;) e requer um cabeçalho Accept.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F274f17bc5807ff307a046bab1489fb18 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1' \
```

O formato da resposta depende do tipo de cabeçalho Aceitar enviado na solicitação. As solicitações de pesquisa também exigem uma `version` ser incluído no cabeçalho Aceitar. A tabela a seguir descreve os cabeçalhos Aceitar disponíveis para pesquisas:

| Accept | Descrição |
| ------ | ----------- |
| `application/vnd.adobe.xed-id+json` | Solicitações de lista (GET), títulos, IDs e versões |
| `application/vnd.adobe.xed-full+json; version={major version}` | $refs e allOf resolvidos, têm títulos e descrições |
| `application/vnd.adobe.xed+json; version={major version}` | Simples com $ref e allOf, tem títulos e descrições |
| `application/vnd.adobe.xed-notext+json; version={major version}` | Simples com $ref e allOf, sem títulos ou descrições |
| `application/vnd.adobe.xed-full-notext+json; version={major version}` | $refs e allOf resolvidos, sem títulos ou descrições |
| `application/vnd.adobe.xed-full-desc+json; version={major version}` | $refs e allOf resolvidos, descritores incluídos |

>[!NOTE]
>
>`application/vnd.adobe.xed-id+json` e `application/vnd.adobe.xed-full+json; version={major version}` são os cabeçalhos Aceitar mais usados. `application/vnd.adobe.xed-id+json` é preferível para listar recursos na [!DNL Schema Registry] como retorna somente o &quot;title&quot;, &quot;id&quot; e &quot;version&quot;. `application/vnd.adobe.xed-full+json; version={major version}` é preferível para exibir um recurso específico (por sua &quot;id&quot;), pois retorna todos os campos (aninhados em &quot;propriedades&quot;), bem como títulos e descrições.

**Resposta**

O esquema JSON retornado descreve a estrutura e as informações de nível de campo (&quot;tipo&quot;, &quot;formato&quot;, &quot;mínimo&quot;, &quot;máximo&quot; etc.) dos dados, serializados como JSON. Se estiver usando um formato de serialização diferente de JSON para assimilação (como Parquet ou Scala), a variável [Guia do Registro de Schema](../xdm/tutorials/create-schema-api.md) contém uma tabela que mostra o tipo de JSON desejado (&quot;meta:xdmType&quot;) e sua representação correspondente em outros formatos.

Juntamente com esta tabela, a variável [!DNL Schema Registry] O Guia do desenvolvedor contém exemplos detalhados de todas as chamadas possíveis que podem ser feitas usando o [!DNL Schema Registry] API.

### Propriedade &quot;esquema&quot; do conjunto de dados (DEPRECATED - EOL 2019-05-30)

Os conjuntos de dados podem conter uma propriedade de &quot;esquema&quot; que agora está obsoleta e permanece disponível temporariamente para compatibilidade com versões anteriores. Por exemplo, uma solicitação de listagem (GET) semelhante à feita anteriormente, em que &quot;schema&quot; foi substituído por &quot;schemaRef&quot; no `properties` parâmetro de consulta, pode retornar o seguinte:

```json
{
  "5ba9452f7de80400007fc52a": {
    "name": "Sample Dataset 1",
    "description": "Description of Sample Dataset 1.",
    "schema": "@/xdms/context/person"
  }
}
```

Se a propriedade &quot;schema&quot; de um conjunto de dados for preenchida, isso indica que o esquema está obsoleto `/xdms` esquema e, quando suportado, o conector ETL deve usar o valor na propriedade &quot;schema&quot; com o parâmetro `/xdms` endpoint (um endpoint obsoleto no [[!DNL Catalog API]](https://www.adobe.io/experience-platform-apis/references/catalog/)) para recuperar o esquema herdado.

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
>Um parâmetro de consulta opcional, `expansion=xdm`, instrui a API a expandir totalmente e embutir qualquer esquema referenciado. Você pode querer fazer isso ao apresentar uma lista de todos os campos em potencial ao usuário.

**Resposta**

Semelhante às etapas para [exibição do esquema do conjunto de dados](#view-dataset-schema), a resposta contém um esquema JSON que descreve a estrutura e as informações no nível de campo dos dados, serializados como JSON.

>[!NOTE]
>
>Quando o campo &quot;schema&quot; estiver vazio ou totalmente ausente, o conector deverá ler o campo &quot;schemaRef&quot; e usar o [API do registro de esquema](https://www.adobe.io/experience-platform-apis/references/schema-registry/) conforme mostrado nas etapas anteriores para [exibir um esquema de conjunto de dados](#view-dataset-schema).

### A propriedade &quot;observableSchema&quot;

A propriedade &quot;observableSchema&quot; de um conjunto de dados tem uma estrutura JSON que corresponde à do JSON do esquema XDM. O &quot;observableSchema&quot; contém os campos que estavam presentes nos arquivos de entrada recebidos. Ao gravar dados no [!DNL Experience Platform], um usuário não precisa usar todos os campos do esquema de destino. Em vez disso, eles devem fornecer apenas os campos que estão sendo usados.

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

O aplicativo ETL pode fornecer um recurso para visualizar dados ([&quot;Figura 8&quot; no Fluxo de trabalho ETL](./workflow.md)). A API de acesso a dados fornece várias opções para visualizar dados.

Informações adicionais, incluindo a orientação passo a passo para visualizar dados usando a API de acesso a dados, podem ser encontradas no [tutorial sobre acesso a dados](../data-access/tutorials/dataset-data.md).

### Obter detalhes do conjunto de dados usando o parâmetro de consulta &quot;propriedades&quot;

Como mostrado nas etapas acima para [exibir uma lista de conjuntos de dados](#view-list-of-datasets), você pode solicitar &quot;arquivos&quot; usando o parâmetro de consulta &quot;propriedades&quot;.

Você pode consultar a [Visão geral do Serviço de catálogo](../catalog/home.md) para obter informações detalhadas sobre como consultar conjuntos de dados e filtros de resposta disponíveis.

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

### Listar arquivos de conjunto de dados usando o atributo &quot;arquivos&quot;

Também é possível usar uma solicitação GET para buscar detalhes do arquivo usando o atributo &quot;files&quot;.

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

As IDs de arquivo do conjunto de dados retornadas na resposta anterior podem ser usadas em uma solicitação do GET para buscar mais detalhes do arquivo por meio da [!DNL Data Access] API.

A variável [visão geral do acesso a dados](../data-access/home.md) contém detalhes sobre como usar o [!DNL Data Access] API.

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

A propriedade &quot;href&quot; pode ser usada para buscar dados de visualização por meio da [[!DNL Data Access API]](../data-access/home.md).

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

Mais informações sobre o [!DNL Data Access] incluindo solicitações e respostas detalhadas, está disponível na [visão geral do acesso a dados](../data-access/home.md).

### Obter &quot;fileDescription&quot; do conjunto de dados

O componente de destino como saída de dados transformados, o engenheiro de dados escolherá um conjunto de dados de saída ([&quot;Figura 12&quot; no Fluxo de trabalho ETL](workflow.md)). O esquema XDM está associado ao conjunto de dados de saída. Os dados a serem gravados serão identificados pelo atributo &quot;fileDescription&quot; da entidade do conjunto de dados das APIs de Descoberta de Dados. Essas informações podem ser buscadas usando uma ID de conjunto de dados (`{DATASET_ID}`). A propriedade &quot;fileDescription&quot; na resposta JSON fornecerá as informações solicitadas.

**Formato da API**

```shell
GET /catalog/dataSets/{DATASET_ID}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{DATASET_ID}` | A variável `id` do conjunto de dados que você está tentando acessar. |

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

Os dados serão gravados em [!DNL Experience Platform] usar [API de assimilação de dados](https://www.adobe.io/experience-platform-apis/references/data-ingestion/).  A gravação de dados é um processo assíncrono. Quando os dados são gravados na Adobe Experience Platform, um lote é criado e marcado como bem-sucedido somente após os dados serem totalmente gravados.

Entrada de dados [!DNL Experience Platform] devem ser redigidos sob a forma de ficheiros Parquet.

## Fase de execução

Conforme a execução é iniciada, o conector (conforme definido no componente de origem) lerá os dados de [!DNL Experience Platform] usando o [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/). O processo de transformação lerá os dados de um determinado intervalo de tempo. Internamente, ele consultará lotes de conjuntos de dados de origem. Durante a consulta, ele usará uma data de início parametrizada (rolagem para dados de séries de tempo ou dados incrementais) e listará arquivos de conjunto de dados para esses lotes e começará a fazer solicitações de dados para esses arquivos de conjunto de dados.

### Exemplo de transformações

A variável [exemplos de transformações ETL](./transformations.md) O documento contém várias transformações de exemplo, incluindo manipulação de identidade e mapeamentos de tipo de dados. Use essas transformações para referência.

### Ler dados de [!DNL Experience Platform]

Usar o [[!DNL Catalog API]](https://www.adobe.io/experience-platform-apis/references/catalog/), você pode buscar todos os lotes entre uma hora de início e uma hora de término especificadas e classificá-los pela ordem em que foram criados.

**Solicitação**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches?dataSet=DATASETID&createdAfter=START_TIMESTAMP&createdBefore=END_TIMESTAMP&sort=desc:created" \
  -H "Accept: application/json" \
  -H "Authorization:Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

Detalhes sobre a filtragem de lotes podem ser encontrados na [Tutorial de acesso a dados](../data-access/tutorials/dataset-data.md).

### Obter arquivos de um lote

Depois de ter a ID do lote que você está procurando (`{BATCH_ID}`), é possível recuperar uma lista de arquivos pertencentes a um lote específico por meio da [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/).  Os detalhes para fazer isso estão disponíveis no [[!DNL Data Access] tutorial](../data-access/tutorials/dataset-data.md).

**Solicitação**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/files" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

### Acessar arquivos usando a ID do arquivo

Uso do identificador exclusivo de um arquivo (`{FILE_ID`), o [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/) O pode ser usado para acessar os detalhes específicos do arquivo, incluindo o nome, o tamanho em bytes e um link para baixá-lo.

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

A variável [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/) para acessar o conteúdo de um arquivo específico. Para buscar o conteúdo, uma solicitação GET é feita usando o valor retornado para `_links.self.href` ao acessar um arquivo usando a ID do arquivo.

**Solicitação**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/{DATASET_FILE_ID}?path=filename1.csv" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

A resposta a essa solicitação contém o conteúdo do arquivo. Para obter mais informações, incluindo detalhes sobre paginação de resposta, consulte a [Como consultar dados por meio da API de acesso a dados](../data-access/tutorials/dataset-data.md) tutorial.

### Validar registros para conformidade com esquema

Quando os dados estão sendo gravados, os usuários podem optar por validar os dados de acordo com as regras de validação definidas no esquema XDM. Mais informações sobre validação de esquema podem ser encontradas no [ETL Ecosystem Integration Reference Code on (Código de referência de integração de ecossistemas ETL em) [!DNL GitHub]](https://github.com/adobe/experience-platform-etl-reference/blob/fd08dd9f74ae45b849d5482f645f859f330c1951/README.md#validation).

Se você estiver usando a implementação de referência encontrada em [[!DNL GitHub]](https://github.com/adobe/experience-platform-etl-reference/blob/fd08dd9f74ae45b849d5482f645f859f330c1951/README.md), você pode ativar a validação de esquema nesta implementação usando a propriedade do sistema `-DenableSchemaValidation=true`.

A validação pode ser executada para tipos XDM lógicos, usando atributos como `minLength` e `maxlength` para strings, `minimum` e `maximum` para números inteiros e muito mais. A variável [Guia do desenvolvedor da API do registro de esquema](../xdm/api/getting-started.md) contém uma tabela que descreve os tipos XDM e as propriedades que podem ser usadas para validação.

>[!NOTE]
>
>Os valores mínimo e máximo fornecidos para vários `integer` tipos são os valores MÍN. e MAX que o tipo pode suportar, mas esses valores podem ser restritos ainda mais aos mínimos e máximos de sua escolha.

### Criar um lote

Depois que os dados forem processados, a ferramenta ETL gravará os dados em [!DNL Experience Platform] usando o [API de assimilação em lote](https://www.adobe.io/experience-platform-apis/references/data-ingestion/). Antes de serem adicionados a um conjunto de dados, os dados devem estar vinculados a um lote que será carregado posteriormente em um conjunto de dados específico.

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

Detalhes para criar um lote, incluindo solicitações e respostas de amostra, podem ser encontrados no [Visão geral da assimilação em lote](../ingestion/batch-ingestion/overview.md).

### Gravar no conjunto de dados

Depois de criar um novo lote com êxito, os arquivos podem ser carregados para um conjunto de dados específico. Vários arquivos podem ser publicados em um lote até que ele seja promovido. Os arquivos podem ser carregados usando a API de Upload de Arquivo Pequeno. No entanto, se os arquivos forem muito grandes e o limite do gateway for excedido, você poderá usar a API de Upload de Arquivo Grande. Detalhes para usar o Upload de arquivos grandes e pequenos podem ser encontrados na [Visão geral da assimilação em lote](../ingestion/batch-ingestion/overview.md).

**Solicitação**

Entrada de dados [!DNL Experience Platform] devem ser redigidos sob a forma de ficheiros Parquet.

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

Depois que todos os arquivos tiverem sido carregados no lote, o lote poderá ser marcado para conclusão. Ao fazer isso, o [!DNL Catalog] Entradas &quot;DataSetFile&quot; são criadas para os arquivos concluídos e associadas ao lote de geração. A variável [!DNL Catalog] Em seguida, o lote é marcado como bem-sucedido, o que aciona fluxos downstream para assimilar os dados disponíveis.

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

Antes de executar novas tarefas na ferramenta ETL, verifique se o último lote foi concluído com êxito. A variável [[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/) O fornece uma opção específica de lote que fornece os detalhes dos lotes relevantes.

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

Um status de lote individual pode ser recuperado por meio da variável [[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/) emitindo um pedido GET utilizando o método `{BATCH_ID}`. A variável `{BATCH_ID}` usado será o mesmo que a ID retornada quando o lote for criado.

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

Para fazer isso, os administradores de dados do cliente usarão o [!DNL Platform] Interface para remover os lotes que contêm dados corrompidos. Em seguida, o ETL provavelmente precisará ser executado novamente, preenchendo novamente com dados corretos. Se a própria fonte tiver dados corrompidos, o engenheiro/administrador de dados precisará corrigir os lotes de origem e assimilar novamente os dados (no Adobe Experience Platform ou por meio de conectores ETL).

Com base no tipo de dados gerado, será a escolha do engenheiro de dados remover um único lote ou todos os lotes de determinados conjuntos de dados. Os dados serão removidos/arquivados de acordo [!DNL Experience Platform] diretrizes.

É um cenário provável de que a funcionalidade ETL para limpar dados seja importante.

Quando a limpeza for concluída, os administradores do cliente precisarão reconfigurar o Adobe Experience Platform para reiniciar o processamento dos serviços principais a partir do momento em que os lotes forem excluídos.

## Processamento em lote simultâneo

A critério do cliente, os administradores/engenheiros de dados podem decidir extrair, transformar e carregar dados de maneira sequencial ou simultânea, dependendo das características de um conjunto de dados específico. Isso também se baseará no caso de uso para o qual o cliente está direcionando com os dados transformados.

Por exemplo, se o cliente persistir em um armazenamento de persistência atualizável e a sequência ou a ordem dos eventos for importante, o cliente poderá precisar processar estritamente os trabalhos com transformações ETL sequenciais.

Em outros casos, dados fora de ordem podem ser processados por aplicativos/processos downstream que classificam internamente usando um carimbo de data e hora especificado. Nesses casos, as transformações ETL paralelas podem ser viáveis para melhorar os tempos de processamento.

Para lotes de origem, ele dependerá novamente da preferência do cliente e da restrição do consumidor. Se os dados de origem puderem ser coletados em paralelo, independentemente da regência/ordem de uma linha, o processo de transformação poderá criar lotes de processos com um grau mais alto de paralelismo (otimização baseada no processamento fora de ordem). Mas se a transformação precisar respeitar carimbos de data e hora ou alterar a ordem de precedência, o agendador/invocador de ferramentas da API de acesso a dados ou ETL terá que garantir que os lotes não sejam processados fora de ordem, quando possível.

## Adiamento

Adiamento é um processo no qual os dados de entrada ainda não estão completos o suficiente para serem enviados aos processos de downstream, mas podem ser utilizáveis no futuro. Os clientes determinarão sua tolerância individual à janela de dados para correspondência futura em relação ao custo do processamento para informar sua decisão de deixar os dados de lado e reprocessá-los na próxima execução de transformação, esperando que eles possam ser enriquecidos e reconciliados/compilados em algum momento futuro dentro da janela de retenção. Esse ciclo está em andamento até que a linha seja processada o suficiente ou considerada muito obsoleta para continuar investindo no. Cada iteração gerará dados adiados, que são um superconjunto de todos os dados adiados em iterações anteriores.

A Adobe Experience Platform não identifica dados adiados no momento, portanto, as implementações de clientes devem confiar nas configurações manuais de ETL e conjunto de dados para criar outro conjunto de dados no [!DNL Platform] espelhamento do conjunto de dados de origem que pode ser usado para manter dados adiados. Nesse caso, os dados adiados serão semelhantes aos dados do instantâneo. Em cada execução da transformação ETL, os dados de origem serão unidos aos dados adiados e enviados para processamento.

## Changelog

| Data | Ação | Descrição |
| ---- | ------ | ----------- |
| 2019-01-19 | Propriedade &quot;fields&quot; removida dos conjuntos de dados | Anteriormente, os conjuntos de dados incluíam uma propriedade &quot;fields&quot; que continha uma cópia do esquema. Esse recurso não deve mais ser usado. Se a propriedade &quot;fields&quot; for encontrada, ela deverá ser ignorada e &quot;observedSchema&quot; ou &quot;schemaRef&quot; deverá ser usado em seu lugar. |
| 2019-03-15 | Propriedade &quot;schemaRef&quot; adicionada aos conjuntos de dados | A propriedade &quot;schemaRef&quot; de um conjunto de dados contém um URI que faz referência ao esquema XDM no qual o conjunto de dados se baseia e representa todos os campos potenciais que podem ser usados pelo conjunto de dados. |
| 2019-03-15 | Todos os identificadores do usuário final são mapeados para a propriedade &quot;identityMap&quot; | O &quot;identityMap&quot; é um encapsulamento de todos os identificadores exclusivos de um assunto, como CRM ID, ECID ou ID do programa de fidelidade. Este mapa é usado por [[!DNL Identity Service]](../identity-service/home.md) para resolver todas as identidades conhecidas e anônimas de um assunto, formando um único gráfico de identidade para cada usuário final. |
| 2019-05-30 | EOL e remover a propriedade &quot;schema&quot; dos conjuntos de dados | A propriedade &quot;schema&quot; do conjunto de dados forneceu um link de referência para o esquema usando o modelo obsoleto `/xdms` endpoint na variável [!DNL Catalog] API. Isso foi substituído por um &quot;schemaRef&quot; que fornece a &quot;id&quot;, &quot;version&quot; e &quot;contentType&quot; do esquema conforme referenciado no novo [!DNL Schema Registry] API. |
