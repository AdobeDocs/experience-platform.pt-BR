---
keywords: Experience Platform;página inicial;tópicos populares;serviço de fluxo;
title: Rascunho de fluxos de dados usando a API do serviço de fluxo
description: Saiba como definir seus fluxos de dados em um estado de rascunho usando a API do Serviço de fluxo.
badge: label="Novo recurso" type="Positivo"
exl-id: aad6a302-1905-4a23-bc3d-39e76c9a22da
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 3%

---

# Rascunhos de fluxos de dados usando a API de serviço de fluxo

Salve seus fluxos de dados como rascunhos ao usar a API de serviço de fluxo fornecendo a `mode=draft` parâmetro de consulta durante a chamada de criação do fluxo. Os rascunhos podem ser atualizados posteriormente com novas informações e publicados quando estiverem prontos. Este tutorial aborda as etapas para definir seus fluxos de dados em um estado de rascunho usando a API de serviço de fluxo.

## Introdução

Este tutorial requer que você tenha uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Origens](../../home.md): [!DNL Experience Platform] O permite que os dados sejam assimilados de várias fontes e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando o [!DNL Platform] serviços.
* [Sandboxes](../../../sandboxes/home.md): [!DNL Experience Platform] O fornece sandboxes virtuais que particionam uma única [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

### Pré-requisitos

Este tutorial requer que você já tenha gerado os ativos necessários para criar um fluxo de dados. Isso inclui o seguinte:

* Uma conexão de base autenticada
* Uma conexão de origem
* Um esquema XDM do Target
* Um conjunto de dados de destino
* Uma conexão de destino
* Um mapeamento

Se você ainda não tiver esses valores, selecione uma origem em [o catálogo na visão geral das origens](../../home.md). Em seguida, siga as instruções dessa fonte para gerar os ativos necessários para elaborar um fluxo de dados.

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da Platform com êxito, consulte o manual em [introdução às APIs da Platform](../../../landing/api-guide.md).

## Definir um fluxo de dados para o estado de rascunho

As seções a seguir descrevem o processo para definir um fluxo de dados como rascunho, atualizar o fluxo de dados, publicar o fluxo de dados e, por fim, excluir o fluxo de dados.

### Rascunhar um fluxo de dados

Para definir um fluxo de dados como rascunho, faça uma solicitação POST à `/flows` ao adicionar o `mode=draft` como parâmetro de consulta. Isso permite criar um fluxo de dados e salvá-lo como rascunho.

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

Uma resposta bem-sucedida retorna a variável `id` e as correspondentes `etag` do seu fluxo de dados.

```json
{
  "id": "c9751426-dff8-49b0-965f-50defcf4187b",
  "etag": "\"69057131-0000-0200-0000-640f48320000\""
}
```

### Atualizar um fluxo de dados

Para atualizar o rascunho, faça uma solicitação PATCH ao `/flows` ao fornecer a ID do fluxo de dados que você deseja atualizar. Durante essa etapa, você também deve fornecer um `If-Match` parâmetro de cabeçalho, que corresponde ao `etag` do fluxo de dados que você deseja atualizar.

**Formato da API**

```http
PATCH /flows/{FLOW_ID}
```

**Solicitação**

As solicitações a seguir adicionam transformações de mapeamento ao fluxo de dados de rascunho.

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

Uma resposta bem-sucedida retorna a ID de fluxo e `etag`. Para verificar a alteração, você pode fazer uma solicitação GET para a `/flows` ao fornecer a ID do fluxo.

```json
{
  "id": "c9751426-dff8-49b0-965f-50defcf4187b",
  "etag": "\"69057131-0000-0200-0000-640f48320000\""
}
```

### Publicar um fluxo de dados

Quando o rascunho estiver pronto para ser publicado, faça uma solicitação POST ao `/flows` ao fornecer a ID do fluxo de dados de rascunho que você deseja publicar, bem como uma operação de ação para publicação.

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

Uma resposta bem-sucedida retorna a ID e a variável `etag` do seu fluxo de dados.

```json
{
  "id": "c9751426-dff8-49b0-965f-50defcf4187b",
  "etag": "\"69057131-0000-0200-0000-640f48320000\""
}
```

### Excluir um fluxo de dados

Para excluir o fluxo de dados, faça uma solicitação DELETE ao `/flows` ao fornecer a ID do fluxo de dados que você deseja excluir. Para obter etapas detalhadas sobre como excluir um fluxo de dados usando a API de Serviço de fluxo, leia o guia em [exclusão de um fluxo de dados na API](./delete-dataflows.md).
