---
title: Guia da API da Higiene de dados
description: Saiba como corrigir ou excluir programaticamente os dados pessoais armazenados de seus clientes no Adobe Experience Platform.
exl-id: 78c8b15b-b433-4168-a1e8-c97b96e4bf85
source-git-commit: e4cc78591d0d3b4abd660956b1263092697d63d5
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 0%

---

# Guia da API de higiene de dados

>[!IMPORTANT]
>
>Os recursos de higiene de dados no Adobe Experience Platform estão disponíveis apenas para organizações que compraram o Adobe Healthcare Shield ou o Privacy Shield.

A API de higiene de dados permite corrigir ou excluir programaticamente os dados pessoais armazenados de seus clientes no Adobe Experience Platform, bem como programar datas de expiração para os conjuntos de dados. Este guia aborda as etapas de pré-requisito para usar a API e fornece links para uma documentação mais específica do ponto de extremidade.

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

## Expirações do conjunto de dados

A expiração de um conjunto de dados é uma ação &quot;excluir um conjunto de dados&quot; atrasada. Ao criar uma expiração de conjunto de dados, você está especificando uma hora futura na qual esse conjunto de dados deve ser excluído. Consulte a [guia do endpoint de expiração de conjunto de dados](./dataset-expiration.md) para obter detalhes sobre como agendar expirações do conjunto de dados na API.

## Exclusão do consumidor

A API de Higiene de dados permite excluir todos os registros associados a uma identidade do consumidor em um ou todos os conjuntos de dados. Todas as tarefas de higiene de dados que excluem identidades de consumidores são representadas por uma construção chamada ordem de trabalho. Consulte a [guia do endpoint de ordem de trabalho](./workorder.md) para obter detalhes sobre como trabalhar com exclusões do consumidor na API.

## Quota

Sua organização está limitada a uma cota de trabalho mensal predeterminada para cada tipo de operação de higiene de dados, que pode variar dependendo do licenciamento. Consulte a [guia de endpoint de cota](./quota.md) para obter detalhes sobre como visualizar o status atual da cota de seus processos de higiene de dados.

## Próximas etapas

Este guia cobriu como gerenciar solicitações de higiene de dados usando chamadas de API. Para obter informações sobre como executar essas ações na interface do usuário da plataforma, consulte o [guia da interface do usuário de higiene de dados](../ui/overview.md).
