---
keywords: Experience Platform;página inicial;tópicos populares;Adobe Experience Platform;guia de api;guia de api da plataforma;introdução à plataforma;guia do desenvolvedor
solution: Experience Platform
title: Introdução às APIs do Adobe Experience Platform
description: O Adobe Experience Platform fornece serviços de API que estão intimamente vinculados entre si. Este guia contém informações sobre os serviços disponíveis, cabeçalhos necessários para operações CRUD, mensagens de erro, coleções do Postman e exemplos de chamadas de API.
exl-id: a362bcb4-a908-43a8-abd3-0e1d21cb9117
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '1379'
ht-degree: 2%

---

# Introdução às APIs do Adobe Experience Platform

O Adobe Experience Platform é desenvolvido sob uma filosofia de &quot;API first&quot;. Usando APIs da Platform, você pode executar programaticamente operações básicas de CRUD (Criar, Ler, Atualizar, Excluir) em relação aos dados, como configurar atributos calculados, acessar dados/entidades, exportar dados, excluir dados ou lotes desnecessários e muito mais.

As APIs para cada serviço de Experience Platform compartilham o mesmo conjunto de cabeçalhos de autenticação e usam sintaxes semelhantes para suas operações CRUD. O guia a seguir descreve as etapas necessárias para começar a usar as APIs da plataforma.

## Autenticação e cabeçalhos

Para fazer chamadas para endpoints da Platform com êxito, é necessário concluir o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). Concluir o tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários nas chamadas de API de Experience Platform, conforme mostrado abaixo:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

### Cabeçalho da sandbox

Todos os recursos no Experience Platform são isolados em sandboxes virtuais específicas. As solicitações para APIs da Platform exigem um cabeçalho que especifique o nome da sandbox em que a operação ocorrerá:

- `x-sandbox-name: {SANDBOX_NAME}`

Para obter mais informações sobre sandboxes na Platform, consulte a [documentação de visão geral da sandbox](../sandboxes/home.md).

### Cabeçalho de tipo de conteúdo

