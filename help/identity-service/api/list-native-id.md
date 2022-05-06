---
keywords: Experience Platform, home, tópicos populares, identificação xid, XID
solution: Experience Platform
title: Obter a ID nativa de uma identidade
topic-legacy: API guide
description: Os dados de identidade geralmente são fornecidos como um valor de sequência de ID e namespace de identidade em dados XDM assimilados e ao fornecer uma identidade para uso em uma chamada de API. Quando as identidades são persistentes no Serviço de identidade, uma ID é gerada e atribuída a essa identidade, chamada de XID nativa. APIs da plataforma que exigem suporte a dados de identidade usando esse formulário mais compacto para a ID agregada e o namespace. XID é uma string codificada em base64.
exl-id: e734f5d8-e00b-43fa-b06c-97c73e1f7c71
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 1%

---

# Obter a ID nativa de uma identidade

Os dados de identidade geralmente são fornecidos como um valor de sequência de ID e namespace de identidade em dados XDM assimilados e ao fornecer uma identidade para uso em uma chamada de API. Quando as identidades forem mantidas em [!DNL Identity Service], uma ID é gerada e atribuída a essa identidade, chamada de XID nativo. [!DNL Platform] As APIs que exigem suporte a dados de identidade usando esse formulário mais compacto para a ID agregada e o namespace. XID é uma string codificada em base64.

>[!NOTE]
>
>Esse formato é usado principalmente para Adobe interno. O XID nativo como um valor singular é mais eficiente em termos de espaço e é o que é usado internamente no [!DNL Platform] soluções para armazenamento e serialização. No entanto, não é legível por seres humanos, é opaco e requer uma chamada separada para obter o uso.

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
