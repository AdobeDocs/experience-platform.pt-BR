---
keywords: Experience Platform, home, tópicos populares, Adobe Experience Platform, guia de api, guia de api da plataforma, introdução à plataforma, guia do desenvolvedor
solution: Experience Platform
title: Introdução às APIs do Adobe Experience Platform
topic-legacy: api guide
description: A Adobe Experience Platform fornece serviços de API que estão intimamente vinculados uns aos outros. Este guia contém informações sobre os serviços disponíveis, cabeçalhos necessários para operações CRUD, mensagens de erro, coleções de Postman e chamadas de API de exemplo.
exl-id: a362bcb4-a908-43a8-abd3-0e1d21cb9117
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1425'
ht-degree: 0%

---

# Introdução às APIs do Adobe Experience Platform

O Adobe Experience Platform é desenvolvido sob uma filosofia de &quot;API first&quot;. Usando as APIs da plataforma, você pode executar programaticamente operações CRUD básicas (Criar, Ler, Atualizar, Excluir) em relação aos dados, como configurar atributos calculados, acessar dados/entidades, exportar dados, excluir dados desnecessários ou lotes e muito mais.

As APIs de cada serviço do Experience Platform compartilham o mesmo conjunto de cabeçalhos de autenticação e usam sintaxes semelhantes para suas operações CRUD. O guia a seguir descreve as etapas necessárias para começar a usar as APIs da plataforma.

## Autenticação e cabeçalhos

Para fazer chamadas com êxito para pontos de extremidade da plataforma, é necessário concluir o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em chamadas de API do Experience Platform, conforme mostrado abaixo:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

### Cabeçalho de sandbox

Todos os recursos no Experience Platform são isolados para sandboxes virtuais específicas. As solicitações para APIs da plataforma exigem um cabeçalho que especifica o nome da sandbox em que a operação ocorrerá:

- `x-sandbox-name: {SANDBOX_NAME}`

Para obter mais informações sobre sandboxes na Platform, consulte a [documentação de visão geral da sandbox](../sandboxes/home.md).

### Cabeçalho do tipo conteúdo

