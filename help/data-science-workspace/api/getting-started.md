---
keywords: Experience Platform;guia do desenvolvedor;endpoint;Data Science Workspace;popular topics;data science workspace;data science
solution: Experience Platform
title: Guia do desenvolvedor da API Sensei Machine Learning
topic: Developer guide
description: Este guia do desenvolvedor fornece etapas para ajudá-lo a start usando a API Sensei Machine Learning e demonstra chamadas de API para executar operações CRUD em vários recursos da Data Science Workspace.
translation-type: tm+mt
source-git-commit: ece2ae1eea8426813a95c18096c1b428acfd1a71
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 2%

---


# [!DNL Sensei Machine Learning] Guia do desenvolvedor da API

A API [!DNL Sensei Machine Learning] fornece um mecanismo para que os cientistas de dados organizem e gerenciem serviços de aprendizado de máquina, desde a integração de algoritmos por experimentação e implantação de serviços.

Este guia do desenvolvedor fornece etapas para ajudá-lo a start usando a [API de aprendizado de máquina do Sensei](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) e demonstra chamadas de API para executar operações CRUD em vários recursos da Data Science Workspace.

## Introdução

Você deve ter concluído o tutorial [authentication](https://www.adobe.com/go/platform-api-authentication-en) para ter acesso aos seguintes cabeçalhos de solicitação para fazer chamadas para [!DNL Adobe Experience Platform] APIs:

* Autorização: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos em [!DNL Experience Platform] são isolados para caixas de proteção virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifique o nome da caixa de proteção em que a operação ocorrerá:

* x-sandbox-name: `{SANDBOX_NAME}`

Para obter mais informações sobre caixas de proteção em [!DNL Platform], consulte a [documentação de visão geral da caixa de proteção](../../sandboxes/home.md).

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho adicional:

* Tipo de conteúdo: application/json

## Próximas etapas

Depois de coletar as credenciais de autenticação necessárias, você pode continuar com as seções subsequentes deste guia do desenvolvedor para obter exemplos de chamadas de API para os seguintes grupos de pontos finais:

* [Motores](./engines.md)
* [Experimentos](./experiments.md)
* [Insights](./insights.md)
* [MLInentons (Receitas)](./mlinstances.md)
* [MLServices](./mlservices.md)
* [Modelos](./models.md)
* [Apêndice](./appendix.md)