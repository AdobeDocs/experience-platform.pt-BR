---
keywords: Experience Platform;guia do desenvolvedor;endpoint;Data Science Workspace;tópicos populares;data science workspace;data science
solution: Experience Platform
title: Guia da API do Sensei Machine Learning
description: A API do Sensei Machine Learning permite que os desenvolvedores executem operações CRUD em vários recursos do Espaço de trabalho de ciência de dados. Siga este manual para saber como executar operações importantes usando a API.
exl-id: d51d0eb2-b1e9-4cc1-889a-9487395703b0
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 10%

---

# [!DNL Sensei Machine Learning] Manual da API

A variável [!DNL Sensei Machine Learning] A API fornece um mecanismo para que cientistas de dados organizem e gerenciem serviços de aprendizado de máquina, desde a integração de algoritmos até a experimentação e a implantação do serviço.

Este guia do desenvolvedor fornece etapas para ajudar você a começar a usar o [API do Sensei Machine Learning](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml), e demonstra chamadas de API para executar operações CRUD em vários recursos do Espaço de trabalho de ciência de dados.

## Introdução

É necessário que você tenha concluído a [autenticação](https://www.adobe.com/go/platform-api-authentication-en) tutorial para ter acesso aos seguintes cabeçalhos de solicitação para fazer chamadas para [!DNL Adobe Experience Platform] APIs:

* Autorização: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Todos os recursos em [!DNL Experience Platform] são isolados em sandboxes virtuais específicas. Todas as solicitações para [!DNL Platform] As APIs exigem um cabeçalho que especifique o nome da sandbox em que a operação ocorrerá:

* x-sandbox-name: `{SANDBOX_NAME}`

Para obter mais informações sobre sandboxes no [!DNL Platform], consulte o [documentação de visão geral da sandbox](../../sandboxes/home.md).

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho adicional:

* Tipo de conteúdo: application/json

## Próximas etapas

Depois de obter as credenciais de autenticação necessárias, você pode prosseguir para as seções subsequentes deste guia do desenvolvedor para obter exemplos de chamadas de API para os seguintes grupos de endpoints:

* [Mecanismos](./engines.md)
* [Experimentos](./experiments.md)
* [Insights](./insights.md)
* [MLInstances (Receitas)](./mlinstances.md)
* [MLServices](./mlservices.md)
* [Modelos](./models.md)
* [Apêndice](./appendix.md)
