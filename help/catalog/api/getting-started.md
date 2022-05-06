---
keywords: Experience Platform, home, tópicos populares, serviço de catálogo, catálogo, serviço de catálogo, Catálogo
solution: Experience Platform
title: Guia da API do Serviço de catálogo
topic-legacy: developer guide
description: A API do Serviço de catálogo permite que os desenvolvedores gerenciem os metadados do conjunto de dados no Adobe Experience Platform. Siga este manual para saber como executar operações importantes usando a API.
exl-id: 812fcdae-ed0e-4f2b-84d7-26f2f79e71b9
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 3%

---

# [!DNL Catalog Service] Manual da API

[!DNL Catalog Service] é o sistema de registro para localização e linhagem de dados no Adobe Experience Platform. [!DNL Catalog] atua como um armazenamento de metadados ou &quot;catálogo&quot;, onde você pode encontrar informações sobre seus dados no [!DNL Experience Platform], sem precisar acessar os dados propriamente ditos. Consulte a [[!DNL Catalog] visão geral](../home.md) para obter mais informações.

Este guia do desenvolvedor fornece etapas para ajudá-lo a começar a usar o [!DNL Catalog] API. O guia fornece exemplos de chamadas de API para executar operações principais usando [!DNL Catalog].

## Pré-requisitos

[!DNL Catalog] rastreia metadados para vários tipos de recursos e operações no [!DNL Experience Platform]. Este guia do desenvolvedor requer uma compreensão funcional das várias [!DNL Experience Platform] serviços envolvidos na criação e gerenciamento desses recursos:

* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): O quadro normalizado pelo qual [!DNL Platform] organiza os dados de experiência do cliente.
* [Ingestão em lote](../../ingestion/batch-ingestion/overview.md): How [!DNL Experience Platform] O assimila e armazena dados de arquivos de dados, como CSV e Parquet.
* [Assimilação de fluxo](../../ingestion/streaming-ingestion/overview.md): How [!DNL Experience Platform] O assimila e armazena dados de dispositivos cliente e servidor em tempo real.

As seções a seguir fornecem informações adicionais que você precisará saber ou ter em mãos para fazer chamadas para o [!DNL Catalog Service] API.

## Lendo exemplos de chamadas de API

Este guia fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações do . Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de exemplo retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler exemplos de chamadas de API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no [!DNL Experience Platform] guia de solução de problemas.

## Coletar valores para cabeçalhos necessários

Para fazer chamadas para [!DNL Platform] As APIs devem ser concluídas primeiro [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todos [!DNL Experience Platform] Chamadas de API, conforme mostrado abaixo:

* Autorização: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Todos os recursos em [!DNL Experience Platform] são isoladas em sandboxes virtuais específicas. Todas as solicitações para [!DNL Platform] As APIs exigem um cabeçalho que especifica o nome da sandbox em que a operação ocorrerá:

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre sandboxes em [!DNL Platform], consulte o [documentação de visão geral da sandbox](../../sandboxes/home.md).

Todas as solicitações que contêm uma carga útil (POST, PUT, PATCH) exigem um cabeçalho adicional:

* Tipo de conteúdo: application/json

## Práticas recomendadas para [!DNL Catalog] Chamadas de API

Ao executar solicitações do GET para a [!DNL Catalog] API, a prática recomendada é incluir parâmetros de consulta em suas solicitações para retornar somente os objetos e propriedades necessários. As solicitações não filtradas podem fazer com que as cargas de resposta atinjam mais de 3 GB, o que pode retardar o desempenho geral.

É possível exibir objetos específicos incluindo a ID no caminho da solicitação ou usar parâmetros de consulta, como `properties` e `limit` para filtrar as respostas. Os filtros podem ser passados como cabeçalhos e como parâmetros de consulta, com aqueles passados como parâmetros de consulta tendo prioridade. Consulte o documento em [filtrar dados do catálogo](filter-data.md) para obter mais informações.

Como algumas consultas podem aumentar a carga da API, os limites globais foram implementados em [!DNL Catalog] consultas para oferecer suporte adicional às práticas recomendadas.

## Próximas etapas

Este documento cobria os pré-requisitos necessários para fazer chamadas para o [!DNL Catalog] API. Agora você pode prosseguir para as chamadas de exemplo fornecidas neste guia do desenvolvedor e seguir com suas instruções.

A maioria dos exemplos neste guia usa o `/dataSets` endpoint, mas os princípios podem ser aplicados a outros endpoints no [!DNL Catalog] (como `/batches` e `/accounts`). Consulte a [Referência da API do serviço de catálogo](https://www.adobe.io/experience-platform-apis/references/catalog/) para obter uma lista completa de todas as chamadas e operações disponíveis para cada endpoint.

Para um fluxo de trabalho passo a passo que demonstra como a variável [!DNL Catalog] A API está envolvida com a assimilação de dados, consulte o tutorial em [criação de um conjunto de dados](../datasets/create.md).
