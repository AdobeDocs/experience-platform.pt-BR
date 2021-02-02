---
keywords: Experience Platform;home;popular topics;date range
solution: Experience Platform
title: Introdução à API Observability Insights
topic: developer guide
description: A API Observability Insights permite recuperar dados de métricas para vários recursos do Adobe Experience Platform. Este documento fornece uma introdução aos conceitos principais que você precisa saber antes de tentar fazer chamadas para a API do Observability Insights.
translation-type: tm+mt
source-git-commit: ece2ae1eea8426813a95c18096c1b428acfd1a71
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---


# Introdução à API [!DNL Observability Insights]

A API [!DNL Observability Insights] permite recuperar dados de métricas para vários recursos do Adobe Experience Platform. Este documento fornece uma introdução aos conceitos principais que você precisa saber antes de tentar fazer chamadas para a API [!DNL Observability Insights].

## Lendo chamadas de exemplo da API

A documentação da API [!DNL Observability Insights] fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção sobre como ler chamadas de API de exemplo no [guia de solução de problemas do Experience Platform](../../landing/troubleshooting.md).

## Cabeçalhos obrigatórios

Para fazer chamadas para [!DNL Platform] APIs, você deve primeiro concluir o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API [!DNL Experience Platform], como mostrado abaixo:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Todos os recursos em [!DNL Experience Platform] são isolados para caixas de proteção virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifique o nome da caixa de proteção em que a operação ocorrerá. Para obter mais informações sobre caixas de proteção em [!DNL Platform], consulte a [documentação de visão geral da caixa de proteção](../../sandboxes/home.md).

* `x-sandbox-name: {SANDBOX_NAME}`

## Próximas etapas

Para começar a fazer chamadas usando a API [!DNL Observability Insights], prossiga para o [guia de ponto de extremidade de métricas](./metrics.md).