---
keywords: Experience Platform;home;popular topics;identity xid;XID
solution: Experience Platform
title: Obter a ID nativa de uma identidade
topic: API guide
description: Os dados de identidade normalmente são fornecidos como um valor de sequência de ID e namespace de identidade nos dados XDM ingeridos e ao fornecer uma identidade para uso em uma chamada de API. Quando as identidades são persistentes no Serviço de identidade, uma ID é gerada e atribuída a essa identidade, chamada de XID nativo. APIs de plataforma que exigem suporte a dados de identidade usando esse formulário mais compacto para a ID agregada e a namespace. XID é uma string codificada em base64.
translation-type: tm+mt
source-git-commit: 0af537e965605e6c3e02963889acd85b9d780654
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 0%

---


# Obter o XID para uma identidade

Os dados de identidade normalmente são fornecidos como um valor de sequência de ID e namespace de identidade nos dados XDM ingeridos e ao fornecer uma identidade para uso em uma chamada de API. Quando as identidades são persistentes em [!DNL Identity Service], uma ID é gerada e atribuída a essa identidade, chamada de XID nativo. [!DNL Platform] As APIs que exigem suporte a dados de identidade usando esse formulário mais compacto para a ID agregada e a namespace. XID é uma string codificada em base64.

>[!NOTE]
>
>Esse formato é usado principalmente para Adobe interno. O XID nativo como um valor singular é mais eficiente em termos de espaço e é o que é usado internamente em [!DNL Platform] soluções para armazenamento e serialização. No entanto, ele não é legível pelo ser humano, é opaco e requer uma chamada separada para obtê-lo para uso.

Adquira o XID para obter um determinado valor de ID e namespace usando o serviço descrito nesta seção.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

```json
{
    "xid":"BVrqzwVuzbXrLfmnaG3rXrLf3KJg"
}
```
