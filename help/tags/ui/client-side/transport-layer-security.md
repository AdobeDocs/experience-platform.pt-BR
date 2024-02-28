---
title: Informações de Segurança da camada de transporte (TLS)
description: Informações sobre quais versões e cifras TLS são usadas
source-git-commit: 35ee2aca2b92cb8abe1fc69ad6cbc66b0e241e89
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 16%

---

# Informações de Segurança da camada de transporte (TLS)

>[!NOTE]
>
>O Adobe Experience Platform Launch foi reformulado como um conjunto de tecnologias de coleção de dados na Adobe Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Para obter uma referência consolidada das alterações de terminologia, consulte as [atualizações de termos](../../term-updates.md) documento.

O TLS (Transport Layer Security) é um protocolo criptográfico que fornece segurança completa para dados enviados entre aplicativos pela Internet. Para obter informações mais detalhadas sobre TLS, leia a [Noções básicas de TLS](https://www.internetsociety.org/deploy360/tls/basics/) documentação.

As tags na Adobe Experience Platform são um sistema de gerenciamento de tags projetado para carregar scripts dinamicamente em seu site. O TLS protege a comunicação entre o host de Adobe `assets.adobedtm.com` e seu site quando esses scripts forem carregados.

Há várias versões TLS disponíveis e ele oferece suporte a várias cifras diferentes. Nem todas as versões e cifras são as mesmas, pois algumas são consideradas menos ou mais seguras do que outras.

## Versões e cifras TLS compatíveis

A opção de host Adobe atualmente suporta as seguintes versões e cifras TLS:

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

Se você estiver [auto-hospedagem](../publishing/hosts/self-hosting-libraries.md) biblioteca, as versões TLS compatíveis serão determinadas pelo seu próprio serviço de hospedagem.

## Cifras TLS a serem removidas em 1º de maio de 2024

```
PORT    STATE SERVICE
443/tcp open  https
| ssl-enum-ciphers:
|   TLSv1.2:
|     ciphers:
|       TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384 (secp256r1) - A
|       TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256 (secp256r1) - A
|       TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384 (secp256r1) - A
|       TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256 (secp256r1) - A
|       TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA (secp256r1) - A
|       TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA (secp256r1) - A
|       TLS_RSA_WITH_AES_256_GCM_SHA384 (rsa 2048) - A
|       TLS_RSA_WITH_AES_128_GCM_SHA256 (rsa 2048) - A
|       TLS_RSA_WITH_AES_256_CBC_SHA256 (rsa 2048) - A
|       TLS_RSA_WITH_AES_128_CBC_SHA256 (rsa 2048) - A
|       TLS_RSA_WITH_AES_256_CBC_SHA (rsa 2048) - A
|       TLS_RSA_WITH_AES_128_CBC_SHA (rsa 2048) - A
|     compressors:
|       NULL
|     cipher preference: server
|   TLSv1.3:
|     ciphers:
|       TLS_AKE_WITH_AES_128_CCM_8_SHA256 (secp256r1) - A
|       TLS_AKE_WITH_AES_128_CCM_SHA256 (secp256r1) - A
|     cipher preference: client
|_  least strength: A
```
