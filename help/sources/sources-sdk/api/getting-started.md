---
keywords: Experience Platform;página inicial;tópicos populares;fontes;conectores;conectores de origem;fontes sdk;sdk;SDK
solution: Experience Platform
title: Introdução a Origens de Autoatendimento (SDK em Lote)
description: Este documento fornece uma introdução às informações de pré-requisito que você precisa saber antes de tentar criar uma nova origem usando Origens de Autoatendimento (SDK em Lote).
exl-id: ba131442-ff20-4854-87fe-918aa313382d
source-git-commit: 863889984e5e77770638eb984e129e720b3d4458
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 17%

---

# Introdução a Origens de Autoatendimento (SDK em Lote)

Fontes de autoatendimento (SDK em lote) permitem integrar sua própria origem baseada em REST para trazer dados em lote para a Adobe Experience Platform. Este documento fornece uma introdução aos conceitos principais que você precisa saber antes de tentar fazer chamadas para a [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Pré-requisitos

Para usar Origens de Autoatendimento (SDK em lote), você deve garantir que tenha acesso a uma organização da Sandbox provisionada com Origens da Adobe Experience Platform.

Este guia também requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../home.md): o Experience Platform permite que os dados sejam assimilados de várias fontes e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.
* [Sandboxes](../../../sandboxes/home.md): o Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

## Leitura de chamadas de API de amostra

A documentação das Fontes de Autoatendimento (SDK em Lote) e da API do [!DNL Flow Service] fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e conteúdos de solicitação formatados corretamente. Também fornece exemplos de JSON retornado nas respostas da API. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas de Experience Platform.

## Coletar valores para cabeçalhos necessários

Para fazer chamadas para APIs da Platform, primeiro conclua o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). Concluir o tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API da [!DNL Experience Platform], conforme mostrado abaixo:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Todos os recursos na Platform, incluindo aqueles pertencentes a [!DNL Flow Service], são isolados em sandboxes virtuais específicas. Todas as solicitações para APIs da Platform exigem um cabeçalho que especifique o nome da sandbox em que a operação ocorrerá:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre sandboxes na Platform, consulte a [documentação da sandbox](../../../sandboxes/home.md).

Todas as solicitações que contêm um conteúdo (POST, PUT, PATCH) exigem um cabeçalho adicional:

* `Content-Type: application/json`

## Próximas etapas

Para começar a criar uma nova fonte com Fontes de Autoatendimento (SDK em Lote), consulte o tutorial em [criação de uma nova fonte](./create.md).
