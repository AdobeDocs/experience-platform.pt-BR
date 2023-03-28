---
keywords: Experience Platform; home; tópicos populares; serviço de fluxo;
title: Fluxos de dados de rascunho usando a API do serviço de fluxo
description: Saiba como definir seus fluxos de dados em um estado de rascunho usando a API do Serviço de fluxo.
badge: label="Novo recurso" type="Positivo"
source-git-commit: d093e34ae4b353d1ed6db922b6da66cf23f25c48
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 3%

---

# Fluxos de dados de rascunho usando a API do Serviço de fluxo

Salve seus fluxos de dados como rascunhos ao usar a API do Serviço de fluxo fornecendo o `mode=draft` parâmetro de consulta durante a chamada de criação de fluxo. Os rascunhos podem ser atualizados posteriormente com novas informações e depois publicados assim que estiverem prontos. Este tutorial aborda as etapas para definir seus fluxos de dados em um estado de rascunho usando a API do Serviço de Fluxo.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../home.md): [!DNL Experience Platform] permite que os dados sejam assimilados de várias fontes, fornecendo a capacidade de estruturar, rotular e aprimorar os dados recebidos usando [!DNL Platform] serviços.
* [Sandboxes](../../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

### Pré-requisitos

Este tutorial requer que você já tenha gerado os ativos necessários para criar um fluxo de dados. Isso inclui o seguinte:

* Uma conexão base autenticada
* Uma conexão de origem
* Um esquema XDM de destino
* Um conjunto de dados de destino
* Uma conexão de destino
* Um mapeamento

Se você ainda não tiver esses valores, selecione uma fonte de [o catálogo na visão geral das fontes](../../home.md). Em seguida, siga as instruções dessa fonte específica para gerar os ativos necessários para projetar um fluxo de dados.

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da plataforma com êxito, consulte o guia em [introdução às APIs do Platform](../../../landing/api-guide.md).

## Definir um fluxo de dados para um estado de rascunho

As seções a seguir descrevem o processo para definir um fluxo de dados como rascunho, atualizar o fluxo de dados, publicar o fluxo de dados e, eventualmente, excluir o fluxo de dados.

### Rascunho de um fluxo de dados

Para definir um fluxo de dados como rascunho, faça uma solicitação de POST para a `/flows` endpoint ao adicionar o `mode=draft` como parâmetro de consulta. Isso permite criar um fluxo de dados e salvá-lo como rascunho.

**Formato da API**

```http
POST /flows?mode=draft
```

| Parâmetro | Descrição |
| --- | --- |
| `mode` | Um parâmetro de consulta fornecido pelo usuário que decide o estado do fluxo de dados. Para definir um fluxo de dados como rascunho, defina `mode` para `draft`. |

**Solicitação**

A solicitação a seguir cria um fluxo de dados de rascunho.

```shell
  'https://platform-int.adobe.io/data/foundation/flowservice/flows?mode=draft' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "HTTP source dataflow for ACME data",
    "sourceConnectionIds": [
        "61c0c5f1-bfe5-40f7-8f8c-a4dc175ddac6"
    ],
    "targetConnectionIds": [
        "78f41c31-3652-4a5e-b264-74331226dcf3"
    ],
    "flowSpec": {
        "id": "c1a19761-d2c7-4702-b9fa-fe91f0613e81",
        "version": "1.0"
    }
  }'
```

**Resposta**

Uma resposta bem-sucedida retorna a variável `id` e os `etag` do seu fluxo de dados.

```json
{
  "id": "c9751426-dff8-49b0-965f-50defcf4187b",
  "etag": "\"69057131-0000-0200-0000-640f48320000\""
}
```

### Atualizar um fluxo de dados

Para atualizar seu rascunho, faça uma solicitação de PATCH para a `/flows` endpoint ao fornecer a ID do fluxo de dados que deseja atualizar. Durante essa etapa, você também deve fornecer um `If-Match` parâmetro header , que corresponde ao `etag` do fluxo de dados que você deseja atualizar.

**Formato da API**

```http
PATCH /flows/{FLOW_ID}
```

**Solicitação**

As solicitações a seguir adicionam transformações de mapeamento ao fluxo de dados rascunhado.

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/flowservice/flows/c9751426-dff8-49b0-965f-50defcf4187b' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -H 'If-Match: "69057131-0000-0200-0000-640f48320000"' \
  -d '[
        {
          "op": "add",
          "path": "/transformations",
          "value": [
              {
                  "name": "Mapping",
                  "params": {
                      "mappingId": "44d42ed27c46499a80eb0c0705c38cbd",
                      "mappingVersion": 0
                  }
              }
          ]
      }
  ]'
```

**Resposta**

Uma resposta bem-sucedida retorna a ID do fluxo e `etag`. Para verificar a alteração, você pode fazer uma solicitação do GET para o `/flows` endpoint ao fornecer a ID do fluxo.

```json
{
  "id": "c9751426-dff8-49b0-965f-50defcf4187b",
  "etag": "\"69057131-0000-0200-0000-640f48320000\""
}
```

### Publicar um fluxo de dados

Quando o rascunho estiver pronto para ser publicado, faça uma solicitação de POST para a variável `/flows` endpoint ao fornecer a ID do fluxo de dados de rascunho que deseja publicar, bem como uma operação de ação para publicação.

**Formato da API**

```http
POST /flows/{FLOW_ID}/action?op=publish
```

| Parâmetro | Descrição |
| --- | --- |
| `op` | Uma operação de ação que atualiza o estado do fluxo de dados consultado. Para publicar um fluxo de dados de rascunho, defina `op` para `publish`. |

**Solicitação**

A solicitação a seguir publica o fluxo de dados de rascunho.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows/c9751426-dff8-49b0-965f-50defcf4187b/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Resposta**

Uma resposta bem-sucedida retorna a ID e a `etag` do seu fluxo de dados.

```json
{
  "id": "c9751426-dff8-49b0-965f-50defcf4187b",
  "etag": "\"69057131-0000-0200-0000-640f48320000\""
}
```

### Excluir um fluxo de dados

Para excluir seu fluxo de dados, faça uma solicitação de DELETE para o `/flows` endpoint ao fornecer a ID do fluxo de dados que deseja excluir. Para obter etapas detalhadas sobre como excluir um fluxo de dados usando a API do Serviço de fluxo, leia o guia em [exclusão de um fluxo de dados na API](./delete-dataflows.md).