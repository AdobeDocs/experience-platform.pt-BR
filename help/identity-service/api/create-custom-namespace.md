---
keywords: Experience Platform, home, tópicos populares, namespace, namespace, namespaces, namespaces, namespace de identidade, namespace de identidade, identidade, identidade
solution: Experience Platform
title: Criar um namespace personalizado na API do serviço de identidade
description: Usando a API de Namespace de identidade, você pode criar um namespace de identidade personalizado que estará disponível somente para sua organização.
exl-id: 6015a225-4508-49cc-9dda-fb9f73a8746c
source-git-commit: ad9fb0bcc7bca55da432c72adc94d49e3c63ad6e
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 5%

---

# Criar um namespace personalizado na API do serviço de identidade

Usar o [!DNL Identity Namespace] Você pode criar um namespace de identidade personalizado que estará disponível somente para sua organização.

Para obter recomendações sobre como criar namespaces personalizados, consulte [a documentação de perguntas frequentes do Serviço de identidade](../troubleshooting-guide.md).

>[!NOTE]
>
>Namespaces são um qualificador para identidades. Dessa forma, depois que um namespace é criado, ele não pode ser excluído.

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

Acesse o próximo tutorial para [listar a ID nativa de uma identidade](./list-native-id.md)
