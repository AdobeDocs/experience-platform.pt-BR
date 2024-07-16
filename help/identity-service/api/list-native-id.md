---
keywords: Experience Platform;página inicial;tópicos populares;identidade xid;XID
solution: Experience Platform
title: Obter a ID nativa de uma identidade
description: Os dados de identidade normalmente são fornecidos como um valor de sequência de ID e um namespace de identidade nos dados XDM assimilados e ao fornecer uma identidade para uso em uma chamada de API. Quando as identidades persistem no Serviço de identidade, uma ID é gerada e atribuída a essa identidade, chamada de XID nativo. APIs da Platform que exigem suporte a dados de identidade usando essa forma mais compacta para a ID agregada e o namespace. XID é uma sequência de caracteres codificada na base64.
role: Developer
exl-id: e734f5d8-e00b-43fa-b06c-97c73e1f7c71
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 1%

---

# Obter a ID nativa de uma identidade

Os dados de identidade normalmente são fornecidos como um valor de sequência de ID e um namespace de identidade nos dados XDM assimilados e ao fornecer uma identidade para uso em uma chamada de API. Quando as identidades são persistentes em [!DNL Identity Service], uma ID é gerada e atribuída a essa identidade, chamada de XID nativo. [!DNL Platform] APIs que exigem suporte a dados de identidade usando esta forma mais compacta para a ID agregada e o namespace. XID é uma sequência de caracteres codificada na base64.

>[!NOTE]
>
>Esse formato é principalmente para uso interno em Adobe. O XID nativo como um valor singular é mais eficiente em termos de espaço e é usado internamente nas soluções [!DNL Platform] para armazenamento e serialização. No entanto, ele não é legível por humanos, é opaco e requer uma chamada separada para ser utilizado.

Adquira o XID para um determinado valor de ID e namespace usando o serviço descrito nesta seção.

**Formato da API**

```http
GET https://platform-{REGION}.adobe.io/data/core/identity/identity?namespace={NAMESPACE}&id={ID_VALUE}
```

**Solicitação**

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/identity?namespace=email&id=test@adobetest.com' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

```json
{
    "xid":"BVrqzwVuzbXrLfmnaG3rXrLf3KJg"
}
```
