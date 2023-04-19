---
keywords: Experience Platform; introdução; conteúdo; marcação de conteúdo; marcação de cores; extração de cores;
solution: Experience Platform
title: Marcação de cores na API de marcação de conteúdo
description: O serviço de Marcação de cores, quando recebe uma imagem, pode calcular o histograma de cores de pixels e classificá-las por cores dominantes em compartimentos.
exl-id: 6b3b6314-cb67-404f-888c-4832d041f5ed
source-git-commit: e6ea347252b898f73c2bc495b0324361ee6cae9b
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 5%

---

# Marcação de cores

O serviço de marcação de cores, quando recebe uma imagem, pode computar um histograma de cores de pixels e classificá-las por cores dominantes em compartimentos. As cores nos pixels da imagem são agrupadas em 40 cores predominantes que são representativas do espectro de cores. Um histograma de valores de cor é então calculado entre essas 40 cores. O serviço tem duas variantes:

**Marcação de cores (imagem completa)**

Esse método extrai um histograma de cores na imagem inteira.

**Marcação de cores (com máscara)**

Esse método usa um extrator de primeiro plano baseado em aprendizado profundo para identificar objetos em primeiro plano. Uma vez extraídos os objetos em primeiro plano, um histograma é calculado sobre as cores dominantes das regiões em primeiro e segundo plano, juntamente com toda a imagem.

**Extração de tons**

Além das variantes mencionadas acima, é possível configurar o serviço para recuperar um histograma de tons para:

- A imagem geral (ao usar a variante de imagem completa)
- A imagem geral e as regiões de primeiro e segundo plano (ao usar a variante com máscara)

A imagem a seguir foi usada no exemplo mostrado neste documento:

![imagem de teste](../images/QQAsset1.jpg)

**Formato da API**

```http
POST /services/v2/predict
```

**Solicitação - variante de imagem completa**

