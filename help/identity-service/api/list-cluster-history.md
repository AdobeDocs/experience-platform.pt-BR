---
keywords: Experience Platform;página inicial;tópicos populares;identidades;histórico de cluster
solution: Experience Platform
title: Obter Histórico de Cluster de uma Identidade
description: As identidades podem mover clusters ao longo de várias execuções de gráficos de dispositivos. O Serviço de identidade oferece visibilidade das associações de cluster de uma determinada identidade ao longo do tempo.
role: Developer
exl-id: e52edb15-e3d6-4085-83d5-212bbd952632
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 2%

---

# Obter o histórico de cluster de uma identidade

As identidades podem mover clusters ao longo de várias execuções de gráficos de dispositivos. [!DNL Identity Service] fornece visibilidade sobre as associações de cluster de uma determinada identidade ao longo do tempo.

Use o parâmetro `graph-type` opcional para indicar o tipo de saída do qual obter o cluster. As opções são:

- `None` - Não executar compilação de identidade.
- `Private Graph` - Executar compilação de identidade com base em seu gráfico de identidade privado. Se nenhum `graph-type` for fornecido, este será o padrão.

## Obter o histórico de cluster de uma única identidade

**Formato da API**

```http
GET https://platform-{REGION}.adobe.io/data/core/identity/cluster/history
```

**Solicitação**

Opção 1: Forneça a identidade como namespace (`nsId`, por ID) e valor de ID (`id`).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/history?nsId=411&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Opção 2: Forneça a identidade como namespace (`ns`, por nome) e valor de ID (`id`).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/history?ns=AMO&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Opção 3: Forneça a identidade como XID (`xid`). Para obter mais informações sobre como obter o XID de uma identidade, consulte a seção deste documento que aborda a [obtenção do XID de uma identidade](./list-native-id.md).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/history?xid=CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

## Obter o histórico do cluster de várias identidades

Use o método `POST` como um equivalente em lote do método `GET` descrito acima para retornar os históricos de cluster de várias identidades.

>[!NOTE]
>
>A solicitação não deve indicar mais de 1000 identidades. Solicitações que excedem 1000 identidades resultarão em um código de status 400.

**Formato da API**

```http
POST https://platform-va7.adobe.io/data/core/identity/clusters/history
```

**Solicitar corpo**

Opção 1: Forneça uma lista de XIDs para os quais recuperar membros de cluster.

```shell
{
    "xids": ["GYMBWaoXbMtZ1j4eAAACepuQGhs","b2NJK9a5X7x4LVE4rUqkMyM"],
    "graph-type": "Private Graph"
}
```

Opção 2: forneça uma lista de identidades como IDs compostas, onde cada uma nomeia o valor da ID e o namespace pelo código do namespace.

```shell
{
    "compositeXids": [{
            "ns": "AdCloud",
            "id": "WRbM7AAAAJ_PBZHl"
        },
        {
            "ns": "AddCloud",
            "id": "WY-RNgAAArI4rGBo"
        }
    ]
}
```

**Solicitação**

**Solicitação de stub**

O uso do cabeçalho `x-uis-cst-ctx: stub` retornará uma resposta com stub. Esta é uma solução temporária para facilitar o progresso do desenvolvimento da integração inicial, enquanto os serviços estão sendo concluídos. Isso será descontinuado quando não for mais necessário.

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/clusters/history \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-uis-cst-ctx: stub' \
  -d '{
        "xids": ["GYMBWaoXbMtZ1j4eAAACepuQGhs","b2NJK9a5X7x4LVE4rUqkMyM"],
        "graph-type": "Private Graph"
      }'
```

**Usando XIDs**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/clusters/history \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "xids": ["GYMBWaoXbMtZ1j4eAAACepuQGhs","b2NJK9a5X7x4LVE4rUqkMyM"],
        "graph-type": "Private Graph"
      }' | json_pp
```

**Usando UIDs**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/clusters/history \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "compositeXids": [{
                "nsid": 411,
                "id": "WRbM7AAAAJ_PBZHl"
            },
            {
                "nsid": 411,
                "id": "WY-RNgAAArI4rGBo"
            }
        ],
        "graph-type": "Private Graph"
      }' | json_pp
```

**Resposta**

```json
{
    "version": 1,
    "xidsClusterHistory": [{
            "xid": "GZsBQnHQaGtL46ZKSvO9bNRE1DcUyQA",
            "compositeXid": {
                "nsid": 411,
                "id": "WY-RNgAAArI4rGBo"
            },
            "clusterHistory": [{
                    "clusterId": "4c686f23-0871-41c2-b4f4-adef89f6bd2c",
                    "cRecordedTS": "1504741401382"
                },
                {
                    "clusterId": "29bf066c-971a-11e7-abc4-cec278b6b50a",
                    "cRecordedTS": "1502063001629"
                },
                {
                    "clusterId": "aeb2f60c-b0f1-446a-91dd-d28ab6a44ff9",
                    "cRecordedTS": "1499384601763"
                }
            ]
        },
        {
            "xid": "CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8",
            "compositeXid": {
                "nsid": 411,
                "id": "WY-RNgAAArI4rGBo"
            },
            "clusterHistory": [{
                "clusterId": "4c686f23-0871-41c2-b4f4-adef89f6bd2c",
                "cRecordedTS": "1504741401937"
            }]
        }
    ],
    "unprocessedXids": ["cb0665db616f49758713252d8a335c1e"],
    "unprocessedNids": [{
        "nsid": 411,
        "id": "WY-RNgAAArI4rGBo"
    }]

}
```

>[!NOTE]
>
>A resposta sempre terá uma entrada para cada XID fornecido na solicitação, independentemente de os XIDs de uma solicitação pertencerem ao mesmo cluster ou se um ou mais tiverem algum cluster associado.

## Próximas etapas

Prossiga para o próximo tutorial para [listar mapeamentos de identidade](./list-identity-mappings.md)
