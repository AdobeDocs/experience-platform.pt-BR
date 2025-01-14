---
keywords: Experience Platform;guia do desenvolvedor;endpoint;Data Science Workspace;tópicos populares;espaço de trabalho de ciência de dados;ciência de dados
solution: Experience Platform
title: Guia da API do Sensei Machine Learning
description: A API do Sensei Machine Learning permite que os desenvolvedores executem operações CRUD em vários recursos do Data Science Workspace. Siga este manual para saber como executar operações importantes usando a API.
role: Developer
exl-id: d51d0eb2-b1e9-4cc1-889a-9487395703b0
source-git-commit: 863889984e5e77770638eb984e129e720b3d4458
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 13%

---

# [!DNL Sensei Machine Learning] Manual da API

>[!NOTE]
>
>O Data Science Workspace não está mais disponível para compra.
>
>Esta documentação destina-se aos clientes existentes com direitos anteriores ao Data Science Workspace.

A API [!DNL Sensei Machine Learning] fornece um mecanismo para cientistas de dados organizarem e gerenciarem serviços de aprendizado de máquina, desde a integração de algoritmos até a experimentação e a implantação do serviço.

Este guia do desenvolvedor fornece etapas para ajudar você a começar a usar a [API do Sensei Machine Learning](https://developer.adobe.com/experience-platform-apis/references/sensei-machine-learning/) e demonstra chamadas de API para executar operações CRUD em vários recursos do Data Science Workspace.

## Introdução

Você precisa concluir o tutorial de [autenticação](https://www.adobe.com/go/platform-api-authentication-en) para ter acesso aos seguintes cabeçalhos de solicitação para fazer chamadas para APIs [!DNL Adobe Experience Platform]:

* Autorização: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id `{ORG_ID}`

Todos os recursos em [!DNL Experience Platform] estão isolados em sandboxes virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifique o nome da sandbox em que a operação ocorrerá:

* x-sandbox-name: `{SANDBOX_NAME}`

Para obter mais informações sobre sandboxes em [!DNL Platform], consulte a [documentação de visão geral da sandbox](../../sandboxes/home.md).

Todas as solicitações que contêm um conteúdo (POST, PUT, PATCH) exigem um cabeçalho adicional:

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
