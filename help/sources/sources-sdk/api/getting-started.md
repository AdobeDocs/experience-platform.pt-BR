---
keywords: Experience Platform;página inicial;tópicos populares;fontes;conectores;conectores de origem;fontes sdk;sdk;SDK
solution: Experience Platform
title: Introdução a fontes de autoatendimento (SDK em lote)
description: Este documento fornece uma introdução às informações de pré-requisito que você precisa saber antes de tentar criar uma nova origem usando Origens de Autoatendimento (SDK em Lote).
exl-id: ba131442-ff20-4854-87fe-918aa313382d
source-git-commit: 2a5d545db18a5dd33c5ff2ac5c543ec35db4ca00
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---

# Introdução a fontes de autoatendimento (SDK em lote)

Fontes de autoatendimento (SDK em lote) permitem integrar sua própria fonte baseada em REST para trazer dados em lote para a Adobe Experience Platform. Este documento fornece uma introdução aos conceitos principais que você precisa saber antes de tentar fazer chamadas para o [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Pré-requisitos

Para usar o Self-Serve Sources (Batch SDK), você deve garantir que tenha acesso a uma organização Sandbox provisionada com o Adobe Experience Platform Sources.

Este guia também requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Origens](../../home.md): o Experience Platform permite que os dados sejam assimilados de várias fontes e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.
* [Sandboxes](../../../sandboxes/home.md): o Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

## Leitura de chamadas de API de amostra

As Fontes de autoatendimento (SDK em lote) e [!DNL Flow Service] A documentação da API fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O exemplo de JSON retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas de Experience Platform.

## Coletar valores para cabeçalhos obrigatórios

Para fazer chamadas para APIs da Platform, primeiro conclua o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). Concluir o tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todos os [!DNL Experience Platform] Chamadas de API, conforme mostrado abaixo:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Todos os recursos na Platform, incluindo os que pertencem a [!DNL Flow Service], são isolados em sandboxes virtuais específicas. Todas as solicitações para APIs da Platform exigem um cabeçalho que especifique o nome da sandbox em que a operação ocorrerá:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre sandboxes na Platform, consulte a [documentação da sandbox](../../../sandboxes/home.md).

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho adicional:

* `Content-Type: application/json`

## Próximas etapas

Para começar a criar uma nova fonte com Fontes de autoatendimento (SDK em lote), consulte o tutorial em [criação de uma nova fonte](./create.md).
