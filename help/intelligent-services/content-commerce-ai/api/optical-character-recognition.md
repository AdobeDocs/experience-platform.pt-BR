---
keywords: OCR;presença de texto;reconhecimento ótico de caracteres
solution: Experience Platform
title: Presença de Texto e Reconhecimento Óptico de Caracteres
description: Na API de marcação de conteúdo, o serviço de Presença de texto/Reconhecimento ótico de caracteres (OCR) pode indicar se o texto está presente em uma determinada imagem. Se houver texto, o OCR poderá retornar o texto.
exl-id: 85b976a7-0229-43e9-b166-cdbd213b867f
source-git-commit: b124ed97da8bde2a7fc4f10d350c81a47e096f29
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 4%

---

# Presença de Texto e Reconhecimento Óptico de Caracteres

O serviço de Presença de Texto/OCR (reconhecimento ótico de caracteres), quando recebe uma imagem, pode indicar se o texto está presente na imagem. Se houver texto, o OCR poderá retornar o texto.

A imagem a seguir foi usada no exemplo de solicitação mostrado neste documento:

![Imagem de exemplo](../images/sample_image.png)

**Formato da API**

```http
POST /services/v2/predict
```

**Solicitação**

A solicitação a seguir verifica se o texto está presente com base na imagem de entrada fornecida na carga. Consulte a tabela abaixo do exemplo de carga para obter mais informações sobre os parâmetros de entrada mostrados.

Execução com imagem integrada:

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v2/predict \
-H 'Prefer: respond-async, wait=59' \
-H "x-api-key: $API_KEY" \
-H "content-type: multipart/form-data" \
-H "authorization: Bearer $API_TOKEN" \
-F file=@sample_image.png \
-F 'contentAnalyzerRequests={
  "sensei:name": "Feature:cintel-object-detection:Service-b9ace8b348b6433e9e7d82371aa16690",
  "sensei:invocation_mode": "asynchronous",
  "sensei:invocation_batch": false,
  "sensei:engines": [
    {
      "sensei:execution_info": {
        "sensei:engine": "Feature:cintel-object-detection:Service-b9ace8b348b6433e9e7d82371aa16690"
      },
      "sensei:inputs": {
        "documents": [
        {
          "sensei:multipart_field_name": "file",
          "dc:format": "image/jpg"
        }
        ]
      },
      "sensei:params": {
        "correct_with_dictionary": true,
        "min_probability": 0.2,
        "min_relevance": 0.01,
        "filter_with_dictionary": true
      },
      "sensei:outputs":{
        "result" : {
          "sensei:multipart_field_name" : "result",
          "dc:format": "application/json"
        }
      }
    }
  ]
}'
```

**Resposta**

Uma resposta bem-sucedida retorna o texto que foi detectado na variável `tags` para cada imagem transmitida na solicitação. Se não houver texto em uma determinada imagem, `is_text_present` é 0 e `tags` é uma lista vazia.

[resultado0, resultado1, ...]: lista de respostas para cada documento de entrada. Cada resultado é um diretório com chaves:

1. request_element_id: índice correspondente ao arquivo de entrada para essa resposta, 0 para a primeira imagem na lista de documentos da solicitação, 1 para a próxima e assim por diante.
2. tags: lista de dicionários, cada dicionário tem duas chaves: texto, que é uma palavra reconhecida da imagem, e relevância, que é calculada como a fração da área da caixa delimitadora do texto extraído em comparação com a imagem completa. 0,01 seria traduzido como um texto que ocupa pelo menos 1% da imagem.
3. is_text_present: 0 ou 1 dependendo se o texto está presente na imagem. Se as tags forem 0, a lista estará vazia.

```json
{
  "contentAnalyzerResponse": {
    "statuses": [
      {
        "sensei:engine": "Feature:cintel-object-detection:Service-b9ace8b348b6433e9e7d82371aa16690",
        "invocations": [
          {
            "sensei:outputs": {
              "result": {
                "sensei:multipart_field_name": "result",
                "dc:format": "application/json"
              }
            },
            "message": null,
            "status": "200"
          }
        ]
      }
    ],
    "request_id": "dttklFR7DPtMtEmjlRSx5BYP5WGg3tTx"
  },
  "result": [
    {
      "is_text_present": 1,
      "tags": [
        {
          "text": "yosemite",
          "relevance": 0.05604639115920341
        }
      ],
      "request_element_id": 0
    }
  ]
}
```

**Solicitação**

A solicitação a seguir verifica se o texto está presente com base na imagem de entrada fornecida na carga. Consulte a tabela abaixo do exemplo de carga para obter mais informações sobre os parâmetros de entrada mostrados.

Execução com URL:

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v2/predict \
-H 'Prefer: respond-async, wait=59' \
-H "x-api-key: $API_KEY" \
-H "content-type: multipart/form-data" \
-H "authorization: Bearer $API_TOKEN" \
-F 'contentAnalyzerRequests={
  "sensei:name": "Feature:cintel-object-detection:Service-b9ace8b348b6433e9e7d82371aa16690",
  "sensei:invocation_mode": "asynchronous",
  "sensei:invocation_batch": false,
  "sensei:engines": [
    {
      "sensei:execution_info": {
        "sensei:engine": "Feature:cintel-object-detection:Service-b9ace8b348b6433e9e7d82371aa16690"
      },
      "sensei:inputs": {
        "documents": [
        {
          "repo:path": <IMG_URL_PATH>,
          "sensei:repoType": "HTTP",
          "dc:format": "image/jpg"
        }
        ]
      },
      "sensei:params": {
        "correct_with_dictionary": true
      },
      "sensei:outputs":{
        "result" : {
          "sensei:multipart_field_name" : "result",
          "dc:format": "application/json"
        }
      }
    }
  ]
}'
```

