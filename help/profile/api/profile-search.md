---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Guia do desenvolvedor da API do Perfil do cliente em tempo real
topic: guide
translation-type: tm+mt
source-git-commit: 95e002c60389ca7e4c1dcf32bbcf6f552cd55d95

---


# Pesquisa de Perfis

A pesquisa de Perfis é usada para pesquisar e indexar campos configuráveis contidos em várias fontes de dados e retorná-los em tempo quase real.

Este guia fornece informações para ajudá-lo a entender melhor a pesquisa de Perfis e inclui exemplos de chamadas de API para executar ações básicas usando a API.

## Introdução

Os pontos de extremidade da API usados neste guia fazem parte da API do Perfil do cliente em tempo real. Antes de continuar, leia o guia [do desenvolvedor do Perfil do cliente em tempo](getting-started.md)real.

Em particular, a seção [de](getting-started.md) introdução do guia do desenvolvedor do Perfil inclui links para tópicos relacionados, um guia para ler as chamadas de API de amostra neste documento e informações importantes sobre os cabeçalhos necessários que são necessários para fazer chamadas com êxito para quaisquer APIs da plataforma de experiência.

### Obter resultados de pesquisa

O ponto de extremidade de pesquisa pode ser usado para obter resultados de pesquisa com base nos valores do `schema.name` parâmetro obrigatório e parâmetros de query opcionais adicionais. Vários parâmetros podem ser usados, separados por E comercial (&amp;).

**Formato da API**

```http
GET /search?{QUERY_PARAMETERS}
```

| Parâmetro | Descrição |
|---|---|
| `schema.name` | **Obrigatório.** O nome da classe de schema que contém o conteúdo a ser pesquisado, escrito em formato de notação de pontos. Atualmente, somente `schema.name=_xdm.context.segmentdefinition` é suportado. |
| `limit` | O número de resultados da pesquisa a serem retornados. O valor padrão é 50. |
| `page` | O número de página usado para paginar os resultados do query pesquisado. |
| `s` | Um query que está em conformidade com a implementação da Microsoft da sintaxe [de pesquisa de](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax)Lucene. Se nenhum termo de pesquisa for especificado, todos os registros associados `schema.name` serão retornados. Uma explicação mais detalhada pode ser encontrada na seção Parâmetros [de](#search-parameters) pesquisa deste documento. |
| `namespace` | Identifica os dados reais a serem pesquisados na classe do schema especificada no `schema.name` parâmetro. |
| `organization.type` | Determina o conteúdo da resposta. O formato do conteúdo retornado depende dos valores usados em `schema.name`. Para `_xdm.context.segmentdefinition`, os valores válidos são `hierarchy` ou `hierarchyinfo`. |
| `organization.id` | **Obrigatório se`organization.type`for especificado.** Atribui a hierarquia da organização especificada quando usada com a hierarquia `organization.type` . |

**Solicitação**

```shell
curl -X GET \
    https://platform.adobe.io/data/core/ups/search?schema.name=_xdm.context.segmentdefinition \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma matriz de objetos que atendem aos seus critérios de pesquisa. Neste exemplo, como o `schema.name` parâmetro era `_xdm.context.segmentdefinition`, uma lista de definições de segmento é retornada.

```json
{
  "aam-hierarchy": {
    "_xdm.context.segmentdefinition": [
      {
        "isFolder": true,
        "id": "100023",
        "name": "Segment Definition 1",
        "description": "Sample description.",
        "parentFolderId": "99970"
      },
      {
        "isFolder": false,
        "id": "1000028",
        "name": "Segment Definition 2",
        "description": "Sample description.",
        "parentFolderId": "103584"
      }
    ]
  },
  "page": {
    "totalCount": 2,
    "totalPages": 1,
    "pageOffset": "1",
    "pageSize": 2,
    "limit": 2
  }
}
```

### Criar solicitações de provisionamento

Você pode criar solicitações de provisionamento para ativar a pesquisa de Perfis em schemas, fazendo uma solicitação POST ao `/search/provisioning/component/init` endpoint.

**Solicitação**

>[!CAUTION]
>Essa solicitação POST não contém uma carga e, portanto, não requer um cabeçalho Content-Type. Além disso, não há cabeçalho Sandbox porque todos os dados são enviados para uma caixa de proteção global.

```shell
curl -X POST \
    https://platform.adobe.io/data/core/ups/search/provisioning/component/init \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' 
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 201 (Criado) e a seguinte mensagem:

```plaintext
The request has been fulfilled and resulted in a new resource being created.
```

### Processar solicitações de configuração

O ponto de extremidade de configuração pode ser usado para configurar os índices, os indexadores e as conexões de fonte de dados apropriados para uma nova Organização IMS. Duas propriedades são necessárias para lidar com solicitações de configuração: `databaseName` e `containerName`.

`databaseName` representa o nome do banco de dados de Perfis da organização que será configurada.

`containerName` representa o nome do container preenchido por um conector de dados, que é o que é lido durante a configuração. Há dois valores para `containerName`, um ou ambos podem ser usados na solicitação POST:
- `_xdm.content.segmentdefinition`
- `_experience.audiencemanager.segmentfolder`

### Criar uma solicitação de configuração

A chamada de API a seguir gera a fonte de dados, o indexador e o índice necessários com base nos parâmetros fornecidos na carga da solicitação.

**Formato da API**

```http
POST /search/configure
```

**Solicitação**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/search/configure \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "databaseName": {DATABASE_NAME},
    "containerName": "_xdm.context.segmentdefinition" "_experience.audiencemanager.segmentfolder"
  }'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 202 (Aceito) e uma mensagem de texto simples.

