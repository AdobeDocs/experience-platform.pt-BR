---
keywords: Experience Platform, home, tópicos populares, acesso aos dados, api de acesso aos dados, acesso aos dados da consulta
solution: Experience Platform
title: Visualizar dados do conjunto de dados usando a API de acesso a dados
topic-legacy: tutorial
type: Tutorial
description: Saiba como localizar, acessar e baixar dados armazenados em um conjunto de dados usando a API de acesso a dados no Adobe Experience Platform. Você também será apresentado a alguns dos recursos exclusivos da API de acesso a dados, como paginação e downloads parciais.
exl-id: 1c1e5549-d085-41d5-b2c8-990876000f08
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1390'
ht-degree: 4%

---

# Exibir dados do conjunto de dados usando [!DNL Data Access] API

Este documento fornece um tutorial passo a passo que aborda como localizar, acessar e baixar dados armazenados em um conjunto de dados usando o [!DNL Data Access] API no Adobe Experience Platform. Você também será apresentado a alguns dos recursos exclusivos do [!DNL Data Access] API, como paginação e downloads parciais.

## Introdução

Este tutorial requer um entendimento prático sobre como criar e preencher um conjunto de dados. Consulte a [tutorial de criação de conjunto de dados](../../catalog/datasets/create.md) para obter mais informações.

As seções a seguir fornecem informações adicionais que você precisará saber para fazer chamadas com êxito para as APIs da plataforma.

### Lendo exemplos de chamadas de API

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações do . Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de exemplo retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler exemplos de chamadas de API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no [!DNL Experience Platform] guia de solução de problemas.

### Coletar valores para cabeçalhos necessários

