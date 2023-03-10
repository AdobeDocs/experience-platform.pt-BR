---
keywords: Semelhança visual;similaridade visual;api ccai
solution: Experience Platform
title: Semelhança visual na API da IA de conteúdo e comércio
description: O serviço de semelhança visual, quando recebe uma imagem, encontra automaticamente imagens visualmente semelhantes de um catálogo.
exl-id: fe31d9be-ee42-44fa-b83f-3b8a718cb4e3
source-git-commit: b124ed97da8bde2a7fc4f10d350c81a47e096f29
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 3%

---

# Semelhança visual

>[!NOTE]
>
>[!DNL Content and Commerce AI] O está na versão beta. A documentação está sujeita a alterações.

O serviço de semelhança visual, quando recebe uma imagem, encontra automaticamente imagens visualmente semelhantes de um catálogo.

A imagem a seguir foi usada no exemplo de solicitação mostrado neste documento:

![imagem de teste](../images/Query_Image.jpeg)

**Formato da API**

```http
POST /services/v1/predict
```

**Solicitação**

A solicitação a seguir recupera imagens visualmente semelhantes de um catálogo, com base nos parâmetros de entrada fornecidos na carga. Consulte a tabela abaixo do exemplo de carga para obter mais informações sobre os parâmetros de entrada mostrados.

>[!CAUTION]
>
>`analyzer_id` determina qual [!DNL Sensei Content Framework] é usada. Verifique se você tem o `analyzer_id` antes de fazer o seu pedido. Entre em contato com a equipe beta da IA de conteúdo e comércio para receber seu `analyzer_id` para este serviço.

```SHELL
curl -i -X POST https://sensei.adobe.io/services/v1/predict \
  -H 'Authorization: Bearer $API_TOKEN' \
  -H 'Content-Type: multipart/form-data' \
  -H 'cache-control: no-cache,no-cache' \
  -H 'x-api-key: $API_KEY' \
  -F file=@test_image.jpg \
  -F 'contentAnalyzerRequests={
   "enable_diagnostics":"true",
   "requests":[
     {
         "analyzer_id": "Feature:cintel-deep-product-search:Service-316a8cf750c6440396061c8f73a7a585",
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
            "custom": {}
            }]
          }
      }
    ]
}'
```

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| `analyzer_id` | A variável [!DNL Sensei] ID do serviço em que sua solicitação foi implantada. Essa ID determina qual das opções [!DNL Sensei Content Frameworks] são usados. Para obter serviços personalizados, entre em contato com a equipe da IA de conteúdo e comércio para configurar uma ID personalizada. | Sim |
| `application-id` | A ID do aplicativo criado. | Sim |
| `data` | Uma matriz que contém um objeto JSON com cada objeto na matriz representando uma imagem. Quaisquer parâmetros transmitidos como parte dessa matriz substituem os parâmetros globais especificados fora do `data` matriz. Qualquer uma das propriedades restantes descritas abaixo nesta tabela pode ser substituída de dentro de `data`. | Sim |
| `content-id` | A ID exclusiva do elemento de dados retornado na resposta. Se isso não for transmitido, uma ID gerada automaticamente será atribuída. | Não |
| `content` | O conteúdo a ser analisado pelo serviço de similaridade visual. Caso a imagem faça parte do corpo da solicitação, use `-F file=@<filename>` no comando curl para transmitir a imagem, deixando esse parâmetro como uma string vazia. <br> Se a imagem for um arquivo no S3, passe o url assinado. Quando o conteúdo faz parte do corpo da solicitação, a lista de elementos de dados deve ter apenas um objeto. Se mais de um objeto for transmitido, somente o primeiro será processado. | Sim |
| `content-type` | Usado para indicar se a entrada faz parte do corpo da solicitação ou de um url assinado para um bucket do S3. O padrão para essa propriedade é `inline`. | Não |
| `encoding` | O formato de arquivo da imagem de entrada. Atualmente, somente imagens JPEG e PNG podem ser processadas. O padrão para essa propriedade é `jpeg`. | Não |
| `threshold` | O limite de pontuação (0 a 1) acima do qual os resultados precisam ser retornados. Usar o valor `0` para retornar todos os resultados. O padrão para essa propriedade é `0`. | Não |
| `top-N` | O número de resultados a serem retornados (não pode ser um número inteiro negativo). Usar o valor `0` para retornar todos os resultados. Quando usado em conjunto com `threshold`, o número de resultados retornados é o menor de ambos os limites definidos. O padrão para essa propriedade é `0`. | Não |
| `custom` | Quaisquer parâmetros personalizados a serem transmitidos. | Não |
| `historic-metadata` | Uma matriz que pode receber metadados. | Não |

**Resposta**

Uma resposta bem-sucedida retorna uma `response` matriz que contém um `feature_value` e `feature_name` para cada imagem visualmente semelhante encontrada no catálogo.

As imagens visualmente semelhantes a seguir foram retornadas na resposta de exemplo mostrada abaixo:

![imagens semelhantes](../images/results.jpg)

```json
{
  "status": 200,
  "content_id": "test_image.jpg",
  "cas_responses": [
    {
      "status": 200,
      "analyzer_id": "Feature:cintel-deep-product-search:Service-316a8cf750c6440396061c8f73a7a585",
      "content_id": "test_image.jpg",
      "result": {
        "response_type": "feature",
        "response": [
          {
            "feature_value": [
              {
                "feature_value": "678",
                "feature_name": "G34WS945.F1"
              },
              {
                "feature_value": "678",
                "feature_name": "1431RDM JANELLE RAW JACKE"
              },
              {
                "feature_value": "657",
                "feature_name": "GF4045877841 CARLA FLR"
              },
              {
                "feature_name": "1707-686-SGU PATCH XYZ",
                "feature_value": "657"
              },
              {
                "feature_name": "5495MJT AJA BLK",
                "feature_value": "646"
              },
              {
                "feature_name": "IDEAL",
                "feature_value": "645"
              },
              {
                "feature_value": "644",
                "feature_name": "HCAJRA439 CALI JEAN"
              },
              {
                "feature_name": "KT279RK-ONL",
                "feature_value": "644"
              },
              {
                "feature_name": "SP190404-ELLIS",
                "feature_value": "642"
              },
              {
                "feature_name": "GF4174848718 KENDALL DIS",
                "feature_value": "640"
              }
            ],
            "feature_name": "visual_similarity"
          }
        ]
      }
    }
  ],
  "error": []
}
```
