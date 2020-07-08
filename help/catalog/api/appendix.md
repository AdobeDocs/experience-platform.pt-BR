---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Apêndice do guia do desenvolvedor do serviço de catálogo
topic: developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '908'
ht-degree: 0%

---


# Apêndice do guia do desenvolvedor do serviço de catálogo

Este documento contém informações adicionais para ajudá-lo a trabalhar com a API de catálogo.

## Visualização de objetos interrelacionados {#view-interrelated-objects}

Alguns objetos de Catálogo podem ser inter-relacionados a outros objetos de Catálogo. Quaisquer campos prefixados por `@` em cargas de resposta denotam objetos relacionados. Os valores desses campos assumem a forma de um URI, que pode ser usado em uma solicitação GET separada para recuperar os objetos relacionados que representam.

O conjunto de dados de exemplo retornado no documento ao [procurar um conjunto de dados](look-up-object.md) específico contém um `files` campo com o seguinte valor de URI: `"@/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files"`. O conteúdo do `files` campo pode ser visualizado usando este URI como o caminho para uma nova solicitação GET.

**Formato da API**

```http
GET {OBJECT_URI}
```

| Parâmetro | Descrição |
| --- | --- |
| `{OBJECT_URI}` | O URI fornecido pelo campo de objeto inter-relacionado (excluindo o `@` símbolo). |

**Solicitação**

A solicitação a seguir usa o URI fornecido como `files` propriedade do conjunto de dados de exemplo para recuperar uma lista dos arquivos associados do conjunto de dados.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista de objetos relacionados. Neste exemplo, uma lista de arquivos de conjunto de dados é retornada.

```json
{
    "7d501090-0280-11ea-a6bb-f18323b7005c-1": {
        "id": "7d501090-0280-11ea-a6bb-f18323b7005c-1",
        "batchId": "7d501090-0280-11ea-a6bb-f18323b7005c",
        "dataSetViewId": "5ba9452f7de80400007fc52b",
        "imsOrg": "{IMS_ORG}",
        "createdUser": "{USER_ID}",
        "createdClient": "{CLIENT_ID}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1573256315368,
        "updated": 1573256315368
    },
    "148ac690-0280-11ea-8d23-8571a35dce49-1": {
        "id": "148ac690-0280-11ea-8d23-8571a35dce49-1",
        "batchId": "148ac690-0280-11ea-8d23-8571a35dce49",
        "dataSetViewId": "5ba9452f7de80400007fc52b",
        "imsOrg": "{IMS_ORG}",
        "createdUser": "{USER_ID}",
        "createdClient": "{CLIENT_ID}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1573255982433,
        "updated": 1573255982433
    },
    "64dd5e19-8ea4-4ddd-acd1-f43cccd8eddb-1": {
        "id": "64dd5e19-8ea4-4ddd-acd1-f43cccd8eddb-1",
        "batchId": "64dd5e19-8ea4-4ddd-acd1-f43cccd8eddb",
        "dataSetViewId": "5ba9452f7de80400007fc52b",
        "imsOrg": "{IMS_ORG}",
        "createdUser": "{USER_ID}",
        "createdClient": "{CLIENT_ID}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1569499425037,
        "updated": 1569499425037
    }
}
```

## Fazer várias solicitações em uma única chamada

O endpoint raiz da API de catálogo permite que várias solicitações sejam feitas em uma única chamada. A carga da solicitação contém uma matriz de objetos que representam o que normalmente seriam solicitações individuais, que são então executadas em ordem.

Se essas solicitações forem modificações ou adições ao Catálogo e qualquer uma das alterações falhar, todas as alterações serão revertidas.

**Formato da API**

```http
POST /
```

**Solicitação**

A solicitação a seguir cria um novo conjunto de dados e, em seguida, cria visualizações relacionadas para esse conjunto de dados. Este exemplo demonstra o uso de linguagem de modelo para acessar valores retornados em chamadas anteriores para uso em chamadas subsequentes.

Por exemplo, se você deseja fazer referência a um valor que foi retornado de uma subsolicitação anterior, é possível criar uma referência no formato: `<<{REQUEST_ID}.{ATTRIBUTE_NAME}>>` (onde `{REQUEST_ID}` é a ID fornecida pelo usuário para a subsolicitação, conforme demonstrado abaixo). É possível fazer referência a qualquer atributo disponível no corpo de um objeto de resposta de subsolicitação anterior usando esses modelos.