A solicitação de exemplo a seguir usa o método de imagem completa para marcação de cores e extrai cores de uma imagem com base nos parâmetros de entrada fornecidos na carga útil. Consulte a tabela abaixo do exemplo de carga para obter mais informações sobre os parâmetros de entrada mostrados.

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v2/predict \
-H 'Prefer: respond-async, wait=59' \
-H "x-api-key: $API_KEY" \
-H "content-type: multipart/form-data" \
-H "authorization: Bearer $API_TOKEN" \
-F 'contentAnalyzerRequests={
  "sensei:name": "Feature:autocrop:Service-af865523d46547e2b17fdf9b38e32a72",
  "sensei:invocation_mode": "synchronous",
  "sensei:invocation_batch": false,
  "sensei:engines": [
    {
      "sensei:execution_info": {
        "sensei:engine": "Feature:autocrop:Service-af865523d46547e2b17fdf9b38e32a72"
      },
      "sensei:inputs": {
        "documents": [{
            "sensei:multipart_field_name": "infile_1",
            "dc:format": "image/jpg"
          }]
      },
      "sensei:params": {
        "top_n": 5,
        "min_coverage": 0.005      
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

**Resposta - variante de imagem completa**

Uma resposta bem-sucedida retorna os detalhes das cores extraídas. Cada cor é representada por um `feature_value` , que contém as seguintes informações:

- Um nome de cor
- A porcentagem que essa cor aparece em relação à imagem
- O valor de RGB da cor

`"White":{"coverage":0.5834,"rgb":{"red":254,"green":254,"blue":243}}`significa que a cor encontrada é branca, que se encontra em 58,34% da imagem, e tem um valor RGB médio de 254, 254, 243.

```json
{
    "statuses": [{
        "sensei:engine": "Feature:autocrop:Service-af865523d46547e2b17fdf9b38e32a72",
        "invocations": [{
            "sensei:outputs": {
                "result": {
                    "sensei:multipart_field_name": "result",
                    "dc:format": "application/json"
                }
            },
            "message": null,
            "status": "200"
        }]
    }],
    "request_id": "bfpzaJxKDxtgxpjUj5QDrN1jasjUw2RM"
}  
 
[{
    "overall": {
        "colors": {
            "White": {
                "coverage": 0.5834,
                "rgb": {
                    "red": 254,
                    "green": 254,
                    "blue": 243
                }
            },
            "Orange": {
                "coverage": 0.254,
                "rgb": {
                    "red": 249,
                    "green": 165,
                    "blue": 45
                }
            },
            "Gold": {
                "coverage": 0.0817,
                "rgb": {
                    "red": 253,
                    "green": 188,
                    "blue": 58
                }
            },
            "Mustard": {
                "coverage": 0.0727,
                "rgb": {
                    "red": 253,
                    "green": 207,
                    "blue": 84
                }
            },
            "Cream": {
                "coverage": 0.0082,
                "rgb": {
                    "red": 253,
                    "green": 236,
                    "blue": 174
                }
            }
        }
    }
}]
```

Observe que o resultado aqui tem cor extraída na região da imagem &quot;geral&quot;.

**Solicitação - variante de imagem mascarada**

A solicitação de exemplo a seguir usa o método de mascaramento para marcação de cores. Habilitamos isso definindo a variável `enable_mask` para `true` na solicitação.

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v2/predict \
-H 'Prefer: respond-async, wait=59' \
-H "x-api-key: $API_KEY" \
-H "content-type: multipart/form-data" \
-H "authorization: Bearer $API_TOKEN" \
-F 'contentAnalyzerRequests={
  "sensei:name": "Feature:autocrop:Service-af865523d46547e2b17fdf9b38e32a72",
  "sensei:invocation_mode": "synchronous",
  "sensei:invocation_batch": false,
  "sensei:engines": [
    {
      "sensei:execution_info": {
        "sensei:engine": "Feature:autocrop:Service-af865523d46547e2b17fdf9b38e32a72"
      },
      "sensei:inputs": {
        "documents": [{
            "sensei:multipart_field_name": "infile_1",
            "dc:format": "image/jpg"
          }]
      },
      "sensei:params": {
        "top_n": 5,
        "min_coverage": 0.005,
        "enable_mask": true,
        "retrieve_tone": true     
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

>Observação: Além disso, também definimos a variável `retrieve_tone` para `true` no pedido acima referido. Isso nos permite recuperar um histograma de distribuição de tons sobre tons quentes, neutros e frios nas regiões geral, de primeiro e de plano de fundo da imagem.

**Resposta - variante de imagem mascarada**

```json
{
    "statuses": [{
        "sensei:engine": "Feature:autocrop:Service-af865523d46547e2b17fdf9b38e32a72",
        "invocations": [{
            "sensei:outputs": {
                "result": {
                    "sensei:multipart_field_name": "result",
                    "dc:format": "application/json"
                }
            },
            "message": null,
            "status": "200"
        }]
    }],
    "request_id": "gpeCyJsrJvOWd94WwZOyPBPrKi2BQyla"
}  
 
 
[{
    "overall": {
        "colors": {
            "White": {
                "coverage": 0.5834,
                "rgb": {
                    "red": 254,
                    "green": 254,
                    "blue": 243
                }
            },
            "Orange": {
                "coverage": 0.254,
                "rgb": {
                    "red": 249,
                    "green": 165,
                    "blue": 45
                }
            },
            "Gold": {
                "coverage": 0.0817,
                "rgb": {
                    "red": 253,
                    "green": 188,
                    "blue": 58
                }
            },
            "Mustard": {
                "coverage": 0.0727,
                "rgb": {
                    "red": 253,
                    "green": 207,
                    "blue": 84
                }
            },
            "Cream": {
                "coverage": 0.0082,
                "rgb": {
                    "red": 253,
                    "green": 236,
                    "blue": 174
                }
            }
        },
        "tones": {
            "warm": 0.4084,
            "neutral": 0.5916,
            "cool": 0
        }
    },
    "foreground": {
        "colors": {
            "Orange": {
                "coverage": 0.6022,
                "rgb": {
                    "red": 249,
                    "green": 165,
                    "blue": 45
                }
            },
            "Gold": {
                "coverage": 0.1935,
                "rgb": {
                    "red": 253,
                    "green": 188,
                    "blue": 58
                }
            },
            "Mustard": {
                "coverage": 0.1722,
                "rgb": {
                    "red": 253,
                    "green": 207,
                    "blue": 84
                }
            },
            "Cream": {
                "coverage": 0.0173,
                "rgb": {
                    "red": 253,
                    "green": 235,
                    "blue": 170
                }
            },
            "Yellow": {
                "coverage": 0.0148,
                "rgb": {
                    "red": 254,
                    "green": 229,
                    "blue": 117
                }
            }
        },
        "tones": {
            "warm": 0.9827,
            "neutral": 0.0173,
            "cool": 0
        }
    },
    "background": {
        "colors": {
            "White": {
                "coverage": 0.9923,
                "rgb": {
                    "red": 254,
                    "green": 254,
                    "blue": 243
                }
            },
            "Dark_Brown": {
                "coverage": 0.0077,
                "rgb": {
                    "red": 83,
                    "green": 68,
                    "blue": 57
                }
            }
        },
        "tones": {
            "warm": 0,
            "neutral": 1.0,
            "cool": 0
        }
    }
}]
```

Além das cores da imagem geral, você também pode ver as cores das regiões de primeiro e segundo plano agora. Como habilitamos a recuperação de tons para cada uma das regiões acima, também podemos recuperar um histograma de tons.

**Parâmetros de entrada**

| Nome | Tipo de dados | Obrigatório | Padrão | Valores | Descrição |
| --- | --- | --- | --- | --- | --- |
| `documents` | array (Document-Object) | Sim | - | Consulte abaixo | Lista de elementos json com cada item na lista representando um documento. |
| `top_n` | number | Não | 0 | Número inteiro não negativo | Número de resultados a serem retornados. 0, para retornar todos os resultados. Quando usado em conjunto com o limite, o número de resultados retornados será menor de qualquer um dos limites. |
| `min_coverage` | number | Não | 0.05 | Número real | Limite de cobertura acima do qual os resultados devem ser devolvidos. Excluir parâmetro para retornar todos os resultados. |
| `resize_image` | number | Não | Verdadeiro | Verdadeiro/Falso | Redimensionar ou não a imagem de entrada. Por padrão, as imagens são redimensionadas para 320*320 pixels antes da extração de cores ser executada. Para fins de depuração, também podemos permitir que o código seja executado em imagens completas, definindo isso como Falso. |
| `enable_mask` | number | Não | Falso | Verdadeiro/Falso | Ativa/desativa a extração de cores |
| `retrieve_tone` | number | Não | Falso | Verdadeiro/Falso | Ativa/desativa a extração de tons |

**Objeto Documento**

| Nome | Tipo de dados | Obrigatório | Padrão | Valores | Descrição |
| -----| --------- | -------- | ------- | ------ | ----------- |
| `repo:path` | string | - | - | - | Url pré-assinado do documento a partir do qual as frases-chave devem ser extraídas. |
| `sensei:repoType` | string | - | - | HTTPS | Tipo de acordo de recompra onde o documento está sendo armazenado. |
| `sensei:multipart_field_name` | string | - | - | - | Use isso ao passar o documento como um argumento multiparte, em vez de usar urls pré-assinados. |
| `dc:format` | string | Sim | - | &quot;text/plain&quot;,<br>&quot;application/pdf&quot;,<br>&quot;text/pdf&quot;,<br>&quot;text/html&quot;,<br>&quot;text/rtf&quot;,<br>&quot;application/rtf&quot;,<br>&quot;application/msword&quot;,<br>&quot;application/vnd.openxmlformats-officedocument.wordprocessingml.document&quot;,<br>&quot;application/mspowerpoint&quot;,<br>&quot;application/vnd.ms-powerpoint&quot;,<br>&quot;application/vnd.openxmlformats-officedocument.presentationml.presentation&quot; | A codificação de documento é verificada em relação aos tipos de codificação de entrada permitidos antes de ser processada. |