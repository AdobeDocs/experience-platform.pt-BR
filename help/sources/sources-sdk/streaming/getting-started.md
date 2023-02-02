---
title: Introdução às fontes de autoatendimento (SDK de streaming)
description: Este documento fornece uma introdução às informações de pré-requisito que você precisa saber antes de tentar criar uma nova fonte usando Fontes de autoatendimento (SDK de streaming).
hide: true
hidefromtoc: true
source-git-commit: 7744fef9751212a40f8f20df52812d38130c42fc
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---

# Introdução às fontes de autoatendimento (SDK de streaming)

Fontes de autoatendimento (SDK de streaming) permitem integrar sua própria fonte para trazer dados de streaming para a Adobe Experience Platform. Este documento fornece uma introdução aos conceitos principais que você precisa saber antes de tentar fazer chamadas para o [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Processo de alto nível

O processo passo a passo para configurar sua fonte no Experience Platform é descrito abaixo:

### Integração

* [Criar uma nova especificação de conexão para o SDK de streaming](create.md).
* [Atualize a especificação do fluxo de transmissão com sua nova ID de especificação de conexão](update-flow-specs.md).
* [Teste e envie sua fonte de transmissão](submit.md).

### Documentação

* Para começar a documentar sua fonte, leia o [visão geral sobre como criar documentação para fontes de autoatendimento](../documentation/doc-overview.md).
* Leia o guia em [uso da interface da Web do GitHub](../documentation/github.md) para obter as etapas sobre como criar a documentação usando o GitHub.
* Leia o guia em [uso de um editor de texto](../documentation/text-editor.md) para obter etapas sobre como criar a documentação usando o computador local.
* [Use o modelo de documentação da API do SDK de transmissão para documentar sua fonte na API](streaming-template-api.md).
* [Use o modelo de documentação da interface do usuário do SDK de streaming para documentar sua fonte na interface do usuário](streaming-template-ui.md).

Você também pode baixar os modelos de documentação abaixo:

* [Modelo de documentação da API](../assets/streaming/streaming-template-api.zip)
* [Modelo de documentação da interface do usuário](../assets/streaming/streaming-template-ui.zip)

## Pré-requisitos

>[!IMPORTANT]
>
>A fonte que você está integrando com o Experience Platform deve ser capaz de suportar um webhook no qual um endpoint pode ser inscrito para enviar atualizações.

Para usar as Fontes de autoatendimento (SDK de streaming), é necessário garantir que você tenha acesso a uma organização de sandbox provisionada com as Fontes Adobe Experience Platform.

Este guia também requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../home.md): O Experience Platform permite que os dados sejam assimilados de várias fontes, fornecendo a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.
* [Sandboxes](../../../sandboxes/home.md): O Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

## Lendo exemplos de chamadas de API

As fontes de autoatendimento (SDK de streaming) e [!DNL Flow Service] A documentação da API fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de exemplo retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler exemplos de chamadas de API](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas do Experience Platform.

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

Para começar a criar uma nova fonte com Fontes de autoatendimento (SDK de streaming), consulte o tutorial em [criação de uma nova fonte](./create.md).
