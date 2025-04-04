---
keywords: Experience Platform;página inicial;tópicos populares;intervalo de datas
solution: Experience Platform
title: Introdução à API dos Insights de observação
description: A API de Insights de capacidade de observação permite recuperar dados de métricas para vários recursos do Adobe Experience Platform. Este documento fornece uma introdução aos conceitos principais que você precisa saber antes de tentar fazer chamadas para a API dos Insights de observação.
exl-id: 3b120bd6-155d-467e-b98e-05478f8a4cc5
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 18%

---

# Introdução à API [!DNL Observability Insights]

A API [!DNL Observability Insights] permite recuperar dados de métrica para vários recursos do Adobe Experience Platform. Este documento fornece uma introdução aos conceitos principais que você precisa saber antes de tentar fazer chamadas para a API [!DNL Observability Insights].

## Leitura de chamadas de API de amostra

A documentação da API [!DNL Observability Insights] fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e conteúdos de solicitação formatados corretamente. Também fornece exemplos de JSON retornado nas respostas da API. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre como ler chamadas de API de exemplo no [guia de solução de problemas do Experience Platform](../../landing/troubleshooting.md).

## Cabeçalhos obrigatórios

Para fazer chamadas para APIs do [!DNL Experience Platform], primeiro complete o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). Concluir o tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API da [!DNL Experience Platform], conforme mostrado abaixo:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Todos os recursos em [!DNL Experience Platform] estão isolados em sandboxes virtuais específicas. Todas as solicitações para [!DNL Experience Platform] APIs exigem um cabeçalho que especifique o nome da sandbox em que a operação ocorrerá. Para obter mais informações sobre sandboxes em [!DNL Experience Platform], consulte a [documentação de visão geral da sandbox](../../sandboxes/home.md).

* `x-sandbox-name: {SANDBOX_NAME}`

## Próximas etapas

Para começar a fazer chamadas usando a API [!DNL Observability Insights], prossiga para o [manual de ponto de extremidade de métricas](./metrics.md).
