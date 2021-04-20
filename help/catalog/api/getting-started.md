---
keywords: Experience Platform, home, tópicos populares, serviço de catálogo, serviço de catálogo, Catálogo
solution: Experience Platform
title: Guia da API do Serviço de catálogo
topic: developer guide
description: A API do Serviço de catálogo permite que os desenvolvedores gerenciem os metadados do conjunto de dados na Adobe Experience Platform. Siga este guia para saber como executar operações principais usando a API.
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 0%

---


# [!DNL Catalog Service] Guia da API

[!DNL Catalog Service] é o sistema de registro para localização e linhagem de dados na Adobe Experience Platform. [!DNL Catalog] O atua como um armazenamento de metadados ou &quot;catálogo&quot;, onde é possível encontrar informações sobre seus dados no  [!DNL Experience Platform], sem precisar acessar os dados propriamente ditos. Consulte a [[!DNL Catalog] visão geral](../home.md) para obter mais informações.

Este guia do desenvolvedor fornece etapas para ajudá-lo a começar a usar a API [!DNL Catalog]. O guia fornece exemplos de chamadas de API para executar operações principais usando [!DNL Catalog].

## Pré-requisitos

[!DNL Catalog] rastreia metadados para vários tipos de recursos e operações no  [!DNL Experience Platform]. Este guia do desenvolvedor requer uma compreensão funcional dos vários serviços [!DNL Experience Platform] envolvidos na criação e no gerenciamento desses recursos:

* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): A estrutura padronizada pela qual  [!DNL Platform] organiza os dados de experiência do cliente.
* [Ingestão](../../ingestion/batch-ingestion/overview.md) em lote: Como o  [!DNL Experience Platform] assimila e armazena dados de arquivos de dados, como CSV e Parquet.
* [Assimilação](../../ingestion/streaming-ingestion/overview.md) de fluxo: Como  [!DNL Experience Platform] assimila e armazena dados de dispositivos cliente e do lado do servidor em tempo real.

As seções a seguir fornecem informações adicionais que você precisará saber ou ter em mãos para fazer chamadas com êxito para a API [!DNL Catalog Service].

## Lendo exemplos de chamadas de API

Este guia fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações do . Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de exemplo retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no [!DNL Experience Platform] guia de solução de problemas.

## Coletar valores para cabeçalhos necessários

Para fazer chamadas para [!DNL Platform] APIs, primeiro complete o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API [!DNL Experience Platform], conforme mostrado abaixo:

* Autorização: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos em [!DNL Experience Platform] são isolados para sandboxes virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifica o nome da sandbox em que a operação ocorrerá:

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre sandboxes em [!DNL Platform], consulte a [documentação de visão geral da sandbox](../../sandboxes/home.md).

Todas as solicitações que contêm uma carga útil (POST, PUT, PATCH) exigem um cabeçalho adicional:

* Tipo de conteúdo: application/json

## Práticas recomendadas para chamadas de API [!DNL Catalog]

Ao executar solicitações GET para a API [!DNL Catalog], a prática recomendada é incluir parâmetros de consulta em suas solicitações para retornar somente os objetos e propriedades necessários. As solicitações não filtradas podem fazer com que as cargas de resposta atinjam mais de 3 GB, o que pode retardar o desempenho geral.

Você pode exibir objetos específicos incluindo sua ID no caminho da solicitação ou usar parâmetros de consulta, como `properties` e `limit` para filtrar as respostas. Os filtros podem ser passados como cabeçalhos e como parâmetros de consulta, com aqueles passados como parâmetros de consulta tendo prioridade. Consulte o documento em [filtrando dados do catálogo](filter-data.md) para obter mais informações.

Como algumas consultas podem aumentar a carga da API, limites globais foram implementados em consultas [!DNL Catalog] para oferecer suporte adicional às práticas recomendadas.

## Próximas etapas

Este documento cobriu o conhecimento de pré-requisito necessário para fazer chamadas para a API [!DNL Catalog]. Agora você pode prosseguir para as chamadas de exemplo fornecidas neste guia do desenvolvedor e seguir com suas instruções.

A maioria dos exemplos neste guia usa o endpoint `/dataSets`, mas os princípios podem ser aplicados a outros endpoints no [!DNL Catalog] (como `/batches` e `/accounts`). Consulte a [Referência da API do Serviço de Catálogo](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) para obter uma lista completa de todas as chamadas e operações disponíveis para cada endpoint.

Para obter um fluxo de trabalho passo a passo que demonstra como a API [!DNL Catalog] está envolvida com a assimilação de dados, consulte o tutorial em [criar um conjunto de dados](../datasets/create.md).
