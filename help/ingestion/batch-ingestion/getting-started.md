---
keywords: Experience Platform, perfil, perfil do cliente em tempo real, solução de problemas, API
title: Introdução à API de assimilação de dados
type: Documentation
description: The Data Ingestion API getting started guide outlines the key concepts and basic functionality that you need to know before you can begin to ingest data into Experience Platform using APIs.
exl-id: 0653de2b-3268-478b-a23f-c458b6d3df7c
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%

---

# Introdução à API de assimilação de dados {#getting-started}

Usando pontos de extremidade da API de assimilação de dados, é possível executar operações básicas de CRUD para assimilar dados no Adobe Experience Platform.

O uso dos guias da API requer uma compreensão funcional de vários serviços da Adobe Experience Platform envolvidos no trabalho com dados. Before using the Data Ingestion API, please review the documentation for the following services:

* [Batch ingestion](./overview.md): Allows you to ingest data into Adobe Experience Platform as batch files.
* [[!DNL Real-time Customer Profile]](../home.md): Fornece um perfil de cliente unificado em tempo real com base em dados agregados de várias fontes.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): A estrutura padronizada pela qual a Platform organiza os dados de experiência do cliente.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para fazer chamadas para o [!DNL Profile] Pontos de extremidade da API.

## Lendo exemplos de chamadas de API

A documentação da API de assimilação de dados fornece exemplos de chamadas de API para demonstrar como formatar corretamente as solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de exemplo retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler exemplos de chamadas de API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no [!DNL Experience Platform] guia de solução de problemas.

## Cabeçalhos obrigatórios

A documentação da API também requer que você tenha completado o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en) para fazer chamadas para [!DNL Platform] endpoints. Completing the authentication tutorial provides the values for each of the required headers in [!DNL Experience Platform] API calls, as shown below:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

All requests with a payload in the request body (such as POST, PUT, and PATCH calls) must include a `Content-Type` header. Accepted values specific to each call are provided in the call parameters.

All resources in [!DNL Experience Platform] are isolated to specific virtual sandboxes. Solicitações para [!DNL Platform] As APIs exigem um cabeçalho que especifica o nome da sandbox em que a operação ocorrerá:

* `x-sandbox-name: {SANDBOX_NAME}`

Para obter mais informações sobre sandboxes em [!DNL Platform], consulte o [documentação de visão geral da sandbox](../../sandboxes/home.md).