>[!NOTE]
>
>Quando uma subsolicitação executada retorna somente a referência a um objeto (como é o padrão para a maioria das solicitações POST e PUT na API de catálogo), essa referência recebe alias do valor `id` e pode ser usada como `<<{OBJECT_ID}.id>>`.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
    {
      "id": "firstObjectId",
      "resource": "/dataSets",
      "method": "post",
      "body": {
        "type": "raw",
        "name": "First Dataset"
      }
    }, 
    {
      "id": "secondObjectId",
      "resource": "/datasetViews",
      "method": "post",
      "body": {
        "status": "enabled",
        "dataSetId": "<<firstObjectId.id>>"
      }
    }
  ]'
```

| Propriedade | Descrição |
| --- | --- |
| `id` | ID fornecida pelo usuário que está anexada ao objeto de resposta para que você possa corresponder solicitações a respostas. O catálogo não armazena esse valor e simplesmente o retorna na resposta para fins de referência. |
| `resource` | O caminho do recurso relativo à raiz da API de catálogo. O protocolo e o domínio não devem fazer parte deste valor e devem receber o prefixo &quot;/&quot;. <br/><br/> Ao usar PATCH ou DELETE como a ID da subsolicitação `method`, inclua a ID do objeto no caminho do recurso. Para não ser confundido com o fornecido pelo usuário, `id`o caminho do recurso usa a ID do próprio objeto Catalog (por exemplo, `resource: "/dataSets/1234567890"`). |
| `method` | O nome do método (GET, PUT, POST, PATCH ou DELETE) relacionado à ação realizada na solicitação. |
| `body` | O documento JSON que normalmente seria transmitido como carga em uma solicitação POST, PUT ou PATCH. Esta propriedade não é necessária para solicitações GET ou DELETE. |

**Resposta**

Uma resposta bem-sucedida retorna uma matriz de objetos que contém o `id` que você atribuiu a cada solicitação, o código de status HTTP para a solicitação individual e a resposta `body`. Como as três solicitações de amostra foram todas para criar novos objetos, o `body` de cada objeto é uma matriz que contém apenas a ID do objeto recém-criado, como é o padrão com as respostas POST mais bem-sucedidas no Catálogo.

```json
[
    {
        "id": "firstObjectId",
        "code": 200,
        "body": [
            "@/dataSets/5be230aef5b02914cd52dbfa"
        ]
    },
    {
        "id": "secondObjectId",
        "code": 200,
        "body": [
            "@/dataSetViews/5be230aef5b02914cd52dbfb"
        ]
    }
]
```

Tenha cuidado ao inspecionar a resposta a uma solicitação múltipla, pois será necessário verificar o código de cada solicitação individual e não depender apenas do código de status HTTP da solicitação POST pai.  É possível que uma única subsolicitação retorne um 404 (como uma solicitação GET em um recurso inválido) enquanto a solicitação geral retorna 200.

## Cabeçalhos de solicitação adicionais

O Catálogo fornece várias convenções de cabeçalho para ajudar a manter a integridade dos seus dados durante as atualizações.

### Se-Correspondência

É uma boa prática usar o controle de versão de objetos para evitar o tipo de corrupção de dados que ocorre quando um objeto é salvo por vários usuários quase simultaneamente.

A prática recomendada ao atualizar um objeto envolve primeiro fazer uma chamada de API para a visualização (GET) do objeto a ser atualizado. Contido na resposta (e em qualquer chamada em que a resposta contenha um único objeto) é um `E-Tag` cabeçalho que contém a versão do objeto. Adicionar a versão do objeto como um cabeçalho de solicitação chamado `If-Match` nas chamadas de atualização (PUT ou PATCH) resultará na atualização somente se a versão ainda for a mesma, ajudando a evitar a colisão de dados.

Se as versões não corresponderem (o objeto foi modificado por outro processo desde que foi recuperado), você receberá o status HTTP 412 (Falha na pré-condição) indicando que o acesso ao recurso do público alvo foi negado.

### Pragma

Ocasionalmente, talvez você queira validar um objeto sem salvar as informações. Usar o `Pragma` cabeçalho com um valor de `validate-only` permite enviar solicitações POST ou PUT somente para fins de validação, impedindo que quaisquer alterações nos dados sejam persistentes.

## compactação de dados

Compaction é um serviço Experience Platform que une dados de arquivos pequenos em arquivos maiores sem alterar dados. Por motivos de desempenho, às vezes é benéfico combinar um conjunto de arquivos pequenos em arquivos maiores para fornecer acesso mais rápido aos dados ao ser consultado.

Quando os arquivos em um lote ingerido forem compactados, seu objeto de Catálogo associado será atualizado para fins de monitoramento.