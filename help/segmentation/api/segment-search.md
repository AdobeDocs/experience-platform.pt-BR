---
keywords: Experience Platform, segmentação, serviço de segmentação, solução de problemas, API, seg, segmento, segmento, pesquisa, pesquisa de segmento;
title: Endpoint da API de pesquisa de segmento
topic-legacy: guide
description: Na API do Serviço de segmentação da Adobe Experience Platform, a Pesquisa de segmento é usada para pesquisar campos contidos em várias fontes de dados e retorná-los em tempo quase real. Este guia fornece informações para ajudá-lo a entender melhor a Pesquisa de segmento e inclui exemplos de chamadas de API para executar ações básicas usando a API.
exl-id: bcafbed7-e4ae-49c0-a8ba-7845d8ad663b
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1201'
ht-degree: 2%

---

# Ponto de extremidade de Pesquisa de Segmento

A Pesquisa de segmento é usada para pesquisar campos contidos em várias fontes de dados e retorná-los em tempo quase real.

Este guia fornece informações para ajudá-lo a entender melhor a Pesquisa de segmento e inclui exemplos de chamadas de API para executar ações básicas usando a API.

## Introdução

Os endpoints usados neste guia fazem parte da API [!DNL Adobe Experience Platform Segmentation Service]. Antes de continuar, reveja o [guia de introdução](./getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas para a API com êxito, incluindo cabeçalhos necessários e como ler chamadas de API de exemplo.

Além dos cabeçalhos necessários descritos na seção de introdução, todas as solicitações para o endpoint de Pesquisa de segmento exigem o seguinte cabeçalho adicional:

- x-ups-search-version: &quot;1.0&quot;

### Pesquisar em vários namespaces

Esse endpoint de pesquisa pode ser usado para pesquisar em vários namespaces, retornando uma lista de resultados de contagem de pesquisa. Vários parâmetros podem ser usados, separados por &quot;E&quot; comercial (&amp;).

**Formato da API**

```http
GET /search/namespaces?schema.name={SCHEMA}
GET /search/namespaces?schema.name={SCHEMA}&s={SEARCH_TERM}
```

| Parâmetros | Descrição |
| ---------- | ----------- | 
| `schema.name={SCHEMA}` | **(Obrigatório)** Onde {SCHEMA} representa o valor da classe de esquema associado aos objetos de pesquisa. Atualmente, somente `_xdm.context.segmentdefinition` é suportado. |
| `s={SEARCH_TERM}` | *(Opcional)* Onde {SEARCH_TERM} representa uma consulta que está em conformidade com a implementação da Microsoft da sintaxe de pesquisa do  [Lucene](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax). Se nenhum termo de pesquisa for especificado, todos os registros associados a `schema.name` serão retornados. Uma explicação mais detalhada pode ser encontrada no [apêndice](#appendix) deste documento. |

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

Esse endpoint de pesquisa pode ser usado para recuperar uma lista de todos os objetos indexados de texto completo dentro do namespace especificado. Vários parâmetros podem ser usados, separados por &quot;E&quot; comercial (&amp;).

**Formato da API**

```http
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}&s={SEARCH_TERM}
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}&entityId={ENTITY_ID}
```

| Parâmetros | Descrição |
| ---------- | ----------- | 
| `schema.name={SCHEMA}` | **(Obrigatório)** Onde {SCHEMA} contém o valor da classe de esquema associado aos objetos de pesquisa. Atualmente, somente `_xdm.context.segmentdefinition` é suportado. |
| `namespace={NAMESPACE}` | **(Obrigatório)** Onde {NAMESPACE} contém o namespace no qual você deseja pesquisar. |
| `s={SEARCH_TERM}` | *(Opcional)* Onde {SEARCH_TERM} contém uma consulta que está em conformidade com a implementação da Microsoft da sintaxe de pesquisa do  [Lucene](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax). Se nenhum termo de pesquisa for especificado, todos os registros associados a `schema.name` serão retornados. Uma explicação mais detalhada pode ser encontrada no [apêndice](#appendix) deste documento. |
| `entityId={ENTITY_ID}` | *(Opcional)* Limita sua pesquisa para dentro da pasta designada, especificada com {ENTITY_ID}. |
| `limit={LIMIT}` | *(Opcional)* Onde {LIMIT} representa o número de resultados de pesquisa a serem retornados. O valor padrão é 50. |
| `page={PAGE}` | *(Opcional)* Onde {PAGE} representa o número de página usado para paginar resultados da consulta pesquisada. Observe que o número da página começa em **0**. |


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

Uma resposta bem-sucedida retorna o status HTTP 200 com resultados correspondentes à consulta de pesquisa.

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

Esse endpoint de pesquisa pode ser usado para obter as informações estruturais sobre o objeto de pesquisa solicitado.

**Formato da API**

```http
GET /search/taxonomy?schema.name={SCHEMA}&namespace={NAMESPACE}&entityId={ENTITY_ID}
```

| Parâmetros | Descrição |
| ---------- | ----------- | 
| `schema.name={SCHEMA}` | **(Obrigatório)** Onde {SCHEMA} contém o valor da classe de esquema associado aos objetos de pesquisa. Atualmente, somente `_xdm.context.segmentdefinition` é suportado. |
| `namespace={NAMESPACE}` | **(Obrigatório)** Onde {NAMESPACE} contém o namespace no qual você deseja pesquisar. |
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

Após a leitura deste guia, você tem uma melhor compreensão de como a Pesquisa de segmento funciona.

## Apêndice {#appendix}

As seções a seguir fornecem informações adicionais sobre como os termos de pesquisa funcionam. As consultas de pesquisa são gravadas da seguinte maneira: `s={FieldName}:{SearchExpression}`. Assim, por exemplo, para procurar por um segmento chamado AAM ou [!DNL Platform], você usaria a seguinte consulta de pesquisa: `s=segmentName:AAM%20OR%20Platform`.

> !![NOTE] Para práticas recomendadas, a expressão de pesquisa deve ser codificada em HTML, como o exemplo mostrado acima.

### Pesquisar campos {#search-fields}

A tabela a seguir lista os campos que podem ser pesquisados no parâmetro de consulta de pesquisa.

| Nome do campo | Descrição |
| ---------- | ----------- |
| folderId | A pasta ou pastas que têm a ID da pasta da pesquisa especificada. |
| folderLocation | O local ou locais que têm o local da pasta da pesquisa especificada. |
| parentFolderId | O segmento ou a pasta que tem a ID da pasta principal da pesquisa especificada. |
| segmentId | O segmento corresponde à ID de segmento da pesquisa especificada. |
| segmentName | O segmento corresponde ao nome do segmento de sua pesquisa especificada. |
| segmentDescription | O segmento corresponde à descrição do segmento de sua pesquisa especificada. |

### Expressão de pesquisa {#search-expression}

A tabela a seguir lista as especificações de como as consultas de pesquisa funcionam ao usar a API de pesquisa de segmento.

>!![NOTE] Os exemplos a seguir são mostrados em um formato codificado que não seja HTML para maior clareza. Para práticas recomendadas, o HTML codifica sua expressão de pesquisa.

| Exemplo de expressão de pesquisa | Descrição |
| ------------------------- | ----------- |
| fofo | Procure qualquer palavra. Isso retornará resultados se a palavra &quot;foo&quot; for encontrada em qualquer um dos campos pesquisáveis. |
| foo E barra | Uma pesquisa booleana. Isso retornará resultados se **e** as palavras &quot;foo&quot; e &quot;bar&quot; forem encontradas em qualquer um dos campos pesquisáveis. |
| barra OU rodapé | Uma pesquisa booleana. Isso retornará resultados se **ou** a palavra &quot;foo&quot; ou a palavra &quot;bar&quot; forem encontradas em qualquer um dos campos pesquisáveis. |
| barra FOTO NÃO | Uma pesquisa booleana. Isso retornará resultados se a palavra &quot;foo&quot; for encontrada, mas a palavra &quot;bar&quot; não for encontrada em nenhum dos campos pesquisáveis. |
| name: foo E barra | Uma pesquisa booleana. Isso retornará resultados se **ambos** as palavras &quot;foo&quot; e &quot;bar&quot; forem encontradas no campo &quot;name&quot;. |
| executar* | Uma pesquisa curinga. Usar um asterisco (*) corresponde a 0 ou mais caracteres, o que significa que retornará resultados se o conteúdo de qualquer um dos campos pesquisáveis contiver uma palavra que começa com &quot;executar&quot;. Por exemplo, isso retornará resultados se as palavras &quot;executa&quot;, &quot;executando&quot;, &quot;runner&quot; ou &quot;runt&quot; forem exibidas. |
| câmara? | Uma pesquisa curinga. Usar um ponto de interrogação (?) corresponde somente a um caractere, o que significa que retornará resultados se o conteúdo de qualquer um dos campos pesquisáveis começar com &quot;cam&quot; e uma letra adicional. Por exemplo, isso retornará resultados se as palavras &quot;camp&quot; ou &quot;cams&quot; forem exibidas, mas não retornará resultados se as palavras &quot;câmera&quot; ou &quot;campfire&quot; forem exibidas. |
| &quot;guarda-chuva azul&quot; | Uma pesquisa de frase. Isso retornará resultados se o conteúdo de qualquer um dos campos pesquisáveis contiver a frase completa &quot;guarda-chuva azul&quot;. |
| azul\~ | Uma busca difusa. Como opção, você pode colocar um número entre 0 e 2 após o til (~) para especificar a distância de edição. Por exemplo, &quot;blue\~1&quot; retornaria &quot;blue&quot;, &quot;blues&quot; ou &quot;cola&quot;. A pesquisa difusa pode **somente** ser aplicada a termos, não a frases. No entanto, é possível anexar til ao final de cada palavra em uma frase. Por exemplo, &quot;acampar\~ em\~ no\~ verão\~&quot; seria igual a &quot;acampar no verão&quot;. |
| &quot;aeroporto de hotel&quot;\~5 | Uma pesquisa de proximidade. Esse tipo de pesquisa é usado para localizar termos próximos um do outro em um documento. Por exemplo, a frase `"hotel airport"~5` encontrará os termos &quot;hotel&quot; e &quot;aeroporto&quot; em até 5 palavras de distância em um documento. |
| `/a[0-9]+b$/` | Uma pesquisa de expressão regular. Esse tipo de pesquisa encontra uma correspondência com base no conteúdo entre barras para frente &quot;/&quot;, conforme documentado na classe RegExp. Por exemplo, para localizar documentos contendo &quot;motel&quot; ou &quot;hotel&quot;, especifique `/[mh]otel/`. Pesquisas de expressões regulares são comparadas com palavras únicas. |

Para obter uma documentação mais detalhada sobre a sintaxe de consulta, leia a [documentação da sintaxe de consulta do Lucene](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax).
