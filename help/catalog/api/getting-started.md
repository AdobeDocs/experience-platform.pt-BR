---
keywords: Experience Platform;página inicial;tópicos populares;serviço de catálogo;catálogo;Serviço de catálogo;Catálogo
solution: Experience Platform
title: Guia da API do Serviço de catálogo
description: A API do Serviço de catálogo permite que os desenvolvedores gerenciem metadados do conjunto de dados na Adobe Experience Platform. Siga este manual para saber como executar operações importantes usando a API.
exl-id: 812fcdae-ed0e-4f2b-84d7-26f2f79e71b9
source-git-commit: 07451b8ab4bcb7ca43ad0c8a821478b2c9682894
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 34%

---

# [!DNL Catalog Service] Manual da API

O [!DNL Catalog Service] é o sistema de registro para localização e linhagem de dados na Adobe Experience Platform. [!DNL Catalog] O atua como um armazenamento de metadados ou &quot;catálogo&quot;, onde você pode encontrar informações sobre seus dados na [!DNL Experience Platform], sem precisar acessar os dados propriamente ditos. Consulte a [[!DNL Catalog] visão geral das ](../home.md) para obter mais informações.

Este manual do desenvolvedor fornece etapas para ajudar a começar a usar a API [!DNL Catalog]. O guia fornece chamadas de API de exemplo para executar operações importantes usando [!DNL Catalog].

## Pré-requisitos

[!DNL Catalog] rastreia metadados para vários tipos de recursos e operações no [!DNL Experience Platform]. Este guia do desenvolvedor requer uma compreensão funcional dos vários [!DNL Experience Platform] serviços envolvidos na criação e no gerenciamento desses recursos:

* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): a estrutura padronizada pela qual a [!DNL Platform] organiza os dados de experiência do cliente.
* [Assimilação em lote](../../ingestion/batch-ingestion/overview.md): Como [!DNL Experience Platform] A assimila e armazena dados de arquivos de dados, como CSV e Parquet.
* [Assimilação por transmissão](../../ingestion/streaming-ingestion/overview.md): Como [!DNL Experience Platform] A assimila e armazena dados de dispositivos do lado do cliente e do lado do servidor em tempo real.

As seções a seguir fornecem informações adicionais que você precisará saber ou ter em mãos para fazer chamadas com êxito para o [!DNL Catalog Service] API.

## Leitura de chamadas de API de amostra

Este manual fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e conteúdos de solicitação formatados corretamente. Também fornece exemplos de JSON retornado nas respostas da API. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no manual de solução de problemas da [!DNL Experience Platform].

## Coletar valores para cabeçalhos necessários

Para fazer chamadas para APIs da [!DNL Platform], primeiro conclua o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). Concluir o tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API da [!DNL Experience Platform], conforme mostrado abaixo:

* Autorização: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Todos os recursos em [!DNL Experience Platform] são isolados em sandboxes virtuais específicas. Todas as solicitações para [!DNL Platform] As APIs exigem um cabeçalho que especifique o nome da sandbox em que a operação ocorrerá:

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre sandboxes no [!DNL Platform], consulte o [documentação de visão geral da sandbox](../../sandboxes/home.md).

Todas as solicitações que contêm um conteúdo (POST, PUT, PATCH) exigem um cabeçalho adicional:

* Tipo de conteúdo: application/json

## Práticas recomendadas para [!DNL Catalog] Chamadas de API

Ao executar solicitações do GET para o [!DNL Catalog] API, a prática recomendada é incluir parâmetros de consulta em suas solicitações para retornar somente os objetos e as propriedades necessárias. Solicitações não filtradas podem fazer com que as cargas de resposta atinjam tamanhos acima de 3 GB, o que pode retardar o desempenho geral.

Você pode exibir objetos específicos incluindo a respectiva ID no caminho da solicitação ou usar parâmetros de consulta como `properties` e `limit` para filtrar respostas. Os filtros podem ser transmitidos como cabeçalhos e como parâmetros de consulta, com os transmitidos como parâmetros de consulta tendo prioridade. Consulte o documento sobre [filtragem de dados do catálogo](filter-data.md) para obter mais informações.

Como alguns queries podem colocar uma carga pesada sobre a API, limites globais foram implementados em [!DNL Catalog] consultas para oferecer mais suporte às práticas recomendadas.

## Próximas etapas

Este documento cobriu os conhecimento necessários para fazer chamadas para a API da [!DNL Catalog]. Agora você pode prosseguir para as chamadas de amostra fornecidas neste manual do desenvolvedor e seguir suas instruções.

A maioria dos exemplos neste guia usa o `/dataSets` endpoint, mas os princípios podem ser aplicados a outros endpoints dentro [!DNL Catalog] (como `/batches`). Consulte a [Referência da API do serviço de catálogo](https://www.adobe.io/experience-platform-apis/references/catalog/) para obter uma lista completa de todas as chamadas e operações disponíveis para cada endpoint.

Para um fluxo de trabalho passo a passo que demonstra como a [!DNL Catalog] A API está envolvida com a assimilação de dados, consulte o tutorial sobre [criação de um conjunto de dados](../datasets/create.md).
