---
title: Guia da API do MTLS
description: Saiba como usar a API de serviço mTLS para recuperar e verificar com segurança os certificados públicos emitidos pelo Adobe.
role: Developer
source-git-commit: f805d03ff2cd3a4f84ca8068023d83986f8bdfbb
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 1%

---

# Visão geral da API de serviço do MTLS

Use a API de Serviço MTLS para recuperar com segurança os certificados públicos emitidos pelo Adobe para os aplicativos de sua organização. Essa API garante que as trocas de dados entre seus clientes e a Adobe Experience Platform sejam autenticadas e criptografadas, fornecendo uma camada adicional de segurança. Ao verificar externamente a autenticidade dos certificados, você pode aprimorar a confiança e proteger informações confidenciais.

## Certificado público

Um certificado público é um documento digital usado para autenticar a identidade de um servidor ou cliente em comunicações seguras. No contexto da API de serviço mTLS, esses certificados garantem que as trocas de dados com o Adobe Experience Platform sejam autenticadas e criptografadas. A recuperação e a verificação desses certificados por meio da API confirmam sua autenticidade, melhorando a segurança e a confiabilidade das transações de dados e protegendo informações confidenciais. Para saber como recuperar seu certificado público, consulte o [manual do endpoint](./public-certificate-endpoint.md) para saber como fazer chamadas.

## Próximas etapas

Para começar a fazer chamadas usando a API de Serviço MTLS, leia o [guia de introdução](./getting-started.md) para obter informações importantes sobre cabeçalhos necessários, como ler chamadas de API de exemplo e muito mais.