Para fazer chamadas para [!DNL Platform] As APIs devem ser concluídas primeiro [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todos [!DNL Experience Platform] Chamadas de API, conforme mostrado abaixo:

- Autorização: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Todos os recursos em [!DNL Experience Platform] são isoladas em sandboxes virtuais específicas. Todas as solicitações para [!DNL Platform] As APIs exigem um cabeçalho que especifica o nome da sandbox em que a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre sandboxes em [!DNL Platform], consulte o [documentação de visão geral da sandbox](../../sandboxes/home.md).

Todas as solicitações que contêm uma carga útil (POST, PUT, PATCH) exigem um cabeçalho adicional:

- Tipo de conteúdo: application/json

## Diagrama de sequência

Este tutorial segue as etapas descritas no diagrama de sequência abaixo, destacando a funcionalidade principal do [!DNL Data Access] API.</br>
![](../images/sequence_diagram.png)

O [!DNL Catalog] A API permite recuperar informações relacionadas a lotes e arquivos. O [!DNL Data Access] A API permite acessar e baixar esses arquivos via HTTP como downloads completos ou parciais, dependendo do tamanho do arquivo.

## Localizar os dados

Antes de começar a usar a variável [!DNL Data Access] , é necessário identificar o local dos dados que deseja acessar. No [!DNL Catalog] Na API, há dois endpoints que você pode usar para navegar pelos metadados de uma organização e recuperar a ID de um lote ou arquivo que você deseja acessar:

- `GET /batches`: Retorna uma lista de lotes em sua organização
- `GET /dataSetFiles`: Retorna uma lista de arquivos em sua organização

Para obter uma lista abrangente de endpoints no [!DNL Catalog] Consulte a API [Referência da API](https://www.adobe.io/experience-platform-apis/references/catalog/).

## Recupere uma lista de lotes na organização IMS

Usar o [!DNL Catalog] Você pode retornar uma lista de lotes em sua organização:

**Formato da API**

```http
GET /batches
```

**Solicitação**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/batches/' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

A resposta inclui um objeto que lista todos os lotes relacionados à Organização IMS, com cada valor de nível superior representando um lote. Os objetos de lote individuais contêm os detalhes para esse lote específico. A resposta abaixo foi minimizada para espaço.

```json
{
    "{BATCH_ID_1}": {
        "imsOrg": "{ORG_ID}",
        "created": 1516640135526,
        "createdClient": "{CREATED_CLIENT}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "updated": 1516640135526,
        "status": "processing",
        "version": "1.0.0",
        "availableDates": {}
    },
    "{BATCH_ID_2}": {
    ...
    }
}
```

### Filtrar a lista de lotes

Geralmente, os filtros são solicitados a localizar um determinado lote para recuperar dados relevantes para um caso de uso específico. Os parâmetros podem ser adicionados a um `GET /batches` para filtrar a resposta retornada. A solicitação abaixo retornará todos os lotes criados após um tempo especificado, em um conjunto de dados específico, classificados por quando foram criados.

**Formato da API**

```http
GET /batches?createdAfter={START_TIMESTAMP}&dataSet={DATASET_ID}&sort={SORT_BY}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{START_TIMESTAMP}` | O carimbo de data e hora de início em milissegundos (por exemplo, 1514836799000). |
| `{DATASET_ID}` | O identificador do conjunto de dados. |
| `{SORT_BY}` | Classifica a resposta pelo valor fornecido. Por exemplo, `desc:created` classifica os objetos por data de criação em ordem decrescente. |

**Solicitação**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/batches?createdAfter=1521053542579&dataSet=5cd9146b21dae914b71f654f&orderBy=desc:created' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

```json
{   "{BATCH_ID_3}": {
        "imsOrg": "{ORG_ID}",
        "relatedObjects": [
            {
                "id": "5c01a91863540f14cd3d0439",
                "type": "dataSet"
            },
            {
                "id": "00998255b4a148a2bfd4804c2f327324",
                "type": "batch"
            }
        ],
        "status": "success",
        "metrics": {
            "recordsFailed": 0,
            "recordsWritten": 2,
            "startTime": 1550791835809,
            "endTime": 1550791994636
        },
        "errors": [],
        "created": 1550791457173,
        "createdClient": "{CLIENT_CREATED}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "updated": 1550792060301,
        "version": "1.0.116"
    },
    "{BATCH_ID_4}": {
        "imsOrg": "{ORG_ID}",
        "status": "success",
        "relatedObjects": [
            {
                "type": "batch",
                "id": "00aff31a9ae84a169d69b886cc63c063"
            },
            {
                "type": "dataSet",
                "id": "5bfde8c5905c5a000082857d"
            }
        ],
        "metrics": {
            "startTime": 1544571333876,
            "endTime": 1544571358291,
            "recordsRead": 4,
            "recordsWritten": 4
        },
        "errors": [],
        "created": 1544571077325,
        "createdClient": "{CLIENT_CREATED}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "updated": 1544571368776,
        "version": "1.0.3"
    }
}
```

Uma lista completa de parâmetros e filtros pode ser encontrada no [Referência da API do catálogo](https://www.adobe.io/experience-platform-apis/references/catalog/).

## Recuperar uma lista de todos os arquivos pertencentes a um determinado lote

Agora que você tem a ID do lote que deseja acessar, é possível usar a variável [!DNL Data Access] API para obter uma lista de arquivos pertencentes a esse lote.

**Formato da API**

```http
GET /batches/{BATCH_ID}/files
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{BATCH_ID}` | Identificador de lote do lote que você está tentando acessar. |

**Solicitação**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/5c6f332168966814cd81d3d3/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

```json
{
    "data": [
        {
            "dataSetFileId": "8dcedb36-1cb2-4496-9a38-7b2041114b56-1",
            "dataSetViewId": "5cc6a9b60d4a5914b7940a7f",
            "version": "1.0.0",
            "created": "1558522305708",
            "updated": "1558522305708",
            "isValid": false,
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1"
                }
            }
        }
    ],
    "_page": {
        "limit": 100,
        "count": 1
    }
}
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `data._links.self.href` | O URL para acessar esse arquivo. |

A resposta contém uma matriz de dados que lista todos os arquivos dentro do lote especificado. Os arquivos são referenciados pela ID do arquivo, que é encontrada na variável `dataSetFileId` campo.

## Acessar um arquivo usando uma ID de arquivo

Depois de ter uma ID de arquivo exclusiva, você pode usar a variável [!DNL Data Access] API para acessar os detalhes específicos sobre o arquivo, incluindo seu nome, tamanho em bytes e um link para baixá-lo.

**Formato da API**

```http
GET /files/{FILE_ID}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{FILE_ID}` | O identificador do arquivo que você deseja acessar. |

**Solicitação**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Dependendo de a ID de arquivo apontar para um arquivo individual ou um diretório, a matriz de dados retornada pode conter uma única entrada ou uma lista de arquivos pertencentes a esse diretório. Cada elemento de arquivo conterá detalhes como o nome do arquivo, o tamanho em bytes e um link para baixar o arquivo.

**Caso 1: A ID de arquivo aponta para um único arquivo**

**Resposta**

```json
{
    "data": [
        {
            "name": "{FILE_NAME}.parquet",
            "length": "249058",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_1}?path={FILE_NAME_1}.parquet"
                }
            }
        }
    ],
    "_page": {
        "limit": 100,
        "count": 1
    }
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{FILE_NAME}.parquet` | O nome do arquivo. |
| `_links.self.href` | O URL para baixar o arquivo. |

**Caso 2: A ID de arquivo aponta para um diretório**

**Resposta**

```json
{
    "data": [
        {
            "dataSetFileId": "{FILE_ID_2}",
            "dataSetViewId": "460590b01ba38afd1",
            "version": "1.0.0",
            "created": "150151267347",
            "updated": "150151267347",
            "isValid": true,
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_2}"
                }
            }
        },
        {
            "dataSetFileId": "{FILE_ID_3}",
            "dataSetViewId": "460590b01ba38afd1",
            "version": "1.0.0",
            "created": "150151267685",
            "updated": "150151267685",
            "isValid": true,
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_3}"
                }
            }
        }
    ],
    "_page": {
        "limit": 100,
        "count": 2
    }
}
```

| Propriedade | Descrição |
| -------- | ----------- | 
| `data._links.self.href` | O URL para baixar o arquivo associado. |

Essa resposta retorna um diretório contendo dois arquivos separados, com IDs `{FILE_ID_2}` e `{FILE_ID_3}`. Nesse cenário, é necessário seguir o URL de cada arquivo para acessar o arquivo.

## Recuperar os metadados de um arquivo

Você pode recuperar os metadados de um arquivo fazendo uma solicitação de HEAD. Isso retorna os cabeçalhos de metadados do arquivo, incluindo seu tamanho em bytes e formato de arquivo.

**Formato da API**

```http
HEAD /files/{FILE_ID}?path={FILE_NAME}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{FILE_ID}` | O identificador do arquivo. |
| `{FILE_NAME}` | O nome do arquivo (por exemplo, profiles.parquet) |

**Solicitação**

```shell
curl -I 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1?path=profiles.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Os cabeçalhos de resposta contêm os metadados do arquivo consultado, incluindo:
- `Content-Length`: Indica o tamanho da carga em bytes
- `Content-Type`: Indica o tipo de arquivo.

