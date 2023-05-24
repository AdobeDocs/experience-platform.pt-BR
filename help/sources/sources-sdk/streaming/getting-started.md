---
title: Introdução a fontes de autoatendimento (SDK de transmissão)
description: Este documento fornece uma introdução às informações de pré-requisito que você precisa saber antes de tentar criar uma nova fonte usando Fontes de autoatendimento (SDK de transmissão).
hide: true
hidefromtoc: true
exl-id: 6cc13279-ce0b-45bc-ad25-e2e6aafc2af0
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---

# Introdução a fontes de autoatendimento (SDK de transmissão)

Fontes de autoatendimento (SDK de transmissão) permitem integrar sua própria fonte para trazer dados de transmissão para a Adobe Experience Platform. Este documento fornece uma introdução aos conceitos principais que você precisa saber antes de tentar fazer chamadas para o [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Processo de alto nível

O processo passo a passo para configurar sua origem no Experience Platform é descrito abaixo:

### Integração

* [Criar uma nova especificação de conexão para o SDK de transmissão](create.md).
* [Atualize a especificação do fluxo de transmissão com a nova ID de especificação de conexão](update-flow-specs.md).
* [Testar e enviar sua fonte de streaming](submit.md).

### Documentação

* Para começar a documentar sua origem, leia o [visão geral sobre a criação de documentação para Fontes de autoatendimento](../documentation/doc-overview.md).
* Leia o guia em [usar a interface da Web do GitHub](../documentation/github.md) para obter etapas sobre como criar a documentação usando o GitHub.
* Leia o guia em [uso de um editor de texto](../documentation/text-editor.md) para obter etapas sobre como criar a documentação usando o computador local.
* [Use o modelo de documentação da API do SDK de streaming para documentar sua fonte na API](streaming-template-api.md).
* [Use o modelo de documentação da interface do SDK de transmissão para documentar sua origem na interface](streaming-template-ui.md).

Você também pode baixar os modelos de documentação abaixo:

* [Modelo da documentação da API](../assets/streaming/streaming-template-api.zip)
* [Modelo de documentação da interface do usuário](../assets/streaming/streaming-template-ui.zip)

## Pré-requisitos

>[!IMPORTANT]
>
>A fonte que você está integrando com o Experience Platform deve ser capaz de suportar um webhook no qual um endpoint pode ser inscrito para enviar atualizações.

Para usar as Fontes de autoatendimento (SDK de transmissão), você deve garantir que tenha acesso a uma organização de sandbox provisionada com o Adobe Experience Platform Sources.

Este guia também requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Origens](../../home.md): o Experience Platform permite que os dados sejam assimilados de várias fontes e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.
* [Sandboxes](../../../sandboxes/home.md): o Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

## Leitura de chamadas de API de amostra

As Fontes de autoatendimento (SDK de transmissão) e [!DNL Flow Service] A documentação da API fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O exemplo de JSON retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas de Experience Platform.

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

Para começar a criar uma nova fonte com fontes de autoatendimento (SDK de transmissão), consulte o tutorial em [criação de uma nova fonte](./create.md).
