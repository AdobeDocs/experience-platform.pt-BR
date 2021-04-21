---
keywords: Experience Platform, home, tópicos populares, intervalo de datas
solution: Experience Platform
title: Introdução à API do Observability Insights
topic-legacy: developer guide
description: A API da Observability Insights permite recuperar dados de métrica para vários recursos do Adobe Experience Platform. Este documento fornece uma introdução aos conceitos principais que você precisa saber antes de tentar fazer chamadas para a API do Observability Insights .
exl-id: 3b120bd6-155d-467e-b98e-05478f8a4cc5
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---

# Introdução à API [!DNL Observability Insights]

A API [!DNL Observability Insights] permite recuperar dados de métrica para vários recursos do Adobe Experience Platform. Este documento fornece uma introdução aos conceitos principais que você precisa saber antes de tentar fazer chamadas para a API [!DNL Observability Insights].

## Lendo exemplos de chamadas de API

A documentação da API [!DNL Observability Insights] fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de exemplo retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre como ler chamadas de API de exemplo no [Guia de solução de problemas do Experience Platform](../../landing/troubleshooting.md).

## Cabeçalhos obrigatórios

Para fazer chamadas para [!DNL Platform] APIs, primeiro complete o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API [!DNL Experience Platform], conforme mostrado abaixo:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Todos os recursos em [!DNL Experience Platform] são isolados para sandboxes virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifica o nome da sandbox em que a operação ocorrerá. Para obter mais informações sobre sandboxes em [!DNL Platform], consulte a [documentação de visão geral da sandbox](../../sandboxes/home.md).

* `x-sandbox-name: {SANDBOX_NAME}`

## Próximas etapas

Para começar a fazer chamadas usando a API [!DNL Observability Insights], continue com o [guia do endpoint de métricas](./metrics.md).
