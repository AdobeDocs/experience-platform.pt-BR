---
keywords: Experience Platform;página inicial;tópicos populares;Serviço de catálogo;api de catálogo;apêndice
solution: Experience Platform
title: Apêndice do Guia da API do Serviço de catálogo
description: Este documento contém informações adicionais para ajudar você a trabalhar com a API do catálogo no Adobe Experience Platform.
exl-id: fafc8187-a95b-4592-9736-cfd9d32fd135
source-git-commit: 24db94b959d1bad925af1e8e9cbd49f20d9a46dc
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 1%

---

# Apêndice do guia de API [!DNL Catalog Service]

Este documento contém informações adicionais para ajudar você a trabalhar com a API [!DNL Catalog].

## Exibir objetos inter-relacionados {#view-interrelated-objects}

Alguns objetos [!DNL Catalog] podem ser inter-relacionados com outros objetos [!DNL Catalog]. Quaisquer campos que tenham o prefixo `@` em cargas de resposta denotam objetos relacionados. Os valores desses campos tomam a forma de um URI, que pode ser usado em uma solicitação do GET separada para recuperar os objetos relacionados que representam.

O conjunto de dados de exemplo retornado no documento em [procurando um conjunto de dados específico](look-up-object.md) contém um campo `files` com o seguinte valor de URI: `"@/datasetFiles?datasetId={DATASET_ID}"`. O conteúdo do campo `files` pode ser visualizado usando esse URI como o caminho para uma nova solicitação GET.

**Formato da API**

```http
GET {OBJECT_URI}
```

| Parâmetro | Descrição |
| --- | --- |
| `{OBJECT_URI}` | O URI fornecido pelo campo de objeto inter-relacionado (excluindo o símbolo `@`). |

**Solicitação**

A solicitação a seguir usa o URI fornecido com a propriedade `files` do conjunto de dados de exemplo para recuperar uma lista dos arquivos associados do conjunto de dados.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/datasetFiles?datasetId={DATASET_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
        "imsOrg": "{ORG_ID}",
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
        "imsOrg": "{ORG_ID}",
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
        "imsOrg": "{ORG_ID}",
        "createdUser": "{USER_ID}",
        "createdClient": "{CLIENT_ID}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1569499425037,
        "updated": 1569499425037
    }
}
```

## Cabeçalhos de solicitação adicionais

O [!DNL Catalog] fornece várias convenções de cabeçalho para ajudar você a manter a integridade dos dados durante as atualizações.

### Se-Correspondência

É uma boa prática usar o controle de versão de objetos para evitar o tipo de corrupção de dados que ocorre quando um objeto é salvo por vários usuários quase simultaneamente.

A prática recomendada ao atualizar um objeto envolve primeiro fazer uma chamada de API para exibir (GET) o objeto a ser atualizado. Contido na resposta (e qualquer chamada em que a resposta contenha um único objeto) é um cabeçalho `E-Tag` que contém a versão do objeto. Adicionar a versão do objeto como um cabeçalho de solicitação chamado `If-Match` em suas chamadas de atualização (PUT ou PATCH) resultará na atualização apenas se a versão ainda for a mesma, ajudando a evitar colisão de dados.

Se as versões não corresponderem (o objeto foi modificado por outro processo desde que você o recuperou), você receberá o status HTTP 412 (Falha na pré-condição), indicando que o acesso ao recurso de destino foi negado.

### Pragma

Ocasionalmente, talvez você queira validar um objeto sem salvar as informações. O uso do cabeçalho `Pragma` com um valor de `validate-only` permite enviar solicitações POST ou PUT somente para fins de validação, impedindo que as alterações nos dados sejam persistentes.

## Compactação de dados

A compactação é um serviço [!DNL Experience Platform] que mescla dados de arquivos pequenos em arquivos maiores sem alterar dados. Por motivos de desempenho, às vezes é útil combinar um conjunto de arquivos pequenos em arquivos maiores para fornecer acesso mais rápido aos dados ao serem consultados.

Quando os arquivos em um lote assimilado tiverem sido compactados, seu objeto [!DNL Catalog] associado será atualizado para fins de monitoramento.
