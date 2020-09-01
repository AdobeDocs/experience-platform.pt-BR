---
keywords: Experience Platform;segmentation;segmentation service;troubleshooting;API;seg;segment;Segment;search;segment search;
solution: Adobe Experience Platform
title: Ponto de extremidade de pesquisa de segmento
topic: guide
description: A Pesquisa de segmento é usada para pesquisar campos contidos em várias fontes de dados e retorná-los em tempo quase real. Este guia fornece informações para ajudá-lo a entender melhor a Pesquisa de segmentos e inclui exemplos de chamadas de API para executar ações básicas usando a API.
translation-type: tm+mt
source-git-commit: 17ef6c1c6ce58db2b65f1769edf719b98d260fc6
workflow-type: tm+mt
source-wordcount: '1179'
ht-degree: 2%

---


# Ponto de extremidade de Pesquisa de segmento

A Pesquisa de segmento é usada para pesquisar campos contidos em várias fontes de dados e retorná-los em tempo quase real.

Este guia fornece informações para ajudá-lo a entender melhor a Pesquisa de segmentos e inclui exemplos de chamadas de API para executar ações básicas usando a API.

## Introdução

Os pontos de extremidade usados neste guia fazem parte da [!DNL Adobe Experience Platform Segmentation Service] API. Antes de continuar, consulte o guia [de](./getting-started.md) introdução para obter informações importantes que você precisa saber para fazer chamadas à API com sucesso, incluindo cabeçalhos necessários e como ler chamadas de exemplo de API.

Além dos cabeçalhos necessários descritos na seção de introdução, todas as solicitações ao terminal de Pesquisa de segmento exigem o seguinte cabeçalho adicional:

- x-ups-search-version: &quot;1.0&quot;

### Pesquisar em várias namespaces

Esse ponto de extremidade de pesquisa pode ser usado para pesquisar por várias namespaces, retornando uma lista de resultados de contagem de pesquisa. Vários parâmetros podem ser usados, separados por E comercial (&amp;).

**Formato da API**

```http
GET /search/namespaces?schema.name={SCHEMA}
GET /search/namespaces?schema.name={SCHEMA}&s={SEARCH_TERM}
```

| Parâmetros | Descrição |
| ---------- | ----------- | 
| `schema.name={SCHEMA}` | **(Obrigatório)** Em que {SCHEMA} representa o valor da classe do schema associado aos objetos de pesquisa. Atualmente, somente `_xdm.context.segmentdefinition` é suportado. |
| `s={SEARCH_TERM}` | *(Opcional)* Onde {SEARCH_TERM} representa um query que está em conformidade com a implementação da Microsoft da sintaxe [de pesquisa de](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax)Lucene. Se nenhum termo de pesquisa for especificado, todos os registros associados `schema.name` serão retornados. O [apêndice](#appendix) deste documento contém uma explicação mais detalhada. |

**Solicitação**

```shell
curl -X GET \
    https://platform.adobe.io/data/core/ups/search/namespaces?schema.name=_xdm.context.segmentdefinition \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'x-ups-search-version: 1.0' 
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com as seguintes informações.

```json
{
  "namespaces": [
    {
      "namespace": "AAMTraits",
      "displayName": "AAMTraits",
      "count": 45
    },
    {
      "namespace": "AAMSegments",
      "displayName": "AAMSegment",
      "count": 10
    },
    {
      "namespace": "SegmentsAISegments",
      "displayName": "SegmentSAISegment",
      "count": 3
    }
  ],
  "totalCount": 3,
  "status": {
    "message": "Success"
  }
}
```

### Pesquisar entidades individuais

Esse ponto de extremidade de pesquisa pode ser usado para recuperar uma lista de todos os objetos indexados de texto completo dentro da namespace especificada. Vários parâmetros podem ser usados, separados por E comercial (&amp;).

**Formato da API**

```http
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}&s={SEARCH_TERM}
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}&entityId={ENTITY_ID}
```

| Parâmetros | Descrição |
| ---------- | ----------- | 
| `schema.name={SCHEMA}` | **(Obrigatório)** Onde {SCHEMA} contém o valor da classe do schema associado aos objetos de pesquisa. Atualmente, somente `_xdm.context.segmentdefinition` é suportado. |
| `namespace={NAMESPACE}` | **(Obrigatório)** Onde {NAMESPACE} contém a namespace na qual você deseja pesquisar. |
| `s={SEARCH_TERM}` | *(Opcional)* Onde {SEARCH_TERM} contém um query que está em conformidade com a implementação da Microsoft da sintaxe [de pesquisa de](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax)Lucene. Se nenhum termo de pesquisa for especificado, todos os registros associados `schema.name` serão retornados. O [apêndice](#appendix) deste documento contém uma explicação mais detalhada. |
| `entityId={ENTITY_ID}` | *(Opcional)* Limita sua pesquisa à pasta designada, especificada com {ENTITY_ID}. |
| `limit={LIMIT}` | *(Opcional)* Onde {LIMIT} representa o número de resultados de pesquisa a serem retornados. O valor padrão é 50. |
| `page={PAGE}` | *(Opcional)* Onde {PAGE} representa o número de página usado para paginar os resultados do query pesquisado. Observe que o número de página start em **0**. |


**Solicitação**

```shell
curl -X GET \
    https://platform.adobe.io/data/core/ups/search/entities?schema.name=_xdm.context.segmentdefinition&namespace=AAMSegments \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'x-ups-search-version: 1.0' 
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com resultados que correspondem ao query de pesquisa.

