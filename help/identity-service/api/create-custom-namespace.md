---
keywords: Experience Platform;página inicial;tópicos populares;namespace;namespaces;namespaces;namespace de identidade;namespace de identidade;identidade;identidade
solution: Experience Platform
title: Criar um namespace personalizado na API do serviço de identidade
description: Usando a API de namespace de identidade, você pode criar um namespace de identidade personalizado que estará disponível somente para sua organização.
role: Developer
exl-id: 6015a225-4508-49cc-9dda-fb9f73a8746c
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 5%

---

# Criar um namespace personalizado na API do serviço de identidade

Usando a API [!DNL Identity Namespace], você pode criar um namespace de identidade personalizado que estará disponível somente para sua organização.

Para obter recomendações sobre como criar namespaces personalizados, consulte [a documentação de Perguntas frequentes do Serviço de Identidade](../troubleshooting-guide.md).

>[!NOTE]
>
>Namespaces são um qualificador para identidades. Sendo assim, uma vez criado, o namespace não poderá ser excluído.

**Formato da API**

```http
POST /idnamespace/identities
```

**Solicitação**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/idnamespace/identities \
  -H 'Accept-Encoding: gzip, deflate' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -d '{
        "name": "Loyalty Member",
        "code": "Loyalty",
        "description": "Loyalty Program Member ID",
        "idType": "Cross_device"
      }'
```

**Resposta**

```json
{
    "updateTime": 1576286879075,
    "code": "Loyalty",
    "status": "ACTIVE",
    "description": "Loyalty Program Member ID",
    "id": 10093197,
    "createTime": 1576286879075,
    "idType": "Cross_device",
    "name": "Loyalty Member",
    "custom": true
}
```

## Próximas etapas

Prossiga para o próximo tutorial para [listar a ID nativa de uma identidade](./list-native-id.md)
