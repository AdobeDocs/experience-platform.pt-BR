---
title: Guia da API de higiene de dados
description: Saiba como corrigir ou excluir programaticamente os dados pessoais armazenados dos clientes no Adobe Experience Platform.
exl-id: 78c8b15b-b433-4168-a1e8-c97b96e4bf85
source-git-commit: da8b5d9fffdf8a176a4d70be5df5b3021cf0df7b
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 0%

---

# Guia da API de higiene de dados

>[!IMPORTANT]
>
>Atualmente, os recursos de higiene de dados na Adobe Experience Platform estão disponíveis apenas para organizações que compraram **Adobe Healthcare Shield** ou **Proteção de segurança e privacidade do Adobe**.

A API de higiene de dados permite corrigir ou excluir programaticamente os dados pessoais armazenados dos clientes no Adobe Experience Platform, bem como programar datas de expiração para conjuntos de dados. Este guia aborda as etapas de pré-requisito para usar a API e fornece links para documentações mais específicas do endpoint.

## Introdução

Você pode acessar a API de higiene de dados por meio do seguinte caminho raiz: `https://platform.adobe.io/data/core/hygiene/`

Essas seções abaixo descrevem os conceitos principais que você precisa saber antes de tentar fazer chamadas para a API.

### Coletar valores para cabeçalhos obrigatórios

Para fazer chamadas para a API de higiene de dados, primeiro colete suas credenciais de autenticação. Siga as [Guia de autenticação de API](../../landing/api-authentication.md) para gerar valores para cada um dos cabeçalhos necessários para a API de higiene de dados, conforme mostrado abaixo:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho adicional:

* `Content-Type: application/json`

### Leitura de chamadas de API de amostra

Este documento fornece um exemplo de chamada de API para demonstrar como formatar suas solicitações. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../landing/api-guide.md#sample-api) no guia de introdução às APIs Experience Platform.

## Expirações do conjunto de dados

A expiração de um conjunto de dados é uma ação de &quot;exclusão de um conjunto de dados&quot; atrasada. Ao criar uma expiração de conjunto de dados, você está especificando um momento futuro em que esse conjunto de dados deve ser excluído. Consulte a [guia de ponto de extremidade de expiração do conjunto de dados](./dataset-expiration.md) para obter detalhes sobre como agendar as expirações do conjunto de dados na API.

## Exclusões de registro

>[!IMPORTANT]
>
>As solicitações de exclusão de registro só estão disponíveis para organizações que compraram **Adobe Healthcare Shield**.
>
>
>As exclusões de registros devem ser usadas para limpeza de dados, remoção de dados anônimos ou minimização de dados. Eles são **não** a ser usado para solicitações de direitos do titular dos dados (conformidade) como relacionadas a regulamentos de privacidade, como o Regulamento Geral sobre a Proteção de Dados (GDPR). Para todos os casos de uso de conformidade, use [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) em vez disso.

A API de higiene de dados permite excluir todos os registros associados a uma identidade em um ou todos os conjuntos de dados. Todas as tarefas de higiene de dados que excluem identidades são representadas por uma construção chamada ordem de serviço. Consulte a [guia de ponto de extremidade de ordem de trabalho](./workorder.md) para obter detalhes sobre como trabalhar com exclusões de registros na API.

## Cota

Sua organização está limitada a uma cota de trabalho mensal predeterminada para cada tipo de operação de higiene de dados, que pode variar dependendo do licenciamento. Consulte a [guia de endpoint de cota](./quota.md) para obter detalhes sobre como visualizar o status atual da cota de seus processos de higiene de dados.

## Próximas etapas

Este guia abordou como gerenciar solicitações de higiene de dados usando chamadas de API. Para obter informações sobre como executar essas ações na interface do usuário da Platform, consulte a [guia da interface de higiene de dados](../ui/overview.md).
