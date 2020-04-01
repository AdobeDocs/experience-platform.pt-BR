---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guia do desenvolvedor do serviço de catálogo
topic: developer guide
translation-type: tm+mt
source-git-commit: eec5b07427aa9daa44d23f09cfaf1b38f8e811f3

---


# Guia do desenvolvedor do serviço de catálogo

O serviço de catálogo é o sistema de registro para localização e linhagem de dados na Adobe Experience Platform. O Catálogo atua como um armazenamento de metadados ou &quot;catálogo&quot;, onde você pode encontrar informações sobre seus dados na Experience Platform, sem precisar acessar os próprios dados. Consulte a visão geral [do](../home.md) catálogo para obter mais informações.

Este guia do desenvolvedor fornece etapas para ajudá-lo a start usando a API de catálogo. O guia então fornece exemplos de chamadas de API para executar operações principais usando o Catálogo.

## Pré-requisitos

O Catálogo rastreia metadados para vários tipos de recursos e operações na Experience Platform. Este guia do desenvolvedor requer um entendimento prático dos vários serviços da plataforma de experiência envolvidos na criação e gerenciamento desses recursos:

* [Modelo de dados de experiência (XDM)](../../xdm/home.md): A estrutura padronizada pela qual a Plataforma organiza os dados de experiência do cliente.
* [Ingestão](../../ingestion/batch-ingestion/overview.md)em lote: Como a plataforma Experience ingere e armazena dados de arquivos de dados, como CSV e Parquet.
* [Inclusão](../../ingestion/streaming-ingestion/overview.md)de transmissão: Como a plataforma Experience ingere e armazena dados de dispositivos do cliente e do servidor em tempo real.

As seções a seguir fornecem informações adicionais que você precisará conhecer ou ter em mãos para fazer chamadas à API do serviço de catálogo com êxito.

## Lendo chamadas de exemplo da API

Este guia fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção sobre [como ler chamadas](../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de exemplo no guia de solução de problemas da plataforma Experience.

## Reunir valores para cabeçalhos necessários

Para fazer chamadas para APIs de plataforma, você deve primeiro concluir o tutorial [de](../../tutorials/authentication.md)autenticação. A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas da API da plataforma da experiência, como mostrado abaixo:

* Autorização: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos da plataforma Experience são isolados para caixas de proteção virtuais específicas. Todas as solicitações para APIs de plataforma exigem um cabeçalho que especifique o nome da caixa de proteção em que a operação ocorrerá:

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] Para obter mais informações sobre caixas de proteção na Plataforma, consulte a documentação [de visão geral da](../../sandboxes/home.md)caixa de proteção.

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho adicional:

* Tipo de conteúdo: application/json

## Práticas recomendadas para chamadas de API de catálogo

Ao executar solicitações GET para a API de catálogo, a prática recomendada é incluir parâmetros de query em suas solicitações para retornar somente os objetos e as propriedades de que você precisa. As solicitações não filtradas podem fazer com que as cargas de resposta atinjam mais de 3 GB, o que pode retardar o desempenho geral.

Você pode visualização objetos específicos incluindo sua ID no caminho da solicitação ou usar parâmetros de query, como `properties` e `limit` para filtrar respostas. Os Filtros podem ser passados como cabeçalhos e como parâmetros de query, com aqueles passados como parâmetros de query tendo prioridade. Consulte o documento sobre como [filtrar dados](filter-data.md) do catálogo para obter mais informações.

Como alguns query podem sobrecarregar a API, limites globais foram implementados em query de catálogo para oferecer suporte adicional às práticas recomendadas.

## Próximas etapas

Este documento cobriu os conhecimentos pré-requisitos necessários para fazer chamadas para a API de catálogo. Agora você pode continuar com as chamadas de amostra fornecidas neste guia do desenvolvedor e seguir com suas instruções.

A maioria dos exemplos neste guia usam o `/dataSets` endpoint, mas os princípios podem ser aplicados a outros endpoints dentro do Catalog (como `/batches` e `/accounts`). Consulte a referência [API do serviço de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) catálogo para obter uma lista completa de todas as chamadas e operações disponíveis para cada terminal.

Para obter um fluxo de trabalho passo a passo que demonstra como a API de catálogo está envolvida com a ingestão de dados, consulte o tutorial sobre como [criar um conjunto de dados](../datasets/create.md).
