---
title: Guia da API de higiene de dados
description: Saiba como corrigir ou excluir programaticamente os dados pessoais armazenados dos clientes no Adobe Experience Platform.
role: Developer
exl-id: 78c8b15b-b433-4168-a1e8-c97b96e4bf85
source-git-commit: 8aa8a1c42e9656716be746ba447a5f77a8155b4c
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 6%

---

# Guia da API de higiene de dados

A API de higiene de dados permite corrigir ou excluir programaticamente os dados pessoais armazenados dos clientes no Adobe Experience Platform, bem como programar datas de expiração para conjuntos de dados. Este guia aborda as etapas de pré-requisito para usar a API e fornece links para documentações mais específicas do endpoint.

## Introdução

Você pode acessar a API de Limpeza de Dados pelo seguinte caminho raiz: `https://platform.adobe.io/data/core/hygiene/`

Essas seções abaixo descrevem os conceitos principais que você precisa saber antes de tentar fazer chamadas para a API.

### Coletar valores para cabeçalhos obrigatórios

Para fazer chamadas para a API de higiene de dados, primeiro colete suas credenciais de autenticação. Siga o [guia de autenticação de API](../../landing/api-authentication.md) para gerar valores para cada um dos cabeçalhos necessários para a API de Limpeza de Dados, conforme mostrado abaixo:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Todas as solicitações que contêm um conteúdo (POST, PUT, PATCH) exigem um cabeçalho adicional:

* `Content-Type: application/json`

### Leitura de chamadas de API de amostra

Este documento fornece um exemplo de chamada de API para demonstrar como formatar suas solicitações. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../landing/api-guide.md#sample-api) no guia de introdução para APIs do Experience Platform.

## Expirações de conjuntos de dados

A expiração de um conjunto de dados é uma ação de &quot;exclusão de um conjunto de dados&quot; atrasada. Ao criar uma expiração de conjunto de dados, você está especificando um momento futuro em que esse conjunto de dados deve ser excluído. Consulte o [guia de ponto de extremidade de expiração do conjunto de dados](./dataset-expiration.md) para obter detalhes sobre o agendamento de expirações do conjunto de dados na API.

## Exclusões de registro

>[!IMPORTANT]
>
>As exclusões de registros devem ser usadas para limpeza de dados, remoção de dados anônimos ou minimização de dados. Eles **não** devem ser usados para solicitações de direitos do titular dos dados (conformidade) relacionadas a regulamentos de privacidade, como o Regulamento Geral sobre a Proteção de Dados (GDPR). Para todos os casos de uso de conformidade, use o [Adobe Experience Platform Privacy Service](../../privacy-service/home.md).

A API de higiene de dados permite excluir todos os registros associados a uma identidade em um ou todos os conjuntos de dados. Todas as tarefas do ciclo de vida de dados que excluem identidades são representadas por uma construção chamada ordem de serviço. Consulte o [manual de ponto de extremidade de ordem de trabalho](./workorder.md) para obter detalhes sobre como trabalhar com exclusões de registros na API.

## Cota

Sua organização está limitada a uma cota de trabalho mensal predeterminada para cada tipo de operação do ciclo de vida dos dados, que pode variar dependendo do licenciamento. Consulte o [manual de ponto de extremidade de cota](./quota.md) para obter detalhes sobre como visualizar o status atual da cota de seus processos do ciclo de vida dos dados.

## Próximas etapas

Este guia abordou como gerenciar solicitações de ciclo de vida de dados usando chamadas de API. Para obter informações sobre como executar essas ações na interface do usuário do Experience Platform, consulte o [guia da interface do usuário do ciclo de vida dos dados](../ui/overview.md).
