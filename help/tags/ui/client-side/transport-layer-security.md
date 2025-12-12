---
title: Informações de Segurança da camada de transporte (TLS)
description: Informações sobre quais versões e cifras TLS são usadas
exl-id: 04948cd8-6cf0-4159-a9d3-3130b97af106
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 13%

---

# Informações de Segurança da camada de transporte (TLS)

O TLS (Transport Layer Security) é um protocolo criptográfico que fornece segurança completa para dados enviados entre aplicativos pela Internet. Para obter informações mais detalhadas sobre TLS, leia a [documentação de noções básicas sobre TLS](https://www.internetsociety.org/deploy360/tls/basics/).

As tags na Adobe Experience Platform são um sistema de gerenciamento de tags projetado para carregar scripts dinamicamente em seu site. O TLS protege a comunicação entre o host do Adobe `assets.adobedtm.com` e seu site quando esses scripts são carregados.

Há várias versões TLS disponíveis e ele oferece suporte a várias cifras diferentes. Nem todas as versões e cifras são as mesmas, pois algumas são consideradas menos ou mais seguras do que outras.

## Versões e cifras TLS compatíveis

A opção de host do Adobe atualmente é compatível com as seguintes versões e cifras TLS:

```
PORT    STATE SERVICE
443/tcp open  https
| ssl-enum-ciphers:
|   TLSv1.2:
|     ciphers:
|       TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384 (secp256r1) - A
|       TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256 (secp256r1) - A
|       TLS_ECDHE_ECDSA_WITH_CHACHA20_POLY1305_SHA256 (secp256r1) - A
|       TLS_ECDHE_RSA_WITH_CHACHA20_POLY1305_SHA256 (secp256r1) - A
|       TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384 (secp256r1) - A
|       TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256 (secp256r1) - A
|     compressors:
|       NULL
|     cipher preference: server
|   TLSv1.3:
|     ciphers:
|       TLS_AKE_WITH_AES_128_GCM_SHA256 (secp256r1) - A
|       TLS_AKE_WITH_AES_256_GCM_SHA384 (secp256r1) - A
|       TLS_AKE_WITH_CHACHA20_POLY1305_SHA256 (secp256r1) - A
|     cipher preference: client
|_  least strength: A
```

### Auto-hospedagem

Se você estiver [hospedando automaticamente](../publishing/hosts/self-hosting-libraries.md) sua biblioteca, as versões TLS com suporte serão determinadas pelo seu próprio serviço de hospedagem.
