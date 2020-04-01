---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: Guia do desenvolvedor da API Sensei Machine Learning
topic: Developer guide
translation-type: tm+mt
source-git-commit: b0b44f4aaf365f58086cfa17d27fbba6ed2a2a97

---


# Guia do desenvolvedor da API Sensei Machine Learning

A API Sensei Machine Learning fornece um mecanismo para que os cientistas de dados organizem e gerenciem serviços de aprendizado de máquina, desde a integração de algoritmos até a experimentação e a implantação de serviços.

Este guia do desenvolvedor fornece etapas para ajudá-lo a start usando a API [de aprendizado de máquina](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml)Sensei e demonstra chamadas de API para executar operações CRUD em vários recursos da Data Science Workspace.

## Introdução

Você deve ter concluído o tutorial de [autenticação](../../tutorials/authentication.md) para ter acesso aos seguintes cabeçalhos de solicitação para fazer chamadas às APIs da plataforma Adobe Experience:

* Autorização: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos da plataforma Experience são isolados para caixas de proteção virtuais específicas. Todas as solicitações para APIs de plataforma exigem um cabeçalho que especifique o nome da caixa de proteção em que a operação ocorrerá:

* x-sandbox-name: `{SANDBOX_NAME}`

Para obter mais informações sobre caixas de proteção na Plataforma, consulte a documentação [de visão geral da](../../sandboxes/home.md)caixa de proteção.

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