Todas as solicitações com uma carga no corpo da solicitação (como chamadas de POST, PUT e PATCH) devem incluir um cabeçalho `Content-Type`. Os valores aceitos são específicos para cada endpoint da API. Se um valor `Content-Type` específico for necessário para um ponto de extremidade, seu valor será mostrado nas solicitações de API de exemplo fornecidas pelos [guias de API para serviços individuais da plataforma](#api-guides).

## Fundamentos da API do Experience Platform

As APIs da Adobe Experience Platform empregam várias tecnologias e sintaxes subjacentes que são importantes para o entendimento a fim de gerenciar eficientemente os recursos da plataforma.

Para saber mais sobre as tecnologias de API subjacentes que a Platform utiliza, incluindo objetos de esquema JSON de exemplo, visite o guia [Experience Platform API fundamentals](api-fundamentals.md) .

## Coleções de postman para APIs do Experience Platform

O Postman é uma plataforma de colaboração para desenvolvimento de API que permite configurar ambientes com variáveis predefinidas, compartilhar coleções de API, simplificar solicitações de CRUD e muito mais. A maioria dos serviços de API da Platform tem coleções Postman que podem ser usadas para ajudar a fazer chamadas de API.

Para saber mais sobre o Postman, incluindo como configurar um ambiente, uma lista de coleções disponíveis e como importar coleções, visite a [documentação do Platform Postman](postman.md).

## Lendo chamadas de API de exemplo {#sample-api}

Os formatos de solicitação variam de acordo com a API de plataforma em uso. A melhor maneira de aprender como estruturar suas chamadas de API é seguindo os exemplos fornecidos na documentação do serviço de plataforma específico que você está usando.

A documentação de [!DNL Experience Platform] mostra exemplos de chamadas de API de duas maneiras diferentes. Primeiro, a chamada é apresentada em seu **API format**, uma representação de modelo mostrando somente a operação (GET, POST, PUT, PATCH, DELETE) e o ponto de extremidade que está sendo usado (por exemplo, `/global/classes`). Alguns modelos também mostram a localização das variáveis para ajudar a ilustrar como uma chamada deve ser formulada, como `GET /{VARIABLE}/classes/{ANOTHER_VARIABLE}`.

As chamadas são mostradas como comandos cURL em um **Request**, que inclui os cabeçalhos necessários e o &quot;caminho base&quot; completo necessário para interagir com a API com êxito. O caminho base deve ser prefixado para todos os pontos finais. Por exemplo, o ponto de extremidade `/global/classes` acima é `https://platform.adobe.io/data/foundation/schemaregistry/global/classes`. Você verá o formato da API/padrão de solicitação em toda a documentação e deverá usar o caminho completo mostrado na solicitação de exemplo ao fazer suas próprias chamadas para APIs da plataforma.

### Exemplo de solicitação de API

A seguir, um exemplo de solicitação de API que demonstra o formato que você encontrará na documentação.

**Formato da API**

O formato da API mostra a operação (GET) e o ponto de extremidade que está sendo usado. As variáveis são indicadas por chaves (neste caso, `{CONTAINER_ID}`).

```http
GET /{CONTAINER_ID}/classes
```

**Solicitação**

Nesta solicitação de exemplo, as variáveis do formato da API recebem valores reais no caminho da solicitação. Além disso, todos os cabeçalhos necessários são mostrados como valores de cabeçalho de amostra ou variáveis, onde informações confidenciais (como tokens de segurança e IDs de acesso) devem ser incluídas.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/classes \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

A resposta ilustra o que você esperaria receber após uma chamada bem-sucedida para a API, com base na solicitação que foi enviada. Ocasionalmente, a resposta é truncada para o espaço, o que significa que você pode ver mais informações ou informações adicionais para aquela que é exibida na amostra.

```json
{
    "results": [
        {
            "title": "XDM ExperienceEvent",
            "$id": "https://ns.adobe.com/xdm/context/experienceevent",
            "meta:altId": "_xdm.context.experienceevent",
            "version": "1"
        },
        {
            "title": "XDM Individual Profile",
            "$id": "https://ns.adobe.com/xdm/context/profile",
            "meta:altId": "_xdm.context.profile",
            "version": "1"
        }
    ],
    "_links": {}
}
```

## Mensagens de erro

O [Guia de solução de problemas da plataforma](troubleshooting.md#errors-and-troubleshooting) fornece uma lista de erros que podem ser encontrados ao usar qualquer serviço do Experience Platform.

Para obter guias de solução de problemas em serviços individuais da Platform, consulte o [diretório de solução de problemas de serviço](troubleshooting.md#service-troubleshooting-directory).

Para obter mais informações sobre endpoints específicos nas APIs da plataforma, incluindo cabeçalhos obrigatórios e corpos de solicitação, consulte os [Guias da API da plataforma](#api-guides).

## Guias da API da plataforma {#api-guides}

| Guia da API | Descrição |
| --- | --- |
| [[!DNL Access Control] Guia da API](.././access-control/api/getting-started.md) | O endpoint da API [!DNL Access Control] pode recuperar as políticas atuais em vigor para um usuário em determinados recursos em uma sandbox especificada. Todos os outros recursos de controle de acesso são fornecidos por meio do [Adobe Admin Console](https://adminconsole.adobe.com/). |
| [Guia da API de assimilação em lote](.././ingestion/batch-ingestion/api-overview.md) | A API [!DNL Data Ingestion] do Adobe Experience Platform permite assimilar dados na Platform como arquivos em lote. Os dados que estão sendo assimilados podem ser os dados do perfil de um arquivo simples em um sistema CRM (como um arquivo Parquet) ou dados que estão em conformidade com um esquema conhecido no Registro de Schema (XDM). |
| [[!DNL Catalog Service] Guia da API](.././catalog/api/getting-started.md) | A API [!DNL Catalog Service] permite que os desenvolvedores gerenciem os metadados do conjunto de dados no Adobe Experience Platform. Isso inclui locais de dados, estágios de processamento, erros que ocorreram durante o processamento e relatórios de dados. |
| [[!DNL Data Access] Guia da API](.././data-access/api.md) | A API [!DNL Data Access] permite que os desenvolvedores recuperem informações sobre conjuntos de dados assimilados no Experience Platform. Isso inclui acessar e baixar arquivos de conjunto de dados, recuperar informações de cabeçalho, listar lotes com falha e êxito e baixar arquivos CSV / Parquet de visualização. |
| [[!DNL Dataset Service] Guia da API](.././data-governance/labels/dataset-api.md) | A API do Serviço de conjunto de dados permite aplicar e editar rótulos de uso para conjuntos de dados. Ela faz parte dos recursos de catálogo de dados da Adobe Experience Platform, mas é separada da API do Serviço de catálogo que gerencia os metadados do conjunto de dados. |
| [[!DNL Flow Service] Guia da API](.././sources/tutorials/api/create-dataset-base-connection.md) <br>  (Fontes e destinos) | A API [!DNL Flow Service] é usada para coletar e centralizar seus dados de várias fontes diferentes e é usada para criar e ativar dados para vários destinos no Adobe Experience Platform. O serviço fornece uma RESTful API da qual todas as fontes compatíveis são conectáveis. |
| [[!DNL Identity Service] Guia da API](.././identity-service/api/getting-started.md) | A API [!DNL Identity Service] permite que os desenvolvedores gerenciem a identificação entre dispositivos, entre canais e quase em tempo real de seus clientes usando gráficos de identidade no Adobe Experience Platform. |
| [[!DNL Observability Insights] Guia da API](.././observability/api/overview.md) | [!DNL Observability Insights] O é uma RESTful API que permite que os desenvolvedores exponham as principais métricas de observabilidade no Adobe Experience Platform. Essas métricas fornecem informações sobre as estatísticas de uso da plataforma, verificações de integridade de serviços da plataforma, tendências históricas e indicadores de desempenho para várias funcionalidades da plataforma. |
| [[!DNL Policy Service] Guia da API](.././data-governance/api/overview.md) <br>  (Governança de dados) | A API [!DNL Policy Service] permite criar e gerenciar rótulos e políticas de uso de dados para determinar quais ações de marketing podem ser tomadas em relação aos dados que contêm determinados rótulos de uso de dados. Para aplicar rótulos a conjuntos de dados e campos, consulte o guia [[!DNL Dataset Service] API](.././data-governance/labels/dataset-api.md) |
| [[!DNL Privacy Service] Guia da API](.././privacy-service/api/getting-started.md) | A API [!DNL Privacy Service] permite que os desenvolvedores criem e gerenciem solicitações de clientes para acessar ou excluir seus dados pessoais em aplicativos Experience Cloud, em conformidade com as regulamentações legais de privacidade. |
| [[!DNL Query Service] Guia da API](.././query-service/api/getting-started.md) | A API [!DNL Query Service] permite que os desenvolvedores consultem seus dados do Adobe Experience Platform usando o SQL padrão. |
| [[!DNL Real-time Customer Profile] Guia da API](.././profile/api/overview.md) | A API do perfil do cliente em tempo real permite que os desenvolvedores explorem e trabalhem com dados do perfil, incluindo a visualização de perfis, a criação e atualização de políticas de mesclagem, a exportação ou a amostragem de dados do perfil e a exclusão de dados do perfil que não são mais necessários ou foram adicionados com erro. |
| [Guia da API de sandbox](.././sandboxes/api/getting-started.md) | A API de sandbox permite que os desenvolvedores gerenciem programaticamente ambientes de sandbox virtuais isolados no Adobe Experience Platform. |
| [[!DNL Schema Registry] Guia](.././xdm/api/overview.md) <br>  de API (XDM) | A API [!DNL Schema Registry] permite que os desenvolvedores gerenciem programaticamente todos os esquemas e recursos relacionados do Experience Data Model (XDM) no Adobe Experience Platform. |
| [[!DNL Segmentation Service] Guia da API](.././segmentation/api/overview.md) | A API [!DNL Segmentation Service] permite que os desenvolvedores gerenciem programaticamente as operações de segmentação no Adobe Experience Platform. Isso inclui a criação de segmentos e a geração de públicos-alvo a partir dos dados do Perfil do cliente em tempo real. |
| [[!DNL Sensei Machine Learning] Guia da API](.././data-science-workspace/api/getting-started.md) <br>  (Data Science Workspace) | A API [!DNL Sensei Machine Learning] fornece um mecanismo para os cientistas de dados organizarem e gerenciarem os serviços de aprendizado de máquina (ML) a partir de integração de algoritmo, experimentação e implantação de serviço. |

Para obter mais informações sobre endpoints e operações específicos disponíveis para cada serviço, consulte a [documentação de referência da API](http://www.adobe.com/go/platform-api-reference-en) no Adobe I/O.

## Próximas etapas

Este documento introduziu os cabeçalhos necessários, os guias disponíveis e forneceu um exemplo de chamada à API. Agora que você tem os valores de cabeçalho necessários para fazer chamadas de API no Adobe Experience Platform, selecione um endpoint de API que deseja explorar na tabela [Guias de API da plataforma](#api-guides).

Para obter respostas a perguntas frequentes, consulte o [Guia de solução de problemas da plataforma](troubleshooting.md).

Para configurar um ambiente Postman e explorar as coleções Postman disponíveis, consulte o [Guia do Platform Postman](postman.md).
