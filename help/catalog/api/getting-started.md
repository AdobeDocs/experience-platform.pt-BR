---
keywords: Experience Platform;home;popular tópicos;serviço de catálogo;catálogo;serviço de catálogo;Catálogo;Catálogo
solution: Experience Platform
title: Guia do desenvolvedor do serviço de catálogo
topic: developer guide
description: Este guia do desenvolvedor fornece etapas para ajudá-lo a start usando a API de catálogo. O guia então fornece exemplos de chamadas de API para executar operações principais usando o Catálogo.
translation-type: tm+mt
source-git-commit: ece2ae1eea8426813a95c18096c1b428acfd1a71
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 0%

---


# [!DNL Catalog Service] guia do desenvolvedor

[!DNL Catalog Service] é o sistema de registro para localização e linhagem de dados no Adobe Experience Platform. [!DNL Catalog] atua como um armazenamento de metadados ou &quot;catálogo&quot; no qual você pode encontrar informações sobre seus dados  [!DNL Experience Platform], sem precisar acessar os próprios dados. Consulte a [[!DNL Catalog] visão geral](../home.md) para obter mais informações.

Este guia do desenvolvedor fornece etapas para ajudá-lo a start usando a API [!DNL Catalog]. O guia então fornece exemplos de chamadas de API para executar operações principais usando [!DNL Catalog].

## Pré-requisitos

[!DNL Catalog] rastreia metadados para vários tipos de recursos e operações dentro  [!DNL Experience Platform]. Este guia do desenvolvedor requer um entendimento prático dos vários [!DNL Experience Platform] serviços envolvidos na criação e gerenciamento desses recursos:

* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): A estrutura padronizada pela qual  [!DNL Platform] organiza os dados de experiência do cliente.
* [Ingestão](../../ingestion/batch-ingestion/overview.md) em lote: Como  [!DNL Experience Platform] ingere e armazena dados de arquivos de dados, como CSV e Parquet.
* [Inclusão](../../ingestion/streaming-ingestion/overview.md) de transmissão: Como  [!DNL Experience Platform] ingere e armazena dados de dispositivos do cliente e do servidor em tempo real.

As seções a seguir fornecem informações adicionais que você precisará conhecer ou ter em mãos para fazer chamadas com êxito para a API [!DNL Catalog Service].

## Lendo chamadas de exemplo da API

Este guia fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção em [como ler chamadas de API de exemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas [!DNL Experience Platform].

## Reunir valores para cabeçalhos necessários

Para fazer chamadas para [!DNL Platform] APIs, você deve primeiro concluir o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API [!DNL Experience Platform], como mostrado abaixo:

* Autorização: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos em [!DNL Experience Platform] são isolados para caixas de proteção virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifique o nome da caixa de proteção em que a operação ocorrerá:

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre caixas de proteção em [!DNL Platform], consulte a [documentação de visão geral da caixa de proteção](../../sandboxes/home.md).

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho adicional:

* Tipo de conteúdo: application/json

## Práticas recomendadas para chamadas de API [!DNL Catalog]

Ao executar solicitações de GET para a API [!DNL Catalog], a prática recomendada é incluir parâmetros de query em suas solicitações para retornar somente os objetos e propriedades de que você precisa. As solicitações não filtradas podem fazer com que as cargas de resposta atinjam mais de 3 GB, o que pode retardar o desempenho geral.

Você pode visualização objetos específicos incluindo sua ID no caminho da solicitação ou usar parâmetros de query como `properties` e `limit` para filtrar respostas. Os filtros podem ser passados como cabeçalhos e como parâmetros de query, com aqueles passados como parâmetros de query tendo prioridade. Consulte o documento em [filtrando dados do catálogo](filter-data.md) para obter mais informações.

Como alguns query podem sobrecarregar a API, limites globais foram implementados em query [!DNL Catalog] para oferecer suporte adicional às práticas recomendadas.

## Próximas etapas

Este documento cobriu o conhecimento pré-requisito necessário para fazer chamadas para a API [!DNL Catalog]. Agora você pode continuar com as chamadas de amostra fornecidas neste guia do desenvolvedor e seguir com suas instruções.

A maioria dos exemplos neste guia usa o endpoint `/dataSets`, mas os princípios podem ser aplicados a outros endpoints dentro de [!DNL Catalog] (como `/batches` e `/accounts`). Consulte a [Referência da API do serviço de catálogo](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) para obter uma lista completa de todas as chamadas e operações disponíveis para cada endpoint.

Para obter um fluxo de trabalho passo a passo que demonstra como a API [!DNL Catalog] está envolvida com a ingestão de dados, consulte o tutorial em [criação de um conjunto de dados](../datasets/create.md).