Todas as solicitações com uma carga no corpo da solicitação (como chamadas POST, PUT e PATCH) devem incluir uma `Content-Type` cabeçalho. Os valores aceitos são específicos para cada endpoint de API. Se uma determinada `Content-Type` for necessário para um endpoint, seu valor será mostrado nas solicitações de API de exemplo fornecidas pelo [Guias de API para serviços de plataforma individuais](#api-guides).

## Fundamentos da API Experience Platform

As APIs do Adobe Experience Platform empregam várias tecnologias e sintaxes subjacentes que são importantes de entender para gerenciar efetivamente os recursos da plataforma.

Para saber mais sobre as tecnologias de API subjacentes que a Platform utiliza, incluindo objetos de esquema JSON de exemplo, visite o [Fundamentos da API Experience Platform](api-fundamentals.md) guia.

## Coleções Postman para APIs Experience Platform

O Postman é uma plataforma de colaboração para o desenvolvimento de API que permite configurar ambientes com variáveis predefinidas, compartilhar coleções de API, simplificar solicitações CRUD e muito mais. A maioria dos serviços de API da Platform tem coleções do Postman que podem ser usadas para ajudar a fazer chamadas de API.

Para saber mais sobre o Postman, incluindo como configurar um ambiente, uma lista de coleções disponíveis e como importar coleções, visite o [Documentação do Platform Postman](postman.md).

## Leitura de chamadas de API de amostra {#sample-api}

Os formatos de solicitação variam dependendo da API da plataforma que está sendo usada. A melhor maneira de saber como estruturar suas chamadas de API é seguindo os exemplos fornecidos na documentação do serviço da Platform específico que você está usando.

A documentação do [!DNL Experience Platform] O mostra exemplos de chamadas de API de duas maneiras diferentes. Primeiro, a chamada é apresentada em sua **Formato da API**, uma representação de modelo que mostra apenas a operação (GET, POST, PUT, PATCH, DELETE) e o endpoint que está sendo usado (por exemplo, `/global/classes`). Alguns modelos também mostram a localização das variáveis para ajudar a ilustrar como uma chamada deve ser formulada, como `GET /{VARIABLE}/classes/{ANOTHER_VARIABLE}`.

As chamadas são exibidas como comandos cURL em uma **Solicitação**, que inclui os cabeçalhos necessários e o &quot;caminho base&quot; completo necessário para interagir com êxito com a API. O caminho base deve ser anexado previamente a todos os endpoints. Por exemplo, a tabela acima `/global/classes` o endpoint torna-se `https://platform.adobe.io/data/foundation/schemaregistry/global/classes`. Você verá o formato da API/padrão de solicitação em toda a documentação e deve usar o caminho completo mostrado no exemplo de solicitação ao fazer suas próprias chamadas para APIs da plataforma.

### Exemplo de solicitação de API

Veja a seguir um exemplo de solicitação da API que demonstra o formato que você encontrará na documentação.

**Formato da API**

O formato da API mostra a operação (GET) e o endpoint que está sendo usado. As variáveis são indicadas por chaves (nesse caso, `{CONTAINER_ID}`).

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

A resposta ilustra o que você esperaria receber após uma chamada bem-sucedida para a API, com base na solicitação enviada. Ocasionalmente, a resposta é truncada por espaço, o que significa que você pode ver mais informações ou informações adicionais para aquelas exibidas na amostra.

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

A variável [Guia de solução de problemas da Platform](troubleshooting.md#errors-and-troubleshooting) O fornece uma lista de erros que você pode encontrar ao usar qualquer serviço Experience Platform.

Para obter guias de solução de problemas sobre serviços de plataforma individuais, consulte a [diretório de solução de problemas de serviço](troubleshooting.md#service-troubleshooting-directory).

Para obter mais informações sobre endpoints específicos nas APIs da Platform, incluindo cabeçalhos e corpos de solicitação necessários, consulte o [Guias da API da plataforma](#api-guides).

## Guias da API da plataforma {#api-guides}

| Manual da API | Descrição |
| --- | --- |
| [[!DNL Access Control] Manual da API](.././access-control/api/getting-started.md) | A variável [!DNL Access Control] O endpoint da API pode recuperar as políticas atuais em vigor para um usuário em determinados recursos em uma sandbox especificada. Todos os outros recursos de controle de acesso são fornecidos por meio do [Adobe Admin Console](https://adminconsole.adobe.com/). |
| [Guia da API de assimilação em lote](.././ingestion/batch-ingestion/api-overview.md) | O ADOBE EXPERIENCE PLATFORM [!DNL Data Ingestion] A API permite assimilar dados na Platform como arquivos em lote. Os dados assimilados podem ser os dados do perfil de um arquivo simples em um sistema CRM (como um arquivo Parquet) ou dados que estejam em conformidade com um esquema conhecido no Registro de Esquemas (XDM). |
| [[!DNL Catalog Service] Manual da API](.././catalog/api/getting-started.md) | A variável [!DNL Catalog Service] A API permite que os desenvolvedores gerenciem metadados do conjunto de dados na Adobe Experience Platform. Isso inclui locais de dados, estágios de processamento, erros que ocorreram durante o processamento e relatórios de dados. |
| [[!DNL Data Access] Manual da API](.././data-access/api.md) | A variável [!DNL Data Access] A API permite que os desenvolvedores recuperem informações sobre conjuntos de dados assimilados no Experience Platform. Isso inclui acessar e baixar arquivos de conjunto de dados, recuperar informações de cabeçalho, listar lotes com falha e bem-sucedidos e baixar arquivos CSV/Parquet de visualização. |
| [[!DNL Dataset Service] Manual da API](.././data-governance/labels/dataset-api.md) | A API de serviço do conjunto de dados permite aplicar e editar rótulos de uso para conjuntos de dados. Ela faz parte dos recursos de catálogo de dados da Adobe Experience Platform, mas é separada da API de serviço de catálogo que gerencia metadados do conjunto de dados. |
| [[!DNL Identity Service] Manual da API](.././identity-service/api/getting-started.md) | A variável [!DNL Identity Service] A API permite que os desenvolvedores gerenciem a identificação entre dispositivos, canais e quase em tempo real dos clientes usando gráficos de identidade no Adobe Experience Platform. |
| [[!DNL Observability Insights] Manual da API](.././observability/api/overview.md) | [!DNL Observability Insights] é uma API RESTful que permite aos desenvolvedores expor as principais métricas de observabilidade no Adobe Experience Platform. Essas métricas fornecem insights sobre estatísticas de uso da Platform, verificações de integridade de serviços da Platform, tendências históricas e indicadores de desempenho para várias funcionalidades da Platform. |
| [[!DNL Policy Service] Guia da API](.././data-governance/api/overview.md) <br> (Governança de dados) | A variável [!DNL Policy Service] A API permite criar e gerenciar rótulos e políticas de uso de dados para determinar quais ações de marketing podem ser executadas em relação aos dados que contêm determinados rótulos de uso de dados. Para aplicar rótulos a conjuntos de dados e campos, consulte o [[!DNL Dataset Service] API](.././data-governance/labels/dataset-api.md) guia |
| [[!DNL Privacy Service] Manual da API](.././privacy-service/api/getting-started.md) | A variável [!DNL Privacy Service] A API permite que os desenvolvedores criem e gerenciem solicitações de clientes para acessar ou excluir seus dados pessoais nos aplicativos Experience Cloud, em conformidade com as regulamentações legais de privacidade. |
| [[!DNL Query Service] Manual da API](.././query-service/api/getting-started.md) | A variável [!DNL Query Service] A API permite que os desenvolvedores consultem seus dados do Adobe Experience Platform usando SQL padrão. |
| [[!DNL Real-Time Customer Profile] Manual da API](.././profile/api/overview.md) | A API de perfil do cliente em tempo real permite que os desenvolvedores explorem e trabalhem com dados de perfil, incluindo a exibição de perfis, criação e atualização de políticas de mesclagem, exportação ou amostragem de dados de perfil e exclusão de dados de perfil que não são mais necessários ou que foram adicionados por engano. |
| [Guia da API de sandbox](.././sandboxes/api/getting-started.md) | A API de sandbox permite que os desenvolvedores gerenciem programaticamente ambientes isolados de sandbox virtual no Adobe Experience Platform. |
| [[!DNL Schema Registry] Guia da API](.././xdm/api/overview.md) <br> (XDM) | A variável [!DNL Schema Registry] A API permite que os desenvolvedores gerenciem programaticamente todos os esquemas e recursos relacionados do Experience Data Model (XDM) no Adobe Experience Platform. |
| [[!DNL Segmentation Service] Manual da API](.././segmentation/api/overview.md) | A variável [!DNL Segmentation Service] A API permite que os desenvolvedores gerenciem programaticamente as operações de segmentação no Adobe Experience Platform. Isso inclui a criação de segmentos e a geração de públicos-alvo a partir dos dados do Perfil do cliente em tempo real. |
| [[!DNL Sensei Machine Learning] Guia da API](.././data-science-workspace/api/getting-started.md) <br> (Espaço de trabalho de ciência de dados) | A variável [!DNL Sensei Machine Learning] A API fornece um mecanismo para que cientistas de dados organizem e gerenciem serviços de aprendizado de máquina (ML) com base em integração de algoritmo, experimentação e implantação de serviço. |

Para obter mais informações sobre endpoints e operações específicos disponíveis para cada serviço, consulte [Documentação de referência da API](https://www.adobe.com/go/platform-api-reference-en) no Adobe I/O.

## Próximas etapas

Este documento apresentou os cabeçalhos necessários, os guias disponíveis e forneceu um exemplo de chamada de API. Agora que você tem os valores de cabeçalho necessários para fazer chamadas de API no Adobe Experience Platform, selecione um endpoint de API que deseja explorar na [Tabela de guias da API da plataforma](#api-guides).

Para obter respostas para perguntas frequentes, consulte o [Guia de solução de problemas da Platform](troubleshooting.md).

Para configurar um ambiente do Postman e explorar as coleções disponíveis do Postman, consulte [Guia do Platform Postman](postman.md).