```json
{
  "entities": [
    {
       "id": "1012667",
       "base64EncodedSourceId": "RFVGamdydHpEdy01ZTE1ZGJlZGE4YjAxMzE4YWExZWY1MzM1",
       "sourceId": "DUFjgrtzDw-5e15dbeda8b01318aa1ef533",
       "isFolder": true,
       "parentFolderId": "974139",
       "name": "aam-47995 verification (100)"
    },
    {
       "id": "14653311",
       "base64EncodedSourceId": "REVGamduLVgzdy01ZTE2ZjRhNjc1ZDZhMDE4YThhZDM3NmY1",
       "sourceId": "DEFjgn-X3w-5e16f4a675d6a018a8ad376f",
       "isFolder": false,
       "parentFolderId": "324050",
       "name": "AAM - Heavy equipment",
       "description": "AAM - Acme Equipment"
    }
 
 ],
  "page": {
    "totalCount": 2,
    "totalPages": 1,
    "pageOffset": 0,
    "pageSize": 10
  },
  "status": {
    "message": "Success"
  }
}
```

### Obter informações estruturais sobre um objeto de pesquisa

Esse terminal de pesquisa pode ser usado para obter informações estruturais sobre o objeto de pesquisa solicitado.

**Formato da API**

```http
GET /search/taxonomy?schema.name={SCHEMA}&namespace={NAMESPACE}&entityId={ENTITY_ID}
```

| Parâmetros | Descrição |
| ---------- | ----------- | 
| `schema.name={SCHEMA}` | **(Obrigatório)** Onde {SCHEMA} contém o valor da classe do schema associado aos objetos de pesquisa. Atualmente, somente `_xdm.context.segmentdefinition` é suportado. |
| `namespace={NAMESPACE}` | **(Obrigatório)** Onde {NAMESPACE} contém a namespace na qual você deseja pesquisar. |
| `entityId={ENTITY_ID}` | **(Obrigatório)** A ID do objeto de pesquisa sobre o qual você deseja obter as informações estruturais, especificadas com {ENTITY_ID}. |

**Solicitação**

```shell
curl -X GET \
    https://platform.adobe.io/data/core/ups/search/taxonomy?schema.name=_xdm.context.segmentdefinition&namespace=AAMSegments&entityId=porsche11037 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'x-ups-search-version: 1.0' 
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com informações estruturais detalhadas sobre o objeto de pesquisa solicitado.

```json
{
    "taxonomy": [
        {
            "id": "0",
            "base64EncodedSourceId": "RFVGZ01BLTVlNjgzMGZjMzk3YjQ1MThhYWExYTA4Zg2",
            "name": "AAMTraits for Cars",
            "parentFolderId": "root"
        },
        {
            "id": "150561",
            "base64EncodedSourceId": "RFVGamdpRk1BZy01ZTY4MzBmYzM5N2I0NTE4YWFhMWEwOGY1",
            "name": "Fast Cars",
            "parentFolderId": "carTraits"
        },
        {
            "id": "porsche11037",
            "base64EncodedSourceId": "REFGZ01CLTVlNjczMGZjMzk3YjQ1MThhZGIxYTA4Zg==",
            "name": "Porsche",
            "parentFolderId": "redCarsFolderId"
        }
    ],
    "status": {
        "message": "Success"
    }
}
```

## Próximas etapas

Depois de ler este guia, agora você tem uma melhor compreensão de como a Pesquisa de segmentos funciona.

## Apêndice {#appendix}

As seções a seguir fornecem informações adicionais sobre como os termos de pesquisa funcionam. Os query de pesquisa são escritos da seguinte maneira: `s={FieldName}:{SearchExpression}`. Assim, por exemplo, para pesquisar por um segmento chamado AAM ou [!DNL Platform], você usaria o seguinte query de pesquisa: `s=segmentName:AAM%20OR%20Platform`.

> !![NOTE] Para práticas recomendadas, a expressão de pesquisa deve ser codificada em HTML, como o exemplo mostrado acima.

### Campos de pesquisa {#search-fields}

A tabela a seguir lista os campos que podem ser pesquisados dentro do parâmetro do query de pesquisa.

| Nome do campo | Descrição |
| ---------- | ----------- |
| folderId | A pasta ou pastas que têm a ID da pasta da pesquisa especificada. |
| folderLocation | O local ou locais que têm o local da pasta da pesquisa especificada. |
| parentFolderId | O segmento ou pasta que tem a ID da pasta pai da pesquisa especificada. |
| segmentId | O segmento corresponde à ID do segmento da pesquisa especificada. |
| segmentName | O segmento corresponde ao nome do segmento da pesquisa especificada. |
| segmentDescription | O segmento corresponde à descrição do segmento de sua pesquisa especificada. |

### Expressão de pesquisa {#search-expression}

A tabela a seguir lista os detalhes de como os query de pesquisa funcionam ao usar a API de pesquisa de segmento.

>!![NOTE] Os exemplos a seguir são mostrados em um formato não codificado em HTML para maior clareza. Para as práticas recomendadas, o HTML codifica sua expressão de pesquisa.

| Exemplo de expressão de pesquisa | Descrição |
| ------------------------- | ----------- |
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
