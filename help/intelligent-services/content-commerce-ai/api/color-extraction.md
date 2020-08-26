---
keywords: Experience Platform;getting started;content ai;commerce ai;content and commerce ai;color extraction;Color extraction
solution: Experience Platform
title: Extração de cores
topic: Developer guide
description: O serviço de extração de cores, quando recebe uma imagem, pode calcular o histograma das cores dos pixels e classificá-las por cores dominantes em compartimentos.
translation-type: tm+mt
source-git-commit: 690ddbd92f0a2e4e06b988e761dabff399cd2367
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 2%

---


# Extração de cores

>[!NOTE]
>
>[!DNL Content and Commerce AI] está em beta. A documentação está sujeita a alterações.

O serviço de extração de cores, quando recebe uma imagem, pode computar um histograma de cores de pixel e classificá-las por cores dominantes em compartimentos. As cores nos pixels da imagem são divididas em 40 cores predominantes que são representativas do espectro de cores. Um histograma de valores de cor é então calculado entre essas 40 cores. O serviço tem duas variantes:

**Extração colorida (imagem completa)**

Este método extrai um histograma de cores na imagem inteira.

**Extração colorida (com máscara)**

Este método usa um extrator de primeiro plano baseado em aprendizado profundo para identificar objetos em primeiro plano. O modelo é treinado em um catálogo de imagens de comércio eletrônico. Depois que o objeto de primeiro plano é extraído, um histograma é calculado sobre as cores dominantes, conforme descrito anteriormente.

A imagem a seguir foi usada no exemplo mostrado neste documento:

![imagem de teste](../images/QQAsset1.jpg)

**Formato da API**

```http
POST /services/v1/predict
```

**Solicitação**

A solicitação de exemplo a seguir usa o método de imagem completa para a extração de cores.

A solicitação a seguir extrai cores de uma imagem com base nos parâmetros de entrada fornecidos na carga. Consulte a tabela abaixo do exemplo de carga para obter mais informações sobre os parâmetros de entrada mostrados.

>[!CAUTION]
>
>`analyzer_id` determina qual [!DNL Sensei Content Framework] é usado. Verifique se você tem o direito `analyzer_id` antes de fazer sua solicitação. Para o serviço de extração de cores, a `analyzer_id` ID é:
>`Feature:image-color-histogram:Service-6fe52999293e483b8e4ae9a95f1b81a7`

```SHELL
curl -i -X POST https://sensei.adobe.io/services/v1/predict \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: multipart/form-data' \
  -H 'x-api-key: {API_KEY}' \
  -H 'cache-control: no-cache,no-cache' \
  -F file=@test_image.jpg \
  -F 'contentAnalyzerRequests={
   "enable_diagnostics":"true",
   "requests":[
     {
         "analyzer_id": "Feature:image-color-histogram:Service-6fe52999293e483b8e4ae9a95f1b81a7",
         "parameters": {
          "application-id": "1234", 
          "content-type": "inline", 
          "encoding": "jpeg", 
          "threshold": "0", 
          "top-N": "0", 
          "custom": {}, 
          "data": [{
            "content-id": "0987", 
            "content": "inline-image", 
            "content-type": "inline", 
            "encoding": "jpeg", 
            "threshold": "0", 
            "top-N": "0", 
            "historic-metadata": [], 
            "custom": {"exclude_mask": 1}
            }]
          }
      }
    ]
}'
```

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| `analyzer_id` | A ID de [!DNL Sensei] serviço em que sua solicitação é implantada. Essa ID determina qual dos [!DNL Sensei Content Frameworks] é usada. Para serviços personalizados, entre em contato com a equipe do AI de Conteúdo e Comércio para configurar uma ID personalizada. | Sim |
| `application-id` | A ID do aplicativo criado. | Sim |
| `data` | Uma matriz que contém objetos JSON. Cada objeto na matriz representa uma imagem. Todos os parâmetros transmitidos como parte dessa matriz substituem os parâmetros globais especificados fora da `data` matriz. Qualquer uma das propriedades restantes descritas abaixo nesta tabela pode ser substituída de dentro `data`. | Sim |
| `content-id` | A ID exclusiva do elemento de dados retornado na resposta. Se isso não for passado, uma ID gerada automaticamente será atribuída. | Não |
| `content` | O conteúdo a ser analisado pelo serviço de extração de cores. No evento de que a imagem faça parte do corpo da solicitação, use `-F file=@<filename>` o comando curl para passar a imagem, deixando esse parâmetro como uma string vazia. <br> Se a imagem for um arquivo no S3, passe o url assinado. Quando o conteúdo faz parte do corpo da solicitação, a lista de elementos de dados deve ter apenas um objeto. Se mais de um objeto for transmitido, somente o primeiro objeto será processado. | Sim |
| `content-type` | Usado para indicar se a entrada é parte do corpo da solicitação ou um url assinado para um bucket S3. O padrão para essa propriedade é `inline`. | Não |
| `encoding` | O formato de arquivo da imagem de entrada. Atualmente, somente imagens JPEG e PNG podem ser processadas. O padrão para essa propriedade é `jpeg`. | Não |
| `threshold` | O limite de pontuação (0 a 1) acima do qual os resultados precisam ser retornados. Use o valor `0` para retornar todos os resultados. O padrão para essa propriedade é `0`. | Não |
| `top-N` | O número de resultados a serem retornados (não pode ser um número inteiro negativo). Use o valor `0` para retornar todos os resultados. Quando usado em conjunto com `threshold`, o número de resultados retornados é o menor dos dois limites definidos. O padrão para essa propriedade é `0`. | Não |
| `custom` | Quaisquer parâmetros personalizados a serem transmitidos. | Não |
| `historic-metadata` | Uma matriz que pode ser passada para metadados. | Não |

**Resposta**

Uma resposta bem-sucedida retorna os detalhes das cores extraídas. Cada cor é representada por uma `feature_value` chave, que contém as seguintes informações:

- Um nome de cor
- A porcentagem que essa cor aparece em relação à imagem
- O valor RGB da cor

No primeiro objeto de exemplo abaixo, a cor `feature_value` de `White,0.59,251,251,243` fundo significa que a cor encontrada é branca, branca é encontrada em 59% da imagem e tem um valor RGB de 251.251.243.

```json
{
  "status": 200,
  "content_id": "test_image.jpg",
  "cas_responses": [
    {
      "status": 200,
      "analyzer_id": "Feature:image-color-histogram:Service-e952f4acd7c2425199b476a2eb459635",
      "content_id": "test_image.jpg",
      "result": {
        "response_type": "feature",
        "response": [
          {
            "feature_value": [
              {
                "feature_name": "color_name_and_rgb",
                "feature_value": "White,0.59,251,251,243"
              },
              {
                "feature_value": "Orange,0.30,248,169,48",
                "feature_name": "color_name_and_rgb"
              },
              {
                "feature_name": "color_name_and_rgb",
                "feature_value": "Mustard,0.08,251,199,77"
              },
              {
                "feature_name": "color_name_and_rgb",
                "feature_value": "Gold,0.02,250,191,55"
              }
            ],
            "feature_name": "color"
          }
        ]
      }
    }
  ],
  "error": []
}
```

| Propriedade | Descrição |
| --- | --- |
| `content_id` | O nome da imagem que foi carregada na solicitação de POST. |
| `feature_value` | Uma matriz cujos objetos contêm chaves com o mesmo nome de propriedade. Essas teclas contêm uma string que representa o nome da cor, uma porcentagem que essa cor aparece em relação à imagem enviada na cor `content_id`e o valor RGB da cor. |
