---
keywords: Experience Platform;home;popular topics;identidades de lista;cluster de listas;home;popular topics;identities;
solution: Experience Platform
title: Lista de todas as identidades em um cluster
topic: API guide
description: As identidades que estão relacionadas em um gráfico de identidade, independentemente da namespace, são consideradas parte do mesmo "cluster" nesse gráfico de identidade. As opções abaixo fornecem os meios para acessar todos os membros do cluster.
translation-type: tm+mt
source-git-commit: 73035aec86297cfc4ee9337cf922d599001379c3
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 1%

---


# Lista de todas as identidades em um cluster

As identidades que estão relacionadas em um gráfico de identidade, independentemente da namespace, são consideradas parte do mesmo &quot;cluster&quot; nesse gráfico de identidade. As opções abaixo fornecem os meios para acessar todos os membros do cluster.

## Obter identidades associadas para uma única identidade

Recupere todos os membros do cluster para obter uma única identidade.

Você pode usar o parâmetro opcional `graph-type` para indicar o gráfico de identidade do qual o cluster será obtido. As opções são:

- Nenhum - Não execute nenhum ajuste de identidade.
- Gráfico privado - Realize a identificação com base no seu gráfico de identidade particular. Se nenhum `graph-type` for fornecido, esse será o padrão.

**Formato da API**

```http
GET https://platform-{REGION}.adobe.io/data/core/identity/cluster/members?{PARAMETERS}
```

**Solicitação**

Opção 1: Forneça a identidade como namespace (`nsId`, por ID) e valor de ID (`id`).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/members?nsId=411&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Opção 2: Forneça a identidade como namespace (`ns`, por nome) e valor de ID (`id`).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/members?ns=AMO&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Opção 3: Forneça a identidade como XID (`xid`). Para obter mais informações sobre como obter um XID de identidade, consulte a seção desse documento cobrindo [obter o XID de uma identidade](./list-native-id.md).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/members?xid=CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

## Obter identidades associadas para várias identidades

Use `POST` como um equivalente em lote do método `GET` descrito acima para retornar as identidades nos clusters de várias identidades.

>[!NOTE]
>
>O pedido deve indicar no máximo 1000 identidades. As solicitações que excederem 1000 identidades resultarão em um código de status 400.

**Formato da API**

```http
POST https://platform-{REGION}.adobe.io/data/core/identity/clusters/members
```

**Solicitação**

A solicitação a seguir demonstra o fornecimento de uma lista de XIDs para a qual recuperar membros do cluster.

**Solicitação de Stub**

O uso do cabeçalho `x-uis-cst-ctx: stub` retornará uma resposta com bloqueio. Esta é uma solução temporária para facilitar o progresso do desenvolvimento da integração precoce, enquanto os serviços estão sendo concluídos. Isso será substituído quando não for mais necessário.

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/clusters/members \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-uis-cst-ctx: stub' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "xids": ["GYMBWaoXbMtZ1j4eAAACepuQGhs","b2NJK9a5X7x4LVE4rUqkMyM"]
}'
```

**Chamar usando XIDs**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/clusters/members \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "xids": ["GYMBWaoXbMtZ1j4eAAACepuQGhs","b2NJK9a5X7x4LVE4rUqkMyM"],
    "graph-type": "Private Graph"
}' | json_pp
```

**Chamar usando UIDs**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/clusters/members \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

**Resposta &quot;estubada&quot;**

```json
{
   "version": 1,
   "clusters": [{
           "xid": "GZsBQnHQaGtL46ZKSvO9bNRE1DcUyQA",
           "compositeXid": {
               "nsid": 411,
               "id": "WRbM7AAAAJ_PBZHl"
           },
           "members": ["e8138f65-d3d3-4485-a7e1-6712e047349d", "21312343536983537571245438594"],
           "members": [{
                   "nsid": 0,
                   "id": "27064814400205787570627663430729680462"
               },
               {
                   "nsid": 411,
                   "id": "86826386186182763871263871263876128612"
               }
           ]
       },
       {
           "xid": "CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8",
           "compositeXid": {
               "nsid": 411,
               "id": "WRbM7AAAAJ_PBZHl"
           },
           "members": [],
           "members": []
       }
   ],
   "unprocessedXids": ["cb0665db616f49758713252d8a335c1e"],
   "unprocessedNids": [{
       "nsid": 411,
       "id": "WY-RNgAAArI4rGBo"
   }]
}
```

**Resposta completa**

```json
{
   "unprocessedXids": [],
   "unprocessedNids": [],
   "version": "1.0.0",
   "clusters": [{
           "xid": "411|WRbM7AAAAJ_PBZHl",
           "members": [
               "411|WRbM7AAAAJ_PBZHl",
               "0|47713142741924778930324734610798294416"
           ],
           "compositeXid": {
               "nsid": 411,
               "id": "WRbM7AAAAJ_PBZHl"
           },
           "members": [{
                   "nsid": 411,
                   "id": "WRbM7AAAAJ_PBZHl"
               },
               {
                   "nsid": 0,
                   "id": "47713142741924778930324734610798294416"
               }
           ]
       },
       {
           "xid": "411|WY-RNgAAArI4rGBo",
           "compositeXid": {
               "nsid": 411,
               "id": "WY-RNgAAArI4rGBo"
           },
           "members": [
               "411|WY-RNgAAArI4rGBo",
               "411|WY-RNgAAArI4rGGy"
           ],
           "members": [{
                   "nsid": 411,
                   "id": "WY-RNgAAArI4rGBo"
               },
               {
                   "nsid": 411,
                   "id": "WY-RNgAAArI4rGGy"
               }
           ]

       }
   ]
}
```

>[!NOTE]
>
>A resposta sempre terá uma entrada para cada XID fornecido na solicitação, independentemente de os XIDs de uma solicitação pertencerem ao mesmo cluster ou se um ou mais têm algum cluster associado.

## Próximas etapas

Vá para o próximo tutorial para [lista do histórico de cluster de uma identidade](./list-cluster-history.md)