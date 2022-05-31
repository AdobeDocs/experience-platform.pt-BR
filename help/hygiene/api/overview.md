---
title: Guia da API da Higiene de dados
description: Saiba como corrigir ou excluir programaticamente os dados pessoais armazenados de seus clientes no Adobe Experience Platform.
exl-id: 78c8b15b-b433-4168-a1e8-c97b96e4bf85
source-git-commit: 22da9e39e168d9a995c7c134733aa7a1b3587749
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 1%

---

# Guia da API de higiene de dados

>[!IMPORTANT]
>
>Os recursos de higiene de dados no Adobe Experience Platform estão disponíveis apenas para organizações que compraram o Adobe Shield for Healthcare.

A API de higiene de dados permite corrigir ou excluir programaticamente os dados pessoais armazenados de seus clientes no Adobe Experience Platform, bem como agendar protocolos TTL (time-to-live) para conjuntos de dados. Este guia aborda as etapas de pré-requisito para usar a API e fornece links para uma documentação mais específica do ponto de extremidade.

## Introdução

Você pode acessar a API da Higiene de dados por meio do seguinte caminho raiz: `https://platform.adobe.io/data/core/hygiene/`

Essas seções abaixo destacam os conceitos principais que você precisa saber antes de tentar fazer chamadas para a API.

### Coletar valores para cabeçalhos necessários

Para fazer chamadas para a API da Higiene de Dados, primeiro você deve coletar suas credenciais de autenticação. Siga as [Guia de autenticação de API](../../landing/api-authentication.md) para gerar valores para cada um dos cabeçalhos necessários para a API da Higiene de dados, conforme mostrado abaixo:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Todas as solicitações que contêm uma carga útil (POST, PUT, PATCH) exigem um cabeçalho adicional:

* `Content-Type: application/json`

### Lendo exemplos de chamadas de API

Este documento fornece um exemplo de chamada à API para demonstrar como formatar suas solicitações. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler exemplos de chamadas de API](../../landing/api-guide.md#sample-api) no guia de introdução para APIs do Experience Platform.

<!-- ## Work orders

A work order is a representation of a data hygiene task that deletes consumer identities from a specific dataset or all datasets. See the [work order endpoint guide](./workorder.md) for details on working with work orders in the API. -->

## Tempo de vida (TTL) para conjuntos de dados

Um TTL de conjunto de dados é uma ação atrasada &quot;excluir um conjunto de dados&quot;. Ao criar um TTL, você está especificando um horário futuro no qual esse conjunto de dados deve ser excluído. Consulte a [guia do endpoint TTL do conjunto de dados](./ttl.md) para obter detalhes sobre como agendar TTLs de conjuntos de dados na API.

## Próximas etapas

Este guia cobriu como gerenciar solicitações de higiene de dados usando chamadas de API. Para obter informações sobre como executar essas ações na interface do usuário da plataforma, consulte o [guia da interface do usuário de higiene de dados](../ui/overview.md).
