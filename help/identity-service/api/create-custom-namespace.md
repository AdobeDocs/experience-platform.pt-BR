---
keywords: Experience Platform;home;popular topics;namespace;Namespace;namespaces;Namespaces;identity namespace;Identity namespace;identity;Identity
solution: Experience Platform
title: Criar uma namespace personalizada
topic: API guide
description: Usando a API de Namespace de identidade, você pode criar uma namespace de identidade personalizada que estará disponível somente para sua organização.
translation-type: tm+mt
source-git-commit: 3376d6cace9ab196f457e2bf7b84cde06693103c
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 4%

---


# Criação de uma namespace personalizada

Usando a [!DNL Identity Namespace] API, você pode criar uma namespace de identidade personalizada que estará disponível somente para sua organização.

Para obter recomendações sobre como criar namespaces personalizadas, consulte [a documentação](../troubleshooting-guide.md)de Perguntas frequentes do Serviço de identidade.

>[!NOTE]
>
>Namespaces são qualificadores de identidades. Como tal, uma namespace criada não pode ser excluída.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

Vá para o próximo tutorial para [lista da ID nativa de uma identidade](./list-native-id.md)