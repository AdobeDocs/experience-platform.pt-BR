---
keywords: Experience Platform;introdução;conteúdo;marcação de conteúdo;marcação de cores;extração de cores;
solution: Experience Platform
title: Marcação de cores na API de marcação de conteúdo
description: O serviço de Marcação de cores, quando recebe uma imagem, pode calcular o histograma de cores de pixels e classificá-las por cores dominantes em compartimentos.
exl-id: 6b3b6314-cb67-404f-888c-4832d041f5ed
source-git-commit: fd8891bdc7d528e327d2a72c2427f7bbc6dc8a03
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 6%

---

# Marcação de cores

O serviço de marcação de cores, quando recebe uma imagem, pode calcular um histograma de cores de pixels e classificá-las por cores dominantes em compartimentos. As cores nos pixels da imagem são classificadas em 40 cores predominantes, que são representativas do espectro de cores. Um histograma de valores de cor é então calculado entre essas 40 cores. O serviço tem duas variantes:

**Marcação de cores (imagem completa)**

Este método extrai um histograma de cores pela imagem inteira.

**Marcação de cores (com máscara)**

Esse método usa um extrator de primeiro plano baseado em aprendizagem profunda para identificar objetos em primeiro plano. Depois que os objetos de primeiro plano são extraídos, um histograma é calculado sobre as cores dominantes para as regiões de primeiro plano e plano de fundo, juntamente com a imagem inteira.

**Extração de tom**

Além das variantes mencionadas acima, você pode configurar o serviço para recuperar um histograma de tons para:

- A imagem geral (ao usar a variante de imagem completa)
- A imagem geral e as regiões de primeiro e segundo plano (ao usar a variante com mascaramento)

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

Uma resposta bem-sucedida retorna os detalhes das cores extraídas. Cada cor é representada por um `feature_value` que contém as seguintes informações:

- Um nome de cor
- A porcentagem de exibição dessa cor em relação à imagem
- O valor de RGB da cor

`"White":{"coverage":0.5834,"rgb":{"red":254,"green":254,"blue":243}}`significa que a cor encontrada é branca, encontrada em 58,34% da imagem, e tem um valor médio de RGB de 254, 254, 243.

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

Observe que o resultado aqui tem cores extraídas na região de imagem &quot;geral&quot;.

**Solicitação - variante de imagem mascarada**

O exemplo de solicitação a seguir usa o método de mascaramento para a marcação de cores. Isso é ativado ao configurar o `enable_mask` parâmetro para `true` na solicitação.

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

>[!NOTE]
>
>Além disso, a `retrieve_tone` também está definido como `true` no pedido acima. Isso nos permite recuperar um histograma de distribuição de tons quentes, neutros e frios nas regiões geral, de primeiro plano e plano de fundo da imagem.

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

Além das cores da imagem geral, agora também é possível ver as cores das regiões do primeiro plano e do plano de fundo. Como a recuperação de tons está habilitada para cada uma das regiões acima, você também pode recuperar o histograma de tons.

**Parâmetros de entrada**

| Nome | Tipo de dados | Obrigatório | Padrão | Valores | Descrição |
| --- | --- | --- | --- | --- | --- |
| `documents` | matriz (Document-Object) | Sim | - | Consulte abaixo | Lista de elementos JSON com cada item na lista representando um documento. |
| `top_n` | number | Não | 0 | Inteiro não negativo | Número de resultados a serem retornados. 0, para retornar todos os resultados. Quando usado em conjunto com o limite, o número de resultados retornados será menor de ambos os limites. |
| `min_coverage` | number | Não | 0.05 | Número real | Limite de cobertura acima do qual os resultados precisam ser retornados. Excluir parâmetro para retornar todos os resultados. |
| `resize_image` | number | Não | Verdadeiro | Verdadeiro/falso | Se a imagem de entrada deve ser redimensionada ou não. Por padrão, as imagens são redimensionadas para 320*320 pixels antes da extração de cores. Para fins de depuração, também podemos permitir que o código seja executado na imagem completa, definindo isso como `False`. |
| `enable_mask` | number | Não | Falso | Verdadeiro/falso | Ativa/desativa a extração de cores |
| `retrieve_tone` | number | Não | Falso | Verdadeiro/falso | Ativa/desativa a extração de tons |

**Objeto do documento**

| Nome | Tipo de dados | Obrigatório | Padrão | Valores | Descrição |
| -----| --------- | -------- | ------- | ------ | ----------- |
| `repo:path` | string | - | - | - | URL pré-assinado do documento. |
| `sensei:repoType` | string | - | - | HTTPS | Tipo de repositório onde a imagem está sendo armazenada. |
| `sensei:multipart_field_name` | string | - | - | - | Use isso ao passar o arquivo de imagem como um argumento em várias partes, em vez de usar URLs pré-assinados. |
| `dc:format` | string | Sim | - | &quot;image/jpg&quot;,<br>&quot;image/jpeg&quot;,<br>&quot;image/png&quot;,<br>&quot;image/tiff&quot; | A codificação de imagem é verificada em relação aos tipos de codificação de entrada permitidos antes de ser processada. |