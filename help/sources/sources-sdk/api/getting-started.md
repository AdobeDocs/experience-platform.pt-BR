---
keywords: Experience Platform, home, tópicos populares, fontes, conectores, conectores de origem, sdk de fontes, sdk, SDK
solution: Experience Platform
title: Introdução às fontes de autoatendimento (SDK em lote)
topic-legacy: developer guide
description: Este documento fornece uma introdução às informações de pré-requisito que você precisa saber antes de tentar criar uma nova fonte usando Fontes de autoatendimento (SDK em lote).
exl-id: ba131442-ff20-4854-87fe-918aa313382d
source-git-commit: 4d7799b01c34f4b9e4a33c130583eadcfdc3af69
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 0%

---

# Introdução às fontes de autoatendimento (SDK em lote)

Fontes de autoatendimento (SDK em lote) permitem integrar sua própria fonte baseada em REST para trazer dados em lote para o Adobe Experience Platform. Este documento fornece uma introdução aos conceitos principais que você precisa saber antes de tentar fazer chamadas para o [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Pré-requisitos

Para usar as Fontes de autoatendimento (SDK em lote), você deve garantir que tenha acesso a uma Caixa de proteção da Organização IMS provisionada com as Fontes da Adobe Experience Platform.

Este guia também requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../home.md): O Experience Platform permite que os dados sejam assimilados de várias fontes, fornecendo a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.
* [Sandboxes](../../../sandboxes/home.md): O Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

## Lendo exemplos de chamadas de API

As fontes de autoatendimento (SDK em lote) e [!DNL Flow Service] A documentação da API fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de exemplo retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler exemplos de chamadas de API](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas do Experience Platform.

## Coletar valores para cabeçalhos necessários

Para fazer chamadas para APIs da plataforma, primeiro conclua o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todos [!DNL Experience Platform] Chamadas de API, conforme mostrado abaixo:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Todos os recursos na Platform, incluindo aqueles pertencentes a [!DNL Flow Service], são isoladas em sandboxes virtuais específicas. Todas as solicitações para APIs da plataforma exigem um cabeçalho que especifica o nome da sandbox em que a operação ocorrerá:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre sandboxes na Platform, consulte o [documentação da sandbox](../../../sandboxes/home.md).

Todas as solicitações que contêm uma carga útil (POST, PUT, PATCH) exigem um cabeçalho adicional:

* `Content-Type: application/json`

## Próximas etapas

Para começar a criar uma nova fonte com Fontes de autoatendimento (SDK em lote), consulte o tutorial em [criação de uma nova fonte](./create.md).