## Acessar o conteúdo de um arquivo

Você também pode acessar o conteúdo de um arquivo usando a variável [!DNL Data Access] API.

**Formato da API**

```shell
GET /files/{FILE_ID}?path={FILE_NAME}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{FILE_ID}` | O identificador do arquivo. |
| `{FILE_NAME}` | O nome do arquivo (por exemplo, profiles.parquet). |

**Solicitação**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1?path=profiles.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o conteúdo do arquivo.

## Baixar conteúdo parcial de um arquivo

O [!DNL Data Access] A API permite baixar arquivos em partes. É possível especificar um cabeçalho de intervalo durante uma `GET /files/{FILE_ID}` solicitação para baixar um intervalo específico de bytes de um arquivo. Se o intervalo não for especificado, a API baixará o arquivo inteiro por padrão.

O exemplo de HEAD no [seção anterior](#retrieve-the-metadata-of-a-file) O fornece o tamanho de um arquivo específico em bytes.

**Formato da API**

```http
GET /files/{FILE_ID}?path={FILE_NAME}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{FILE_ID} ` | O identificador do arquivo. |
| `{FILE_NAME}` | O nome do arquivo (por exemplo, profiles.parquet) |

**Solicitação**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1?path=profiles.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Range: bytes=0-99'
```

| Propriedade | Descrição |
| -------- | ----------- | 
| `Range: bytes=0-99` | Especifica o intervalo de bytes a serem baixados. Se isso não for especificado, a API baixará o arquivo inteiro. Neste exemplo, os primeiros 100 bytes serão baixados. |

**Resposta**

O corpo da resposta inclui os primeiros 100 bytes do arquivo (conforme especificado pelo cabeçalho &quot;Intervalo&quot; na solicitação) junto com o Status HTTP 206 (Conteúdo Parcial). A resposta também inclui os seguintes cabeçalhos:

- Duração do conteúdo: 100 (o número de bytes retornados)
- Tipo de conteúdo: application/parquet (um arquivo Parquet foi solicitado, portanto, o tipo de conteúdo da resposta é `parquet`)
- Intervalo de conteúdo: bytes 0-99/249058 (o intervalo solicitado (0-99) do número total de bytes (249058))

## Configurar a paginação de resposta da API

Respostas no [!DNL Data Access] As APIs são paginadas. Por padrão, o número máximo de entradas por página é 100. Parâmetros de paginação podem ser usados para modificar o comportamento padrão.

- `limit`: Você pode especificar o número de entradas por página de acordo com seus requisitos usando o parâmetro &quot;limit&quot;.
- `start`: O deslocamento pode ser definido pelo parâmetro de consulta &quot;start&quot;.
- `&`: Você pode usar um E comercial para combinar vários parâmetros em uma única chamada.

**Formato da API**

```http
GET /batches/{BATCH_ID}/files?start={OFFSET}
GET /batches/{BATCH_ID}/files?limit={LIMIT}
GET /batches/{BATCH_ID}/files?start={OFFSET}&limit={LIMIT}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{BATCH_ID}` | Identificador de lote do lote que você está tentando acessar. |
| `{OFFSET}` | O índice especificado para iniciar a matriz de resultados (por exemplo, start=0) |
| `{LIMIT}` | Controla quantos resultados são retornados na matriz de resultados (por exemplo, limit=1) |

**Solicitação**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/5c102cac7c7ebc14cd6b098e/files?start=0&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**:

A resposta contém um `"data"` matriz com um único elemento, conforme especificado pelo parâmetro de solicitação `limit=1`. Esse elemento é um objeto que contém os detalhes do primeiro arquivo disponível, conforme especificado pela variável `start=0` na solicitação (lembre-se de que na numeração baseada em zero, o primeiro elemento é &quot;0&quot;).

O `_links.next.href` contém o link para a próxima página de respostas, onde você pode ver que a variável `start` O parâmetro foi avançado para `start=1`.

```json
{
    "data": [
        {
            "dataSetFileId": "{FILE_ID_1}",
            "dataSetViewId": "5a9f264c2aa0cf01da4d82fa",
            "version": "1.0.0",
            "created": "1521053793635",
            "updated": "1521053793635",
            "isValid": false,
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_1}"
                }
            }
        }
    ],
    "_page": {
        "limit": 1,
        "count": 6
    },
    "_links": {
        "next": {
            "href": "https://platform.adobe.io/data/foundation/export/batches/5c102cac7c7ebc14cd6b098e/files?start=1&limit=1"
        },
        "page": {
            "href": "https://platform.adobe.io/data/foundation/export/batches/5c102cac7c7ebc14cd6b098e/files?start=0&limit=1",
            "templated": true
        }
    }
}
```
