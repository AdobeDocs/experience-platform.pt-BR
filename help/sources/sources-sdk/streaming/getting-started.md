---
title: Introdução a fontes de autoatendimento (SDK de transmissão)
description: Este documento fornece uma introdução às informações de pré-requisito que você precisa saber antes de tentar criar uma nova fonte usando Fontes de autoatendimento (SDK de transmissão).
exl-id: 6cc13279-ce0b-45bc-ad25-e2e6aafc2af0
badge: Beta
source-git-commit: 256857103b4037b2cd7b5b52d6c5385121af5a9f
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 12%

---

# Introdução a fontes de autoatendimento (SDK de transmissão)

>[!NOTE]
>
>O SDK de transmissão de fontes de autoatendimento está na versão beta. Leia a [visão geral das fontes](../../home.md#terms-and-conditions) para obter mais informações sobre o uso de fontes com rótulo beta.

Fontes de autoatendimento (SDK de transmissão) permitem integrar sua própria fonte para trazer dados de transmissão para a Adobe Experience Platform. Este documento fornece uma introdução aos conceitos principais que você precisa saber antes de tentar fazer chamadas para a [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Processo de alto nível

O processo passo a passo para configurar sua origem no Experience Platform é descrito abaixo:

### Integração

* [Crie uma nova especificação de conexão para o SDK de Streaming](create.md).
* [Atualize a especificação de fluxo de streaming com a nova ID de especificação de conexão](update-flow-specs.md).
* [Testar e enviar sua fonte de streaming](submit.md).

### Documentação

* Para começar a documentar sua origem, leia a [visão geral sobre como criar documentação para Fontes de Autoatendimento](../documentation/doc-overview.md).
* Leia o guia em [usando a interface da Web do GitHub](../documentation/github.md) para obter etapas sobre como criar a documentação usando o GitHub.
* Leia o guia em [usando um editor de texto](../documentation/text-editor.md) para obter as etapas sobre como criar a documentação usando o computador local.
* [Use o modelo de documentação da API do SDK de Streaming para documentar sua origem na API](streaming-template-api.md).
* [Use o modelo de documentação da interface do SDK de Streaming para documentar sua origem na interface](streaming-template-ui.md).

Você também pode baixar os modelos de documentação abaixo:

* [Modelo da documentação da API](../assets/streaming/streaming-template-api.zip)
* [Modelo de documentação da interface do usuário](../assets/streaming/streaming-template-ui.zip)

## Pré-requisitos

>[!IMPORTANT]
>
>A fonte que você está integrando com o Experience Platform deve ser capaz de suportar um webhook no qual um endpoint pode ser inscrito para enviar atualizações.

Para usar as Fontes de autoatendimento (SDK de transmissão), você deve garantir que tenha acesso a uma organização de sandbox provisionada com o Adobe Experience Platform Sources.

Este guia também requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../home.md): o Experience Platform permite que os dados sejam assimilados de várias fontes e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.
* [Sandboxes](../../../sandboxes/home.md): o Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

## Leitura de chamadas de API de amostra

A documentação das Fontes de Autoatendimento (SDK de Streaming) e da API do [!DNL Flow Service] fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e conteúdos de solicitação formatados corretamente. Também fornece exemplos de JSON retornado nas respostas da API. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas de Experience Platform.

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

Para começar a criar uma nova fonte com Fontes de Autoatendimento (SDK de Transmissão), consulte o tutorial em [criação de uma nova fonte](./create.md).
