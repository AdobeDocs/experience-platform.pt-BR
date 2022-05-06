---
keywords: Experience Platform, guia do desenvolvedor, endpoint, Data Science Workspace, tópicos populares, data science workspace, ciência de dados
solution: Experience Platform
title: Guia da API do Sensei Machine Learning
topic-legacy: Developer guide
description: A API Sensei Machine Learning permite que os desenvolvedores executem operações CRUD em vários recursos do Data Science Workspace. Siga este manual para saber como executar operações importantes usando a API.
exl-id: d51d0eb2-b1e9-4cc1-889a-9487395703b0
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 9%

---

# [!DNL Sensei Machine Learning] Manual da API

O [!DNL Sensei Machine Learning] A API fornece um mecanismo para os cientistas de dados organizarem e gerenciarem os serviços de aprendizado de máquina, desde a integração de algoritmos à experimentação e à implantação de serviços.

Este guia do desenvolvedor fornece etapas para ajudá-lo a começar a usar o [API de aprendizado de máquina do Sensei](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml)e demonstra as chamadas de API para executar operações CRUD em vários recursos do Data Science Workspace.

## Introdução

É necessário que você tenha completado o [autenticação](https://www.adobe.com/go/platform-api-authentication-en) para ter acesso aos seguintes cabeçalhos de solicitação para fazer chamadas para [!DNL Adobe Experience Platform] APIs:

* Autorização: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Todos os recursos em [!DNL Experience Platform] são isoladas em sandboxes virtuais específicas. Todas as solicitações para [!DNL Platform] As APIs exigem um cabeçalho que especifica o nome da sandbox em que a operação ocorrerá:

* x-sandbox-name: `{SANDBOX_NAME}`

Para obter mais informações sobre sandboxes em [!DNL Platform], consulte o [documentação de visão geral da sandbox](../../sandboxes/home.md).

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
