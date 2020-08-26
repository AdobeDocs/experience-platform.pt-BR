---
keywords: Experience Platform;getting started;content ai;commerce ai;content and commerce ai;keyword extraction;Keyword extraction
solution: Experience Platform
title: Extração de cores
topic: Developer guide
description: O serviço de extração de palavra-chave, quando recebe um documento de texto, extrai automaticamente palavras-chave ou frases-chave que melhor descrevem o assunto do documento. Para extrair palavras-chave, é usada uma combinação de algoritmos de reconhecimento de entidade nomeada (NER) e de extração de palavra-chave não supervisionada.
translation-type: tm+mt
source-git-commit: 690ddbd92f0a2e4e06b988e761dabff399cd2367
workflow-type: tm+mt
source-wordcount: '742'
ht-degree: 3%

---


# Extração de palavra-chave

>[!NOTE]
>
>[!DNL Content and Commerce AI] está em beta. A documentação está sujeita a alterações.

O serviço de extração de palavra-chave, quando recebe um documento de texto, extrai automaticamente palavras-chave ou frases-chave que melhor descrevem o assunto do documento. Para extrair palavras-chave, é usada uma combinação de algoritmos de reconhecimento de entidade nomeada (NER) e de extração de palavra-chave não supervisionada.

**Extração de palavra-chave não supervisionada**

Para extração de palavra-chave não supervisionada, é usado [[!DNL YAKE]](http://yake.inesctec.pt/) . [!DNL YAKE] é um método rápido e preciso de extração automática de palavra-chave sem supervisão usado para selecionar as palavras-chave mais importantes de um documento. As [!DNL YAKE] extrações de palavras-chave são filtradas para selecionar somente frases substantivas.

**Reconhecimento de entidade nomeada**

Para reconhecimento de entidade nomeada, é usado o modelo OntoNotes de [[!DNL spaCy]](https://spacy.io/). Esse modelo atribui vetores de token específicos do contexto, tags de parte da fala (POS), análise de dependência e entidades nomeadas. O modelo do OntoNotes é um dos [!DNL spaCy] modelos principais. Mais informações sobre o modelo do OntoNotes podem ser encontradas [aqui](https://spacy.io/models/en).

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

Os resultados de [!DNL OntoNotes] são combinados com as palavras-chave de [!DNL YAKE], e são retornados em ordem classificada de acordo com sua importância.

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

## Apêndice {#appendix}

A tabela a seguir contém os parâmetros disponíveis que podem ser utilizados de dentro `custom`.

| Nome | Descrição | Obrigatório |
| --- | --- | --- |
| `min-n` | O número mínimo de palavras necessárias nas palavras-chave. | Não |
| `entity-types` | Tipos de entidades a serem devolvidas. Consulte a tabela de reconhecimento de entidade nomeada no início deste documento. | Não |