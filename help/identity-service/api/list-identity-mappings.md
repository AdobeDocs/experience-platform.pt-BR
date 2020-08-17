---
keywords: Experience Platform;home;popular topics;identity;Identity
solution: Experience Platform
title: Mapeamentos de identidade de lista
topic: API guide
description: Um mapeamento é uma coleção de todas as identidades em um cluster, para uma namespace especificada.
translation-type: tm+mt
source-git-commit: c081a7521be9715ca32d35504922a70767924fd7
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 1%

---


# Mapeamentos de identidade de lista

Um mapeamento é uma coleção de todas as identidades em um cluster, para uma namespace especificada.

## Obter um mapeamento de identidade para uma única identidade

Dada uma identidade, recupere todas as identidades relacionadas da mesma namespace que a representada pela identidade na solicitação.

**Formato da API**

```http
GET https://platform-{REGION}.adobe.io/data/core/identity/mapping
```

**Solicitação**

Opção 1: Forneça a identidade como namespace (`nsId`, por ID) e valor de ID (`id`).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/mapping?nsId=411&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Opção 2: Forneça a identidade como namespace (`ns`, por nome) e valor de ID (`id`).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/mapping?ns=AMO&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Opção 3: Forneça a identidade como XID (`xid`). Para obter mais informações sobre como obter um XID de identidade, consulte a seção deste documento que cobre a [obtenção do XID para uma identidade](./list-native-id.md).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/mapping?xid=CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

### Obter mapeamentos de identidade para várias identidades

Use o `POST` método como um equivalente em lote do `GET` método descrito acima para recuperar mapeamentos para várias identidades.

>[!NOTE]
>
>O pedido deve indicar no máximo 1000 identidades. As solicitações que excederem 1000 identidades resultarão em um código de status 400.

**Formato da API**

```http
POST https://platform.adobe.io/data/core/identity/mappings
```

**Corpo da solicitação**

Opção 1: Forneça uma lista de XIDs para a qual recuperar mapeamentos.

```shell
{
    "xids": ["GYMBWaoXbMtZ1j4eAAACepuQGhs","b2NJK9a5X7x4LVE4rUqkMyM"],
    "graph-type": "Private Graph"
}
```

Opção 2: Forneça uma lista de identidades como IDs compostas, em que cada uma nomeie o valor da ID e a namespace por ID de namespace. Este exemplo demonstra o uso desse método ao substituir o padrão `graph-type` de &quot;Gráfico privado&quot;.

```shell
{
    "compositeXids": [{
            "nsid": 411,
            "id": "WRbM7AAAAJ_PBZHl"
        },
        {
            "nsid": 411,
            "id": "WY-RNgAAArI4rGBo"
        }
    ],
    "graph-type": "None"
}
```

**Solicitação**

**Uso de XIDs**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/mappings \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: 111111@AdobeOrg' \
  -d '{
        "xids" : ["GesCQXX0CAESEE8wHpswUoLXXmrYy8KBTVgA"],
        "targetNs": "0",
        "graph-type": "Private Graph"
      }' | json_pp
```

**Uso de UIDs**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/mappings \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: 111111@AdobeOrg' \
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
        "targetNs": "0",
        "graph-type": "Private Graph"
      }' | json_pp
```

Se nenhuma identidade relacionada foi encontrada com a entrada fornecida, um código de `HTTP 204` resposta é retornado sem conteúdo.

**Resposta**

```json
{
    "version": 1,
    "mappings": [{
        "xid": "CAESEPl1uYyma1kMDWxx7dhbwGo",
        "mapping": [{
            "xid": "81218968060697815473313992060878182012",
            "lastAssociationTime": "1493310475047"
        }],
        "compositeXid": {
            "nsid": 411,
            "id": "WY-RNgAAArI4rGBo"
        },
        "mapping": [{
            "compositeXid": {
                "nsid": 411,
                "id": "WY-RNchvdsTSJS"
            },
            "lastAssociationTime": "1493310475047"
        }],

        "regions": [{
            "regionId": "10",
            "lastAssociationTime": "1493310475047"
        }]
    }],
    "unprocessedXids": ["cb0665db616f49758713252d8a335c1e"],
    "unprocessedNids": [{
        "nsid": 411,
        "id": "WY-RNgAAArI4rGBo"
    }]
}
```

- `lastAssociationTime`: O carimbo de data e hora quando a identidade de entrada foi associada pela última vez a essa identidade.
- `regions`: Fornece o `regionId` e `lastAssociationTime` para onde a identidade foi vista.

## Próximas etapas

Vá para o próximo tutorial para [lista das namespaces](./list-namespaces.md)disponíveis.
