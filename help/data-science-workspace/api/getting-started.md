---
keywords: Experience Platform, guia do desenvolvedor, endpoint, Data Science Workspace, tópicos populares, data science workspace, ciência de dados
solution: Experience Platform
title: Guia da API de aprendizado de máquina do Sensei
topic-legacy: Developer guide
description: A API Sensei Machine Learning permite que desenvolvedores executem operações CRUD em vários recursos do Data Science Workspace. Siga este guia para saber como executar operações principais usando a API.
exl-id: d51d0eb2-b1e9-4cc1-889a-9487395703b0
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 2%

---

# [!DNL Sensei Machine Learning] Guia da API

A API [!DNL Sensei Machine Learning] fornece um mecanismo para que os cientistas de dados organizem e gerenciem serviços de aprendizado de máquina, desde a integração de algoritmos à experimentação e à implantação de serviços.

Este guia do desenvolvedor fornece etapas para ajudá-lo a começar a usar a [API de aprendizado de máquina do Sensei](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml), e demonstra chamadas de API para executar operações CRUD em vários recursos do Data Science Workspace.

## Introdução

Você deve ter concluído o tutorial [authentication](https://www.adobe.com/go/platform-api-authentication-en) para ter acesso aos seguintes cabeçalhos de solicitação para fazer chamadas para APIs [!DNL Adobe Experience Platform]:

* Autorização: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos em [!DNL Experience Platform] são isolados para sandboxes virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifica o nome da sandbox em que a operação ocorrerá:

* x-sandbox-name: `{SANDBOX_NAME}`

Para obter mais informações sobre sandboxes em [!DNL Platform], consulte a [documentação de visão geral da sandbox](../../sandboxes/home.md).

Todas as solicitações que contêm uma carga útil (POST, PUT, PATCH) exigem um cabeçalho adicional:

* Tipo de conteúdo: application/json

## Próximas etapas

Depois de coletar as credenciais de autenticação necessárias, você pode prosseguir para as seções subsequentes deste guia do desenvolvedor para obter exemplos de chamadas de API para os seguintes grupos de pontos finais:

* [Motores](./engines.md)
* [Experimentos](./experiments.md)
* [Insights](./insights.md)
* [MLIntent (Receitas)](./mlinstances.md)
* [MLServices](./mlservices.md)
* [Modelos](./models.md)
* [Apêndice](./appendix.md)