```plaintext
The request has been accepted for processing, but the processing has not been completed.
```

### Excluir uma solicitação de configuração

A chamada de API a seguir remove as entradas de índice correspondentes e exclui o indexador e a fonte de dados com base nos parâmetros fornecidos na carga da solicitação.

>[!NOTE]
>O índice em si não será excluído, pois é um recurso compartilhado.

**Formato da API**

```http
DELETE /search/configure
```

**Solicitação**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/ups/search/configure \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "databaseName": {DATABASE_NAME},
    "containerName": "_xdm.context.segmentdefinition" "_experience.audiencemanager.segmentfolder"
  }'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 202 (Aceito) e uma mensagem de texto simples.

```plaintext
The request has been accepted for processing, but the processing has not been completed.
```

## Próximas etapas

Depois de ler este guia, agora você tem uma melhor compreensão de como a pesquisa de Perfil do cliente em tempo real funciona. Para obter mais informações sobre o Perfil do cliente em tempo real, leia a visão geral [do Perfil do cliente em tempo](../home.md)real. Para obter mais informações sobre Segmentação, leia a visão geral [da](../../segmentation/home.md)Segmentação.

## Apêndice {#appendix}

### Parâmetros de pesquisa {#search-parameters}

A tabela a seguir lista as especificações de como o parâmetro de pesquisa funciona ao usar a API de pesquisa.

| Query de pesquisa | Descrição |
|------------ | -----------|
| foo | Procure qualquer palavra. Isso retornará os resultados se a palavra &quot;foo&quot; for encontrada em qualquer um dos campos pesquisáveis. |
| foo E barra | Uma pesquisa booleana. Isso retornará os resultados se **ambas** as palavras &quot;foo&quot; e &quot;barra&quot; forem encontradas em qualquer um dos campos pesquisáveis. |
| barra OU do rodapé | Uma pesquisa booleana. Isso retornará os resultados se **** a palavra &quot;foo&quot; ou a palavra &quot;barra&quot; forem encontradas em qualquer um dos campos pesquisáveis. |
| barra Foo NOT | Uma pesquisa booleana. Isso retornará os resultados se a palavra &quot;foo&quot; for encontrada, mas a palavra &quot;barra&quot; não for encontrada em nenhum dos campos pesquisáveis. |
| name: foo E barra | Uma pesquisa booleana. Isso retornará os resultados se **ambas** as palavras &quot;foo&quot; e &quot;bar&quot; forem encontradas no campo &quot;nome&quot;. |
| run* | Uma pesquisa curinga. Usar um asterisco (*) corresponde a 0 ou mais caracteres, o que significa que retornará resultados se o conteúdo de qualquer um dos campos pesquisáveis contiver uma palavra que seja start com &quot;executar&quot;. Por exemplo, isso retornará os resultados se as palavras &quot;executa&quot;, &quot;executa&quot;, &quot;runner&quot; ou &quot;runt&quot; forem exibidas. |
| cam? | Uma pesquisa curinga. Usando um ponto de interrogação (?) corresponde somente a exatamente um caractere, o que significa que retornará resultados se o conteúdo de qualquer um dos start de campos pesquisáveis for exibido com &quot;cam&quot; e uma letra adicional. Por exemplo, isso retornará os resultados se as palavras &quot;acampamento&quot; ou &quot;cams&quot; forem exibidas, mas não retornará os resultados se as palavras &quot;câmera&quot; ou &quot;fogueira&quot; forem exibidas. |
| &quot;guarda-chuva azul&quot; | Uma pesquisa de frases. Isso retornará os resultados se o conteúdo de qualquer um dos campos pesquisáveis contiver a frase completa &quot;guarda-chuva azul&quot;. |
| azul\~ | Uma busca indistinta. Opcionalmente, você pode colocar um número entre 0 e 2 após o til (~) para especificar a distância de edição. Por exemplo, &quot;azul\~1&quot; seria &quot;azul&quot;, &quot;azul&quot; ou &quot;cola&quot;. A pesquisa indistinta **só** pode ser aplicada a termos, não a frases. Entretanto, é possível anexar tildes ao final de cada palavra em uma frase. Assim, por exemplo, &quot;acampando\~ em\~ o\~ verão\~&quot; corresponderia a &quot;acampamento no verão&quot;. |
| &quot;aeroporto de hotel&quot;\~5 | Uma busca de proximidade. Esse tipo de pesquisa é usado para encontrar termos próximos uns dos outros em um documento. Por exemplo, a frase `"hotel airport"~5` encontrará os termos &quot;hotel&quot; e &quot;aeroporto&quot; em até 5 palavras entre si em um documento. |
| `/a[0-9]+b$/` | Uma pesquisa de expressão regular. Esse tipo de pesquisa encontra uma correspondência com base no conteúdo entre barras iniciais &quot;/&quot;, conforme documentado na classe RegExp. Por exemplo, para localizar documentos contendo &quot;motel&quot; ou &quot;hotel&quot;, especifique `/[mh]otel/`. Pesquisas expressões regulares são comparadas com palavras únicas. |

Para obter uma documentação mais detalhada sobre a sintaxe do query, leia a documentação [da sintaxe do query](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax)Lucene.
