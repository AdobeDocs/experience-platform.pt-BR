---
keywords: Experience Platform, home, tópicos populares, intervalo de datas
solution: Experience Platform
title: Introdução à API do Observability Insights
topic-legacy: developer guide
description: A API da Observability Insights permite recuperar dados de métrica para vários recursos do Adobe Experience Platform. Este documento fornece uma introdução aos conceitos principais que você precisa saber antes de tentar fazer chamadas para a API do Observability Insights .
exl-id: 3b120bd6-155d-467e-b98e-05478f8a4cc5
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---

# Introdução ao [!DNL Observability Insights] API

O [!DNL Observability Insights] A API permite recuperar dados de métrica para vários recursos do Adobe Experience Platform. Este documento fornece uma introdução aos conceitos principais que você precisa saber antes de tentar fazer chamadas para o [!DNL Observability Insights] API.

## Lendo exemplos de chamadas de API

O [!DNL Observability Insights] A documentação da API fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de exemplo retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre como ler chamadas de API de exemplo no [Guia de solução de problemas do Experience Platform](../../landing/troubleshooting.md).

## Cabeçalhos obrigatórios

Para fazer chamadas para [!DNL Platform] As APIs devem ser concluídas primeiro [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todos [!DNL Experience Platform] Chamadas de API, conforme mostrado abaixo:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Todos os recursos em [!DNL Experience Platform] são isoladas em sandboxes virtuais específicas. Todas as solicitações para [!DNL Platform] As APIs exigem um cabeçalho que especifica o nome da sandbox em que a operação ocorrerá. Para obter mais informações sobre sandboxes em [!DNL Platform], consulte o [documentação de visão geral da sandbox](../../sandboxes/home.md).

* `x-sandbox-name: {SANDBOX_NAME}`

## Próximas etapas

Para começar a fazer chamadas usando a variável [!DNL Observability Insights] , continue para a API [guia do endpoint de métricas](./metrics.md).
