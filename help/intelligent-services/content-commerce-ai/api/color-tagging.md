---
keywords: Experience Platform;introdução;conteúdo;marcação de conteúdo;marcação de cores;extração de cores;
solution: Experience Platform
title: Marcação de cores na API de marcação de conteúdo
description: O serviço de Marcação de cores, quando recebe uma imagem, pode calcular o histograma de cores de pixels e classificá-las por cores dominantes em compartimentos.
exl-id: 6b3b6314-cb67-404f-888c-4832d041f5ed
source-git-commit: a42bb4af3ec0f752874827c5a9bf70a66beb6d91
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 5%

---

# Marcação de cores

O serviço de marcação de cores, quando recebe uma imagem, pode calcular um histograma de cores de pixels e classificá-las por cores dominantes em compartimentos. As cores nos pixels da imagem são classificadas em 40 cores predominantes, que são representativas do espectro de cores. Um histograma de valores de cor é então calculado entre essas 40 cores. O serviço tem duas variantes:

**Marcação de cores (imagem completa)**

Este método extrai um histograma de cores pela imagem inteira.

**Marcação de cores (com máscara)**

Esse método usa um extrator de primeiro plano baseado em aprendizagem profunda para identificar objetos em primeiro plano. O modelo é treinado em um catálogo de imagens de comércio eletrônico. Depois que o objeto de primeiro plano é extraído, um histograma é calculado sobre as cores dominantes, conforme descrito anteriormente.

A imagem a seguir foi usada no exemplo mostrado neste documento:

![imagem de teste](../images/QQAsset1.jpg)

**Formato da API**

```http
POST /services/v2/predict
```

**Solicitação**

O exemplo de solicitação a seguir usa o método de imagem completa para marcação de cores.

A solicitação a seguir extrai cores de uma imagem com base nos parâmetros de entrada fornecidos na carga. Consulte a tabela abaixo do exemplo de carga para obter mais informações sobre os parâmetros de entrada mostrados.

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v2/predict \
-H 'Prefer: respond-async, wait=59' \
-H "x-api-key: $API_KEY" \
-H "content-type: multipart/form-data" \
-H "authorization: Bearer $API_TOKEN" \
-F 'contentAnalyzerRequests={
  "sensei:name": "Feature:cintel-image-classifier:Service-60887e328ded447d86e01122a4f19c58",
  "sensei:invocation_mode": "synchronous",
  "sensei:invocation_batch": false,
  "sensei:engines": [
    {
      "sensei:execution_info": {
        "sensei:engine": "Feature:cintel-image-classifier:Service-60887e328ded447d86e01122a4f19c58"
      },
      "sensei:inputs": {
        "documents": [{
            "sensei:multipart_field_name": "infile_1",
            "dc:format": "image/jpg"
          }]
      },
      "sensei:params": {
        "application-id": "1234",
        "enable_mask": 0
      },
      "sensei:outputs":{
        "result" : {
          "sensei:multipart_field_name" : "result",
          "dc:format": "application/json"
        }
      }
    }
  ]
}' \
-F 'infile_1=@1431RDMJANELLERAWJACKE_2.jpg'
```

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| `application-id` | A ID do aplicativo criado. | Sim |
| `documents` | Uma lista de elementos JSON com cada item na lista representando um documento. | Sim |
| `top_n` | O número de resultados a serem retornados (não pode ser um número inteiro negativo). Usar o valor `0` para retornar todos os resultados. Quando usado em conjunto com `threshold`, o número de resultados retornados é o menor de ambos os limites definidos. O padrão para essa propriedade é `0`. | Não |
| `min_coverage` | Limite de cobertura acima do qual os resultados precisam ser retornados. Exclua o parâmetro para retornar todos os resultados. | Não |
| `resize_image` | Indica se a imagem de entrada deve ser redimensionada. Por padrão, as imagens são redimensionadas para 320*320 pixels antes da aplicação da marcação de cores. Para fins de depuração, também podemos permitir que o código seja executado na imagem completa, definindo isso como False. | Não |
| `enable_mask` | Ativa/desativa a marcação de cores na máscara. | Não |

| Nome | Tipo de dados | Obrigatório | Padrão | Valores | Descrição |
| -----| --------- | -------- | ------- | ------ | ----------- |
| `repo:path` | string | - | - | - | URL pré-assinado do documento do qual as frases-chave serão extraídas. |
| `sensei:repoType` | string | - | - | HTTPS | Tipo de repositório onde a imagem está sendo armazenada. |
| `sensei:multipart_field_name` | string | - | - | - | Use isso ao transmitir um arquivo de imagem como um argumento de várias partes em vez de usar urls pré-assinados. |
| `dc:format` | string | Sim | - | &quot;image/jpg&quot;, <br> &quot;image/jpeg&quot;, <br>&quot;image/png&quot;, <br>&quot;image/tiff&quot; | A codificação de imagem é verificada em relação aos tipos de codificação de entrada permitidos antes de ser processada. |

**Resposta**

Uma resposta bem-sucedida retorna os detalhes das cores extraídas. Cada cor é representada por um `feature_value` que contém as seguintes informações:

- Um nome de cor
- A porcentagem de exibição dessa cor em relação à imagem
- O valor de RGB da cor

No primeiro objeto de exemplo abaixo, a variável `feature_value` de `Mud_Green,0.069,102,72,95` significa que a cor encontrada é verde-lama, verde-lama é encontrado em 6,9% da imagem, e tem um valor de RGB de 102,72,95.

```json
{
  "status": 200,
  "content_id": "test_image.jpg",
  "cas_responses": [
    {
{
  "statuses": [
    {
      "sensei:engine": "Feature:cintel-image-classifier:Service-60887e328ded447d86e01122a4f19c58",
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
  "request_id": "hsxycVq5Q9KbZ7MWrt6NXcSNWbonSLf3"
}

[
  {
    "request_element_id": "0",
    "colors": {
      "Mud_Green": {
        "coverage": 0.0694,
        "rgb": {
          "red": 102,
          "blue": 72,
          "green": 95
        }
      },
      "Dark_Brown": {
        "coverage": 0.1226,
        "rgb": {
          "red": 113,
          "blue": 77,
          "green": 84
        }
      },
      "Pink": {
        "coverage": 0.0731,
        "rgb": {
          "red": 234,
          "blue": 201,
          "green": 209
        }
      },
      "Dark_Gray": {
        "coverage": 0.1533,
        "rgb": {
          "red": 63,
          "blue": 58,
          "green": 59
        }
      },
      "Olive": {
        "coverage": 0.492,
        "rgb": {
          "red": 177,
          "blue": 126,
          "green": 170
        }
      },
      "Brown": {
        "coverage": 0.0896,
        "rgb": {
          "red": 141,
          "blue": 85,
          "green": 105
        }
      }
    }
  }
]
}
```
