---
keywords: Experience Platform;getting started;content ai;commerce ai;content and commerce ai;keyword extraction;Keyword extraction
solution: Experience Platform
title: Extração de cores
topic: Developer guide
description: O serviço de extração de palavra-chave, quando recebe um documento de texto, extrai automaticamente palavras-chave ou frases-chave que melhor descrevem o assunto do documento. Para extrair palavras-chave, é usada uma combinação de algoritmos de reconhecimento de entidade nomeada (NER) e de extração de palavra-chave não supervisionada.
translation-type: tm+mt
source-git-commit: eb92a7d57b1ef0ca19bc2d175ad1b2014ac1a8b0
workflow-type: tm+mt
source-wordcount: '1059'
ht-degree: 3%

---


# Extração de palavra-chave

>[!NOTE]
>
>[!DNL Content and Commerce AI] está em beta. A documentação está sujeita a alterações.

O serviço de extração de palavra-chave, quando recebe um documento de texto, extrai automaticamente palavras-chave ou frases-chave que melhor descrevem o assunto do documento. Para extrair palavras-chave, é usada uma combinação de algoritmos de reconhecimento de entidade nomeada (NER) e de extração de palavra-chave não supervisionada.

As entidades nomeadas reconhecidas por [!DNL Content and Commerce AI] estão listadas na seguinte tabela:

| Nome da entidade | Descrição |
| --- | --- |
| PESSOA | Pessoas, incluindo ficção. |
| NORP | Nacionalidades ou grupos religiosos ou políticos. |
| GPE | Países, cidades e estados. |
| LOC | Locais não-GPE, cadeias montanhosas, massas de água. |
| FAC | Edifícios, aeroportos, autoestradas, pontes, etc. |
| ORG | Empresas, agências, instituições, etc. |
| PRODUTO | Objetos, veículos, alimentos, etc. (Não serviços.) |
| EVENTO | Furacões, batalhas, guerras, eventos esportivos etc. |
| WORK_OF_ART | Títulos de livros, canções, etc. |
| LEI | Documentos nomeados transforma-se em leis. |
| IDIOMA | Qualquer idioma nomeado. |