```json
{
  "contentAnalyzerResponse": {
    "statuses": [
      {
        "sensei:engine": "Feature:cintel-object-detection:Service-b9ace8b348b6433e9e7d82371aa16690",
        "invocations": [
          {
            "sensei:outputs": {
              "result": {
                "sensei:multipart_field_name": "result",
                "dc:format": "application/json"
              }
            },
            "message": null,
            "status": "200"
          }
        ]
      }
    ],
    "request_id": "ZbdhcK0JqS4Wg1wGdlEHGR3JOm530YNn"
  },
  "result": [
    {
      "is_text_present": 0,
      "tags": [],
      "request_element_id": 0
    }
  ]
}
```

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| `documents` | Lista de elementos JSON com cada item na lista representando uma imagem. Todos os parâmetros transmitidos como parte dessa lista substituem o parâmetro global especificado fora da lista para o elemento de lista correspondente. | Sim |
| `sensei:multipart_field_name` | field_name do qual ler o caminho do arquivo de entrada. | Sim |
| `repo:path` | URL pré-assinado para ativo de imagem. | Sim |
| `sensei:repoType` | &quot;HTTP&quot; (para url pré-assinado). | Não |
| `dc:format` | Formato codificado da imagem de entrada. Somente formatos de imagem como jpeg, jpg, png e tiff são permitidos para codificação de imagem. O dc:format corresponde aos formatos permitidos. | Não |
| `correct_with_dictionary` | Corrigir as palavras com um dicionário de inglês? Se essa opção não estiver ativada, você poderá ter palavras que não estejam em inglês reconhecidas. O padrão é True: ativado.) Observe que quando o dicionário está ativado, não é necessário que você sempre receba uma palavra em inglês. Tentamos corrigi-la, mas se não for possível em uma certa distância de edição, retornamos a palavra original. | Não |
| `filter_with_dictionary` | Se as palavras devem ser filtradas para conter somente as palavras do dicionário de inglês? Se essa opção estiver ativada, as palavras retornadas sempre pertencerão ao inglês grande , que compreende 470 mil palavras. | Não |
| `min_probability` | Qual é a probabilidade mínima para as palavras reconhecidas? Somente as palavras extraídas da imagem e com uma probabilidade maior que min_probability são retornadas pelo serviço. O valor padrão é definido como 0,2. | Não |
| `min_relevance` | Qual é a relevância mínima para as palavras reconhecidas? Somente as palavras extraídas da imagem e que têm relevância maior que min_importance são retornadas pelo serviço. O valor padrão é definido em 0,01. A relevância é calculada como a fração da área da caixa delimitadora do texto extraído em comparação com a imagem completa. 0,01 seria traduzido como um texto que ocupa pelo menos 1% da imagem. | Não |

| Nome | Tipo de dados | Obrigatório | Padrão | Valores | Descrição |
| -----| --------- | -------- | ------- | ------ | ----------- |
| `repo:path` | string | - | - | - | URL pré-assinado da imagem da qual o texto precisa ser extraído. |
| `sensei:repoType` | string | - | - | HTTPS | Tipo de repositório onde a imagem está sendo armazenada. |
| `sensei:multipart_field_name` | string | - | - | - | Use isso ao passar a imagem como um argumento de várias partes em vez de usar urls pré-assinados. |
| `dc:format` | string | Sim | - | &quot;image/jpg&quot;, <br>&quot;image/jpeg&quot;, <br>&quot;image/png&quot;, <br>&quot;image/tiff&quot; | A codificação de imagem é verificada em relação aos tipos de codificação de entrada permitidos antes de ser processada. |