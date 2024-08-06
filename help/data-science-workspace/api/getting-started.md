---
keywords: Experience Platform; guia do desenvolvedor; Extremidade; Área de trabalho de ciência de dados; tópicos populares; espaço de trabalho de ciência de dados; ciência de dados
solution: Experience Platform
title: Guia da API de aprendizado de máquina do Sensei
description: A API de aprendizagem de máquina do Sensei permite que os desenvolvedores realizem operações de CRUD em vários recursos de Área de trabalho de Ciência de Dados. Siga este manual para saber como executar operações importantes usando a API.
role: Developer
exl-id: d51d0eb2-b1e9-4cc1-889a-9487395703b0
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 13%

---

# [!DNL Sensei Machine Learning] Manual da API

>[!NOTE]
>
>O Área de trabalho de ciência de dados não está mais disponível para compra.
>
>Esta documentação destina-se a clientes existentes com direitos anteriores à Data Science Área de trabalho.

A [!DNL Sensei Machine Learning] API fornece um mecanismo para que os cientistas de dados organizem e gerenciar serviços de aprendizagem de máquina, desde algoritmos integrados por experimentação e até o serviço de implantação.

Este guia do desenvolvedor fornece etapas para ajudá-lo a start usando a API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) de aprendizagem de máquina do [Sensei e demonstra as chamadas de API para executar operações de CRUD em vários recursos do Data Science Área de trabalho.

## Introdução

É necessário ter concluído a [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en) no solicitar ter acesso aos seguintes cabeçalhos solicitação para fazer chamadas para [!DNL Adobe Experience Platform] APIs:

* Autorização: Portador `{ACCESS_TOKEN}`
* chave de x-api: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Todos os recursos são isolados em [!DNL Experience Platform] áreas virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifique o nome da sandbox em que a operação ocorrerá:

* x-sandbox-name: `{SANDBOX_NAME}`

Para obter mais informações sobre sandboxes in[!DNL Platform], consulte a documentação](../../sandboxes/home.md) de visão geral da [área de segurança.

Todas as solicitações que contêm um conteúdo (POST, PUT, PATCH) exigem um cabeçalho adicional:

* Content-Type: aplicativo/json

## Próximas etapas

Depois de reunir as credenciais de autenticação necessárias, você pode prosseguir para as seções subsequentes deste guia do desenvolvedor para chamadas de API de amostra para os seguintes grupos de endpoint:

* [Motores](./engines.md)
* [Experimentos](./experiments.md)
* [Insights](./insights.md)
* [MLInstances (Receitas)](./mlinstances.md)
* [MLServices](./mlservices.md)
* [Modelos](./models.md)
* [Apêndice](./appendix.md)