>[!NOTE]
>
>Se você planeja processar PDFs, pule para as instruções de extração [de palavra-chave](#pdf-extraction) PDF neste documento. Além disso, o suporte para tipos de arquivos adicionais, como docx, ppt, amd xml, está definido para ser lançado em uma data posterior.

**Formato da API**

```http
POST /services/v1/predict
```

**Solicitação**

A solicitação a seguir extrai palavras-chave de um documento com base nos parâmetros de entrada fornecidos na carga.

JSON simplificado do arquivo de entrada:

```json
{
  "application-id": "1234",
  "language": "en",
  "content-type": "inline",
  "encoding": "utf-8",
  "threshold": 0.01,
  "top-N": 10,
  "custom": {
    "min-n": 2,
    "entity-types": ["PERSON"]
  },
  "data": [
    {
      "content-id": "abc123",
      "content": "But an influential faction on the ATP player council, which is chaired by Novak Djokovic, staged a rebellion against Kermodes regime in the spring, and he will leave the post on Dec 31"
    }
  ]
}
```

Consulte a tabela abaixo do exemplo de carga para obter mais informações sobre os parâmetros de entrada mostrados.

>[!CAUTION]
>
>`analyzer_id` determina qual [!DNL Sensei Content Framework] é usado. Verifique se você tem o direito `analyzer_id` antes de fazer sua solicitação. Para o serviço de extração de palavra-chave, a `analyzer_id` ID é:
>`Feature:cintel-ner:Service-1a35aefb0f0f4dc0a3b5262370ebc709`

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v1/predict \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Content-Type: multipart/form-data" \
  -H "cache-control: no-cache,no-cache" \
  -H "x-api-key: {API_KEY}" \
  -F file="{
    \"application-id\": \"1234\", 
    \"language\": \"en\", 
    \"content-type\": \"inline\", 
    \"encoding\": \"utf-8\",
    \"threshold\": 0.01,
    \"top-N\": 10,
    \"custom\": {
        \"min-n\": 2,
        \"entity-types\": [\"PERSON\"]
      },
    \"data\": [{
      \"content-id\": \"abc123\", 
      \"content\": \"But an influential faction on the ATP player council, which is chaired by Novak Djokovic, staged a rebellion against Kermodes regime in the spring, and he will leave the post on Dec 31\"
      }]
    }" \
  -F 'contentAnalyzerRequests={
    "enable_diagnostics":"true",
    "requests":[{
         "analyzer_id": "Feature:cintel-ner:Service-1a35aefb0f0f4dc0a3b5262370ebc709",
         "parameters": {}
    }]
}'
```

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| `analyzer_id` | A ID de [!DNL Sensei] serviço em que sua solicitação é implantada. Essa ID determina qual dos [!DNL Sensei Content Frameworks] é usada. Para serviços personalizados, entre em contato com a equipe do AI de Conteúdo e Comércio para configurar uma ID personalizada. | Sim |
| `application-id` | A ID do aplicativo criado. | Sim |
| `data` | Uma matriz que contém um objeto JSON com cada objeto na matriz que representa um documento. Todos os parâmetros transmitidos como parte dessa matriz substituem os parâmetros globais especificados fora da `data` matriz. Qualquer uma das propriedades restantes descritas abaixo nesta tabela pode ser substituída de dentro `data`. | Sim |
| `language` | Idioma do texto de entrada. O valor padrão é `en`. | Não |
| `content-type` | Usado para indicar se a entrada é parte do corpo da solicitação ou um url assinado para um bucket S3. O padrão para essa propriedade é `inline`. | Sim |
| `encoding` | O formato de codificação do texto de entrada. Isso pode ser `utf-8` ou `utf-16`. O padrão para essa propriedade é `utf-8`. | Não |
| `threshold` | O limite de pontuação (0 a 1) acima do qual os resultados precisam ser retornados. Use o valor `0` para retornar todos os resultados. O padrão para essa propriedade é `0`. | Não |
| `top-N` | O número de resultados a serem retornados (não pode ser um número inteiro negativo). Use o valor `0` para retornar todos os resultados. Quando usado em conjunto com `threshold`, o número de resultados retornados é o menor dos dois limites definidos. O padrão para essa propriedade é `0`. | Não |
| `custom` | Quaisquer parâmetros personalizados a serem transmitidos. Essa propriedade requer um objeto JSON válido para funcionar. Consulte o [apêndice](#appendix) para obter mais informações sobre os parâmetros personalizados. | Não |
| `content-id` | A ID exclusiva do elemento de dados retornado na resposta. Se isso não for passado, uma ID gerada automaticamente será atribuída. | Não |
| `content` | O conteúdo usado pelo serviço de extração de palavra-chave. O conteúdo pode ser texto bruto (tipo de conteúdo &quot;em linha&quot;). <br> Se o conteúdo for um arquivo em S3 (tipo de conteúdo &quot;s3-bucket&quot;), passe o url assinado. Quando o conteúdo faz parte do corpo da solicitação, a lista de elementos de dados deve ter apenas um objeto. Se mais de um objeto for transmitido, somente o primeiro objeto será processado. | Sim |

**Resposta**

Uma resposta bem-sucedida retorna um objeto JSON que contém palavras-chave extraídas na `response` matriz.

```json
{
  "status": 200,
  "cas_responses": [
    {
      "status": 200,
      "analyzer_id": "Feature:cintel-ner:Service-1a35aefb0f0f4dc0a3b5262370ebc709",
      "content_id": "",
      "result": {
        "response_type": "feature",
        "response": [
          {
            "feature_value": [
              {
                "feature_value": "success",
                "feature_name": "status"
              },
              {
                "feature_name": "labels",
                "feature_value": [
                  {
                    "feature_name": "atp player",
                    "feature_value": [
                      {
                        "feature_value": "KEYWORD",
                        "feature_name": "type"
                      },
                      {
                        "feature_value": 0.007743432063478832,
                        "feature_name": "score"
                      }
                    ]
                  },
                  {
                    "feature_name": "Novak Djokovic",
                    "feature_value": [
                      {
                        "feature_name": "type",
                        "feature_value": "PERSON"
                      },
                      {
                        "feature_name": "score",
                        "feature_value": 0
                      }
                    ]
                  },
                  {
                    "feature_value": [
                      {
                        "feature_name": "type",
                        "feature_value": "KEYWORD"
                      },
                      {
                        "feature_value": 0.00899321792126428,
                        "feature_name": "score"
                      }
                    ],
                    "feature_name": "player council"
                  },
                  {
                    "feature_value": [
                      {
                        "feature_value": "KEYWORD",
                        "feature_name": "type"
                      },
                      {
                        "feature_value": 0.007743432063478832,
                        "feature_name": "score"
                      }
                    ],
                    "feature_name": "kermodes regime"
                  },
                  {
                    "feature_value": [
                      {
                        "feature_name": "type",
                        "feature_value": "KEYWORD"
                      },
                      {
                        "feature_name": "score",
                        "feature_value": 0.0006052376660884209
                      }
                    ],
                    "feature_name": "atp player council"
                  }
                ]
              }
            ],
            "feature_name": "abc123"
          }
        ]
      }
    }
  ],
  "error": []
}
```

## EXTRAÇÃO de palavra-chave PDF {#pdf-extraction}

O serviço de extração de palavras-chave oferece suporte a PDFs, no entanto, é necessário usar uma nova Analyzer ID para arquivos PDF e alterar o tipo de documento para PDF. Consulte o exemplo abaixo para obter mais informações.

**Formato da API**

```http
POST /services/v1/predict
```

**Solicitação**

A solicitação a seguir extrai palavras-chave de um documento PDF com base nos parâmetros de entrada fornecidos na carga.

>[!CAUTION]
>
>`analyzer_id` determina qual [!DNL Sensei Content Framework] é usado. Verifique se você tem o direito `analyzer_id` antes de fazer sua solicitação. Para a extração de palavra-chave PDF, a `analyzer_id` ID é:
>`Feature:cintel-ner:Service-7a87cb57461345c280b62470920bcdc5`

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v1/predict \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Content-Type: multipart/form-data" \
  -H "cache-control: no-cache,no-cache" \
  -H "x-api-key: {API_KEY}" \
  -F file=@TestPDF.pdf \
  -F 'contentAnalyzerRequests={
    "enable_diagnostics":"true",
    "requests":[{
    "analyzer_id": "Feature:cintel-ner:Service-7a87cb57461345c280b62470920bcdc5",
    "parameters": {
      "application-id": "1234",
      "content-type": "file",
      "encoding": "pdf",
      "threshold": "0.01",
      "top-N": "0",
      "custom": {},
      "data": [{
        "content-id": "abc123",
        "content": "file",
        }]
      }
    }]
  }'
```

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| `analyzer_id` | A ID de [!DNL Sensei] serviço em que sua solicitação é implantada. Essa ID determina qual dos [!DNL Sensei Content Frameworks] é usada. Para serviços personalizados, entre em contato com a equipe do AI de Conteúdo e Comércio para configurar uma ID personalizada. | Sim |
| `application-id` | A ID do aplicativo criado. | Sim |
| `data` | Uma matriz que contém um objeto JSON com cada objeto na matriz que representa um documento. Todos os parâmetros transmitidos como parte dessa matriz substituem os parâmetros globais especificados fora da `data` matriz. Qualquer uma das propriedades restantes descritas abaixo nesta tabela pode ser substituída de dentro `data`. | Sim |
| `language` | Idioma de entrada. The default value is `en` (english). | Não |
| `content-type` | Usado para indicar o tipo de conteúdo de entrada. Isto deve ser definido como `file`. | Sim |
| `encoding` | O formato de codificação da entrada. Isto deve ser definido como `pdf`. Mais tipos de codificação estão definidos para serem suportados em uma data posterior. | Sim |
| `threshold` | O limite de pontuação (0 a 1) acima do qual os resultados precisam ser retornados. Use o valor `0` para retornar todos os resultados. O padrão para essa propriedade é `0`. | Não |
| `top-N` | O número de resultados a serem retornados (não pode ser um número inteiro negativo). Use o valor `0` para retornar todos os resultados. Quando usado em conjunto com `threshold`, o número de resultados retornados é o menor dos dois limites definidos. O padrão para essa propriedade é `0`. | Não |
| `custom` | Quaisquer parâmetros personalizados a serem transmitidos. Essa propriedade requer um objeto JSON válido para funcionar. Consulte o [apêndice](#appendix) para obter mais informações sobre os parâmetros personalizados. | Não |
| `content-id` | A ID exclusiva do elemento de dados retornado na resposta. Se isso não for passado, uma ID gerada automaticamente será atribuída. | Não |
| `content` | Isto deve ser definido como `file`. | Sim |

**Resposta**

Uma resposta bem-sucedida retorna um objeto JSON que contém palavras-chave extraídas na `response` matriz.

```json
{
  "statusCode": 200,
  "body": {
    "type": "JSON",
    "matchType": "strict",
    "json": {
      "status": 200,
      "content_id": "161hw2.pdf",
      "cas_responses": [
        {
          "status": 200,
          "analyzer_id": "Feature:cintel-ner:Service-7a87cb57461345c280b62470920bcdc5",
          "content_id": "161hw2.pdf",
          "result": {
            "response_type": "feature",
            "response": [
              {
                "feature_value": [
                  {
                    "feature_name": "status",
                    "feature_value": "success"
                  },
                  {
                    "feature_value": [
                      {
                        "feature_name": "delbick",
                        "feature_value": [
                          {
                            "feature_name": "score",
                            "feature_value": 0.03673855028832046
                          },
                          {
                            "feature_name": "type",
                            "feature_value": "KEYWORD"
                          }
                        ]
                      },
                      {
                        "feature_name": "Ci",
                        "feature_value": [
                          {
                            "feature_name": "score",
                            "feature_value": 0
                          },
                          {
                            "feature_name": "type",
                            "feature_value": "PERSON"
                          }
                        ]
                      }
                    ],
                    "feature_name": "labels"
                  }
                ],
                "feature_name": "abc123"
              }
            ]
          }
        }
      ],
      "error": []
    }
  }
}
```

Para obter mais informações e um exemplo sobre como usar a extração PDF que contém instruções sobre como configurar, implantar e integrar com o serviço de nuvem AEM. Visite o repositório [github do funcionário da extração PDF](https://github.com/adobe/asset-compute-example-workers/tree/master/projects/worker-ccai-pdfextract)CCI.

## Apêndice {#appendix}

A tabela a seguir contém os parâmetros disponíveis que podem ser utilizados de dentro `custom`.

| Nome | Descrição | Obrigatório |
| --- | --- | --- |
| `min-n` | O número mínimo de palavras necessárias nas palavras-chave. | Não |
| `entity-types` | Tipos de entidades a serem devolvidas. Consulte a tabela de reconhecimento de entidade nomeada no início deste documento. | Não |